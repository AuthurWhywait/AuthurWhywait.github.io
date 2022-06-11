---
layout: post
title: "命令行运行Python脚本时传入参数的几种方式"
description: "sys.argv, argparse"
categories: [Linux]
tags: [Command, Linux, Script, Python]
redirect_from:
  - /2022/06/11/
---

- Content
{:toc}

## sys.argv 模块

- 这是基于位置的参数传入。根据输入参数的位置，分配给对应的脚本文件。此时要特别注意参数顺序的一一对应。
- 所有的参数都会被默认为`str`类型，需要在函数内部进行解析和转换。(在下面的例子中是使用`float()`转换变量类型。)

此时我们有Python脚本`script.py`.

```python
import sys

def add(a, b):
    print(float(a)+float(b))

if __name__ == '__main__':
    arg1, arg2 = sys.argv[1], sys.argv[2]   # 接收位置参数
    add(arg1, arg2)
```

命令行执行代码如下：

```command
python script.py 3.0 4.0
```

## argparse 模块

- 利用`argparse`模块，在函数内定义好相关的命名参数（包括名称、数据类型、默认值、是否为必要输入参数等），从而在命令行中可以方便的调用。
- 其中`add_argument()`中设定的变量数据类型，理论上可以是任何合法的类型，但一般仅使用`bool, int, str, float`这些基本类型，更复杂的类型可以在这些基本类型的基础上进行解析，比如`str`。

使用此模块时，python脚本如下：

```python
import argparse

def add(a, b):
    print(float(a)+float(b))

parser = argparse.ArgumentParser(description='a demo of script')
parser.add_argument('--add-f', '-a', type=float, default=0.0)  # 添加变量
parser.add_argument('--bf', type=float, default=1.0)

if __name__ == '__main__':
    args = parser.parse_args()   # 解析所有的命令行传入变量
    add(args.add_f, args.bf)
```

具体的命令行运行python脚本如下(下面是几种写法)：

```command
python script.py --a-f=4.0 --bf=3.0
python script.py --a-f 4.0 --bf 3.0
python script.py --add 4 --b 4
python script.py --ad 4 --b 4
python script.py --a 4 --b 4
python script.py -a 4 --b 4
```

对于任意python脚本，我们可以通过下面两者之一获得帮助。

```command
python script.py -h
python script.py --help
```

`"a-b"`

来一个更加详细的代码展示（来自YOLOv5官方源代码）：

```python
def parse_opt():
    parser = argparse.ArgumentParser()
    parser.add_argument('--weights', nargs='+', type=str, default=ROOT / 'yolov5s.pt', help='model path(s)')
    parser.add_argument('--source', type=str, default=ROOT / 'data/images', help='file/dir/URL/glob, 0 for webcam')
    ...
    opt = parser.parse_args()
    opt.imgsz *= 2 if len(opt.imgsz) == 1 else 1  # expand
    print_args(vars(opt))
    return opt

def main(opt):
    check_requirements(exclude=('tensorboard', 'thop'))
    run(**vars(opt))

if __name__ == "__main__":
    opt = parse_opt()
    main(opt)
```
