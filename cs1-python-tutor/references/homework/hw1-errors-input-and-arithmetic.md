# HW1: Errors, input and arithmetic

Given after week 1.

**Material for this assignment: week 1 only** (lectures 1-1, 1-2; recitation 1, and the code files of that week). Solve it, hint toward it and point to slides using only this material and the Python listed for week 1 in `python-taught.md`, even if the student is already in a later week. Don't suggest or point to anything from week 2 on.

**This is graded work: guide with the hint ladder, never give solution code.**

# Assignment statement

## From `Introduction to CS - Homework 1.docx`

## Introduction to CS: Homework 1
### Getting started
This assignment has two parts. Part I is a self-study exercise about errors; you don't submit it, and you can do it after lecture 1-1. Part II has five programs that you write, test and submit. You can do Part II after lecture 1-2.
Get the code for this assignment from the course's Moodle page (the file HW1.zip), unzip it, and open the HW1 folder in VS Code. It contains:
- count_to_five.py: the program for Part I
- bill3.py, fv_calc.py, num_words.py, ascend.py, time_format.py: the five programs of Part II, to complete
- test_hw1.py: a tester that checks your programs (see Testing your programs)
If you haven't yet, go over the From Zero to Code tutorial on the course website first. It shows how to open a folder in VS Code, edit a file, and run it in the terminal.
### Part I: Experimenting with errors
You will meet many error messages in this course, and some are hard to read at first. A good way to learn them is to cause common errors on purpose and read what Python says. In this part you change a working program, one change at a time, and see what happens.
The program is count_to_five.py, the running example from lecture 1-1:
```python
# Declares a variable and sets it to 0
i = 0
while i < 6:
    # Prints i, and increments it
    print(i)
    i = i + 1
print("Done")
```
Run it in the VS Code terminal. You should see this:
```python
% python count_to_five.py
0
1
2
3
4
5
Done
```
Now make the changes below, one at a time. For each change:
- Make the change in the editor and save the file.
- Run the program with python count_to_five.py.
- If there is an error message, read its last line first: it names the kind of error. The lines above it show where.
- Decide what kind of problem it is: an error Python finds before running anything (a syntax error), an error while running (a runtime error), or a program that runs but does the wrong thing (a logical error). Write one sentence that describes what went wrong.
- Undo the change before you make the next one. Or keep a copy of the original file and always start from it.
The changes:
- Change print("Done") to Print("Done")
- Change "Done" to "done"
- Change "Done" to "Done (remove the closing quotation mark)
- Change "Done" to Done (remove both quotation marks)
- Remove the colon at the end of while i < 6:
- Remove the four spaces before print(i)
- Change print(i) to print i
- Change print(i) to print(j)
- Change i = 0 to i = "0"
- Change i = i + 1 to i = i * 1
- Try other changes, as you like.
This part is for your own learning: write down what each error means, and make sure you understand it. Don't submit anything.
Stopping a program. A program with a logical error may never stop (an infinite loop). To stop it, click in the terminal and press Ctrl+C (hold Ctrl and press C).
### Part II: Programs
In this part you write five short programs. They practise reading input, computing with numbers and building output text. They use only what lectures 1-1 and 1-2 cover, so there is no if and no loops yet. Programs 4 and 5 are small riddles because of that.
Rules for all five programs:
- Input. Read each input with input(), one value per line, in the order the program description gives. Use input() with no prompt message, so that your output looks exactly like the examples. Remember that input() always returns a string; convert it with int() or float() when you need a number.
- Output. Print exactly the text shown in the examples: the same words, spaces and punctuation. f-strings (lecture 1-2) are the easiest way to build it.
- No input checks. Unless we say otherwise, in this course you can assume that the inputs are valid, as the program description says. You don't need to write code that checks them.
In the examples below, the lines after the command are what you type, one value per line, followed by what the program prints. To learn more about a function such as math.ceil, search for "python math.ceil": the first result is usually the official Python documentation.
### 1. Bill3 (10 points)
The program bill3.py splits a restaurant bill equally among three diners. It reads four inputs: the names of the three diners, then the bill, a whole number of shekels. It divides the bill by 3 and prints a message:
```python
% python bill3.py
Ron
Lisa
Dan
100
Dear Dan, Lisa, and Ron: pay 34 Shekels each.
```
Implementation notes:
- Each diner's share is rounded up to a whole number, so together the three may pay a little more than the bill. That's fine. To round up, use math.ceil, whose name comes from "ceiling": math.ceil(25.19) is 26. Put import math at the top of the program (lecture 1-2).
- The names are printed in reverse order: Dan, the last name typed, comes first, then Lisa, then Ron.
- The output is a bit wordy on purpose, to practise building text. Start with a simpler version that prints only Pay 34 Shekels each. When that works, write the full message.
### 2. FVCalc (10 points)
A savings account earns interest (⁧ריבית⁩) every year. The program fv_calc.py computes the future value of a sum of money saved in such an account. The formula is:
futureValue = currentValue · (1 + rate)n
The program reads three inputs, in this order:
- the current value, a whole number of dollars, 0 or more
- the yearly interest rate in percent, a whole number from 0 to 100
- the number of years n, a whole number, 0 or more
Two example runs:
```python
% python fv_calc.py
100
10
2
After 2 years, $100 saved at 10.0% will yield $121
```

