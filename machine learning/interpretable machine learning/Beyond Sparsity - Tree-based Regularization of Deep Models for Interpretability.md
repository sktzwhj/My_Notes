#Beyound Sparsity: Tree-based Regularization of Deep Models for Interpretability
##Authors: Mike Wu et al. from Stanford Uni
##Published in AAAI'18 (previous version in NIPS workshop)

It is really popular recently to do joint optimizations between DNN and some other models. 

The differetiable boundary tree learns a concise representation by using boundary tree as a measure for complexity.This paper uses decision tree (the avg length of decision path) to learn a model that requires less nodes to mimic.

The motivation to choose recurrent neural network is still not clear for me...What will happen if using this in simple classification problem?

However, for image data, this method may not be applicable because non-structural data may result in huge decision no matter how you do the optimization.
