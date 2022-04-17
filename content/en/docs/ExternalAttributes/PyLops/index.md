---
title: PyLops Attributes
description: various external attributes that use the PyLops linear operator library
weight: 5
tags: ["ExternalAttrib", "pylops", "inversion", "modelling"]
categories: ["docs"]
---

The 6.6.8 release of the wmPlugins includes a number of new Python external attribute scripts that use the [PyLops](https://pylops.readthedocs.io/en/latest/)
linear operator library for seismic modelling and inversion.

Assuming wmPlugins is installed using the OpendTect Installation Manager, the scripts will be in the *bin/python/wmpy/PyLops* folder
of the OpendTect software folder and include:

-  PyLops/ex_poststack_inversion.py
-  PyLops/ex_poststack_relative_inversion.py
-  PyLops/ex_poststack_modelling.py
-  PyLops/ex_prestack_modelling.py
-  PyLops/ex_make_1d_seismic.py

Using these scripts requires a Python environment with the PyLops module and it's dependencies installed. The section
[Installing PyLops](#installing-pylops) describes the PyLops installation process.

## PyLops/ex_poststack_inversion.py

This Python [External Attribute](../../plugins/externalattrib) script uses the pylops.avo.poststack.PoststackInversion operator to do
post-stack seismic inversion. The output is either the log Acoustic Impedance (AI) volume or the residual error.

The inputs required are volumes of the seismic to be inverted, a background log AI model and the seismic wavelet. Note that the polarity
of the seismic wavelet must match the data.

The following figures show inversion input and output for a 1D model created by the PyLops/ex_make_1d_seismic.py script.

{{< figure src="ex_pylops_poststack_inversion-02.png" width="90%" class="img-centered" caption="**Impedance Model (red) and Background Model (blue)**" >}}
{{< figure src="ex_pylops_poststack_inversion-03.png" width="90%" class="img-centered" caption="**Impedance Model (red) and Seismic Model (blue)**" >}}
{{< figure src="ex_pylops_poststack_inversion-04.png" width="90%" class="img-centered" caption="**Impedance Model (red) and Inverted Impedance (blue)**" >}}

There is also a PyLops/ex_poststack_relative_inversion.py script that runs the inversion without a background model:

{{< figure src="ex_pylops_poststack_inversion-05.png" width="90%" class="img-centered" caption="**Impedance Model (red) and Inverted Relative Impedance (blue)**" >}}

{{< figure src="ex_pylops_poststack_inversion-07.png" width="90%" class="img-centered" caption="**Inverted Relative Impedance Example**" >}}

### Input Parameters
{{< figure src="ex_pylops_poststack_inversion_input.png" width="90%" class="img-centered" caption="**ex_poststack_inversion.py input parameters**" >}}

{{<table "table table-striped table-bordere">}}
| NAME | DESCRIPTION |
|------|-------------|
| Output | What to calculate - choice of Acoustic Impedance or the Residual Error. |
| Regularization (%) | A small amount of noise to add to stabilize the inversion. |
| Wavelet | An OpendTect wavelet file. |
{{</table>}}
</br>
Note the wavelet polarity must be consistent with the polarity of the data being inverted.

## PyLops/ex_prestack_modelling.py

The PyLops/ex_prestack_modelling.py script uses the pylops.avo.avo.AVOLinearModelling operator to create a pre-stack angle volume
from well data. The output is either an Aki-Richards or Fatti approximate reflectivity model filtered by a user specified wavelet.

The inputs required are 3 log data cubes with compressional sonic (DT in us/m), shear sonic (DTS in us/m) and density (RHOB in g/cc). These
can be created from well log data using the "Create Log Cube" right mouse button context menu in the scene well tree or the
"Processing|Create Seismic Output|From Well Logs" main menu. Also needed is a wavelet with the appropriate polarity for the data being modelled.

The generated synthetics can be displayed in the 3D window and compared with real angle stack data through the well location.

{{< figure src="ex_pylops_prestack_modelling-01.jpg" width="90%" class="img-centered" caption="**Prestack modelling example**" >}}

### Input Parameters
{{< figure src="ex_pylops_prestack_modelling_input.png" width="90%" class="img-centered" caption="**ex_prestack_modelling.py input parameters**" >}}

{{<table "table table-striped table-bordered">}}
| NAME | DESCRIPTION |
|------|-------------|
| Angle (deg) | The desired output angle volume. |
| Method | What approximation to use, Aki RIchards or Fatti. |
| Wavelet | An OpendTect wavelet file. |
{{</table>}}

## Installing PyLops
The PyLops Python package and it's dependencies can be installed in an active conda environment using:

```
conda install -c conda-forge pylops
```
or

```
pip install pylops
```
See the [PyLops documentation](https://pylops.readthedocs.io/en/latest/installation.html) for more information.


