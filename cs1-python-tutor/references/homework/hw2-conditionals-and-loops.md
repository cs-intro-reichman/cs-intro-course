# HW2: Conditionals and loops

Given after week 2.

**Material for this assignment: weeks 1 to 2 only** (lectures 1-1, 1-2, 2-1, 2-2, 2-x; recitations 1, 2, and the code files of those weeks). Solve it, hint toward it and point to slides using only this material and the Python listed for weeks 1 to 2 in `python-taught.md`, even if the student is already in a later week. Don't suggest or point to anything from week 3 on.

**This is graded work: guide with the hint ladder, never give solution code.**

# Assignment statement

## From `Introduction to CS - Homework 2.docx`

## Introduction to CS: Homework 2
### Getting started
In this assignment you write, test and submit five programs. They practise conditions and loops: if, while and for (lectures 2-1 and 2-2).
Rule: use only what lectures 1-1 to 2-2 teach. In particular, don't use string indexing or slicing (s[0], s[0:2]), string methods such as upper or find, or the in operator as a test (ch in s). These come in lecture 3-1. Looping over a string with for ch in s is fine (lecture 2-2).
Get the code for this assignment from the course's Moodle page (the file HW2.zip), unzip it, and open the HW2 folder in VS Code. It contains:
- time_calc.py, test_random.py, cheers.py, calc_pi.py, collatz.py: the five programs, to complete
- test_hw2.py: a tester that checks your programs (see Testing your programs)
Rules for all five programs:
- Input. Read each input with input(), one value per line, in the order the program description gives. Use input() with no prompt message, so that your output looks exactly like the examples.
- Output. Print exactly the text shown in the examples: the same words, spaces and punctuation.
- No input checks. Unless we say otherwise, you can assume that the inputs are valid, as the program description says. You don't need to write code that checks them.
In the examples below, the lines after the command are what you type, one value per line, followed by what the program prints.
### 1. TimeCalc (20 points)
The program time_calc.py reads a time in the 24-hour hh:mm format and a number of minutes to add. It computes the time plus the minutes, and prints the result in the same hh:mm format. For example, 10:30 plus 4055 minutes is 06:05. Here is one way to calculate it:
- Total minutes: 10 × 60 + 30 + 4055 = 4685
- Total hours: 4685 // 60 = 78
- New hours: 78 % 24 = 6 (the hours go round the clock every 24 hours)
- New minutes: 4685 − 78 × 60 = 5, which is also 4685 % 60
- So the answer is 06:05.
Some example runs:
```python
% python time_calc.py
10:20
30
10:50
```

```python
% python time_calc.py
10:20
40
11:00
```

```python
% python time_calc.py
09:25
700
21:05
```

```python
% python time_calc.py
10:30
4055
06:05
```

```python
% python time_calc.py
22:07
12345
11:52
```

