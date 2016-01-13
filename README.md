# HFSS and MATLAB

HFSS can be controlled with Matlab in Windows. This is useful for performing customized design parameter sweeps or optimizations that are not included in HFSS. I have used this approach sucessfully to design several different devices, and the results are published here. Read more there if you're interested!

"A Compact Filter-Bank Waveguide Spectrometer for Millimeter Wavelengths"
http://arxiv.org/abs/1502.02735

"WSPEC: A waveguide filter-bank focal plane array spectrometer for millimeter wave astronomy and cosmology"
http://arxiv.org/abs/1509.04658

"Design of Dual-Polarization Horn-Coupled Kinetic Inductance Detectors for Cosmic Microwave Background Polarimetry"
http://arxiv.org/abs/1503.04684

Anyway, the general workflow is to use the Matlab-HFSS API https://code.google.com/p/hfss-api/ to in Matlab change the dimension of a HFSS structure you have already drawn with the normal HFSS interface. Then have Matlab tell HFSS to resimulate with the new dimensions. Finally, have Matlab read in the simulation results. The dimension can be optimized automatically by having Matlab resimulate with a wide range of different dimensions, and then the dimension with the best performance can be selected afterwards. Alternately, an optimization algorithm can be used to minimize/maximize a single design goal, or a merit function that is a compromise among several design goals.

This kind of optimization functionality is built in to HFSS already for S-matrix simulations, or for absorbed-power simulations at a single frequency. However, since I had an application with a merit function that I couldn't define easily in the HFSS toolbox, and I also have needed broadband absorbed-power simulations, this is what lead me towards this Matlab/HFSS scripted approach.

In addition to optimizing a single design, this approach can be used for tolerancing analysis. A random number generator in Matlab can be used to select a new dimension, resimulate in HFSS, then repeat for a large number of dimensions from the random number generator. This can be used to get upper and lower bounds on device performance when dimensions are varied randomly, as can happen in the fabrication process.

