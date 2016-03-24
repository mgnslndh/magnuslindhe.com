---
layout: post
tags: mitsubishi, plc, automation
category: Automation
title: Host station port number is expressed using a hexadecimal number
---

Just a quick reminder to my self in case I make this mistake in the future. The configuration of the built-in ethernet port open settings in GX Developer IEC requires port numbers to be expressed in hex. 

This can be confusing if the configured port number only use digits between 0 and 9 like my current configuration. I managed to get confused by this even though the dialog explicitly states that you need to use hexadecimal numbers for the port configuration. 

![Built-in ethernet port open settings](/images/2016-03-24-built-in-ethernet-port-open-settings-hexadecimal.png)

If you take a quick look at it and try to send a request to port 1392 you will not succeed:

    client.Open("192.168.0.1", 1392);
    client.ReadWords("D0", 1); 

The correct code also needs to use the hexadecimal number:

    client.Open("192.168.0.1", 0x1392);
    
Or use the correct decimal number:

    client.Open("192.168.0.1", 5010);