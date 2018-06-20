#mLSM - Making Authenticated Storage Faster in Ethereum
##Authors: Pandian Raju et al. from  UTA and VMWare
##Published in HotStorage'18

This paper is interesting as it combines the blockchain research with such low-level storage design. Most blockchain researchers, as I know, would regard the underlying infrastructures as black boxes. However, the practical implementation matters for such a big system. 

The authors say that the current merkle tree in Ethereum (patricia tree) design introduces too much read and write amplifications. Therefore, they design some merkle-LSM to solve the problem. 

This is some initial stage research and not much experimental results are available. Looking forward to their progress and it is also some hints for us to design application-specific infrastructu

