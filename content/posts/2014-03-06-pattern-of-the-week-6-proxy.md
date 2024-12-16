---
author: "Russell Patterson"
date: 2014-03-06 05:03:57+00:00
draft: false
title: 'Pattern of the Week: Proxy'
url: /2014/03/pattern-of-the-week-proxy/
categories:
- Pattern of the Week
- Technical
---

_This is the sixth in a series of "Pattern of the Week" posts. I'm primarily sticking with the [Gang of Four](http://www.amazon.com/gp/product/B000SEIBB8/ref=as_li_qf_sp_asin_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=B000SEIBB8&linkCode=as2&tag=russepatte-20) patterns, but I may branch off occasionally. Thanks for reading._

Type: **Structural**

This week's pattern is called the Proxy pattern. This pattern is primarily used to add security or to implement caching for objects. For my example, I'll be adding security to this class:
 

    
    public class SomeService : ISomeService
    {
        public List<string> GetStrings()
        {
            return new List<string>
                {
                    "String1",
                    "String2",
                    "String3"
                };
        }
    }



This is a pretty simple class, which implements the following interface:
 

    
    public interface ISomeService
    {
        List<string> GetStrings();
    }



Now, suppose I want to make sure that not everyone has access to the GetStrings method. Well, I could modify the GetStrings method itself, and add some complex code to check a user's permissions, or I could implement a Proxy to do that for me. The main benefit to using this approach is that I don't overly complicate GetStrings, and I can [separate these two concerns](http://en.wikipedia.org/wiki/Separation_of_concerns) (permissions and data access). Here's my Proxy class:
 

    
    public class SomeServiceProxy : ISomeService
    {
        private readonly ISomeService _someService;
    
        public SomeServiceProxy()
        {
            _someService = new SomeService();
        }
    
        public List<string> GetStrings()
        {
            ValidateAccess("GetStrings");
    
            return _someService.GetStrings();
        }
    
        private void ValidateAccess(string methodName)
        {
            // Here, we could call some other class to get whether 
            // the user has access to this whatever method they're accessing.
            // We could throw an exception if they dont have access.
            throw new SecurityException("You don't have access to this action.");
        }
    }



The proxy implements the same interface as the original class. This means that you should be able to swap the proxy for the original object with minimal code changes. So how does this all work? Basically, we would use the Proxy to access the object, and if the user doesn't have access (which we're not checking here), a SecurityException will be thrown, preventing access to the underlying resource. Obviously, in a real-world use of this pattern, you would actually check the user's permissions in the ValidateAccess method (and always remember to default to least privilege on errors).

You may notice that this pattern is fairly similar to the [Decorator](http://russellpatterson.com/2014/02/pattern-of-the-week-2-decorator/) pattern. The difference between the two, as far as I can tell, is that the Proxy actually owns the object that it is adding functionality to (it creates it), while the Decorator has the object passed in as a parameter in the constructor.

This is pretty much all there is to this pattern. If you need additional help, please take a look at the full source code below, or feel free to comment, and I'll respond directly.

Visit next week for an explanation of the Prototype pattern.

[View Sample Code](https://github.com/russellwpatterson/pattern-of-the-week/)
