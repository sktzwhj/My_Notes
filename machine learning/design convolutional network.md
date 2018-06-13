#deep learning学习的一点笔记

##关于卷积网络的参数选择
###1. 如何决定conv filter的大小和数量呢？
conv filter的大小取决于所要提取的特征的粒度，如果要提取非常细节的特征，应该就需要比较小的filter。
至于数量，应该就是要提取多少种特征，比如不同的纹理，色彩之类的。

在选择这些参数的时候，还是需要考虑网络的复杂度。
复杂度可以通过参数的数量来描述，因为这些参数都是要通过反向传播来进行学习的。

就卷积核来说，比如5x5的filter,参数就是25个，再乘以卷积核的数量，就是这一层的参数数量，当然还要加上bias。
