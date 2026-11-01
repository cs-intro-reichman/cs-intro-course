# Week 2 code files

The code files shown in the week 2 lectures.

### `a.py`
```python
# lecture 2-1 — a.py
i = 0
while i < 4:
    i += 1

# four passes: i takes 0, 1, 2, 3 and ends at 4
```

### `abs_value.py`
```python
# lecture 2-1 — abs_value.py
x = int(input("Enter a number: "))
if x < 0:
    x = -x
print("Absolute value:", x)

# $ python abs_value.py
# Enter a number: -12
# Absolute value: 12
```

### `augmented.py`
```python
# lecture 2-1 — augmented.py
count = 0      # a sample value, so the file runs on its own
count = count + 1     # what we wrote
count += 1            # the same thing

# count = count + 1 and count += 1 are the same instruction.
```

### `b.py`
```python
# lecture 2-1 — b.py
i = 0
while i <= 4:
    i += 1

# five passes: i takes 0, 1, 2, 3, 4 and ends at 5
```

### `bug_reinit.py`
```python
# lecture 2-1 — bug_reinit.py
n = int(input("n: "))
i = 0
while i < n:
    total = 0
    total += i
    i += 1
print(total)

# total = 0 sits inside the body, so each pass throws away the sum so far.
# With n = 4 the loop ends with total = 3, not 6.
```

### `bug_updates.py`
```python
# lecture 2-1 — bug_updates.py
n = 3
while n > 0:
    print(n)
n -= 1

# The update is outside the loop body, so n never reaches 0: the program prints 3
# for ever, and the line after the loop is never reached.
```

### `builtin.py`
```python
# lecture 2-2 — builtin.py
x = 26
print(bin(x))      # 0b11010

s = "11010"
print(int(s, 2))   # 26

# what the hand-written conversions do, in one call each
```

### `chained.py`
```python
# lecture 2-1 — chained.py
grade = 87          # a sample value, so the file runs on its own

if 0 <= grade <= 100:
    print("Valid grade")

# 0 <= grade <= 100 is one comparison, not two.
```

### `chained_if.py`
```python
# lecture 2-1 — chained_if.py
a = 5          # sample values, so the file runs on its own
b = 3

if a == b:
    print("a equals b")
if a > b:
    print("a is greater")
if a < b:
    print("b is greater")

# three independent ifs: every test runs, every time.
```

### `coin_flip.py`
```python
# lecture 2-1 — coin_flip.py
import random

if random.random() < 0.5:
    print("Heads")
else:
    print("Tails")

# if-else: exactly one of the two branches runs. Run it four or five times.
```

### `condition.py`
```python
# lecture 2-1 — condition.py
score = 72          # sample values, so the file runs on its own
attendance = 0.9

if score >= 60 and attendance >= 0.8:
    print("Pass")

# a condition is any expression with a True/False value.
```

### `correct.py`
```python
# lecture 2-1 — correct.py
n = int(input("n: "))
i = 0
total = 0
while i < n:
    total += i
    i += 1
print(total)

# total = 0 before the loop, so the sum survives every pass. n = 4 gives 6.
```

### `count_letter.py`
```python
# lecture 2-2 — count_letter.py
word = input("Enter a word: ")
target = input("Enter a letter to count: ")

count = 0
for ch in word:
    if ch == target:
        count += 1

print(target, "appears", count, "times in", word)

# banana, a -> a appears 3 times in banana
```

### `count_up.py`
```python
# lecture 2-1 — count_up.py
n = int(input())
count = 0
while count < n:
    print(count)
    count = count + 1

# the running while example: initialize, condition, update. n = 3 prints 0 1 2.
```

### `count_up_for.py`
```python
# lecture 2-2 — count_up_for.py
for i in [0,1,2,3,4]:
    print(i)

# the same five lines, with no counter to maintain
```

### `count_up_while.py`
```python
# lecture 2-2 — count_up_while.py
i = 0
while i < 5:
    print(i)
    i += 1

# 0 1 2 3 4, one per line
```

### `digit_sum.py`
```python
# lecture 2-1 — digit_sum.py
n = int(input("Number: "))
total = 0
while n > 0:
    digit = n % 10
    total += digit
    n = n // 10    # or n //= 10
print("Digit sum:", total)

# $ python digit_sum.py
# Number: 4071
# Digit sum: 12
```

