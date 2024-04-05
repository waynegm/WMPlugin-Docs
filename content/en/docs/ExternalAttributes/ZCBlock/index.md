---
title: ZC Block
description: blocks a seismic trace between zero crossings
weight: 10
categories: ["docs"]
tags: ["ExternalAttrib", "filter"]
---

__Script: Miscellaneous/ex_zc_block.py__

## Description
This Python [External Attribute]({{<relref "/externalattrib" >}}) script blocks a seismic trace between zero crossings. The block amplitude is
determined by the min/max of the interval blocked.

The script requires the Numba Python package.

## Examples
This example shows the attribute output (black wiggle) over the input (variable density). To get a blocky wiggle display interpolation has to be turned off in the 2D viewer properties.
{{< figure src="ex_zc_block_example.jpg" width="90%" class="img-centered" caption="**Zero crossing block**" >}}

## Input Parameters
{{< figure src="ex_zc_block_input.jpg" width="90%" class="img-centered" caption="**ex_zc_block.py input parameters**" >}}

There are no input parameters other than selection of the input volume.




