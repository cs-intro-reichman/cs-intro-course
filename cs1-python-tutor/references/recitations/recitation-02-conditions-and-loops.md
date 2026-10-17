# Recitation, week 2: Conditions and loops

## From `recitation 2.pptx`

## Slide 1
```python
while
```
PYTHON COURSE · WEEK 2 · RECITATION 2
Recitation 2
Conditions and loops

## Slide 2
Recitation overview
Warm-up
Conditions
while
for
Monte Carlo
Extra
Wrap-up
1
Loop predictions
how many lines, and why
2
Conditions
elif, order, and a one-line if
3
while
games that stop when something happens
4
for and range
count, accumulate, nest

## Slide 3
Warm-up: how many lines?
Warm-up
Conditions
while
for
Monte Carlo
Extra
Wrap-up
WARM-UP · 4 MIN
One character apart. How many lines does each print, and what is i after?
`warmup_loops_1.py`
```python
# A
i = 0
while i < 5:
    print(i)
    i += 1

# B
i = 0
while i <= 5:
    print(i)
    i += 1
```
The answers
A: 5 lines, 0 to 4, and i ends at 5
B: 6 lines, 0 to 5, and i ends at 6
Neither is wrong: using one when you meant the other is the bug

## Slide 4
Warm-up: what goes wrong?
WARM-UP · 4 MIN
Two more. Each has one of the classic loop bugs. Which, and what is printed?
`warmup_loops_2.py`
```python
# C
i = 0
while i < 5:
    print(i)
i += 1

# D
total = 0
for i in range(1, 4):
    total = 0
    total += i
print(total)
```
The answers
C: prints 0 forever - the update sits outside the body. Ctrl-C stops it
D: prints 3, not 6 - total is reset to 0 on every pass
Read the indentation, not the intention

## Slide 5
Warm-up: range
WARM-UP · 2 MIN
Four loops with for. Write the four lines they print.
`warmup_range.py`
```python
for i in range(2, 11, 3):
    print(i, end=" ")
print()
for i in range(5, 0, -2):
    print(i, end=" ")
print()
for ch in "abc":
    print(ch * 2, end=" ")
print()
for i in range(3, 3):
    print("never")
print("done")
```
```python
The answers
2 5 8
5 3 1
aa bb cc
done (the empty range runs 0 times)
```

## Slide 6
Exercise 1: Ticket price
Warm-up
Conditions
while
for
Monte Carlo
Extra
Wrap-up
EASY · 7 MIN ON YOUR OWN
Task: a cinema charges by age. Read an age and print the price.
Under 5: free. 5 to 17: 20. 18 to 64: 40. 65 and up: 25
One if-elif-else chain, with the tests in an order that works
Print 'Free' for a price of 0, using the conditional expression (one line)
```python
terminal
```
```python
Age: 3
Free

Age: 70
Price: 25
```
```python
Think about
An elif chain stops at the first True test
x if condition else y is a value: assign it, print it
```

## Slide 7
Exercise 1: one solution
`ticket.py`
```python
age = int(input("Age: "))

if age < 5:
    price = 0
elif age < 18:
    price = 20
elif age < 65:
    price = 40
else:
    price = 25

msg = f"Price: {price}"
print("Free" if price == 0 else msg)
```
```python
Reading the chain
Each test assumes the earlier ones failed: age < 18 only runs for ages 5 and up, so it means 5 to 17
The else: whoever is left - 65 and up
A value, not a statement: the conditional expression picks one of two strings to print
```
`python ticket.py`
```python
Age: 17
Price: 20
```

## Slide 8
Alice reordered the tests. Same result?
Alice tested the biggest group first. Same result for every age?
```python
ticket.py (ours)
```
```python
if age < 5:
    price = 0
elif age < 18:
    price = 20
elif age < 65:
    price = 40
else:
    price = 25
```
`ticket_alice.py`
```python
if age < 65:
    price = 40
elif age < 18:
    price = 20
elif age < 5:
    price = 0
else:
    price = 25
```
```python
No. A three-year-old passes age < 65 first and pays 40. The later tests never run.
Rule: most specific test first, or make every test exclusive: 5 <= age < 18.
```

