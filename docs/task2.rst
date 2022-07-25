==================================
TASK 2:  *Detecting and measuring sources*
==================================

The next part of the project concentrates on identifying, and measuring the properties of sources or objects.

========  ========
❓         **TASK 2A:** *Detection Image*
========  ========
|         First of all, following :ref:`Example4`, create a detection science and weight image by stacking the F105W, F125W, F140W, and F160W images together. You will use this image to detect faint sources.
========  ========
 
|
 
2.1  Significance maps
-----------------------
To identify sources we need to have an estimate of the noise in each pixel. In the context of *Hubble* this is provided by the weight (wht) map in each filter. The values in this image correspond to:

:math:`$$ weight = \frac{1}{noise^2} $$`

By dividing the signal (science, or sci) map by the noise map (derived from the weight map) we can obtain a significance map, essentially the sigma-to-noise in every pixel. :ref:`Example5` demonstrates this and Figure 4 shows the output.
 
|

.. figure:: /Images/significance_map.jpg
   :width: 300
   :alt: Figure 4
   
   **Figure 4:** F105W significance image of the centre of the HUDF created by example5. Pixels coloured in grey have a signal-to-noise < 2 with the colour scale stretching from −2 to 2. Coloured pixels have a signal-to-noise > 2 with a scale stretching from 2 to 50.

|

========  ========
❓         **TASK 2B:** *Significance map*
========  ========
|         Create a significance map of a 400 pixel wide area centred on (3100, 1800).
========  ========

|

2.2  Segmentation
-----------------
`Segmentation <https://en.wikipedia.org/wiki/Image_segmentation>`_ is one way of detecting sources (objects) in an image. In the simplest implementation we can identify collections of connected pixels which are all above some threshold. Simple segmentation is controlled by two parameters: the minimum number of connected pixels n\ :sub:`pixels`\  and the required significance *threshold* for each pixel. :ref:`Example6` demonstrates the use of simple segmentation routines using the *astropy.photutils* module with the results of simple segmentation shown in Figure 5.

|

.. figure:: /Images/segm.png 
   :width: 300
   :alt: Figure 5
   
   **Figure 5:** F125W segmentation map assuming n\ :sub:`pixels` = 5 and threshold = 2.5.


One problem with simple segmentation like this is that nearby objects are often merged together. To
overcome this we can use de-blending techniques, again this is demonstrated in :ref:`Example6`.

|

========  ========
❓         **TASK 2C:** *Detecting Sources with Segmentation*
========  ========
|         Create a segmentation image (with no de-blending) of the same region you looked at in 2b. Assuming n\ :sub:`pixels` = 5 and *threshold = 2.5*. Next, systematically explore the impact of changing npixels (must bean integer) and threshold on the number of sources detected.
========  ========

|

========  ========
❓         **TASK 2D:** *The impact of de-blending*
========  ========
|         Sticking with n\ :sub:`pixels` = 5 and *threshold = 2.5* now explore the impact of the parameters that control de-blending on the number of sources. 
========  ========

|

2.3  Measuring the signal (and noise) of sources
------------------------------------------------
Our next task is to measure the signal (and noise) of our sources. Again, there are many of ways of doing this. We’ll start off by simply summing the flux in the segmentation region of each object. This is sometimes referred to as an *isophotal* flux though technically this is only truly isophotal if the noise is uniform. This is demonstrated in :ref:`Example7` and :ref:`Example8`.

|

========  ========
❓         **TASK 2E:** *Measure the signal of all sources*
========  ========
|         Measure the signal (e/s) of all the sources in the region. To do this you can combine the segmentation map with the detection science image. Plot a histogram. Do the same for the de-blended image and discuss the difference. 
========  ========

|

========  ========
❓         **TASK 2F:** *Make a multi-band catalogue*
========  ========
|         Using the original (un-blended) segmentation map measure the signal and noise (or error) of every object in every single filter and create a catalogue using a dictionary. Save this catalogue for use later.
========  ========


A popular alternative is to simply place an aperture over each source and calculate the flux through in that aperture. This can be done easily using *photutils.aperture*. This is demonstrated in :ref:`Example9`.

|

========  ========
❓         **TASK 2G:** *Aperture photometry STRETCH*
========  ========
|          Repeat Task 2F but using aperture photometry instead. Assume an aperture 5 pixels in radius.
========  ========
