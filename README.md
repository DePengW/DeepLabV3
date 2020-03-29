# DeepLabV3
基于Pytorch的DeepLabV3复现
This is a PyTorch implementation of DeepLabv3 that aims to reuse the resnet implementation in torchvision as much as possible. This means we use the PyTorch model checkpoint when finetuning from ImageNet, instead of the one provided in TensorFlow.

We try to match every detail in DeepLabv3, except that Multi-Grid other than (1, 1, 1) is not yet supported. On PASCAL VOC 2012 validation set, using the same hyperparameters, we reproduce the performance reported in the paper (GPU with 16GB memory is required). We also support the combination of Group Normalization + Weight Standardization:
