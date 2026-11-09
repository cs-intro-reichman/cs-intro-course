# Lecture 4-2: Functions, part 2: modules, API and design (week 4)

## Slide 1: Functions, Part 2
INTRO TO CS COURSE · WEEK 4 · LECTURE 2
Functions, Part 2
Modules, API, and design

## Slide 2
Lecture overview
1
Modules and API
using a function someone else wrote
2
Designing with functions
splitting a task into pieces
Why functions
Anatomy
Call and return
Defaults and keywords
Modules and API
Designing
A worked design

## Slide 3: Modularity
Modularity
Dividing a program into named pieces.
Less complexity: each piece can be understood on its own
Less duplication: fewer places for bugs
Testable: a function can be checked by itself
Shareable: two people can write two functions at once
Why functions
Anatomy
Call and return
Defaults and keywords
Modules and API
Designing
A worked design
one long
program
read_input
compute
report
The same work — with names you can call.

## Slide 4: A library and its user
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
the user: what is needed.
mymath.py
main.py
import mymath
mymath.my_sqrt(2)  →  1.4142
One file asks; the other answers.

## Slide 5: Calling syntax
Calling syntax
How you call a function depends on where it is.
```python
Same file: my_sqrt(2), just the name
Another module: mymath.my_sqrt(2)
```

## Slide 6: The caller's view: a black box
The caller's view: a black box
An API describes what a function does for its caller.
What it is called: the name and its parameters
What it gives back: the value, and what it means
What it assumes: the inputs it will not accept
Not how: the caller does not need the body.
16
input
my_sqrt
?
4.0012
output
The same machine — and the caller never opens it.

## Slide 7: Documenting the API
Documenting the API
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
```python
terminal
```
```python
help(mymath.my_sqrt)
my_sqrt(x, epsilon=0.001)
    Return a number whose
    square is near x.
```

## Slide 8: Functions vs. methods
Functions vs. methods
Both take inputs and return a result. They differ in where they live.
```python
a
```
```python
b
```
```python
c
```
```python
len
```
```python
a
```
```python
b
```
```python
c
```
```python
.upper()
```
function
method
how it is called
```python
len(s)
```
```python
s.upper()
```
where it lives
on its own
inside a type
works on
often many types
only its own type
Function: the value goes inside. Method: before the dot.
```python
Rule of thumb (A tendency, not a law)
Many types: Usually a function: len, print, str.
One type: Usually a method: .upper() is only for strings.
```
```python
Two dots, two meanings
mymath.  — before the dot is a module: where the function lives.
s.  — before the dot is a value: what the method works on.
Same character; one says where to look, the other what to act on.
```

## Slide 9: A method belongs to its data type
A method belongs to its data type
Python enforces where a method lives.
`errors.py`
```python
x = 5
x.upper()     # AttributeError
```
`arguments.py`
```python
s = "Hello"
s.count("l")          # 2
s.replace("l", "L")   # 'HeLLo'
```
The value before the dot is the first input.
```python
5
```
```python
int
```
!
```python
'int' object has no attribute 'upper'
```
An int has no such tool.
```python
upper
```
```python
name 'upper' is not defined
```
No such function.
```python
H
```
```python
e
```
```python
l
```
```python
l
```
```python
o
```
```python
.count()
```
```python
"l"
```
the value acted on
the argument
```python
upper("hi")   # NameError
```

## Slide 10: What makes a good function
What makes a good function
```python
One job: if the name needs “and”, it is two functions
A good name: says what it returns or does, like perimeter, is_right, print_primes
Few parameters: many parameters suggest a bad design
A docstring: one sentence saying what it returns
```
Why functions
Anatomy
Call and return
Defaults and keywords
Modules and API
Designing
A worked design

## Slide 11: Top-down design
Top-down design
The task: in one sentence, what must the program do?
Split it: name the pieces the task needs
Repeat: split any piece that is still too big
Stop: when every piece is one small job
Number guessing game
Set up
Play a round
Finish
Pick a secret
Set max tries
Read a guess
Check guess
Show result
Offer replay

## Slide 12: A decomposition diagram
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

