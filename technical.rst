=================
Technical Details
=================

.. toctree::
    :maxdepth: 2

    template_matching
    deeplearning

Bossa Nova specific details are available in this document.

The problem can be approached in three different ways as follows.

* Feature Matching
* Template Matching
* Deep Learning

-------------
Problem Setup
-------------
There are no manual annotations available for the panorama images. To learn any model, we need training images. Hence the initial idea is to use the planogram information and generate training images from the panoramas. The second part of the problem setup is to use the training images and create a generalized model to do localization and recognition.

-----------------
Prior Information
-----------------

Planogram
---------
**Planogram** has the information about what items has to be placed on what location and how many items are placed together. It is available as a JSON file. Some more information about the JSON file structure can be found in https://sites.google.com/site/bnrcapstone/info/planogram.

We will refer the panorama images as follows.

* `pano2 <https://cmu.app.box.com/files/0/f/6582507945/BNR-20151106_110529EST>`_ - Cereal boxes panorama image.
* `pano5 <https://cmu.app.box.com/files/0/f/6276449141/BNR-20160115_105818EST>`_ - Panorama with tiny cylindrical objects with spices.
* `pano6 <https://cmu.app.box.com/files/0/f/11306722370/A16S>`_ - The panorama for which the manual annotation is available. (A16S aisle)
* `pano7 <https://bnrobotics.box.com/s/maxzqzuj82omqmjbrico93vhu1i2y36p>`_ - Another instance of A16S aisle

To analyze the results well, we took a blind baseline which is directly using the planogram information alone. To analyze the result, we randomly annotated 92 boxes in pano2 and 92 boxes in pano5 that covers all kinds of products. The baseline result for pano2 and pano5 are shown below.

=====   =========
..      Avg. IOU
=====   =========
pano2   67.25%
pano5   44.19%
=====   =========

3D Pointcloud
-------------
We tried using the point cloud information to segment the objects separately. But it did not work as expected. The cereal boxes are so close together and the pointcloud is not very dense.

----------------
Feature Matching
----------------
We explored the Deformable Spatial Pyramid [dsp]_ as the feature matching technique. It splits the image into grids and connects the features together. This worked well for deformable objects like chips packets. The results are

=====   =========
..      Avg. IOU
=====   =========
pano2   69.35%
pano5   53.55%
=====   =========

The advantage with DSP is that it worked well for deformable objects compared with normal HOG template matching. The con is that it takes a very long time to do matching. We used the matlab code available from the authors.
