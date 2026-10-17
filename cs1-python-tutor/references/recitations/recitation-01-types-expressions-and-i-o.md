# Recitation, week 1: Types, expressions and I/O

## From `recitation 1.pptx`

## Slide 1
```python
>>>
```
INTRO TO CS COURSE · WEEK 1 · RECITATION 1
Recitation 1
Types, expressions and I/O

## Slide 2
Recitation overview
Warm-up
Receipt & time
Bugs
Booleans
Randomness
Extra
Wrap-up
1
REPL warm-up
predict, then run
2
Receipt and time
input, casting, // and %
3
Bugs and booleans
three kinds of errors; answers without if
4
Randomness
a fair die, built step by step

## Slide 3
How this recitation works
Warm-up
Receipt & time
Bugs
Booleans
Randomness
Extra
Wrap-up
Try first
Every exercise starts with time on your own - the chip says how many minutes. No solution appears before it runs out.
Three levels
Easy, Mid and High, in that order. Extra, at the end, is for a fast room or for home.
Only this week
Nothing here needs if, loops or anything from week 2. If you know them, do not use them yet.
The files
Every program shown is in the 'recitation 1 code' folder. Run it, change it, break it.

## Slide 4
Before we start: three checks
Warm-up
Receipt & time
Bugs
Booleans
Randomness
Extra
Wrap-up
```python
1 · The interpreter
In a terminal, type python --version (or python3 --version). You should see Python 3.13.
```
```python
2 · The REPL
Type python, then 2 ** 10 at the >>> prompt. You should see 1024. Leave with exit().
```
```python
3 · A script
In VS Code, open an empty folder, create hello.py with one print line, and press Run.
```

## Slide 5
Warm-up: numbers
Warm-up
Receipt & time
Bugs
Booleans
Randomness
Extra
Wrap-up
WARM-UP · 4 MIN
Write the output of every line on paper. Then we run it and compare.
`warmup_numbers.py`
```python
print(7 / 2)
print(7 // 2)
print(7 % 2)
print(2 ** 10)
print(-7 // 2)
print(type(7 / 2))
print(10 / 5)
print(1 / 3)
```
```python
Your answers
?
?
?
?
?
?
?
?
```

## Slide 6
Warm-up: numbers - the answers
What each line prints. Check it against your paper.
`warmup_numbers.py`
```python
print(7 / 2)
print(7 // 2)
print(7 % 2)
print(2 ** 10)
print(-7 // 2)
print(type(7 / 2))
print(10 / 5)
print(1 / 3)
```
```python
The answers
3.5
3
1
1024
-4
<class 'float'>
2.0
0.3333333333333333
```

## Slide 7
Warm-up: text and casting
WARM-UP · 4 MIN
Same game. One of these lines does not print anything. Which one, and why?
`warmup_text.py`
```python
print("6" + "5")
print("6" * 3)
print(6 * "5")
print(int("6") + 5)
print(str(6) + "5")
print(float("6"))
print(bool(0), bool("0"))
print("6" + 5)
```
```python
Your answers
?
?
?
?
?
?
?
?
```

## Slide 8
Warm-up: text and casting - the answers
What each line prints - and the one line that does not.
`warmup_text.py`
```python
print("6" + "5")
print("6" * 3)
print(6 * "5")
print(int("6") + 5)
print(str(6) + "5")
print(float("6"))
print(bool(0), bool("0"))
print("6" + 5)
```
```python
The answers
65
666
555
11
65
6.0
False True
TypeError - and the program stops
```

## Slide 9
Exercise 1: The receipt
Warm-up
Receipt & time
Bugs
Booleans
Randomness
Extra
Wrap-up
EASY · 7 MIN ON YOUR OWN
Task: a cashier types an item, a quantity and a unit price. Print the receipt.
Read the item name, the quantity (whole) and the unit price
VAT is 18% of the subtotal; the total is subtotal plus VAT
Three lines of output, built with f-strings, rounded to 2 digits
```python
terminal
```
```python
Item: notebook
Quantity: 3
Unit price: 12.5
notebook x 3 = 37.5
VAT (18%): 6.75
Total: 44.25
```
```python
Think about
Input is text: wrap input() in int() or float()
round(x, 2) rounds x to two decimal places
```

