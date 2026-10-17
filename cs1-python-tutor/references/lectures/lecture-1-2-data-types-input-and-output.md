# Lecture 1-2: Data types, input and output (week 1)

## Slide 1
INTRO TO CS COURSE · WEEK 1 · LECTURE 2
Data Types, Input and Output
Variables, dynamic typing, expressions, input and output

## Slide 2
Lecture overview
Data types
Variables
Expressions
Input / output
int
float
str
bool
Casting
1
Data types
every value has one
2
Variables
a name that refers to a value
3
Expressions
operators, precedence, and traps
4
The four types
int, float, str, bool — and casting

## Slide 3
Data
The same data – different representations
User view
What a person sees on the screen.
Programmer view
Data is manipulated using variables, statements,...
`programmer_view.py`
```python
sales_person = "Jack"
commission = 0.04
kg_sold = 509
```
Computer view
Data is represented as 0’s and 1’s (bits)
Data types
Expressions
Input / output
int
float
str
bool
Casting
Variables

## Slide 4
What is a Data Type?
A Data Type is a set of possible values, together with the operations allowed on them.
```python
The values
… −2  −1  0  1  2  3 …
Everything a value of this type
is allowed to be.
```
```python
The operations
+  −  *  /  //  %  **
Everything you are allowed
to do with them.
```

## Slide 5
Every value has a type
Every value that exists while a program runs has a type of its own.
type() - the built-in that answers “what type is this value?”
The type decides — which operations are legal, and what they mean.

## Slide 6
`types_demo.py`
```python
type(5)          # <class 'int'>
type(3.14)       # <class 'float'>
type(True)       # <class 'bool'>
type("hello")    # <class 'str'>
```
Every value has a type

## Slide 7
Fundamental Data Types in Python
```python
int
5
Whole numbers.
Exact, and unlimited in size.
```
```python
str
"hello"
Text.
Any characters, in quotes.
```
```python
float
3.14
Real numbers.
Stored with finite precision.
```
```python
bool
True
Logical values.
Only True and False.
```

## Slide 8
What is a Variable ?
You can picture it as a label you stick on a value.
You can peel it off one value and stick onto another.
A Variable is a name that refers to a value in the program.
`variables_demo.py`
```python
x = -13
x = 25.5
x = "hello"
```
Data types
Expressions
Input / output
int
float
bool
str
Casting
Variables

## Slide 9
Variable creation and assignment
Assignment (=) - Binds a name of the variable to a value.
Automatic creation - Creating a variable happens implicitly on its first assignment.
A variable has no type — type(x) reports the type of the value x refers to right now.

## Slide 10
Variable creation and assignment
Memory view during execution
The code (abstraction)
```python
x = -13
x = 25
x = x + 1
y = x - 5
```
The name is a label
state 2
```python
-13
```
```python
25
```
```python
x
```
state 3
```python
-13
```
```python
25
```
```python
26
```
```python
x
```
state 4
```python
-13
```
```python
25
```
```python
26
```
```python
x
```
```python
21
```
```python
y
```
In memory (implementation), after each line
state 1
```python
-13
```
```python
x
```
.                          The value is what is sitting in memory — and re-assigning moves the label.

## Slide 11
…and in memory, it is bits
The code (abstraction)
```python
x = -13
x = 25
x = x + 1
y = x - 5
```
The memory actually holds bits
In memory (actual implementation – in bits), after each line
state 1
```python
11110011
```
```python
x
```
state 2
```python
11110011
```
```python
00011001
```
```python
x
```
state 3
```python
11110011
```
```python
00011001
```
```python
00011010
```
```python
x
```
state 4
```python
11110011
```
```python
00011001
```
```python
00011010
```
```python
x
```
```python
00010101
```
```python
y
```
Actual memory view during execution

## Slide 12
The same name, a different kind of value
`dynamic_typing.py`
```python
x = 5          # type(x) is int
x = "hello"    # type(x) is now str - perfectly legal
```
This is what "dynamically typed" means.

## Slide 13
Static vs. Dynamic Typing
Statically typed
The type of every variable is fixed and checked before the program runs.

Java · C · C++ · C# · Go · Rust · Swift
Dynamically typed
Types belong to values and are checked while the program runs.


Python · JavaScript · Ruby · PHP
Determined by when types are checked and bound.

## Slide 14
Strong vs. Weak Typing
Strongly typed
types are strictly enforced, with little or no automatic conversion.

Python · Java · Ruby · Swift
Weakly typed
types are converted automatically when needed.

