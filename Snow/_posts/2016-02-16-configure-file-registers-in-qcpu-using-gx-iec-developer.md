---
layout: post
tags: mitsubishi, qcpu, plc, ethernet, mc protocol
category: Automation
title: Configure file registers in QCPU using GX IEC Developer
---

If you get the error code 0x4031 when using MC Protocol to communicate with a QCPU it means that you are trying to read or write to a device address that is out of range. You might as, I did, forgot to setup the file registers in GX IEC Developer.

![Q Parameter Setting](..\images\2016-02-16-q-parameter-setting.png)
