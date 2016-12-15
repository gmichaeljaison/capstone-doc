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

Dataset
=======
* We had pano6 annotated from Bossanova. We selected first 97 products to test all scenarios.
* We manually annotated pano7. The overlap with the above 97 products was 77. So we have 77 common products with ground truth between pano6 and pano7.
* This is used for further experiments.

Classification
==============

.. image:: /imgs/classification.png

Data Augmentation is used to create training images to train the network. Please refer the Data Augmenation page for more details. Approximately 400 training images per class are created. Then we finetuned the AlexNet architecture which is pretrained on ImageNet.

Experiments
-----------
We experiemented with web only, pano only and web + pano combinations. The Classification Results are shown below.

We experimented with both AlexNet and VGG-16 architecture for classification. VGG-16 gave 5% more accuracy than AlexNet. The results shown below are from AlexNet.

.. image:: /imgs/cls-results.png

The time to train the AlexNet for 40,000 iteration in Caffe is approximately 2-3 hours, and in VGG-16 is 4-5 hours.

Detection
=========

.. image:: /imgs/detection.png

We used ZF-Net architecture for detection pipeline. The region proposal ratio is changed from [0.5, 1, 2] to [0.75, 1, 1.25]. This is mainly to take advantage of the information that majority of the cereal boxes come under these ratios. Apart from that it is the plain Faster RCNN pipeline.

Experiments
-----------
We experimented with pano only and pano + web option. We have pano7 as training images and pano6 for testing. Pano7 have proper annotation.

The Detection results are shown below. The graph shown below is Recall-IOU curve. The x-axis denotes the IOU threshold that is used to measure the accuracy of the system (y-axis). 

.. image:: /imgs/det-results.png

It can be noted that the highest accuracy is obtained when using pano + web option. Also the accuracy started dropping off after the threshold of 0.5. The main reason might be due the fact the pano6 annotation from Bossanova is not accurate.

Please see the slides for more visual results.

.. images:: /imgs/det-example.png


