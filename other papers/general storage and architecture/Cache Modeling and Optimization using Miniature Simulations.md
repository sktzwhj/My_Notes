#Title: Cache Modeling and Optimization using Miniature Simulations
##Authors: Carl Waldspurger et al. from CachePhysics and Datos IO
##Published in USENIX ATC'17 (best paper)
##Date of read: July 31, 2017

这篇文章是讲如何通过模拟的方式来分析缓存的性能，因为像LIRS以及ARC这样的算法目前没有低开销的模拟方法，所以在分析性能的时候，对于不同的cache size可能就需要跑很多个instance，这样代价是很大的。　

为什么对于non-stack的缓存算法不能用基于sampling的方法来处理呢？
我认为主要是因为每个data block之间的关系并非独立的。

感觉上这篇文章的方法也不是作者首先提出来的，所以作为一个以实验为主的文章能够拿到best paper也是让人很