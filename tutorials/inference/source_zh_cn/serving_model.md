# 通过配置模型提供Servable

`Linux` `Ascend` `Serving` `初级` `中级` `高级`

<!-- TOC -->

- [通过配置模型提供Servable](#通过配置模型提供servable)
    - [概述](#概述)
    - [相关概念](#相关概念)
        - [预处理和后处理](#预处理和后处理)
        - [方法](#方法)
        - [实例](#实例)
    - [模型配置](#模型配置)
        - [预处理和后处理定义](#预处理和后处理定义)
        - [模型声明](#模型声明)
        - [方法定义](#方法定义)

<!-- /TOC -->

<a href="https://gitee.com/mindspore/docs/tree/master/tutorials/inference/source_zh_cn/serving_model.md" target="_blank"><img src="_static/logo_source.png"></a>

## 概述

MindSpore Serving当前仅支持Ascend 310和Ascend 910环境。

MindSpore Serving的Servable提供推理服务，包含两种类型。一种是推理服务来源于单模型，一种是推理服务来源于多模型组合，多模型组合正在开发中。

本文将说明如何对单模型进行配置以提供Servable，以下所有Servable配置说明针对的是单模型Servable，Serving客户端简称客户端。

本文以ResNet-50作为样例介绍如何配置模型提供Servable。样例代码可参考[ResNet-50样例](https://gitee.com/mindspore/serving/blob/master/example/resnet/) 。

## 相关概念

### 预处理和后处理

模型提供推理能力，模型的每个输入和输出的数据类型、数据长度、Shape是固定的。

如果客户端发来的数据不能直接满足模型输入要求，需要通过预处理转化为满足模型输入的数据。
如果模型的输出不直接提供给客户端，需要通过后处理转化为所需的输出数据。

以下图是`resnet50` Servable数据流程图，描述了图像数据从Serving客户端通过网络传输到Serving，Serving进行预处理、推理和后处理，最后向Serving客户端返回结果：

![image](images/resnet_example.png)

针对Resnet50推理模型，客户端发来的数据为jpg、png等格式的图片，预期返回图片的分类。Resnet模型输入为经过图片`Decode`、`Resize`、`Normalize`等操作产生的Tensor，输出为每个类别的得分Tensor。需要通过预处理将图片转化为满足模型输入的Tensor，通过后处理返回**得分最大的类别名称**或者**前5类别名称及其得分**。

在不同的场景下，如果来自客户端的数据输入组成、结构或类型不同，可以提供不同的预处理。如果对模型的输出也有不同的要求，可以提供不同的后处理。比如上述`resnet50` Servable，针对返回**得分最大的类别名称**还是**前5类别名称及其得分**这两种场景提供了两个后处理。

### 方法

上述的`resnet` Servable提供了`classify_top5`和`classify_top1`两个方法（`Method`）。`classify_top5`输入为`image`，输出为`label`和`score`，返回前5的分类名称和得分。`classify_top1`预处理和`classify_top5`一致，而后处理不同，输入为`image`，输出为`label`，返回最大得分的分类名称。

一个Servable可提供一个或多个方法，Servable的名称和方法的名称标记了Serving提供的一个服务，每个方法对客户端提供的数据进行可选的预处理，接着进行模型推理，对模型的推理结果进行可选的后处理，最后将需要的结果返回给客户端。

Servable包含如下内容：

- 指定可选的预处理和可选的后处理；
- 定义方法输入、预处理、模型、后处理、方法输出之间的数据流，前者可作为后者的输入。比如方法输出的值可来源于方法输入、预处理、模型或后处理；
- 指定方法名，使客户端可以通过方法名指定使用的方法；
- 指定方法的输入和输出名称，使客户端可以通过名称来指定输入、获取输出。

### 实例

每次请求可包括一个或多个实例，每个实例之间相互独立，结果互不影响。比如一张图片返回一个分类类别，三张独立的图片独立返回三个分类类别。

## 模型配置

以Resnet50模型为例，模型配置文件目录结果如下图所示：

```shell
resnet50
├── 1
│   └── resnet_classify.mindir
├── 2
│   └── resnet_classify.mindir
└── servable_config.py
```

- 目录`resnet50`指示Servable的名称。

- 通过`servable_config.py`配置Servable，其中包括预处理和后处理定义、模型声明、方法定义。

- 目录`1`和`2`表示版本`1`和版本`2`的模型，模型版本为正整数，从`1`开始，数字越大表示版本越新。

- `resnet_classify.mindir`为模型文件，Servable启动会加载对应版本的模型文件。

### 预处理和后处理定义

预处理和后处理定义方式例子如下：

```python
import mindspore.dataset as ds
import mindspore.dataset.transforms.c_transforms as TC
import mindspore.dataset.vision.c_transforms as VC

# preprocess, using MindData Eager
def preprocess_eager(instances):
    """
    Define preprocess pipeline, the function arg is multi instances, every instance is tuple of inputs.
    this example has one input and one output.
    Use MindData Eager.
    """
    image_size = 224
    mean = [0.485 * 255, 0.456 * 255, 0.406 * 255]
    std = [0.229 * 255, 0.224 * 255, 0.225 * 255]

    decode = VC.Decode()
    resize = VC.Resize([image_size,image_size])
    normalize = VC.Normalize(mean=mean, std=std)
    hwc2chw = VC.HWC2CHW()

    for instance in instances:
        image = instance[0]
        image = decode(image)
        image = resize(image)
        image = normalize(image)
        image = hwc2chw(image)
        yield (image,)

# postprocess of top1
def postprocess_top1(instances):
    """
    Define postprocess pipeline, the function arg is multi instances, every instance is tuple of inputs
    This example has one input and one output
    """
    for instance in instances:
        score = instance[0] # get input 0
        max_idx = np.argmax(score)
        yield idx_2_label[max_idx]

# postprocess of top5
def postprocess_top5(instances):
    """
    Define postprocess pipeline, the function arg is multi instances, every instance is tuple of inputs
    This example has one input and two output
    """
    for instance in instances:
        score = instance[0] # get input 0
        idx = np.argsort(score)[::-1][:5] # top 5
        ret_label = [idx_2_label[i] for i in idx]
        ret_score = score[idx]
        yield ";".join(ret_label), ret_score
```

预处理和后处理定义格式相同，入参为实例数据组成的tuple，每个实例数据为输入数据组成的tuple，每个输入数据为**numpy对象**，通过`yield`返回实例的处理结果，`yield`返回的数据类型可为**numpy对象、Python的bool、int、float、str、bytes**组成的tuple。

预处理和后处理输入的来源和输出的使用由[方法定义](https://www.mindspore.cn/tutorial/inference/zh-CN/master/serving_model.html#id9)决定。

### 模型声明

`resnet50` Servabale模型声明示例代码如下所示：

```python
from mindspore_serving.worker import register
register.declare_servable(servable_file="resnet50_1b_imagenet.mindir", model_format="MindIR", with_batch_dim=True)
```

其中`declare_servable`入参`servable_file`指示模型的文件名称；`model_format`指示模型的模型类别，当前Ascend310环境支持`OM`和`MindIR`两种模型类型，Ascend910环境仅支持`MindIR`模型类型。

如果模型输入和输出第1维度不是`batch`维度，需要设置参数`with_batch_dim=False`，`with_batch_dim`默认为`True`。

设置`with_batch_dim`为`True`，主要针对处理图片、文本等包含`batch`维度的模型。假设`batch_size=2`，当前请求有3个实例，共3张图片，会拆分为2次模型推理，第1次处理2张图片返回2个结果，第2次对剩余的1张图片进行拷贝做一次推理并返回1个结果，最终返回3个结果。

![image](images/resnet_with_batch.png)

设置`with_batch_dim`为`False`，主要针对不涉及或不考虑`batch`维度的模型。比如输入输出为二维Tensor的矩阵乘模型。请求的每个实例将单独作一次推理任务。

![image](./images/matmul_without_batch.png)

### 方法定义

方法定义的例子如下：

```python
from mindspore_serving.worker import register

@register.register_method(output_names=["label"])
def classify_top1(image):
    """Define method `classify_top1` for servable `resnet50`.
     The input is `image` and the output is `lable`."""
    x = register.call_preprocess(preprocess_pipeline, image)
    x = register.call_servable(x)
    x = register.call_postprocess(postprocess_top1, x)
    return x


@register.register_method(output_names=["label", "score"])
def classify_top5(image):
    """Define method `classify_top5` for servable `resnet50`.
     The input is `image` and the output is `lable` and `score`. """
    x = register.call_preprocess(preprocess_pipeline, image)
    x = register.call_servable(x)
    label, score = register.call_postprocess(postprocess_top5, x)
    return label, score
```

Python函数和Servable方法对应关系如下表：

|  Python函数 | Servable方法  |
|  ----  | ----  |
| 函数名 | 方法名 |
| 入参和入参名称 | 入参和入参名称 |
| `register_method`的`output_names`参数 | 出参和出参名称 |

- `call_preprocess`指示了使用的预处理及其输入。

- `call_servable`指示了模型推理的输入。

- `call_postprocess`指示了使用的后处理及其输入。

- `return`指示了方法的返回数据，和`register_method`的`output_names`参数对应。

方法定义不能包括if、for、while等分支结构，预处理和后处理可选，模型推理必选，且顺序不能打乱。