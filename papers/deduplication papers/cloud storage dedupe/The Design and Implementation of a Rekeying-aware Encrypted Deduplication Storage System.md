#The Design and Implementation of a Rekeying-aware Encrypted Deduplication Storage System
##Authors: Chuan Qin et al. from CUHK
##Published in TOS'17
##Date of read: July 20, 2017

这篇文章是在那篇TKDE的文章之后读的，感觉TKDE那篇很可能是会议没中投了期刊，创新感觉很有限。

这篇更原创一些。

这篇回答了我读那篇文章时产生的疑问，也就是rekeying的开销问题。　

这篇文章的想法非常精妙，基本思路是

利用All-or-Nothing Transform(AONT)，这算是一个不基于key的加密，相当于是把文件的顺序打乱了，然后如果不知道文件的所有内容，就无法解开文件。

具体用法如下：
首先用MLE　key对文件进行加密，然后用AONT生成一个加密后数据的package。这个package中有很小一段数据，用另外一个key，叫做file key来加密，而这个file key只有这个文件的拥有者才有。当owner group发生变化的时候，就对这个file key进行重新生成和分发。

这篇文章做了假设，认为这个file key的管理server是相当安全的，应该不会被CSP compromise。

这样，file key就防止了不在这个owner group中的用户访问这个文件而且防止了服务器compromise。而由于数据的主体还是只被MLE加密的，因此并不会影响deduplication。


