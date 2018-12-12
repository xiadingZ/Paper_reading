### Review

有5篇是学习spatio-temporal特征的

- Interaction-aware Spatio-temporal Pyramid Attention Networks for Action Classification

  优点

  - 利用到了多尺度特征，并且保证了每个尺度的attention的差异性
  - 利用PCA思想保证了学习到channel feature之间的interaction

  改进点

  - 这个attention只针对了图像的静态信息，没有包含动作信息，应该对光流也进行attention操作后和spatial的结合起来

- Spatiotemporal Multiplier Networks for Video Action Recognition

  优点

  - 考虑了空间特征和时间特征的结合

  改进点

  - 融合的方式很初级，只是加法或乘法操作，可以参考STCB算法的融合方式

- Spatiotemporal Pyramid Network for Video Action Recognition

  优点

  - 利用Count Sketches映射实现的STCB算法实现了一种bilinear融合方式
  - 利用时间信息对空间信息进行了attention

  改进点

  - 只在CNN的最后面一层进行特征融合，可以在中间层进行特征融合

- Action Recognition with Coarse-to-Fine Deep Feature Integration and Asynchronous Fusion

  优点

  - 通过coarse-to-fine网络进行层级训练的思想很好
  - 异步特征融合网络

- 改进点

  - 这个异步还是太high-level，应该在CNN网络的scale-level进行特征融合
  - coarse-to-fine的类别是由一个预训练好的参数固定的网络A给出，就相当于是transfer-learning来学习如何提取特征，那么上限会被网络A的性能限制。



计划：

- 设计一种在空间流和时间流提特征时中间层特征融合的方法，可以对多个scale进行soft attention或hard attention后融合。还需要考虑一下特征融合的方式。
- 光流的10帧覆盖范围太小，可以在video level对多个时间戳的光流进行PCA或attention。

- coarse-to-fine的思想很好，适合需要区分特征很相似的类别的情况。可以考虑针对三种粒度的动作集设计三个惩罚度不同的损失函数，分三阶段进行训练，先保证能分到正确的最粗粒度的动作集。