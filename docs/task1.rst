=======================
TASK 1:  *Basic image analysis*
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

.. figure:: /docs/Images/XDF_centre_rgb.jpg 
   :width: 300
   :alt: Figure 3
   
   **Figure 3:** RGB image of the centre of the F125W-band HUDF created by example3.

|

========  ========
❓         **TASK 1C:** *RGB Image*
========  ========
|         Using `example3 </Examples/example3.ipynb>`_ and `example4 </Examples/example4.ipynb>`_ as guides produce a false-colour image of the entire masked XDF using <ins>all 8 filters</ins>. You should define 3 groups of consecutive filters (e.g. ['f435w','f606w'], ['f775w','f850lp'], ['f105w','f125w','f140w','f160w']), combine each group, and then combine those stacks together into an RGB image. Congratulations you’ve now created your own pretty HUDF image. By choosing different filters in each group and playing with the scaling you can make an entirely unique and original version.
========  ========