## Slide 10
Exercise 1: one solution
`receipt.py`
```python
item = input("Item: ")
quantity = int(input("Quantity: "))
price = float(input("Unit price: "))

subtotal = quantity * price
vat = subtotal * 0.18
total = subtotal + vat

print(f"{item} x {quantity} = {subtotal}")
print(f"VAT (18%): {round(vat, 2)}")
print(f"Total: {round(total, 2)}")
```
```python
Three things to notice
Casting: int() for a count, float() for a price - the type says what the value is
f-strings: anything inside the braces is evaluated and turned into text
round(): only the printed value is rounded; the arithmetic is exact as it can be
```

## Slide 11
Exercise 1: the run
`receipt.py`
```python
item = input("Item: ")
quantity = int(input("Quantity: "))
price = float(input("Unit price: "))

subtotal = quantity * price
vat = subtotal * 0.18
total = subtotal + vat

print(f"{item} x {quantity} = {subtotal}")
print(f"VAT (18%): {round(vat, 2)}")
print(f"Total: {round(total, 2)}")
```
`python receipt.py`
```python
Item: notebook
Quantity: 3
Unit price: 12.5
notebook x 3 = 37.5
VAT (18%): 6.75
Total: 44.25
```

## Slide 12
Exercise 1, expansion: a discount
`receipt_discount.py`
```python
item = input("Item: ")
quantity = int(input("Quantity: "))
price = float(input("Unit price: "))
discount = float(input("Discount (%): "))
subtotal = quantity * price
paid = subtotal * (1 - discount / 100)
vat = paid * 0.18
total = paid + vat
print(f"{item} x {quantity} = {subtotal}")
print(f"After discount: {round(paid, 2)}")
print(f"VAT (18%): {round(vat, 2)}")
print(f"Total: {round(total, 2)}")
```
```python
What changed
One more input: the discount, as a percentage
One more line: 1 - discount / 100 is the part the customer pays
Order matters: the discount first, then VAT on the reduced price
Try it: notebook, 3, 12.5, 10 gives 33.75, 6.08 and 39.83
```

## Slide 13
Exercise 2: Seconds to h:m:s
Warm-up
Receipt & time
Bugs
Booleans
Randomness
Extra
Wrap-up
EASY · 8 MIN ON YOUR OWN
Task: read a number of seconds and print it as hours, minutes and seconds.
3725 seconds is 1 hour, 2 minutes and 5 seconds
Use only whole numbers: no decimal point anywhere in the output
Two operators do all the work - which two?
```python
terminal
```
```python
Seconds: 3725
1 hours
2 minutes
5 seconds
```
```python
Think about
// answers 'how many whole units fit?'
% answers 'what is left over?'
An hour is 3600 seconds, a minute is 60
```

## Slide 14
The idea: peel off the units
3725 seconds. Take the biggest unit first, then work on what is left.
```python
1 · Hours - how many whole hours fit: 3725 // 3600 is 1
2 · What is left - the remainder: 3725 % 3600 is 125
3 · Minutes - the same pair on what is left, with 60: 125 // 60 is 2
4 · Seconds - and the remainder of that: 125 % 60 is 5
```
In pseudocode
read the number of seconds
hours = seconds // 3600
rest = seconds % 3600
minutes = rest // 60
seconds = rest % 60
print hours, minutes, seconds

## Slide 15
Exercise 2: one solution
`seconds.py`
```python
total = int(input("Seconds: "))

hours = total // 3600
rest = total % 3600
minutes = rest // 60
seconds = rest % 60

print(f"{hours} hours")
print(f"{minutes} minutes")
print(f"{seconds} seconds")
```
```python
Why these operators
Why not /: 3725 / 3600 is 1.0347..., a float
The remainder: % keeps the seconds that did not fit into hours
Naming: rest is a variable, computed once and used twice
```
`python seconds.py`
```python
Seconds: 3725
1 hours
2 minutes
5 seconds
```

