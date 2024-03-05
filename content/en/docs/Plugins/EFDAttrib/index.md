---
title: EFDAttrib
description: spectral (time-frequency) decomposition using empirical fourier decomposition
weight: 3
categories: ["docs"]
tags: [time-frequency", "spectral-decomposition"]
---
{{% refs %}}
This attribute plugin for the open source seismic interpretation platform [OpendTect] Version 6.0.0 or later performs spectral
(time-frequency) decomposition using empirical fourier decomposition.

## Description

This plugin can be used as an alternative to the
<a href="http://opendtect.org/rel/doc/User/base/appendix_spectral-decomposition.htm" target="_blank">OpendTect FFT spectral decomposition attribute</a>.

It does spectral decomposition using [Empirical Fourier Decomposition (Zhou etal(2019)](https://arxiv.org/abs/1912.00414).
The plugin provides 2 new attributes that generate the mode decomposition and a spectral
decomposition from the mode decomposition. These provide a signal analysis akin to
Empirical Mode Decomposition. These attributes can work quite well for a simple mixture of frequency chirps but appear to be
less useful for typical seismic data.

{{< figure src="image-01.png"  width="90%" class="img-centered" caption="**Empirical Fourier Mode/Spectral Decomposition**">}}

## Input Parameters

### EFD Modes
This attribute has 3 parameters:
{{<table "table table-striped table-bordered">}}
| NAME | DESCRIPTION |
|------|-------------|
| Input Data | The attribute volume to be analysed. |
| Number of Modes | The number of modes expected.  |
| Output Mode | The mode to output. |
{{</table>}}

{{< figure src="image-02.png" width="90%" class="img-centered" caption="**EFD Modes input parameter dialog**" >}}

The "Display EFD Modes panel" button will generate the attribute for a trace in the input
data volume.

### EFD Spectral Decomposition
This attribute has 4 parameters:
{{<table "table table-striped table-bordered">}}
| NAME | DESCRIPTION |
|------|-------------|
| Input Data | The attribute volume to be analysed. |
| Number of Modes | The number of modes expected.  |
| Output Frequency (Hz) | The frequency to output. |
| Output Frequency Step (Hz) | The frequency step for output. |
{{</table>}}

{{< figure src="image-03.png" width="90%" class="img-centered" caption="**EFD Spectral Decomposition input parameter dialog**" >}}

The "Display Time/Frequency panel" button will generate the attribute for a trace in the input
data volume.
