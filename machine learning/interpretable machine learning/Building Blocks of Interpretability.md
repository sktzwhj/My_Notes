#Buolding Blocks of Interpretability
##Distill March, 2018

Existing interpretability methods focus on the input/output layers of deep nets because these two layers have clear semantic meanings. 

This paper provides interfaces so that we can map the probabilites to the hidden features which contribute to a certan class. (question: how do they do visualization for hidden neurons?)

pixel may not be the unit when we think about the contributions to the final classification result. Higher-level semantic features should be. 

Basicly, the conventioanl saliency method can tell how much a certain part in the input has contributed to the final probability. This paper drills it down to how a detector contributes to a prediction.

I like the idea of saying human-scale interfaces which are indeed a problem we have met in our own work.
(question: how does they group the neurons to make the interpretation meaningful)