## Slide 9
Exercise 2: Guess the number
Warm-up
Conditions
while
for
Monte Carlo
Extra
Wrap-up
MID · 10 MIN ON YOUR OWN
Task: the computer picks a secret number from 1 to 100. The player guesses until it is found.
After every guess print Higher, Lower or Correct
A guess outside 1 to 100 is refused with a message and does not count
At the end, print how many valid tries it took
```python
terminal
```
```python
Guess: 50
Higher
Guess: 200
Between 1 and 100, please
Guess: 62
Correct in 2 tries
```
```python
Think about
Rounds unknown in advance: while True and break when it is found
The secret: int(random.random() * 100) + 1, a 100-sided die
```

## Slide 10
Exercise 2: one solution
`guess.py`
```python
import random
secret = int(random.random() * 100) + 1
tries = 0
while True:
    guess = int(input("Guess: "))
    if guess < 1 or guess > 100:
        print("Between 1 and 100, please")
    else:
        tries += 1
        if guess < secret:
            print("Higher")
        elif guess > secret:
            print("Lower")
        else:
            print(f"Correct in {tries} tries")
            break
```
```python
The shape of the loop
while True: the exit is in the middle of the body, where the answer is known
The invalid branch first: it counts nothing and asks again
Nested if: inside the else, the three valid cases; tries is bumped once, before them
break: ends the loop at once; the header never becomes False
```

## Slide 11
Exercise 2: the run
`guess.py`
```python
import random
secret = int(random.random() * 100) + 1
tries = 0
while True:
    guess = int(input("Guess: "))
    if guess < 1 or guess > 100:
        print("Between 1 and 100, please")
    else:
        tries += 1
        if guess < secret:
            print("Higher")
        elif guess > secret:
            print("Lower")
        else:
            print(f"Correct in {tries} tries")
            break
```
`python guess.py`
```python
Guess: 50
Higher
Guess: 75
Lower
Guess: 62
Correct in 3 tries
```

## Slide 12
Exercise 2, expansion: the computer guesses
`computer_guesses.py`
```python
low = 1
high = 100
rounds = 0
while True:
    guess = (low + high) // 2
    rounds += 1
    answer = input(f"Is it {guess}? (h/l/c) ")
    if answer == "c":
        print(f"Got it in {rounds} rounds")
        break
    elif answer == "h":
        low = guess + 1
    else:
        high = guess - 1
```
Roles reversed
You think of a number; the computer guesses the middle of what is left
h means 'higher than that', l means 'lower', c means 'correct'
Halving: every answer throws away half the range - at most 7 rounds for 1 to 100
Bisection in disguise: lecture 3-2 will do this to find a square root

## Slide 13
Exercise 3: The 3n + 1 game
Warm-up
Conditions
while
for
Monte Carlo
Extra
Wrap-up
MID · 10 MIN ON YOUR OWN
Task: start from n. If n is even, halve it; if it is odd, make it 3n + 1. Stop at 1. Count the steps.
6 -> 3 -> 10 -> 5 -> 16 -> 8 -> 4 -> 2 -> 1: eight steps
Read n, print the sequence on one line, then the number of steps
Nobody has proved that every n reaches 1 - but every n ever tried does
```python
terminal
```
```python
n: 6
6 3 10 5 16 8 4 2 1
8 steps
```
```python
Think about
A loop that runs until a condition is met: while n != 1
Even or odd: n % 2 == 0
One accumulator counts the steps
```

## Slide 14
Exercise 3: one solution
`collatz.py`
```python
n = int(input("n: "))

steps = 0
while n != 1:
    print(n, end=" ")
    if n % 2 == 0:
        n = n // 2
    else:
        n = 3 * n + 1
    steps += 1
print(n)
print(f"{steps} steps")
```
```python
Reading the loop
The condition: n != 1 - the loop ends when n becomes 1, however long that takes
Two updates: exactly one of the two branches changes n on every pass
The last 1: printed after the loop, because the body never sees n == 1
n // 2, not n / 2: keep n an int, or 3.0 appears in the output
```

