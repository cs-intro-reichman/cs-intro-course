# Lecture 4-1: Functions (week 4)

## Slide 1: Functions
INTRO TO CS COURSE · WEEK 4 · LECTURE 1
Functions
Naming and reusing code

## Slide 2
1
Anatomy
what a function is made of
Lecture overview
2
Call and return
what happens while it runs
3
Defaults and keywords
calling it in more than one way
Why functions
Anatomy
Call and return
Defaults and keywords
Modules and API
Designing
A worked design

## Slide 3: The big picture
The big picture
Each layer uses the one below it.
any program you may want to write
functions
conditionals and loops
variables and expressions
values and types
Today: functions.

## Slide 4: The same loop, twice
The same loop, twice
`two_roots_bad.py`
```python
# Two square roots: the same loop, twice
epsilon = 0.01
a = 16
g = a / 2
while abs(g * g - a) > epsilon:
    g = g - (g * g - a) / (2 * g)
print(f"root of {a}: {round(g, 4)}")

b = 105
g = b / 2
while abs(g * g - b) > epsilon:
    g = g - (g * g - b) / (2 * g)
print(f"root of {b}: {round(g, 4)}")
```
Why functions
Anatomy
Call and return
Defaults and keywords
Modules and API
Designing
A worked design
```python
root of 16: 4.0012
root of 105: 10.247
```

## Slide 5: The same loop, named
The same loop, named
`my_sqrt.py`
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
```python
terminal
```
```python
root of 16: 4.0012
root of 105: 10.247
```
```python
Definition
```
```python
Call
```
```python
Why functions
Write once: the loop is in one place.
Fix once: a fix applies to every call.
Readable: my_sqrt(16) says what it does.
Reuse it: other programs can call it.
```

## Slide 6: Anatomy of a function
Anatomy of a function
`my_sqrt.py`
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
def
The keyword that starts a definition.
my_sqrt
The function's name.
(x)
The function’s parameter(s)
Why functions
Anatomy
Call and return
Defaults and keywords
Modules and API
Designing
A worked design

## Slide 7: Body and return value
Body and return value
`my_sqrt.py`
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
The body
The indented block. It runs only when called.
return g
Returns a value and ends the call.
```python
Local names
epsilon and g exist only during the call.
```

## Slide 8: What a function is
What is a function?
Takes: zero, one or more inputs, its arguments
Does: whatever its body says, when it is called
Returns: one value (None if there is no return). 
Hides: its local names and its code from the caller (“encapsulation”)
16
the argument
my_sqrt
epsilon · g
local names, only while it runs
4.0012
one value back
Takes, does, returns — and hides.

## Slide 9: A function calling a function
A function calling a function
`hypot.py`
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
    res = my_sqrt(dx * dx + dy * dy)
    return res

print(round(hypot(2, 1, 5, 4), 4))
```
```python
terminal
```
```python
4.2426
```

## Slide 10: Arguments and parameters
Arguments and parameters
Two words for the two sides of a call.
Parameters: the names in the def line
Arguments: the values at the call
Matching: each parameter gets its argument
In order: the i-th parameter binds to the i-th argument
Why functions
Anatomy
Call and return
Defaults and keywords
Modules and API
Designing
A worked design
```python
The call
hypot(2, 1, 5, 4)
```
2
1
5
4
x1
y1
x2
y2
```python
The definition
def hypot(x1, y1, x2, y2)
```
The i-th parameter binds to the i-th argument.
`hypot.py`
```python
def hypot(x1, y1, x2, y2):      # the parameters
    dx = x2 - x1
    dy = y2 - y1
    res = my_sqrt(dx * dx + dy * dy)
    return res
d = hypot(2, 1, 5, 4)           # the arguments
```
Parameters
Arguments

## Slide 11: Calling a function
Calling a function
A call pauses the caller and runs the function.
main
prints the distance
hypot(2, 1, 5, 4)
computes dx, dy
calls
my_sqrt(18)
runs the loop
calls
Only one function runs at a time. The other two wait.

## Slide 12: Returning from a call
Returning from a call
return sends a value back, and the caller continues.
main
prints the distance
hypot(2, 1, 5, 4)
computes dx, dy
my_sqrt(18)
runs the loop
returns
returns
The returned value replaces the call in the caller's code.

## Slide 13: The order of events
The order of events
Step 1: main starts running
Step 2: main calls hypot and suspends
Step 3: hypot calls my_sqrt and suspends
Step 4: my_sqrt returns; hypot resumes
Step 5: hypot returns; main prints and ends

## Slide 14: The run-time stack
The call stack
`hypot.py`
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
    res = my_sqrt(dx * dx + dy * dy)
    return res

print(round(hypot(2, 1, 5, 4), 4))
```
main
the program itself
hypot(2, 1, 5, 4)
x1  y1  x2  y2  ·  dx  ·  dy  ·  res
my_sqrt(18)
x  ·  epsilon  ·  g
the call stack  (grows upward)
The Call Stack (or Run-time Stack) is the memory mechanism that tracks active function calls. 
Each call gets its own isolated frame to store local variables and parameters. 
When a function returns, its frame is popped and execution resumes in the caller. 
How Python tracks active function calls and local variables

## Slide 15: Calling one function two ways
Calling one function two ways
The problem: sometimes we choose epsilon, usually we do not
Bad solution: two almost identical functions
Python's solution: a default value for epsilon
Why functions
Anatomy
Call and return
Defaults and keywords
Modules and API
Designing
A worked design

## Slide 16: Default parameter values
Default parameter values
`my_sqrt_default.py`
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
my_sqrt(2)
epsilon = 0.001
The default steps in
my_sqrt(2, 1e-9)
epsilon = 1e-9
The caller decides
A default is a fallback, not a fixed value.
```python
terminal
```
```python
1.4142156862745099
1.5
1.4142135623746899
```

## Slide 17: Keyword arguments
Keyword arguments
```python
By position: my_sqrt(2, 1e-9), order decides
By name: my_sqrt(x=2, epsilon=1e-9), the call says
Any order: named arguments may come in any order
Mixed: my_sqrt(2, epsilon=1e-9), positional first, then named
Usual style: main inputs by position, optional ones by name
Why: the call is easier to read
```

## Slide 18: Calling by name
Calling by name
`keyword_args.py`
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
print(my_sqrt(2, epsilon=1e-9))
```
```python
by position: my_sqrt(2, 1e-9) 
```
2
1e-9
x
epsilon
```python
by name: my_sqrt(epsilon=1e-9, x=2) 
```
1e-9
2
x
epsilon
Named arguments may arrive in any order.
```python
terminal
```
```python
1.4142135623746899
1.4142135623746899
1.4142135623746899
1.4142135623746899
```

## Slide 19: Type hints
Type hints
`type_hints.py`
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
```python
Parameters
x: float says x is a float.
```
```python
Return value
-> float says it returns a float.
```
Not checked
Python does not enforce hints.
Optional
Later lectures leave them out.

## Slide 20: Lecture summary
Lecture summary
Anatomy: def, parameters, a body, and one value out
Call and return: a call pauses the caller, and each call keeps its own frame
Defaults and keywords: one function, called in more than one way
Why functions
Anatomy
Call and return
Defaults and keywords
Modules and API
Designing
A worked design

## Slide 21
Next: Functions, Part 2
Modules, API, and design
INTRO TO CS COURSE · WEEK 4 · LECTURE 2
