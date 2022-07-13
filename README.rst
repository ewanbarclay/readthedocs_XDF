Exploring the Hubble Ultra Deep Field
=====================================

Introduction
------------

The Hubble Ultra Deep Field (HUDF), also known (due to a re-branding
exercise) as the `eXtreme Deep Field (XDF) <http://xdf.ucolick.org>`__,
is the Hubble Space Telescope’s deepest view of the Universe. The aim of
this project is to become familiar with analysing Hubble imaging using
python. The ultimate goal is to identify candidate high-redshift
galaxies. ### Astronomical images Astronomical cameras are typically
sensitive to a broad wavelength range. To gain spectral information we
must combine the camera (detector) with a filter that is only
transparent to light over a (typically) small range of wavelengths,
typically O(100nm). These individual images are monochromatic (i.e. they
contain no colour information) and can thus be represented by a simple
two-dimensional array where each element of the array denotes the signal
in that pixel. Images in several filters, or bands, can be combined, as
we’ll see to generate colour images.

Astronomical images are typically held in the `Flexible Image Transport
System (FITS) <https://en.wikipedia.org/wiki/FITS>`__. In addition to
the raw image data FITS file can also contain meta-data in a header and
even tabular data. Examples of this meta-data are the values necessary
to convert from pixel coordinates (e.g. (x, y)) to a position on the
sky. #### Uncertainties Having quantified uncertainties (errors) is a
critical ingredient in science. There are actually several different
ways to estimate the uncertainty on, for example, the flux of an object.
However, the best is when a noise (often expressed as a weight) image is
provided. ### About the HUDF images Hubble imaging of the HUDF consists
of imaging in 8 optical and near-IR filters stretching from the blue end
of the optical ( 400nm) to almost 2000nm in the near-IR. These filters
are named (from blue to red) f435w, f606w, f775w, f850lp, f105w, f125w,
f140w, and f160w. The first 4 were obtained with the Advanced Camera for
Surveys (ACS) while the final 4 were obtained with Wide Field Camera 3
(WFC3).

The filter transmission curves for these filters, showing the fraction
of light transmitted through each filter as a function of wavelength,
are shown in Figure 1.

For each filter there are a pair of images: a science (sci) and weight
(wht) image. These respectively contain the signal in electrons per
second (e/s), and an estimate of the noise in each pixel. The noise can
be estimated from the weight according to:

.. math::  noise = {1 \over \sqrt{weight}} 

Because of the way these high-level science images were constructed most
of the pixels in these images are actually empty (unobserved). For this
reason a mask is also provided allowing you to easily mask empty and
other unwanted pixels.

.. raw:: html

   <figure>

.. raw:: html

   <p align="center">

.. raw:: html

   <figcaption>

.. raw:: html

   <p align="center">

Figure 1: Hubble filters used to observe the HUDF.

.. raw:: html

   </figcaption>

.. raw:: html

   </p>

.. raw:: html

   </figure>

This project
~~~~~~~~~~~~

In this project you will learn how to analyse *Hubble* images using
python through a series of task. In addition to numpy, scipy, and
matplotlib, you will also need to install astropy and photuils. To aid
you there are a series of examples in
`Examples </Examples/Examples.ipynb>`__.

1 Basic image analysis
----------------------

We’ll begin with a few basic python image analysis tasks to get you
started. ### 1.1 Working with pixels First, we’ll look at analysing the
pixel data in the image. `example1 </Examples/example1.ipynb>`__
demonstrates how to read in the image data and convert it to an array of
pixel values.

