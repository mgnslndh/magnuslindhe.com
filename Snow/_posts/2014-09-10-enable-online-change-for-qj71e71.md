---
layout: post
tags: PLC, Mitsubishi, MELSEC, QJ71E71, E71, MC Protocol, GX Works2
category: Automation
title: Enable online changes for QJ71E71
---

The Mitsubishi QJ71E71 is an ethernet module that can be used to communicate with a Mitsubishi Q-series PLC from an external application. The default setting is however to deny write requests when the PLC is in run mode. In order for external applications to make changes to device registers in the PLC this setting needs to be changed.

<!--excerpt-->

The QJ71E71 can easily be configured to allow write requests from external applications during run mode and this is how you do it using GX Works2:

1. Open a project and expand the "Parameter" and "Network Parameter nodes"
2. Open up the module configuration window by double clicking on the node "Ethernet / CC IE / MELSECNET"
3. Click on the button "Operation Setting" to open the ethernet operation settings.

![Enable Online Change](/images/2014-09-10-GXWorks-Configure-Ethernet.png)

4. Tick the check box labeled "Enable Online Change" to enable external applications to exchange data when the PLC is in run mode. 

![Enable Online Change](/images/2014-09-10-GXWorks-enable-online-change.png)

<div class="alert alert-info">In GX Developer which is an older development environment this option is called "Enable Write at RUN time".</div>

Data communication with the QJ71E71 is carried out using the MELSEC Communication Protocol (MC Protocol) using either UDP or TCP. MC Protocol supports communication in both binary and ASCII formats.



