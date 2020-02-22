---
author: "Russell Patterson"
date: 2014-09-29 04:04:55+00:00
draft: false
title: 'iOS 8: Notifications Changes'
url: /2014/09/ios-8-notifications-changes/
categories:
- iOS
- Technical
---

We're updating our iOS application at work, and I came across some fun with iOS 8 and notifications. So, I thought I'd write a short post about it.

In iOS 7, we used the following method on the shared UIApplication instance to set up notifications:
 

    
    
    [[UIApplication sharedApplication] registerForRemoteNotificationTypes:(
                                                             UIRemoteNotificationTypeAlert |
                                                             UIRemoteNotificationTypeBadge |
                                                             UIRemoteNotificationTypeSound
                                                             )];
    



In iOS 8, this doesn't work. So now, it's a multi-step process:

    
    
    UIApplication *application = [UIApplication sharedApplication];
    
    UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeAlert |
                                                                                         UIUserNotificationTypeBadge |
                                                                                         UIUserNotificationTypeSound)
                                                                             categories:nil];
    [application registerUserNotificationSettings:settings];
    [application registerForRemoteNotifications];
    



First, we get an instance of the shared _UIApplication_ (this is obviously optional, but I think it makes the code easier to read). Then, we create a UIUserNotificationSettings instance that specifies which notifications we want. After that, we register for user notifications, and finally, register for remote notifications. 

The new method, _registerForRemoteNotifications:_, sends the same messages as the _registerForRemoteNotificationTypes:_ method. These are _application:didRegisterForRemoteNotificationsWithDeviceToken:_ for a successful registration, and _application:didFailToRegisterForRemoteNotificationsWithError:_ for an error.

Well, what if you want to support both iOS 7 and iOS 8? It's simple. See if the _UIApplication_ instance responds to the new selector. Here's the complete code:


    
    
    UIApplication *application = [UIApplication sharedApplication];
        
    if([application respondsToSelector:@selector(registerUserNotificationSettings:)])  // iOS 8
    {
        UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeAlert |
                                                                                             UIUserNotificationTypeBadge |
                                                                                             UIUserNotificationTypeSound)
                                                                                 categories:nil];
        [application registerUserNotificationSettings:settings];
        [application registerForRemoteNotifications];
    }
    else // iOS < 8
    {
        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeAlert |
                                                         UIRemoteNotificationTypeBadge |
                                                         UIRemoteNotificationTypeSound)];
    }
    



Let me know if you have any questions or if there's a better way to do this in the comments. 

**EDIT: I originally messed up the if statement in the complete code above. I used _registerUserNotificationSettings_ instead of _registerUserNotificationSettings:_ which caused the statement to be false, even on iOS 8.**