+----------------------------------------------------------------+-----+
| ❓                                                              | **T |
|                                                                | ASK |
|                                                                | 1A: |
|                                                                | Pi  |
|                                                                | xel |
|                                                                | Di  |
|                                                                | str |
|                                                                | ibu |
|                                                                | tio |
|                                                                | n** |
+================================================================+=====+
|                                                                | Fir |
|                                                                | st, |
|                                                                | mo  |
|                                                                | del |
|                                                                | the |
|                                                                | no  |
|                                                                | ise |
|                                                                | as  |
|                                                                | a   |
|                                                                | ga  |
|                                                                | uss |
|                                                                | ian |
|                                                                | c   |
|                                                                | ent |
|                                                                | red |
|                                                                | at  |
|                                                                | z   |
|                                                                | ero |
|                                                                | and |
|                                                                | es  |
|                                                                | tim |
|                                                                | ate |
|                                                                | σ   |
|                                                                | for |
|                                                                | the |
|                                                                | F1  |
|                                                                | 05W |
|                                                                | ba  |
|                                                                | nd. |
|                                                                | **H |
|                                                                | int |
|                                                                | :** |
|                                                                | th  |
|                                                                | ere |
|                                                                | sho |
|                                                                | uld |
|                                                                | be  |
|                                                                | no  |
|                                                                | sig |
|                                                                | nal |
|                                                                | con |
|                                                                | tri |
|                                                                | but |
|                                                                | ion |
|                                                                | to  |
|                                                                | the |
|                                                                | ne  |
|                                                                | gat |
|                                                                | ive |
|                                                                | pix |
|                                                                | els |
|                                                                | so  |
|                                                                | you |
|                                                                | can |
|                                                                | use |
|                                                                | t   |
|                                                                | hem |
|                                                                | to  |
|                                                                | m   |
|                                                                | eas |
|                                                                | ure |
|                                                                | σ.  |
|                                                                | To  |
|                                                                | do  |
|                                                                | t   |
|                                                                | his |
|                                                                | fi  |
|                                                                | rst |
|                                                                | e   |
|                                                                | xcl |
|                                                                | ude |
|                                                                | po  |
|                                                                | sit |
|                                                                | ive |
|                                                                | p   |
|                                                                | ixe |
|                                                                | ls. |
|                                                                | σ   |
|                                                                | w   |
|                                                                | ill |
|                                                                | t   |
|                                                                | hen |
|                                                                | sim |
|                                                                | ply |
|                                                                | be  |
|                                                                | −P3 |
|                                                                | 1.7 |
|                                                                | (i. |
|                                                                | e.  |
|                                                                | the |
|                                                                | ne  |
|                                                                | gat |
|                                                                | ive |
|                                                                | of  |
|                                                                | the |
|                                                                | 31. |
|                                                                | 7th |
|                                                                | per |
|                                                                | cen |
|                                                                | til |
|                                                                | e). |
|                                                                | Ne  |
|                                                                | xt, |
|                                                                | e   |
|                                                                | xcl |
|                                                                | ude |
|                                                                | pix |
|                                                                | els |
|                                                                | w   |
|                                                                | ith |
|                                                                | mag |
|                                                                | nit |
|                                                                | ude |
|                                                                | >   |
|                                                                | 10σ |
|                                                                | and |
|                                                                | p   |
|                                                                | lot |
|                                                                | b   |
|                                                                | oth |
|                                                                | a   |
|                                                                | d   |
|                                                                | ens |
|                                                                | ity |
|                                                                | his |
|                                                                | tog |
|                                                                | ram |
|                                                                | (   |
|                                                                | **H |
|                                                                | int |
|                                                                | :** |
|                                                                | use |
|                                                                | pl  |
|                                                                | t.h |
|                                                                | ist |
|                                                                | (…, |
|                                                                | d   |
|                                                                | ens |
|                                                                | ity |
|                                                                | =   |
|                                                                | Tru |
|                                                                | e)) |
|                                                                | of  |
|                                                                | the |
|                                                                | pi  |
|                                                                | xel |
|                                                                | dis |
|                                                                | tri |
|                                                                | but |
|                                                                | ion |
|                                                                | and |
|                                                                | a   |
|                                                                | nor |
|                                                                | mal |
|                                                                | dis |
|                                                                | tri |
|                                                                | but |
|                                                                | ion |
|                                                                | w   |
|                                                                | ith |
|                                                                | the |
|                                                                | s   |
|                                                                | ame |
|                                                                | σ   |
|                                                                | as  |
|                                                                | you |
|                                                                | ’ve |
|                                                                | j   |
|                                                                | ust |
|                                                                | ca  |
|                                                                | lcu |
|                                                                | lat |
|                                                                | ed. |
|                                                                | T   |
|                                                                | hey |
|                                                                | wo  |
|                                                                | n’t |
|                                                                | al  |
|                                                                | ign |
|                                                                | per |
|                                                                | fec |
|                                                                | tly |
|                                                                | as  |
|                                                                | the |
|                                                                | pi  |
|                                                                | xel |
|                                                                | dis |
|                                                                | tri |
|                                                                | but |
|                                                                | ion |
|                                                                | un  |
|                                                                | sur |
|                                                                | pri |
|                                                                | sin |
|                                                                | gly |
|                                                                | co  |
|                                                                | nta |
|                                                                | ins |
|                                                                | m   |
|                                                                | ore |
|                                                                | po  |
|                                                                | sit |
|                                                                | ive |
|                                                                | p   |
|                                                                | ixe |
|                                                                | ls. |
+----------------------------------------------------------------+-----+

1.2 Cutting out an image
~~~~~~~~~~~~~~~~~~~~~~~~

Often we only want to analyse a small portion (a cutout) of an image
instead of the full image. This can be done by slicing the image array,
for example cutout = img[xmin:xmax, xmin:xmax] or via a python slice. An
example of slicing is given in `example2 </Examples/example2.ipynb>`__.

1.3 Making plots of images
~~~~~~~~~~~~~~~~~~~~~~~~~~

