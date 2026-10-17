# Week 1 code files

The code files shown in the week 1 lectures.

### `age_check.py`
```python
# lecture 1-2 — age_check.py
city = input("City: ")
age  = int(input("Age: "))

print(city == "Tel Aviv")   # True — already a bool
too_young = age < 18        # the same value, with a name
if too_young:
    print("You are too young for this")
```

### `bad_input.py`
```python
# lecture 1-2 — bad_input.py
age = int(input("How old are you? "))
print(age + 1)

# $ python bad_input.py
# How old are you? hello
# Traceback (most recent call last):
#   File "bad_input.py", line 1, in <module>
#     age = int(input("How old are you? "))
#           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
# ValueError: invalid literal for int() with base 10: 'hello'
```

### `big_int.py`
```python
# lecture 1-2 — big_int.py
print(2 ** 100)
# 1267650600228229401496703205376
```

### `brackets.py`
```python
# lecture 1-2, slide 50 — Where the brackets go
print(11 * 0.3)
# 3.3
print(int(11 * 0.3))    # 3
print(int(11) * 0.3)
# 3.3
```

### `builtins_demo.py`
```python
# lecture 1-2 — builtins_demo.py
# built in - no import needed
print(abs(-3))           # 3
print(round(3.7))        # 4
print(round(3.14159, 2)) # 3.14
```

### `casting.py`
```python
# lecture 1-2 — casting.py
print(str(1234) + str(99))    # 123499
print(int("123"))             # 123
print(int(2.71828))           # 2     truncates
print(float("3.5"))           # 3.5
print(bool(0), bool(""))      # False False
```

### `casting_exercise.py`
```python
# lecture 1-2 — casting_exercise.py
print(7 / 2)
print(7 // 2)
print(int(7 / 2))
print(7 % 2)
print(int("7") // 2)
print("7" * int(7 / 2))
```

### `comparing_floats.py`
```python
# lecture 1-2 — comparing_floats.py
a = 0.7 + 0.1
b = 0.9 - 0.1

print(abs(a - b) < 1e-9)    # True
```

### `comparisons.py`
```python
# lecture 1-2 — comparisons.py
b*b - 4.0*c >= 0   # nonnegative?
year % 100 == 0    # new century?
x != 1             # not 1?
num % 2 == 0       # num is even ?
```

### `count_to_five.py`
```python
# lecture 1-1 — count_to_five.py
# Declares a variable and sets it to 0
i = 0
while i < 6:
    # Prints i, and increments it
    print(i)
    i = i + 1
print("Done")
```

### `count_to_five_bad.py`
```python
# lecture 1-1 — count_to_five_bad.py
i=0;
while i<6:print(i);i=i+1
print("Done")
```

### `division.py`
```python
# lecture 1-2 — division.py
print(5 / 2)     # 2.5
print(5 // 2)    # 2
print(4 / 2)     # 2.0
```

### `dog.py`
```python
# lecture 1-1 — dog.py
class Dog:
    def __init__(self, name):
        self.name = name
    def bark(self):
        print(self.name + " says woof")
rex = Dog("Rex")
rex.bark()
```

### `dynamic_typing.py`
```python
# lecture 1-2 — dynamic_typing.py
x = 5          # type(x) is int
x = "hello"    # type(x) is now str - perfectly legal
```

### `float_ops.py`
```python
# lecture 1-2 — float_ops.py
print(3.141 + 0.03)    # 3.171
print(6.02e23 / 2)     # 3.01e+23
print(5.0 / 2.0)       # 2.5
print(5.0 // 2.0)      # 2.0
print(1.0 / 3.0)       # 0.3333333333333333
print(1.0 / 0.0)       # ZeroDivisionError
```

### `fstrings.py`
```python
# lecture 1-2 — fstrings.py
a = 2
b = 3
print(f"{a} + {b} = {a + b}")       # 2 + 3 = 5

name = input()
age = int(input())
print(f"Hello {name}, next year you will be {age + 1}")
```

### `hello.py`
```python
# lecture 1-1 — hello.py
print("Hello World")
```

