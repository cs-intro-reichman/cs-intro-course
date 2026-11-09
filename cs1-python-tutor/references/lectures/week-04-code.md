# Week 4 code files

The code files shown in the week 4 lectures.

### `arguments.py`
```python
# lecture 4-1 — arguments.py
# (this slide and its file came from lecture 3-1, where they are skipped)
s = "Hello"
s.count("l")          # 2
s.replace("l", "L")   # 'HeLLo'

# Prints nothing: both lines are values the REPL would show. .count
# answers 2 and .replace answers 'HeLLo' — and s itself is unchanged.
```

### `caesar.py`
```python
# lecture 4-1 — caesar.py
# The same design, with the bodies filled in. Each numbered step of the
# algorithm is one line, and the three steps inside `Shift letter` are the
# three lines of shift_letter.
def shift_letter(ch, shift):
    """Return ch shifted inside a..z."""
    position = ord(ch) - ord("a")       # 2.1.1  a..z  ->  0..25
    position = (position + shift) % 26  # 2.1.2  the shift, with the wrap
    return chr(position + ord("a"))     # 2.1.3  back to a letter


def encrypt(text, shift=3):
    """Return text with its lowercase letters shifted."""
    result = ""                         # 1
    for ch in text:                     # 2
        if ch.islower():                # 2.1
            ch = shift_letter(ch, shift)
        result = result + ch            # 2.2
    return result


def decrypt(text, shift=3):
    """Return the message that encrypt(text, shift) came from."""
    return encrypt(text, -shift)


text = input("Message: ")
shift = int(input("Shift: "))
print(encrypt(text, shift))

# Message: hello, world
# Shift: 3
# khoor, zruog
#
# The lowercase test lives in the loop, not in shift_letter, so the function
# does only what its name says. The price is that it assumes a lowercase
# letter: shift_letter(",", 3) answers "c", which is nonsense. Deciding what
# counts as a letter is the caller's job.
#
# decrypt is one line because encrypt already exists: -3 % 26 is 23, so the
# same modulo that wraps z to c wraps a back to x.
```

### `caesar_check.py`
```python
# lecture 4-1 — caesar_check.py
# The same functions, with the asserts that check them one at a time.
def shift_letter(ch, shift):
    """Return ch shifted inside a..z."""
    position = ord(ch) - ord("a")
    position = (position + shift) % 26
    return chr(position + ord("a"))


def encrypt(text, shift=3):
    """Return text with its lowercase letters shifted."""
    result = ""
    for ch in text:
        if ch.islower():
            ch = shift_letter(ch, shift)
        result = result + ch
    return result


def decrypt(text, shift=3):
    """Return the message that encrypt(text, shift) came from."""
    return encrypt(text, -shift)


# shift_letter(ch, shift) -> one letter. It assumes it is given one.
assert shift_letter("a", 3) == "d"
assert shift_letter("z", 3) == "c", "the wrap: 25 + 3 is 2, not 28"

# encrypt(text, shift) -> a string. Here is where a non-letter is decided.
assert encrypt("hello, world", 3) == "khoor, zruog"   # the comma and the space
assert encrypt("xyz", 3) == "abc"
assert encrypt("abc") == "def"                        # the default shift

# decrypt undoes it, whatever the shift
assert decrypt("khoor, zruog", 3) == "hello, world"
assert decrypt(encrypt("hello", 7), 7) == "hello"

print("all checks passed")

# The last one is the strongest check on the pair, and it could not be written
# at all on the flat program of lecture 3-1: it tests a property of two
# functions together, not one value.
```

### `caesar_design.py`
```python
# lecture 4-1 — caesar_design.py
# The design first: names, parameters, promises. The bodies are stubs, so the
# program already runs and main can be checked before anything is encrypted.
def shift_letter(ch, shift):
    """Return ch shifted inside a..z."""
    return ch


def encrypt(text, shift=3):
    """Return text with its lowercase letters shifted."""
    return text


text = input("Message: ")
shift = int(input("Shift: "))
print(encrypt(text, shift))

# Message: hello, world
# Shift: 3
# hello, world
#
# The message comes back unchanged, which is what a stub should do. The run
# already proves the prompts, the int() on the shift and the call are right.
```

### `errors.py`
```python
# lecture 4-1 — errors.py
# (this slide and its file came from lecture 3-1, where they are skipped)
x = 5
x.upper()     # AttributeError
upper("hi")   # NameError

# ON PURPOSE BROKEN — this is the error demo of the slide.
# x.upper() on an int raises AttributeError, and upper("hi") raises
# NameError: there is no plain function by that name. Run the lines one at
# a time; the file stops at the first of them.
```