### `elif.py`
```python
# lecture 2-1 — elif.py
a = 5          # sample values, so the file runs on its own
b = 3

if a == b:
    print("a equals b")
elif a > b:
    print("a is greater")
else:
    print("b is greater")

# the same flow as the nested if, with flat indentation.
```

### `expression.py`
```python
# lecture 2-1 — expression.py
a = 4          # sample values, so the file runs on its own
b = 9

max_val = a if a >= b else b
print(max_val)

# the conditional expression: an if/else that has a value.
```

### `factorial.py`
```python
# lecture 2-2 — factorial.py
n = int(input("n: "))
factorial = 1
for i in range(1, n + 1):
    factorial *= i
print(factorial)

# n = 5 gives 120. factorial = 1, not 0: zero would annihilate the product.
```

### `fixed.py`
```python
# lecture 2-1 — fixed.py
n = 3
while n > 0:
    print(n)
    n -= 1

# the update back inside the block, so n reaches 0 and the loop ends: 3, 2, 1.
```

### `gamblers_ruin.py`
```python
# lecture 2-2 — gamblers_ruin.py
import random

start = int(input("Starting cash: "))
goal  = int(input("Goal: "))
T     = int(input("Number of games: "))

n_wins = 0
n_flips = 0

for t in range(T):                    # repeat the experiment T times
    cash = start
    while 0 < cash < goal:            # play one game until ruin or goal
        if random.random() < 0.5:
            cash += 1
        else:
            cash -= 1
        n_flips += 1
    if cash == goal:
        n_wins += 1

print("Percentage of winning games:", 100 * n_wins / T, "%")
print("Average number of flips per game:", n_flips / T)

# the whole simulation: a while loop for one game, a for loop over the games.
```

### `harmonic.py`
```python
# lecture 2-2 — harmonic.py
n = int(input("n: "))
total = 0.0
for i in range(1, n + 1):
    total += 1 / i
print(total)

# n = 4 gives 2.083333333333333. The .0 states that the result is a float.
```

### `infinite.py`
```python
# lecture 2-1 — infinite.py
# Slide 27 shows this code without the comment and asks what happens.
count = 10
while count > 0:
    print(count)
    count += 1   # wrong way

# 10  11  12  13  14  ...
# KeyboardInterrupt
#
# The stopping condition is count > 0 and every pass makes count larger, so
# the condition never becomes False. Ctrl-C is the only way out.
```

### `left.py`
```python
# lecture 2-2 — left.py
n = int(input("n: "))
for row in range(1, n + 1):
    for star in range(row):
        print("*", end="")
    print()

# n = 4 gives *, **, ***, **** - the inner bound depends on the outer variable
```

### `letters.py`
```python
# lecture 2-2 — letters.py
for ch in "binary":
    print(ch)

# b i n a r y, one per line - a string is a sequence of characters
```

### `lines.py`
```python
# lecture 2-2 — lines.py
for count in range(100):
    print("I will not argue ...")

# the same line 100 times; count is never read inside the body
```

### `many_games.py`
```python
# lecture 2-2 — many_games.py
import random

start = int(input("Starting cash: "))
goal  = int(input("Goal: "))

n_wins = 0

T = 100
for t in range(T):
    cash = start
    while 0 < cash < goal:
        if random.random() < 0.5:
            cash += 1
        else:
            cash -= 1
    if cash == goal:
        n_wins += 1
# calculate winning games percentage
print(f"Percentage of winning games: {n_wins * 100 / T}%")

# The right-hand card of slide 40, written out in full: the outer loop of the card
# with the inner game of one_game.py in place of its `# ... one game ...` line, so
# the card really runs. 50 -> 250 reaches the goal about one game in five; change
# T for a different estimate.
```

### `max_v1.py`
```python
# lecture 2-1 — max_v1.py
x = 4          # sample values, so the file runs on its own
y = 9

# 1 — symmetric
if x >= y:
    max_val = x
else:
    max_val = y
print(max_val)
```

### `max_v2.py`
```python
# lecture 2-1 — max_v2.py
x = 4          # sample values, so the file runs on its own
y = 9

# 2 — assume, then correct
max_val = x
if y > max_val:
    max_val = y
print(max_val)
```

### `missing_colon.py`
```python
# lecture 2-1 — missing_colon.py
# This file does not run. Add the colon at the end of line 4 and it does.
x = -5
if x < 0
    x = -x
print("Absolute value:", x)

#   File "missing_colon.py", line 4
#     if x < 0
#             ^
# SyntaxError: expected ':'
```

### `missing_indent.py`
```python
# lecture 2-1 — missing_indent.py
# This file does not run. Indent line 5 and it does.
x = 5
if x > 0:
print("x is positive")