## Slide 16
Exercise 3: Three bugs
Warm-up
Receipt & time
Bugs
Booleans
Randomness
Extra
Wrap-up
MID · 10 MIN ON YOUR OWN
Task: this program has three bugs, one of each kind. Find them, name the kind, fix them.
Run it as it is; read the message from the last line up
Fix one bug, run again, read the next message
The third bug prints no message: the program runs, the answer is wrong
```python
terminal
```
```python
$ python average.py
  File "average.py", line 5
    print(f"Average: {average}"
         ^
SyntaxError: '(' was never closed
```

## Slide 17
Exercise 3: the three bugs, fixed
`average.py`
```python
# average.py - the average of two grades
first = float(input("First grade: "))
second = float(input("Second grade: "))
average = (first + second) / 2
print(f"Average: {average}")
```
```python
One of each kind
Syntax: the missing ) on line 5 - Python refuses to run anything until it is fixed
Runtime: second / 2 divides text by a number - TypeError the moment that line runs; cast both inputs
Logical: first + second / 2 adds first to half of second; parentheses fix the precedence
```
`python average.py`
```python
First grade: 80
Second grade: 90
Average: 85.0
```

## Slide 18
Reading a traceback
The habit that saves the most time this semester:
Last line first - the kind of error and what caused it
Then the File line - the file name and the line number
Then the caret - points at the exact expression that failed
Everything in between is Python showing its work
A traceback is not an insult.
It is the interpreter telling you, as precisely as it can, where to look.

## Slide 19
Exercise 4: Answers without if
Warm-up
Receipt & time
Bugs
Booleans
Randomness
Extra
Wrap-up
MID · 10 MIN ON YOUR OWN
Task: two yes-or-no questions. Print True or False - the comparison is the answer.
Triangle: read three stick lengths. Can they form a triangle? Each pair of sides must add up to more than the third
Palindrome: read a three-digit number. Is it the same backwards? 121 yes, 123 no
No if anywhere: a boolean expression is a value - print it, or store it
```python
terminal
```
```python
Sides: 3 4 5 -> True
Sides: 1 2 5 -> False
Number: 121 -> True
Number: 123 -> False
```
```python
Think about
and joins three comparisons into one answer
First digit of a 3-digit number: n // 100; last digit: n % 10
```

## Slide 20
Exercise 4: the triangle
`triangle.py`
```python
a = int(input("Side a: "))
b = int(input("Side b: "))
c = int(input("Side c: "))

ok = a + b > c and a + c > b and b + c > a
print(f"Triangle: {ok}")
```
```python
One expression is the answer
Precedence: + binds tighter than >, and > tighter than and - no parentheses needed, but they never hurt
A name for the answer: ok holds True or False; next week if ok: will read like English
Three tests: 3 4 5, 1 2 5 and 5 1 2 - the last one catches a program that checked only one pair
```
`python triangle.py`
```python
Side a: 5
Side b: 1
Side c: 2
Triangle: False
```

## Slide 21
Exercise 4: the palindrome
`palindrome3.py`
```python
n = int(input("A three-digit number: "))

first = n // 100
last = n % 10
print(f"Palindrome: {first == last}")
```
```python
Digits without strings
First digit: n // 100 - how many whole hundreds
Last digit: n % 10 - what is left after the tens
The middle digit never matters: 121, 131 and 191 are all palindromes
Inside the f-string: first == last is evaluated, and the result is True or False
```
`python palindrome3.py`
```python
A three-digit number: 121
Palindrome: True
```

## Slide 22
Exercise 5: A fair die
Warm-up
Receipt & time
Bugs
Booleans
Randomness
Extra
Wrap-up
HIGH · 12 MIN ON YOUR OWN
Task: simulate a fair six-sided die. Print a whole number from 1 to 6, each equally likely.
```python
You have random.random(): a float in [0, 1) - 0 is possible, 1 is not
Four things are wrong with that for a die. Name them before you fix them
Then: an N-sided die, and then any whole number from low to high (both included)
```
```python
the REPL
```
```python
>>> import random
>>> random.random()
0.7303...
>>> ???
4
```
```python
Think about
Multiplying stretches the range; adding shifts it; int() cuts the decimals
Check each step on paper with 0.0 and with 0.999
```

