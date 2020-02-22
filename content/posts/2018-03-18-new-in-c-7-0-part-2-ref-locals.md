---
author: "Russell Patterson"
date: 2018-03-18 23:22:39+00:00
draft: false
title: 'New in C# 7.0: Part 2 – Ref Locals'
url: /2018/03/new-in-c-7-0-part-2-ref-locals/
categories:
- C#
- Technical
---

After about a year, I'm finally trying to start writing some more blog posts, so I'll pick up right where I left off. Today, I'm going to give a brief overview of Ref Locals.

Ref Locals allow you to create an alias for a variable so that you are not creating another copy of the data or reference (in the case of an object), in memory. In previous versions of C#, if you wanted to refer to a local variable with a different name, you'd have to do this:
 

    
    var original1 = "This is a test";
    var copy1 = original1;
                
    original1 = "whatever";
                
    Console.WriteLine("Not Ref Locals:");
    Console.WriteLine(original1);   // "whatever"
    Console.WriteLine(copy1);       // "This is a test"



This unfortunately creates another copy of the variable, so changes to the original are not reflected in the copy. With Ref Locals, you can ensure changes are reflected in both places:


    
    var original2 = "This is a test";
    ref var copy2 = ref original2;
    
    copy2 = "whatever";
    
    Console.WriteLine("Ref Locals:");
    Console.WriteLine(original2);   // "whatever"
    Console.WriteLine(copy2);       // "whatever"



This is particularly helpful when dealing with arrays of items.
 

    
    string[] arrayOfStrings = { "this", "is", "a", "test" };
    var thirdItem = arrayOfStrings[2];      // a
    
    thirdItem = "not a";
    
    Console.WriteLine(string.Join(" ", arrayOfStrings));    // this is a test
    
    ref var thirdItemRef = ref arrayOfStrings[2];        // a
    
    thirdItemRef = "not a";
    
    Console.WriteLine(string.Join(" ", arrayOfStrings));    // this is not a test



The changes will be reflected in the array itself, instead of just in the copy version of the variable.

That's it for today. Next week is Ref Returns.