We’ll now look at exploring some image data. The image data you’ve read
in is simply stored as a 2D array of pixel values. As such we can simply
use plt.imshow(image) to produce a plot of the image.
`example2 </Examples/example2.ipynb>`__ demonstrates how to do this.

+--------------------------------------------------------------+--------+
| ❓                                                            | **TASK |
|                                                              | 1B:    |
|                                                              | Weight |
|                                                              | Map**  |
+==============================================================+========+
|                                                              | P      |
|                                                              | roduce |
|                                                              | plots  |
|                                                              | of     |
|                                                              | each   |
|                                                              | un-    |
|                                                              | masked |
|                                                              | weight |
|                                                              | map.   |
|                                                              | You    |
|                                                              | should |
|                                                              | do     |
|                                                              | this   |
|                                                              | effic  |
|                                                              | iently |
|                                                              | with a |
|                                                              | loop:  |
|                                                              | **do   |
|                                                              | not**  |
|                                                              | simply |
|                                                              | repeat |
|                                                              | the    |
|                                                              | code 8 |
|                                                              | times. |
|                                                              | You    |
|                                                              | should |
|                                                              | notice |
|                                                              | that   |
|                                                              | the    |
|                                                              | weight |
|                                                              | maps   |
|                                                              | for    |
|                                                              | the    |
|                                                              | f435w, |
|                                                              | f606w, |
|                                                              | f775w, |
|                                                              | and    |
|                                                              | f850lp |
|                                                              | are    |
|                                                              | dif    |
|                                                              | ferent |
|                                                              | from   |
|                                                              | those  |
|                                                              | for    |
|                                                              | f105w, |
|                                                              | f125w, |
|                                                              | f140w, |
|                                                              | and    |
|                                                              | f160w. |
|                                                              | This   |
|                                                              | is     |
|                                                              | b      |
|                                                              | ecause |
|                                                              | images |
|                                                              | in the |
|                                                              | former |
|                                                              | f      |
|                                                              | ilters |
|                                                              | were   |
|                                                              | ob     |
|                                                              | tained |
|                                                              | using  |
|                                                              | the    |
|                                                              | ad     |
|                                                              | vanced |
|                                                              | camera |
|                                                              | for    |
|                                                              | s      |
|                                                              | urveys |
|                                                              | (ACS)  |
|                                                              | inst   |
|                                                              | rument |
|                                                              | while  |
|                                                              | the    |
|                                                              | latter |
|                                                              | were   |
|                                                              | ob     |
|                                                              | tained |
|                                                              | with   |
|                                                              | Wide   |
|                                                              | Field  |
|                                                              | Camera |
|                                                              | 3      |
|                                                              | (      |
|                                                              | WFC3). |
|                                                              | ACS    |
|                                                              | and    |
|                                                              | WFC3   |
|                                                              | have   |
|                                                              | dif    |
|                                                              | ferent |
|                                                              | fie    |
|                                                              | ld-of- |
|                                                              | views. |
|                                                              | For    |
|                                                              | the    |
|                                                              | WFC3   |
|                                                              | f      |
|                                                              | ilters |
|                                                              | also   |
|                                                              | notice |
|                                                              | the    |
|                                                              | “      |
|                                                              | holes” |
|                                                              | in the |
|                                                              | weight |
|                                                              | maps   |
|                                                              | c      |
|                                                              | orresp |
|                                                              | onding |
|                                                              | to bad |
|                                                              | areas  |
|                                                              | of the |
|                                                              | de     |
|                                                              | tector |
|                                                              | (ca    |
|                                                              | mera). |
+--------------------------------------------------------------+--------+

.. raw:: html

   <figure>

.. raw:: html

   <p align="center">

.. raw:: html

   </p>

.. raw:: html

   <p align="center">

Figure 2: Plot of the trimmed centre of the F125W-band HUDF created by
`example2 </Examples/example2.ipynb>`__.

.. raw:: html

   </p>

1.4 Combining (stacking) images
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A common task is to combine images either taken with the same filter
(often) or with different filters (occasionally). Doing so boosts the
sensitivity of the image, albeit, in the latter case, at the expense of
the loss of spectral information. To optimise the sensitivity images
should be combined by weighting each image with its corresponding weight
image. An example of this process is shown in
`example4 </Examples/example4.ipynb>`__.

1.5 Making colour images
~~~~~~~~~~~~~~~~~~~~~~~~

Most people’s experience with *Hubble* imaging is from the glorious
colour images available here. As explained in the introduction
*Hubble’s* does not capture ‘colour’ images. Instead images in multiple
filters are combined together. To obtain ‘full-colour’ requires at least
3 filters, thereby mimicking the human visual system. The simplest
application is to simply map 3 filters to the red (R), green (G), and
blue (B) channels. `example3 </Examples/example3.ipynb>`__ demonstrates
how to do this using 3 of the ACS bands. Figure 3 shows one of the
outputs of `example3 </Examples/example3.ipynb>`__.

