---
layout: post
tags: mitsubishi, plc, automation, usb
category: Automation
title: Install Mitsubishi Easysocket USB Drivers on Windows 8
---

After installing GX Works 2 1.501X on my Windows 8 development laptop I found out that I was not able to communicate with the PLC through the USB cable as usual. After some troubleshooting I found out that the Mitsubishi Easysocket USB drivers has not been installed properly:

![Mitsubishi Easysocker USB Driver not installed correctly on Windows 8](/images/2015-09-09-melsec-usb-driver-warning.png)

This issue can easily be fixed by updating the drivers. Just follow these steps:

1. Open Device Manager
2. Locate the USB driver named "MELSEC" as depicted in the image above
3. Right click on the driver and select "Update Driver Software" from the context menu.
4. Click on "Browse my computer for dirver software"
5. Browse to the installation directory of Easysocket and select the sub folder "USBDrivers". My location was "C:\Program Files (x86)\MELSOFT\Easysocket\USBDrivers" but it could depend on where GX Works2 was installed.
6. Click "Install" when Device Manager identifies the driver as "Easysocket USB Drivers" from Mitsubishi Electric Corporation.

!["Easysocket USB Drivers" from Mitsubishi Electric Corporation](/images/2015-09-09-melsec-usb-driver-found.png)

Device Manager should be able to find the driver and update it successfully. When the installation is done the driver should appear with the name "MITSUBISHI Easysocket Driver" like this in Device Manager:

![Working installation of "Easysocket USB Drivers"](/images/2015-09-09-melsec-usb-driver-ok.png)

