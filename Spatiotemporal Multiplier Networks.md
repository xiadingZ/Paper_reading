## Spatiotemporal Multiplier Networks for Video Action Recognition

这篇文章主要是探讨了2-stream方式的空间特征和时间特征的融合方式。借鉴了Resnet的思想。一个stream是2D CNN作用到RGB图像上，一个stream是光流特征。在两个stream之间加入了一些连接达到了交互的效果。

原始的2stream方式是在softmax预测时进行融合，这个文章尝试了几种在中间层进行交互的方式。有加法连接与乘法连接，单向连接及双向连接。经过试验得知乘法连接效果最好，可能是因为惩罚对信息的形象比较大，这样就能更有效地捕捉到信息。示意图如下。

![p3](imgs_xd/p3.png)



由于每个光流片段的范围太小，只包含了10帧左右，所以之后还利用了1D temporal 卷积，以及以identity matrix初始化的特征空间转换矩阵，学习了整个视频的global temporal特征，W作为temporal filter,进行特征空间转化，由于对网络路径的变化比较大时会影响预训练的模型，所以初始化为identity matrix，可以加在任何地方。

![p4](imgs_xd/p4.png)



总结：

这篇文章探索了两个stream特征在中间层的交互方式。但是他的连接方式是同步的，训练时要两个stream一起训练，增加了训练复杂度，而且同层连接可能不太合适，appearance stream与temporal stream可能是不同层的特征才有很好的对应关系。

不太理解1维卷积中加上W作为temporal filter的作用。