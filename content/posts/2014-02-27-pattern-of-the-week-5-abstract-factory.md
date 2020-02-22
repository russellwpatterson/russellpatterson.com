---
author: "Russell Patterson"
date: 2014-02-27 04:42:16+00:00
draft: false
title: 'Pattern of the Week: Abstract Factory'
url: /2014/02/pattern-of-the-week-abstract-factory/
categories:
- Pattern of the Week
- Technical
---

_This is the fifth in a series of "Pattern of the Week" posts. I'm primarily sticking with the [Gang of Four](http://www.amazon.com/gp/product/B000SEIBB8/ref=as_li_qf_sp_asin_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=B000SEIBB8&linkCode=as2&tag=russepatte-20) patterns, but I may branch off occasionally. Thanks for reading._

Type: **Creational**

This week's pattern is the Abstract Factory pattern. To explain this, we must first understand the **factory class**.

Factories create things, plain and simple. Whether we're talking about software development or retail, that is what they do. Factory classes typically look something like this:
 

    
    public ISomething CreateSomething()
    {
        return new ConcreteSomething();
    }



The method creates an instance of its favorite implementation of the interface that is returned. Obviously, with a simple code change, you could swap out "ConcreteSomething" for "SpecialSomething" and your code would still work, assuming of course that those are both implementations of _ISomething_. This is a central idea of a SOLID principle, called the [Liskov Substitution Principle](http://en.wikipedia.org/wiki/Liskov_substitution_principle). Basically, we should be able to swap out an implementation of an interface without breaking our code, or changing the behavior of the application, i.e., post-conditions of using the interface should be the same no matter the implementation that we use. Now that we've talked about Factories and [Barbara Liskov](http://en.wikipedia.org/wiki/Barbara_Liskov), let's go back to the pattern at hand.

The Abstract Factory pattern can be used when you want to define different versions of the same _family_ of interfaces in your application. You know that you need certain objects that implement certain interfaces, but you might need to swap out which ones you use depending on a number of factors (which OS, database server, etc.). The implementation of certain interfaces that you end up using is completely dependent on what implementation of the factory you're using. Here's an abstract factory interface, which creates clothes (kind of like a real factory!):
 

    
    
    public interface IClothesFactory
    {
        IShirt CreateShirt();
        IPants CreatePants();
    }



This interface defines two methods: CreateShirt(), and CreatePants(). These methods return IShirt and IPants respectively. Let's look at those interfaces:
 

    
    public interface IShirt
    {
        void DescribeShirt();
    }
    
    public interface IPants
    {
        void DescribePants();
    }



Alright, so we now have defined our interfaces that we will use in the factory. So what do we do next? Well, an interface is fairly useless without implementations, so let's create some. Here is a DressClothesFactory:
 

    
    
    public class DressClothesFactory : IClothesFactory
    {
        public IShirt CreateShirt()
        {
            return new DressShirt();
        }
    
        public IPants CreatePants()
        {
            return new DressPants();
        }
    }



Simple enough, right? The factory defines the CreateShirt() method as returning a _DressShirt_, which is an implementation of _IShirt_, and it defines CreatePants() as returning _DressPants_, which is an implementation of _IPants_. We could also define a _CasualClothesFactory_ which would return a T-Shirt and Jeans respectively.

The real power of this is when we define a method or class that takes an abstract factory implementation, and uses it to instantiate the classes that it needs. For example, let's look at the ShowWhatAmIWearingToday() method:
 

    
    private void ShowWhatAmIWearingToday(IClothesFactory factory)
    {
        Console.WriteLine("Here's what I'm wearing today:");
    
        var shirt = factory.CreateShirt();
        shirt.DescribeShirt();
    
        var pants = factory.CreatePants();
        pants.DescribePants();
    }



We know ahead of time that we need to get a shirt and get pants, but we don't really care if it's a casual day or a dress-up day. We still need those two things no matter what, the only difference is what specific family of IShirt/IPants we're using.

This is pretty much all there is to this pattern. If you need additional help, please take a look at the full source code below, or feel free to comment, and I'll respond directly.

Visit next week for an explanation of the Proxy pattern.

[View Sample Code](https://github.com/rwpcpe/pattern-of-the-week/)
