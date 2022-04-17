---
title: Installation
layout: page
weight: 1
description: binary installation
---

**As of OpendTect 6.4.5 this suite of plugins can be installed using the OpendTect Installation Manager. Just activate the WMPlugins
option in the installer.**

{{< figure src="od_install_mgr.jpg"  class="img-centered" caption="**OpendTect Installation Manager**">}}

This will automatically install the latest available version of the plugin for your OpendTect installation into the OpendTect
installation folder.

Compiled versions of the plugins for Linux x86_64 and Windows x86_64 are also available for download from the
[GitHub project release page.](https://github.com/waynegm/OpendTect-Plugins/releases)

Note that the plugin  version installed should match the OpendTect version. For example the 6.4 series of plugin binaries
should work with all OpendTect 6.4 releases but won't work with OpendTect 6.0, 6.2 or 6.6.

The following instructions are only needed for a manual intallation.

## Linux

### Sitewide Installation
To install the plugins into the OpendTect program folder (eg __/opt/seismic/OpendTect/6.4.0/ __):

1. Copy the contents of the __bin/lux64/Release/__ folder in the tgz file to __/opt/seismic/OpendTect/6.4.0/bin/lux64/Release/__;

2. Copy the contents of the __plugins/lux64/__ folder in the tgz file to __/opt/Seismic/OpendTect/6.4.0/plugins/lux64/__; and

3. Restart OpendTect.

### Per-user Installation

On Linux it is also possible to install the plugin files in a users __.od__ folder. Note that the OpendTect-6.4.0-plugins won't work in OpendTect 6.2.0 and the OpendTect-6.2.0-plugins won't work in OpendTect 6.4.0. See the [faq] for a workaround if you want a per-user installation and want to run multiple versions of OpendTect.

1. Copy the contents of the __bin/lux64/Release/__ folder in the tgz file to the users __.od/bin/lux64/Release/__ folder;

2. Copy the contents of the __plugins/lux64/__ folder in the tgz file to the users __.od/plugins/lux64/__ folder; and

3. Restart OpendTect.

## Windows

### Sitewide Installation
To install the plugins into the OpendTect program folder (eg __c:\Program Files\Opendtect\6.4.0 __):

1. Copy the contents of the __bin\win64\Release\ __ folder in the zip file to __c:\Program Files\Opendtect\6.4.0\bin\win64\Release\ __;

2. Copy the contents of the __plugins\win64\ __ folder in the zip file to __c:\Program Files\Opendtect\6.4.0\plugins\win64\ __; and

3. Restart OpendTect.

### Per-user Installation

On Windows it is also possible to install the plugin files in a users __.od__ folder. Note that the OpendTect-6.4.0-plugins won't work in OpendTect 6.2 and the OpendTect-6.2-plugins won't work in OpendTect 6.4. See the [faq] for a workaround if you want a per-user installation and want to run multiple versions of OpendTect.

1. Copy the contents of the __bin\win64\Release\ __ folder in the zip file to the users __C:\Users\%username%\\.od\bin\win64\Release\ __ folder;

2. Copy the contents of the __plugins\win64\ __ folder in the zip file to the users __C:\Users\%username%\\.od\plugins\win64\ __ folder; and

3. Restart OpendTect.
