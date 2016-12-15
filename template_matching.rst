-----------------
Template Matching
-----------------
The straighforward way to do template matching is to use grayscale or rgb image directly. Another way is to use HOG features to do template matching. Even though HOG features does not have the color information, it matches the structure or pattern in the image. It worked well for the cereal boxes kind of images. The results are as follows.

=====   ======= ======  ======
..      Gray    RGB     HOG 
=====   ======= ======  ======
pano2   71.85%  73.96%  79.59%
pano5   45.11%  47.34%  57.57%
=====   ======= ======  ======

The above result used the planogram information to search only in the nearby region. One another information that is available from the planogram is the number of instances to search for. The idea is to search for n objects together based on the order in the planogram. This method is referred as part-based template matching.

Part-based template matching
----------------------------
Item level matching had difficulty in mapping all the instances. It had more false positives as well. To make use of the planogram information about the number of instances, we modelled each instance as a part of the model. This allows a small deformation among each part of the model to match real time scenario. For an image like below, the part-based model can be used to recognize all the instances together. The illustration of steps is shown below.

.. image:: /imgs/part1.png
    :height: 150px

.. image:: /imgs/part2.png

.. image:: /imgs/part3.png

.. image:: /imgs/part4.png

The results from the part-based model are given below.

=====   =========
..      Avg. IOU
=====   =========
pano2   82.45%
pano5   63.97%
=====   =========


Deep Template Matching
----------------------
The template matching also heavily relies on the feature space on which the template and image are matched. Even though HOG performed well for rigid objects, the tiny and deformable objects need a better embedding to match. In this approach, we have used Deep features to do template matching.

.. image:: /imgs/tmpl-match.png

We have also combined multiple deep features from different layers together. The results are shown below.

=================== ======  ======
Method              pano2   pano5
=================== ======  ======
HOG + Conv1 + Conv2 81.90%  61.60%
HOG + Conv2         83.90%  60.88%
HOG + Conv4         81.67%  66.30%
HOG + Conv3 + Conv4 81.54%  66.78%
=================== ======  ======

Conclusion
----------
Even though the matching techniques gave higher matching performance, it cannot be completely reliable to create training image automatically. Hence these methods are not used to create training images directly.