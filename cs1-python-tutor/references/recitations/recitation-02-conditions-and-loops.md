# Recitation, week 2: Conditions and loops

## From `recitation 2.pptx`

## Slide 1
```python
while
```
PYTHON COURSE · WEEK 2 · RECITATION 2
Recitation 2
Conditions and while loops

## Slide 2
Recitation overview
Warm-up
Conditions
while
Nested loops
Sentinel
Extra
Wrap-up
1
Predictions
booleans, floats, and the four loop bugs
2
Conditions
elif, order, a one-line if, and guards
3
while
games that stop when something happens
4
Loops inside loops
patterns, and a stream that ends with a sentinel

## Slide 3
Warm-up: booleans and floats
Warm-up
Conditions
while
Nested loops
Sentinel
Extra
Wrap-up
WARM-UP · 3 MIN
x is 7. Write the output of every line before we run it. Two of the lines are traps.
`warmup_booleans.py`
```python
x = 7
print(x > 5 and x < 10)
print(not x == 7)
print(x % 2 == 0 or x % 3 == 0)
print(5 <= x <= 7)
print(x == 7.0, x == "7")
print(0.1 + 0.2 == 0.3)
print(abs(0.1 + 0.2 - 0.3) < 1e-9)
print(type(x > 5))
```
```python
The answers
True
False
False (7 is odd and not a multiple of 3)
True (one comparison, not two)
True False (7 == 7.0, but "7" is text)
False (the float trap)
True (compare the gap)
<class 'bool'>
```

## Slide 4
Warm-up: how many lines?
Warm-up
Conditions
while
Nested loops
Sentinel
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

## Slide 5
Warm-up: what goes wrong?
Warm-up
Conditions
while
Nested loops
Sentinel
Extra
Wrap-up
WARM-UP · 2 MIN
Two more. Each has one of the classic loop bugs. Which, and what is printed?
`warmup_loops_2.py`
```python
# C
i = 0
while i < 5:
    print(i)
i += 1

# D
i = 1
total = 0
while i < 4:
    total = 0
    total += i
    i += 1
print(total)
```
```python
The answers
C: prints 0 forever - the update sits outside the body. Ctrl-C stops it
D: prints 3, not 6 - total is reset to 0 on every pass
Read the indentation, not the intention
```

## Slide 6
Exercise 1: Ticket price
Warm-up
Conditions
while
Nested loops
Sentinel
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
Exercise 1: Is Eligible to Vote
Warm-up
Conditions
while
Nested loops
Sentinel
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

## Slide 8
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

## Slide 9
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

## Slide 10
Exercise 2: The quadratic equation, properly
Warm-up
Conditions
while
Nested loops
Sentinel
Extra
Wrap-up
EASY · 7 MIN ON YOUR OWN
Task: lecture 1-2's quadratic.py crashes when d is negative, and assumes a is 1. Fix both.
Read a, b and c as floats; the equation is a x² + b x + c = 0
If a is 0 it is not quadratic: one root -c / b when b is not 0, otherwise 'Not an equation'
Otherwise d = b² - 4 a c decides: no real roots, one root, or two
Round every root to 2 digits; call math.sqrt only when it is safe
```python
terminal
```
```python
a: 1
b: -3
c: 2
x1 = 2.0
x2 = 1.0
```
Think about
A guard runs before the operation it protects: test d, then take the root
Ask about a before d: the formula divides by 2a
Three cases of d: an elif chain, in an order that cannot overlap

## Slide 11
Exercise 2: one solution
`quadratic.py`
```python
import math
a = float(input("a: "))
b = float(input("b: "))
c = float(input("c: "))
if a == 0:
    if b == 0:
        print("Not an equation")
    else:
        print(f"One root: {round(-c / b, 2)}")
else:
    d = b * b - 4 * a * c
    if d < 0:
        print("No real roots")
    elif d == 0:
        print(f"One root: {round(-b / (2 * a), 2)}")
    else:
        root = math.sqrt(d)
        print(f"x1 = {round((-b + root) / (2 * a), 2)}")
        print(f"x2 = {round((-b - root) / (2 * a), 2)}")
```
Guards, nested
a == 0 first: the formula divides by 2a, so the linear case is answered before any root is computed
d decides: an elif chain with three cases that cannot overlap - negative, zero, positive
math.sqrt(d) only in the else: the guard of lecture 2-1, protecting the call that crashed in lecture 1-2
round(..., 2) on the printed value: the arithmetic stays exact; only the text is shortened
`python quadratic.py`
```python
a: 1
b: 2
c: 1
One root: -1.0
```

