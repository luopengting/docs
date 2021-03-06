# API Mapping

Mapping between PyTorch APIs and MindSpore APIs, which is provided by the community.

| PyTorch APIs                                         | MindSpore APIs                                                 | INFO |
|------------------------------------------------------|----------------------------------------------------------------|------|
| torch.abs                                            | mindspore.ops.Abs                                              | same |
| torch.acos                                           | mindspore.ops.ACos                                             | same |
| torch.add                                            | mindspore.ops.Add                                              | same |
| torch.argmax                                         | mindspore.ops.Argmax                                           | same |
| torch.argmin                                         | mindspore.ops.Argmin                                           | same |
| torch.asin                                           | mindspore.ops.Asin                                             | same |
| torch.atan                                           | mindspore.ops.Atan                                             | same |
| torch.atan2                                          | mindspore.ops.Atan2                                            | same |
| torch.bitwise_and                                    | mindspore.ops.BitwiseAnd                                       | same |
| torch.bitwise_or                                     | mindspore.ops.BitwiseOr                                        | same |
| torch.bmm                                            | mindspore.ops.BatchMatMul                                      | same |
| torch.broadcast_tensors                              | mindspore.ops.BroadcastTo                                      |[diff](https://gitee.com/mindspore/docs/blob/master/resource/api_mapping/BroadcastTo_en.md)|
| torch.cat                                            | mindspore.ops.Concat                                           | same |
| torch.ceil                                           | mindspore.ops.Ceil                                             | same |
| torch.chunk                                          | mindspore.ops.Split                                            | same |
| torch.clamp                                          | mindspore.ops.clip_by_value                                    | same |
| torch.cos                                            | mindspore.ops.Cos                                              | same |
| torch.cosh                                           | mindspore.ops.Cosh                                             | same |
| torch.cuda.device_count                              | mindspore.communication.get_group_size                         | same |
| torch.cuda.set_device                                | mindspore.context.set_context                                  |[diff](https://gitee.com/mindspore/docs/blob/master/resource/api_mapping/set_context_en.md)|
| torch.cumprod                                        | mindspore.ops.CumProd                                          | same |
| torch.cumsum                                         | mindspore.ops.CumSum                                           | same |
| torch.det                                            | mindspore.nn.MatDet                                            | same |
| torch.diag                                           | mindspore.nn.MatrixDiag                                        |[diff](https://gitee.com/mindspore/docs/blob/master/resource/api_mapping/MatrixDiag_en.md)|
| torch.digamma                                        | mindspore.nn.DiGamma                                           | same |
| torch.distributed.all_gather                         | mindspore.ops.AllGather                                        | same |
| torch.distributed.all_reduce                         | mindspore.ops.AllReduce                                        | same |
| torch.distributions.gamma.Gamma                      | mindspore.ops.Gamma                                            | same |
| torch.distributed.get_rank                           | mindspore.communication.get_rank                               | same |
| torch.distributed.init_process_group                 | mindspore.communication.init                                   |[diff](https://gitee.com/mindspore/docs/blob/master/resource/api_mapping/init_en.md)|
| torch.div                                            | mindspore.ops.Div                                              | same |
| torch.dot                                            | mindspore.ops.tensor_dot                                       |[diff](https://gitee.com/mindspore/docs/blob/master/resource/api_mapping/tensor_dot_en.md)|
| torch.eq                                             | mindspore.ops.Equal                                            | same |
| torch.erfc                                           | mindspore.ops.Erfc                                             | same |
| torch.exp                                            | mindspore.ops.Exp                                              | same |
| torch.expm1                                          | mindspore.ops.Expm1                                            | same |
| torch.eye                                            | mindspore.ops.Eye                                              | same |
| torch.flatten                                        | mindspore.ops.Flatten                                          |[diff](https://gitee.com/mindspore/docs/blob/master/resource/api_mapping/Flatten_en.md)|
| torch.flip                                           | mindspore.ops.ReverseV2                                        | same |
| torch.floor                                          | mindspore.ops.Floor                                            | same |
| torch.floor_divide                                   | mindspore.ops.FloorDiv                                         |[diff](https://gitee.com/mindspore/docs/blob/master/resource/api_mapping/FloorDiv_en.md)|
| torch.fmod                                           | mindspore.ops.Mod                                              | same |
| torch.gather                                         | mindspore.ops.GatherD                                          | same |
| torch.histc                                          | mindspore.ops.HistogramFixedWidth                              | same |
| torch.inverse                                        | mindspore.nn.MatInverse                                        | same |
| torch.lgamma                                         | mindspore.nn.LGamma                                            | same |
| torch.linspace                                       | mindspore.ops.LinSpace                                         | same |
| torch.load                                           | mindspore.load_checkpoint                                      | same |
| torch.log                                            | mindspore.ops.Log                                              | same |
| torch.log1p                                          | mindspore.ops.Log1p                                            | same |
| torch.logsumexp                                      | mindspore.nn.ReduceLogSumExp                                   | same |
| torch.matmul                                         | mindspore.nn.MatMul                                            | same |
| torch.max                                            | mindspore.ops.Maximum                                          | same |
| torch.mean                                           | mindspore.ops.ReduceMean                                       | same |
| torch.min                                            | mindspore.ops.Minimum                                          | same |
| torch.mm                                             | mindspore.ops.MatMul                                           | same |
| torch.mul                                            | mindspore.ops.Mul                                              | same |
| torch.nn.AdaptiveAvgPool2d                           | mindspore.ops.ReduceMean                                       |[diff](https://gitee.com/mindspore/docs/blob/master/resource/api_mapping/ReduceMean_en.md)|
| torch.nn.AvgPool1d                                   | mindspore.nn.AvgPool1d                                         | same |
| torch.nn.AvgPool2d                                   | mindspore.nn.AvgPool2d                                         | same |
| torch.nn.BatchNorm1d                                 | mindspore.nn.BatchNorm1d                                       | same |
| torch.nn.BatchNorm2d                                 | mindspore.nn.BatchNorm2d                                       | same |
| torch.nn.Conv2d                                      | mindspore.nn.Conv2d                                            | same |
| torch.nn.ConvTranspose2d                             | mindspore.nn.Conv2dTranspose                                   | same |
| torch.nn.CrossEntropyLoss                            | mindspore.nn.SoftmaxCrossEntropyWithLogits                     | same |
| torch.nn.CTCLoss                                     | mindspore.ops.CTCLoss                                          | same |
| torch.nn.Dropout                                     | mindspore.nn.Dropout                                           | same |
| torch.nn.Embedding                                   | mindspore.nn.Embedding                                         | same |
| torch.nn.Flatten                                     | mindspore.nn.Flatten                                           |[diff](https://gitee.com/mindspore/docs/blob/master/resource/api_mapping/nn_Flatten_en.md)|
| torch.nn.functional.adaptive_avg_pool2d              | mindspore.nn.AvgPool2d                                         |[diff](https://gitee.com/mindspore/docs/blob/master/resource/api_mapping/AvgPool2d_en.md)|
| torch.nn.functional.avg_pool2d                       | mindspore.ops.AvgPool                                          | same |
| torch.nn.functional.binary_cross_entropy             | mindspore.ops.BinaryCrossEntropy                               | same |
| torch.nn.functional.conv2d                           | mindspore.ops.Conv2D                                           | same |
| torch.nn.functional.elu                              | mindspore.ops.Elu                                              | same |
| torch.nn.functional.log_softmax                      | mindspore.nn.LogSoftmax                                        | same |
| torch.nn.functional.normalize                        | mindspore.ops.L2Normalize                                      |[diff](https://gitee.com/mindspore/docs/blob/master/resource/api_mapping/L2Normalize_en.md)|
| torch.nn.functional.one_hot                          | mindspore.ops.OneHot                                           | same |
| torch.nn.functional.pad                              | mindspore.ops.Pad                                              | same |
| torch.nn.functional.pixel_shuffle                    | mindspore.ops.DepthToSpace                                     | same |
| torch.nn.functional.relu                             | mindspore.ops.ReLU                                             | same |
| torch.nn.functional.softmax                          | mindspore.ops.Softmax                                          | same |
| torch.nn.functional.softplus                         | mindspore.ops.Softplus                                         | same |
| torch.nn.functional.softsign                         | mindspore.ops.Softsign                                         | same |
| torch.nn.GELU                                        | mindspore.nn.GELU                                              | same |
| torch.nn.GELU                                        | mindspore.nn.FastGelu                                          |[diff](https://gitee.com/mindspore/docs/blob/master/resource/api_mapping/FastGelu_en.md)|
| torch.nn.GroupNorm                                   | mindspore.nn.GroupNorm                                         | same |
| torch.nn.init.constant_                              | mindspore.common.initializer.Constant                          | diff |
| torch.nn.init.uniform_                               | mindspore.common.initializer.Uniform                           |[diff](https://gitee.com/mindspore/docs/blob/master/resource/api_mapping/Uniform_en.md)|
| torch.nn.KLDivLoss                                   | mindspore.ops.KLDivLoss                                        | same |
| torch.nn.L1Loss                                      | mindspore.nn.L1Loss                                            | same |
| torch.nn.LayerNorm                                   | mindspore.nn.LayerNorm                                         | same |
| torch.nn.LeakyReLU                                   | mindspore.nn.LeakyReLU                                         | same |
| torch.nn.Linear                                      | mindspore.nn.Dense                                             | diff |
| torch.nn.LSTM                                        | mindspore.nn.LSTM                                              | same |
| torch.nn.LSTMCell                                    | mindspore.nn.LSTMCell                                          | same |
| torch.nn.MaxPool2d                                   | mindspore.nn.MaxPool2d                                         | same |
| torch.nn.Module                                      | mindspore.nn.Cell                                              | same |
| torch.nn.Module.load_state_dict                      | mindspore.load_param_into_net                                  | same |
| torch.nn.ModuleList                                  | mindspore.nn.CellList                                          | same |
| torch.nn.MSELoss                                     | mindspore.nn.MSELoss                                           | same |
| torch.nn.Parameter                                   | mindspore.Parameter                                            | same |
| torch.nn.ParameterList                               | mindspore.ParameterTuple                                       | diff |
| torch.nn.PixelShuffle                                | mindspore.ops.DepthToSpace                                     | same |
| torch.nn.PReLU                                       | mindspore.nn.PReLU                                             | same |
| torch.nn.ReLU                                        | mindspore.nn.ReLU                                              | same |
| torch.nn.ReplicationPad2d                            | mindspore.nn.Pad                                               | same |
| torch.nn.Sequential                                  | mindspore.nn.SequentialCell                                    | same |
| torch.nn.Sigmoid                                     | mindspore.nn.Sigmoid                                           | same |
| torch.nn.SmoothL1Loss                                | mindspore.nn.SmoothL1Loss                                      | same |
| torch.nn.Softmax                                     | mindspore.nn.Softmax                                           | same |
| torch.nn.SyncBatchNorm.convert_sync_batchnorm        | mindspore.nn.GlobalBatchNorm                                   | same |
| torch.nn.Tanh                                        | mindspore.nn.Tanh                                              | same |
| torch.nn.Unfold                                      | mindspore.nn.Unfold                                            | same |
| torch.nn.Upsample                                    | mindspore.ops.ResizeBilinear                                   | diff |
| torch.norm                                           | mindspore.nn.Norm                                              | diff |
| torch.numel                                          | mindspore.ops.Size                                             | same |
| torch.ones                                           | mindspore.ops.Ones                                             | same |
| torch.ones_like                                      | mindspore.ops.OnesLike                                         | same |
| torch.optim.Adadelta                                 | mindspore.ops.ApplyAdadelta                                    | diff |
| torch.optim.Adagrad                                  | mindspore.ops.ApplyAdagrad                                     | diff |
| torch.optim.Adam                                     | mindspore.nn.Adam                                              | same |
| torch.optim.Adamax                                   | mindspore.ops.ApplyAdaMax                                      | same |
| torch.optim.AdamW                                    | mindspore.nn.AdamWeightDecay                                   | same |
| torch.optim.lr_scheduler.CosineAnnealingWarmRestarts | mindspore.nn.cosine_decay_lr                                   | same |
| torch.optim.lr_scheduler.StepLR                      | mindspore.nn.piecewise_constant_lr                             | same |
| torch.optim.Optimizer.step                           | mindspore.nn.TrainOneStepCell                                  | diff |
| torch.optim.RMSprop                                  | mindspore.nn.RMSProp                                           | same |
| torch.optim.SGD                                      | mindspore.nn.SGD                                               | same |
| torch.pow                                            | mindspore.ops.Pow                                              | same |
| torch.prod                                           | mindspore.ops.ReduceProd                                       | same |
| torch.rand                                           | mindspore.ops.UniformReal                                      | same |
| torch.randint                                        | mindspore.ops.UniformInt                                       | same |
| torch.randn                                          | mindspore.ops.StandardNormal                                   | same |
| torch.range                                          | mindspore.nn.Range                                             | same |
| torch.round                                          | mindspore.ops.Rint                                             | same |
| torch.save                                           | mindspore.save_checkpoint                                      | same |
| torch.sigmoid                                        | mindspore.ops.Sigmoid                                          | same |
| torch.sin                                            | mindspore.ops.Sin                                              | same |
| torch.sinh                                           | mindspore.ops.Sinh                                             | same |
| torch.sparse.FloatTensor                             | mindspore.Tensor                                               | diff |
| torch.split                                          | mindspore.ops.Split                                            | same |
| torch.sqrt                                           | mindspore.ops.Sqrt                                             | same |
| torch.squeeze                                        | mindspore.ops.Squeeze                                          | same |
| torch.stack                                          | mindspore.ops.Stack                                            | same |
| torch.std_mean                                       | mindspore.ops.ReduceMean                                       | diff |
| torch.sum                                            | mindspore.ops.ReduceSum                                        | same |
| torch.tan                                            | mindspore.ops.Tan                                              | same |
| torch.tanh                                           | mindspore.ops.Tanh                                             | same |
| torch.tensor                                         | mindspore.Tensor                                               | same |
| torch.Tensor                                         | mindspore.Tensor                                               | same |
| torch.Tensor.chunk                                   | mindspore.ops.Split                                            | same |
| torch.Tensor.expand                                  | mindspore.ops.BroadcastTo                                      | same |
| torch.Tensor.fill_                                   | mindspore.ops.Fill                                             | same |
| torch.Tensor.float                                   | mindspore.ops.Cast                                             |[diff](https://gitee.com/mindspore/docs/blob/master/resource/api_mapping/Cast_en.md)|
| torch.Tensor.index_add                               | mindspore.ops.InplaceAdd                                       | same |
| torch.Tensor.mm                                      | mindspore.ops.MatMul                                           | same |
| torch.Tensor.mul                                     | mindspore.ops.Mul                                              | same |
| torch.Tensor.pow                                     | mindspore.ops.Pow                                              | same |
| torch.Tensor.repeat                                  | mindspore.ops.Tile                                             | same |
| torch.repeat_interleave                              | mindspore.ops.repeat_elements                                  | same |
| torch.Tensor.requires_grad_                          | mindspore.Parameter.requires_grad                              | same |
| torch.Tensor.round                                   | mindspore.ops.Round                                            | same |
| torch.Tensor.scatter                                 | mindspore.ops.ScatterNd                                        | same |
| torch.Tensor.scatter_add_                            | mindspore.ops.ScatterNdAdd                                     | diff |
| torch.Tensor.sigmoid                                 | mindspore.nn.Sigmoid                                           | same |
| torch.Tensor.sign                                    | mindspore.ops.Sign                                             | same |
| torch.Tensor.size                                    | mindspore.ops.Shape                                            | same |
| torch.Tensor.sqrt                                    | mindspore.ops.Sqrt                                             | same |
| torch.Tensor.sub                                     | mindspore.ops.Sub                                              | same |
| torch.Tensor.t                                       | mindspore.ops.Transpose                                        | diff |
| torch.Tensor.transpose                               | mindspore.ops.Transpose                                        | same |
| torch.Tensor.unsqueeze                               | mindspore.ops.ExpandDims                                       | same |
| torch.Tensor.view                                    | mindspore.ops.Reshape                                          | same |
| torch.Tensor.zero_                                   | mindspore.ops.ZerosLike                                        | same |
| torch.transpose                                      | mindspore.ops.Transpose                                        | same |
| torch.tril                                           | mindspore.nn.Tril                                              | same |
| torch.triu                                           | mindspore.nn.Triu                                              | same |
| torch.unbind                                         | mindspore.ops.Unstack                                          | same |
| torch.unique                                         | mindspore.ops.Unique                                           | diff |
| torch.unsqueeze                                      | mindspore.ops.ExpandDims                                       | same |
| torch.utils.data.DataLoader                          | mindspore.DatasetHelper                                        | same |
| torch.utils.data.Dataset                             | mindspore.dataset.MindDataset                                  | same |
| torch.utils.data.distributed.DistributedSampler      | mindspore.dataset.DistributedSampler                           | same |
| torch.zeros                                          | mindspore.ops.Zeros                                            | same |
| torch.zeros_like                                     | mindspore.ops.ZerosLike                                        | same |
| torchvision.datasets.ImageFolder                     | mindspore.dataset.ImageFolderDataset                           | same |
| torchvision.ops.nms                                  | mindspore.ops.NMSWithMask                                      | same |
| torchvision.ops.roi_align                            | mindspore.ops.ROIAlign                                         | same |
| torchvision.transforms.CenterCrop                    | mindspore.dataset.vision.py_transforms.CenterCrop              | same |
| torchvision.transforms.ColorJitter                   | mindspore.dataset.vision.py_transforms.RandomColorAdjust       | same |
| torchvision.transforms.Compose                       | mindspore.dataset.transforms.py_transforms.Compose             | same |
| torchvision.transforms.Normalize                     | mindspore.dataset.vision.py_transforms.Normalize               | same |
| torchvision.transforms.RandomHorizontalFlip          | mindspore.dataset.vision.py_transforms.RandomHorizontalFlip    | same |
| torchvision.transforms.Resize                        | mindspore.dataset.vision.py_transforms.Resize                  | same |
| torchvision.transforms.ToTensor                      | mindspore.dataset.vision.py_transforms.ToTensor                | same |