## Slide 23
The idea: stretch, cut, shift
random.random() is a float in [0, 1). Fix one gap per step; check 0.0 and 0.999 each time.
```python
1 · Stretch - r * 6 is a float in [0, 6): 0.0 stays 0.0, 0.999 becomes 5.994
2 · Cut - int(r * 6) is a whole number from 0 to 5: 5.994 becomes 5
3 · Shift - int(r * 6) + 1 is a whole number from 1 to 6: a die
4 · Check - each face owns a slice of width 1/6 of [0, 1): the die is fair
```
In pseudocode
r = a random float in [0, 1)
stretch: r * 6, now in [0, 6)
cut: int(...), now 0 to 5
shift: + 1, now 1 to 6
print it

## Slide 24
Exercise 5: one solution, step by step
`die.py`
```python
import random

r = random.random()
print(f"random.random() gave {r}")

stretched = r * 6
cut = int(stretched)
face = cut + 1
print(f"stretched: {stretched}")
print(f"cut: {cut}")
print(f"the die shows {face}")
```
```python
Why it is fair
Equal slices: r falls in [0, 1/6) for a 1, in [1/6, 2/6) for a 2, and so on - six slices of the same size
The top is safe: r is never 1.0, so r * 6 is never 6.0, so the face is never 7
One line: int(random.random() * 6) + 1 is how it is written in real code
```

## Slide 25
Exercise 5: the run
`die.py`
```python
import random

r = random.random()
print(f"random.random() gave {r}")

stretched = r * 6
cut = int(stretched)
face = cut + 1
print(f"stretched: {stretched}")
print(f"cut: {cut}")
print(f"the die shows {face}")
```
```python
python die.py (one run)
```
```python
random.random() gave 0.7303
stretched: 4.3818
cut: 4
the die shows 5
```

## Slide 26
Exercise 5: N sides, and any range
The same three steps, with the task's own numbers in place of 6 and 1.
`die_n.py`
```python
import random
n = int(input("How many sides? "))
r = random.random()
face = int(r * n) + 1
print(f"The die shows {face}")
```
`random_range.py`
```python
import random
low = int(input("Lowest: "))
high = int(input("Highest: "))
count = high - low + 1
r = random.random()
value = int(r * count) + low
print(f"Picked {value}")
```
N sides: stretch by N, cut, shift by 1. N = 6 is the die; N = 2 is a coin.
A range: high - low + 1 values, so stretch by that count and shift by low. Check: 0.0 gives low, 0.999 gives high.

## Slide 27
Exercise 5: is doubling a die two dice?
Dana rolled one die and doubled it. Noam rolled two. Same thing?
`double_die.py`
```python
import random
face = int(random.random() * 6) + 1
total = 2 * face
print(f"Doubled: {total}")
```
`two_dice.py`
```python
import random
first = int(random.random() * 6) + 1
second = int(random.random() * 6) + 1
total = first + second
print(f"Two dice: {total}")
```
```python
Think about
Can Dana's program ever print 7? Can it print 3?
Which total does Noam's program print most often, and why?
How many times does each program call random.random()?
```

## Slide 28
Exercise 5: is doubling a die two dice?
Dana rolled one die and doubled it. Noam rolled two. Same thing?
`double_die.py`
```python
import random
face = int(random.random() * 6) + 1
total = 2 * face
print(f"Doubled: {total}")
```
`two_dice.py`
```python
import random
first = int(random.random() * 6) + 1
second = int(random.random() * 6) + 1
total = first + second
print(f"Two dice: {total}")
```
```python
No. Dana's total is always even, and 2, 4, ..., 12 are equally likely. Noam's can be 7, and 7 is the most likely sum.
Each call to random.random() is a fresh draw: two independent values need two calls.
```