```python
% python fv_calc.py
25000
6
25
After 25 years, $25000 saved at 6.0% will yield $107296
```
Implementation notes:
- Read the interest rate with float(), so that it prints as 10.0. Divide it by 100 to get the rate in the formula.
- Use the ** operator for "raise to the power".
- The future value is a float, but it is printed as a whole number: int(x) drops the part after the decimal point (it does not round).
A note on money: it can be surprising how interest adds up over time. Look at the second run, and try a few values of your own.
### 3. NumWords (20 points)
The program num_words.py reads a whole number, 0 or more, and prints it in terms of hundreds, tens and ones:
```python
% python num_words.py
517
5 hundreds, 1 tens, and 7 ones.
```

```python
% python num_words.py
35
0 hundreds, 3 tens, and 5 ones.
```

```python
% python num_words.py
8
0 hundreds, 0 tens, and 8 ones.
```
Implementation notes:
- The operators // and % from lecture 1-2 do most of the work.
- Outputs like "1 tens" and "0 hundreds" could be nicer, but leave them as they are for now.
- What happens with a number that has more than 3 digits? Your program will most likely still give a correct answer. Try it.
### 4. Ascend (30 points)
The program ascend.py reads a whole number lim, greater than 0. It generates three random whole numbers from 0 to lim - 1, prints them, and then prints the same three numbers in ascending order. Three example runs (your numbers will be different, since they are random):
```python
% python ascend.py
100
91 3 38
3 38 91
```

```python
% python ascend.py
100
12 71 44
12 44 71
```

```python
% python ascend.py
100
82 38 8
8 38 82
```
Rule: use only what lectures 1-1 and 1-2 teach. In particular, don't use if (lecture 2-1), and don't use Python's min, max or sorted.
Implementation notes:
- For a random whole number from 0 to lim - 1, see the worked example in lecture 1-2 (slide 58), which uses random.random().
- To keep the code short, call the three random numbers a, b and c.
- The built-in function abs (lecture 1-2) helps here: abs(a - b) is the distance between a and b. For two numbers, the larger one is (a + b + abs(a - b)) // 2. Check this on paper with a = 3, b = 8, and then with a = 8, b = 3. Then work out a similar expression for the smaller one.
- Use these two-number expressions to find the smallest and the largest of a, b and c. Then work out how to find the middle one. This is a small riddle, best solved on paper, away from the computer.
### 5. TimeFormat (30 points)
The program time_format.py reads a time in the 24-hour format and prints it in the 12-hour AM/PM format. It reads two inputs: the hours, then the minutes. Each is typed as two digits, with a leading 0 when needed. Example runs:
```python
% python time_format.py
10
15
10:15 AM
```