## Slide 12
Exercise 2: the run
`quadratic.py`
```python
import math
a = float(input("a: "))
b = float(input("b: "))
c = float(input("c: "))
if a == 0:
    if b == 0:
        print("Not an equation")
    else:
        print(f"One root: {round(-c / b, 2)}")
else:
    d = b * b - 4 * a * c
    if d < 0:
        print("No real roots")
    elif d == 0:
        print(f"One root: {round(-b / (2 * a), 2)}")
    else:
        root = math.sqrt(d)
        print(f"x1 = {round((-b + root) / (2 * a), 2)}")
        print(f"x2 = {round((-b - root) / (2 * a), 2)}")
```
`python quadratic.py`
```python
a: 1
b: -3
c: 2
x1 = 2.0
x2 = 1.0

a: 0
b: 2
c: -8
One root: 4.0
```

## Slide 13
Exercise 3: Guess the number
Warm-up
Conditions
while
Nested loops
Sentinel
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

## Slide 14
Exercise 3: one solution
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

## Slide 15
Exercise 3: the run
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

## Slide 16
Exercise 3, expansion: the computer guesses
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

## Slide 17
Exercise 4: The 3n + 1 game
Warm-up
Conditions
while
Nested loops
Sentinel
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

## Slide 18
Exercise 4: one solution
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

## Slide 19
Exercise 4: the run
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

## Slide 20
Exercise 5: Patterns
Warm-up
Conditions
while
Nested loops
Sentinel
Extra
Wrap-up
MID · 10 MIN ON YOUR OWN
Task: read a size n and print two patterns with a while loop inside a while loop.
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

## Slide 21
Exercise 5: the hollow square
`hollow_square.py`
```python
n = int(input("n: "))

i = 0
while i < n:
    j = 0
    while j < n:
        on_row = i == 0 or i == n - 1
        on_col = j == 0 or j == n - 1
        if on_row or on_col:
            print("*", end="")
        else:
            print(" ", end="")
        j += 1
    print()
    i += 1
```
```python
A cell is a pair (i, j)
The visit: two loops reach every cell once, row by row; j = 0 sits inside the outer loop, so every row starts at column 0
The border: first or last row, or first or last column - two booleans, joined by or
The row: end="" keeps the cells on one line; the bare print() ends it
The updates: j += 1 is the last line of the inner body, i += 1 the last line of the outer one
Try n = 1 and n = 2: every cell is on the border
```

## Slide 22
Exercise 5: the run
`hollow_square.py`
```python
n = int(input("n: "))

i = 0
while i < n:
    j = 0
    while j < n:
        on_row = i == 0 or i == n - 1
        on_col = j == 0 or j == n - 1
        if on_row or on_col:
            print("*", end="")
        else:
            print(" ", end="")
        j += 1
    print()
    i += 1
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

## Slide 23
Exercise 5: the checkerboard
`checkerboard.py`
```python
n = int(input("n: "))

i = 0
while i < n:
    j = 0
    while j < n:
        if (i + j) % 2 == 0:
            print("#", end="")
        else:
            print(".", end="")
        j += 1
    print()
    i += 1
```
```python
Parity of i + j
Same skeleton: two loops, one if per cell, one bare print() per row
The test: a # where i + j is even - one step in any direction flips the parity
Why it works: neighbours differ by one in i or in j, never in both
Your turn: swap the two characters without touching the condition
```

## Slide 24
Exercise 5: the run
`checkerboard.py`
```python
n = int(input("n: "))

i = 0
while i < n:
    j = 0
    while j < n:
        if (i + j) % 2 == 0:
            print("#", end="")
        else:
            print(".", end="")
        j += 1
    print()
    i += 1
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

## Slide 25
Exercise 6: Statistics until -1
Warm-up
Conditions
while
Nested loops
Sentinel
Extra
Wrap-up
HIGH · 12 MIN ON YOUR OWN
Task: read non-negative numbers until -1 is entered. Report what came in.
Print how many numbers there were, their sum, their average (2 digits), the smallest and the largest
If -1 was the very first thing typed, print 'No numbers were entered.' and nothing else
Lecture 2-1's smallest.py found the minimum; keep its shape and add the other four answers
```python
terminal
```
```python
Number (-1 to finish): 8
Number (-1 to finish): 3
Number (-1 to finish): -1
Count: 2
Sum: 11
Average: 5.5
Smallest: 3
Largest: 8
```
Think about
The first number seeds smallest and largest: read it before the loop
Four accumulators, initialised once; the average divides by count, so guard the empty case

## Slide 26
The idea: seed, then stream
The numbers arrive one at a time and the program does not know how many. One value ends the stream; the rest is bookkeeping.
```python
1 · Seed - read the first number before the loop; it is the smallest and the largest so far
2 · Test - the loop runs while the number is not the sentinel: while x != END
3 · Account - count it, add it, and move smallest and largest if it beats them
4 · Next - the last line of the body reads the next number; the header tests it
5 · Report - after the loop: nothing was entered, or the five answers
```
In pseudocode
read x
count = 0, total = 0
smallest = x, largest = x
while x is not -1:
      count it, add it
      smallest? largest?
      read the next x
