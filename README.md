# ISGRI Reconstruction in small time bins

before OSA11, it was not generally possible to reconstruct standard spectra/image/lightcurves 
in time bins smaller than approximately 8s.

This was because efficiency computation in *ii_shadow_build* used deadtime correction 
relying on instantenous measurements of the HK rates, available every 8 seconds. 
If a measurement was not in the selected time interval, 
the efficiency was set to zero, the data was excluded from the analysis.
While in principle, arbitrarily small time interval could contain the required 
measurement, it could not be the case consistently unless the interval is longer than 8s.

This problem was widely understood, and the patch was provided to extrapolate the correction
in between the HK measurements, allowing efficiency computation and flux reconstruction
in arbitrarity small intervals.

However, in some cases, this brought up another issue: very short intense signals, which
contain very few background, may cause the spectral Noisy Pixel detection in
ii_shadow_build to misfire, disabling all pixels with source counts. This results
in seemingly normal efficiency, missing exceptionally only the useful pixels in some
energy ranges.

This additional "Spectral" noisy pixel detection can be disabled by setting *NoisyDetFlag*
parameter to *0*.
It corresponds to ibis_science_analysis parameter [IBIS_NoisyDetMethod](see https://www.isdc.unige.ch/integral/download/osa/doc/11.0/osa_um_ibis/node148.html).



