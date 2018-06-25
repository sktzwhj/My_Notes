#GAN

##generator

vector -> generator -> matrix (e.g., image)

from generator -> matrix, if you are generating image, you can use deconvolutional layer before

##descriminator

matrix -> discriminator -> score

##GAN is a structured learning problem

classification/regression/structured learning

outputs are different-> class/scalar/components with dependancy

##Why structured learning is hard?
1. zero/one shot 
2. machine has to learn to do planing
e.g., you have to generate meaningful images/voices, etc. 
so for structured learning, the approaches can be classified into
(1) bottom up
learn to generate the object at the component level (generator)
(2) top down 
evaluating the whole object, and find the best one (discriminator)

##conditional generation
###why not generator learn by itself?
e.g., we can use an autoencoder to get a lower-dimensional vector for each image, then use the vector as input and the image as the output to train the generator. 

The decocder in autoencoder can be used as a generator. 

but the problem is: you may able to generate valid images by vectors like [0,1] and [1,0]. But the linear combination of them may not able to generate any meaningful images. 

A solution is Variational Auto-Encoder (minimize reconstruction error)

potential problem?
optimization target - generated image be closer enough to the target.
it will be fine if the generator can truly copy the target image. nothing interesting...
we hope the generator can make a little bit error to increase the diversity of output images. then the important thing is what mistakes are fine. this error cannot be measured by pixel-wise comparisons.

you need to model the co-relationships between pixels. you can use very deep RNN which may be hard to train.

###Why not the discriminator does not do by itself?
You can regard it as a binary classifcation,

discriminator has other names - evaluation fucntion, potential fucntion, energy function

using discriminator to generate object by itself?
It is easier to catch the relation between the components by discriminator. 
we can enumerate a lot of objects and find those that maximize the score. 
(is that feasible?)

How to learn the discriminator?
Because we only have good images but no negative samples so that we cannot learn.

we can randomly generate some noise. but we cannot learn a good discriminator. The key is that we need to have decent fake images. 

Then the question becomes how to generate those realistic negative examples?

##That's why we need GAN. 

generator v.s. discriminator

generator
pros - easy to generate even with deep model cons- hard to learn the correlation between components

discriminator
pros - considering the big picture cons - generation is not feasible. 

generator can be used to generate feasible the results of argmax for the discriminator. 

##How to implement the GAN

vector (code) -> NN generator -> image (actually it is a hidden layer which has the same size with the image you want to generate) -> discriminator -> score. (the architecture of GAN)

##How to train?
(1) initilize generator and discriminator. (random for both)
in each iteration:
(1) generator generates examples 
(2) train the discriminator - score = 1 for real objects and score = 0 for generated objects. 
(3) fix the discriminator to re-train the generator to generate new examples to enhance the discriminator. 


##Conditional Generation
i.e., gives some descriptions and generate the corresponding objects. 

but how to connect code and attributes we want

GAN + AutoEncoder 

image -> encoder -> code -> generator(pre-trained) -> image
minimize the distance between input image and output image. 

conditional gan, the discriminator needs to check both the input and output of the generator. that is, it not only check if the image is real but also whether it matches the input description. 







