---
layout: post
tags: virtualization
category: Miscellaneous
title: VMware Player with 64-bit guest operating system
---

I was greeted with the following dialong when trying to start a Windows Server 2008 virtual machine in VMware Player on my 64-bit Windows 7 laptop:

<!--excerpt-->

![This virtual machine is configured for 64-bit guest operating systems](/images/2012-04-11-vmwareplayer-64-bit-guest-os.png)

The provided link explains [the requirements for running a 64-bit guest in VMware products](http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1003945) but the dialog pretty much tells me what I need to do: 

* Reeboot and enable VT (Virtualization Technology) in BIOS

After performing the required configuration I once again started the Windows Server 2008 virtual machine and it booted as expected. My HP EliteBook 8560p also had an option [Virtualization Technology for Directed I/O](http://www.intel.com/technology/itj/2006/v10i3/2-io/5-platform-hardware-support.htm) which I kept disabled. I am not sure if it is supported by VMware Player 4.0.2 or not.

VMware has a [utility](http://downloads.vmware.com/d/details/processor_check_5_5_dt/dCpiQGhkYmRAZQ==) that can be used to determine if the host processor is capable of running 64 bit guest operating systems.   

