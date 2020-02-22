---
author: "Russell Patterson"
date: 2018-04-01 23:00:33+00:00
draft: false
title: 'New in C# 7.0: Part 4 - Expression-Bodied Members'
url: /2018/04/new-in-c-7-0-part-4-expression-bodied-members/
categories:
- C#
- Technical
---

This week, we're discussing Expression-Bodied Members in C# 7.0. Now, this was an existing feature in C# 6.0, but it was limited to only methods, like so:


    
    public void DoAThingCS6() => Console.WriteLine("This is a test");



With the new additions in C# 7.0, we can now do Constructors, Deconstructors, and Properties. A Constructor definition looks like this:


    
    public SomeClass() => DoAThing();



Similarly, a Deconstructor looks like this:
 

    
    ~SomeClass() => DoAThing();



Finally, although auto-properties are shorter, you can write properties with specific implementations with this new shorthand:
 

    
    private string someField;
    public string SomeProperty 
    {
        get => someField;
        set => someField = value;
    }



That's it for this week. Next week, we'll go over Pattern Matching.
