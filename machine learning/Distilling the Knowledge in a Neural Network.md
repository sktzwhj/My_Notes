#Distilling the Knowledge in a Neural Network
##Authors: Geoffrery Hinton, Oriol Vinyals and Jeff Dean from Google
##Date: Jan 15, 2018

这篇文章所其实可以算作一篇模型压缩的相关文章，其distill knowledge的目的并不是将知识转化为一种人可以理解的形式，而是说将复杂模型学到的东西用一个简单模型来进行拟合。

单看作者就知道文章的重要性了，对于神经网络的很多理解，不得不说Hinton大神的洞察力惊人。像是dropout这种简单却有效的方法，纵使其数学形式也许不那么完美，但是从ensemble角度的解释已经很让人兴奋了。

本文的根本思想就是将复杂网络学到的soft target给简单网络作为监督数据对其进行训练。具体来说，用复杂网络的logit或者softmax输出，可以向简单网络提供不仅限于原label这样的简单信息。logit或者softmax输出中还包含了复杂网络学到的一个数据点到不同类的可能性，这本身也是一种feature。或者说，这里logit本身就是一种大信息量的标签。然后将其考虑进去重新设计loss function，从而实现直接训练一个简单的拟合网络的目的。

这篇文章对我们修改关于interpretable model sharing工作也有启发。其实logit就表达了复杂网络学到的知识，如果说用简单的神经网络来拟合这个结果算是一种模型压缩的话，用boundary tree这样的结构则是为了以可解释性为目的对数据进行重新组织。从这个角度来写文章，说不定是一个更好的方式。

