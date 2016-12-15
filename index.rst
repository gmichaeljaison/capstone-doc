.. instance-recognition documentation master file, created by
   sphinx-quickstart on Sat Nov 26 14:24:48 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to instance-recognition's documentation!
================================================

.. toctree::
   :maxdepth: 2

   overview
   technical
   ref
   contact

Overview
========

General overview of the capstone project **"Fast and Robust Object Instance Recognition"** for the `Bossa Nova Robotics <http://www.bossanova.com/>`_.

The project duration is from ``Jan 2016`` to ``Dec 2016``.

Team Members
------------

* `Michael Jaison Gnanasekar <http://www.michaeljaison.me>`_
* `Shreyas Joshi <https://sites.google.com/site/shreyas25joshi>`_

Faculty Advisors
----------------

* `Martial Hebert <http://www.cs.cmu.edu/~hebert/>`_
* `Deva Ramanan <http://www.cs.cmu.edu/~deva/>`_

Problem Statement
=================

.. image:: /imgs/robot.jpg
	:height: 300px

The project is to develop a robust and high-speed method for recognizing objects in large panorama images containing hundreds of various objects.
The panoramas are captured by a mobile robot, and the objects should be recognized at the speed at which the panorama is produced.

Assumptions
-----------
* There are about 200 objects aligned on a wall of 6ft in height and 40 ft in length.
* The objects are captured by a robot running parallel to the wall using multiple onboard cameras pointing to the wall.
* The images of the entire wall are stitched into a single panorama.
* The objects are moved from time to time so different panoramas will have variations in the objects location, orientation, and presence or absence.
* The objects have a multitude of forms, including boxes, bottles, deformable bags, clothes, of various sizes.
* The vast majority of objects will be front facing.
* Some objects will be shown in top, bottom, or side view.
* Some objects will have variations in their orientations.
* Many objects are repeated multiple times.
* The objects have small variations in distance from the camera.
* The objects various surface reflectivity properties and are illuminated with unequal lighting.
* Students are allowed to label objects manually in training sets.
* The majority of labeled images will show the front view of the object.
* Some objects will be rotated up to 45 degrees from front view.
* 3D point clouds of the scene are available and can be used in the process.

Datasets
--------
* Bossa Nova supplied stitched panorama images with planogram information of 3 different aisles.
* Bossa Nova supplied the 3D point cloud upon request.
* Bossa Nova supplied camera position for each original image upon request.

Public Datasets used
--------------------
* Grocery Product Dataset [groc_dataset]_
* Grozi-120 Dataset UCSD [grozi_dataset]_


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

