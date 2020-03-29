# DeepLabV3
代码解读：https://blog.csdn.net/weixin_42028608/article/details/104956170
### 1.介绍
<center class="half">
    <img src="https://img-blog.csdnimg.cn/20200329215713477.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjAyODYwOA==,size_16,color_FFFFFF,t_70"  width="300"/>
    <img src="https://img-blog.csdnimg.cn/20200329220232356.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjAyODYwOA==,size_16,color_FFFFFF,t_70"  width="300"/>
</center>

此代码是基于Pytorch的Deeplabv3复现，除了论文中的Multi-Grid的（1,2,4）改为了（1,1,1），其余尽量还原了论文中的设置。在VOC2012的val上，使用相同的超参数情况下，复现出与论文相当的结果。另外，我们加入了 Group Normalization（GN） + Weight Standardization（WS）的实验结果：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200329210435426.png)
### 2.环境配置
python3.6 + torch1.1.0

### 3. 数据集准备
#### 3.1 PASCAL VOC 2012 Dataset

>>>>>>> 07640b51b7af7030832da5ae0f6fd1d0aa857b33
```bash
mkdir data
cd data
wget http://host.robots.ox.ac.uk/pascal/VOC/voc2012/VOCtrainval_11-May-2012.tar
tar -xf VOCtrainval_11-May-2012.tar
cd VOCdevkit/VOC2012/
wget http://cs.jhu.edu/~cxliu/data/SegmentationClassAug.zip
wget http://cs.jhu.edu/~cxliu/data/SegmentationClassAug_Visualization.zip
wget http://cs.jhu.edu/~cxliu/data/list.zip
unzip SegmentationClassAug.zip
unzip SegmentationClassAug_Visualization.zip
unzip list.zip
```

<<<<<<< HEAD
## Prepare Cityscapes Dataset
=======
#### 3.2 Cityscapes Dataset

>>>>>>> 07640b51b7af7030832da5ae0f6fd1d0aa857b33
```bash
unzip leftImg8bit_trainvaltest.zip
unzip gtFine_trainvaltest.zip
git clone https://github.com/mcordts/cityscapesScripts.git
mv cityscapesScripts/cityscapesscripts ./
rm -rf cityscapesScripts
python cityscapesscripts/preparation/createTrainIdLabelImgs.py
```
<<<<<<< HEAD
=======

### 4. 训练
#### 4.1 训练BN的模型

```cpp
python main.py --train --exp bn_lr7e-3 --epochs 50 --base_lr 0.007
```
#### 4.1 训练GN+WS的模型
若想使用GN+WS进行实验，应先下载在ImageNet预训练好的GN+WS ResNet101模型
```bash
wget https://cs.jhu.edu/~syqiao/WeightStandardization/R-101-GN-WS.pth.tar -P data/
python main.py --train --exp gn_ws_lr7e-3 --epochs 50 --base_lr 0.007 --groups 32 --weight_std
```

### 5. 测试
- 已训练好的BN模型下载地址：

```bash
wget https://cs.jhu.edu/~cxliu/data/deeplab_resnet101_pascal_v3_bn_lr7e-3_epoch50.pth -P data/
```
- 已训练好的GN+WS模型下载地址：

```bash
wget https://cs.jhu.edu/~cxliu/data/deeplab_resnet101_pascal_v3_gn_ws_lr7e-3_epoch50.pth -P data/
```
#### 5.1 测试BN的模型
```bash
python main.py --exp bn_lr7e-3 --epochs 50 --base_lr 0.007
```
#### 5.2 测试GN+WS的模型
```bash
python main.py --exp gn_ws_lr7e-3 --epochs 50 --base_lr 0.007 --groups 32 --weight_std
```
<front size = 1>注：测试图片的输出结果存于data/val


>>>>>>> 07640b51b7af7030832da5ae0f6fd1d0aa857b33
