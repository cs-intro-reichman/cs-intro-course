# Recitation, week 4: Functions, lists and tuples

## From `recitation 4.pptx`

## Slide 1
```python
def
```
PYTHON COURSE · WEEK 4 · RECITATION 4
Recitation 4
Approximation and functions

## Slide 2
Recitation overview
Warm-up
Functions
Roots
Design
Newton
Extra
Wrap-up
1
Predictions
None, local names, and three passes of bisection
2
Functions
small, named, tested in the REPL
3
Roots
lecture 3-2's loops, one function away
4
Design
a date, built top-down; Newton, with a trace

## Slide 3
Warm-up: functions
Warm-up
Functions
Roots
Design
Newton
Extra
Wrap-up
WARM-UP · 4 MIN
Four printed lines. Which call prints which, and what is b?
`warmup_functions.py`
```python
def double(x):
    return 2 * x
def shout(word):
    print(word.upper())

a = double(4)
b = shout("hi")
print(a, b)
print(double(double(3)))
x = 10
def change():
    x = 5
change()
print(x)
```
The answers
HI   (printed during the call to shout)
8 None
12
10

## Slide 4
Warm-up: bisection by hand
Warm-up
Functions
Roots
Design
Newton
Extra
Wrap-up
WARM-UP · 4 MIN
Lecture 3-2's bisection with x = 10. Fill in low, high and g after the first three passes.
`warmup_bisection.py`
```python
# Bisection (lecture 3-2), for x = 10
x = 10
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
```python
The answers
start   low 1.0  high 10.0  g 5.5
pass 1  5.5 too big   -> high 5.5   g 3.25
pass 2  3.25 too big  -> high 3.25  g 2.125
pass 3  2.125 too small -> low 2.125 g 2.6875
the run: 3.1621 in 8 steps
sequential search: about 21,600 steps
```

## Slide 5
Exercise 1: Three small functions
Warm-up
Functions
Roots
Design
Newton
Extra
Wrap-up
EASY · 8 MIN ON YOUR OWN
Task: three small functions, each with a docstring, tested in the REPL.
```python
is_leap(year): True for a leap year - lecture 1-2's rule, as a function
digit_sum(n): the sum of the digits of n - recitation 2's loop, as a function
count_vowels(text): how many of a, e, i, o, u the text contains, in either case
Save as small_functions.py; import and call in the REPL
```
```python
the REPL
```
```python
>>> import small_functions as sf
>>> sf.is_leap(1900)
False
>>> sf.digit_sum(4913)
17
>>> sf.count_vowels("Reichman")
3
```
```python
Think about
return a value; never print inside these functions
A comparison is already a value: return it
The accumulator pattern: count in a loop, return after the loop
```

## Slide 6
Exercise 1: one solution
`small_functions.py`
```python
def is_leap(year):
    """Return True when year is a leap year."""
    by_400 = year % 400 == 0
    by_4 = year % 4 == 0 and year % 100 != 0
    return by_400 or by_4


def digit_sum(n):
    """Return the sum of the digits of n (n >= 0)."""
    total = 0
    while n > 0:
        total += n % 10
        n = n // 10
    return total


def count_vowels(text):
    """Return how many vowels text contains."""
    count = 0
    for ch in text.lower():
        if ch in "aeiou":
            count += 1
    return count
