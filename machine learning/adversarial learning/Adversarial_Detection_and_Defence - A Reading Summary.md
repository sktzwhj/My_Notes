#Adversarial Detection and Defence - A Reading Summary

近来做东西不是特别顺利，心里想索性就先放一放，多读一点东西。而且最近我也有另一个领悟，不管学什么东西，如果最后没有形成输出，就会忘记得非常快，而且其中很多细节也没有办法细想，因此以后读论文还是写一写summary吧。读了一些关于adversarial　attack　和 detection的东西，显然到目前为止，这个问题依然没有得到解决，大多数尝试都显得治标不治本，但是如何治本？这大概是高维空间没有办法解决的问题？看了Ian Goodfellow发在CACM上的文章，感觉最后的总结也说出了目前的情形，大家都在尝试，但是其实甚至不知道这个问题到底是不是有完美的解。或者说到了哪一天我们可以从理论上发现这其实是无解的？

##Attack

首先，从攻击手段来看，目前比较有名的包括

###Fast Gradient Sign Method (FGSM)
这个方法又可以包括两种，一种是Targeted另一种是Untargeted。
对于Untargeted，只要maximize J(\theta, x, label_true)即可。
而对于Targeted, 则是minimize J(\theta, x, target_label)。
这种方法从根本上说，就是朝着loss梯度的方向进行修改。

如果再改进一下该方法，就是Iterative Gradient Sign Method。
这种方法就是每次加少量的扰动，然后进行很多次迭代知道到达最大迭代次数或者找到一个adversarial sample。其根本目的是为了在添加尽可能少的扰动的情况下生成攻击样本。

###Jacobian-based Saliency Map Attack (JSMA)
与FGSM相比, JSMA则更多是找到一个adversarial并确保其L0-norm最小，即修改尽可能少的像素点。

另外，这种攻击方式是依据saliency map来的，简单来讲就是根据模型F的正向梯度来，这一点要和FGSM当中针对loss的梯度区分开来。

这种方法有两个变种，即在进行targeted构造的时候，可以maximize logit of the target class或者softmax of the target class

###CW
一种更强的样本生成方法，同样限制L-norms来减小perturbation的大小。


##Defence

能检测出来自然是defence的第一步了，至于检测出来怎么办，目前的检测方法有挺多种，但其实很多看起来都不是很有趣，这里列举一下看过的。

###Distillation as a defence
这值Nicolas Papernot提出的方法，根本思想是通过网络输出的软标签重新训练一个网络，然后再两个网络一起来进行预测。
其出发点大致如下：
已有方法在构造adversarial example的时候主要是依赖于梯度，如果梯度很大，很小的扰动就可以生成有效的攻击样本。
所以这篇文章讲，要想减小由input variation带来的输出扰动，我们必须让模型更加平滑，也就是说，距离不远的样本不应该得到很不一样的输出。

距离benigh样本不远的样本可以用不同的norm距离来描述。

用soft labels训练出来的网络，与原网络相比的泛化能力应该更好，因为soft labels实际上描述了类和类之间的相似性？总感觉这个说法有点悬。。

关于距离不远的样本不应该得到很不一样的输出，下文给出了一个更直接的做法

###Matigating Evasion Attacks to DNN via Region-based Classification

这文章基本就是把那个思想很直接的实现了一遍，不过道理上感觉就不会太玄妙了。

###Data preprocessing
还有一种方法是说我把输入squeeze一下，也就是说直接对输入降一下维度，比如把图片的色深降一点，或者把图片平滑一。这个方法其实还有点降维打击的意思，因为如果是benigh的样本的话，按道理说这种程度上的变化应该不会使得结果发生太大的变化。但是如果是adversarial,比如就是仰仗那一两个像素点来实现攻击的，那你平滑一下很有可能就会使得攻击失效了。

类似的还包括对图像进行压缩以及使用PCA。
但是这类方法不可避免会导致对于正常样本的accu也下降。
类似的还有采用随机化的方法对数据进行padding或者缩放等等。

###Universal Attack and Defense
这是ICLR今年防御文章里效果最好的一篇，但有趣的是这篇文章只拿到了poster而且分数还不太高。

这篇文章讲我们把attack和defense都统一到同一个框架下来，变成一个min(max())的问题。

具体来说，里面就是要通过perturbation来maxmize loss，外面就是要通过调整网络结构来minimize这个loss。这样从理论上看就非常好看了，后面的求解过程看得我有点云里雾里，但是总体感觉就不那么empieracal了。而且从效果来看，本文也的确要更好一些。

###DeepCloak
这篇文章也很有意思，是说在最后hidden layer到softmax之间加上一些层，然后学出一些mask，这些mask可以把那些adversarial容易利用的feature去掉，这样减小攻击者可以利用的模型容量。

当然这个方法的问题也非常明显，降低正常样本的accu，同时这种方法其实依赖于已知的攻击类型，而且既然是用一个模型，肯定就会有准确度的问题。这个模型会不会也可以攻击呢？这又是另一个嵌套的问题。

——————————————————————————————————————————————————————————————————
不过读这些东西让我对DNN的边界又有了一些新的认识。

大家现在都关注微小扰动造成的攻击，但是其实微小还是不微小，其实重要性都差不多的。如果要用机器学习来构建全自动化的系统，即使是修改很大的样本也不可能依赖人去看，不然这不就成了个悖论。因为对于adversarial的样本，你也一样可以让人来看prediction是不是make sense。那还要模型干什么。。。

发现这个领域的文献实在是太多了，再读几篇。

###MagNet: a Two-Pronged Defense against Adversarial Examples
一直在考虑那些perturbate比较严重的情况下，如何检测？
本文给出了一种思路，即
训练一个autoencoder，这个autoencoder捕捉到了正常数据的feature，然后用reconstruction error来estimate一个样本到manifold的距离。
如果一个样本距离正常样本的manifold比较远，那么说明可能是对抗样本。
但是实际上今年ICLR上, Dawn Song组的文章已经讨论过对抗样本的manifold问题，有的对抗样本距离正常样本的manifold实际上并不远。
本文的另一个思路是，对于距离正常样本manifold比较远的样本，就用autoencoder重建的样本放到网络中得到softmax output。如果原样本与经过autoencoder重建的样本经过网络得到的softmax输出差异很大，则可能是对抗样本。
文章并没有对这种方法给出详细的解释，可能更多是基于实验发现。

本文还指出可以恢复正常样本的样子，这一点其实简单地对对抗样本增加随机扰动就可以很大概率恢复其正常label，至少我自己的实验发现对fgsm是很容易的。但是作者认为随机扰动没有利用正常样本本来的分布信息，因此提出在正常样本上训练一个autoencoder，然后对于对对抗样本，用autoencoder的输出来作为对其的恢复，因为autoencoder实际上是尽量把对抗样本向正常样本的方向推进了一些。

