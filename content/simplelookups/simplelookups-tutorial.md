---
author: "Russell Patterson"
date: 2013-12-22 00:44:18+00:00
draft: false
title: SimpleLookups Tutorial
type: page
url: /simplelookups-api/simplelookups-tutorial
---

SimpleLookups is a small .NET library that is designed to make "lookup" values easy to retrieve from a SQL Server database. For example, if you have a database that is full of Employees, you might have an EmployeeType table. Instead of writing all the code necessary to list these, or even get one of them, you can use SimpleLookups. All I ask is that you follow a specific format on your tables. They have to look like this (for EmployeeType example):

    
    EmployeeTypeId INT
    EmployeeTypeName VARCHAR(..)
    EmployeeTypeCode VARCHAR(..)
    EmployeeTypeDescription VARCHAR(..)
    Active BIT


But, let's face it. They probably already do.

Here's how you use it:

1. Initialize SimpleLookups in your application's startup code, using your connection string. You can load this from your app.config/web.config, or simply hard-code it. You can also configure the connection strings you want to use through the [web.config file](http://russellwritescode.com/simplelookups-api/configuration-files/). 

    
    SimpleLookups.Initialize("Data Source=SERVER;Initial Catalog=DATABASE;User ID=USERNAME;Password=PASSWORD");



2. Create a mostly blank class object for the intended lookup type. This should inherit from the SimpleLookups.Lookup type.

    
    public class EmployeeType : SimpleLookups.Lookup { }



3. Instantiate a LookupManager for this type to perform CRUD operations.

    
    var employeeTypeManager = new SimpleLookups.LookupManager<employeetype>();



4. Use SimpleLookups when you need a lookup value. In this one, I'm looking for an EmployeeType with Id = 3.

    
    var empType3 = employeeTypeManager.Get(3);


Maybe I'm looking for all the active EmployeeTypes?

    
    var actives = employeeTypeManager.Get(true);


Or maybe an EmployeeType with a specific code?

    
    var salaryEmpType = employeeTypeManager.Get("SALARY");



That's it! If you have any suggestions to improve how it works, please send an email to YouDidThatWrong (at) russellwritescode.com.

The download package also has a script to create lookup tables if you are at that stage in your project.

[Download](http://russellwritescode.com/things-i-work-on/)
[View Source Code (GitHub)](https://github.com/rwpcpe/simple-lookups/)
[View SimpleLookups API Documentation](http://russellwritescode.com/simplelookups-api/)