```
```python
Three shapes of function
A one-liner: the boolean is the value, so return the comparison itself
A loop that empties its input: n is a local name; the caller's number is untouched
An accumulator: count in a loop, return after the loop; return inside the loop would stop at the first vowel
Docstrings: the first line of the body, in triple quotes, says what comes back; help(sf.digit_sum) reads it
```
```python
the REPL
```
```python
>>> sf.is_leap(2000)
True
>>> sf.digit_sum(0)
0
>>> sf.count_vowels("xyz")
0
```

## Slide 7
Exercise 2: Roots, as functions
Warm-up
Functions
Roots
Design
Newton
Extra
Wrap-up
MID · 10 MIN ON YOUR OWN
Task: lecture 3-2 found a square root by bisection. Change the function, keep the loop, give it a name.
```python
cube_root(x, epsilon=1e-6): bracket 0 to x if x >= 1, else 0 to 1; stop when |g³ - x| < epsilon; return g
solve_cos(epsilon=1e-6): the g in [0, 1] with cos(g) = g; math.cos is the only new tool
Both in roots.py; call each with the default and with a keyword argument
```
```python
the REPL
```
```python
>>> import roots
>>> roots.cube_root(27)
3.000000022351742
>>> roots.cube_root(2, epsilon=0.1)
1.25
>>> roots.solve_cos()
0.7390851974487305
```
```python
Think about
Which half still contains the answer? For cos(g) - g: positive means the answer is to the right
epsilon as a parameter with a default, as in lecture 4-1's my_sqrt
No print, no input: the caller decides what to show
```

## Slide 8
Exercise 2: the cube root
```python
roots.py (part 1)
```
```python
"""Roots by approximation, as functions."""
import math


def cube_root(x, epsilon=1e-6):
    """Return the cube root of x >= 0, by bisection."""
    low = 0.0
    high = 1.0 if x < 1 else x
    g = (low + high) / 2
    while abs(g ** 3 - x) >= epsilon:
        if g ** 3 < x:
            low = g
        else:
            high = g
        g = (low + high) / 2
    return g
```
```python
The lecture's loop, one function away
The function: g ** 3 - x in the condition and in the update, where the lecture had g * g - x
The bracket: a conditional expression picks 0 to x or 0 to 1 - the answer must be inside from the start
epsilon has a default: cube_root(27) uses 1e-6; cube_root(2, epsilon=0.1) is deliberately sloppy
```
```python
the REPL
```
```python
>>> import roots
>>> roots.cube_root(27)
3.000000022351742
>>> roots.cube_root(2, epsilon=0.1)
1.25
```

## Slide 9
Exercise 2: cos(x) = x
```python
roots.py (part 2)
```
```python
def solve_cos(epsilon=1e-6):
    """Return the g in [0, 1] with cos(g) = g."""
    low = 0.0
    high = 1.0
    g = (low + high) / 2
    while abs(math.cos(g) - g) >= epsilon:
        if math.cos(g) - g > 0:
            low = g
        else:
            high = g
        g = (low + high) / 2
    return g
```
```python
An equation with no formula
The function: math.cos(g) - g is zero exactly where cos(x) = x
The sign decides: positive at 0, negative at 1, so a positive midpoint means the answer is to the right
No x: the equation is fixed, so epsilon is the only parameter - and it has a default
Keyword arguments: solve_cos(epsilon=0.01) says what the 0.01 is; solve_cos(0.01) works too
```
```python
the REPL
```
```python
>>> roots.solve_cos()
0.7390851974487305
>>> roots.solve_cos(epsilon=0.01)
0.734375
>>> round(roots.solve_cos(), 4)
0.7391
```

## Slide 10
Exercise 3: Design before code
Warm-up
Functions
Roots
Design
Newton
Extra
Wrap-up
MID · 10 MIN ON YOUR OWN
Task: read a day, a month and a year. Is it a real date? If it is, which day of the year is it?
First the design: name the functions, give each a signature and a docstring
Then stubs, so the program runs end to end with wrong answers
Then the bodies, one at a time, each tested in the REPL
February has 29 days in a leap year - exercise 1 already knows which years those are
```python
terminal
```
```python
Day: 29
Month: 2
Year: 2024
Day 60 of 2024

Day: 31
Month: 4
Year: 2026
Not a valid date
```
Think about
A function per question: leap year? days in this month? is the date real? which day of the year?
The day of the year is a sum over the months before it: a loop that calls a function

## Slide 11
The idea: the pieces, then the diagram
Ask what main needs to know, and name a function for each answer.
1 · is_leap(year) - exercise 1, unchanged
2 · days_in(month, year) - 28, 29, 30 or 31; it asks is_leap about February
3 · is_valid_date(day, month, year) - the month is 1 to 12 and the day fits the month
4 · day_of_year(day, month, year) - the days of the months before, plus the day
5 · main - reads three numbers, asks, prints; the only part that prints
The design, written down
main calls is_valid_date and day_of_year
is_valid_date calls days_in
day_of_year calls days_in, in a loop
days_in calls is_leap

every arrow points down; only main prints

## Slide 12
Exercise 3: the stubs
```python
date_design.py (the four stubs)
```
```python
def is_leap(year):
    """Return True for a leap year."""
    return False


