---
author: "Russell Patterson"
date: 2014-02-13 03:31:53+00:00
draft: false
title: 'Pattern of the Week: Strategy'
url: /2014/02/pattern-of-the-week-strategy/
categories:
- Pattern of the Week
- Technical
---

_This is the third in a series of "Pattern of the Week" posts. I'm primarily sticking with the [Gang of Four](http://www.amazon.com/gp/product/B000SEIBB8/ref=as_li_qf_sp_asin_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=B000SEIBB8&linkCode=as2&tag=russepatte-20) patterns, but I may branch off occasionally. Thanks for reading._

Type: **Behavioral**  
Difficulty: **Beginner**

This week's pattern is the Strategy pattern. This pattern can be used when you have a set of similar algorithms. The easiest way to explain it is with an example, so let's look at the following class:
 

    
    
    namespace Strategy
    {
        public class Warrior
        {
            private readonly IWeapon _primaryWeapon;
            public Warrior(IWeapon primaryWeapon)
            {
                _primaryWeapon = primaryWeapon;
            }
    
            public void Attack()
            {
                _primaryWeapon.Use();
            }
        }
    }
    



Here we have a class that represents a _Warrior_. There is a primary weapon that is passed into the constructor. The warrior has a method called Attack, which uses that weapon. Let's look at the IWeapon interface.


    
    
    namespace Strategy
    {
        public interface IWeapon
        {
            void Use();
        }
    }
    



This interface has just one method, Use(). When the Warrior needs to attack, he needs to be able to use his weapon. Seems pretty straightforward, right? No matter what kind of weapon that the warrior has, he needs to _use_ that weapon in order to attack. The only difference between each type of weapon is _how_ the warrior uses it. This is the essence of the Strategy pattern. It allows the ability to change the how without changing the what. Let's take a look at the implementations of the IWeapon interface.


    
    
    namespace Strategy
    {
        public class Sword : IWeapon
        {
            public void Use()
            {
                Console.WriteLine("Attack with Sword!");
            }
        }
    
        public class Shotgun : IWeapon
        {
            public void Use()
            {
                Console.WriteLine("Attack with shotgun!");
            }
        }
    
        public class Grenade : IWeapon
        {
            public void Use()
            {
                Console.WriteLine("Attack with a grenade! BOOM!");
            }
        }
    }
    



For example's sake, I didn't elaborate on how the warrior would use each weapon, but obviously there are huge differences. One slashes with a sword, fires a shotgun, and throws a grenade. However, how the warrior approaches using a weapon is the same: he thinks, "I need to use my weapon", and then he does whatever it takes to do that.

So, how do we use this? It's pretty simple. If we want a Warrior who uses a Sword, we do this:

    
    
    var warriorWithSword = new Warrior(new Sword());
    



We would do the same thing for all of the other weapon types too.

This pattern may look very familiar to those of us who use [Dependency Injection](http://en.wikipedia.org/wiki/Dependency_injection), or more specifically, Constructor Injection. Constructor Injection is probably the most widely used example of the Strategy pattern, but there are other things you can use it for as well. An example that comes to mind is that you could implement data access as a strategy pattern, then pass in the proper implementation based on the database server type that you are using.

That’s all! Visit next week for an explanation of the Template Method pattern.

[View Sample Code](https://github.com/russellwpatterson/pattern-of-the-week/)
