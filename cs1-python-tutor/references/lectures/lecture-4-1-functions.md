# Lecture 4-1: Functions (week 4)

## Slide 1: Functions
f
PYTHON COURSE · WEEK 4 · LECTURE 2
Functions
Naming and reusing code
Reichman University

## Slide 2: The big picture
The big picture
Each layer uses the one below it.
any program you may want to write
functions
conditionals and loops
variables and expressions
values and types
Today: functions.

## Slide 3: The same loop, twice
The same loop, twice
`two_roots_bad.py`
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
the file is in “week 4 code / two_roots_bad.py”.

## Slide 4: Why functions
Why functions
Write once: the loop is in one place
Fix once: a fix applies to every call
Readable: my_sqrt(16) says what it does
Reuse it: other programs can call it

## Slide 5: The same loop, named
The same loop, named
```python
python my_sqrt.py
root of 16: 4.0012
root of 105: 10.247
```
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
[LIVE] the file is in “week 4 code / my_sqrt.py”.

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
The parameters: the inputs.

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
Local names
epsilon and g exist only during the call.

## Slide 8: What a function is
What a function is
```python
Takes: zero, one or more inputs, its arguments
Does: whatever its body says, when it is called
Returns: one value (None if there is no return). return a, b packs two values into one tuple.
Hides: its local names and its code from the caller
```

## Slide 9: A function calling a function
A function calling a function
```python
python hypot.py
4.2426
```
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
    return my_sqrt(dx * dx + dy * dy)

print(round(hypot(2, 1, 5, 4), 4))
```
[LIVE] the file is in “week 4 code / hypot.py”.

## Slide 10: Arguments and parameters
Arguments and parameters
Two words for the two sides of a call.
Parameters: the names in the def line
Arguments: the values at the call
Matching: each parameter gets its argument
In order: first argument to first parameter

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

## Slide 14: Functions: the plan
Functions: the plan
Five parts.
Anatomy
Call and return
Defaults and keywords
Modules and API
Designing with functions

## Slide 15: Calling one function two ways
Calling one function two ways
The problem: sometimes we choose epsilon, usually we do not
Bad solution: two almost identical functions
Python's solution: a default value for epsilon

## Slide 16: Default parameter values
Default parameter values
```python
python my_sqrt_default.py
1.4142156862745099
1.5
1.4142135623746899
```
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
[LIVE] the file is in “week 4 code / my_sqrt_default.py”.

## Slide 17: Keyword arguments
Keyword arguments
By position: my_sqrt(2, 1e-9), order decides
By name: my_sqrt(x=2, epsilon=1e-9), the call says
Any order: named arguments may come in any order
Mixed: my_sqrt(2, epsilon=1e-9), positional first, then named
Usual style: main inputs by position, optional ones by name
Why: the call is easier to read

## Slide 18: Calling by name
Calling by name
```python
python keyword_args.py
1.4142135623746899
1.4142135623746899
1.4142135623746899
1.4142135623746899
```
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
[LIVE] the file is in “week 4 code / keyword_args.py”.

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
[LIVE] the file is in “week 4 code / type_hints.py”.
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

## Slide 20: Functions: the plan
Functions: the plan
Five parts.
Anatomy
Call and return
Defaults and keywords
Modules and API
Designing with functions

## Slide 21: Modularity
Modularity
Dividing a program into named pieces.
Less complexity: each piece can be understood on its own
Less duplication: fewer places for bugs
Testable: a function can be checked by itself
Shareable: two people can write two functions at once

## Slide 22: A library and its user
A library and its user
`mymath.py`
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
the library: how it is done.
`main.py`
```python
# Using the library from another file
import mymath

print(mymath.my_sqrt(2))
print(mymath.hypot(2, 1, 5, 4))
```
[LIVE] the user: what is needed.

## Slide 23: Calling syntax
Calling syntax
How you call a function depends on where it is.
Same file: my_sqrt(2), just the name
Another module: mymath.my_sqrt(2)

## Slide 24: The caller's view: a black box
The caller's view: a black box
An API describes what a function does for its caller.
What it is called: the name and its parameters
What it gives back: the value, and what it means
What it assumes: the inputs it will not accept
Not how: the caller does not need the body

## Slide 25: Documenting the API
Documenting the API
```python
help(mymath.my_sqrt)
my_sqrt(x, epsilon=0.001)
    Return a number whose
    square is near x.
