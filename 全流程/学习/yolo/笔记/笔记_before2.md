[TOC]

---

# DETR

可以从【翻译图片】的角度理解DETR



DETR的创新点：

1. Anchor-Based 变为 Object Query
2. 基于NMS去除多余预测框 变为 从头就不输出那么多预测框+二分图匹配



输入 Transformer Encoder 的格式：(token总数, token维度)



encoder感知位置，decoder明确边缘

---

# 可变形卷积 Deformable Convlution



---

# Deformable DETR



---

# RT-DETR

YOLO的后处理的置信度阈值和NMS中的IOU阈值都需要手动设置