## Slide 15
Exercise 3: the run
`collatz.py`
```python
n = int(input("n: "))

steps = 0
while n != 1:
    print(n, end=" ")
    if n % 2 == 0:
        n = n // 2
    else:
        n = 3 * n + 1
    steps += 1
print(n)
print(f"{steps} steps")
```
`python collatz.py`
```python
n: 6
6 3 10 5 16 8 4 2 1
8 steps
```

## Slide 16
Exercise 3, expansion: the longest chain
`longest_chain.py`
```python
best_start = 1
best_steps = 0
for start in range(1, 100):
    n = start
    steps = 0
    while n != 1:
        if n % 2 == 0:
            n = n // 2
        else:
            n = 3 * n + 1
        steps += 1
    if steps > best_steps:
        best_steps = steps
        best_start = start
print(f"{best_start} takes {best_steps} steps")
```
```python
A loop inside a loop
The outer for tries every start below 100; the inner while runs one chain
Reset per start: n = start and steps = 0 belong inside the outer loop
Running maximum: remember the best so far, and which start produced it
Answer: 97 takes 118 steps
```
`python longest_chain.py`
```python
97 takes 118 steps
```

## Slide 17
Exercise 4: Patterns
Warm-up
Conditions
while
for
Monte Carlo
Extra
Wrap-up
MID · 10 MIN ON YOUR OWN
Task: read a size n and print two patterns with nested loops.
A hollow square: stars on the border, spaces inside
A checkerboard: # and . alternating, every row shifted by one
Each cell is one print(..., end=""); one bare print() ends a row
```python
terminal
```
```python
n: 5
*****   #.#.#
*   *   .#.#.
*   *   #.#.#
*   *   .#.#.
*****   #.#.#
```
Think about
Which cells are on the border? Think about i and j, not about the picture
On the checkerboard, what do all the # cells have in common? Add i and j

## Slide 18
Exercise 4: the hollow square
`hollow_square.py`
```python
n = int(input("n: "))

for i in range(n):
    for j in range(n):
        on_row = i == 0 or i == n - 1
        on_col = j == 0 or j == n - 1
        if on_row or on_col:
            print("*", end="")
        else:
            print(" ", end="")
    print()
```
```python
A cell is a pair (i, j)
The visit: two loops reach every cell once, row by row
The border: first or last row, or first or last column - two booleans, joined by or
The row: end="" keeps the cells on one line; the bare print() ends it
Try n = 1 and n = 2: every cell is on the border
```

## Slide 19
Exercise 4: the run
`hollow_square.py`
```python
n = int(input("n: "))

for i in range(n):
    for j in range(n):
        on_row = i == 0 or i == n - 1
        on_col = j == 0 or j == n - 1
        if on_row or on_col:
            print("*", end="")
        else:
            print(" ", end="")
    print()
```
`python hollow_square.py`
```python
n: 5
*****
*   *
*   *
*   *
*****
```

## Slide 20
Exercise 4: the checkerboard
`checkerboard.py`
```python
n = int(input("n: "))

for i in range(n):
    for j in range(n):
        if (i + j) % 2 == 0:
            print("#", end="")
        else:
            print(".", end="")
    print()
```
```python
Parity of i + j
Same skeleton: two loops, one if per cell, one bare print() per row
The test: a # where i + j is even - one step in any direction flips the parity
Why it works: neighbours differ by one in i or in j, never in both
Your turn: swap the two characters without touching the condition
```

## Slide 21
Exercise 4: the run
`checkerboard.py`
```python
n = int(input("n: "))

for i in range(n):
    for j in range(n):
        if (i + j) % 2 == 0:
            print("#", end="")
        else:
            print(".", end="")
    print()
```
`python checkerboard.py`
```python
n: 5
#.#.#
.#.#.
#.#.#
.#.#.
#.#.#
```

