#numpy and images in python

##How to show float lists as gray image

a trick is to scale the float 

so we can do the followings,

img = numpy.array(list).reshape((M,N)), M,N are the dimensions of the img
then simply do plt.imshow(img, cmp = 'gray', clim = (0, 1))