---
layout: post
title: "MySQL: 组合查询，指定选取"
description: "notes of coding in Leetcode"
categories: [MySQL]
tags: [Leetcode, Notes]
redirect_from:
  - /2022/04/13/
---

- Content
{:toc}

## HAVING

The `HAVING` clause was added to SQL because the `WHERE` keyword cannot be used with aggregate functions.

> The following SQL statement lists the number of customers in each country, sorted high to low (Only include countries with more than 5 customers):

```sql
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5
ORDER BY COUNT(CustomerID) DESC;
```

## 重构

在重构table的时候（行转列、列转行）常用：

- UNION ALL

`UNION ALL` 可以将许多table纵向拼接

## IS NOT NULL

使用在判断的地方，例如 `WHERE price IS NOT NULL`，可以作为一个判断是否为空的语句。

## LIMIT and OFFSET

The `LIMIT` clause is used to specify the number of records to return.

The `LIMIT` clause is useful on large tables with thousands of records. Returning a large number of records can impact performance.

The following SQL statement selects the first three records from the "Customers" table:

```sql
SELECT * FROM Customers
LIMIT 3;
```

You can also specify an OFFSET from where to start returning data.

```sql
SELECT * FROM artists LIMIT 5 OFFSET [Number of rows to skip];
```

For example, if you want to get 5 artists, but not the first five. You want to get rows 3 through 8. You’ll want to add an OFFSET of 2 to skip the first two rows:

```sql
SELECT * FROM artists LIMIT 5 OFFSET 2;
```

## About NULL

`SELECT NULL` will return `NULL`.