#   File "missing_indent.py", line 5
#     print("x is positive")
#     ^
# IndentationError: expected an indented block after 'if' statement on line 4
```

### `names.py`
```python
# lecture 2-2 — names.py
for name in ["Messi", "Ronaldo", "Neymar"]:
    print("Hello,", name)

# Hello, Messi / Hello, Ronaldo / Hello, Neymar
```

### `nested_for.py`
```python
# lecture 2-2 — nested_for.py
for i in range(3):
    for j in range(3):
        print("*", end="")
    print()

# the same three rows - range() re-counts j by itself on every outer pass
```

### `nested_if.py`
```python
# lecture 2-1 — nested_if.py
a = 5          # sample values, so the file runs on its own
b = 3

if a == b:
    print("a equals b")
else:
    if a > b:
        print("a is greater")
    else:
        print("b is greater")

# nested ifs: the second test runs only if the first failed.
```

### `nested_while.py`
```python
# lecture 2-2 — nested_while.py
i = 0
while i < 3:
    j = 0   # forget this
    while j < 3:
        print("*", end="")
        j += 1
    print()
    i += 1

# *** three times. Drop the j = 0 line and rows 2 and 3 come out empty.
```

### `no_effect.py`
```python
# lecture 2-2 — no_effect.py
for i in range(5):
    print(i, end=" ")
    i = 10
    print(i)

# 0 10 / 1 10 / 2 10 / 3 10 / 4 10 - the loop rebinds i at the top of every pass
```

### `one_game.py`
```python
# lecture 2-2 — one_game.py
cash = start
while 0 < cash < goal:
    if random.random() < 0.5:
        cash += 1
    else:
        cash -= 1
    n_flips += 1

# the inner loop of gamblers_ruin.py: one game, length unknown in advance.
```

### `plural.py`
```python
# lecture 2-1 — plural.py
count = 3
word = "items" if count > 1 else "item"
print(f"You bought {count} {word}")

# $ python plural.py
# You bought 3 items
```

### `point.py`
```python
# lecture 2-1 — point.py
import random

while True:
    # generate random x,y in [-1,1)
    x = 2.0 * random.random() - 1.0
    y = 2.0 * random.random() - 1.0
    if x**2 + y**2 <= 1.0:
        break
print("Inside:", x, y)
```

### `powers.py`
```python
# lecture 2-1 — powers.py
n = int(input("n: "))
i = 0
v = 1
while i <= n:
    print(i, v)
    i += 1
    v *= 2

# $ python powers.py
# n: 6
# 0 1
# 1 2
# 2 4
# 3 8
# 4 16
# 5 32
# 6 64
```

### `powers_a.py`
```python
# lecture 2-2 — powers_a.py
n = int(input("n: "))
for i in range(n + 1):
    print(i, 2 ** i)

# the power is rebuilt from nothing on every pass
```

### `powers_b.py`
```python
# lecture 2-2 — powers_b.py
n = int(input("n: "))
v = 1
for i in range(n + 1):
    print(i, v)
    v *= 2

# the same output, carrying the previous value forward: one multiplication per pass
```

### `quadratic.py`
```python
# lecture 2-1 — quadratic.py
import math

a = 1
b = 1
c = 2

d = b * b - 4.0 * a * c
if d < 0.0:
    print("No real roots")
else:
    root = math.sqrt(d)
    print("x1 =", (-b + root) / (2*a))
    print("x2 =", (-b - root) / (2*a))

# a guard condition: test the discriminant before taking its root.
```

### `self_practice.txt`
```
lecture 2-1, slide 41 - self practice

Write a program that prints each of these. The outer structure never changes;
only the number of stars per row, and where the row starts.

square          left            right           centered

***             *                 *               *
***             **               **             ***
***             ***             ***            *****
```

### `smallest.py`
```python
# lecture 2-1 — smallest.py
x = int(input("Number (-1 to finish): "))
smallest = x
while x != -1:
    if x < smallest:
        smallest = x
    x = int(input("Number (-1 to finish): "))
if smallest == -1:
    print("No numbers were entered.")
else:
    print("Smallest:", smallest)

# a sample session:
# Number (-1 to finish): 4
# Number (-1 to finish): 9
# Number (-1 to finish): 2
# Number (-1 to finish): 7
# Number (-1 to finish): -1
# Smallest: 2

