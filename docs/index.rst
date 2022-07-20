#######################################
Exploring the Hubble Ultra Deep Field
#######################################

=============
Introduction
=============

The Hubble Ultra Deep Field (HUDF), also known (due to a re-branding exercise) as the `eXtreme Deep Field (XDF) <http://xdf.ucolick.org>`_ , is the Hubble Space Telescope’s deepest view of the Universe.
The aim of this project is to become familiar with analysing Hubble imaging using python. The ultimate goal is to identify candidate high-redshift galaxies. 


Astronomical images
-------------------

Astronomical cameras are typically sensitive to a broad wavelength range. To gain spectral information we must combine the camera (detector) with a filter that is only transparent to light over a (typically) small range of wavelengths, typically O(100nm). These individual images are monochromatic (i.e. they contain no colour information) and can thus be represented by a simple two-dimensional array where each element of the array denotes the signal in that pixel. Images in several filters, or bands, can be combined, as we’ll see to generate colour images.

Astronomical images are typically held in the `Flexible Image Transport System (FITS) <https://en.wikipedia.org/wiki/FITS>`_. In addition to the raw image data FITS file can also contain meta-data in a header and even tabular data. Examples of this meta-data are the values necessary to convert from pixel coordinates (e.g. (x, y)) to a position on the sky.

Uncertainties
-------------
Having quantified uncertainties (errors) is a critical ingredient in science. There are actually several different ways to estimate the uncertainty on, for example, the flux of an object. However, the best is when a noise (often expressed as a weight) image is provided.

About the HUDF images
---------------------
Hubble imaging of the HUDF consists of imaging in 8 optical and near-IR filters stretching from the blue end of the optical ( 400nm) to almost 2000nm in the near-IR. These filters are named (from blue to red) f435w, f606w, f775w, f850lp, f105w, f125w, f140w, and f160w. The first 4 were obtained with the Advanced Camera for Surveys (ACS) while the final 4 were obtained with Wide Field Camera 3 (WFC3).

The filter transmission curves for these filters, showing the fraction of light transmitted through each filter as a function of wavelength, are shown in Figure 1. 

For each filter there are a pair of images: a science (sci) and weight (wht) image. These respectively contain the signal in electrons per second (e/s), and an estimate of the noise in each pixel. The noise can be estimated from the weight according to:

.. role:: raw-math(raw)
    :format: latex html
    
:raw-math:`$$ noise = \frac{1}{\sqrt{weight}} $$`
    

Because of the way these high-level science images were constructed most of the pixels in these images are actually empty (unobserved). For this reason a mask is also provided allowing you to easily mask empty and other unwanted pixels.

|

.. figure:: /Images/filters.png 
   :width: 500
   :alt: Figure 1
   
   **Figure 1:** Hubble filters used to observe the HUDF.
  
|

This project
------------
In this project you will learn how to analyse *Hubble* images using python through a series of task. In addition to numpy, scipy, and matplotlib, you will also need to install astropy and photuils. To aid you there are a series of examples in `Examples </Examples/Examples.ipynb>`_.

|
  
=======================
1  Basic image analysis
=======================
We’ll begin with a few basic python image analysis tasks to get you started.

1.1  Working with pixels
-------------------------
First, we’ll look at analysing the pixel data in the image. `example1 </Examples/example1.ipynb>`_ demonstrates how to read in the image data and convert it to an array of pixel values.

|

========  ========
❓         **TASK 1A:** *Pixel Distribution*
========  ========
|         First, model the noise as a gaussian centred at zero and estimate σ for the F105W band. **Hint:** there should be no signal contribution to the negative   pixels so you can use them to measure σ. To do this first exclude positive pixels. σ will then simply be −P31.7 (i.e. the negative of the 31.7th percentile). Next, exclude pixels with magnitude > 10σ and plot both a density histogram (**Hint:** use plt.hist(..., density = True)) of the pixel distribution and a normal distribution with the same σ as you’ve just calculated. They won’t align perfectly as the pixel distribution unsurprisingly contains more positive pixels.
========  ========

1.2  Cutting out an image
-------------------------
Often we only want to analyse a small portion (a cutout) of an image instead of the full image. This can be done by slicing the image array, for example cutout = img[xmin:xmax, xmin:xmax] or via a python slice. An example of slicing is given in `example2 </Examples/example2.ipynb>`_.
  
  
1.3  Making plots of images
---------------------------
We’ll now look at exploring some image data. The image data you’ve read in is simply stored as a 2D array of pixel values. As such we can simply use *plt.imshow(image)* to produce a plot of the image. `example2 </Examples/example2.ipynb>`_ demonstrates how to do this.

|