.. raw:: html

   <figure>

.. raw:: html

   <p align="center">

.. raw:: html

   </p>

.. raw:: html

   <p align="center">

Figure 3: RGB image of the centre of the F125W-band HUDF created by
`example3 </Examples/example3.ipynb>`__.

.. raw:: html

   </p>

+--------------------------------------------------------------+--------+
| ❓                                                            | **TASK |
|                                                              | 1C:    |
|                                                              | RGB    |
|                                                              | I      |
|                                                              | mage** |
+==============================================================+========+
|                                                              | Using  |
|                                                              | `ex    |
|                                                              | ample3 |
|                                                              |  </Exa |
|                                                              | mples/ |
|                                                              | exampl |
|                                                              | e3.ipy |
|                                                              | nb>`__ |
|                                                              | and    |
|                                                              | `ex    |
|                                                              | ample4 |
|                                                              |  </Exa |
|                                                              | mples/ |
|                                                              | exampl |
|                                                              | e4.ipy |
|                                                              | nb>`__ |
|                                                              | as     |
|                                                              | guides |
|                                                              | p      |
|                                                              | roduce |
|                                                              | a      |
|                                                              | false- |
|                                                              | colour |
|                                                              | image  |
|                                                              | of the |
|                                                              | entire |
|                                                              | masked |
|                                                              | XDF    |
|                                                              | using  |
|                                                              | all 8  |
|                                                              | fi     |
|                                                              | lters. |
|                                                              | You    |
|                                                              | should |
|                                                              | define |
|                                                              | 3      |
|                                                              | groups |
|                                                              | of     |
|                                                              | conse  |
|                                                              | cutive |
|                                                              | f      |
|                                                              | ilters |
|                                                              | (e.g.  |
|                                                              | [‘f435 |
|                                                              | w’,‘f6 |
|                                                              | 06w’], |
|                                                              | [      |
|                                                              | ‘f775w |
|                                                              | ’,‘f85 |
|                                                              | 0lp’], |
|                                                              | [‘f10  |
|                                                              | 5w’,‘f |
|                                                              | 125w’, |
|                                                              | ‘f140w |
|                                                              | ’,‘f16 |
|                                                              | 0w’]), |
|                                                              | c      |
|                                                              | ombine |
|                                                              | each   |
|                                                              | group, |
|                                                              | and    |
|                                                              | then   |
|                                                              | c      |
|                                                              | ombine |
|                                                              | those  |
|                                                              | stacks |
|                                                              | to     |
|                                                              | gether |
|                                                              | into   |
|                                                              | an RGB |
|                                                              | image. |
|                                                              | Con    |
|                                                              | gratul |
|                                                              | ations |
|                                                              | you’ve |
|                                                              | now    |
|                                                              | c      |
|                                                              | reated |
|                                                              | your   |
|                                                              | own    |
|                                                              | pretty |
|                                                              | HUDF   |
|                                                              | image. |
|                                                              | By     |
|                                                              | ch     |
|                                                              | oosing |
|                                                              | dif    |
|                                                              | ferent |
|                                                              | f      |
|                                                              | ilters |
|                                                              | in     |
|                                                              | each   |
|                                                              | group  |
|                                                              | and    |
|                                                              | p      |
|                                                              | laying |
|                                                              | with   |
|                                                              | the    |
|                                                              | s      |
|                                                              | caling |
|                                                              | you    |
|                                                              | can    |
|                                                              | make   |
|                                                              | an     |
|                                                              | en     |
|                                                              | tirely |
|                                                              | unique |
|                                                              | and    |
|                                                              | or     |
|                                                              | iginal |
|                                                              | ve     |
|                                                              | rsion. |
+--------------------------------------------------------------+--------+

2 Detecting and measuring sources
---------------------------------

The next part of the project concentrates on identifying, and measuring
the properties of sources or objects.

+--------------------------------------------------------------+--------+
| ❓                                                            | **TASK |
|                                                              | 2A:    |
|                                                              | Det    |
|                                                              | ection |
|                                                              | I      |
|                                                              | mage** |
+==============================================================+========+
|                                                              | First  |
|                                                              | of     |
|                                                              | all,   |
|                                                              | fol    |
|                                                              | lowing |
|                                                              | `exa   |
|                                                              | mple4  |
|                                                              | </Exam |
|                                                              | ples/e |
|                                                              | xample |
|                                                              | 4.ipyn |
|                                                              | b>`__, |
|                                                              | create |
|                                                              | a      |
|                                                              | det    |
|                                                              | ection |
|                                                              | s      |
|                                                              | cience |
|                                                              | and    |
|                                                              | weight |
|                                                              | image  |
|                                                              | by     |
|                                                              | st     |
|                                                              | acking |
|                                                              | the    |
|                                                              | F105W, |
|                                                              | F125W, |
|                                                              | F140W, |
|                                                              | and    |
|                                                              | F160W  |
|                                                              | images |
|                                                              | tog    |
|                                                              | ether. |
|                                                              | You    |
|                                                              | will   |
|                                                              | use    |
|                                                              | this   |
|                                                              | image  |
|                                                              | to     |
|                                                              | detect |
|                                                              | faint  |
|                                                              | so     |
|                                                              | urces. |
+--------------------------------------------------------------+--------+