JavaScript · C · PHP · Perl
Determined by whether implicit type conversions are allowed.

## Slide 15
Dynamic Typing – Pros & Cons
Pros - Quicker to write - Less boilerplate, no declarations, faster prototyping. 
Cons - Errors arrive later - Type errors surface only when the code executes, sometimes under specific inputs.
Middle ground - Type hints - Optional static-like annotations (e.g., x: int = 5).

## Slide 16
Naming - Python requirements
Allowed characters - letters, digits, underscores ( _ ) only.
Must start with a letter or underscore – names cannot start with a digit.
Case-sensitive — age, Age and AGE are three different names.
No reserved words — the 35 keywords (from lecture 1-1) are out of bounds.
Nothing else is enforced — the syntax rules are minimal, which is why the conventions matter.

## Slide 17
Naming: Legal and illegal names
```python
age
```
```python
student_count
```
```python
_temp
```
```python
MAX_SCORE
```
```python
2nd_place
```
starts with a digit
```python
my-name
```
hyphens are not allowed
```python
class
```
a reserved word
```python
my name
```
no spaces

## Slide 18
Naming: Python conventions (readability)
```python
snake_case (PEP 8) – Use lowercase words separated by underscores for variable names (e.g., student_count, total_price, is_leap_year).
Meaningful names - Choose clear, descriptive names (student_count instead of sc). Reserve short names like i or j strictly for loop counters.
ALL_CAPS for constants – Used for values intended never to change during execution (e.g., MAX_SCORE = 100). A convention only (not enforced by python).
```

## Slide 19
What is an expression ?
```python
Operands - the values or variables that an operator acts upon (e.g., x and 4 in the x + 4)
Operator rules – each operator is defined for specific data types.
```
Data types
Expressions
Input / output
int
float
str
bool
Casting
An expression is a combination of values, variables and operators that evaluate to a single value.
Variables

## Slide 20
Operator overloading
`overloading.py`
```python
6 + 5        # 11
"6" + "5"    # '65'
```
How it works
The operand types determine the actual operation executed by the symbol
Not all operators apply to all types
Some operations are invalid for specific types
Same symbol, different operations
`type_error.py`
```python
6 - 5        # 1
"6" - "5"
# TypeError: unsupported operand type(s)
# for -: 'str' and 'str'
```

## Slide 21
Assignment vs. Comparison
Two things that look almost the same, and are not:
=  is a statement: it binds a name to a value
==  is an operator: it compares two values and produces True or False

## Slide 22
Output: print()
`io_demo.py`
```python
print("Hello!")
print("Result:", 42)            # Result: 42
x = 3
print(2, "+", x, "=", 2 + x)    # 2 + 3 = 5
```
Data types
Expressions
Input / output
int
float
str
bool
Casting
print() - Python’s built-in function that outputs values to the screen,
separated by spaces by default. 
Variables

## Slide 23
Input: input()
`input_demo.py`
```python
# Silent input (no prompt)
name = input()
```
input() - Python’s built-in function that reads a line of input from the user as text.
```python
# Input with a prompt message
name = input("What's your name? ")
print("Hello", name, "!")
```
Prompt – an optional string printed to the screen to guide the user on what to enter.

## Slide 24
input() always returns text
`input_is_text.py`
```python
age = input("How old are you? ")
print(type(age))
print(age - 1)
```
```python
Return value is always text
Even if the user types digits, input() always returns a string (e.g., "18" instead of the number 18).
```
Python is strongly typed
Python will not automatically convert text to numbers for arithmetic operations. Mixing types causes a runtime error.
Digits entered via input() are stored as text, not numbers.
```python
terminal
```
```python
TypeError: unsupported operand type(s)
           for -: 'str' and 'int'
```
```python
<class 'str'>
```
```python
How old are you? 
```
```python
18
```

## Slide 25
From text to number
`int_input_preview.py`
```python
age = int(input("How old are you? "))
print(age - 1)
```
int() converts text to a whole number — the full story in the Casting section.
So what do we do if we want to read a number ?
```python
terminal
```
```python
How old are you? 18
17
```

## Slide 26
Command-line input
A program can also receive input directly from the command line:
sys.argv - captures arguments passed after the program’s name when executed in the terminal.
For now, we will focus on interactive input via input(). You will primarily encounter sys.argv when reading existing codebase or running automated scripts.