def days_in(month, year):
    """Return the days in month (1-12) of year."""
    return 30


def is_valid_date(day, month, year):
    """Return True when the date exists."""
    return True


def day_of_year(day, month, year):
    """Return the day number in the year, 1 to 366."""
    return 0
```
It runs, and it is wrong
Real names, parameters and docstrings - and a placeholder body each
The program runs end to end: the shape is checked before any hard part is written
Day 0 of 2026: wrong, and expected - a stub promises nothing but the shape
Next: fill in one body, run, fill in the next - is_leap first, because days_in needs it
`python date_design.py`
```python
Day: 24
Month: 10
Year: 2026
Day 0 of 2026
```

## Slide 13
Exercise 3: the bodies (1 of 2)
```python
date.py (lines 2-21)
```
```python
def is_leap(year):
    """Return True for a leap year."""
    by_400 = year % 400 == 0
    by_4 = year % 4 == 0 and year % 100 != 0
    return by_400 or by_4


def days_in(month, year):
    """Return the days in month (1-12) of year."""
    if month == 2:
        return 29 if is_leap(year) else 28
    if month == 4 or month == 6 or month == 9 or month == 11:
        return 30
    return 31


def is_valid_date(day, month, year):
    """Return True when the date exists."""
    if month < 1 or month > 12:
        return False
    return 1 <= day <= days_in(month, year)
```
Three bodies, each one job
is_leap: exercise 1, with the two halves of the rule named before they are combined
days_in: three cases with early returns; February asks is_leap, and a conditional expression picks 28 or 29
is_valid_date: a guard on the month first, so days_in is never asked about month 13
Nothing prints: the functions answer; main prints

## Slide 14
Exercise 3: the bodies (2 of 2)
```python
date.py (lines 24-39)
```
```python
def day_of_year(day, month, year):
    """Return the day number in the year, 1 to 366."""
    total = 0
    for m in range(1, month):
        total += days_in(m, year)
    return total + day


day = int(input("Day: "))
month = int(input("Month: "))
year = int(input("Year: "))
if is_valid_date(day, month, year):
    print(f"Day {day_of_year(day, month, year)} of {year}")
else:
    print("Not a valid date")
```
```python
A loop that calls a function
day_of_year: an accumulator over range(1, month) - the months before - plus the day
main is unchanged: the same seven lines as on the stubs slide - the design held
Two calls in main: the guard first, then the answer; both read like the task
```
`python date.py`
```python
Day: 29
Month: 2
Year: 2024
Day 60 of 2024

Day: 24
Month: 10
Year: 2026
Day 297 of 2026
```

## Slide 15
Exercise 4: Newton, with a trace
Warm-up
Functions
Roots
Design
Newton
Extra
Wrap-up
HIGH · 12 MIN ON YOUR OWN
Task: lecture 3-2's Newton found a square root in 3 steps. Do it for the cube root, and watch it work.
```python
cube_root_newton(x, epsilon=1e-6, trace=False): f(g) = g³ - x and f'(g) = 3g², so the next guess is g - (g³ - x) / (3g²)
Start from x / 2 when x > 1, else from 1.0; stop when |g³ - x| < epsilon
trace=True prints the guess after every step; the function still returns g
Count the steps for 27 and for 2 - against bisection's 26 and 20
```
```python
the REPL
```
```python
>>> roots.cube_root_newton(27, trace=True)
step 1: 9.049382716049383
step 2: 6.142823558176272
step 3: 4.333725614685509
step 4: 3.3683535855517652
step 5: 3.0388137235951382
step 6: 3.0004936436555805
step 7: 3.000000081210202
step 8: 3.000000000000002
3.000000000000002
```
Think about
Two defaults, so three ways to call: positional, by keyword, or not at all
A flag may change what is printed, never what is returned

## Slide 16
Exercise 4: one solution
```python
roots.py (part 3)
```
```python
def cube_root_newton(x, epsilon=1e-6, trace=False):
    """Return the cube root of x > 0, by Newton."""
    g = x / 2 if x > 1 else 1.0
    steps = 0
    while abs(g ** 3 - x) >= epsilon:
        g = g - (g ** 3 - x) / (3 * g ** 2)
        steps += 1
        if trace:
            print(f"step {steps}: {g}")
    return g