## Slide 13: Design before code
Design before code
Signatures: each function's name and parameters
Docstrings: in one sentence, what does it return?
Stubs: placeholder bodies, so the program runs
Bodies last: fill in and test one at a time
```python
def average(a, b):
```
```python
"""Return the mean of a and b."""
```
```python
avg = (a + b) / 2
```
```python
return 0.0
```
```python
body
```

## Slide 14: Stubs first, bodies later
Stubs first, bodies later
`stubs.py`
```python
# Sketch first: the real bodies come later
def hypot(x1, y1, x2, y2):
    return 0.0

def my_sqrt(x, epsilon=0.001):
    return 0.0

print(hypot(2, 1, 5, 4))
```
What is a stub?
A function with its real name and parameters, but a placeholder body (here, return 0.0).
The program already runs, so you can check how the pieces fit together, then write the real bodies one at a time.
```python
terminal
```
```python
0.0
```

## Slide 15: The design, written down
The design, written down
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
```python
terminal
```
```python
perimeter: 0.0
right angle: False
```

## Slide 16: Then fill in the bodies
Then fill in the bodies
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
```python
terminal
```
```python
perimeter: 12.0
right angle: True
```

## Slide 17: Your turn: decompose
Your turn: decompose
Draw the diagram first. No code yet.
The task
Read a whole number n. Print every prime number from 2 to n, and then how many primes there were.
Your steps
1. Name the functions you need.
2. Give each a signature and a   docstring.
3. Draw who calls whom.
Why functions
Anatomy
Call and return
Defaults and keywords
Modules and API
Designing
A worked design

## Slide 18: Solution: the pieces
Solution: the pieces
```python
The task: read n, print the primes from 2 to n, then their count
main: reads n, tries every k from 2 to n, counts the primes
is_prime(k): one job, True if k is a prime number
Stop: is_prime needs no “and”, so it is small enough
```

## Slide 19: Solution: the diagram
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

## Slide 20: Solution: the design, written down
Solution: the design, written down
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
```python
terminal
```
```python
20

0 primes
```

## Slide 21: Solution: fill in the body
Solution: fill in the body
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
```python
terminal
```
```python
20
2 3 5 7 11 13 17 19 
8 primes
```

## Slide 22: Checking a function with assert
Checking a function with assert
`primes_check.py`
```python
# is_prime(k) -> True or False
assert is_prime(7)
assert is_prime(2), "2 is prime"   # easy to get wrong
assert not is_prime(9)

# count_primes(n) -> a number
assert count_primes(10) == 4       # 2 3 5 7
assert count_primes(1) == 0        # none at all
print("all checks passed")
```
```python
What assert is
Syntax: assert <condition you believe is true>
Semantics: if condition is True, nothing happens and the program carries on. If it is False, the program stops, with an AssertionError.
It is possible to add an error message in case condition is False (e.g., "2 is prime" )
```
```python
terminal
```
```python
all checks passed
```
```python
terminal
```
```python
AssertionError: 2 is prime
```
```python
With return k > 2 in is_prime:
```
Verifying that your function fulfills its guarantees

## Slide 23: Design and AI tools
Design and AI tools
AI tools can now write a function body in seconds.
What they need: a clear name, parameters and docstring
Yours to decide: what the pieces are and how they fit
How you check: test each small function by itself
You design
name, parameters, docstring
AI writes
the function body
You check
test each function alone

## Slide 24: Class exercise: the Caesar cipher
Class exercise: the Caesar cipher
Task: shift every lowercase letter of a given string a fixed number of places.
Why functions
Anatomy
Call and return
Defaults and keywords
Modules and API
Designing
A worked design
```python
terminal
```
```python
hello, world
3
khoor, zruog
```
Algorithm: which steps are functions?
Initialize: Create an empty string.
1
Loop over input's characters one by one:
2
Check if character is a lower case letter. If it is:
2,1
Shift letter
Convert letter to position 0 to 25
2,1.1
Shift letter position, wrapping from 25 to 0
2,1.2
Convert back from position to letter
2,1.3
Append character to new string.
2.2
```python
a
```
```python
d
```
```python
b
```
```python
e
```
```python
c
```
```python
f
```
```python
d
```
```python
g
```
```python
e
```
```python
h
```
```python
f
```
```python
i
```
```python
g
```
```python
j
```
```python
h
```
```python
k
```
```python
i
```
```python
l
```
```python
j
```
```python
m
```
```python
k
```
```python
n
```
```python
l
```
```python
o
```
```python
m
```
```python
p
```
```python
n
```
```python
q
```
```python
o
```
```python
r
```
```python
p
```
```python
s
```
```python
q
```
```python
t
```
```python
r
```
```python
u
```
```python
s
```
```python
v
```
```python
t
```
```python
w
```
```python
u
```
```python
x
```
```python
v
```
```python
y
```
```python
w
```
```python
z
```
```python
x
```
```python
a
```
```python
y
```
```python
b
```
```python
z
```
```python
c
```
outer: plain
inner: shift 3
```python
x
```
```python
23
```
```python
26
```
```python
0
```
```python
a
```
Test first: xyz with shift 3 must give abc.

