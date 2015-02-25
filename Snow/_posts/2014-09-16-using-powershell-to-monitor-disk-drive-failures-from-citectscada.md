---
layout: post
tags: CitectSCADA, VijeoSCADA, Schneider Electric, Citect, SCADA, Powershell, Scripting
categories: Automation
published: draft
title: Using Powershell to monitor disk drive failures from CitectSCADA
---

Today a colleague of mine asked for help with creating a Powershell script for monitoring disk failures from CitectSCADA. He wanted to use the event log to look for specific events related to disk failures. We figured that it would be best if the script was run by Windows Task Scheduler and output a file with current status of disk drives. This way we can run some Cicode periodically to check the status without having to block CitectSCADA while searching the event log.

<!--excerpt-->

We created a function `Evaluate-DiskAlarm` that would evaluate the alarm status of a specified disk. The `Evaluate-DiskAlarm` function in turn depends on another function `Set-Alarm` that writes the alarm state for a disk drive to an INI file. CitectSCADA has nice API for reading INI files so this seemed like a good fit. The source `Server Administrator` is a Dell Disk Controller. 

	function Evaluate-DiskAlarm ($disk) 
	{    
	    $onMessage = "Device failed:  Physical Disk {0}*" -f $disk
	    $offMessage = "Device returned to normal:  Physical Disk {0}*" -f $disk
	
	    $on = Get-EventLog -logname System -source "Server Administrator" -newest 1 -message $onMessage
	    $off = Get-EventLog -logname System -source "Server Administrator" -newest 1 -message $offMessage 
	
	    if(!$on)
	    {
	        Set-Alarm $disk "Off"
	    }
	    elseif($on -and !$off)
	    {
	        Set-Alarm $disk "On"
	    }    
	    elseif($off.TimeGenerated -ge $on.TimeGenerated)
	    {
	        Set-Alarm $disk "Off"
	    }
	    else
	    {
	        Set-Alarm $disk "On"
	    }           
	}

The scheduled script must make calls to `Evaluate-DiskAlarm` and provide an identification of each disk that should be monitored. The events we are looking for use three numbers separated by colons to identify the disks:

    Evaluate-DiskAlarm "0:0:0"
	Evaluate-DiskAlarm "0:0:1"
	Evaluate-DiskAlarm "0:0:2"

And the output will end up in an INI file (functions not included here) looking like this:


My colleague was rather happy with this solution but I could not let go of a thought that it must be possible to monitor that drive status through WMI. CitectSCADA does not have a driver for WMI but since we are already doing this in Powershell why not continue?

I came up with a tiny script fetches information of the installed disk drives and outputs it as comma separated values. That should not be too hard for CitectSCADA to consume since it has been equipped by a brand new database API backed by ADO.NET.

	function Export-DiskStatus ($path)
	{
		Get-WmiObject -class Win32_DiskDrive | 
		Select DeviceId, Caption, Capabilities, ConfigManagerErrorCode, ErrorCleared, LastErrorCode, NeedsCleaning, Status | 
		%{ $_ | Add-Member NoteProperty SmartEnabled ($_.Capabilities -contains 10); $_ } | 
		Select * -Exclude Capabilities |
		Export-Csv $path
	}

I picked the properties of Win32_DiskDevice that seemed related to failures or errors. `ConfigManagerErrorCode`, `ErrorCleared`, `LastErrorCode` and `NeedsCleaning` will be empty if there is nothing to report.

`ErrorCleared` means that any error indicated by `LastErrorCode` is no longer active.

`SmartEnabled` indicates that the drive has SMART Notifications enabled. This feature can predict a failure before it happens. This will be indicated by the  `Status` column (which is OK when everything is... OK)  