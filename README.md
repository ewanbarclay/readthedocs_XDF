# Exploring the Hubble Ultra Deep Field
## Introduction
The Hubble Ultra Deep Field (HUDF), also known (due to a re-branding exercise) as the [eXtreme Deep Field (XDF)](http://xdf.ucolick.org), is the Hubble Space Telescope’s deepest view of the Universe.
The aim of this project is to become familiar with analysing Hubble imaging using python. The ultimate goal is to identify candidate high-redshift galaxies.
### Astronomical images
Astronomical cameras are typically sensitive to a broad wavelength range. To gain spectral information we must combine the camera (detector) with a filter that is only transparent to light over a (typically) small range of wavelengths, typically O(100nm). These individual images are monochromatic (i.e. they contain no colour information) and can thus be represented by a simple two-dimensional array where each element of the array denotes the signal in that pixel. Images in several filters, or bands, can be combined, as we’ll see to generate colour images.

Astronomical images are typically held in the [Flexible Image Transport System (FITS)](https://en.wikipedia.org/wiki/FITS). In addition to the raw image data FITS file can also contain meta-data in a header and even tabular data. Examples of this meta-data are the values necessary to convert from pixel coordinates (e.g. (x, y)) to a position on the sky.
#### Uncertainties
Having quantified uncertainties (errors) is a critical ingredient in science. There are actually several different ways to estimate the uncertainty on, for example, the flux of an object. However, the best is when a noise (often expressed as a weight) image is provided.
### About the HUDF images
Hubble imaging of the HUDF consists of imaging in 8 optical and near-IR filters stretching from the blue end of the optical ( 400nm) to almost 2000nm in the near-IR. These filters are named (from blue to red) f435w, f606w, f775w, f850lp, f105w, f125w, f140w, and f160w. The first 4 were obtained with the Advanced Camera for Surveys (ACS) while the final 4 were obtained with Wide Field Camera 3 (WFC3).

The filter transmission curves for these filters, showing the fraction of light transmitted through each filter as a function of wavelength, are shown in Figure. For each filter there are a pair of images: a science (sci) and weight (wht) image. These respectively contain the signal in electrons per second (e/s), and an estimate of the noise in each pixel. The noise can be estimated from the weight according to:

$$ noise = {1 \over \sqrt{weight}} $$

Because of the way these high-level science images were constructed most of the pixels in these images are actually empty (unobserved). For this reason a mask is also provided allowing you to easily mask empty and other unwanted pixels.

<figure>
<p align="center">
  <img src="/Images/filters.png" alt="Trulli" style="width:60%" align = "center">
</p>
<p align = "center">
Figure 1: Hubble filters used to observe the HUDF.
</p>

  
#### This project
In this project you will learn how to analyse *Hubble* images using python through a series of task. In addition to numpy, scipy, and matplotlib, you will also need to install astropy and photuils. To aid you there are a series of examples in [Examples](/Examples/Examples.html).
## 1  Basic image analysis
We’ll begin with a few basic python image analysis tasks to get you started.
### 1.1  Working with pixels
First, we’ll look at analysing the pixel data in the image. [example1](/Examples/example1.ipynb) demonstrates how to read in the image data and convert it to an array of pixel values.

