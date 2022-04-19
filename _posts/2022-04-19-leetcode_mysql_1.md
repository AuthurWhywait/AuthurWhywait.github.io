---
layout: post
title: "MySQL: 合并"
description: "notes of coding in Leetcode"
categories: [MySQL]
tags: [Leetcode, Notes]
redirect_from:
  - /2022/04/19/
---

- Content
{:toc}

## JOIN

- inner join：2表值都存在
- outer join：附表中值可能存在null的情况。

> outer join 包括 left join , right join 和full join ,看情况来选择需要的外连接

1. A inner join B：取交集
2. A left join B：取A全部，B没有对应的值，则为null
3. A right join B：取B全部，A没有对应的值，则为null
4. A full outer join B：取并集，彼此没有对应的值为null

上述4种的对应条件，在on后填写。

## ORDER BY

- 升序：order by ...
- 降序：order by ... desc

## 日期比较

- datediff(日期1, 日期2)：得到的结果是日期1与日期2相差的天数。如果日期1比日期2大，结果为正；如果日期1比日期2小，结果为负。
- timestampdiff(时间类型, 日期1, 日期2)：这个函数和上面diffdate的正、负号规则刚好相反。日期1大于日期2，结果为负，日期1小于日期2，结果为正。

<div align=center><a href="https://leetcode-cn.com/problems/rising-temperature/solution/tu-jie-sqlmian-shi-ti-ru-he-bi-jiao-ri-qi-shu-ju-b/"><img src="https://pic.leetcode-cn.com/006f72189f8a62549e64a2236cc9dc03d484e914e49dfa4d7a061f0e758983e4-1.png" width=600px/></a></div>

## ON vs WHERE

两者放置相同条件，之所以可能会导致结果集不同，就是因为优先级。on的优先级是高于where的。

LEFT JOIN 关键字会从左表 (table_name1) 那里返回所有的行，即使在右表 (table_name2) 中没有匹配的行。
数据库在通过连接两张或多张表来返回记录时，都会生成一张中间的临时表，然后再将这张临时表返回给用户。

在left join下，两者的区别：

on是在生成临时表的时候使用的条件，不管on的条件是否起到作用，都会返回左表 (table_name1) 的行。
where则是在生成临时表之后使用的条件，此时已经不管是否使用了left join了，只要条件不为真的行，全部过滤掉。

## References

- https://blog.csdn.net/cs958903980/article/details/60139792