### `input_demo.py`
```python
# lecture 1-2 — input_demo.py

# Silent input (no prompt)
name = input()

# Input with a prompt message
name = input("What's your name? ")
print("Hello", name, "!")
```

### `input_is_text.py`
```python
# lecture 1-2 — input_is_text.py
age = input("How old are you? ")
print(type(age))     # <class 'str'>
print(age - 1)

# How old are you? 18
# <class 'str'>
# Traceback (most recent call last):
#   File "input_is_text.py", line 3, in <module>
#     print(age - 1)
#           ~~~~^~~
# TypeError: unsupported operand type(s) for -: 'str' and 'int'
```

### `int_input.py`
```python
# lecture 1-2, slide 29 — Reading an integer from the user
age = int(input("How old are you? "))
print("Next year you'll be", age + 1)
```

### `int_input_preview.py`
```python
# lecture 1-2 — int_input_preview.py
age = int(input("How old are you? "))
print(age - 1)      # 17

# How old are you? 18
# 17
```

### `int_ops.py`
```python
# lecture 1-2 — int_ops.py
print(5 + 3)     # 8
print(5 - 3)     # 2
print(5 * 3)     # 15
print(5 / 5)     # 1.0   a float, not an int
print(5 // 5)    # 1     floor division
print(5 % 3)     # 2
print(2 ** 10)   # 1024
print(1 / 0)     # ZeroDivisionError
```

### `invalid_operations.py`
```python
# lecture 1-2 — invalid_operations.py
1.0 / 0.0        # ZeroDivisionError
math.sqrt(-1.0)  # ValueError
1.0 + "3"        # TypeError
```

### `io_demo.py`
```python
# lecture 1-2 — io_demo.py
print("Hello!")
print("Result:", 42)            # Result: 42
x = 3
print(2, "+", x, "=", 2 + x)    # 2 + 3 = 5
```

### `leap_year.py`
```python
# lecture 1-2 — leap_year.py
year = int(input("Enter a year: "))
is_leap = (year % 400 == 0)
is_leap = is_leap or (year % 4 == 0 and year % 100 != 0)
print(is_leap)

# 2020 -> True   1900 -> False   2028 -> True
```

### `math_demo.py`
```python
# lecture 1-2 — math_demo.py
import math
print(math.sqrt(16))   # 4.0
print(math.floor(3.7)) # 3
print(math.ceil(3.2))  # 4
print(math.pi)        # 3.141592653589793
```

### `mixed_types.py`
```python
# lecture 1-2 — mixed_types.py
print(5 + 2.0)        # 7.0
print(5.0 // 2)       # 2.0
print(10 * 1.5)       # 15.0
print(7 % 2.0)        # 1.0
print(type(5 + 2.0))  # <class 'float'>
```

### `overloading.py`
```python
# lecture 1-2 — overloading.py
6 + 5        # 11
"6" + "5"    # '65'
```

### `precedence.py`
```python
# lecture 1-2 — precedence.py
print(3 * 5 - 2)     # 13   * binds first
print(3 - 5 - 2)     # -4   - associates left to right
print(3 - (5 - 2))   # 0    parentheses always win
```

### `programmer_view.py`
```python
# lecture 1-2 — programmer_view.py
sales_person = "Jack"
commission = 0.04
kg_sold = 509
```

### `pseudocode.txt`
```
# lecture 1-1 — pseudocode.txt
set i to 0
while i is less than 6:
    print i
    increase i by 1
print "Done"
```

### `quadratic.py`
```python
# lecture 1-2 — quadratic.py
import math
b = float(input("b: "))
c = float(input("c: "))
d = math.sqrt(b * b - 4.0 * c)
print((-b + d) / 2.0)
print((-b - d) / 2.0)
```

### `random_demo.py`
```python
# lecture 1-2 — random_demo.py
import random
print(random.random())               # in [0, 1)
print(2.0 * random.random())         # in [0, 2)
print(2.0 * random.random() - 1.0)   # in [-1, +1)
```