```
```python
The rule, with one f
The update: g - (g ** 3 - x) / (3 * g ** 2) - the tangent crosses zero there
The start: x / 2 above 1, else 1.0 - never 0, which the update divides by
trace: a parameter with a default of False; the print lives inside if trace:
Two defaults: cube_root_newton(27), (27, trace=True) and (2, 1e-9) are all valid calls
```
```python
the REPL
```
```python
>>> roots.cube_root_newton(2, trace=True)
step 1: 1.3333333333333333
step 2: 1.2638888888888888
step 3: 1.259933493449977
step 4: 1.2599210500177698
1.2599210500177698
```

## Slide 17
Exercise 5: A module and its user
Warm-up
Functions
Roots
Design
Newton
Extra
Wrap-up
MID · 6 MIN ON YOUR OWN
Task: roots.py is a library. Write use_roots.py: a second file that imports it and prints a report.
The cube roots of 27 and 2, the sloppy cube root of 2 (epsilon 0.1), the solution of cos(x) = x, and Newton's cube root of 27
Rounded to 4 digits, one line each - the rounding happens in the user, not in the library
Give roots.py a module docstring, and read one function back with help()
```python
terminal
```
```python
$ python use_roots.py
cube root of 27: 3.0
cube root of 2: 1.2599
sloppy: 1.25
cos(x) = x at 0.7391
newton: 3.0
```
```python
Think about
import roots, then roots.cube_root(27) - module name, dot, function name
The library returns values; the user decides what to show
Run from the folder that holds both files
```

## Slide 18
Exercise 5: the user
`use_roots.py`
```python
import roots

print("cube root of 27:", round(roots.cube_root(27), 4))
print("cube root of 2:", round(roots.cube_root(2), 4))
print("sloppy:", round(roots.cube_root(2, epsilon=0.1), 4))
print("cos(x) = x at", round(roots.solve_cos(), 4))
print("newton:", round(roots.cube_root_newton(27), 4))
```
```python
The caller sees names and promises
import roots, then roots.cube_root(27): the file name without .py, from the same folder; module name, dot, function
The report knows what, not how: nothing about brackets, epsilon or loops appears here
round() in the user: the library returns the full float; the caller chooses the digits
```
`python use_roots.py`
```python
cube root of 27: 3.0
cube root of 2: 1.2599
sloppy: 1.25
cos(x) = x at 0.7391
newton: 3.0
```

## Slide 19
Extra 1: Sequential search, as a function
Warm-up
Functions
Roots
Design
Newton
Extra
Wrap-up
EXTRA
Task: a big increment jumps over the answer, and lecture 3-2's loop never ends. Fix it, inside a function.
```python
sqrt_sequential(x, increment=0.0001, epsilon=0.01): step g up from 1.0 until g² is within epsilon of x (x >= 1)
The guard: stop as well when g has passed x, and return -1.0 to say the increment was too big
Call it with the defaults, with increment 0.01, with increment 0.7, and with all three arguments
```
```python
terminal
```
```python
$ python sqrt_sequential.py
3.9988
4.0
-1.0
1.4139
```
Think about
Two reasons to stop, joined with and; one if after the loop decides which one it was
A returned -1.0 is a signal the caller must test for - say so in the docstring

## Slide 20
Extra 1: one solution
`sqrt_sequential.py`
```python
def sqrt_sequential(x, increment=0.0001, epsilon=0.01):
    """Return a g with g * g near x, stepping up from 1.0;
    -1.0 when the increment jumps over the answer."""
    g = 1.0
    while abs(g * g - x) >= epsilon and g <= x:
        g = g + increment
    if g > x:
        return -1.0
    return g