# and with nothing entered at all:
# Number (-1 to finish): -1
# No numbers were entered.
```

### `square.py`
```python
# lecture 2-1 — square.py
i = 0
while i < 3:
    j = 0
    while j < 3:
        print("*", end="")
        j += 1
    print()
    i += 1

# $ python square.py
# ***
# ***
# ***
#
# j is set to 0 inside the outer body, so it starts again at 0 on every row.
```

### `statement.py`
```python
# lecture 2-1 — statement.py
a = 4          # sample values, so the file runs on its own
b = 9

if a > b:
    max_val = a
else:
    max_val = b
print(max_val)

# the same choice written as a statement rather than an expression.
```

### `sum.py`
```python
# lecture 2-2 — sum.py
n = int(input("n: "))
total = 0
for i in range(1, n + 1):
    total += i
print(total)

# n = 4 gives 1 + 2 + 3 + 4 = 10
```

### `tax_v1.py`
```python
# lecture 2-1 — tax_v1.py
income = int(input("Income: "))
if income <= 5280:
    rate = 0.10
else:
    if income <= 9010:
        rate = 0.14
    else:
        if income <= 14000:
            rate = 0.21
        else:
            if income <= 20000:
                rate = 0.31
            else:
                rate = 0.34
print("rate:", rate)

# tax brackets as nested ifs: every level pushes the code further right.
```

### `tax_v2.py`
```python
# lecture 2-1 — tax_v2.py
income = int(input("Income: "))
if income <= 5280:
    rate = 0.10
elif income <= 9010:
    rate = 0.14
elif income <= 14000:
    rate = 0.21
elif income <= 20000:
    rate = 0.31
else:
    rate = 0.34
print("rate:", rate)

# the same brackets as an if-elif-else chain, which stays flat.
```

### `times_table.py`
```python
# lecture 2-2 — times_table.py
n = int(input("n: "))
for i in range(1, n + 1):
    for j in range(1, n + 1):
        print(i * j, end="\t")
    print()

# n = 3 gives three rows of three products
```

### `to_binary.py`
```python
# lecture 2-2 — to_binary.py
x = int(input("n (>= 0): "))
s = ""
while x > 0:
    s = str(x % 2) + s
    x = x // 2
print(s)

# 26 -> 11010. For x = 0 it prints nothing: see to_binary_fixed.py
```

### `to_binary_fixed.py`
```python
# lecture 2-2 — to_binary_fixed.py
x = int(input("n (>= 0): "))
s = ""
if x == 0:
    s = "0"
else:
    while x > 0:
        s = str(x % 2) + s
        x = x // 2
print(s)

# 26 -> 11010,  0 -> 0. Zero is the one non-negative integer with no digits to peel.
```

### `to_decimal.py`
```python
# lecture 2-2 — to_decimal.py
s = input("Binary number: ")
value = 0
for ch in s:
    value = value * 2 + int(ch)
print(value)

# 11010 -> 26. Everything so far is worth twice as much, plus this digit.
```

### `to_decimal_safe.py`
```python
# lecture 2-2 — to_decimal_safe.py
s = input("Binary number: ")
value = 0
valid = True
for ch in s:
    if ch != "0" and ch != "1":
        valid = False
        break
    value = value * 2 + int(ch)
if valid:
    print(value)
else:
    print("Not a binary number.")

# 11010 -> 26,  1021 -> Not a binary number.  The loop discovers, the code after it acts.
```

### `validate.py`
```python
# lecture 2-1 — validate.py
grade = int(input("Grade (0-100): "))
while not (0 <= grade <= 100):
    print("That is not a valid grade.")
    grade = int(input("Grade (0-100): "))
print("Grade recorded:", grade)

# input validation: the read is written twice, before and inside the loop.
```

### `validate_break.py`
```python
# lecture 2-1 — validate_break.py
while True:
    grade = int(input("Grade (0-100): "))
    if 0 <= grade <= 100:
        break
    print("That is not a valid grade.")
print("Grade recorded:", grade)

# the same validation with while True and a break, so the read is written once.
```

### `version_a.py`
```python
# lecture 2-1 — version_a.py
# Block includes print statement
x = -5         # a sample value, so the file runs on its own
if x < 0:
    x = -x
    print("negative")
```

### `version_b.py`
```python
# lecture 2-1 — version_b.py
# Block ends before print statement
x = -5         # a sample value, so the file runs on its own
if x < 0:
    x = -x
print("done")
```
