#On Smart Query Routing: For Distributed Graph Querying with Decoupled Storage
##Authors: Arijit Khan et al. from NTU, ETH and Microsoft Research
##Published in USENIX ATC'18

Key design choices of this paper:

1. decoupled design - processing and storage layers are logically decoupled. 
2. Smart routing built upon the decoupled architecture. 

(1) The routing will consider the localities of the queries. Not only routing the queries on the same node to the same server but also consider the neighboring relationships. (2) maximizing the throughput. In other words, prioritize the queries with more workloads. (3) The decision should be made fast. Say, O(n) time complexity where n is the number of queries. 

Challenges for achieving the above-mentioned targets:

1. trade-offs exist between locality utilization and load balance. 
2. how to know what data exists in which server. (obviously, you cannot go to search the cache given the efficiency)

(1) topology-aware locality
if u and v are nearby nodes, then successive queries on u and v must be sent to the same processor. It is very likely that h-hop neighborhoods of u and v will significantly overlap. but how can you know two nodes are neighbors? storing all edges can be too expensive. 

(2) query stealing
due to the power law, some processors can be quite busy. so we allow the idle processors to steal some queries from those that are too busy.

To solve the topology-aware locality problem, they use a method named landmark routing which is basicly just sample some nodes in the graph as landmarks and pre-compute the distances of the other nodes to the landmarks. 

To know the cache content, they use moving average to 'compute' the content the content. The rationale behind this is that the content can be indexed by the node id. However, I doubt a random assigned node with a very large node id make this assumption in