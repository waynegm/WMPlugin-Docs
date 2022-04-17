---
title: GeopackageDisplay
description: display lines and polylines in a Geopackage database on an OpendTect 3D horizon
weight: 4
categories: ["docs"]
tags: ["Geopackage"]
---

This plugin displays lines and polylines from a Geopackage database file over an [opendtect] 3D horizon.

## Description

The plugin adds a "Geopackage Display" item to the "Add" context menu of 3D Horizons in the scene tree. Selecting the item opens a dialog box for selecting the Geopackage file, the layer to display and the line color and width. Multiple layers can be displayed.

{{< figure src="geopackage_display_menu.jpg" width="90%" class="img-centered" caption="**Geopackage Display menu item**" >}}

### Notes
-  The plugin requires the survey to have a projection based CRS defined.
-  This plugin is actually part of the [geopackageexport] plugin - see notes there as well

{{< figure src="geopackage_display_example.jpg" width="90%" class="img-centered" caption="**GIS data draped on an OpendTect 3D horizon**" >}}


