-----------------
Deep Learning
-----------------
The second part of the problem is to create a generalized model that can both recognize and localize the object in the given image. RCNN gives the state-of-art performance in object detection. To make use of the RCNN for our usecase, we need a lot of training images. Since we dealt with very less training images, we used data augmentation techniques to create training data.

We explored both Fast-RCNN [fast_rcnn]_ and Faster-RCNN [faster_rcnn]_ methods. Fast-RCNN uses Selective search region proposals. Faster-RCNN uses RPN network to learn the region proposals. In the Fast-RCNN method, we replaced the in-built selective search proposal method with our own set of region proposals. Since the scale is known for all the products through the planogram, we created a set of region proposals using sliding-window approach for all possible box sizes.