========  ========
❓         **TASK 1B:** *Weight Map*
========  ========
|         Produce plots of each un-masked weight map. You should do this efficiently with a loop: **do not** simply repeat the code 8 times. You should notice that the weight maps for the f435w, f606w, f775w, and f850lp are different from those for f105w, f125w, f140w, and f160w. This is because images in the former filters were obtained using the advanced camera for surveys (ACS) instrument while the latter were obtained with Wide Field Camera 3 (WFC3). ACS and WFC3 have different field-of-views. For the WFC3 filters also notice the "holes" in the weight maps corresponding to bad areas of the detector (camera). 
========  ========

|

.. figure:: /Images/XDF_centre_f125w.jpg
   :width: 300
   :alt: Figure 2

   **Figure 2:** Plot of the trimmed centre of the F125W-band HUDF created by example2.

|

1.4  Combining (stacking) images
---------------------------------
A common task is to combine images either taken with the same filter (often) or with different filters (occasionally). Doing so boosts the sensitivity of the image, albeit, in the latter case, at the expense of the loss of spectral information. To optimise the sensitivity images should be combined by weighting each image with its corresponding weight image. An example of this process is shown in `example4 </Examples/example4.ipynb>`_.
  
1.5  Making colour images
--------------------------
Most people’s experience with *Hubble* imaging is from the glorious colour images available here. As explained in the introduction *Hubble’s* does not capture 'colour' images. Instead images in multiple filters are combined together. To obtain 'full-colour' requires at least 3 filters, thereby mimicking the human visual system. The simplest application is to simply map 3 filters to the red (R), green (G), and blue (B) channels. `example3 </Examples/example3.ipynb>`_ demonstrates how to do this using 3 of the ACS bands. Figure 3 shows one of the outputs of `example3 </Examples/example3.ipynb>`_.

|

.. figure:: /Images/XDF_centre_rgb.jpg 
   :width: 300
   :alt: Figure 3
   
   **Figure 3:** RGB image of the centre of the F125W-band HUDF created by example3.

|

========  ========
❓         **TASK 1C:** *RGB Image*
========  ========
|         Using `example3 </Examples/example3.ipynb>`_ and `example4 </Examples/example4.ipynb>`_ as guides produce a false-colour image of the entire masked XDF using <ins>all 8 filters</ins>. You should define 3 groups of consecutive filters (e.g. ['f435w','f606w'], ['f775w','f850lp'], ['f105w','f125w','f140w','f160w']), combine each group, and then combine those stacks together into an RGB image. Congratulations you’ve now created your own pretty HUDF image. By choosing different filters in each group and playing with the scaling you can make an entirely unique and original version.
========  ========

|

==================================
2  Detecting and measuring sources
==================================

The next part of the project concentrates on identifying, and measuring the properties of sources or objects.

========  ========
❓         **TASK 2A:** *Detection Image*
========  ========
|         First of all, following `example4 </Examples/example4.ipynb>`_, create a detection science and weight image by stacking the F105W, F125W, F140W, and F160W images together. You will use this image to detect faint sources.
========  ========
 
|
 
2.1  Significance maps
-----------------------
To identify sources we need to have an estimate of the noise in each pixel. In the context of *Hubble* this is provided by the weight (wht) map in each filter. The values in this image correspond to:

.. role:: raw-math(raw)
    :format: latex html
    
:raw-math:`$$ weight = \frac{1}{noise^2} $$`

By dividing the signal (science, or sci) map by the noise map (derived from the weight map) we can obtain a significance map, essentially the sigma-to-noise in every pixel. `example5 </Examples/example5.ipynb>`_ demonstrates this and Figure 4 shows the output.
 
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
`Segmentation <https://en.wikipedia.org/wiki/Image_segmentation>`_ is one way of detecting sources (objects) in an image. In the simplest implementation we can identify collections of connected pixels which are all above some threshold. Simple segmentation is controlled by two parameters: the minimum number of connected pixels *n<sub>pixels</sub>* and the required significance *threshold* for each pixel. `example6 </Examples/example6.ipynb>`_ demonstrates the use of simple segmentation routines using the *astropy.photutils* module with the results of simple segmentation shown in Figure 5.

|

.. figure:: /Images/segm.png 
   :width: 300
   :alt: Figure 5
   
   **Figure 5:** F125W segmentation map assuming n\ :sub:`pixels` = 5 and threshold = 2.5.


One problem with simple segmentation like this is that nearby objects are often merged together. To
overcome this we can use de-blending techniques, again this is demonstrated in `example6 </Examples/example6.ipynb>`_.

|

========  ========
❓         **TASK 2C:** *Detecting Sources with Segmentation*
========  ========
|         Create a segmentation image (with no de-blending) of the same region you looked at in 2b. Assuming *n<sub>pixels</sub> = 5* and *threshold = 2.5*. Next, systematically explore the impact of changing npixels (must bean integer) and threshold on the number of sources detected.
========  ========

|

