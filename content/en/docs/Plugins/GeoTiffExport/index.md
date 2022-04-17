---
title: GeotiffExport
description: export OpendTect 3D horizon and attribute data to a GeoTIFF image
weight: 6
categories: ["docs"]
tags: ["Geopackage", "qgis", "geotif"]
---


This plugin, for the open source seismic interpretation platform [opendtect] Version 6.4.0 or later, exports [opendtect] 3D horizon and attribute data to a  [GeoTIFF](https://en.wikipedia.org/wiki/GeoTIFF) image. GeoTIFF is a public domain metadata standard which allows georeferencing information to be embedded within a TIFF image file. GeoTIFF image files are widely supported by GIS software.

## Description

The plugin adds a "Geotiff Export" item to the Survey-Export main menu. Selecting the item opens a dialog box for selecting the 3D horizon and attributes to export and the destination file name. The horizon Z values and attributes values are exported to Float32 bands in the output image. The plugin supports exporting multiple attributes to a single GeoTIFF file, however some GIS packages may not have the flexibility to display individual bands from a Float32 multiband image (eg QGIS v3.6). If multiband images prove to be a problem the option exists to run the plugin multiple times and save each attribute to a separate GeoTIFF file.

### Notes
-  The plugin requires the survey to have a projection based CRS defined.
-  This plugin is actually part of the [geopackageexport] plugin - see notes there as well

{{< figure src="geotiff_qgis.jpg" width="90%" class="img-centered" caption="**OpendTect 3D horizon data displayed in a QGIS print layout**" >}}

## Input Parameters

{{< figure src="geotiff_input.jpg" width="90%" class="img-centered" >}}