## Slide 22
Exercise 5: Darts and pi
Warm-up
Conditions
while
for
Monte Carlo
Extra
Wrap-up
HIGH · 12 MIN ON YOUR OWN
Task: throw N random points into the square [-1, 1) x [-1, 1). Count how many land inside the unit circle.
The circle covers pi/4 of the square, so 4 * inside / N is an estimate of pi
Print the estimate for N = 100, 1000, 10000 and 100000 and compare with math.pi
Last week's random point in the circle (lecture 2-1) is one dart; now throw N of them
```python
terminal
```
```python
N = 100: 3.24
N = 1000: 3.152
N = 10000: 3.1384
N = 100000: 3.1416
math.pi: 3.1416
```
```python
Think about
A point (x, y) is inside the circle when x * x + y * y <= 1
for n in [100, 1000, 10000, 100000]: walks the four sizes
The accumulator: count the hits
```

## Slide 23
The idea: area as probability
A random point in the square lands inside the circle with probability pi / 4. Count how often it does.
```python
1 · Throw - x = 2 * random.random() - 1, the same for y
2 · Test - inside when x * x + y * y <= 1
3 · Count - hits += 1 for every point inside
4 · Estimate - hits / n is about pi / 4, so pi is about 4 * hits / n
5 · Repeat - more darts, better estimate; the error shrinks slowly
```
In pseudocode
for each size n:
      hits = 0
      repeat n times:
            throw a random point
            if it is inside: hits += 1
      print 4 * hits / n

## Slide 24
Exercise 5: one solution
`monte_carlo_pi.py`
```python
import random
import math

for n in [100, 1000, 10000, 100000]:
    hits = 0
    for i in range(n):
        x = 2 * random.random() - 1
        y = 2 * random.random() - 1
        if x * x + y * y <= 1:
            hits += 1
    estimate = 4 * hits / n
    print(f"N = {n}: {round(estimate, 4)}")
print(f"math.pi: {round(math.pi, 4)}")
```
```python
Reading the program
Two loops: the outer picks a size, the inner throws that many darts
Reset per size: hits = 0 sits inside the outer loop
A fresh point per dart: both random calls are inside the inner loop
The estimate uses /: a float, printed rounded to 4 digits
```

## Slide 25
Exercise 5: the run
`monte_carlo_pi.py`
```python
import random
import math

for n in [100, 1000, 10000, 100000]:
    hits = 0
    for i in range(n):
        x = 2 * random.random() - 1
        y = 2 * random.random() - 1
        if x * x + y * y <= 1:
            hits += 1
    estimate = 4 * hits / n
    print(f"N = {n}: {round(estimate, 4)}")
print(f"math.pi: {round(math.pi, 4)}")
```
```python
python monte_carlo_pi.py (one run)
```
```python
N = 100: 3.24
N = 1000: 3.152
N = 10000: 3.1384
N = 100000: 3.1416
math.pi: 3.1416
```

## Slide 26
Exercise 5, expansion: how often is it 7?
`sevens.py`
```python
import random

N = 10000
sevens = 0
for i in range(N):
    first = int(random.random() * 6) + 1
    second = int(random.random() * 6) + 1
    if first + second == 7:
        sevens += 1

print(f"Sevens: {sevens} of {N}")
print(f"Share: {round(sevens / N, 3)}")
print(f"Expected: {round(1 / 6, 3)}")
```
Last week's question, answered
Two dice, ten thousand times: the same three-part shape - throw, test, count
Expected: 6 of the 36 combinations add up to 7, so about one roll in six
Your turn: count how often the two dice are equal, and how often the total is 2
```python
python sevens.py (one run)
```
```python
Sevens: 1687 of 10000
Share: 0.169
Expected: 0.167
```

## Slide 27
Extra 1: Any base
Warm-up
Conditions
while
for
Monte Carlo
Extra
Wrap-up
EXTRA
Task: generalise the two binary conversions of lecture 2-2 to any base from 2 to 10.
to_base: read a number n >= 0 and a base; print n written in that base (26 in base 3 is 222)
from_base: read a string of digits and a base; print its value (222 in base 3 is 26)
Handle n = 0, and stop with a message if a digit is too big for the base
```python
terminal
```
```python
n: 26
base: 3
222

digits: 222
base: 3
26
```
```python
Think about
In base 2 the loop used % 2 and // 2. What do they become?
Reading back: value = value * base + int(ch) for each character
```

