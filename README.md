# DeepLabV3
此代码是基于Pytorch的Deeplabv3复现，除了论文中的Multi-Grid的（1,2,4）改为了（1,1,1），其余尽量还原了论文中的设置。在VOC2012的val上，使用相同的超参数情况下，复现出与论文相当的结果。另外，我们加入了 Group Normalization（GN） + Weight Standardization（WS）的实验结果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200329210435426.png)