========  ========
❓         **TASK 2D:** *The impact of de-blending*
========  ========
|         Sticking with *n<sub>pixels</sub> = 5* and *threshold = 2.5* now explore the impact of the parameters that control de-blending on the number of sources. 
========  ========

|

2.3  Measuring the signal (and noise) of sources
------------------------------------------------
Our next task is to measure the signal (and noise) of our sources. Again, there are many of ways of doing this. We’ll start off by simply summing the flux in the segmentation region of each object. This is sometimes referred to as an *isophotal* flux though technically this is only truly isophotal if the noise is uniform. This is demonstrated in `example7 </Examples/example7.ipynb>`_ and `example8 </Examples/example8.ipynb>`_.

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


A popular alternative is to simply place an aperture over each source and calculate the flux through in that aperture. This can be done easily using *photutils.aperture*. This is demonstrated in `example9 </Examples/example9.ipynb>`_.

|

========  ========
❓         **TASK 2G:** *Aperture photometry STRETCH*
========  ========
|          Repeat Task 2F but using aperture photometry instead. Assume an aperture 5 pixels in radius.
========  ========

|

===========================
3  Finding distant galaxies
===========================
High-redshift galaxies can be identified using the Lyman-break technique. This takes advantage of a strong break in the spectrum of galaxies caused by the absorption of ionising photons by inter-stellar and inter-galactic hydrogen.

3.1  Changing units
-------------------
The units of the original images are electrons per second (e/s). However, we want units of flux^2, for example in nano-Jansky (nJy). The conversion from from e/s to nJy depends on the observatory, instrument, and filter, and thus is unique for each filter: `example10 </Examples/example10.ipynb>`_ contains the relevant conversion in the form of a dictionary.

|

========  ========
❓         **TASK 3A:** *Convert to Flux*
========  ========
|           Read in the catalogue you created in Task 2f and convert the signal into a flux (nJy) using the conversion dictionary in example9.py. Plot f\ :sub:`f105w` / f\ :sub:`125w` vs. f\ :sub:`f850lp` /f\ :sub:`105w` for all the objects in the catalogue. 
========  ========

|

3.2  Finding distant galaxies
-----------------------------
Firstly, we want to guard against objects which are detected a low-S/N, as these are more likely to be contaminants (or not even real sources). To do this we can simply place a constraint on the signal-to-noise (S/N) in a filter where we know any real high-redshift object should be detected. We are somewhat free to choose the band and threshold but f\ :sub:`f125w` and a S/N> 10 is a reasonable choice. 

Next, we know that high-redshift galaxies have a strong spectral break. If the break falls between two bands A and B we’d expect that f\ :sub:`A` /f\ :sub:`B` should be small. Galaxies at z ∼ 7 have a break between the *f850lp* and *f105w* bands. A reasonable choice of ratio upper-limit is ∼ 0.4.

We also expect the shape of the continuum above the break to be flat, or even negative (i.e. decreasing to longer-wavelength). Using a pair of bands above the break (e.g. *f105w* and *f125w*) we can then place an additional constraint allowing us to further weed out contamination. A reasonable choice for ratio lower-limit is ∼ 0.75. 

Finally, any truly high-redshift object should be undetected in any filter shortward of the break. For z ∼7 objects we wouldn’t expect them to be detected in *f435w*, *f606w*, or *f775w*. This can be implemented by enforcing that any candidate object is detected at less than S/N= 2 in those bands.

In conclusion, our selection criteria can be expressed as follows:

.. class:: center

- S/N(f\ :sub:`f125w` ) > 10 

- f\ :sub:`f850lp` / f\ :sub:`f105w` < 0.4 

- f\ :sub:`f105w` / f\ :sub:`f125w` > 0.75 

- S/N(f\ :sub:`f435w` ) < 2 ∧ S/N(f\ :sub:`f606w` ) < 2 ∧ S/N(f\ :sub:`f775w` ) < 2 

|
|

========  ========
❓         **TASK 3B:** *Identify high-redshift galaxy candidates*
========  ========
|           Add the above flux-ratio criteria to your plot from 3a (either as lines or a shaded region). Apply the criteria to your catalogue of objects and highlight any objects meeting the criteria on your plot.
========  ========

|

========  ========
❓         **TASK 3C:** *Detection image thumbnail*
========  ========
|          Using `example7 </Examples/example7.ipynb>`_ as a guide make detection image thumbnail of your candidate(s), if you have any.
========  ========

|

========  ========
❓         **TASK 3D:** *More thumbnails*
========  ========
|          Following on from 3c also make thumbnails in each band (**Hint:** use *subplots* for ease) in addition to an RGB thumbnail.
========  ========

|

========  ========
❓         **TASK 3E:** *Aperture photometry STRETCH*
========  ========
|          Repeat 3a but using your new aperture photometry based catalogue instead. Produce a plot comparing the flux ratios with the different methods.
========  ========
