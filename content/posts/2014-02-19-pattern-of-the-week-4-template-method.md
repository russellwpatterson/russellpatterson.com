---
author: "Russell Patterson"
date: 2014-02-19 03:44:58+00:00
draft: false
title: 'Pattern of the Week: Template Method'
url: /2014/02/pattern-of-the-week-template-method/
categories:
- Pattern of the Week
- Technical
---

_This is the fourth in a series of "Pattern of the Week" posts. I'm primarily sticking with the [Gang of Four](http://www.amazon.com/gp/product/B000SEIBB8/ref=as_li_qf_sp_asin_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=B000SEIBB8&linkCode=as2&tag=russepatte-20) patterns, but I may branch off occasionally. Thanks for reading._

Type: **Behavioral**

This week's pattern is the Template Method pattern. This pattern allows you to define a set of algorithms that follow the same procedure, but that might have certain parts that differ. For this pattern, I'm borrowing heavily from my post on the [Strategy Pattern](http://russellpatterson.com/2014/02/pattern-of-the-week-3-strategy/), so if you haven't read it yet, you should read that one first.

Alright, let's look at a template method:
 

    
    
    public void Attack()
    {
          Console.WriteLine("{0} is attacking!", GetWarriorName());
    
          var w = GetWeaponOfChoice();
    
          w.Use();
    }



This method, called Attack(), defines a basic algorithm of attack. First, we print out the warrior's name (as a battle cry?), then we get that warrior's weapon of choice, and finally, we use the weapon. Here's the rest of the Warrior abstract class:
 

    
    
    namespace TemplateMethod.Warriors
    {
        public abstract class Warrior : IWarrior
        {
            public void Attack()
            {
                // see above
            }
    
            // This is defined in a derived class
            protected abstract string GetWarriorName();
            protected abstract IWeapon GetWeaponOfChoice();
        }
    }



We use this abstract Warrior class to define specific types of Warriors, like this one:


    
    
    namespace TemplateMethod.Warriors
    {
        public sealed class Samurai : Warrior
        {
            protected override string GetWarriorName()
            {
                return "Samurai";
            }
    
            protected override IWeapon GetWeaponOfChoice()
            {
                return new Sword();
            }
        }
    }



As you can see, the derived class "fills in the blanks" of the template method, by defining what the GetWarriorName() and GetWeaponOfChoice() methods do. We're filling in the blanks of the template by using inheritance. When we call the Attack() method, the methods defined in the derived class are called, completing the algorithm for the type of Warrior we're using.


    
    
    var warrior = new Samurai();
    warrior.Attack();  // prints out "Samurai is attacking!" 
                       // then "Attack with Sword!" 
                       // (per my post on the Strategy Pattern)
    



This is pretty much all there is to the Template Method pattern. If you need additional help, please take a look at the full source code below, or feel free to comment, and I'll respond directly.

Visit next week for an explanation of the Abstract Factory pattern.

[View Sample Code](https://github.com/russellwpatterson/pattern-of-the-week/)