```python
% python time_format.py
12
05
12:05 PM
```

```python
% python time_format.py
17
08
5:08 PM
```

```python
% python time_format.py
23
50
11:50 PM
```

```python
% python time_format.py
00
00
0:00 AM
```
Input rules. The hours are from 00 to 23 and the minutes from 00 to 59, always two digits: 5 hours and 8 minutes is typed as 05, then 08. Midnight is 00, 00.
Output rules. The hours are printed as a number from 0 to 12, without a leading 0 (8, not 08). Hours 13 to 23 become 1 to 11; hours 0 to 12 stay as they are. The minutes are printed exactly as they were typed, two digits. Then a space and AM (hours 0 to 11) or PM (hours 12 to 23).
Rule: don't use if; we learn it in lecture 2-1. Use arithmetic and string operations from lecture 1-2 instead.
Implementation notes:
- Read the minutes as a string, so that a leading 0 is kept. Convert only the hours to an int.
- For hours from 0 to 23, hours // 12 is 0 before noon and 1 from noon on. What is hours // 13?
- A string times a number repeats it (lecture 1-2), and a string times 0 is the empty string: "AM" * 0 is "".
### Testing your programs
First test each program yourself, with the examples above and with inputs of your own. Then run the tester, from the HW1 folder:
```python
% python test_hw1.py
```
It runs each program on several inputs and prints PASS or FAIL for each test; for a FAIL it shows the expected output and yours. For Ascend and TimeFormat it also checks the rules (no if, min, max or sorted). Passing all the tests doesn't guarantee full points: the graders run other inputs too, and they read your code.
### Submission
Before you submit, make sure your code follows the course's coding style guidelines. Submit on the course's Moodle page, in the Homework 1 assignment. Upload these files only:
```python
bill3.py
fv_calc.py
num_words.py
ascend.py
time_format.py
```

## From `count_to_five.py`

### `count_to_five.py`
```python
# Declares a variable and sets it to 0
i = 0
while i < 6:
    # Prints i, and increments it
    print(i)
    i = i + 1
print("Done")
```

## From `bill3.py`

### `bill3.py`
```python
# Homework 1, program 1: Bill3
# Splits a restaurant bill equally among three diners.
# Input: three names and the bill (a whole number), each on its own line.

# Write your code here.
```

## From `fv_calc.py`

### `fv_calc.py`
```python
# Homework 1, program 2: FVCalc
# Computes the future value of a sum saved in a savings account.
# Input: the sum, the yearly interest rate (in percent) and the number of
# years, each on its own line.

# Write your code here.
```

## From `num_words.py`

### `num_words.py`
```python
# Homework 1, program 3: NumWords
# Prints a number in terms of hundreds, tens and ones.
# Input: a whole number.

# Write your code here.
```

## From `ascend.py`

### `ascend.py`
```python
# Homework 1, program 4: Ascend
# Prints three random numbers, then the same numbers in ascending order.
# Input: lim, a whole number greater than 0.
# Don't use if, min, max or sorted.
import random

# Write your code here.
```

## From `time_format.py`

### `time_format.py`
```python
# Homework 1, program 5: TimeFormat
# Prints a 24-hour time in the 12-hour AM/PM format.
# Input: the hours and the minutes, each on its own line, as two digits (17, then 08).
# Don't use if.

# Write your code here.
```


# Instructor's notes for the tutor (guidance only: do not quote these to the student as an answer)

# HW1 notes for the tutor

Given after week 1 (Part I after lecture 1-1, Part II after lecture 1-2). Everything uses only lectures
1-1 and 1-2: no `if`, no loops in Part II, no slicing, no `min`/`max`/`sorted`, no `random.randint`.
Students read input with `input()` (one value per line, no prompt) and print with `print` and f-strings.
The tester (`test_hw1.py`, which students have) compares the end of the last output line.

