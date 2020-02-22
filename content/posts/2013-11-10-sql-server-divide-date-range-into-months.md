---
author: "Russell Patterson"
date: 2013-11-10 21:31:21+00:00
draft: false
title: 'SQL Server: Divide Date Range into Months'

url: /2013/11/sql-server-divide-date-range-into-months/
categories:
- SQL Server
---

I wrote a script the other day that is utterly useless to me, but it might be helpful for someone else, so I thought I'd write a quick post about it.

Suppose you have some date range, let's say "1/20/2013 - 4/29/2014". Now, suppose you want this range to be broken up into one month sections, with a start and end date for each month. Suppose, for some reason, you want to use a recursive common table expression (CTE). You can just do this:


    
    DECLARE @BeginDate DATETIME = '2013-01-20'
    DECLARE @EndDate DATETIME = '2014-04-29'
    
    ;WITH Months (currentDate)
    AS ( SELECT @BeginDate
    UNION ALL
    SELECT DATEADD(MONTH, 1, currentDate)
    FROM Months
    WHERE DATEADD(MONTH, 1, currentDate) <= @EndDate
    )
    SELECT CASE WHEN currentDate < @BeginDate THEN @BeginDate ELSE currentDate END RangeStart, 
    CASE WHEN currentDate > DATEADD(MONTH, -1, @EndDate ) THEN @EndDate ELSE DATEADD(DAY, -1, DATEADD(MONTH, 1, currentDate)) END RangeEnd
    FROM Months


This would produce the following results:

[![months-cte-results](/media/months-cte-results-287x300.png)
](/media/months-cte-results.png)

I think that this is actually pretty cool, but I can't really come up with a reason to use something like this, outside of maybe a financial application. Anyway, I hope someone gets some use out of it.
