---
author: "Russell Patterson"
date: 2017-02-11 13:00:09+00:00
draft: false
title: 'New in C# 7.0: Part 1 - Out Variables'
url: /2017/02/new-in-c-7-0-part-1-out-variables/
categories:
- C#
- Technical
---

This is the first post in a series on the new features available in Visual Studio 2017 and C# 7.0. Today, I'm going to be talking about Out Variables.

One of the great new features is probably something you will use frequently, which is defining an out variable, and using that variable in the same statement. Currently, to use an out variable, one must do something like this:


    
    DateTime dt;
    if (DateTime.TryParse("2016-09-14", out dt))
    {
        Console.WriteLine(dt);
    }



With simple syntactic sugar in the new version, you can instead do this:


    
    if (DateTime.TryParse("2016-09-14", out DateTime dt2))
    {
        Console.WriteLine(dt2);
    }
    
    // Also in-scope here.
    Console.WriteLine(dt2);
    



That's pretty much it. This is definitely a small, but useful little addition to the C# language.

Next time, I'll be going over Ref Returns and Ref Locals.