## Slide 27
The int data type: Data & Operations 
Data types
Expressions
Input / output
int
float
str
bool
Casting
```python
+
```
```python
-
```
```python
*
```
```python
/
```
```python
//
```
floor division
```python
%
```
```python
**
```
exponentiation
```python
Data: whole numbers (integers) - Positive, negative or zero, with no decimal point (e.g., 42, -7, 0).

Operations: 
```
Variables
addition
subtraction
multiplication
division
modulo

## Slide 28
int operations
`int_ops.py`
```python
print(5 + 3) 
print(5 - 3)
print(5 * 3)
print(5 / 5)
print(5 // 5)
print(5 % 3)
print(2 ** 10)
print(1 / 0)
```
```python
# 8
# 2
# 15
# 1.0   a float, not an int
# 1     floor division
# 2
# 1024
# ZeroDivisionError
```

## Slide 29
Precedence
`precedence.py`
```python
print(3 * 5 - 2)     # 13   * binds first
print(3 - 5 - 2)     # -4   - associates left to right
print(3 - (5 - 2))   # 0    parentheses always win
```

## Slide 30
The two divisions 
`division.py`
```python
print(5 / 2)     # 2.5
print(5 // 2)    # 2
print(4 / 2)     # 2.0
```
/ is true division
It always produces a number with a decimal point, even when the answer is whole.
// is floor division
Divide, then throw the remainder away

## Slide 31
Python integers do not overflow
`big_int.py`
```python
print(2 ** 100)
# 1267650600228229401496703205376
```
Arbitrary precision
Python integers automatically allocate more memory as they grow, so there is no fixed upper limit.
No silent wraparound
In languages like C or Java, exceeding maximum integer limits silently rolls values back to negatives (wraparounds). Python completely prevents this bug.

## Slide 32
The float data type: Data & Operations
Data types
Expressions
Input / output
int
float
str
bool
Casting
```python
+
```
```python
-
```
```python
*
```
```python
/
```
```python
//
```
floor division
```python
%
```
```python
**
```
exponentiation
```python
Data: real numbers – Numbers with a fractional part (e.g., 3.14, -0.5, 6.02e23).

Operations: 
```
Variables
addition
subtraction
multiplication
division
modulo

## Slide 33
Examples
`float_ops.py`
```python
print(3.141 + 0.03)    # 3.171
print(6.02e23 / 2.0)   # 3.01e+23
print(5.0 / 2.0)       # 2.5
print(5.0 // 2.0)      # 2.0
print(1.0 / 3.0)       # 0.3333333333333333
print(1.0 / 0.0)       # ZeroDivisionError
```

## Slide 34
When int meets float
`mixed_types.py`
```python
print(5 + 2.0)        # 7.0
print(5.0 // 2)       # 2.0
print(10 * 1.5)       # 15.0
print(7 % 2.0)        # 1.0
print(type(5 + 2.0))  # <class 'float'>
```
The rule
An int mixed with a float always gives a float. The whole number is widened; the fractional side is never cut.
Why it happens
A whole number is a real with nothing after the point, so a float can hold it. An int cannot hold a fraction. So the float side does the work.
```python
Not the same as /
4 / 2 gives 2.0 from two ints. That is the rule of / itself, not a conversion - True division always returns a float.
```

## Slide 35
Math operations & the math module
Python provides built-in functions as well as dedicated modules for mathematical operations.
`builtins_demo.py`
```python
# built in - no import needed
print(abs(-3))           # 3
print(round(3.7))        # 4
print(round(3.14159, 2)) # 3.14
```
Built-in math functions
Always available without importing anything.
`math_demo.py`
```python
import math
print(math.sqrt(16))   # 4.0
print(math.floor(3.7)) # 3
print(math.ceil(3.2))  # 4
print(math.pi)        # 3.141592653589793
```
```python
The math module
Requires import math to access advanced mathematical functions and constants.
```

## Slide 36
How Python handles invalid operations
`invalid_operations.py`
```python
1.0 / 0.0        # ZeroDivisionError
math.sqrt(-1.0)  # ValueError
1.0 + "3"        # TypeError
```
Same mechanism, different errors
When an operation is mathematically or logically invalid, Python raises an exception.
No silent failures
Instead of returning dangerous default values (like Infinity or NaN), Python stops immediately.
Coming up later
How to catch these errors using try / except.

## Slide 37
Example: the quadratic equation
`quadratic.py`
```python
import math
b = float(input("b: "))
c = float(input("c: "))
d = math.sqrt(b * b - 4.0 * c)
print((-b + d) / 2.0)
print((-b - d) / 2.0)
```
Solves x² + bx + c = 0. Try b = -3, c = 2.