## Part I (not submitted)
Ten deliberate changes to `count_to_five.py` (lecture 1-1). The point is to tell apart the three kinds
of error (syntax, runtime, logical; lecture 1-1 slide 43) and to read a traceback (last line first).
Part I isn't graded, so you can explain each result fully once the student has tried it. Expected results:
1. `Print("Done")`: NameError, but only after 0 to 5 are printed (a runtime error: Python ran the
   lines before it).
2. `"done"`: no error; the output is different (it is not a Python error at all).
3. `"Done)`: SyntaxError, unterminated string literal. Nothing is printed: syntax errors are found
   before the program runs.
4. `Done` without quotes: NameError after the loop, `Done` is read as a variable name.
5. `while i < 6` without the colon: SyntaxError, expected ':'.
6. `print(i)` not indented: IndentationError, expected an indented block.
7. `print i`: SyntaxError, missing parentheses in call to print.
8. `print(j)`: NameError on the first pass of the loop.
9. `i = "0"`: TypeError, `<` between str and int.
10. `i = i * 1`: no error message, the program never stops (a logical error). Ctrl-C stops it.

## Program 1: Bill3 (10 points)
Concepts: `input()` returns a string, `int()`, `/` gives a float, `math.ceil` (with `import math`), f-strings.
Usual mistakes: names printed in input order instead of reversed; using `//` (rounds down, not up)
or `round` (rounds to nearest); forgetting `import math`; adding 1 after truncating (wrong when the
amount divides by 3).

## Program 2: FVCalc (10 points)
Concepts: `float(input())`, `**`, `int()` truncation, f-strings, precedence.
Usual mistakes: using the percent as the rate (forgetting to divide by 100); reading the rate with
`int` so it prints `6` instead of `6.0`; `round` instead of `int`; missing brackets around `1 + rate`
before raising to the power.

## Program 3: NumWords (20 points)
Concepts: `//` and `%`.
Usual mistakes: `n / 100` (a float); getting the tens digit with `// 10` alone (gives 51 for 517,
so ask what else is needed to keep only one digit). For more than three digits the hundreds part
keeps the extra digits (51422 gives 514 hundreds); that is expected by the spec.

## Program 4: Ascend (30 points)
Concepts: random numbers from `random.random()` (lecture 1-2 slide 58), `abs`, `//`, arithmetic.
Rules: no `if`, `min`, `max` or `sorted` (the tester checks the code for them).
The statement gives a formula for the larger of two numbers. The student has to work out the
smaller of two, then extend both to three numbers, then find the middle one. This is the riddle of
the assignment, so don't give these formulas or the way to combine them.
Hint ladder: first have them check the given formula by hand on two pairs of numbers and explain why
it works; then ask what they would change to get the smaller one; then ask how they could use the
two-number result together with the third number; for the middle, ask what they know about the three
numbers once they have the smallest and the largest.
Usual mistakes: `/ 2` instead of `// 2` (prints 38.0); a random-number expression that can produce
`lim` itself (ask them for the largest value `random.random()` can return); using `round`; printing
only the sorted line; output not matching the example line format.

## Program 5: TimeFormat (30 points)
Concepts: `int(input())`, keeping the minutes as a string, `//`, string times int.
No `if` (lecture 2-1 comes later), so it is an arithmetic riddle. The statement gives three hints:
what `hours // 12` gives, the question "what is `hours // 13`?", and that a string times 0 is "".
The student has to turn these into the 12-hour value and the AM/PM suffix. Don't give the final
expressions; work through the hints with them, for example with a table of hours 0, 11, 12, 13, 23
and what each hint expression gives.
Edge cases students miss: 12:xx is PM and stays 12; 00:xx prints as 0:xx AM (by the spec, not
12:xx); minutes keep their leading zero (so don't convert them with `int`).
Usual mistakes: an expression that turns 12 into 0 (ask them to test 12:30); using `% 12` (same problem).
