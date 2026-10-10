# Week 3 code files

The code files shown in the week 3 lectures.

### `sqrt_bisection.py`
```python
# Square root of x by bisection (x >= 1)
x = 16
epsilon = 0.01
low = 1.0
high = x
g = (low + high) / 2
steps = 0
while abs(g * g - x) >= epsilon:
    if g * g < x:
        low = g
    else:
        high = g
    g = (low + high) / 2
    steps = steps + 1
print(f"{round(g, 4)} in {steps} steps")
```

### `sqrt_newton.py`
```python
# Square root of x by Newton-Raphson
x = 16
epsilon = 0.01
g = x / 2
steps = 0
while abs(g * g - x) > epsilon:
    g = g - (g * g - x) / (2 * g)
    steps = steps + 1
    print(f"step {steps}: {g}")
print(f"{round(g, 4)} in {steps} steps")
```

### `sqrt_sequential.py`
```python
# Square root of x by sequential search
x = 16
epsilon = 0.01
increment = 0.0001
g = 1.0
steps = 0
while abs(g * g - x) >= epsilon:
    g = g + increment
    steps = steps + 1
print(f"{round(g, 4)} in {steps} steps")
```

### `sqrt_sequential_fixed.py`
```python
# Square root of x by sequential search
x = 16
epsilon = 0.01
increment = 0.0001
g = 1.0
steps = 0
while abs(g * g - x) >= epsilon and g <= x:
    g = g + increment
    steps = steps + 1
if g > x:
    print("Use a smaller increment")
else:
    print(f"{round(g, 4)} in {steps} steps")
```

### `two_roots_bad.py`
```python
# Two square roots: the same loop, twice
epsilon = 0.01
a = 16
g = a / 2
while abs(g * g - a) > epsilon:
    g = g - (g * g - a) / (2 * g)
print(f"root of {a} is about {round(g, 4)}")
b = 105
g = b / 2
while abs(g * g - b) > epsilon:
    g = g - (g * g - b) / (2 * g)
print(f"root of {b} is about {round(g, 4)}")
```
