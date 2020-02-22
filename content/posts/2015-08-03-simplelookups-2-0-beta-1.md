---
author: "Russell Patterson"
date: 2015-08-03 04:49:30+00:00
draft: false
title: SimpleLookups 2.0 Beta 1
url: /2015/08/simplelookups-2-0-beta-1/
categories:
- Simple Lookups
---

Today, I'm releasing the first beta of SimpleLookups v2.0. This version includes the following changes: 

New Features:
- Lookup Caching
- Core improvements/optimizations.
- Support for .NET 4.5.1, 4.5.2, and 4.6.

Removed Features:
- The final version will not support .NET 2.0 and 3.0.

Caching is enabled by default. You can turn it off by adding the following attribute to the  node in your web.config: enableCaching="false". Or, if you use the SimpleLookups.Initialize() method, there's now a set of overloads that deal with caching.

Version 2.0b1 can be downloaded [here](http://simplelookups.com/releases/2.0/SimpleLookups.2.0.0-beta1.zip).

If you run into any issues at all, please email youdidthatwrong@russellwritescode.com and I'll take a look at the issue.

I have a few cleanup tasks to do over the next week or two, so expect the final version to be ready around August 16th. Source will also be released at that time.