### `random_int.py`
```python
# lecture 1-2 — random_int.py
import random
n = int(input("Enter n: "))
r = random.random()      # in [0, 1)
result = int(r * n)      # in [0, n)
print(f"random integer is {result}")
```

### `repl_session.txt`
```
# lecture 1-1 — repl_session.txt
# Transcript of an interactive session -- not a script to run.
>>> 2 ** 10
1024
>>> "spam" + "eggs"
'spameggs'
>>> print("hello")
hello
>>> 1 / 0
ZeroDivisionError: division by zero
```

### `rounding.py`
```python
# lecture 1-2 — rounding.py
print(1.03 - 0.42)                 # 0.6100000000000001
print(1.00 - 9 * 0.10)             # 0.09999999999999998
print((0.7 + 0.1) == (0.9 - 0.1))  # False
```

### `six_and_five.py`
```python
# lecture 1-2, slide 39 — Numbers, or text that looks like numbers
print(6 + 5)                    # 11
print("6" + "5")                # 65
print("6" + str(5))             # 65
print(2, "+", 3, "=", 2 + 3)    # 2 + 3 = 5
```

### `spiral.py`
```python
# lecture 1-1, slide 13 — A taste of programming
# Draws a spiral of squares using turtle graphics.
# Run with: python spiral.py

import turtle
t = turtle.Turtle()
t.speed(0)
colors = ["#A64B00", "#1B3A5C", "#F5B759"]
for i in range(200):
    t.pencolor(colors[i % 3])
    t.forward(i * 2)
    t.right(91)
turtle.done()
```

### `str_growth.py`
```python
# lecture 1-2 — str_growth.py
s = "1"
s = s + " 2 " + s
s = s + " 3 " + s
print(s)
```

### `str_int.py`
```python
# lecture 1-2, slide 57 — Python will not convert for you
s1 = "Tel"
print(s1 + 3)
# TypeError: can only concatenate str
#            (not "int") to str
print(s1 + str(3))     # Tel3
print(s1 * "3")        # TypeError
print(s1 * int("3"))   # TelTelTel
```

### `str_ops.py`
```python
# lecture 1-2, slide 42 — Text: str
s1 = "Tel"
s2 = "Aviv"
print(s1 + s2)          # TelAviv
print(s2 + s1)          # AvivTel
print(s1 + " " + s2)    # Tel Aviv
```

### `str_ops_concat.py`
```python
# lecture 1-2 — str_ops_concat.py
s1 = "Tel"
s2 = "Aviv"
print(s1 + s2)          # TelAviv
print(s2 + s1)          # AvivTel
print(s1 + " " + s2)    # Tel Aviv
```

### `str_ops_mixed.py`
```python
# lecture 1-2 — str_ops_mixed.py
print(6 + 5)
print("6" + "5")
print("6" + 5)
print(2, "+", 3, "=", 2 + 3)
print(6 * 5)
print("6" * 5)
print(6 * "5")
print("6" * "5")
```

### `str_ops_mult.py`
```python
# lecture 1-2 — str_ops_mult.py
s = "Ha"
laugh = s * 3
divider = 10 * "-"

print(laugh)    # HaHaHa
print(divider)  # ----------
```

### `text_segments.py`
```python
# lecture 1-2 — text_segments.py
text_segment = "We hold these truths ..."
dna_segment = "ATGTTGCGGCTCGGGGCCAA ..."
html_segment = '<!DOCTYPE html> <html lang="en-US"> ...'
```

### `type_error.py`
```python
# lecture 1-2 — type_error.py
6 - 5        # 1
"6" - "5"
# TypeError: unsupported operand type(s)
# for -: 'str' and 'str'
```

### `types_demo.py`
```python
# lecture 1-2 — types_demo.py
type(5)          # <class 'int'>
type(3.14)       # <class 'float'>
type(True)       # <class 'bool'>
type("hello")    # <class 'str'>
```

### `variables_demo.py`
```python
# lecture 1-2 — variables_demo.py
x = -13
x = 25.5
x = "hello"
```
