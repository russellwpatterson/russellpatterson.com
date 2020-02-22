---
author: "Russell Patterson"
date: 2013-12-21 23:32:07+00:00
draft: false
title: SimpleLookups Class
type: page
url: /simplelookups-api/simplelookups/
---

This is the main class of the SimpleLookups package.

**static void Initialize(string defaultConnectionString);** (v1.0+)  
Initializes SimpleLookups with the default connection string.

**static void Initialize(string defaultConnectionString, bool enableCaching, int cacheRefreshPeriod);** (v2.0+)  
Initializes SimpleLookups with the default connection string, and the provided cache settings.

**static void Initialize(string defaultConnectionString, string idColumnPrefix, string nameColumnPrefix, string descriptionColumnPrefix, string codeColumnPrefix, string activeColumnName, bool prefixColumnNamesWithTableName);** (v1.6+)  
Initializes SimpleLookups with the default connection string, and the provided column prefixes.

**static void Initialize(string defaultConnectionString, string idColumnPrefix, string nameColumnPrefix, string descriptionColumnPrefix, string codeColumnPrefix, string activeColumnName, bool prefixColumnNamesWithTableName, bool enableCaching, int cacheRefreshPeriod);** (v2.0+)  
Initializes SimpleLookups with the default connection string, the provided column prefixes, and the provided cache settings.

**static void AddConnectionString(string connectionName, string connectionString);** (v1.0+)  
Adds another connection string that can be used by the CRUD operations. You can reference the connection string by the connectionName you've provided here, in the operations on LookupManager.

