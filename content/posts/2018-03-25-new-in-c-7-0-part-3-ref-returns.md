---
author: "Russell Patterson"
date: 2018-03-25 23:00:10+00:00
draft: false
title: 'New in C# 7.0: Part 3 – Ref Returns'
url: /2018/03/new-in-c-7-0-part-3-ref-returns/
categories:
- C#
- Technical
---

Picking up where I left off last week, there's another interesting new feature called "Ref Returns". Similar to Ref Locals, this allows you to return a reference from a method, and then optionally use it as a Ref Local in the calling code.

Let's look at the following method definition:
 

    
    private static string[] strings = { "this", "is", "a", "test" };
    
    public static ref string GetSomeString(int number)
    {
        if (number < 0 || number >= strings.Length) 
            throw new IndexOutOfRangeException();
    
        // Returns a reference to the actual string, instead of just a copy of it.
        return ref strings[number];
    }



The method takes an integer, and returns an entry from an array with that index. The important differences from a normal method is the ref keyword in the method signature, and the ref keyword after the return keyword. This tells the compiler that you want the method to return a reference to the variable/object, instead of passing it back by value.

When calling the method, we do this, defining a Ref Local in the process:


    
    ref var stringIWant = ref GetSomeString(2);



Or, if we don't want to use it as a reference, and just want to use the value, we can omit the ref keyword in both places.


    
    var stringIWant = GetSomeString(2);



That's it for this week. Next week, we'll be talking about Expression-Bodied Members.
