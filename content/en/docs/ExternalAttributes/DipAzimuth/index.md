---
title: Dip and Azimuth
description: various scripts to estimate orientation
weight: 3
categories: ["docs"]
tags: ["ExternalAttrib", "dipaz"]
---

## Description
These Python [External Attribute](../../plugins/externalattrib) scripts implement various algorithms to estimate orientation, ie dip or dip azimuth.

All scripts will estimate at least the following attributes:

{{<table "table table-striped table-bordered">}}
| OUTPUT | DESCRIPTION |
|--------|-------------|
| Inline Dip | Event dip observed on a crossline in microseconds per metre for time surveys and millimetres per metre for depth surveys. Output can be positive or negative with the convention that events dipping towards larger inline numbers producing positive dips. |
| Crossline Dip | Event dip observed on an inline in microseconds per metre for time surveys and millimetres per metre for depth surveys. Output can be positive or negative with the convention that events dipping towards larger crossline numbers producing positive dips. |
| True Dip | Event dip in microseconds per metre for time surveys and millimetres per metre for depth surveys. Output is always positive. |
| Dip Azimuth | Azimuth of the True Dip direction relative to the survey orientation. Output ranges from -180 to 180 degrees. Positive azimuth is defined from the inline in the direction of increasing crossline numbers. Azimuth = 0 indicates that the dip is dipping in the direction of increasing crossline numbers. Azimuth = 90 indicates that the dip is dipping in the direction of increasing inline numbers. |
{{</table>}}

Some scripts may offer additional outputs such as a measure of event coherency or planarity.

All of the scripts require the numba Python package.

## Orientation from gradients
__Script: ex_gradient_dip.py__

Calculates orientation from inline, crossline and Z gradients. No filtering is applied
{{< figure src="ex_gradient_dip.jpg" width="90%" class="img-centered" caption="**Unfiltered gradient dip - crossline dip on an inline**" >}}

## Orientation from vector filtered gradients
__Script: ex_vf_gradient3_dip.py__