print(round(sqrt_sequential(16), 4))
print(round(sqrt_sequential(16, increment=0.01), 4))
print(sqrt_sequential(16, increment=0.7))
print(round(sqrt_sequential(2, 0.0001, 0.001), 4))
```
```python
Two ways to stop
The condition: not close enough and g <= x - the second half is the whole fix
After the loop: g > x means the guard fired; the function reports it with -1.0 instead of a root
Two defaults, and a docstring that says both: what comes back normally, and what comes back on failure
```
`python sqrt_sequential.py`
```python
3.9988
4.0
-1.0
1.4139
```

## Slide 21
Recitation summary
Warm-up
Functions
Roots
Design
Newton
Extra
Wrap-up
What we practised
Guess, measure, improve, stop
Bisection needs a bracket; Newton needs the slope; both need a tolerance.
A function per job
One job, a good name, a docstring, tested alone in the REPL.
Design, stubs, bodies
Name the pieces, make it run, then fill in one body at a time - bottom of the diagram first.
A flag changes what is printed, never what is returned
And a library never prints at all: the caller decides.
Tools we used
Approximation
abs(), round(), epsilon, a bracket, the Newton update g - f(g) / f'(g), step counts
Functions
def, return, None, local names, default values, keyword arguments, docstrings, help()
Modules
import roots, roots.cube_root(27), a module docstring, running from the right folder
Patterns
early return, a loop that calls a function, a sentinel value for failure

## Slide 22
Self practice
AT HOME
Write a program for each of these.
gcd
gcd(a, b) returns the greatest common divisor by Euclid's rule: while b is not 0, replace (a, b) by (b, a % b). Test it on 48 and 18.
power
power(x, n) returns x to the n with a loop and multiplication only; compare with ** on ten values, and decide what n = 0 should return.
Perfect numbers
divisor_sum(n) returns the sum of the divisors of n below n; is_perfect(n) uses it. Print the perfect numbers below 10000 from a loop in main.
Newton for cos(x) = x
f(g) = cos(g) - g has slope -sin(g) - 1. Write newton_cos(epsilon=1e-6, trace=False) and count its steps against solve_cos.

## Slide 23
PYTHON COURSE · WEEK 5 · RECITATION 5
Next: Lists, tuples and tables
mutate or return, records, comprehensions, and boards

## From `date.py`

### `date.py`
```python
# The same design, with the bodies filled in
def is_leap(year):
    """Return True for a leap year."""
    by_400 = year % 400 == 0
    by_4 = year % 4 == 0 and year % 100 != 0
    return by_400 or by_4


def days_in(month, year):
    """Return the days in month (1-12) of year."""
    if month == 2:
        return 29 if is_leap(year) else 28
    if month == 4 or month == 6 or month == 9 or month == 11:
        return 30
    return 31


def is_valid_date(day, month, year):
    """Return True when the date exists."""
    if month < 1 or month > 12:
        return False
    return 1 <= day <= days_in(month, year)


def day_of_year(day, month, year):
    """Return the day number in the year, 1 to 366."""
    total = 0
    for m in range(1, month):
        total += days_in(m, year)
    return total + day


day = int(input("Day: "))
month = int(input("Month: "))
year = int(input("Year: "))
if is_valid_date(day, month, year):
    print(f"Day {day_of_year(day, month, year)} of {year}")
else:
    print("Not a valid date")
```

## From `date_design.py`

### `date_design.py`
```python
# The design first: names, parameters, promises
def is_leap(year):
    """Return True for a leap year."""
    return False


def days_in(month, year):
    """Return the days in month (1-12) of year."""
    return 30


def is_valid_date(day, month, year):
    """Return True when the date exists."""
    return True


def day_of_year(day, month, year):
    """Return the day number in the year, 1 to 366."""
    return 0


day = int(input("Day: "))
month = int(input("Month: "))
year = int(input("Year: "))
if is_valid_date(day, month, year):
    print(f"Day {day_of_year(day, month, year)} of {year}")
else:
    print("Not a valid date")