## Slide 38
Textual information
HTML:
DNA:
Text:
Python:
```python
text_segment = "We hold these truths ..."
dna_segment = "ATGTTGCGGCTCGGGGCCAA ..."
html_segment = '<!DOCTYPE html> <html lang="en-US"> ...'
```
`text_segments.py`
Data types
Expressions
Input / output
int
float
str
bool
Casting
Variables

## Slide 39
The str data type: Data & Operations 
```python
+
```
concatenations
```python
Data: Textual information (sequences of characters) – enclosed in single of double quotes (e.g., "Hello ", ‘Python’," 42 ").

Operations: 
```
```python
*
```
repetition
more operations and methods – coming up soon...

## Slide 40
The + operator of str 
`str_ops_concat.py`
```python
s1 = "Tel"
s2 = "Aviv"
print(s1 + s2)          # TelAviv
print(s2 + s1)          # AvivTel
print(s1 + " " + s2)    # Tel Aviv
```
What does the operator do ?
The + operator performs string concatenation. It joins two or more strings end-to-end to form a single continuous string.
```python
   Important Note: Spaces
Python does not insert spaces automatically between joined strings. If a space is needed between words, you must include it explicitly (e.g. " ").
```

## Slide 41
```python
The * operator of str 
```
`str_ops_mult.py`
```python
s = "Ha"
laugh = s * 3
divider = 10 * "-"

print(laugh)    # HaHaHa
print(divider)  # ----------
```
```python
What does the operator do ?
The * operator performs string repetition. It duplicates a string a specified number of times and concatenates the copies together.
```
   Rule: Types
Repetition requires exactly one string (str) and one whole number (int). You cannot “multiply” two strings together!

## Slide 42
Class exercise – Predict the output
`str_ops_mixed.py`
```python
print(6 + 5)
print("6" + "5")
print("6" + 5)
print(2, "+", 3, "=", 2 + 3)
print(6 * 5)
print("6" * 5)
print(6 * "5")
print("6" * "5")
```

## Slide 43
`str_growth.py`
```python
s = "1"
s = s + " 2 " + s     
s = s + " 3 " + s     
print(s)
```
Class exercise – Predict the output

## Slide 44
f-strings
`fstrings.py`
```python
a = 2
b = 3
print(f"{a} + {b} = {a + b}")       # 2 + 3 = 5

name = input()
age = int(input())
print(f"Hello {name}, next year you will be {age + 1}")
```
An f before the quote
Anything inside { } is evaluated as Python expressions and automatically converted to text.
No more TypeError!
Numbers inside {} are converted automatically. This is the standard way to build formatted text in Python.

## Slide 45
George Boole · 1815–1864
Created Boolean logic - a mathematical system using only True and False. A century later, it became the foundation upon which all modern computer systems and software are built.
Boolean logic
Data types
Expressions
Input / output
int
float
bool
str
Casting
Variables

## Slide 46
The bool type: Data & Operations
```python
not
```
```python
and
```
```python
or
```
```python
Data: True, False. 

Operations (Boolean connectors):
```

## Slide 47
Boolean connectors truth tables
Every combination of inputs, and the value each connector returns.
a | not a
True | False
False | True
a | b | a and b
True | True | True
True | False | False
False | True | False
False | False | False
a | b | a or b
True | True | True
True | False | True
False | True | True
False | False | False
```python
not
```
```python
and
```
```python
or
```

## Slide 48
operator | meaning | true | false
 | equal | 2 == 2 | 2 == 3
 | not equal | 3 != 2 | 2 != 2
 | less than | 2 < 13 | 2 < 2
 | less than or equal | 2 <= 2 | 3 <= 2
 | greater than | 13 > 2 | 2 > 13
 | greater than or equal | 3 >= 2 | 2 >= 3
Comparison operators
```python
==
```
```python
!=
```
```python
<
```
```python
<=
```
```python
>
```
```python
>=
```

## Slide 49
`age_check.py`
```python
city = input("City: ")
age  = int(input("Age: "))

print(city == "Tel Aviv")   # True — already a bool
too_young = age < 18        # the same value, with a name
if too_young:
    print("You are too young for this")
```
Worked examples

## Slide 50
Worked examples
`comparisons.py`
```python
b*b - 4.0*c >= 0   # nonnegative?
year % 100 == 0    # new century?
x != 1             # not 1?
num % 2 == 0	      # num is even ?
```

## Slide 51
Worked example: leap years
Definition: A leap year (שנה מעוברת) is a year which is 
                       (i) Divisible by 400, or (ii) Divisible by 4 but not by 100.
