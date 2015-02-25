---
layout: post
category: SQL Server
tags: SQL, SQL Server
published: 2014-10-07
title: How to determine the version and edition of a SQL Server instance?
---

A colleague recently asked me how to determine the version and edition of an SQL Server instance. Microsoft has a good [knowledge base article](http://support.microsoft.com/kb/321185) explaining it. There are the two ways I prefer of getting the version and edtion:

If you only need to do a quick check to find out the information I would just run the following query:

    SELECT @@version

Which would produce something similar to this:

    Microsoft SQL Server 2008 (SP1) - 10.0.2531.0 (X64)   Mar 29 2009 
    10:11:52   Copyright (c) 1988-2008 Microsoft Corporation  Express 
    Edition (64-bit) on Windows NT 6.1 <X64> (Build 7600: )

Or you might need the information in a more structured way. Then you could run the following query: 

    SELECT SERVERPROPERTY('productversion'), SERVERPROPERTY ('productlevel'), SERVERPROPERTY ('edition')
