#Bias and variance 

About bias and variance, one of the best explanations I like is:

for a ML problem, we have real world distribution, training data and testing data. 
In real scenarios, we do not have testing data and have no idea about its distribution. 
However, our target is to get a good performance on the testing data. 

real world --bias---> training data (observation) ---variance---> testing data

as indicated by the above relationships. the bias is the model's ability on fitting the whole dataset while variance is whether the model is sensitive to individual training points.

for bias, if we use a complex model, it is likely to fit the training data better. so the bias can be smaller. however, if we want the model to generalize well, it should not be too complex so that would not be influenced much by the individual train points. This indicates the low variance. 

In traditional ML models, the bias and variance are contradicted. However, in deep learning, you can optimize both of them at the same time. Specifically, you can add the number of hidden layers and the number of neurons, or train the model with longer time. To reduce the variance, we can use different regularization methods