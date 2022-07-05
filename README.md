# Exploring the Hubble Ultra Deep Field
## Introduction
The Hubble Ultra Deep Field (HUDF), also known (due to a re-branding exercise) as the eXtreme Deep
Field (XDF), is the Hubble Space Telescope’s deepest view of the Universe.The HUDF
The aim of this project is to become familiar with analysing Hubble imaging using python. The ultimate goal is to identify candidate high-redshift galaxies.
### Astronomical images
Astronomical cameras are typically sensitive to a broad wavelength range. To gain spectral information we must combine the camera (detector) with a filter that is only transparent to light over a (typically) small range of wavelengths, typically O(100nm). These individual images are monochromatic (i.e. they contain no colour information) and can thus be represented by a simple two-dimensional array where each element of the array denotes the signal in that pixel. Images in several filters, or bands, can be combined, as we’ll see to generate colour images.
Astronomical images are typically held in the [Flexible Image Transport System (FITS)](https://en.wikipedia.org/wiki/FITS). In addition to the raw image data FITS file can also contain meta-data in a header and even tabular data. Examples of this meta-data are the values necessary to convert from pixel coordinates (e.g. (x, y)) to a position on the sky.

