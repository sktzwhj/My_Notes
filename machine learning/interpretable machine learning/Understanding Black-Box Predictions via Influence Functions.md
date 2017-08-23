#Title: Understanding Black-Box Predictions via Influence Functions
##Authors: Peng Wei Koh and Percy Liang from Stanford University
##Published in ICML'17


这篇文章通过分析对某个prediction产生影响最大的instance来理解黑盒模型。

和我们认为的一致，这篇文章也指出了采用perturbation这样的方法是开销非常大的。

文章的思想我们之前也考虑过，比如如果把一些数据摘除了进行训练，根据训练结果就可以分析出这些训练样本对于模型重要程度。不过区别在于本文用了一些数学上的优化方法使得这种方法的计算变成可能的。

虽然对于influence function的一些细节还没有仔细了解，但是可以理解其就是leave-one-out retraining的一种近似。

反观我们通过boundary tree找到的这些点，是否可以看一下他们是否就是对于模型对重要的点呢？
关键在于如何定义最重要。。。

可以简单做两个实验：
1. 如果我们只用这些数据进行训练呢？
2. 如果我们训练的时候将这些数据剔除呢