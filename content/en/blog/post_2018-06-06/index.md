---
date: 2018-06-06
title: Python External Attribute Tips & Tricks - Logging
tags: ["python","ExternalAttrib"]
categories: ["howto"]
author: Wayne Mogg
banner: /blog/post_2018-06-06/18_06_06_02.png
---


## Introduction
It is possible to write information to the OpendTect logfile from inside a Python [External Attribute]({{<relref "/externalattrib" >}}) script.

The global variable *xa.logH* (assuming the extattrib module has been imported using *import extattrib as xa*) is a [Python logger object](https://docs.python.org/3/library/logging.html).

## An Example
{{< figure src="18_06_06_01.png"  width="90%" class="img-centered" >}}

On line 18 the Python logger is modified by adjusting the severity level of messages that will appear in the log file. By default only CRITICAL, ERROR and WARNING messages will be written.

On line 22 a message is written to the logfile showing the full path to the Python interpreter executing the script. As this line is in the Compute Loop Initialisation section it is only written at each invocation of the script.

On line 32 a message is written that identifies the location, minimum and maximum of the trace being processed. As this line is in the Compute Loop a message is output for every trace processed.

## The Result
{{< figure src="18_06_06_02.png"  width="90%" class="img-centered" >}}

