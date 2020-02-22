---
author: "Russell Patterson"
date: 2013-12-21 23:34:16+00:00
draft: false
title: LookupManager Class
type: page
url: /simplelookups-api/lookupmanager/
---

For all of these methods, **T** must implement SimpleLookups.Interfaces.ILookup. To implement this interface, you can either implement it directly, or derive an empty implementation from the SimpleLookups.Lookup class.

**bool Create(T lookup);** (v1.0+)  
**bool Create(T lookup, string connectionName);** (v1.0+)  
Creates an entry in the lookup table of that specific type. If the record is not created, but there is no error, the method returns false. If an error occurs, this method will throw a SimpleLookupsException. Check InnerException for details on the error.

**T Get(int id);** (v1.1+)  
**T Get(int id, string connectionName);** (v1.1+)  
Retrieves the matching entry for the provided id. If no record is found, returns null. If an error occurs, this method will throw a SimpleLookupsException. Check InnerException for details on the error.

**T Get(IList<int> ids);** (v1.1+)  
**T Get(IList<int> ids, string connectionName);** (v1.1+)  
Retrieves the matching entries for the provided ids. If no records are found, returns an empty list. If an error occurs, this method will throw a SimpleLookupsException. Check InnerException for details on the error.

**T Get(string code);** (v1.2+)  
**T Get(string code, string connectionName);** (v1.2+)  
Retrieves the matching entry for the provided code. If no record is found, returns null. If an error occurs, this method will throw a SimpleLookupsException. Check InnerException for details on the error.

**T Get(IList<string> codes);** (v1.2+)  
**T Get(IList<string> codes, string connectionName);** (v1.2+)  
Retrieves the matching entries for the provided codes. If no records are found, returns an empty list. If an error occurs, this method will throw a SimpleLookupsException. Check InnerException for details on the error.

**IList<T> Get(bool activeOnly);** (v1.2+)  
**IList<T> Get(bool activeOnly, string connectionName);** (v1.2+)  
Retrieves all of the lookups of the type if the activeOnly flag is false. Returns only active lookups if the activeOnly flag is true. If no records are found, returns an empty list. If an error occurs, this method will throw a SimpleLookupsException. Check InnerException for details on the error.

**bool Update(T lookup);** (v1.0+)  
**bool Update(T lookup, string connectionName);** (v1.0+)  
Updates an existing record by id. If the record isn't found, the method will return false. If an error occurs, this method will throw a SimpleLookupsException. Check InnerException for details on the error.

**bool Delete(int id);** (v1.0+)  
**bool Delete(int id, string connectionName);** (v1.0+)  
Removes an existing record by its id. If the record isn't found, the method will return false. If an error occurs, this method will throw a SimpleLookupsException. Check InnerException for details on the error.

**bool Delete(IList<int> ids);** (v1.1+)  
**bool Delete(IList<int> ids, string connectionName);** (v1.1+)  
Removes existing records by ids. If all of the records aren't found, the method will return false. If any are deleted, it will return true. If an error occurs, this method will throw a SimpleLookupsException. Check InnerException for details on the error.

**bool Delete(string code);** (v1.2+)  
**bool Delete(string code, string connectionName);** (v1.2+)  
Removes an existing record by its code. If the record isn't found, the method will return false. If an error occurs, this method will throw a SimpleLookupsException. Check InnerException for details on the error.

**bool Delete(IList<string> codes);** (v1.2+)  
**bool Delete(IList<string> codes, string connectionName);** (v1.2+)  
Removes existing records by codes. If all of the records aren't found, the method will return false. If any are deleted, it will return true. If an error occurs, this method will throw a SimpleLookupsException. Check InnerException for details on the error.



* * *



**_Removed Methods:_**

**T GetById(int id);** (v1.0; removed v1.1)  
**T GetById(int id, string connectionName);** (v1.0; removed v1.1)  
Retrieves the matching entry for the provided id. If no record is found, returns null. If an error occurs, this method will throw a SimpleLookupsException. Check InnerException for details on the error.

**IList<T> GetAll();** (v1.0-1.1, deprecated v1.2, removed v1.5)   
**IList<T> GetAll(string connectionName);** (v1.0-1.1, deprecated v1.2, removed v1.5)  
Retrieves all of the lookups of the type. If no records are found, returns an empty list. If an error occurs, this method will throw a SimpleLookupsException. Check InnerException for details on the error.

**IList<T> GetActive();** (v1.0-1.1, deprecated v1.2, removed v1.5)  
**IList<T> GetActive(string connectionName);** (v1.0-1.1, deprecated v1.2, removed v1.5)  
Retrieves all of the lookups of the type having their Active flag set to 1. If no records are found, returns an empty list. If an error occurs, this method will throw a SimpleLookupsException. Check InnerException for details on the error.
