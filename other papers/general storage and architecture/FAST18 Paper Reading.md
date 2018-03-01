#FAST2018 paper reading

##1.UKSM: Swift Mmeory Deduplication via Hierachical and Adaptive Memory Region Distilling

来自南京大学的一篇文章。
总体来讲，算是将application hint用到了memory deduplication。具体来说:

总体想法
1.适合进行内存去重的内存页应该是not COW-broken or freed，否则得不偿失
2.尽量降低去重的开销。

观察
1. 同一内存区域的内存往往呈现出类似的去重模式
2. 可以将内存标记为 COW-broken or freed, short-lived, statically-duplicated以及sparse
3. prioritize pages in statically-duplicated regions.

问题就变成了如何快速高效来对这些区域进行标记。

本文用采样的方法来估计去重率与CoW rate，为了降低强哈希算法的开销，采用了progressive partial hashing的方法。

Partial hashing实际上之前就有人提出过[XDE]，本文的出发点是说不同应用数据在进行partial hashing的时候，数据长度应该是不同的。例子比较形象，对于图片，像素区域之间的差异实际比较小，但是对于加密数据，不同数据的差异实际上比较大。

Memory region characterization:
Deduplication-friendly -> many statically-duplicated pages
metrics to study the deduplication effects over a specific kind of regions
1. deduplication gain -> memory saving
2. deduplication loss -> CPU consumption
3. performance impact -> slowdown brought to a running application

##2. ALACC: Accelerating Restore Performance of Data Deduplication Systems Using Adaptive Look-Ahead Window Assisted Chunk Caching
来自U of Minnesota, Twin Cities的一篇文章，感觉他们把ARC cache的思想拿过来做了很多adaptive的缓存。也可以说，ARC其实是一种很好的缓存设计思想，灵活用一下还是有很多玩法。

读性能长期是去重当中需要着重考虑的一个问题，由于碎片化和读放大等导致的读性能问题非常严重。
关于提高读性能实际上有很多方法，比如forward assembly, container-based caching以及chunk-based caching.

forward assembly - read ahead the recipe and allocate the data chunks to the buffers in the forward assembly area
container-based caching - cache the read-out container for future use.
chunk-based caching - cache a subset of data chunks for future use. 

motivation of this paper - the performance of the above-mentioned methods vary. how to combine them and get a good result

this paper - hybrid scheme which combines chunk-based caching and forward assembly, the sizes of the look-ahead window, chunk cache and FAA are dynamically adjusted to reflect the future access information in the recipe. 
