-----------------
Deep Learning
-----------------
The second part of the problem is to create a generalized model that can both recognize and localize the object in the given image. RCNN gives the state-of-art performance in object detection. To make use of the RCNN for our usecase, we need a lot of training images. Since we dealt with very less training images, we used data augmentation techniques to create training data.

We explored both Fast-RCNN [fast_rcnn]_ and Faster-RCNN [faster_rcnn]_ methods. Fast-RCNN uses Selective search region proposals. Faster-RCNN uses RPN network to learn the region proposals. In the Fast-RCNN method, we replaced the in-built selective search proposal method with our own set of region proposals. Since the scale is known for all the products through the planogram, we created a set of region proposals using sliding-window approach for all possible box sizes.

In the inital test using one panorama image as training image and another panorama image as test image, for 40 different classes on pano2 (cereal boxes), we got a good accuracy around 85%. This leads the exploration towards RCNN methods.

Problem Setup
=============
The entire problem can be split into 4 quadrants as shown below. 

.. image:: /imgs/problem-setup.png
	:height: 300px

The Green quadrant is supposed to be the easier problem to solve. The Red quadrant is the harder problem to solve. The Red quadrant is a more general solution, in the sense that it does not need human annotations for the panorama images. It only relies on the web images to create a general model.

Components
==========
The components of the RCNN Detection is given below.

.. image:: /imgs/components.png
	:height: 300px

We analyzed the impact of each component to the final performance. The components are

1. Training Images
	- what kind of training images help learn better?
	- Web Images
	- Panorama Images
	- Annotation
2. Region Proposals
	- Selective search
	- RPN
3. Classification and Regression

To analyze in depth, we changed the detection problem into the Classification problem. The assumption would be that the region proposals are ideal.

Classification
==============

.. image:: /imgs/classification.png

We tried both AlexNet and VGG-16 architecture for classification.

Experiments
-----------

The Classification Results are shown below.

.. image:: /imgs/cls-results.png


Detection
=========

.. image:: /imgs/detection.png

We used ZF-Net architecture for detection pipeline. The region proposal ratio is changed from [0.5, 1, 2] to [0.75, 1, 1.25]. This is mainly to take advantage of the information that majority of the cereal boxes come under these ratios. Apart from that it is the plain Faster RCNN pipeline.


The Detection results are shown below.

.. image:: /imgs/det-results.png