### `function_object.py`
```python
# lecture 4-1, slide 15 — a function is a value, like any other
# my_sqrt is the deck's own function, exactly as slide 5 wrote it.

def my_sqrt(x):
    epsilon = 0.01
    g = x / 2
    while abs(g * g - x) > epsilon:
        g = g - (g * g - x) / (2 * g)
    return g


print(my_sqrt)         # <function my_sqrt at 0x...>  — the address changes
                       # every run; what matters is that it IS something

f = my_sqrt            # no parentheses: the function itself, not its answer
print(f(16))           # 4.001219512195122
print(f is my_sqrt)    # True — one object, two names

# The one character that matters:
#   f = my_sqrt       takes the function
#   f = my_sqrt(16)   takes the answer
#
# And note 4.001219512195122, not 4: this is still the my_sqrt of slide 5,
# with epsilon hard-coded at 0.01 — the approximation of lecture 3-2 is still
# an approximation. The default-parameter slide is what lets the caller
# tighten it.
```

### `hypot.py`
```python
# lecture 4-1 — hypot.py
# A function calling a function: hypot uses my_sqrt, and while my_sqrt runs
# the call to hypot is still waiting. This is the program of the call-stack
# slide.

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

### `keyword_args.py`
```python
# lecture 4-1 — keyword_args.py
# The same call, four ways. Named arguments may arrive in any order, and all
# four lines print the same number.

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

### `main.py`
```python
# lecture 4-1 — main.py
# The user side: what is needed. One file asks, the other answers.
# Run this one; mymath.py must sit beside it.

# Using the library from another file
import mymath

print(mymath.my_sqrt(2))
print(mymath.hypot(2, 1, 5, 4))

# And this is the docstring the help() slide reads:
#   help(mymath.my_sqrt)
```

### `my_sqrt.py`
```python
# lecture 4-1 — my_sqrt.py
# The same loop, named once and reused.

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
# lecture 4-1 — my_sqrt_default.py
# epsilon becomes a parameter with a default: one function, called in more
# than one way. Note the second line: a loose epsilon gives a loose answer.

def my_sqrt(x, epsilon=0.001):
    g = x / 2
    while abs(g * g - x) > epsilon:
        g = g - (g * g - x) / (2 * g)
    return g


print(my_sqrt(2))         # 1.4142156862745099  — the default steps in
print(my_sqrt(2, 0.5))    # 1.5                 — a loose epsilon
print(my_sqrt(2, 1e-9))   # 1.4142135623746899  — the caller decides
```

### `mymath.py`
```python
"""A small library of math functions."""
# lecture 4-1 — mymath.py
# The library side: how it is done. Nothing here prints; it is imported.


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

### `primes.py`
```python
# lecture 4-1 — primes.py
# The same design, with the body filled in. Type 20 when it asks.

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

### `primes_check.py`
```python
# Checking two functions with assert
# A test is one line: write down what you already know, and let Python check it.


def is_prime(k):
    """Return True if k is a prime number."""
    for d in range(2, k):
        if k % d == 0:
            return False
    return True


def count_primes(n):
    """Return how many prime numbers there are from 2 to n."""
    count = 0
    for k in range(2, n + 1):
        if is_prime(k):
            count = count + 1
    return count


# is_prime(k) -> True or False
assert is_prime(7)
assert is_prime(2), "2 is prime"   # easy to get wrong
assert not is_prime(9)

# count_primes(n) -> a number
assert count_primes(10) == 4       # 2 3 5 7
assert count_primes(1) == 0        # none at all
print("all checks passed")
```

### `primes_design.py`
```python
# lecture 4-1 — primes_design.py
# main is written, is_prime is a stub. Type 20 when it asks: it prints no
# primes at all, which is exactly what a stub that always answers False does.

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

### `stubs.py`
```python
# lecture 4-1 — stubs.py
# Sketch first: real names and parameters, placeholder bodies. The program
# already runs, so the pieces can be checked against each other before any
# of them is written.

def hypot(x1, y1, x2, y2):
    return 0.0


def my_sqrt(x, epsilon=0.001):
    return 0.0


print(hypot(2, 1, 5, 4))   # 0.0 — the shape is right, the answer is not yet
```

### `triangle.py`
```python
# lecture 4-1 — triangle.py
# The same design, with the bodies filled in. Nothing above the bodies
# changed. mymath.py must sit beside this file.

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
# lecture 4-1 — triangle_design.py
# The design first: names, parameters, promises. Both bodies are stubs, so
# the numbers are wrong on purpose — what is being checked is the fit.
# mymath.py must sit beside this file.

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

### `two_roots_bad.py`
```python
# lecture 4-1 — two_roots_bad.py
# The same loop, written twice. This is the slide that motivates functions:
# nothing here is wrong, it is just copied.

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

### `type_hints.py`
```python
# lecture 4-1 — type_hints.py
# Type hints say what goes in and what comes out. Python does not enforce
# them: the program runs exactly the same without them.

def my_sqrt(x: float, epsilon: float = 0.001) -> float:
    g = x / 2
    while abs(g * g - x) > epsilon:
        g = g - (g * g - x) / (2 * g)
    return g


print(my_sqrt(2))
print(my_sqrt(2, 1e-9))
```