```

## From `gradebook.py`

### `gradebook.py`
```python
students = [("Dana Levi", 88),
            ("Ron Cohen", 95),
            ("Omer Katz", 51),
            ("Yael Bar", 73)]

def top_student(students):
    """Return the record with the top grade."""
    best = students[0]
    for record in students:
        if record[1] > best[1]:
            best = record
    return best

def failing(students, pass_mark=56):
    """Return the names below pass_mark."""
    names = []
    for name, grade in students:
        if grade < pass_mark:
            names.append(name)
    return names

def curve(students, points):
    """New records, points added, max 100."""
    curved = []
    for name, grade in students:
        new_grade = min(grade + points, 100)
        curved.append((name, new_grade))
    return curved

def add_student(students, name, grade):
    """Add one record, in place."""
    students.append((name, grade))

add_student(students, "Noa Peretz", 64)
name, grade = top_student(students)
print(f"Top: {name} with {grade}")
print(f"Failing: {failing(students)}")
print(f"Curved: {curve(students, 10)}")
```

## From `negatives.py`

### `negatives.py`
```python
def remove_negatives(nums):
    """Remove the negatives, in place."""
    i = 0
    while i < len(nums):
        if nums[i] < 0:
            nums.pop(i)
        else:
            i += 1

def without_negatives(nums):
    """Return a new list, negatives dropped."""
    kept = []
    for x in nums:
        if x >= 0:
            kept.append(x)
    return kept
```

## From `noa.py`

### `noa.py`
```python
def cleaned(nums):
    i = 0
    while i < len(nums):
        if nums[i] < 0:
            nums.pop(i)
        else:
            i += 1
    return nums
```

## From `permutations.py`

### `permutations.py`
```python
def is_permutation(per):
    """True if per holds each of 0..n-1 once."""
    n = len(per)
    seen = [False] * n
    for value in per:
        if value < 0 or value >= n:
            return False
        if seen[value]:
            return False
        seen[value] = True
    return True

def inverse(per):
    """Return the permutation undoing per."""
    inv = [0] * len(per)
    for i in range(len(per)):
        inv[per[i]] = i
    return inv
```

## From `report.py`

### `report.py`
```python
def read_numbers():
    """Return the ints typed on one line."""
    nums = []
    for piece in input("Numbers: ").split():
        nums.append(int(piece))
    return nums

def average(nums):
    """Return the average, 0.0 if empty."""
    if len(nums) == 0:
        return 0.0
    return sum(nums) / len(nums)

def count_above(nums, limit):
    """Return how many are above limit."""
    count = 0
    for x in nums:
        if x > limit:
            count += 1
    return count

nums = read_numbers()
if len(nums) == 0:
    print("No numbers")
else:
    mean = average(nums)
    print(f"Largest: {max(nums)}")
    print(f"Smallest: {min(nums)}")
    print(f"Average: {round(mean, 2)}")
    above = count_above(nums, mean)
    print(f"Above average: {above}")
```

## From `report_stubs.py`

### `report_stubs.py`
```python
def read_numbers():
    """Return the ints typed on one line."""
    return []

def average(nums):
    """Return the average, 0.0 if empty."""
    return 0.0

def count_above(nums, limit):
    """Return how many are above limit."""
    return 0

nums = read_numbers()
print(f"Largest: {max(nums)}")
print(f"Smallest: {min(nums)}")
```

## From `roots.py`

### `roots.py`
```python
"""Roots by approximation, as functions."""
import math


def cube_root(x, epsilon=1e-6):
    """Return the cube root of x >= 0, by bisection."""
    low = 0.0
    high = 1.0 if x < 1 else x
    g = (low + high) / 2
    while abs(g ** 3 - x) >= epsilon:
        if g ** 3 < x:
            low = g
        else:
            high = g
        g = (low + high) / 2
    return g


def solve_cos(epsilon=1e-6):
    """Return the g in [0, 1] with cos(g) = g."""
    low = 0.0
    high = 1.0
    g = (low + high) / 2
    while abs(math.cos(g) - g) >= epsilon:
        if math.cos(g) - g > 0:
            low = g
        else:
            high = g
        g = (low + high) / 2
    return g