## Slide 28
Extra 1: to any base
`to_base.py`
```python
n = int(input("n: "))
base = int(input("base: "))

digits = ""
if n == 0:
    digits = "0"
while n > 0:
    digits = str(n % base) + digits
    n = n // base
print(digits)
```
```python
Nothing depended on 2
% base peels off the last digit, // base drops it
Last digit first: each new digit is put in front of the ones found so far
Zero: the loop never runs, so the if before it supplies the single digit 0
Sanity check: base 10 must print the number unchanged
```

## Slide 29
Extra 1: the run
`to_base.py`
```python
n = int(input("n: "))
base = int(input("base: "))

digits = ""
if n == 0:
    digits = "0"
while n > 0:
    digits = str(n % base) + digits
    n = n // base
print(digits)
```
`python to_base.py`
```python
n: 26
base: 3
222
```

## Slide 30
Extra 1: from any base
`from_base.py`
```python
text = input("digits: ")
base = int(input("base: "))

value = 0
valid = True
for ch in text:
    digit = int(ch)
    if digit >= base:
        valid = False
        break
    value = value * base + digit
if valid:
    print(value)
else:
    print("not a valid number in that base")
```
```python
Horner, with a guard
Left to right: value * base + digit - everything so far is worth base times more, plus this digit
The guard: a digit that is too big for the base makes the number invalid
Flag and break: the loop discovers, the code after the loop acts (lecture 2-2)
A letter still crashes int(ch) - a stated limitation until next week's strings
```

## Slide 31
Extra 1: the run
`from_base.py`
```python
text = input("digits: ")
base = int(input("base: "))

value = 0
valid = True
for ch in text:
    digit = int(ch)
    if digit >= base:
        valid = False
        break
    value = value * base + digit
if valid:
    print(value)
else:
    print("not a valid number in that base")
```
`python from_base.py`
```python
digits: 222
base: 3
26
```

## Slide 32
Recitation summary
Warm-up
Conditions
while
for
Monte Carlo
Extra
Wrap-up
What we practised
Order in an elif chain
Most specific first, or make every test exclusive.
while True and break
Exit from the middle, where the answer is known.
The three moving parts
Initialise, test, update - and reset inside the outer loop.
Simulation
Throw, test, count: the share of hits estimates a probability.
Tools we used
Conditions
if, elif, else, the conditional expression, and, or, chained comparisons
Loops
while, for, range(start, stop, step), break, +=, end=""
Patterns
accumulator, running maximum, flag and break, nested loops
Conversions
% and // peel digits off; value * base + digit reads them back

## Slide 33
Self practice
AT HOME
Write a program for each of these.
Sentinel statistics
Read numbers until -1 is entered. Print how many there were, their sum, their average, the smallest and the largest. Say so if there were none.
A diamond
Read n and print a diamond of stars with 2n - 1 rows: 1 star, then 3, ..., 2n - 1, then back down. abs() helps.
Fizz and buzz
Print the numbers 1 to 50, but replace multiples of 3 by Fizz, multiples of 5 by Buzz, and multiples of both by FizzBuzz.
Count the digits
Read a non-negative integer and print how many digits it has, with a loop and % and // - then check your answer against 0 and 10.

## Slide 34
PYTHON COURSE · WEEK 3 · RECITATION 3
Next: Strings and approximation
indexing, slicing, methods, and bisection

## From `checkerboard.py`

### `checkerboard.py`
```python
n = int(input("n: "))

for i in range(n):
    for j in range(n):
        if (i + j) % 2 == 0:
            print("#", end="")
        else:
            print(".", end="")
    print()
```

## From `collatz.py`

### `collatz.py`
```python
n = int(input("n: "))

steps = 0
while n != 1:
    print(n, end=" ")
    if n % 2 == 0:
        n = n // 2
    else:
        n = 3 * n + 1
    steps += 1
print(n)
print(f"{steps} steps")
```

## From `computer_guesses.py`

### `computer_guesses.py`
```python
low = 1
high = 100
rounds = 0
while True:
    guess = (low + high) // 2
    rounds += 1
    answer = input(f"Is it {guess}? (h/l/c) ")
    if answer == "c":
        print(f"Got it in {rounds} rounds")
        break
    elif answer == "h":
        low = guess + 1
    else:
        high = guess - 1
```

