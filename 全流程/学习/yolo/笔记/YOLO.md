## YOLOv8

支持任务：图像分类（cls）、目标检测（无后缀）、实例分割（seg）、姿态关键点检测（pose）、OBB



实验结果：

1. 参数 mAP50-95

2. 速度 mAP50-95



模型的 n / s / m / l / x 根据 .yaml 文件中的 [depth, width, max_channels] 决定参数量



网络结构：

![YOLOv8结构图](./YOLOv8结构图.jpg)

概括：backbone下采样，head中先上采样再下采样（PAN结构，同YOLOv5），得到P3 / P4 / P5，在三个不同尺度的特征图上分别detect

细节：

1. SPPF中的三个MaxPool2d都是5×5的



检测头：

假设取 80×80 的特征图，则最后输出的 类别特征图（Cls）的通道数为 nc，边框特征图（Bbox）的通道数为 4×reg_max

类别特征图中的nc代表总种类

边框特征图中的reg_max 表示回归分布的离散 bin 数，也就是说，预测的是此物体的框的四条边和本像素中心点的距离在0-16之间的概率：0-1概率为0，1-2概率为0，...,7-8概率为0.7，8-9概率为0.9，9-10概率为0.3，...，15-16概率为0，求期望（向上取值：0\*1+0\*2+...+0.7\*8+0.9\*9+0.3\*10+...+0\*16）

（Anchor-Free）



> YOLOv3：Anchor-Based
>
> k-means算法得出anchor，预测 (tx, ty, tw, th, conf)
>
> 每个像素对应三个Anchor，每个Anchor对应一个预测框



正负样本匹配：



损失函数计算：



## YOLO11

### 1. 性能

（与YOLOv8相比）

### 2. 网络结构

与YOLOv8十分相近，主要是模块的替换：

1. Backbone
   1. C2f模块 换为 C3k2模块
   2. 在SPPF模块后增加 C2PSA模块
2. Head
   1. 分类检测头中的 两个Conv 换为 两个DWConv（深度可分离卷积，参考 MobileNetV1）