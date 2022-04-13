---
layout: post
title: "MySQL: 排序, 修改"
description: "notes of coding in Leetcode"
categories: [MySQL]
tags: [Leetcode, Notes]
redirect_from:
  - /2022/04/12/
---

- Content
{:toc}

## IF

If we only have two choices:

`if (condition, choice 1, choice 2)`

i.e.

```sql
select employee_id, 
    if (employee_id % 2 = 1 and left(name, 1) != 'M', salary, 0) bonus
from Employees
```

## CASE ... END

If choices are more then two, CASE is good choice., shown below.

```sql
case
    when condition_1 then choice_1
    when condition_2 then choice_2
    ...
    else 0
end as bonus
```

i.e.

```sql
select employee_id,
    case
        when employee_id % 2 = 1 and left(name, 1) <> 'M' then salary
        else 0
    end as bonus
from Employees
```

## UPDATE

```sql
update table_name
set
    ... (use IF or CASE)
```

i.e.

Table: `Salary`

    +-------------+----------+
    | Column Name | Type     |
    +-------------+----------+
    | id          | int      |
    | name        | varchar  |
    | sex         | ENUM     |
    | salary      | int      |
    +-------------+----------+
    id is the primary key for this table.
    The sex column is ENUM value of type ('m', 'f').
    The table contains information about an employee.

- Write an SQL query to swap all 'f' and 'm' values (i.e., change all 'f' values to 'm' and vice versa) with a single update statement and no intermediate temporary tables.
- Note that you must write a single update statement, do not write any select statement for this problem.

(use IF)

```sql
update salary
set
    sex = if (sex='f', 'm', 'f')
```

(or use CASE)

```sql
UPDATE salary
SET
    sex = CASE sex
        WHEN 'm' THEN 'f'
        ELSE 'm'
    END
```

## DELETE

We can first `select` what we want, and then change the `select` to `delete`.

```sql
delete p1.*
from Person p1, Person p2
where p1.Email=p2.Email and p1.id > p2.id
```
