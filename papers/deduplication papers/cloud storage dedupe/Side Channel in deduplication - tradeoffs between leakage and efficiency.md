#Title: Side Channels in deduplication: trade-offs between leakage and efficiency
#Authors: Frederik Armknecht et al. from University of Mannheim, Germany
#ASIACCS'17
#Date of Read: July 23, 2017

目前看到的关于encrypted deduplication的潜在攻击模式中，简单总结一下，包括两个方面：
1. 在server一侧，主要考虑server可能有恶意，honest-but-curious。
2. 在client一侧，恶意的client可能会通过side channel去猜测server上已经存储了哪些信息。

对于1,我认为Patrick Lee他们做的那篇用all-or-nothing transform做的算是当前比较好的方案
对于2，这篇文章算是在从更理论的层面上进行讨论。　

Danny Harnik在这个领域算是先驱,他提出基于一个threshold的方法，也就是即使在server一侧已经存了这个文件，也依然要求client传过来，然后把去重的任务在server一侧处理。

不过在具体实现中，想必是不需要真的在server一侧做去重的，这只是服务器在fool恶意client的一种做法。　

但如果server已经有了数据之后还要求client传的话，这就有点浪费网络带宽了。