## Slide 29
Extra: if there is time
Warm-up
Receipt & time
Bugs
Booleans
Randomness
Extra
Wrap-up
EXTRA
Two more exercises. In class if we are ahead of the plan; otherwise the first thing to try at home.
Extra 1: The clock
22:45 plus 150 minutes: the two operators of exercise 2, with a wrap-around at 24.
Extra 2: Four digits
The digits of a four-digit number, their sum, and the number backwards - with // and % only.

## Slide 30
Extra 1: The clock
Warm-up
Receipt & time
Bugs
Booleans
Randomness
Extra
Wrap-up
EXTRA
Task: it is 22:45. A film lasts 150 minutes. When does it end?
Read the hour, the minutes and the duration in minutes
Print the time when the film ends, on a 24-hour clock
22:45 plus 150 minutes is 1:15 the next day - the hours wrap around at 24
```python
terminal
```
```python
Hours now: 22
Minutes now: 45
Duration in minutes: 150
Ends at 1:15
```
```python
Think about
Turn everything into minutes first, then back into hours and minutes
Wrapping around 24: what does % do for you?
```

## Slide 31
Extra 1: one solution
`clock.py`
```python
hours = int(input("Hours now: "))
minutes = int(input("Minutes now: "))
duration = int(input("Duration in minutes: "))

total = hours * 60 + minutes + duration
end_hours = (total // 60) % 24
end_minutes = total % 60

print(f"Ends at {end_hours}:{end_minutes}")
```
```python
The plan, in three lines
One unit: total is minutes since midnight, plus the film
Back out: // 60 gives hours, % 60 gives the minutes that did not fit
The wrap: % 24 turns 25 hours into 1 - the same trick as a clock face
```
`python clock.py`
```python
Hours now: 22
Minutes now: 45
Duration in minutes: 150
Ends at 1:15
```

## Slide 32
Extra 1, expansion: always two digits
`clock_two_digits.py`
```python
hours = int(input("Hours now: "))
minutes = int(input("Minutes now: "))
duration = int(input("Duration in minutes: "))

total = hours * 60 + minutes + duration
end_hours = (total // 60) % 24
end_minutes = total % 60

tens = end_minutes // 10
ones = end_minutes % 10
print(f"Ends at {end_hours}:{tens}{ones}")
```
```python
Digits are units too
Tens and ones: // 10 and % 10 split a number below 100 into its two digits
Printing them side by side: {tens}{ones} with nothing in between
9:05 now prints as 9:05 - and 9:30 still prints as 9:30
```
`python clock_two_digits.py`
```python
Hours now: 9
Minutes now: 0
Duration in minutes: 5
Ends at 9:05
```

## Slide 33
Extra 2: Four digits
Warm-up
Receipt & time
Bugs
Booleans
Randomness
Extra
Wrap-up
EXTRA
Task: read a four-digit number. Print its digits, their sum, and the number backwards.
```python
4913 has the digits 4, 9, 1, 3; their sum is 17; backwards it is 3194
Only //, %, * and + - no strings, no loops
One more line: is the number a palindrome? True or False
```
```python
terminal
```
```python
Number: 4913
Digits: 4 9 1 3
Sum: 17
Backwards: 3194
Palindrome: False
```
```python
Think about
Thousands: n // 1000. Then the remainder, with 100, 10 and 1
Backwards: the units digit goes into the thousands place
```

## Slide 34
Extra 2: one solution
`digits.py`
```python
n = int(input("Number: "))

d1 = n // 1000          # thousands
d2 = n % 1000 // 100    # hundreds
d3 = n % 100 // 10      # tens
d4 = n % 10             # units
backwards = d4 * 1000 + d3 * 100 + d2 * 10 + d1

print(f"Digits: {d1} {d2} {d3} {d4}")
print(f"Sum: {d1 + d2 + d3 + d4}")
print(f"Backwards: {backwards}")
print(f"Palindrome: {n == backwards}")
```
```python
Reading the digit lines
Remainder, then quotient: n % 1000 // 100 drops the thousands, then counts the hundreds
Left to right: % and // have the same precedence, so it is (n % 1000) // 100
Backwards: the place values 1000, 100, 10, 1 are handed out in reverse order
```

