

> [如何选择模型训练的batch size和learning rate（2021）](https://zhuanlan.zhihu.com/p/363645881)
>
> 【学习率 和 batch_size 的关系】
>
> 1. 线性缩放策略：增大batch_size到原来的N倍时，为了保证经过同样数量的样本训练后得到更新的权重相等，学习率应增大到原来的N倍
> 2. 平方根缩放策略：增大batch_size到原来的N倍时，为了保证梯度的方差不变，学习率要相应变大$\sqrt{N}$倍
>
> 目前两种策略都被研究过，使用前者的居多；
>
> 实际建议：
>
> 1. batch_size和学习率一起增大；
> 2. 尽量使用大batch_size+大学习率；



> [【深度学习】batch_size 和 学习率lr 之间的关系](https://www.cnblogs.com/satsuki26681534/p/18937028)
>
> 【分类讨论】
>
> 1. SGD+动量：线性缩放策略
> 2. RMSprop、AdamW：
>    1. 平方根缩放策略
>    2. 避免 batch_size 过小，否则这类自适应优化器可能因梯度方差过大而失效
>
> 【实践建议】
>
> 1. 优先使用较大batch_size，并按线性缩放策略设置学习率



> [当Batch Size增大时，学习率该如何随之变化？](https://zhuanlan.zhihu.com/p/8475391959?share_code=ZxmXsRGUTn10&utm_psn=1963650478333198857)



【Ultralytics】

imgsz默认为640，是因为coco数据集中很多常见图片的短边在480到640像素之间，训练时需要根据自己的数据集选择合适的imgsz



【调参步骤】：

1. 根据模型结构选择优化器和初始学习率：

   1. CNN：SGD，lr=1e-1（学习率先选大，再往小试）
   2. Transformer：AdamW，lr=1e-4（学习率先选小，再往大试）
      1. 微调：lr=1e-5
      2. 从头训练：lr=1e-4

2. 根据显存90%选择batch_size

3. 经验选择epochs

   1. 微调：epochs=100
   2. 从头训练：epochs=300

4. 经验选择warmup epochs：

   1. 微调：warmup epochs=1到3（从3开始实验）
   2. 从头训练：warmup epochs=3到5（从5开始实验）

   > [!CAUTION]
   >
   > 根据训练日志中的什么情况调整 warmup epochs？

5. 测试出最佳 (batch_size, lr) 配对