```
`mymath.py`
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
the file is in “week 4 code / mymath.py”.

## Slide 26: Stubs first, bodies later
Stubs first, bodies later
```python
python stubs.py
0.0
```
`stubs.py`
```python
# Sketch first: the real bodies come later
def hypot(x1, y1, x2, y2):
    return 0.0

def my_sqrt(x, epsilon=0.001):
    return 0.0

print(hypot(2, 1, 5, 4))
```
the file is in “week 4 code / stubs.py”.
What is a stub?
A function with its real name and parameters, but a placeholder body (here, return 0.0).
The program already runs, so you can check how the pieces fit together, then write the real bodies one at a time.

## Slide 27: What makes a good function
What makes a good function
One job: if the name needs “and”, it is two functions
A good name: says what it returns or does, like perimeter, is_right, print_primes
Few parameters: many parameters suggest a bad design
A docstring: one sentence saying what it returns

## Slide 28: Functions: the plan
Functions: the plan
Five parts.
Anatomy
Call and return
Defaults and keywords
Modules and API
Designing with functions

## Slide 29: Top-down design
Top-down design
The task: in one sentence, what must the program do?
Split it: name the pieces the task needs
Repeat: split any piece that is still too big
Stop: when every piece is one small job

## Slide 30: A decomposition diagram
A decomposition diagram
A box is a function. An arrow means “calls”.
The task
Given the three corners of a triangle, print its perimeter and say whether it has a right angle.
main
the top-level code
hypot
in mymath
3 calls
perimeter
to write
is_right
to write
my_sqrt
in mymath

## Slide 31: Design before code
Design before code
Signatures: each function's name and parameters
Docstrings: in one sentence, what does it return?
Stubs: placeholder bodies, so the program runs
Bodies last: fill in and test one at a time

## Slide 32: The design, written down
The design, written down
```python
python triangle_design.py
perimeter: 0.0
right angle: False
```
`triangle_design.py`
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
[LIVE] the file is in “week 4 code / triangle_design.py”.

## Slide 33: Then fill in the bodies
Then fill in the bodies
```python
python triangle.py
perimeter: 12.0
right angle: True
```
`triangle.py`
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
[LIVE] the file is in “week 4 code / triangle.py”.

## Slide 34: Your turn: decompose
Your turn: decompose
Draw the diagram first. No code yet.
The task
Read a whole number n. Print every prime number from 2 to n, and then how many primes there were.
Your steps
1. Name the functions you need.
2. Give each a signature and a docstring.
3. Draw who calls whom.

## Slide 35: Solution: the pieces
Solution: the pieces
The task: read n, print the primes from 2 to n, then their count
main: reads n, tries every k from 2 to n, counts the primes
is_prime(k): one job, True if k is a prime number
Stop: is_prime needs no “and”, so it is small enough

## Slide 36: Solution: the diagram
Solution: the diagram
Two good designs. Every box has one job.
Design A
main
the top-level code
is_prime
to write
Design B
main
the top-level code
print_primes
to write
count_primes
to write
is_prime
to write

## Slide 37: Solution: the design, written down
Solution: the design, written down
```python
python primes_design.py
20

0 primes
```
`primes_design.py`
```python
# The design: main is written, is_prime is a stub
def is_prime(k):
    """Return True if k is a prime number."""
    return False

n = int(input())
count = 0
for k in range(2, n + 1):
    if is_prime(k):
        print(k, end=" ")
        count += 1
print()
print(f"{count} primes")
```
[LIVE] the file is in “week 4 code / primes_design.py”.

## Slide 38: Solution: fill in the body
Solution: fill in the body
```python
python primes.py
20
2 3 5 7 11 13 17 19 
8 primes
```
`primes.py`
```python
# The same design, with the body filled in
def is_prime(k):
    """Return True if k is a prime number."""
    for d in range(2, k):
        if k % d == 0:
            return False
    return True

n = int(input())
count = 0
for k in range(2, n + 1):
    if is_prime(k):
        print(k, end=" ")
        count += 1
print()
print(f"{count} primes")
```
[LIVE] the file is in “week 4 code / primes.py”.

## Slide 39: Design and AI tools
Design and AI tools
AI tools can now write a function body in seconds.
What they need: a clear name, parameters and docstring
Yours to decide: what the pieces are and how they fit
How you check: test each small function by itself
