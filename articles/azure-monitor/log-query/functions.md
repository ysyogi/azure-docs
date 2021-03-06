---
title: Functions in Azure Monitor log queries | Microsoft Docs
description: This article describes how to use functions to call a query from another log query in Azure Monitor.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.assetid: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.topic: conceptual
ms.date: 11/15/2018
ms.author: bwren
---


# Using functions in Azure Monitor log queries

> [!NOTE]
> You should complete [Get started with the Analytics portal](get-started-portal.md) and [Getting started with queries](get-started-queries.md) before completing this lesson.

[!INCLUDE [log-analytics-demo-environment](../../../includes/log-analytics-demo-environment.md)]


To use a log query with another query you can save it as a function. This allows you to simplify complex queries by breaking them into parts and allows you to reuse common code with multiple queries.

## Create a function

Create a function in log analytics in the Azure portal by clicking **Save** and then providing the information in the following table.

| Setting | Description |
|:---|:---|
| Name           | Display name for the query in **Query explorer**. |
| Save as        | Function |
| Function Alias | Short name to use the function in other queries. May not contain spaces and must be unique. |
| Category       | A category to organize saved queries and functions in **Query explorer**. |

> [!NOTE]
> A function in Azure Monitor cannot contain another function.

> [!NOTE]
> Saving a function is possible in Azure Monitor log queries, but currently not for Application Insights queries.



## Use a function
Use a function by including its alias in another query. It can be used like any other table.

## Example
The following sample query returns all missing security updates reported in the last day. Save this query as a function with the alias _security_updates_last_day_. 

```Kusto
Update
| where TimeGenerated > ago(1d) 
| where Classification == "Security Updates" 
| where UpdateState == "Needed"
```

Create another query and reference the _security_updates_last_day_ function to search for SQL-related needed security updates.

```Kusto
security_updates_last_day | where Title contains "SQL"
```

## Next steps
See other lessons for writing Azure Monitor log queries:

- [String operations](string-operations.md)
- [Date and time operations](datetime-operations.md)
- [Aggregation functions](aggregations.md)
- [Advanced aggregations](advanced-aggregations.md)
- [JSON and data structures](json-data-structures.md)
- [Joins](joins.md)
- [Charts](charts.md)
