The training images are downloaded are upcindex.com. There is a scarcity of training data. On an average, there are around 3~5 training images for class. Hence to fine-tune a deep learning framework, we need a huge amount of traning data and hence a data augmentation step.

-----------------
Data Augmentation
-----------------

We designed the data augmentation for classification and detection to introduce more variance in training data and also to include a mutual context information depicting the scenario of a real retail store.

Data Augmentation for Classification
------------------------------------

For a single source training image I, random brightness in the range (-32, 32), random contrast in the range (0.8, 1.2) is added. Different random backgraound images (just the empty shelves, usually not involving any objects) are taken and each modified source image is overlayed on a random backgraound to create a training image. The process is repeated n times to create n training images per class. The entire process is repeated across all classes to generate n number of images per class. (We choose n=400)

.. image:: /imgs/data_aug_C.png
	:height: 300px

Data Augmentation for Detection
-------------------------------

Similar to classification, a source image I is taken and a random brightness and contrast is added, the images is repeated 3-4 times (or the number of times the backgraound image can accomodate). So the training image will now have class C_i and m repeated boxes. Again this process is repeated n times for each class to generate n training images per class. The entire process is repeated across all classes to generate n number of images per class. (We choose n=400, m=1-5)

.. image:: /imgs/data_aug_D.png
	:height: 300px


Validating Data Augmentation step
----------------------------------

To validate the data augmentation step and the framework for classifiation, we experimented on hte grocery product dataset. We choose 138 classes from the cereals (food category). Each class had one training image.
We acheieved similar results as we achieved for BossaNova dataset. 

To fix on the number of the augmented images we experimented with n=200 and n=500 where n is the number of training images per class.

.. image:: /imgs/data_aug_res.png
	:height: 200px