## Slide 35
Extra 2: the run
`digits.py`
```python
n = int(input("Number: "))

d1 = n // 1000          # thousands
d2 = n % 1000 // 100    # hundreds
d3 = n % 100 // 10      # tens
d4 = n % 10             # units
backwards = d4 * 1000 + d3 * 100 + d2 * 10 + d1

print(f"Digits: {d1} {d2} {d3} {d4}")
print(f"Sum: {d1 + d2 + d3 + d4}")
print(f"Backwards: {backwards}")
print(f"Palindrome: {n == backwards}")
```
`python digits.py`
```python
Number: 4913
Digits: 4 9 1 3
Sum: 17
Backwards: 3194
Palindrome: False
```

## Slide 36
The swap without a temporary
Swap two numbers using only + and -. Fill in the trace for a = 7, b = 3.
`swap.py`
```python
a = int(input("a: "))
b = int(input("b: "))

a = a + b
b = a - b
a = a - b

print(f"a = {a}, b = {b}")
```
step | a | b
start | 7 | 3
a = a + b |  | 
b = a - b |  | 
a = a - b |  | 

## Slide 37
The swap without a temporary - the trace
With a = 7, b = 3: after each line, exactly one of the two variables has changed.
`swap.py`
```python
a = int(input("a: "))
b = int(input("b: "))

a = a + b
b = a - b
a = a - b

print(f"a = {a}, b = {b}")
```
step | a | b
start | 7 | 3
a = a + b | 10 | 3
b = a - b | 10 | 7
a = a - b | 3 | 7

## Slide 38
Recitation summary
Warm-up
Receipt & time
Bugs
Booleans
Randomness
Extra
Wrap-up
What we practised
Casting
int(input()) and float(input()) for every number you read.
// and %
Whole units and the remainder: time, money, digits.
f-strings
Expressions inside the braces become text.
Booleans
A comparison is a value: print it, store it, combine it with and.
Tools we used
Built-ins
print, input, int, float, str, bool, type, round, abs
Modules
random.random() in [0, 1); math.pi and math.sqrt in the extras
Operators
+ - * / // % ** and the six comparisons
Errors
SyntaxError, TypeError, ValueError, ZeroDivisionError - read from the bottom

## Slide 39
Self practice
AT HOME
Write a program for each of these.
Circle
Read a radius and print the circumference and the area, using math.pi and round().
Average of three
Read three grades and print their average, rounded to one decimal place.
Change
Read an amount in shekels and print how many 10, 5, 2 and 1 shekel coins give exactly that amount, using as few coins as possible.
Savings
Read a starting amount, a yearly interest rate in percent and a number of years; print the final amount, using **.

## Slide 40
INTRO TO COURSE · WEEK 2 · RECITATION 2
Next: Conditionals and loops
if, elif, else, while and for

## From `average.py`

### `average.py`
```python
# average.py - the average of two grades
first = float(input("First grade: "))
second = float(input("Second grade: "))
average = (first + second) / 2
print(f"Average: {average}")
```

## From `average_bugs.py`

### `average_bugs.py`
```python
# average.py - the average of two grades
first = input("First grade: ")
second = input("Second grade: ")
average = first + second / 2
print(f"Average: {average}"
```

## From `clock.py`

### `clock.py`
```python
hours = int(input("Hours now: "))
minutes = int(input("Minutes now: "))
duration = int(input("Duration in minutes: "))

total = hours * 60 + minutes + duration
end_hours = (total // 60) % 24
end_minutes = total % 60

print(f"Ends at {end_hours}:{end_minutes}")
```

## From `clock_two_digits.py`

### `clock_two_digits.py`
```python
hours = int(input("Hours now: "))
minutes = int(input("Minutes now: "))
duration = int(input("Duration in minutes: "))

total = hours * 60 + minutes + duration
end_hours = (total // 60) % 24
end_minutes = total % 60

tens = end_minutes // 10
ones = end_minutes % 10
print(f"Ends at {end_hours}:{tens}{ones}")
```