```python
% python time_calc.py
23:59
10
00:09
```
Input rules. The time is typed on one line: two digits, a :, and two digits. Both parts have a leading 0 when needed: 5 hours and 8 minutes is 05:08, and midnight is 00:00. The hours are from 00 to 23 and the minutes from 00 to 59. The minutes to add are a whole number, 0 or more, on the next line.
Output rules. The same as the input rules: two digits, a :, two digits. This is different from the output of the TimeFormat program in Homework 1.
Implementation notes:
Reading the time. input() gives the time as one string, such as "09:25". In lecture 2-2, to_decimal.py read a binary number one character at a time: value = value * 2 + int(ch). Do the same in base 10, with two values: the digits before the : build the hours, and the digits after it build the minutes. A flag (lecture 2-2) can record whether the : has been seen yet.
Work in stages. Start with a program that reads the inputs and prints them, and nothing else:
```python
% python time_calc.py
09:30
1475
Hours: 9
Minutes: 30
Minutes to add: 1475
```
Next, compute the new hours and minutes, and print them too, as whole numbers:
```python
New hours: 10
New minutes: 5
```
Once the calculation is right, turn these lines into comments (put # in front of them), and write the final version, which prints the time by the output rules: 10:05.
The leading 0. str(5) is "5". Use if to add a "0" in front when it is needed.






### 2. How random is random.random()? (15 points)

(Dilbert, by Scott Adams, © 2001 United Feature Syndicate)
How good is Python's random number generator, random.random()? Here is one possible test. Call random.random() n times, and count how many of the numbers are greater than 0.5 and how many are less than or equal to 0.5. If the numbers are spread evenly between 0 and 1, the ratio between the two counts should get closer to 1 as n grows.
The program test_random.py reads n, a whole number 0 or more, and performs this test. Example runs (your numbers will be different):
```python
% python test_random.py
100
> 0.5:  47 times
<= 0.5: 53 times
Ratio:  0.8867924528301887
```

```python
% python test_random.py
10000
> 0.5:  4986 times
<= 0.5: 5014 times
Ratio:  0.994415636218588
```

```python
% python test_random.py
3
> 0.5:  3 times
<= 0.5: 0 times
```
The last example shows an important edge case. It can happen that every number is greater than 0.5, as in the cartoon. Then the program must not compute the ratio: the calculation would stop the program with a runtime error (do you see why?). In that case it prints only the first two lines. The program must handle this case.
Implementation notes:
- Call random.random() exactly once for each of the n numbers. The tester relies on this.
- The ratio is the first count divided by the second. Print it as it is, without rounding.
### 3. Cheers (15 points)
The program cheers.py reads a word and a whole number, 0 or more, and prints a crowd cheer. For example:
```python
% python cheers.py
RUNI
5
Give me an R: R!
Give me a  U: U!
Give me an N: N!
Give me an I: I!
What does that spell?
RUNI!!!
RUNI!!!
RUNI!!!
RUNI!!!
RUNI!!!
```
The word has capital letters only, and no spaces. For each letter, the program prints "an" if the letter is one of A, E, F, H, I, L, M, N, O, R, S, X (their names start with a vowel sound: "an R"), and "a" otherwise. After "a" there are two spaces, so that the letters line up. The number says how many times to print the word at the end.
Implementation notes:
- Work in stages. First write a loop that prints only the "Give me" lines, all with "a". Then add the a / an rule. Finally, add the last lines with a second loop.
- To find out whether a letter is one of the twelve, loop over the string "AEFHILMNORSX" and compare. A flag remembers what the loop found, like the valid flag in lecture 2-2.
- What should the program print when the number is 0? Try it.
### 4. CalcPi (20 points)
Consider this sum:
1 − 1/3 + 1/5 − 1/7 + 1/9 − 1/11 + …
The mathematicians Gregory and Leibniz discovered that as the number of terms grows, the sum gets closer and closer to π / 4. The program calc_pi.py uses this sum to approximate π. It reads one input, the number of terms to add, a whole number 0 or more. Two example runs:
```python
% python calc_pi.py
10
pi according to Python: 3.141592653589793
pi, approximated:       3.0418396189294032
```

```python
% python calc_pi.py
1000
pi according to Python: 3.141592653589793
pi, approximated:       3.140592653839794
```
The first line is Python's own value of π, the constant math.pi (after import math), for comparison.
Implementation notes:
- With 10 terms, the sum is 1 − 1/3 + … − 1/19, and the program prints 4 times the sum.
- The signs alternate: +, −, +, −, … Keep the sign in a variable and flip it on each pass (carrying a value forward, lecture 2-2), instead of computing a power of −1 each time.
- Try a few values. How many terms does it take to get the first 4 digits of π right?
### 5. Collatz Conjecture (30 points)
A hailstone sequence is made like this. Start with a whole number greater than 0, called the seed. Then: (1) if the current number is even, divide it by 2; otherwise, multiply it by 3 and add 1. (2) Repeat. Here are the first 7 hailstone sequences (the first number in each is the seed):
```python
1, 4, 2, 1, 4, 2, 1, ...
2, 1, 4, 2, 1, 4, 2, 1, ...
3, 10, 5, 16, 8, 4, 2, 1, 4, 2, 1, ...
4, 2, 1, 4, 2, 1, ...
5, 16, 8, 4, 2, 1, 4, 2, 1, ...
6, 3, 10, 5, 16, 8, 4, 2, 1, 4, 2, 1, ...
7, 22, 11, 34, 17, 52, 26, 13, 40, 20, 10, 5, 16, 8, 4, 2, 1, 4, 2, 1, ...
```
These examples suggest that hailstone sequences tend to reach the number 1. In 1937 the mathematician Lothar Collatz suggested that for every seed, the hailstone sequence eventually reaches 1. This seems to be true, but to this day nobody has proved it (which is why it is called a conjecture, not a theorem). It is one of the best-known unsolved problems in mathematics.
The program collatz.py tests the Collatz conjecture for all the seeds from 1 to n. It reads two inputs: n, a whole number 1 or more, and a mode, which is v (verbose) or c (concise). In verbose mode, the program prints every sequence, from seed 1 to seed n. For each sequence, it prints the numbers until the sequence reaches 1, and then, in brackets, how many numbers it printed. Finally it prints a summary line. In concise mode, the program prints only the summary line.
If the program ends and prints the summary line, it has checked the conjecture up to n. Two example runs:
```python
% python collatz.py
7
v
1 4 2 1 (4)
2 1 (2)
3 10 5 16 8 4 2 1 (8)
4 2 1 (3)
5 16 8 4 2 1 (6)
6 3 10 5 16 8 4 2 1 (9)
7 22 11 34 17 52 26 13 40 20 10 5 16 8 4 2 1 (17)
Every one of the first 7 hailstone sequences reached 1.
```

```python
% python collatz.py
100
c
Every one of the first 100 hailstone sequences reached 1.
```
Implementation notes:
- Work in stages. Start with a loop that prints one hailstone sequence only, for one seed, and test it on several seeds. Then put this loop inside an outer loop that goes over the seeds from 1 to n. Finally, add the verbose / concise modes.
- Look at seed 1: its sequence is 1 4 2 1, not just 1. The loop must make at least one step before it checks whether it reached 1. The while True loop with break (lecture 2-1) fits this.
- To print several numbers on one line, use print(x, end=" ") (lecture 2-1). The count in brackets includes the seed and the final 1.
- Compare strings with ==: mode == "v".
- Try concise mode with large values of n, such as 100000.
### Testing your programs
First test each program yourself, with the examples above and with inputs of your own. Then run the tester, from the HW2 folder:
```python
% python test_hw2.py
```
It runs each program on several inputs and prints PASS or FAIL for each test; for a FAIL it shows the expected output and yours. For TestRandom it controls what random.random() returns, so it can check exact output, including the edge case. Passing all the tests doesn't guarantee full points: the graders run other inputs too, and they read your code.
### Submission
Before you submit, make sure your code follows the course's coding style guidelines. Submit on the course's Moodle page, in the Homework 2 assignment. Upload these files only:
```python
time_calc.py
test_random.py
cheers.py
calc_pi.py
collatz.py
```

## From `time_calc.py`

### `time_calc.py`
```python
# Homework 2, program 1: TimeCalc
# Adds minutes to a 24-hour time and prints the new time.
# Input: a time as hh:mm (for example 09:25), then the number of minutes to add,
# each on its own line.

# Write your code here.
```

## From `test_random.py`

### `test_random.py`
```python
# Homework 2, program 2: TestRandom
# Tests how evenly random.random() splits its values around 0.5.
# Input: n, the number of calls, a whole number 0 or more.
import random

# Write your code here.
```

## From `cheers.py`

### `cheers.py`
```python
# Homework 2, program 3: Cheers
# Prints a crowd cheer for a word.
# Input: a word (capital letters only), then a whole number 0 or more,
# each on its own line.

# Write your code here.
```

## From `calc_pi.py`

### `calc_pi.py`
```python
# Homework 2, program 4: CalcPi
# Approximates pi with the series 1 - 1/3 + 1/5 - 1/7 + ...
# Input: the number of terms, a whole number 0 or more.
import math

# Write your code here.
```

## From `collatz.py`

### `collatz.py`
```python
# Homework 2, program 5: Collatz
# Checks the Collatz conjecture for every seed from 1 to n.
# Input: n (a whole number, 1 or more), then the mode, v or c,
# each on its own line.

# Write your code here.
```


# Instructor's notes for the tutor (guidance only: do not quote these to the student as an answer)

# HW2 notes for the tutor

Given after week 2 (lectures 2-1 and 2-2). Students may use only lectures 1-1 to 2-2: `if`/`elif`/`else`,
the conditional expression, `while`, `while True` with `break`, `for` over `range` or over a string,
flags, `end=` in `print`, f-strings, `str()`, `int()`. Not allowed yet: string indexing or slicing,
string methods (`upper`, `find`, `split`), and `in` as a test (`ch in s`); these come in lecture 3-1.
Input is read with `input()`, one value per line, no prompt. The tester (`test_hw2.py`) compares whole
outputs, so spaces and punctuation matter. Give hints, not code.

## 1. TimeCalc
Concepts: a loop over a string, building a number digit by digit (like `to_decimal.py` in lecture 2-2,
but in base 10), a flag, `//` and `%`, `if` for the leading 0.
Hint ladder: do the example 10:30 + 4055 by hand with the steps in the statement; write the stage that
only prints the parsed hours and minutes; ask how `to_decimal.py` read "1011" and what should change when
the loop meets the colon; then ask what the hours should be after going round the clock.
Usual problems: hours over 23 (missing round-the-clock step); missing leading 0; `int(":")` errors.

## 2. TestRandom
Concepts: a counted loop, a counter, `random.random()`, a guard against division by zero.
Hint ladder: what are the two counts when n is 3 and every number is above 0.5? What does the ratio
need then? Is n = 0 also a problem?
Usual problems: crashing with ZeroDivisionError; calling `random.random()` more than once per number
(the counts then don't add up, and the tester fails); output spacing.

## 3. Cheers
Concepts: `for ch in word`, a nested loop over a string of letters, a flag, a second loop that repeats.
Hint ladder: the statement's stages; for a / an, recall the `valid` flag in lecture 2-2: what does
the loop need to discover, and where must the flag start for each letter?
Usual problems: one space after "a" (there are two); the flag not reset for each letter.

## 4. CalcPi
Concepts: the accumulator pattern, carrying a value forward (the sign), float division.
Hint ladder: write the first three terms by hand; which part changes from term to term? How can the
sign be kept from one pass to the next instead of being recomputed?
Usual problems: one term too many or too few; forgetting to multiply by 4.

## 5. Collatz
Concepts: nested loops, `while True` with `break`, `print(..., end=" ")`, comparing strings with `==`.
Hint ladder: one sequence for one seed; what should seed 1 print, and what does that say about when the
loop tests for 1; then the outer loop over the seeds; then the two modes.
Usual problems: seed 1 printed as `1 (1)`; the count off by one; `/` instead of `//`.