Task: Write a program that determines if a given year is a leap year.
`leap_year.py`
```python
year = int(input("Enter a year: "))
is_leap = (year % 400 == 0)
is_leap = is_leap or (year % 4 == 0 and year % 100 != 0)
print(is_leap)
```
Try: 2026, 2020, 1900, 1600

## Slide 52
The float precision trap
`rounding.py`
```python
print(1.03 - 0.42)  		 # 0.6100000000000001
print(1.00 - 9 * 0.10) 		 # 0.09999999999999998
print((0.7 + 0.1) == (0.9 - 0.1)) # False
```
IEEE 754 representation
Computers stores floats in binary (bits). Some decimal fractions (like 0.1) cannot be represented exactly, leading to small rounding inaccuracies.

## Slide 53
Comparing floats
`comparing_floats.py`
```python
a = 0.7 + 0.1
b = 0.9 - 0.1
print(abs(a - b) < 1e-9)    # True
```
Never use ==
Compare the gap instead, using an epsilon tolerance.
Define required precision
Choose an accuracy threshold suitable for your application domain.
```python
Exact arithmetic alternatives
Use Pythons decimal or fractions modules when exact values are required (e.g., financial calculations).
```

## Slide 54
Casting: Type conversion
Data types
Expressions
Input / output
int
float
str
bool
Casting
int()
Converts text or a float, to a whole number
Truncates the decimal parts (does not round!)
float()
Converts text or int, to a real (decimal) number
str()
Converts any value to a text string.
```python
bool()
Converts any value to True or False.
0, 0.0 and "" becomes False.
```
Variables
Explicitly converting a value from one data type to another using built-in functions.
Python also converts on its own, without being asked - an int mixed with a float, as seen earlier.

## Slide 55
Worked examples
`casting.py`
```python
print(str(1234) + str(99))    # 123499
print(int("123"))             # 123
print(int(2.71828))           # 2     truncates
print(float("3.5"))           # 3.5
print(bool(0), bool(""))      # False False
```

## Slide 56
`casting_exercise.py`
```python
print(7 / 2)
print(7 // 2)
print(int(7 / 2))
print(7 % 2)
print(int("7") // 2)
print("7" * int(7 / 2))
```
Class exercise – Predict the output

## Slide 57
When a conversion fails
`bad_input.py`
```python
age = int(input("How old are you? "))
print(age + 1)
```
What went wrong ?
Read the last line first: int() received text that cannot be converted to a whole number.
Where did it fail ?
The File line gives the file name and the line number.
The carets point at the exact expression that failed.
Reading error messages
Error messages seem cryptic at first, but reading them carefully is an essential debugging skill.
```python
terminal
```
```python
How old are you? 
```
```python
hello
```
```python
Traceback (most recent call last):
  File "bad_input.py", line 1, in <module>
    age = int(input("How old are you? "))
          ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
ValueError: invalid literal for int()
            with base 10: 'hello'
```

## Slide 58
The random module
`random_demo.py`
```python
import random
print(random.random())               # in [0, 1)
print(2.0 * random.random())         # in [0, 2)
print(2.0 * random.random() - 1.0)   # in [-1, +1)
```
Run it twice and get different outputs
The random module provides tools for generating random numbers and values.

## Slide 59
A worked example: a random whole number
`random_int.py`
```python
import random
n = int(input("Enter n: "))
r = random.random()      # in [0, 1)
result = int(r * n)      # in [0, n)
print(f"random integer is {result}")
```

## Slide 60
Lecture summary
```python
int
+ - * / // % **
exact, unlimited size
```
```python
str
+  *
and f-strings
```
```python
float
+ - * / // % **
finite precision
```
```python
bool
not · and · or
and the six comparisons
```
Fundamental Data Types
Data types
Variables
Expressions
Input / output
int
float
str
bool
Casting

## Slide 61
Lecture summary
```python
Every value has a type
type(5)   →   int
A variable is not a box.
It is a name that refers
to a value.
```
```python
Dynamic, and strong
"6" + 5   →   TypeError
The type is checked when
the line runs — and never
converted behind your back.
```
```python
Input arrives as text
input()   →   str
Always. Turning it into a
number is your job.
```
```python
int is exact, float is not
0.1 + 0.2   →   0.30000000000000004
Compare floats with a
tolerance, never with ==.
```

## Slide 62
INTRO TO CS COURSE · WEEK 2 · LECTURE 1
Next: Conditionals and loops
Making a program choose, and making it repeat