Uses [Kroon's (2009)](http://www.k-zone.nl/Kroon_DerivativePaper.pdf "NUMERICAL OPTIMIZATION OF KERNEL BASED IMAGE DERIVATIVES. Dirk-Jan Kroon, University of Twente, Enschede") 3 point derivative filter to estimate data gradients. Next gradient normal unit vectors are determined and smoothed using a vector filter.
{{<table "table table-striped table-bordered">}}
| NAME | DESCRIPTION |
|------|-------------|
| Output | What to calculate - choice of inline dip, crossline dip, true dip or dip azimuth. |
| Z window (+/-samples) | Specifies the extent of the analysis cube in the Z direction. Number of Z samples in cube will be \\((2\*Zwindow+1)\\). |
| Stepout | Specifies the inline and crossline extent of the analysis cube. Number of samples in each direction will be \\((2\*Stepout+1)\\). |
| Filter | Choice of Mean Dip, L1 Vector Median or L2 Vector Median. |
{{</table>}}

The aperture of the vector filtering is \\((2\*ZStepOut-1)\\) \\(Z\\) samples and \\((2\*Stepout-1)\\) samples in the inline and crossline
direction. For example for a 5x5x5 analysis cube \\((Zwindow=2, Stepout=2)\\) the gradients and associated normal unit vectors are generated
on a 3x3x3 cube and vector filtered. The outer samples are only used in the gradient calculation.

{{< figure src="ex_vfmean_gradient_dip.jpg" width="90%" class="img-centered" caption="**Vector filtered gradient dip - crossline dip on an inline - 5x5x5 input**" >}}

## Orientation by the gradient structure tensor
__Scripts: ex_gradient3_st_dip.py & ex_gradient5_st_dip.py__

Uses either [Kroon's (2009)](http://www.k-zone.nl/Kroon_DerivativePaper.pdf "NUMERICAL OPTIMIZATION OF KERNEL BASED IMAGE DERIVATIVES. Dirk-Jan Kroon, University of Twente, Enschede") 3 point or the [Farid and Simoncelli (2004)](http://www.cns.nyu.edu/pub/lcv/farid03-reprint.pdf "Differentiation of Discrete Multidimensional Signals. Hany Farid and Eero P. Simoncelli, IEEE TRANSACTIONS ON IMAGE PROCESSING, VOL. 13, NO. 4, APRIL 2004") 5 point derivative filter to estimate data gradients which are then used to form the gradient structure tensor.

{{<table "table table-striped table-bordered">}}
| NAME | DESCRIPTION |
|------|-------------|
| Output | What to calculate - choice of inline dip, crossline dip, true dip or dip azimuth. |
| Z window (+/-samples) | Specifies the extent of the analysis cube in the Z direction. Number of Z samples in cube will be \\((2*Zwindow+1)\\). |
| Stepout | Specifies the inline and crossline extent of the analysis cube. Number of samples in each direction will be \\((2*Stepout+1)\\). |
{{</table>}}

For the ex_gradient3 script the structure tensor is formed from an aperture of \\((2*ZStepOut-1)\\) \\(Z\\) samples and \\((2\*Stepout-1)\\) samples in the inline and crossline direction.

For the ex_gradient5 script the structure tensor is formed from an aperture of \\((2*ZStepOut-2)\\) \\(Z\\) samples and \\((2\*Stepout-1)\\) samples in the inline and crossline direction.

{{< figure src="ex_gst3_dip.jpg" width="90%" class="img-centered" caption="**Gradient3 structure tensor dip - crossline dip on an inline - 5x5x5 input**" >}}

## Orientation from the 3D complex trace phase
__Script: ex_phase3_dip.py__

Calculates orientation from the 3D complex trace phase gradients as per [Barnes (2007)](http://library.seg.org/doi/abs/10.1190/1.2785048 "A tutorial on complex seismic trace analysis. Arthur E. Barnes. GEOPHYSICS 2007 72:6, W33-W43"). [Kroon's (2009)](http://www.k-zone.nl/Kroon_DerivativePaper.pdf "NUMERICAL OPTIMIZATION OF KERNEL BASED IMAGE DERIVATIVES. Dirk-Jan Kroon, University of Twente, Enschede") 3 point derivative filter is used to compute gradients.
{{<table "table table-striped table-bordered">}}
| NAME | DESCRIPTION |
|------|-------------|
| Output | What to calculate - choice of inline dip, crossline dip, true dip or dip azimuth. |
| Z window (+/-samples) | Specifies the length \\((2*Zwindow+1)\\) of the time domain operator used to generate the complex analytic signal (recommend >= 15) |
| Band | Specifies the proportion of the frequency band to include when generating the complex analytic signal (recommend 0.9). |
{{</table>}}

{{< figure src="ex_phase3_dip.jpg" width="90%" class="img-centered" caption="**Unfiltered phase dip - crossline dip on an inline**" >}}

## Orientation from vector filtered 3D complex trace phase
__Script: ex_vf_phase3_dip.py__

Calculate orientation unit normal vectors using the 3D complex trace phase gradient and apply a vector filter. [Kroon's (2009)](http://www.k-zone.nl/Kroon_DerivativePaper.pdf "NUMERICAL OPTIMIZATION OF KERNEL BASED IMAGE DERIVATIVES. Dirk-Jan Kroon, University of Twente, Enschede") 3 point filter used to compute gradients.
{{<table "table table-striped table-bordered">}}
| NAME | DESCRIPTION |
|------|-------------|
| Output | What to calculate - choice of inline dip, crossline dip, true dip or dip azimuth. |
| Z window (+/-samples) | Specifies the length \\((2*Zwindow+1)\\) of the time domain operator used to generate the complex analytic signal (recommend >= 15) |
| Stepout | Specifies the inline and crossline extent of the analysis cube. Number of samples in each direction will be \\((2*Stepout+1)\\). |
| Filter | Choice of Mean Dip, L1 Vector Median or L2 Vector Median. |
| Vector Filter ZStepOut | Specifies the extent of the analysis cube for vector filtering in the Z direction. Number of Z samples in cube will be \\((2*ZStepOut+1)\\). |
| Band | Specifies the proportion of the frequency band to include when generating the complex analytic signal (recommend 0.9). |
{{</table>}}

The aperture of the vector filter is \\((2\*ZStepOut+1)\\) \\(Z\\) samples and \\((2\*Stepout-1)\\) samples in the inline and crossline direction.

{{< figure src="ex_vfmean_phase3_dip.jpg" width="90%" class="img-centered" caption="**Mean Vector Filtered phase dip - crossline dip on an inline - 3x3x3**" >}}

## Orientation using the envelope weighted 3D complex trace phase structure tensor
__Script: ex_weighted_phase3_st_dip.py__

Forms a structure tensor from the 3D complex trace phase gradients. Tensor elements are weighted by the trace envelope as per [Luo etal (2006)](http://library.seg.org/doi/abs/10.1190/1.2235591?journalCode=gpysa7 "Computation of dips and azimuths with weighted structural tensor approach. Yi Luo, Yuchun Eugene Wang, Nasher M. AlBinHassan and Mohammed N. Alfaraj, GEOPHYSICS 2006 71:5, V119-V121"). [Kroon's (2009)](http://www.k-zone.nl/Kroon_DerivativePaper.pdf "NUMERICAL OPTIMIZATION OF KERNEL BASED IMAGE DERIVATIVES. Dirk-Jan Kroon, University of Twente, Enschede") 3 point filter is used to compute gradients.
{{<table "table table-striped table-bordered">}}
| NAME | DESCRIPTION |
|------|-------------|
| Output | What to calculate - choice of inline dip, crossline dip, true dip or dip azimuth. |
| Z window (+/-samples) | Specifies the length \\((2*Zwindow+1)\\) of the time domain operator used to generate the complex analytic signal (recommend >= 15) |
| Stepout | Specifies the inline and crossline extent of the analysis cube. Number of samples in each direction will be \\((2*Stepout+1)\\). |
| Tensor ZStepOut | Specifies the extent of the analysis cube for vector filtering in the Z direction. Number of Z samples in cube will be \\((2*ZStepOut+1)\\). |
| Band | Specifies the proportion of the frequency band to include when generating the complex analytic signal (recommend 0.9). |
{{</table>}}

The aperture of the structure tensor is \\((2\*ZStepOut+1)\\) \\(Z\\) samples and \\((2\*Stepout-1)\\) samples in the inline and crossline direction.

{{< figure src="ex_phasest_dip.jpg" width="90%" class="img-centered" caption="**Structure tensor phase dip - crossline dip on an inline - 3x3x3 tensor input**" >}}