## From `die.py`

### `die.py`
```python
import random

r = random.random()
print(f"random.random() gave {r}")

stretched = r * 6
cut = int(stretched)
face = cut + 1
print(f"stretched: {stretched}")
print(f"cut: {cut}")
print(f"the die shows {face}")
```

## From `die_n.py`

### `die_n.py`
```python
import random
n = int(input("How many sides? "))
r = random.random()
face = int(r * n) + 1
print(f"The die shows {face}")
```

## From `digits.py`

### `digits.py`
```python
n = int(input("Number: "))

d1 = n // 1000          # thousands
d2 = n % 1000 // 100    # hundreds
d3 = n % 100 // 10      # tens
d4 = n % 10             # units
backwards = d4 * 1000 + d3 * 100 + d2 * 10 + d1

print(f"Digits: {d1} {d2} {d3} {d4}")
print(f"Sum: {d1 + d2 + d3 + d4}")
print(f"Backwards: {backwards}")
print(f"Palindrome: {n == backwards}")
```

## From `double_die.py`

### `double_die.py`
```python
import random
face = int(random.random() * 6) + 1
total = 2 * face
print(f"Doubled: {total}")
```

## From `palindrome3.py`

### `palindrome3.py`
```python
n = int(input("A three-digit number: "))

first = n // 100
last = n % 10
print(f"Palindrome: {first == last}")
```

## From `random_range.py`

### `random_range.py`
```python
import random
low = int(input("Lowest: "))
high = int(input("Highest: "))
count = high - low + 1
r = random.random()
value = int(r * count) + low
print(f"Picked {value}")
```

## From `receipt.py`

### `receipt.py`
```python
item = input("Item: ")
quantity = int(input("Quantity: "))
price = float(input("Unit price: "))

subtotal = quantity * price
vat = subtotal * 0.18
total = subtotal + vat

print(f"{item} x {quantity} = {subtotal}")
print(f"VAT (18%): {round(vat, 2)}")
print(f"Total: {round(total, 2)}")
```

## From `receipt_discount.py`

### `receipt_discount.py`
```python
item = input("Item: ")
quantity = int(input("Quantity: "))
price = float(input("Unit price: "))
discount = float(input("Discount (%): "))
subtotal = quantity * price
paid = subtotal * (1 - discount / 100)
vat = paid * 0.18
total = paid + vat
print(f"{item} x {quantity} = {subtotal}")
print(f"After discount: {round(paid, 2)}")
print(f"VAT (18%): {round(vat, 2)}")
print(f"Total: {round(total, 2)}")
```

## From `seconds.py`

### `seconds.py`
```python
total = int(input("Seconds: "))

hours = total // 3600
rest = total % 3600
minutes = rest // 60
seconds = rest % 60

print(f"{hours} hours")
print(f"{minutes} minutes")
print(f"{seconds} seconds")
```

## From `swap.py`

### `swap.py`
```python
a = int(input("a: "))
b = int(input("b: "))

a = a + b
b = a - b
a = a - b

print(f"a = {a}, b = {b}")
```

## From `triangle.py`

### `triangle.py`
```python
a = int(input("Side a: "))
b = int(input("Side b: "))
c = int(input("Side c: "))

ok = a + b > c and a + c > b and b + c > a
print(f"Triangle: {ok}")
```

## From `two_dice.py`

### `two_dice.py`
```python
import random
first = int(random.random() * 6) + 1
second = int(random.random() * 6) + 1
total = first + second
print(f"Two dice: {total}")
```

## From `warmup_numbers.py`

### `warmup_numbers.py`
```python
print(7 / 2)
print(7 // 2)
print(7 % 2)
print(2 ** 10)
print(-7 // 2)
print(type(7 / 2))
print(10 / 5)
print(1 / 3)
```

## From `warmup_text.py`

### `warmup_text.py`
```python
print("6" + "5")
print("6" * 3)
print(6 * "5")
print(int("6") + 5)
print(str(6) + "5")
print(float("6"))
print(bool(0), bool("0"))
print("6" + 5)
```
