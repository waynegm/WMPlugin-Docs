---
date: 2022-04-15
title: "WMPlugins 6.6.10 Release"
banner: /blog/wmplugins-release-6.6.10/image-01.png
categories: ["release"]
tags: ["AVOPolarAttrib", "EFDAttrib", "ExternalAttrib", "Mistie", "Python"]
---
Announcing the release of version 6.6.10 of the WMPlugins a suite of opensource plugins that extend the opensource seismic interpretation
system [OpendTect](https://dgbes.com/index.php/software#free). This release is built against OpendTect 6.6.7.
<!--more-->

The release includes the following changes:
## AVOPolarAttrib
Nans and Infs generated during the calculation of the attributes are converted to OpendTect Undefined, fixing a crash.

## EFDAttrib
Two new attributes have been added that use [Empirical Fourier Decomposition (Zhou etal(2019)](https://arxiv.org/abs/1912.00414). The
two attributes generate the mode decomposition and a spectral decomposition from the mode decomposition. These provide a signal analysis
akin to Empirical Mode Decomposition. A subsequent post will look at these new attributes in detail and compare the new spectral
decomposition option with the existing WMPlugin tools such as Recursive spectral decomposition and Spectral decomposition by local attribute.

{{< figure src="image-01.png"  width="90%" class="img-centered" caption="**Empirical Fourier Mode/Spectral Decomposition**">}}

## External attributes
This release fixes a crash when loading an attribute set with either a non-existent python interpreter or attribute script and now
reports syntax errors from the script when building the UI via a UI message box. Previously these errors were recorded in the OpendTect
log file but the user did not get any direct feedback that an issue was encountered.

{{< figure src="image-03.png"  width="90%" class="img-centered" caption="**Improved error reporting in the External Attribute plugin**">}}


Also fixed various issues with the included wmpy scripts to make them compatible with the versions of Python modules installed by the OpendTect
installation manager.

## Mistie Analysis
Fixed a crash when estimating misties for depth surveys.

## wmodpy - OpendTect Python Bindings
A decision was made to discontinue development of these within WMPlugins in favour of moving the code
into the dGB managed OpendTect open source code repository system on Github. The new repository will be
called "odpybind".
