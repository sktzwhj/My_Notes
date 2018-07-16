#Generate Adversarial Examples

the idea of generating adversarial examples is just to perturbate the input image according to the loss function which tries to minimize the distance between the model prediction and the target adversarial label. 

some interesting ideas to defense is to use the JPEG compression to compress the image so that a large portion of the noise can be removed. 

not only deep nets, many other simple models like linear regression, softmax regression or even kNN

1. initially, the phenomenon is regarded as a sign of overfitting
2. but if overfitting is the problem, if we change the model, we should be able to see some new random mistakes
3. but a lot of models are actually sharing many similar adversarial examples
4. so it might be a sign of underfitting
5. linear models give unexpected high confidence for something far from the decision boundary even there are no points seen there. 
6. modern deep nets are very piecewise linear
7. the piecewise linear means the relationship between input and output is very linear. it's not saying that the relationship between the parametwers and the output are quite linear

Methods to generate the adversarial examples
1. FGSM Fast Gradient Sign Method
J(x^~, \theta) \a= J(x, \theta) + (x^~ - x)^T\delta_x J(x)

Tramer et al. has a paper talking about how many dimensions are actually adversarial. e.g., in MNIST dataset, around 25 directions exist. 

the Papernot 2016 paper tells about the cross-technique transferability for adversarial examples. it is interesting to see that the transferability from DNN to kNN is the lowest compared with DNN to other models. 