## From `from_base.py`

### `from_base.py`
```python
text = input("digits: ")
base = int(input("base: "))

value = 0
valid = True
for ch in text:
    digit = int(ch)
    if digit >= base:
        valid = False
        break
    value = value * base + digit
if valid:
    print(value)
else:
    print("not a valid number in that base")
```

## From `guess.py`

### `guess.py`
```python
import random
secret = int(random.random() * 100) + 1
tries = 0
while True:
    guess = int(input("Guess: "))
    if guess < 1 or guess > 100:
        print("Between 1 and 100, please")
    else:
        tries += 1
        if guess < secret:
            print("Higher")
        elif guess > secret:
            print("Lower")
        else:
            print(f"Correct in {tries} tries")
            break
```

## From `hollow_square.py`

### `hollow_square.py`
```python
n = int(input("n: "))

for i in range(n):
    for j in range(n):
        on_row = i == 0 or i == n - 1
        on_col = j == 0 or j == n - 1
        if on_row or on_col:
            print("*", end="")
        else:
            print(" ", end="")
    print()
```

## From `longest_chain.py`

### `longest_chain.py`
```python
best_start = 1
best_steps = 0
for start in range(1, 100):
    n = start
    steps = 0
    while n != 1:
        if n % 2 == 0:
            n = n // 2
        else:
            n = 3 * n + 1
        steps += 1
    if steps > best_steps:
        best_steps = steps
        best_start = start
print(f"{best_start} takes {best_steps} steps")
```

## From `monte_carlo_pi.py`

### `monte_carlo_pi.py`
```python
import random
import math

for n in [100, 1000, 10000, 100000]:
    hits = 0
    for i in range(n):
        x = 2 * random.random() - 1
        y = 2 * random.random() - 1
        if x * x + y * y <= 1:
            hits += 1
    estimate = 4 * hits / n
    print(f"N = {n}: {round(estimate, 4)}")
print(f"math.pi: {round(math.pi, 4)}")
```

## From `sevens.py`

### `sevens.py`
```python
import random

N = 10000
sevens = 0
for i in range(N):
    first = int(random.random() * 6) + 1
    second = int(random.random() * 6) + 1
    if first + second == 7:
        sevens += 1

print(f"Sevens: {sevens} of {N}")
print(f"Share: {round(sevens / N, 3)}")
print(f"Expected: {round(1 / 6, 3)}")
```

## From `ticket.py`

### `ticket.py`
```python
age = int(input("Age: "))

if age < 5:
    price = 0
elif age < 18:
    price = 20
elif age < 65:
    price = 40
else:
    price = 25

msg = f"Price: {price}"
print("Free" if price == 0 else msg)
```

## From `ticket_alice.py`

### `ticket_alice.py`
```python
age = int(input("Age: "))

if age < 65:
    price = 40
elif age < 18:
    price = 20
elif age < 5:
    price = 0
else:
    price = 25

msg = f"Price: {price}"
print("Free" if price == 0 else msg)
```

## From `to_base.py`

### `to_base.py`
```python
n = int(input("n: "))
base = int(input("base: "))

digits = ""
if n == 0:
    digits = "0"
while n > 0:
    digits = str(n % base) + digits
    n = n // base
print(digits)
```

## From `warmup_loops_1.py`

### `warmup_loops_1.py`
```python
# A
i = 0
while i < 5:
    print(i)
    i += 1

# B
i = 0
while i <= 5:
    print(i)
    i += 1
```

## From `warmup_loops_2.py`

### `warmup_loops_2.py`
```python
# C
i = 0
while i < 5:
    print(i)
i += 1

# D
total = 0
for i in range(1, 4):
    total = 0
    total += i
print(total)
```

## From `warmup_range.py`

### `warmup_range.py`
```python
for i in range(2, 11, 3):
    print(i, end=" ")
print()
for i in range(5, 0, -2):
    print(i, end=" ")
print()
for ch in "abc":
    print(ch * 2, end=" ")
print()
for i in range(3, 3):
    print("never")
print("done")
```
