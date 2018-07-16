#Simple Understanding of batch normalization

batch normalization is similar to normalizing the input data. The functionality of it is to help the later layers of a deep neural network to stand on a more stable ground. Otherwise, slight change in the first several layers would have very significant impact on the later layer so that it takes longer to learn. Or possibly we cannot train the network due to gradient explosion. 

The alpha and beta parameters in the batch norm can make the batch norm more flexible. In other words, if the network did not find the default normalization help the training process, it can adapt the parameters so that it can even recover the original input. 