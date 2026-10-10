# Week 4 code files

The code files shown in the week 4 lectures.

### `hypot.py`
```python
# Distance between two points, using my_sqrt
def my_sqrt(x):
    epsilon = 0.01
    g = x / 2
    while abs(g * g - x) > epsilon:
        g = g - (g * g - x) / (2 * g)
    return g

def hypot(x1, y1, x2, y2):
    dx = x2 - x1
    dy = y2 - y1
    return my_sqrt(dx * dx + dy * dy)

print(round(hypot(2, 1, 5, 4), 4))
```

### `keyword_args.py`
```python
# Naming the arguments at the call site
def my_sqrt(x, epsilon=0.001):
    g = x / 2
    while abs(g * g - x) > epsilon:
        g = g - (g * g - x) / (2 * g)
    return g

print(my_sqrt(2, 1e-9))
print(my_sqrt(x=2, epsilon=1e-9))
print(my_sqrt(epsilon=1e-9, x=2))
```

### `main.py`
```python
# Using the library from another file
import mymath

print(mymath.my_sqrt(2))
print(mymath.hypot(2, 1, 5, 4))
```

### `my_sqrt.py`
```python
# The same loop, named once and reused
def my_sqrt(x):
    epsilon = 0.01
    g = x / 2
    while abs(g * g - x) > epsilon:
        g = g - (g * g - x) / (2 * g)
    return g

print("root of 16:", round(my_sqrt(16), 4))
print("root of 105:", round(my_sqrt(105), 4))
```

### `my_sqrt_default.py`
```python
# epsilon becomes a parameter, with a default
def my_sqrt(x, epsilon=0.001):
    g = x / 2
    while abs(g * g - x) > epsilon:
        g = g - (g * g - x) / (2 * g)
    return g

print(my_sqrt(2))
print(my_sqrt(2, 0.5))
print(my_sqrt(2, 1e-9))
```

### `mymath.py`
```python
"""A small library of math functions."""

def my_sqrt(x, epsilon=0.001):
    """Return a number whose square is near x."""
    g = x / 2
    while abs(g * g - x) > epsilon:
        g = g - (g * g - x) / (2 * g)
    return g

def hypot(x1, y1, x2, y2):
    """Return the distance between two points."""
    return my_sqrt((x2 - x1) ** 2 + (y2 - y1) ** 2)
```

### `stubs.py`
```python
# Sketch first: the real bodies come later
def hypot(x1, y1, x2, y2):
    return 0.0

def my_sqrt(x, epsilon=0.001):
    return 0.0

print(hypot(2, 1, 5, 4))
```

### `triangle.py`
```python
# The same design, with the bodies filled in
import mymath

def perimeter(a, b, c):
    """Return the sum of the three sides."""
    return a + b + c

def is_right(a, b, c):
    """Return True if a*a + b*b is close to c*c."""
    return abs(a * a + b * b - c * c) < 0.01

a = mymath.hypot(0, 0, 3, 0)
b = mymath.hypot(0, 0, 0, 4)
c = mymath.hypot(3, 0, 0, 4)
print("perimeter:", round(perimeter(a, b, c), 4))
print("right angle:", is_right(a, b, c))
```

### `triangle_design.py`
```python
# The design first: names, parameters, promises
import mymath

def perimeter(a, b, c):
    """Return the sum of the three sides."""
    return 0.0

def is_right(a, b, c):
    """Return True if a*a + b*b is close to c*c."""
    return False

a = mymath.hypot(0, 0, 3, 0)
b = mymath.hypot(0, 0, 0, 4)
c = mymath.hypot(3, 0, 0, 4)
print("perimeter:", round(perimeter(a, b, c), 4))
print("right angle:", is_right(a, b, c))
```

### `type_hints.py`
```python
# Type hints: what goes in, what comes out
def my_sqrt(x: float, epsilon: float = 0.001) -> float:
    g = x / 2
    while abs(g * g - x) > epsilon:
        g = g - (g * g - x) / (2 * g)
    return g

print(my_sqrt(2))
print(my_sqrt(2, 1e-9))
```