def cube_root_newton(x, epsilon=1e-6, trace=False):
    """Return the cube root of x > 0, by Newton."""
    g = x / 2 if x > 1 else 1.0
    steps = 0
    while abs(g ** 3 - x) >= epsilon:
        g = g - (g ** 3 - x) / (3 * g ** 2)
        steps += 1
        if trace:
            print(f"step {steps}: {g}")
    return g
```

## From `small_functions.py`

### `small_functions.py`
```python
def is_leap(year):
    """Return True when year is a leap year."""
    by_400 = year % 400 == 0
    by_4 = year % 4 == 0 and year % 100 != 0
    return by_400 or by_4


def digit_sum(n):
    """Return the sum of the digits of n (n >= 0)."""
    total = 0
    while n > 0:
        total += n % 10
        n = n // 10
    return total


def count_vowels(text):
    """Return how many vowels text contains."""
    count = 0
    for ch in text.lower():
        if ch in "aeiou":
            count += 1
    return count
```

## From `sqrt_sequential.py`

### `sqrt_sequential.py`
```python
def sqrt_sequential(x, increment=0.0001, epsilon=0.01):
    """Return a g with g * g near x, stepping up from 1.0;
    -1.0 when the increment jumps over the answer."""
    g = 1.0
    while abs(g * g - x) >= epsilon and g <= x:
        g = g + increment
    if g > x:
        return -1.0
    return g


print(round(sqrt_sequential(16), 4))
print(round(sqrt_sequential(16, increment=0.01), 4))
print(sqrt_sequential(16, increment=0.7))
print(round(sqrt_sequential(2, 0.0001, 0.001), 4))
```

## From `text_report.py`

### `text_report.py`
```python
import textstats

text = "a rose is a rose is a rose"
print("Words:", textstats.word_count(text))
print("Longest:", textstats.longest_word(text))
print("Unique:", textstats.unique_words(text))
print("Top:", textstats.most_common(text))
```

## From `textstats.py`

### `textstats.py`
```python
"""Small text statistics."""

def words_of(text):
    """Return the lowercase words of text."""
    return text.lower().split()

def word_count(text):
    """Return how many words text has."""
    return len(words_of(text))

def longest_word(text):
    """Return the first longest word."""
    longest = ""
    for w in words_of(text):
        if len(w) > len(longest):
            longest = w
    return longest

def unique_words(text):
    """Return the distinct words, in order."""
    seen = []
    for w in words_of(text):
        if w not in seen:
            seen.append(w)
    return seen

def most_common(text):
    """Return (word, count) of the top word."""
    words = words_of(text)
    best = ("", 0)
    for w in unique_words(text):
        count = words.count(w)
        if count > best[1]:
            best = (w, count)
    return best
```

## From `use_roots.py`

### `use_roots.py`
```python
import roots

print("cube root of 27:", round(roots.cube_root(27), 4))
print("cube root of 2:", round(roots.cube_root(2), 4))
print("sloppy:", round(roots.cube_root(2, epsilon=0.1), 4))
print("cos(x) = x at", round(roots.solve_cos(), 4))
print("newton:", round(roots.cube_root_newton(27), 4))
```

## From `using_noa.py`

### `using_noa.py`
```python
from noa import cleaned

scores = [3, -1, 4, -5, 9]
good = cleaned(scores)
print(good)
print(scores)
good.append(100)
print(scores)
```

## From `warmup_bisection.py`

### `warmup_bisection.py`
```python
# Bisection (lecture 3-2), for x = 10
x = 10
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

## From `warmup_functions.py`

### `warmup_functions.py`
```python
def double(x):
    return 2 * x
def shout(word):
    print(word.upper())

a = double(4)
b = shout("hi")
print(a, b)
print(double(double(3)))
x = 10
def change():
    x = 5
change()
print(x)
```

## From `warmup_lists.py`

### `warmup_lists.py`
```python
a = [1, 2, 3]
b = a
b.append(4)
print(a)
c = a[:]
c[0] = 99
print(a, c)
print(a.sort())
print(a)
t = (1, 2)
x, y = t
print(y, x)
print([1, 2] + [3], [0] * 3)
```
