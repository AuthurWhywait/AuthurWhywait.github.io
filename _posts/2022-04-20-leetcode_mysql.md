---
layout: post
title: "MySQL: 计算函数，控制流，过滤"
description: "notes of coding in Leetcode"
categories: [MySQL]
tags: [Leetcode, Notes]
redirect_from:
  - /2022/04/20/
---

- Content
{:toc}

## 某个区间的表示

一般在where中会使用到，`between ... and ...`。

```sql
select activity_date day, count(distinct user_id) active_users
from activity
where datediff('2019-07-27',activity_date) between 0 and 29
group by activity_date
```

## 关于 GROUP BY

group by 是分组，不仅仅只能依据一个标准分类，也可以依据多个标准分类。类似：

```sql
select
    date_id,
    make_name,
    count(distinct lead_id) unique_leads,
    count(distinct partner_id) unique_partners
from dailysales
group by date_id, make_name;
```

## 找到最大值

```sql
select customer_number
from orders
group by customer_number
order by count(order_number) desc
limit 1
```

## time_stamp

获得一个时间戳具体的年月日，例如：

```sql
where year(time_stamp)='2020'
```

另外`group by`要写在`where`的后面，比方说下面这种方式是正确的，但是如果互换三四两行就会报错。

```sql
select user_id, max(time_stamp) last_stamp
from logins
where year(time_stamp)='2020'
group by user_id
```

## select + sum + if/case

> 学会将各种函数灵活结合。

例题：

  Stocks 表:
  +---------------+-----------+---------------+--------+
  | stock_name    | operation | operation_day | price  |
  +---------------+-----------+---------------+--------+
  | Leetcode      | Buy       | 1             | 1000   |
  | Corona Masks  | Buy       | 2             | 10     |
  | Leetcode      | Sell      | 5             | 9000   |
  | Handbags      | Buy       | 17            | 30000  |
  | Corona Masks  | Sell      | 3             | 1010   |
  | Corona Masks  | Buy       | 4             | 1000   |
  | Corona Masks  | Sell      | 5             | 500    |
  | Corona Masks  | Buy       | 6             | 1000   |
  | Handbags      | Sell      | 29            | 7000   |
  | Corona Masks  | Sell      | 10            | 10000  |
  +---------------+-----------+---------------+--------+

  Result 表:
  +---------------+-------------------+
  | stock_name    | capital_gain_loss |
  +---------------+-------------------+
  | Corona Masks  | 9500              |
  | Leetcode      | 8000              |
  | Handbags      | -23000            |
  +---------------+-------------------+
  Leetcode 股票在第一天以1000美元的价格买入，在第五天以9000美元的价格卖出。资本收益=9000-1000=8000美元。
  Handbags 股票在第17天以30000美元的价格买入，在第29天以7000美元的价格卖出。资本损失=7000-30000=-23000美元。
  Corona Masks 股票在第1天以10美元的价格买入，在第3天以1010美元的价格卖出。在第4天以1000美元的价格再次购买，在第5天以500美元的价格出售。最后，它在第6天以1000美元的价格被买走，在第10天以10000美元的价格被卖掉。资本损益是每次（’Buy'->'Sell'）操作资本收益或损失的和=（1010-10）+（500-1000）+（10000-1000）=1000-500+9000=9500美元。

`if` 版本

```sql
select
    stock_name,
    sum(
        if (operation='Buy', -price, price)
    )
    capital_gain_loss
from stocks
group by stock_name
```

`case` 版本

```sql
select
    stock_name,
    sum(
        case 
            when operation="Buy" 
            then -price else price 
            end
        )
    capital_gain_loss
from stocks
group by stock_name
```

## ORDER BY

我们已经知道按关键字升序和降序的方法：

- `order by ... asc`
- `order by ... desc`

那如果我们要按照两个关键字进行排序呢？比如，我们需要返回的结果表单，以 `travelled_distance` 降序排列 ，如果有两个或者更多的用户旅行了相同的距离, 那么再以 `name` 升序排列 。

实现方法：

```sql
order by
    travelled_distance desc,
    name asc
```

## HAVING

The `HAVING` clause was added to SQL because the `WHERE` keyword cannot be used with aggregate functions.

```sql
select
    sales.product_id,
    product.product_name
from sales
    left join product 
    on sales.product_id=product.product_id
group by sales.product_id
having min(sale_date) >= '2019-01-01'
    and max(sale_date) <= '2019-03-31'
```
