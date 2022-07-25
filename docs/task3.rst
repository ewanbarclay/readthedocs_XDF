===========================
TASK 3:  *Finding distant galaxies*
===========================
High-redshift galaxies can be identified using the Lyman-break technique. This takes advantage of a strong break in the spectrum of galaxies caused by the absorption of ionising photons by inter-stellar and inter-galactic hydrogen.

3.1  Changing units
-------------------
The units of the original images are electrons per second (e/s). However, we want units of flux\ :sup:`2`, for example in nano-Jansky (nJy). The conversion from from e/s to nJy depends on the observatory, instrument, and filter, and thus is unique for each filter: :ref:`Example10` contains the relevant conversion in the form of a dictionary.

|

========  ========
❓         **TASK 3A:** *Convert to Flux*
========  ========
|           Read in the catalogue you created in Task 2f and convert the signal into a flux (nJy) using the conversion dictionary in :ref:`Example9`. Plot f\ :sub:`f105w` / f\ :sub:`125w` vs. f\ :sub:`f850lp` /f\ :sub:`105w` for all the objects in the catalogue. 
========  ========

|

3.2  Finding distant galaxies
-----------------------------
Firstly, we want to guard against objects which are detected a low-S/N, as these are more likely to be contaminants (or not even real sources). To do this we can simply place a constraint on the signal-to-noise (S/N) in a filter where we know any real high-redshift object should be detected. We are somewhat free to choose the band and threshold but f\ :sub:`f125w` and a S/N> 10 is a reasonable choice. 

Next, we know that high-redshift galaxies have a strong spectral break. If the break falls between two bands A and B we’d expect that f\ :sub:`A` /f\ :sub:`B` should be small. Galaxies at z ∼ 7 have a break between the *f850lp* and *f105w* bands. A reasonable choice of ratio upper-limit is ∼ 0.4.

We also expect the shape of the continuum above the break to be flat, or even negative (i.e. decreasing to longer-wavelength). Using a pair of bands above the break (e.g. *f105w* and *f125w*) we can then place an additional constraint allowing us to further weed out contamination. A reasonable choice for ratio lower-limit is ∼ 0.75. 

Finally, any truly high-redshift object should be undetected in any filter shortward of the break. For z ∼7 objects we wouldn’t expect them to be detected in *f435w*, *f606w*, or *f775w*. This can be implemented by enforcing that any candidate object is detected at less than S/N= 2 in those bands.

In conclusion, our selection criteria can be expressed as follows:


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
|          Using :ref:`Example7` as a guide make detection image thumbnail of your candidate(s), if you have any.
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
