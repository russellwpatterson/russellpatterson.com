---
author: "Russell Patterson"
date: 2014-05-18 19:28:49+00:00
draft: false
title: GIT, Powershell, and Windows 8.1
url: /2014/05/git-powershell-and-windows-8-1/
categories:
- Technical
---

This weekend I opted to upgrade(depending on your opinion) my laptop to Windows 8.1. Now that I have lost all credibility, I can move on to talk about my experience with using GIT on Windows 8.1, and the issue I had with my PowerShell profile script.

Like many users, I have a profile script set up in PowerShell so that when I open it, my main code directory is the working directory, and I also have a custom prompt set up to tell me the current folder's GIT status. I wish I could give credit where it is due on this script, but unfortunately I don't know who wrote the original, original version. It was passed to me by my coworkers and I've made some changes/fixes to it to fit my environment.

[![powershellwithgit](/media/powershellwithgit-300x35.png)
](/media/powershellwithgit.png)

As you can see in the image on the left, my PowerShell prompt shows the current branch, master, the current directory, and the status of my local copy (c = created, u = updated, d = deleted).  When I moved to Windows 8.1 (with PowerShell 4.0), the script naturally stopped working properly. So, as a help to anyone out there that also uses this type of script and is making the jump, here's a working version for Windows 8.1, which also works on Windows 7 (PowerShell 2.0+). You have to place it in the following location and it should be named this way for it to work properly:

DRIVE:\Users\USERNAME\Documents\WindowsPowershell\Microsoft.PowerShell_profile.ps1

You can verify this location on your machine by typing "$profile" into PowerShell.

Here's the script. Make sure you replace my working path with your own:
 

    
    Set-Location D:\Development\Git\Private\RWPCode
    	
    function prompt {
        Write-Host("")
        $status_string = ""
        $symbolicref = git symbolic-ref HEAD
        if($symbolicref -ne $NULL) {
            $status_string += "GIT [" + $symbolicref.substring($symbolicref.LastIndexOf("/") +1) + "] "
    
            $differences = (git diff-index --name-status HEAD)
    		$differences = if ($differences -eq $null) { "" } else { $differences }
    				
    		$git_update_count = 0
    		$differences -match "M`t" | Out-Null
    		
    		if($matches -ne $null) {		
    			$git_update_count = $matches.count
    			$matches.clear()
    		}
    		
    		$git_create_count = 0
    		$differences -match "A`t" | Out-Null
    		
    		if($matches -ne $null) {
    			$git_create_count = $matches.count
    			$matches.clear()
    		}
    		
    		$git_delete_count = 0
    		$differences -match "D`t" | Out-Null
    		if($matches -ne $null) {
    			$git_delete_count = $matches.count
    			$matches.clear()
    		}
    
            $status_string += "(c:" + $git_create_count + " u:" + $git_update_count + " d:" + $git_delete_count + ") "
        }
        else {
            $status_string = "PS "
        }
    
        if ($status_string.StartsWith("GIT")) {
            Write-Host ($status_string + $(get-location) + ">") -nonewline -foregroundcolor yellow
        }
        else {
            Write-Host ($status_string + $(get-location) + ">") -nonewline -foregroundcolor white
        }
        return " "
     }



In order to run this, you must first run the following command in PowerShell as an administrator, which will allow you to run unsigned scripts:
 

    
    Set-ExecutionPolicy Unrestricted



There's more information about signed/unsigned PowerShell scripts [here](http://www.hanselman.com/blog/SigningPowerShellScripts.aspx).

Any suggestions for improvement? Hit me up in the comments.

