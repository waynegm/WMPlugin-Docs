---
title: AVO Intercept and Gradient
description: estimate AVO intercept and gradient from angle stacks
weight: 2
categories: ["docs"]
tags: ["ExternalAttrib", "avo"]
---

## Description
These [External Attribute](../../plugins/externalattrib) scripts estimate AVO intercept and gradient based on Shuey's 2 term approximation
to the Zoeppritz equation. Scripts are provided for 3, 4 and 5 angle stacks.

## Intercept and Gradient from Angle Stacks
__Script: Miscellaneous/ex_angle_stacks_3_to_AVOIG.py__
__Script: Miscellaneous/ex_angle_stacks_4_to_AVOIG.py__
__Script: Miscellaneous/ex_angle_stacks_5_to_AVOIG.py__

Takes as input angle stacks and the corresponding angles and fits a least squares line to the \\(amplitude\\) and \\(sin^2(angle)\\) at
each sample point. Output includes the intercept, gradient and the correlation coefficient of the line fit.

### Input Parameters
{{< figure src="ex_AVOIG_4_input.jpg" width="90%" class="img-centered" caption="**ex_angle_stacks_4_to_AVOIG.py input parameters**" >}}

For each input volume the corresponding incident angle must be provided.




