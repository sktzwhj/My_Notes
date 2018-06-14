#Potluck: Cross-Application Approximation Deduplication for Computation-Intensive Mobile Applications
##Authors: Peizhen Guo and Wenjun Hu
##Published in ASPLOS'18

Kinda impressed to see such kind of application papers published in ASPLOS. 

But the idea of this paper is quite interesting. Rather than deduplicating storage space as most work does, they are trying to deduplicate the computation (although not quite new, some similar work has been done for virtual machine versions). 

I am a bit curious about the validity of the motivation in real-world scenarios. Multiple applications share similar input and computation procedures so that we could cache the results of one's computation for the use of another. 