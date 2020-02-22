---
author: "Russell Patterson"
date: 2014-01-25 20:58:34+00:00
draft: false
title: 'Pattern of the Week: Singleton'
url: /2014/01/pattern-of-the-week-singleton/
categories:
- Pattern of the Week
- Technical
---

_This is the first in a (hopefully) long series of "Pattern of the Week" posts. I'm primarily sticking with the Gang of Four patterns, but I may branch off occasionally. Thanks for reading._

Type: **Creational**  
Difficulty: **Beginner**  

Singleton. It is probably the least complicated of all design patterns, yet it can be confusing for beginners. In this post, I will attempt to explain exactly how to create a Singleton, talk about common implementation problems, and provide some sample code so you can see it in action.

The basic idea of a Singleton is simple. I only want **one** of some object. Well, that's easy, right? Don't create more than one. Looks like my work here is done. Well, what if I want to _ensure_ that there is only one instance of a certain class _ever_ created while my application is running? That's where Singleton comes in. Singleton basically protects you from creating more than one of something. It also only creates the instance the first time you use it, i.e., _lazy initialization_. Here's a basic implementation:
 

    
    
    public class Singleton
    {
        private Singleton()
        {
        }
    
        private static Singleton _instance;
        public static Singleton Instance
        {
            get
            {
                if(_instance == null)
                    _instance = new Singleton();
    
                return _instance;
            }
        }
    }
    



The above code is pretty much the simplest way to create a Singleton. It also isn't thread-safe, and it isn't very useful (no properties, members, etc.). Before we go on to that, let's explain what we're looking at. First, you'll notice that the class has a private constructor. This is due to the fact that we don't want people to just do this:


    
    
    var s = new Singleton();
    



You'll also notice a private, static variable on the class called __instance_. This variable is what actually holds the Singleton instance. Finally, you'll notice the _Instance_ property. This is where all the work is done. The getter first checks to see if there is already an instance, and if there isn't, it creates one. Then, it simply returns the instance. This ensures that there is only one.

Now, this is great, right? Not really. What if your application is multi-threaded? Meaning, two threads accessing the Instance property at the same time? Well, thread 1 will hit the if statement, and say, "I need to create an instance." Maybe thread 2 will hit that same if statement before the instance is created, and it'll say, "I need to create an instance." So, it's actually possible to end up with two threads with two different instances of Singleton. Fixing this is simple though. See the below corrected code:
 

    
    
    public class Singleton
    {
        private Singleton()
        {
        }
    
        private static readonly object LockObj = new object();
            
        private static Singleton _instance;
        public static Singleton Instance
        {
            get
            {
                lock (LockObj)
                { 
                    if(_instance == null)
                        _instance = new Singleton();
    
                    return _instance;
                }
            }
        }
    }
    



I've added a static lock object that will prevent more than one thread from going through the instantiate + return code. This means that if the threads reach the code at around the same time, the later one will have to wait. So, looks like we've solved all the problems with Singleton. Wait, what if I create a derived class? You can't create a derived class outside of the Singleton class, since the constructor is private, but what if you create one inside of Singleton?
 

    
    
    public class Singleton
    {
        private Singleton()
        {
        }
    
        private static readonly object LockObj = new object();
            
        private static Singleton _instance;
        public static Singleton Instance
        {
            get
            {
                lock (LockObj)
                { 
                    if(_instance == null)
                        _instance = new Singleton();
    
                    return _instance;
                }
            }
        }
    
        public class Singleton2 : Singleton
        {
        }
    }
    



Then, somewhere in your code, say: 


    
    
    var s2 = new Singleton.Singleton2();
    



Guess what? You've just created two instances of a Singleton class! How do we fix it? Simple. Add the _sealed_ modifier on to the Singleton class. Sealed classes cannot be derived. Here's our final code:


    
    
    public sealed class Singleton
    {
        private Singleton()
        {
        }
    
        private static readonly object LockObj = new object();
            
        private static Singleton _instance;
        public static Singleton Instance
        {
            get
            {
                lock (LockObj)
                { 
                    if(_instance == null)
                        _instance = new Singleton();
    
                    return _instance;
                }
            }
        }
    }
    



To make this useful, you would simply add properties to the Singleton class, then access them like this:


    
    
    // Setting the value
    Singleton.Instance.SomeProperty = "whatever";
    
    // Getting the value
    var x = Singleton.Instance.SomeProperty;
    



That's all! Visit next week for an explanation of the Decorator pattern.

[View Sample Code](https://github.com/rwpcpe/pattern-of-the-week/)
