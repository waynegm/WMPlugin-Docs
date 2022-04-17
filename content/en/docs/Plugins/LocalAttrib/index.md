---
title: LocalAttrib
description: various attributes based on Fomel's local attribute algorithm from the Madagascar package
weight: 8
categories: ["docs"]
tags: ["time-frequency", "spectral-decomposition"]
---

This plugin for the open source seismic interpretation platform [opendtect] Version 6.0 or later is a collection of "Local Attributes" based on the work of [Fomel (2007) and others](https://library.seg.org/doi/abs/10.1190/1.2437573"Local seismic attributes. Sergey Fomel. GEOPHYSICS 2007 72:3") for the <a href="http://www.ahay.org/" target="_blank">Madagascar</a> package. At this point only spectral (time-frequency) decomposition using local attributes (previously called the LTFAttrib) is implemented. The predecessor to this plugin (LTFAttrib, now obsolete) had a hard dependency on the Madagascar libraries and was consequently only available for Linux. This dependency has been removed and the plugin is now available for both Linux and Windows.

## Spectral (Time-frequency) Decomposition by Local Attributes

Formerly called the LTFAttrib, this is an implementation of the method of local time-frequency analysis as described by [Liu, G etal (2011)](http://library.seg.org/doi/abs/10.1190/geo2010-0185.1 "Time-frequency analysis of seismic data using local attributes. Guochang Liu, Sergey Fomel, and Xiaohong Chen. GEOPHYSICS 2011 76:6, P23-P34"). This decomposition uses least-squares inversion with shaping regularization to estimate the time-varying Fourier coefficients. Its principal advantages over the STFT (short time fourier transform) is it much quicker if only a few frequencies are required and it is generally more accurate for short window lengths.

### Examples

{{< juxtapose img1="LTFAttrib_sd.jpg" lbl1="FFT Spectral Decomposition (30Hz +/-28ms window)" img2="LTFAttrib_1.jpg" lbl2="Local time-frequency attribute (30Hz 7 sample smoothing radius)" >}}
<br/>
The output of the LTF attribute (ltf30) is visually identical and also highly correlated to the OpendTect FFT spectral decomposition (sdfreq30) as shown in the following crossplot of the two attributes.

{{< figure src="LTFAttrib_2.jpg" width="90%" class="img-centered" caption="**Crossplot of LTFAttrib vs FFT Spectral Decomposition**" >}}

### Input Parameters

This attribute has 4 parameters:

{{<table "table table-striped table-bordered">}}
| NAME | DESCRIPTION |
|------|-------------|
| Input Volume | The attribute volume to be analysed. |
| Time Gate | Where the attribute is calulated. The time gate does not have to be symmetric. The time gate length is used as the smoothing radius for shaping regularization.The value from the gate centre is output - useful for analysing a zone offset from an horizon. Recommend setting the gate length equal to or less than the FFT window length you would used for the standard OpendTect FFT spectral decomposition. |
| Frequency | The frequency component(s) to estimate. |
| Iterations| The number of inversion iterations. |
{{</table>}}

{{< figure src="LTFAttrib_input_parameters.jpg" class="img-centered" caption="**LTF Attributes input parameters**" >}}