2.1 Significance maps
~~~~~~~~~~~~~~~~~~~~~

To identify sources we need to have an estimate of the noise in each
pixel. In the context of *Hubble* this is provided by the weight (wht)
map in each filter. The values in this image correspond to:

.. math::  weight = {1 \over \{noise^2}} 

By dividing the signal (science, or sci) map by the noise map (derived
from the weight map) we can obtain a significance map, essentially the
sigma-to-noise in every pixel. `example5 </Examples/example5.ipynb>`__
demonstrates this and Figure 4 shows the output.

.. raw:: html

   <figure>

.. raw:: html

   <p align="center">

.. raw:: html

   </p>

.. raw:: html

   <p align="center">

Figure 4: F105W significance image of the centre of the HUDF created by
`example5 </Examples/example5.ipynb>`__. Pixels coloured in grey have a
signal-to-noise < 2 with the colour scale stretching from −2 to 2.
Coloured pixels have a signal-to-noise > 2 with a scale stretching from
2 to 50.

.. raw:: html

   </p>

+--------------------------------------------------------------+--------+
| ❓                                                            | **TASK |
|                                                              | 2B:    |
|                                                              | Signif |
|                                                              | icance |
|                                                              | map**  |
+==============================================================+========+
|                                                              | Create |
|                                                              | a      |
|                                                              | signif |
|                                                              | icance |
|                                                              | map of |
|                                                              | a 400  |
|                                                              | pixel  |
|                                                              | wide   |
|                                                              | area   |
|                                                              | c      |
|                                                              | entred |
|                                                              | on     |
|                                                              | (3100, |
|                                                              | 1800). |
+--------------------------------------------------------------+--------+

2.2 Segmentation
~~~~~~~~~~~~~~~~

`Segmentation <https://en.wikipedia.org/wiki/Image_segmentation>`__ is
one way of detecting sources (objects) in an image. In the simplest
implementation we can identify collections of connected pixels which are
all above some threshold. Simple segmentation is controlled by two
parameters: the minimum number of connected pixels *npixels* and the
required significance *threshold* for each pixel.
`example6 </Examples/example6.ipynb>`__ demonstrates the use of simple
segmentation routines using the *astropy.photutils* module with the
results of simple segmentation shown in Figure 5.

.. raw:: html

   <figure>

.. raw:: html

   <p align="center">

.. raw:: html

   </p>

.. raw:: html

   <p align="center">

Figure 5: F125W segmentation map assuming *npixels = 5* and *threshold =
2.5*.

.. raw:: html

   </p>

One problem with simple segmentation like this is that nearby objects
are often merged together. To overcome this we can use de-blending
techniques, again this is demonstrated in
`example6 </Examples/example6.ipynb>`__.

+--------------------------------------------------------------+--------+
| ❓                                                            | **TASK |
|                                                              | 2C:    |
|                                                              | Det    |
|                                                              | ecting |
|                                                              | S      |
|                                                              | ources |
|                                                              | with   |
|                                                              | Se     |
|                                                              | gmenta |
|                                                              | tion** |
+==============================================================+========+
|                                                              | Create |
|                                                              | a      |
|                                                              | segmen |
|                                                              | tation |
|                                                              | image  |
|                                                              | (with  |
|                                                              | no     |
|                                                              | de-ble |
|                                                              | nding) |
|                                                              | of the |
|                                                              | same   |
|                                                              | region |
|                                                              | you    |
|                                                              | looked |
|                                                              | at in  |
|                                                              | 2b.    |
|                                                              | As     |
|                                                              | suming |
|                                                              | *n     |
|                                                              | pixels |
|                                                              | = 5*   |
|                                                              | and    |
|                                                              | *thr   |
|                                                              | eshold |
|                                                              | =      |
|                                                              | 2.5*.  |
|                                                              | Next,  |
|                                                              | sy     |
|                                                              | stemat |
|                                                              | ically |
|                                                              | e      |
|                                                              | xplore |
|                                                              | the    |
|                                                              | impact |
|                                                              | of     |
|                                                              | ch     |
|                                                              | anging |
|                                                              | n      |
|                                                              | pixels |
|                                                              | (must  |
|                                                              | bean   |
|                                                              | in     |
|                                                              | teger) |
|                                                              | and    |
|                                                              | thr    |
|                                                              | eshold |
|                                                              | on the |
|                                                              | number |
|                                                              | of     |
|                                                              | s      |
|                                                              | ources |
|                                                              | det    |
|                                                              | ected. |
+--------------------------------------------------------------+--------+

