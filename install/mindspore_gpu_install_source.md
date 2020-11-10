# 源码编译方式安装MindSpore GPU版本

<!-- TOC -->

- [源码编译方式安装MindSpore GPU版本](#源码编译方式安装mindspore-gpu版本)
    - [确认系统环境信息](#确认系统环境信息)
    - [从代码仓下载源码](#从代码仓下载源码)
    - [编译MindSpore](#编译mindspore)
    - [安装MindSpore](#安装mindspore)
    - [验证是否成功安装](#验证是否成功安装)

<!-- /TOC -->

<a href="https://gitee.com/mindspore/docs/blob/master/install/mindspore_gpu_install_source.md" target="_blank"><img src="https://gitee.com/mindspore/docs/raw/master/resource/_static/logo_source.png"></a>

本文档介绍如何在GPU环境的Linux系统上，使用源码编译方式快速安装MindSpore。

## 确认系统环境信息

- 确认安装Ubuntu 18.04是64位操作系统。
- 确认安装[GCC](http://ftp.gnu.org/gnu/gcc/gcc-7.3.0/gcc-7.3.0.tar.gz) 7.3.0版本。
- 确认安装[gmp](https://gmplib.org/download/gmp/gmp-6.1.2.tar.xz) 6.1.2及以上版本。
- 确认安装[Python](https://www.python.org/ftp/python/3.7.5/Python-3.7.5.tgz) 3.7.5版本。
- 确认安装[CMake](https://cmake.org/download/) 3.14.1及以上版本。
    - 安装完成后将CMake添加到系统环境变量。
- 确认安装[patch](http://ftp.gnu.org/gnu/patch/) 2.5及以上版本。
    - 安装完成后将patch添加到系统环境变量中。
- 确认安装[Autoconf](https://www.gnu.org/software/autoconf) 2.69及以上版本（可使用系统自带版本）。
- 确认安装[Libtool](https://www.gnu.org/software/libtool) 2.4.6-29.fc30及以上版本（可使用系统自带版本）。
- 确认安装[Automake](https://www.gnu.org/software/automake) 1.15.1及以上版本（可使用系统自带版本）。
- 确认安装[CuDNN](https://developer.nvidia.com/rdp/cudnn-archive) 7.6及以上版本。
- 确认安装[Flex](https://github.com/westes/flex/) 2.5.35及以上版本。
- 确认安装[wheel](https://pypi.org/project/wheel/) 0.32.0及以上版本。
- 确认安装[OpenSSL](https://github.com/openssl/openssl.git) 1.1.1及以上版本。
    - 需保证已经安装了[OpenSSL](https://github.com/openssl/openssl.git)，并设置环境变量`export OPENSSL_ROOT_DIR=“OpenSSL安装目录”`。
- 确认安装[CUDA 10.1](https://developer.nvidia.com/cuda-10.1-download-archive-base)按默认配置安装。  
    - CUDA安装后，若CUDA没有安装在默认位置，需要设置环境变量PATH（如：`export PATH=/usr/local/cuda-${version}/bin:$PATH`）和`LD_LIBRARY_PATH`（如：`export LD_LIBRARY_PATH=/usr/local/cuda-${version}/lib64:$LD_LIBRARY_PATH`），详细安装后的设置可参考[CUDA安装手册](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#post-installation-actions)。
- 确认安装git工具。  
    如果未安装，使用如下命令下载安装：

    ```bash
    apt-get install git
    ```

## 从代码仓下载源码

```bash
git clone https://gitee.com/mindspore/mindspore.git
```

## 编译MindSpore

在源码根目录下执行如下命令。

```bash
bash build.sh -e gpu
```

> `build.sh`中默认的编译线程数为8，如果编译机性能较差可能会出现编译错误，可在执行中增加-j{线程数}来减少线程数量。如`bash build.sh -e gpu -j4`。

## 安装MindSpore

```bash
chmod +x build/package/mindspore_gpu-{version}-cp37-cp37m-linux_{arch}.whl
pip install build/package/mindspore_gpu-{version}-cp37-cp37m-linux_{arch}.whl --trusted-host ms-release.obs.cn-north-4.myhuaweicloud.com -i https://mirrors.huaweicloud.com/repository/pypi/simple
```

> - 在联网状态下，安装whl包时会自动下载MindSpore安装包的依赖项（依赖项详情参见[requirements.txt](https://gitee.com/mindspore/mindinsight/blob/master/requirements.txt)），其余情况需自行安装。
> - `{version}`表示MindSpore版本号，例如下载1.0.1版本MindSpore时，`{version}`应写为1.0.1。  
> - `{arch}`表示系统架构，例如使用的Linux系统是x86架构64位时，`{arch}`应写为`x86_64`。如果系统是ARM架构64位，则写为`aarch64`。

## 验证是否成功安装

```python
import numpy as np
from mindspore import Tensor
import mindspore.ops as ops
import mindspore.context as context

context.set_context(device_target="GPU")
x = Tensor(np.ones([1,3,3,4]).astype(np.float32))
y = Tensor(np.ones([1,3,3,4]).astype(np.float32))
print(ops.tensor_add(x, y))
```

如果输出：

```text
[[[ 2.  2.  2.  2.],
    [ 2.  2.  2.  2.],
    [ 2.  2.  2.  2.]],

    [[ 2.  2.  2.  2.],
    [ 2.  2.  2.  2.],
    [ 2.  2.  2.  2.]],

    [[ 2.  2.  2.  2.],
    [ 2.  2.  2.  2.],
    [ 2.  2.  2.  2.]]]
```

说明MindSpore安装成功了。

## 升级MindSpore版本

当需要升级MindSpore版本时，可执行如下命令：

- 直接在线升级

    ```bash
    pip install --upgrade mindspore_gpu
    ```

- 本地源码编译升级

    在源码根目录下执行编译脚本`build.sh`成功后，在`build/package`目录下找到编译生成的whl安装包，然后执行命令进行升级。

    ```bash
    pip install --upgrade mindspore_gpu-{version}-cp37-cp37m-linux_{arch}.whl
    ```