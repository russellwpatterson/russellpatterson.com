---
author: "Russell Patterson"
date: 2014-02-20 03:19:47+00:00
draft: false
title: Configuration Files
type: page
url: /simplelookups-api/configuration-files/
---
One of the new features in SimpleLookups 1.5 and above is the ability to initialize your database connection strings in the web.config file. The schema file for the config file can be found here:

[v1.5.x](http://simplelookups.com/schemas/1.5/SimpleLookups.xsd)  
[v1.6.x](http://simplelookups.com/schemas/1.6/SimpleLookups.xsd)  
[v2.0.x](http://simplelookups.com/schemas/2.0/SimpleLookups.xsd)

To use this feature, follow these steps:

1. Add the following to the <configSections> element, inside of the main <configuration> element, making sure that the version number matches the version you have:
 

    
    <configSections>
      <section name="simpleLookups" type="SimpleLookups.Configuration.SimpleLookupsConfigurationSection, SimpleLookups, Culture=neutral, PublicKeyToken=8f18859ef6ffa5ed"/>
    </configSections>



2. Add any connection strings as you would normally. See [MSDN](http://msdn.microsoft.com/en-us/library/cc716756(v=vs.110).aspx) for more information about this.

3. Add the <simpleLookups> element inside of the main <configuration> element. Like so:
   

    
    <simpleLookups>
      <connectionStrings>
        <connectionString isDefault="true" connectionStringName="SimpleLookups" />
        <connectionString connectionStringName="Other"/>
      </connectionStrings>
    </simpleLookups>



The connectionStringName attribute is the name of a connection string that has been added. Note: If more than one connection string is defined, one of them must have isDefault="true". As of v1.6, you can also specify the column suffixes that are used, and whether or not the table name is prefixed to the columns in the table. Additionally, as of v2.0, you can set up caching by specifying those settings. The Cache Refresh Period is in seconds. Here's that in action:


    
    <simpleLookups idColumnSuffix="Id4" nameColumnSuffix="Name4" 
         descriptionColumnSuffix="Description4" codeColumnSuffix="Code4" activeColumnName="Active4" 
         prefixColumnsWithTableName="false" enableCaching="true" cacheRefreshPeriod="1800">
      <connectionStrings>
        <connectionString isDefault="true" connectionStringName="SimpleLookups" />
        <connectionString connectionStringName="Other"/>
      </connectionStrings>
    </simpleLookups>



That's all there is to it.
