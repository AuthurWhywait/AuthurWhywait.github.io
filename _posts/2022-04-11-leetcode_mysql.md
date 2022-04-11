---
layout: post
title: "MySQL: SELECT"
description: "notes of coding in Leetcode"
categories: [MySQL]
tags: [Leetcode, Notes]
redirect_from:
  - /2022/04/11/
---

- Content
{:toc}

## 写在前面：基础相关

### 语法要求

- SQL 语句可以单行或多行书写，以分号结尾；
- 可以用空格和缩进来来增强语句的可读性；
- 关键字不区别大小写，建议使用大写。

> 在Windows中，mysql是不区分大小写；Linux中区分大小写.

### MySQL 数据类型

- int：整型
- double：浮点型，例如 double(5,2)表示最多 5 位，其中必须有 2 位小数，即最大值为 999.99；
- decimal：泛型型，在表单线方面使用该类型，因为不会出现精度缺失问题；
- char：固定长度字符串类型；(当输入的字符不够长度时会补空格)
- varchar：固定长度字符串类型；
- text：字符串类型；
- blob：字节类型；
- date：日期类型，格式为：yyyy-MM-dd；
- time：时间类型，格式为：hh:mm:ss
- timestamp：时间戳类型

---

下面开始正经内容。

## WHERE: OR and UNION

`World`表：

    +-------------+---------+
    | Column Name | Type    |
    +-------------+---------+
    | name        | varchar |
    | continent   | varchar |
    | area        | int     |
    | population  | int     |
    | gdp         | int     |
    +-------------+---------+
    name 是这张表的主键。

### OR

```sql
SELECT name, population, area
FROM World
WHERE area >= 3000000
	OR population >= 25000000
```

### UNION

```sql
SELECT name, population, area
FROM World
WHERE area >= 3000000
UNION
SELECT name, population, area
FROM World
WHERE population >= 25000000
```

### OR vs UNION

对于单列来说，用or是没有任何问题的，但是or涉及到多个列的时候，每次select只能选取一个index，如果选择了area，population就需要进行table-scan，即全部扫描一遍，但是使用union就可以解决这个问题，分别使用area和population上面的index进行查询。 但是这里还会有一个问题就是，UNION会对结果进行排序去重，可能会降低一些表现（这有可能是方法一比方法二快的原因），所以最佳的选择应该是两种方法都进行尝试比较。

> see this in [stackoverflow](https://leetcode-cn.com/link/?target=https%3A%2F%2Fstackoverflow.com%2Fquestions%2F13750475%2Fsql-performance-union-vs-or%EF%BC%89)

### UNION and UNION ALL

在纵向拼接中，纵向拼接前后都是查询语句，将查询结果纵向拼接在一起（我们要保证上下两个表的列数一样，否则会报错），并且以上表的字段名称为查询结果的字段名称。

去重用union，不去重用union all。

## WHERE: AND

```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y'
	AND recyclable = 'Y'
```

在`mysql`中我们不使用`==`。

## 'not equal' and Null

MySQL 使用三值逻辑 —— `TRUE`, `FALSE` 和 `UNKNOWN`。任何与 `NULL` 值进行的比较都会与第三种值 `UNKNOWN` 做比较。这个“任何值”包括 `NULL` 本身！这就是为什么 `MySQL` 提供 `IS NULL` 和 `IS NOT NULL` 两种操作来对 `NULL` 特殊判断。

另外不等于2写为 `!= 2` 或者 `<> 2`。

```sql
SELECT name
FROM customer
WHERE referee_id <> 2
	OR referee_id IS NULL;

SELECT name
FROM customer
WHERE referee_id != 2
	OR referee_id IS NULL;
```

## SQL 多表查询

<div align=center><img src="https://cdn.jsdelivr.net/gh/AuthurWhywait/images/20220411153034.png" width=600px/></div>

### Example

某网站包含两个表，Customers 表和 Orders 表。编写一个 SQL 查询，找出所有从不订购任何东西的客户。

`Customers` 表：

    +----+-------+
    | Id | Name  |
    +----+-------+
    | 1  | Joe   |
    | 2  | Henry |
    | 3  | Sam   |
    | 4  | Max   |
    +----+-------+

`Orders` 表：

    +----+------------+
    | Id | CustomerId |
    +----+------------+
    | 1  | 3          |
    | 2  | 1          |
    +----+------------+

mysql代码

```sql
select name as Customers
from customers as a
left join Orders as b
on a.id = b.customerid
where b.id is null
```

可格式化为如下（给一个[格式化网站](https://tool.oschina.net/codeformat/sql)）：

```sql
SELECT name AS Customers
FROM customers a
	LEFT JOIN Orders b ON a.id = b.customerid
WHERE b.id IS NULL
```

返回的结果:

    +-----------+
    | Customers |
    +-----------+
    | Henry     |
    | Max       |
    +-----------+

## References

1. 史上最全SQL基础知识总结(理论+举例). (n.d.). CSDN. https://blog.csdn.net/PILIpilipala/article/details/113798383
2. 寻找用户推荐人. (n.d.). Leetcode. https://leetcode-cn.com/problems/find-customer-referee/solution/xun-zhao-yong-hu-tui-jian-ren-by-leetcode/
3. 图解SQL面试题：查找不在表里的数据. (n.d.). Leetcode. https://leetcode-cn.com/problems/customers-who-never-order/solution/tu-jie-sqlmian-shi-ti-cha-zhao-bu-zai-biao-li-de-s/
