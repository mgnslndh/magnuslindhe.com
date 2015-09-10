---
layout: post
tags: mitsubishi, plc, automation, usb
category: Automation
title: Multiple CPU Configuration errors
---

I am writing a client API in C# for the MELSEC Communication Protocol and wanted to perform a communication test to a PLC. The PLC system I had available was a two CPU system and I used GX IEC Developer to create a simple test program. Since it was a simple communication test to see if the client API was reading and writing devices correctly I was not interested in the second CPU at all.

However, I could not get the PLC program running because of a `CPU LAY ERROR`. This can be fixed by configuring the correct number of CPU in the system. I then received a `MULTI CPU DOWN` error which seemed to occur because the default setting is to share memory between multiple CPU. When this setting was removed I got the program running and could proceed with the communication test. 

![Multiple CPU settings in GX IEC Developer](/images/2015-09-10-multiple-cpu-settings.png)

- Make sure the correct "No. of CPU" is specified.
- Make sure the "Host CPU number" is specified
- Make sure that "Use multiple CPU high speed transmission" is unchecked. 

Hopefully this post will be of use to me or somebody else in the future.