| 
| 

+--------------------------------------------------------------+--------+
| ❓                                                            | **TASK |
|                                                              | 2D:    |
|                                                              | The    |
|                                                              | impact |
|                                                              | of     |
|                                                              | d      |
|                                                              | e-blen |
|                                                              | ding** |
+==============================================================+========+
|                                                              | St     |
|                                                              | icking |
|                                                              | with   |
|                                                              | *n     |
|                                                              | pixels |
|                                                              | = 5*   |
|                                                              | and    |
|                                                              | *thr   |
|                                                              | eshold |
|                                                              | = 2.5* |
|                                                              | now    |
|                                                              | e      |
|                                                              | xplore |
|                                                              | the    |
|                                                              | impact |
|                                                              | of the |
|                                                              | para   |
|                                                              | meters |
|                                                              | that   |
|                                                              | c      |
|                                                              | ontrol |
|                                                              | de-bl  |
|                                                              | ending |
|                                                              | on the |
|                                                              | number |
|                                                              | of     |
|                                                              | so     |
|                                                              | urces. |
+--------------------------------------------------------------+--------+

| 
| 

2.3 Measuring the signal (and noise) of sources
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Our next task is to measure the signal (and noise) of our sources.
Again, there are many of ways of doing this. We’ll start off by simply
summing the flux in the segmentation region of each object. This is
sometimes referred to as an *isophotal* flux though technically this is
only truly isophotal if the noise is uniform. This is demonstrated in
`example7 </Examples/example7.ipynb>`__ and
`example8 </Examples/example8.ipynb>`__.

+--------------------------------------------------------------+--------+
| ❓                                                            | **TASK |
|                                                              | 2E:    |
|                                                              | M      |
|                                                              | easure |
|                                                              | the    |
|                                                              | signal |
|                                                              | of all |
|                                                              | sou    |
|                                                              | rces** |
+==============================================================+========+
|                                                              | M      |
|                                                              | easure |
|                                                              | the    |
|                                                              | signal |
|                                                              | (e/s)  |
|                                                              | of all |
|                                                              | the    |
|                                                              | s      |
|                                                              | ources |
|                                                              | in the |
|                                                              | r      |
|                                                              | egion. |
|                                                              | To do  |
|                                                              | this   |
|                                                              | you    |
|                                                              | can    |
|                                                              | c      |
|                                                              | ombine |
|                                                              | the    |
|                                                              | segmen |
|                                                              | tation |
|                                                              | map    |
|                                                              | with   |
|                                                              | the    |
|                                                              | det    |
|                                                              | ection |
|                                                              | s      |
|                                                              | cience |
|                                                              | image. |
|                                                              | Plot a |
|                                                              | hist   |
|                                                              | ogram. |
|                                                              | Do the |
|                                                              | same   |
|                                                              | for    |
|                                                              | the    |
|                                                              | de-b   |
|                                                              | lended |
|                                                              | image  |
|                                                              | and    |
|                                                              | d      |
|                                                              | iscuss |
|                                                              | the    |
|                                                              | diffe  |
|                                                              | rence. |
+--------------------------------------------------------------+--------+

| 
| 

+--------------------------------------------------------------+--------+
| ❓                                                            | **TASK |
|                                                              | 2F:    |
|                                                              | Make a |
|                                                              | mult   |
|                                                              | i-band |
|                                                              | catal  |
|                                                              | ogue** |
+==============================================================+========+
|                                                              | Using  |
|                                                              | the    |
|                                                              | or     |
|                                                              | iginal |
|                                                              | (un-bl |
|                                                              | ended) |
|                                                              | segmen |
|                                                              | tation |
|                                                              | map    |
|                                                              | m      |
|                                                              | easure |
|                                                              | the    |
|                                                              | signal |
|                                                              | and    |
|                                                              | noise  |
|                                                              | (or    |
|                                                              | error) |
|                                                              | of     |
|                                                              | every  |
|                                                              | object |
|                                                              | in     |
|                                                              | every  |
|                                                              | single |
|                                                              | filter |
|                                                              | and    |
|                                                              | create |
|                                                              | a      |
|                                                              | cat    |
|                                                              | alogue |
|                                                              | using  |
|                                                              | a      |
|                                                              | dicti  |
|                                                              | onary. |
|                                                              | Save   |
|                                                              | this   |
|                                                              | cat    |
|                                                              | alogue |
|                                                              | for    |
|                                                              | use    |
|                                                              | later. |
+--------------------------------------------------------------+--------+

