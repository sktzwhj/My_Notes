#Title: Secure Data Deduplication with Dynamic Ownership Management in Cloud Storage
##Authors:  Junbeom Hur, Dongyoung Koo, Youngjoo Shin, et al. from Korea University
##Published in IEEE Transactions on Knowledge and Data Engineering in 2016
##Date of Read: July 20, 2017

关于secure deduplication发展的脉络，基本上可以这样总结

1. 首先如果用户数据需要加密的话，每个用户如果有自己的秘钥，那么加密后的密文就无法进行去重了
2. 因此convergent encryption出现了，也就是我们说的message-locked encryption
3. 但是在云存储当中，文件的拥有权实际上是在不断发生变化的，因此就会导致些问题，这里有意思的一点是，作者指出，如果一个用户已经删除了一个文件，那么即使他拥有文件的hash，他也不应该还能够访问这个文件。
4. 所以这篇文章提出的解决方案就是，对于一个文件，如果ownership group发生了变化，就用一个group key来重新加密数据块，然后将这个key重新分发给拥有该数据的用户。

简单扫了一下文章的实验，这篇文章的局限性还是比较明显的。首先，我们想像如果某些文件块被大量的用户共同拥有的话，那么文件权限的变化也会经常变化。如果一旦变化就需要对数据进行重新加密，那么这种加密可能会发生得极其频繁，这对于服务器来说，也是一种很大的压力。　