if count is 0: say so
else: print the five answers

## Slide 27
Exercise 6: the loop (1 of 2)
```python
stats.py (lines 1-16)
```
```python
END = -1

x = int(input("Number (-1 to finish): "))
count = 0
total = 0
smallest = x
largest = x

while x != END:
    count += 1
    total += x
    if x < smallest:
        smallest = x
    if x > largest:
        largest = x
    x = int(input("Number (-1 to finish): "))
```
```python
Discover
A named sentinel: END = -1 says what the number means; the header reads while x != END
The seed: smallest and largest start as the first number, not as 0
Two independent ifs: a number can be the new smallest or the new largest, and the first one is both
The read is last: handle the current x, then fetch the next; the header tests it
```

## Slide 28
Exercise 6: the report (2 of 2)
```python
stats.py (lines 18-26)
```
```python
if count == 0:
    print("No numbers were entered.")
else:
    print(f"Count: {count}")
    print(f"Sum: {total}")
    print(f"Average: {round(total / count, 2)}")
    print(f"Smallest: {smallest}")
    print(f"Largest: {largest}")
```
Act
The guard: count == 0 means -1 came first; the else never divides by zero
Five lines, five answers: f-strings with the accumulators, round() for the average only
`python stats.py`
```python
Number (-1 to finish): 8
Number (-1 to finish): 3
Number (-1 to finish): 9
Number (-1 to finish): -1
Count: 3
Sum: 20
Average: 6.67
Smallest: 3
Largest: 9
```

## Slide 29
Exercise 6, expansion: a text sentinel
`stats_text.py`
```python
text = input("Number (done to finish): ")
count = 0
total = 0

while text != "done":
    x = int(text)
    count += 1
    total += x
    text = input("Number (done to finish): ")

if count == 0:
    print("No numbers were entered.")
else:
    print(f"Count: {count}")
    print(f"Average: {round(total / count, 2)}")
```
```python
When -1 is a legitimate value
Read text, not a number: the line stays a string until the loop has checked it
The sentinel is a word: while text != "done" - a string comparison, as in lecture 1-2; no number can collide with it
Cast inside the body: int(text) runs only for real numbers, never for the sentinel
```
`python stats_text.py`
```python
Number (done to finish): 8
Number (done to finish): -1
Number (done to finish): done
Count: 2
Average: 3.5
```

## Slide 30
Extra 1: Digits of any length
Warm-up
Conditions
while
Nested loops
Sentinel
Extra
Wrap-up
EXTRA
Task: recitation 1 took a four-digit number apart. Do it for any length, with a loop.
Read a non-negative integer. Print how many digits it has, their sum, the number backwards, and whether it is a palindrome
Only //, %, * and + inside the loop - no strings
Check your answer on 0 and on 10 before you trust it
```python
terminal
```
```python
Number: 4913
Digits: 4
Sum: 17
Backwards: 3194
Palindrome: False
```
```python
Think about
n % 10 is the last digit, n // 10 drops it (lecture 2-1)
Backwards: backwards * 10 + digit, last digit first
The loop never runs for 0 - how many digits does 0 have?
```

## Slide 31
Extra 1: one solution
`digits_loop.py`
```python
n = int(input("Number: "))
original = n
digits = 0
total = 0
backwards = 0
while n > 0:
    digit = n % 10
    digits += 1
    total += digit
    backwards = backwards * 10 + digit
    n = n // 10
if original == 0:
    digits = 1
print(f"Digits: {digits}")
print(f"Sum: {total}")
print(f"Backwards: {backwards}")
print(f"Palindrome: {original == backwards}")
```
```python
Four accumulators, one loop
Keep the original: n is destroyed by the loop, so a copy is kept for the palindrome test
Peel and push: % 10 takes the last digit, // 10 drops it, * 10 + digit builds the mirror image
The zero guard: the loop never runs for 0, so digits would stay 0; one if fixes the count
10 backwards is 1: the leading zero cannot be stored in a number - correct, and worth saying
```
`python digits_loop.py`
```python
Number: 12321
Digits: 5
Sum: 9
Backwards: 12321
Palindrome: True
```

## Slide 32
Extra 1: the run
`digits_loop.py`
```python
n = int(input("Number: "))
original = n
digits = 0
total = 0
backwards = 0
while n > 0:
    digit = n % 10
    digits += 1
    total += digit
    backwards = backwards * 10 + digit
    n = n // 10
if original == 0:
    digits = 1
print(f"Digits: {digits}")
print(f"Sum: {total}")
print(f"Backwards: {backwards}")
print(f"Palindrome: {original == backwards}")
```
`python digits_loop.py`
```python
Number: 4913
Digits: 4
Sum: 17
Backwards: 3194
Palindrome: False
```