A popular alternative is to simply place an aperture over each source
and calculate the flux through in that aperture. This can be done easily
using *photutils.aperture*. This is demonstrated in
`example9 </Examples/example9.ipynb>`__.

+--------------------------------------------------------------+--------+
| ❓                                                            | **TASK |
|                                                              | 2G:    |
|                                                              | Ap     |
|                                                              | erture |
|                                                              | phot   |
|                                                              | ometry |
|                                                              | STR    |
|                                                              | ETCH** |
+==============================================================+========+
|                                                              | Repeat |
|                                                              | 2f but |
|                                                              | using  |
|                                                              | ap     |
|                                                              | erture |
|                                                              | phot   |
|                                                              | ometry |
|                                                              | in     |
|                                                              | stead. |
|                                                              | Assume |
|                                                              | an     |
|                                                              | ap     |
|                                                              | erture |
|                                                              | 5      |
|                                                              | pixels |
|                                                              | in     |
|                                                              | r      |
|                                                              | adius. |
+--------------------------------------------------------------+--------+

3 Finding distant galaxies
--------------------------

High-redshift galaxies can be identified using the Lyman-break
technique. This takes advantage of a strong break in the spectrum of
galaxies caused by the absorption of ionising photons by inter-stellar
and inter-galactic hydrogen.

3.1 Changing units
~~~~~~~~~~~~~~~~~~

The units of the original images are electrons per second (e/s).
However, we want units of flux^2, for example in nano-Jansky (nJy). The
conversion from from e/s to nJy depends on the observatory, instrument,
and filter, and thus is unique for each filter:
`example10 </Examples/example10.ipynb>`__ contains the relevant
conversion in the form of a dictionary.

+--------------------------------------------------------------+--------+
| ❓                                                            | **TASK |
|                                                              | 3A:    |
|                                                              | C      |
|                                                              | onvert |
|                                                              | to     |
|                                                              | flux** |
+==============================================================+========+
|                                                              | Read   |
|                                                              | in the |
|                                                              | cat    |
|                                                              | alogue |
|                                                              | you    |
|                                                              | c      |
|                                                              | reated |
|                                                              | in     |
|                                                              | Task   |
|                                                              | 2f and |
|                                                              | c      |
|                                                              | onvert |
|                                                              | the    |
|                                                              | signal |
|                                                              | into a |
|                                                              | flux   |
|                                                              | (nJy)  |
|                                                              | using  |
|                                                              | the    |
|                                                              | conv   |
|                                                              | ersion |
|                                                              | dict   |
|                                                              | ionary |
|                                                              | in     |
|                                                              | exampl |
|                                                              | e9.py. |
|                                                              | Plot   |
|                                                              | *f     |
|                                                              | f105w/ |
|                                                              | f125w* |
|                                                              | v      |
|                                                              | s. *ff |
|                                                              | 850lp/ |
|                                                              | f105w* |
|                                                              | for    |
|                                                              | all    |
|                                                              | the    |
|                                                              | o      |
|                                                              | bjects |
|                                                              | in the |
|                                                              | cata   |
|                                                              | logue. |
+--------------------------------------------------------------+--------+

| 
| 

.. _finding-distant-galaxies-1:

3.2 Finding distant galaxies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

| Firstly, we want to guard against objects which are detected a
  low-S/N, as these are more likely to be contaminants (or not even real
  sources). To do this we can simply place a constraint on the
  signal-to-noise (S/N) in a filter where we know any real high-redshift
  object should be detected. We are somewhat free to choose the band and
  threshold but *ff125w* and a S/N> 10 is a reasonable choice.
| Next, we know that high-redshift galaxies have a strong spectral
  break. If the break falls between two bands A and B we’d expect that
  *fA/fB* should be small. Galaxies at z ∼ 7 have a break between the
  *f850lp* and *f105w* bands. A reasonable choice of ratio upper-limit
  is ∼ 0.4. We also expect the shape of the continuum above the break to
  be flat, or even negative (i.e. decreasing to longer-wavelength).
  Using a pair of bands above the break (e.g. *f105w* and *f125w*) we
  can then place an additional constraint allowing us to further weed
  out contamination. A reasonable choice for ratio lower-limit is ∼
  0.75. Finally, any truly high-redshift object should be undetected in
  any filter shortward of the break. For z ∼7 objects we wouldn’t expect
  them to be detected in *f435w*, *f606w*, or *f775w*. This can be
  implemented by enforcing that any candidate object is detected at less
  than S/N= 2 in those bands. In conclusion, our selection criteria can
  be expressed as follows:

.. container::

   S/N(ff125w) > 10 ff850lp/ff105w < 0.4 ff105w/ff125w > 0.75
   S/N(ff435w) < 2 ∧ S/N(ff606w) < 2 ∧ S/N(ff775w) < 2

