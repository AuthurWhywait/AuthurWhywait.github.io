---
layout: post
title: "Arithmetical Operations in Python"
description: "Code examples"
categories: [Python]
tags: [Code]
redirect_from:
  - /2022/04/03/
---

<head>
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$']]
            }
        });
    </script>
</head>

- Content
{:toc}

## Common Arithmetic Operators

```python
a, b = 7, 2
print("a + b = ", a + b)
print("a - b = ", a - b)
print("a * b = ", a * b)
print("a / b = ", a / b)
print("a // b = ", a // b)
print("a ** b = ", a ** b)
print("a % b = ", a % b)
```

    a + b =  9
    a - b =  5
    a * b =  14
    a / b =  3.5
    a // b =  3
    a ** b =  49
    a % b =  1

## Integration

### integrate.quad

> About [scipy.integrate.quad](https://docs.scipy.org/doc/scipy/reference/generated/scipy.integrate.quad.html)

```python
from scipy import integrate
def f(x, a, b):
    return a * x + b
v, err = integrate.quad(f, 1, 2, args = (-1, 1))
print(v)
```

    -0.5

For $\int_{-1}^1\frac{1}{\sqrt{\vert x\vert}}dx$, because $x\ne 0$, we need to add `points=[0]`, otherwise we will get an report like:

    inf
    /usr/local/lib/python3.7/dist-packages/ipykernel_launcher.py:4: RuntimeWarning: divide by zero encountered in double_scalars after removing the cwd from sys.path.

```python
from scipy import integrate
def f(x):
    return 1 / np.sqrt(abs(x))
v, err = integrate.quad(f, -1, 1, points=[0])
print(v)
```

    3.9999999999999813

## About sympy

SymPy is a Python library for symbolic mathematics. It aims to become a full-featured computer algebra system (CAS) while keeping the code as simple as possible in order to be comprehensible and easily extensible. SymPy is written entirely in Python.

```python
from sympy import *
x, y, z = symbols('x, y, z')
f = (2/3)*x**2 + (1/3)*x**2 + x + x + 1
g = (y+1)**3 + (z+2)**2 + 6*y + 2*(z-4)
```

### Simplification and Expansion

```python
print(f.simplify())
print(g.expand())
```

    1.0*x**2 + 2*x + 1
    y**3 + 3*y**2 + 9*y + z**2 + 6*z - 3

### Solve equations

```python
f1 = 2*x - y + z - 10
f2 = 3*x + 2*y - z - 16
f3 = x + 6*y - z - 28
print(solve([f1, f2, f3]))
```

    {x: 46/11, y: 56/11, z: 74/11}

### Limitation

```python
limit(function, independent variable, value)
```

```python
f = (x+1)**2 + y**(1/2) + 3
print(limit(f, x, z+1))
print(limit(f, y, z-1))
print(limit(f, x, 1))
```

Classical limit example: $\lim_{x\to 0}\frac{\sin x}{x}$

```python
f = sin(x)/x
print(limit(f, x, 0))
```

Negative direction approximation: `dir='-'`

```python
print(limit(f, x, 0, dir='-'))
```

Value can also be equal to $\infty$ using `oo`; while for $-\infty$ can be expressed by `-oo`.

### Differential

```python
f = 3 * x**2 + x
g = cos(x*y)
print(diff(f, x))
print(diff(f, x, 2))
print(diff(g, x, 2, y, 4))
```

    6*x + 1
    6
    x**2*(-x**2*y**2*cos(x*y) - 8*x*y*sin(x*y) + 12*cos(x*y))

### Integration

$$\int_{-\infty}^0e^x$$

```python
f = exp(x)
integrate(f, (x, -oo, 0))
```

$$\int (3x^2+1)dx$$

```python
f = 3*x**2 + 1
integrate(f, x)
```

$$\int_{-3}^{4}\int_0^1(x+2y)dxdy$$

```python
f = x + 2*y
integrate(f, (x,0,1), (y,-3,4))
```