## Slide 25: Solution: the pieces
Solution: the pieces
```python
main: reads the message and the shift, encrypts the message and prints the result
encrypt(text, shift): steps 1, 2, 2.1 and 2.2
shift_letter(ch, shift): steps 2.1.1 to 2.1.3
```

## Slide 26: Solution: the diagram
Solution: the diagram
One chain. A box is a function; an arrow means “calls”.
main
the top-level code
encrypt
to write
shift_letter
to write
once per character
```python
Where to stop
shift_letter does three things: 
Letter to number
Shift with the wrap.
Number back to letter.
That is one body, not three more functions - a piece stops earning a name when it is one expression.
```

## Slide 27: Solution: the design, written down
Solution: the design, written down
`caesar_design.py`
```python
# The design first: names, parameters, promises
def shift_letter(ch, shift):
    """Return ch shifted inside a..z."""
    return ch

def encrypt(text, shift=3):
    """Return text with its lowercase letters shifted."""
    return text

text = input("Message: ")
shift = int(input("Shift: "))
print(encrypt(text, shift))
```
```python
terminal
```
```python
hello, world
3
hello, world
```
What this proves
The message comes back unchanged — the stubs run, and main is already right.

## Slide 28: Solution: fill in the bodies
Solution: fill in the bodies
`caesar.py`
```python
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

text = input("Message: ")
shift = int(input("Shift: "))
print(encrypt(text, shift))
```
```python
terminal
```
```python
hello, world
3
khoor, zruog
```
2.1
2.1.1
2.1.2
2.1.3
1
2
2.2

## Slide 29: Your turn: decryption
Your turn: decryption
A follow-up task: undo the cipher, without writing a new loop.
```python
The task: decrypt(text, shift) takes the encrypted message and the shift used to encrypt it, and returns the original.
```
The hint: Encrypt already does the work. 
```python
terminal
```
```python
khoor, zruog
3
hello, world
```
`caesar.py`
```python
def decrypt(text, shift=3):
    """Return the original message."""
    return encrypt(text, -shift)
```
-3 % 26 is 23, so the wrap holds.

## Slide 30: A function is an object
A function is an object
`function_object.py`
```python
def my_sqrt(x):
    epsilon = 0.01
    g = x / 2
    while abs(g * g - x) > epsilon:
        g = g - (g * g - x) / (2 * g)
    return g

print(my_sqrt)        # <function my_sqrt at 0x...>
f = my_sqrt           # no parentheses: the function itself
print(f(16))          # 4.001219512195122
print(f is my_sqrt)   # True - one object, two names
```
```python
The name and the call
my_sqrt is the function’s name.
my_sqrt(16) is what it returns when you call it. 
f = my_sqrt binds the name f to the function’s object. 
f = my_sqrt(16) calls the function and binds the name f to the result (4.0012).
```
my_sqrt
f
one function object
Same function, two names. 
A function is a value, like any other

## Slide 31: Lecture summary
Lecture summary
Modules and API: import it, read its docstring, ignore its body
Designing with functions: top-down, stubs first, and assert each piece on its own
And a function is a value: it can be named, and next lecture it is passed as an argument to another function.
Why functions
Anatomy
Call and return
Defaults and keywords
Modules and API
Designing
A worked design

## Slide 32
Next: Lists and Tuples
Sequences that can be changed
INTRO TO CS COURSE · WEEK 5 · LECTURE 1
