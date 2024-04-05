+++
title = "First Release of Python Bindings to OpendTect"
tags = ["python"]
categories = ["release", "article"]
date = "2021-06-29"
banner = "/blog/opendtect-python-bindings-release/image-01.png"
+++
The 6.6.8 release of the [WMPlugins](https://waynegm.github.io/WMPlugin-Docs/) includes a Python module, **wmodpy**, to access OpendTect survey and well information. Unlike
OpendTect's existing **odpy** module, **wmodpy** is a direct binding to the OpendTect C++ code.
<!--more-->
The **odpy** module, by comparison, uses a command line application to interact with the OpendTect data structures and transfers
data to Python as an ascii data stream. This incurs the overhead of starting this application and the writing and reading of an
ascii data stream on every request. The **wmodpy** module, however, as a direct binding to the OpendTect C++ code allows Python
to directly read from the in-memory representation of the data. Data access with the **wmodpy** module should be much faster.

## Accessing the wmodpy Module
Installing my **WMPlugins** using the OpendTect installation manager will install the **wmodpy** Python module into the *bin/win64/Release*
or *bin/lux64/Release* subfolder of the OpendTect software. You also need a Python environment with at least Numpy but additional
output options exist if the environment also has Pandas. The OpendTect machine learning Python environments already include Numpy
and Pandas. For map display you may want to add a module like Folium to your working environment.

The folder containing the bindings library must be on the PYTHONPATH to be found by an import statement in a Python script or notebook.
You can either use the OpendTect Python Settings dialog (accessible from the Utilities| Installation|Python Settings application menu)
and add the location of the OpendTect executable files to the Custom Module Path or modify the PYTHONPATH within the script.

{{< figure src="image-02.png"  width="90%" class="img-centered" caption="**OpendTect Python Settings Dialog**">}}

The OpendTect Python Settings dialog also allows you to select a custom Python environment to use and also add an icon to the OpendTect
toolbar to start your chosen IDE and console (only OpendTect 6.6.4) with the specified custom Python environment activated and the
Custom Module Paths added to the PYTHONPATH.

The alternative script/notebook  based solution requires something like the following at the top of the script:
``` python
import sys
sys.path.insert(0, 'C:/Program Files/OpendTect/6.6.0/bin/win64/Release')
import wmodpy
```

## General Survey Information
The module includes a number of functions for getting information about OpendTect surveys/projects. These all require
an OpendTect data root folder for context.

{{<table "table table-striped table-bordered">}}
| Command                    | Description |
|----------------------------|-------------|
| get_surveys(data_root:str) | Return list of survey names in the given data_root |
| get_survey_info(data_root:str, surveys:list) | Return a Python dictionary with basic information for the surveys in the given list or all surveys if no list is given |
| get_survey_info_df(data_root:str, surveys:list) | Return a Pandas Dataframe with basic information for the surveys in the given list or all surveys if no list is given |
| get_survey_features(data_root:str, surveys:list) | Return a GeoJSON Feature Collection with basic information for the surveys in the given list or all surveys if no list is given |
{{</table>}}

Some examples:
```python
wmodpy.get_surveys("/mnt/Data/seismic/CooperBasin/ODData")
['13CP06_Dundinna', 'Cooper2D']
```
```python
wmodpy.get_surveys_df("/mnt/Data/seismic/ODData", ["F3_Demo_2020", "Penobscot"])
```
{{< figure src="image-03.png"  width="100%" class="img-centered" caption="**Displaying OpendTect survey info in a Pandas Dataframe**">}}

{{< figure src="image-01.png"  width="100%" class="img-centered" caption="**Displaying OpendTect survey locations on a Folium web map**">}}

## Survey Class
The module adds a *Survey* Python class. Create a *Survey* object for a particular data_root and survey_name combination like this:
```python
f3demo = wmodpy.Survey("/mnt/Data/seismic/ODData", "F3_Demo_2020")
```
The *Survey* object can then be used to get information about the survey:
```python
f3demo.info()
{'Name': ['F3 Demo 2020'], 'Type': ['2D3D'], 'crs': ['EPSG:23031']}
```
To get a full list of methods provided by the *Survey* class use :
```python
help(wmodpy.Survey)
```
The other classes added by the module generally require a *Survey* object for context.

## Wells Class
The *Wells* Python class provides methods to access OpendTect well data within a survey. Creating a *Wells* object requires a
*Survey* object for context:
```python
f3demo_wells = wmodpy.Wells(f3demo)
```
Methods are provided to:
-  List the names of all wells in the project/survey
-  List summary information on all wells
-  List well log information in a well
-  List well log data
-  List markers in a well
-  List a well track

There is also a "features" method that returns a GeoJSON Feature Collection. To get a full list of methods provided by
the *Wells* class use:
```python
help(wmodpy.Wells)
```
You will notice that in many cases the same data can be obtained as either a Python dictionary or as a Pandas Dataframe. Methods
returning a Pandas Dataframe have a suffix of "_df".
```python
f3demo_wells.info()
{'Name': ['F02-1', 'F03-2', 'F03-4', 'F06-1'],
 'UWID': ['', '', '', ''],
 'State': ['', '', '', ''],
 'County': ['', '', '', ''],
 'WellType': ['none', 'none', 'none', 'none'],
 'X': [606554.0, 619101.0, 623255.98, 607903.0],
 'Y': [6080126.0, 6089491.0, 6082586.87, 6077213.0],
 'ReplacementVelocity': [2000.0, 2000.0, 2000.0, 2000.0],
 'GroundElevation': [1.0000000150474662e+30,
  1.0000000150474662e+30,
  1.0000000150474662e+30,
  1.0000000150474662e+30]}
```
```python
f3demo_wells.info_df()
```
{{< figure src="image-04.png"  width="100%" class="img-centered" caption="**Displaying OpendTect well info in a Pandas Dataframe**">}}

Getting well log data in a Pandas Dataframe is as easy as:
```python
f3demo_wells.log_data_df('F02-1',['Vp','Sonic'],0.15, wmodpy.Wells.SampleMode.Upscale)
```
{{< figure src="image-05.png"  width="100%" class="img-centered" caption="**Displaying OpendTect well logs in a Pandas Dataframe**">}}