## Slide 33
Recitation summary
Warm-up
Conditions
while
Nested loops
Sentinel
Extra
Wrap-up
What we practised
Order in an elif chain
Most specific first, or make every test exclusive.
Guard before you compute
Test a, test d, then take the root - never the other way round.
while True and break
Exit from the middle, where the answer is known.
Seed, then stream
Read the first value before the loop; the last line of the body reads the next.
Tools we used
Booleans
the six comparisons, and, or, not, chained comparisons, bool()
Conditions
if, elif, else, nested if, the conditional expression, guards
Loops
while, +=, break, while True, a loop inside a loop, end=""
Patterns
accumulator, running minimum and maximum, sentinel, a trace table

## Slide 34
Self practice
AT HOME
Write a program for each of these.
A diamond
Read n and print a diamond of stars with 2n - 1 rows: 1 star, then 3, ..., 2n - 1, then back down. Two while loops and abs() do it.
Fizz and buzz
Print the numbers 1 to 50 with a while loop, but replace multiples of 3 by Fizz, multiples of 5 by Buzz, and multiples of both by FizzBuzz.
Doubling time
Read an amount and a yearly interest rate in percent. How many years until the amount has doubled? A loop that grows the amount until it passes the target.
Leap years
Read two years and print every leap year between them, one per line, with the boolean of lecture 1-2 inside a while loop. Count them too.

## Slide 35
PYTHON COURSE · WEEK 3 · RECITATION 3
Next: for loops, binary and strings
range, numeral systems, indexing, slicing, and methods

## From `checkerboard.py`

### `checkerboard.py`
```python
n = int(input("n: "))

i = 0
while i < n:
    j = 0
    while j < n:
        if (i + j) % 2 == 0:
            print("#", end="")
        else:
            print(".", end="")
        j += 1
    print()
    i += 1
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

## From `digits_loop.py`

### `digits_loop.py`
```python
n = int(input("Number: "))
original = n
digits = 0
total = 0
backwards = 0
while n > 0:
    digit = n % 10
    digits += 1
    total += digit
    backwards = backwards * 10 + digit
    n = n // 10
if original == 0:
    digits = 1
print(f"Digits: {digits}")
print(f"Sum: {total}")
print(f"Backwards: {backwards}")
print(f"Palindrome: {original == backwards}")
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

i = 0
while i < n:
    j = 0
    while j < n:
        on_row = i == 0 or i == n - 1
        on_col = j == 0 or j == n - 1
        if on_row or on_col:
            print("*", end="")
        else:
            print(" ", end="")
        j += 1
    print()
    i += 1
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

## From `quadratic.py`

### `quadratic.py`
```python
import math
a = float(input("a: "))
b = float(input("b: "))
c = float(input("c: "))
if a == 0:
    if b == 0:
        print("Not an equation")
    else:
        print(f"One root: {round(-c / b, 2)}")
else:
    d = b * b - 4 * a * c
    if d < 0:
        print("No real roots")
    elif d == 0:
        print(f"One root: {round(-b / (2 * a), 2)}")
    else:
        root = math.sqrt(d)
        print(f"x1 = {round((-b + root) / (2 * a), 2)}")
        print(f"x2 = {round((-b - root) / (2 * a), 2)}")
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

## From `stats.py`

### `stats.py`
```python
END = -1

x = int(input("Number (-1 to finish): "))
count = 0
total = 0
smallest = x
largest = x

while x != END:
    count += 1
    total += x
    if x < smallest:
        smallest = x
    if x > largest:
        largest = x
    x = int(input("Number (-1 to finish): "))

if count == 0:
    print("No numbers were entered.")
else:
    print(f"Count: {count}")
    print(f"Sum: {total}")
    print(f"Average: {round(total / count, 2)}")
    print(f"Smallest: {smallest}")
    print(f"Largest: {largest}")
```

## From `stats_text.py`

### `stats_text.py`
```python
text = input("Number (done to finish): ")
count = 0
total = 0

while text != "done":
    x = int(text)
    count += 1
    total += x
    text = input("Number (done to finish): ")

if count == 0:
    print("No numbers were entered.")
else:
    print(f"Count: {count}")
    print(f"Average: {round(total / count, 2)}")
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

## From `warmup_booleans.py`

### `warmup_booleans.py`
```python
x = 7
print(x > 5 and x < 10)
print(not x == 7)
print(x % 2 == 0 or x % 3 == 0)
print(5 <= x <= 7)
print(x == 7.0, x == "7")
print(0.1 + 0.2 == 0.3)
print(abs(0.1 + 0.2 - 0.3) < 1e-9)
print(type(x > 5))
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
i = 1
total = 0
while i < 4:
    total = 0
    total += i
    i += 1
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
