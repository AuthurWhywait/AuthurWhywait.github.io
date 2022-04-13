---
layout: post
title: "MySQL: 字符串处理函数/正则"
description: "notes of coding in Leetcode"
categories: [MySQL]
tags: [Leetcode, Notes]
redirect_from:
  - /2022/04/13/
---

- Content
{:toc}

## 索引

在SQL中，索引从1开始。

> 关于这个点，看到了一个[比较有意思的解释](https://www.saoniuhuo.com/question/detail-1994448.html)：作为一个物种，我们从“1”开始数了几千年，然后把0加到数字的万神殿。 当从表中计算行数时，从1开始计算要直观得多：“1”对于第一行几乎不需要解释，特别是对于不是程序员的人第一行的“0”需要解释。 很容易忘记，但是sql是为非程序员设计的。很多冗长的内容是因为它是为业务用户设计的。

## MySQL中的字符串截取函数

> 原文链接

截取字段name左边的n个字符

```sql
left(name, n)
```

截取字段name右边边的n个字符

```sql
right(name, n)
```

### SUBSTRING

`substring(str, pos, len)`

> pos可为负，len不可为负

截取name这个字段，从第n个字符开始后面的所有字符

```sql
substring(name, n)
```

截取name这个字段，从第n个字符开始，只截取之后的m个字符

```sql
substring(name, n, m)
```

截取name这个字段，从倒数第n个字符之后的所有字符

```sql
substring(name, -n)
```

截取name这个字段，从倒数第n个字符开始，只截取之后m个字符

```sql
substring(name, -n, m)
```

### substring_index

截取第二个 '.' `之前`的所有字符

```sql
substring_index('www.baidu.com', '.', 2) 
```

    www.baidu

截取第二个 '.' （倒数）之后的所有字符

```sql
substring_index('www.baidu.com', '.', -2)
```

    baidu.com

### char_length

获得name字段的长度

```sql
char_length(name)
```

## 字符大小写改变

`upper()`, `lower()`

## ORDER BY

举例，根据 `user_id` 排序

```sql
order by user_id
```

根据字典序排列，升序

```SQL
ORDER BY PRODUCT ASC
```

## DISTINCT

The following SQL statement selects only the DISTINCT values from the "Country" column in the "Customers" table:

```SQL
SELECT DISTINCT Country FROM Customers;
```

## GROUP BY

The GROUP BY statement groups rows that have the same values into summary rows, like "find the number of customers in each country".

The GROUP BY statement is often used with aggregate functions (COUNT(), MAX(), MIN(), SUM(), AVG()) to group the result-set by one or more columns.

```SQL
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
ORDER BY column_name(s);
```

把每一个组中的str组合成一个str，并且用`,`隔开。

```SQL
GROUP_CONCAT(DISTINCT PRODUCT, ORDER BY PRODUCT ASC SEPARATOR ',')
```

## 正则

写一条 SQL 语句，查询患有 I 类糖尿病的患者 ID （patient_id）、患者姓名（patient_name）以及其患有的所有疾病代码（conditions）。I 类糖尿病的代码总是包含前缀 DIAB1 。

    输入：
    Patients表：
    +------------+--------------+--------------+
    | patient_id | patient_name | conditions   |
    +------------+--------------+--------------+
    | 1          | Daniel       | YFEV COUGH   |
    | 2          | Alice        |              |
    | 3          | Bob          | DIAB100 MYOP |
    | 4          | George       | ACNE DIAB100 |
    | 5          | Alain        | DIAB201      |
    +------------+--------------+--------------+
    输出：
    +------------+--------------+--------------+
    | patient_id | patient_name | conditions   |
    +------------+--------------+--------------+
    | 3          | Bob          | DIAB100 MYOP |
    | 4          | George       | ACNE DIAB100 | 
    +------------+--------------+--------------+
    解释：Bob 和 George 都患有代码以 DIAB1 开头的疾病。

```sql
# method 1
SELECT *
FROM PATIENTS
WHERE CONDITIONS LIKE 'DIAB1%'
    OR CONDITIONS LIKE '% DIAB1%'
# method 2
SELECT *
FROM PATIENTS
WHERE CONCAT(' ', CONDITIONS) LIKE '% DIAB1%'
# method 3
SELECT *
FROM patients
WHERE conditions RLIKE '^DIAB1|.*\\sDIAB1';
```

### LIKE vs RLIKE

- `A RLIKE B` ，表示B是否在A里面即可。而`A LIKE B`,则表示B是否是A.
- Rlike功能和like功能大致一样，like是后面只支持简单表达式匹配（_%）,而rlike则支持标准正则表达式语法。所以如果正则表达式使用熟练的话，建议使用rlike，功能更加强大。所有的like匹配都可以被替换成rlike。反之，则不行。但是注意：like是从头逐一字符匹配的，是全部匹配，但是rlike则不是,可以从任意部位匹配，而且不是全部匹配。

## References

1. https://www.saoniuhuo.com/question/detail-1994448.html
2. https://www.cnblogs.com/duanc/archive/2018/04/09/8760372.html
3. https://www.w3schools.com/sql/sql_distinct.asp
4. https://blog.csdn.net/qq_26442553/article/details/79452221
