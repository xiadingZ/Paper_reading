## Spatiotemporal Pyramid Network for Video Action Recognition

本文探讨了一种结合空间特征与时间特征的网络结构。

STCB算法实现了一种特征融合的方式：z=vec(outer_dot(x,y))。x，y是两个待融合的特征，进行外积后进行一次Count Sketches映射，由于Count Sketches映射可以表示为卷积形式，而卷积也可以通过FFT进行快速计算，就有了如下特征融合的算法。

![p7](/Users/xd/code/Paper_reading/imgs_xd/p7.png)



网络先对光流特征进行特征融合后，与spatial特征再一起计算spatiotemporal attention，计算出一个spatiltemporal feature。之后三个特征再做一次融合。得出分类结果。

![p8](/Users/xd/code/Paper_reading/imgs_xd/p8.png)