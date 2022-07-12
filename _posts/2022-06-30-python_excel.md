---
layout: post
title: "Python 对 Excel 文件的读写"
description: "python 对 Excel 的操作总结"
categories: [Python]
tags: [Excel, Code]
redirect_from:
  - /2022/06/30/
---

> 最近使用 Python 处理 Excel 文件, 故而此处记录一下主要的操作.

## 包的引入

```python
import xlrd 文件读取
import xlwt 文件写入
```

## Read

```python
workbook = xlrd.open_workbook(file_path)
# 读取所有sheet的名称;
# 同时, 我们可以通过len()确定sheet个数, 判断是不是有sheet确实的问题.
sheet_names = workbook.sheets()
len(sheet_names)
# 通过sheet的名字或者索引找到sheet
sheet = workbook.sheet_by_name()
sheet = workbook.shhet_by_index()
# 返回工作簿对象的行列数信息, 循环的时候可以作为边界
nr = sheet.nrows
nc = sheet.ncols
# 读取元素信息
sheet.cell_value(i, j)
# 按照索引读取某一行或者某一列
sheet.rwo_values(index)
sheet.col_values(index)
```

空单元格的值为空字符 `''`

```python
sheet.cell_value(index_row, index_col) = ''
```

对于合并单元格的值的处理:

- 对于一个合并单元格, 其值能被索引到的是在最左上角的单元格, 其他索引下的值为空字符串;
- 利用此规律, 可以通过行以及列方向上的小循环找到非空字符串即为该合并单元格中存储的值.

下面是一个列合并单元格的取值处理源代码, 实际情况中, 需要具体情况具体处理:

```python
r = row
while r > -1 and table0.cell_value(r, 0) == '':
    r -= 1
row1 = int(table0.cell_value(r, 0))
```

## Write

```python
workbook = xlwt.Workbook(encoding='utf-8')
sheet = workbook.add_sheet('sheet name')

# 行序号和列序号从 0 开始 
sheet.write(i, j, str)
...

# 保存表格至路径 path
workbook.save('path')
```