+--------------------------------------------------------------+--------+
| ❓                                                            | **TASK |
|                                                              | 3B:    |
|                                                              | Id     |
|                                                              | entify |
|                                                              | h      |
|                                                              | igh-re |
|                                                              | dshift |
|                                                              | galaxy |
|                                                              | candid |
|                                                              | ates** |
+==============================================================+========+
|                                                              | Add    |
|                                                              | the    |
|                                                              | above  |
|                                                              | flux   |
|                                                              | -ratio |
|                                                              | cr     |
|                                                              | iteria |
|                                                              | to     |
|                                                              | your   |
|                                                              | plot   |
|                                                              | from   |
|                                                              | 3a     |
|                                                              | (      |
|                                                              | either |
|                                                              | as     |
|                                                              | lines  |
|                                                              | or a   |
|                                                              | shaded |
|                                                              | re     |
|                                                              | gion). |
|                                                              | Apply  |
|                                                              | the    |
|                                                              | cr     |
|                                                              | iteria |
|                                                              | to     |
|                                                              | your   |
|                                                              | cat    |
|                                                              | alogue |
|                                                              | of     |
|                                                              | o      |
|                                                              | bjects |
|                                                              | and    |
|                                                              | hig    |
|                                                              | hlight |
|                                                              | any    |
|                                                              | o      |
|                                                              | bjects |
|                                                              | m      |
|                                                              | eeting |
|                                                              | the    |
|                                                              | cr     |
|                                                              | iteria |
|                                                              | on     |
|                                                              | your   |
|                                                              | plot.  |
+--------------------------------------------------------------+--------+

| 
| 

+--------------------------------------------------------------+--------+
| ❓                                                            | **TASK |
|                                                              | 3C:    |
|                                                              | Det    |
|                                                              | ection |
|                                                              | image  |
|                                                              | thumb  |
|                                                              | nail** |
+==============================================================+========+
|                                                              | Using  |
|                                                              | `ex    |
|                                                              | ample7 |
|                                                              |  </Exa |
|                                                              | mples/ |
|                                                              | exampl |
|                                                              | e7.ipy |
|                                                              | nb>`__ |
|                                                              | as a   |
|                                                              | guide  |
|                                                              | make   |
|                                                              | det    |
|                                                              | ection |
|                                                              | image  |
|                                                              | thu    |
|                                                              | mbnail |
|                                                              | of     |
|                                                              | your   |
|                                                              | c      |
|                                                              | andida |
|                                                              | te(s), |
|                                                              | if you |
|                                                              | have   |
|                                                              | any.   |
+--------------------------------------------------------------+--------+

| 
| 

+--------------------------------------------------------------+--------+
| ❓                                                            | **TASK |
|                                                              | 3D:    |
|                                                              | More   |
|                                                              | thumbn |
|                                                              | ails** |
+==============================================================+========+
|                                                              | Fol    |
|                                                              | lowing |
|                                                              | on     |
|                                                              | from   |
|                                                              | 3c     |
|                                                              | also   |
|                                                              | make   |
|                                                              | thum   |
|                                                              | bnails |
|                                                              | in     |
|                                                              | each   |
|                                                              | band   |
|                                                              | (**H   |
|                                                              | int:** |
|                                                              | use    |
|                                                              | *sub   |
|                                                              | plots* |
|                                                              | for    |
|                                                              | ease)  |
|                                                              | in     |
|                                                              | ad     |
|                                                              | dition |
|                                                              | to an  |
|                                                              | RGB    |
|                                                              | thum   |
|                                                              | bnail. |
+--------------------------------------------------------------+--------+

| 
| 

+--------------------------------------------------------------+--------+
| ❓                                                            | **TASK |
|                                                              | 3E:    |
|                                                              | Ap     |
|                                                              | erture |
|                                                              | phot   |
|                                                              | ometry |
|                                                              | STR    |
|                                                              | ETCH** |
+==============================================================+========+
|                                                              | Repeat |
|                                                              | 3a but |
|                                                              | using  |
|                                                              | your   |
|                                                              | new    |
|                                                              | ap     |
|                                                              | erture |
|                                                              | phot   |
|                                                              | ometry |
|                                                              | based  |
|                                                              | cat    |
|                                                              | alogue |
|                                                              | in     |
|                                                              | stead. |
|                                                              | P      |
|                                                              | roduce |
|                                                              | a plot |
|                                                              | com    |
|                                                              | paring |
|                                                              | the    |
|                                                              | flux   |
|                                                              | ratios |
|                                                              | with   |
|                                                              | the    |
|                                                              | dif    |
|                                                              | ferent |
|                                                              | me     |
|                                                              | thods. |
+--------------------------------------------------------------+--------+
