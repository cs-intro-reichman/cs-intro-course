# HW4: Algebra and MyString

Given after week 4.

**Material for this assignment: weeks 1 to 4 only** (lectures 1-1, 1-2, 2-1, 2-2, 3-1, 3-2, 4-1, 4-2; recitations 1, 2, 3, 4, and the code files of those weeks). Solve it, hint toward it and point to slides using only this material and the Python listed for weeks 1 to 4 in `python-taught.md`, even if the student is already in a later week. Don't suggest or point to anything from week 5 on.

**This is graded work: guide with the hint ladder, never give solution code.**

# Assignment statement

## From `Introduction to CS - Homework 4.docx`

## Introduction to CS: Homework 4
### Getting started
In this assignment you write two small libraries of functions (lectures 4-1 and 4-2). In Part A you build arithmetic on whole numbers from two operations only: adding 1 and subtracting 1. In Part B you write your own versions of some string methods, as functions.
Rule: use only what lectures 1-1 to 4-2 teach. In particular, don't use lists, and don't use sorted, split, join, min, max or sum. Each part also has rules of its own, given at the start of the part. The tester checks the rules.
Get the code for this assignment from the course's Moodle page (the file HW4.zip), unzip it, and open the HW4 folder in VS Code. It contains:
- algebra.py, my_string.py: the two libraries, to complete
- test_hw4.py: a tester that checks your functions (see Testing your functions)
Each library already has the design written down, as in lecture 4-2: every function has its name, its parameters, a docstring, and a stub body that returns a placeholder value. Your job is to replace each stub body with the real one. Rules for both files:
- Functions, not programs. The functions don't call input() and don't print. They get their inputs as arguments and return a value.
- The calls at the bottom. Each file ends with a few print calls that show what some calls return, with the expected result in a comment. Use them to check your work. You can change them or add your own (for example assert lines, as in lecture 4-2); the tester doesn't use them.
- Names stay. Don't change the names or the parameters of the given functions. You may add functions of your own.
- No input checks. You can assume that the arguments are what the docstring says. One exception: a function that gets a string must also work when the string is empty, "".
### Part A: Algebra (40 points)
Python has the operators +, -, *, /, //, % and **. In this part, suppose it had none of them, and all it could do with a number was add 1 to it or subtract 1 from it. That is enough: addition is adding 1 again and again, multiplication is addition again and again, and so on. You build the operations one on top of the other, each function calling the ones before it.
Rule for algebra.py: the only arithmetic allowed is adding 1 or subtracting 1 (x += 1, x = x + 1, x -= 1, x = x - 1), and -x (the negative of x). No other arithmetic, and no pow, abs, int, round or len. Comparisons (<, ==, ...) are allowed, and so is for _ in range(n) with one argument, to repeat something n times.
The file algebra.py has the following functions. All arguments and all returned values are whole numbers (int):

Some calls and what they return, when the functions are done:
```python
print(minus(2, 7))           # -5
print(times(-3, 4))          # -12
print(plus(2, times(4, 2)))  # 10
print(power(3, 5))           # 243
print(div(25, 7))            # 3
print(mod(25, 7))            # 4
print(sqrt(1000))            # 31
```
Implementation notes:
- Write and test the functions in the order of the table, one at a time (follow lecture 4-2: design first, then fill in the bodies one by one).
- Each function should use the ones before it: times calls plus, power calls times, div and mod call minus, and sqrt calls times. For example, 3 × 4 is 0 + 3 + 3 + 3 + 3: start from 0 and call plus four times.
- Negative numbers. Adding −3 is the same as subtracting 3, so when x2 is negative, plus(x1, x2) can return minus(x1, -x2). Think in the same way about minus and times. power, div, mod and sqrt get only the values in the “assumes” column.
- div(25, 7): how many times can you subtract 7 from 25 before what is left is smaller than 7? mod(25, 7) is what is left.
- sqrt(x) is the largest whole number g with g × g ≤ x. Sequential search (lecture 3-2) finds it: try g = 0, 1, 2, ... For example, sqrt(35) is 5, since 5 × 5 = 25 ≤ 35 but 6 × 6 = 36 > 35.
- These functions are slow: times(1000, 1000) adds 1 a million times. Test them on small numbers.
### Part B: MyString (60 points)
Lectures 3-1 and 4-2 showed the difference between a function, like len(s), and a method, like s.upper(). In this part you write your own versions of some string methods, as functions. The string is given as the first argument: where Python has the method call s.find(ch), our function is called as index_of(s, ch).
Rule for my_string.py: don't use string methods (nothing like s.lower() or s.find()), don't use in or not in as a test (for ch in s is fine), and don't use slicing (s[a:b]). Use len, indexing (s[i]), loops, ord and chr. Compare strings one character at a time.
The file my_string.py has these functions:

Some calls and what they return, when the functions are done:
```python
print(lower_case("This costs 15 Shekels"))  # this costs 15 shekels
print(index_of("clearly", "l"))             # 1
print(index_of("clearly", "l", 3))          # 5
print(last_index_of("clearly", "l"))        # 5
print(contains("unhappy", "happy"))         # True
print(contains("historical", "story"))      # False
print(compare_to("apple", "banana"))        # -1
print(compare_to("apple", "Banana"))        # 1
print(compare_to("date", "dark"))           # 1
print(hash_code("abc"))                     # 5538
```
Implementation notes:
- lower_case: the capital letters A–Z have the codes 65 to 90, and the small letters a–z have the codes 97 to 122 (lecture 3-1). So the code of a small letter is the code of its capital plus 32. Build the result with the accumulator pattern.
- index_of has a default value for start (lecture 4-1). index_of("clearly", "l") searches from position 0 and returns 1. index_of("clearly", "l", 3) searches from position 3 and returns 5.
- last_index_of: a loop can run backwards, for example range(len(s) - 1, -1, -1) (lecture 2-2).
- contains: try each position in s1 where s2 could start, and there compare the characters of s2 one by one. break can make the inner loop simpler. Test with contains("aaab", "aab"), which is True. The empty string appears in every string, so contains("abc", "") is True.
- compare_to: dictionary order, as in lecture 3-1. Compare the characters from the left, one pair at a time. At the first pair that is different, the string with the smaller character comes first. If all the characters of the shorter string match, the shorter string comes first: "abc" comes before "abcd". Capital and small letters are different characters: compare them by their codes, as they are, without changing them to lower case. All capitals (codes 65 to 90) come before all small letters (97 to 122), so compare_to("Zoo", "zoo") is −1 and compare_to("apple", "Banana") is 1. Don't compare the two whole strings with <: that is the work the function does.
- hash_code(s): for a string of length n, the hash code is ord(s[0]) × 7n−1 + ord(s[1]) × 7n−2 + ... + ord(s[n−2]) × 7 + ord(s[n−1]). For example, hash_code("abc") is 97 × 49 + 98 × 7 + 99 = 5538, and the hash code of "" is 0. It can be computed the same way as binary to decimal in lecture 2-2 (value = value * 2 + digit), with 7 instead of 2 and the code of the character instead of the digit. Later in the course we will see what hash codes are used for.
### Testing your functions
First test each function yourself, with the calls at the bottom of the file and with calls of your own. Then run the tester, from the HW4 folder:
```python
% python test_hw4.py
```
It checks the rules, calls each function with several arguments and prints PASS or FAIL for each call; for a FAIL it shows the expected value and the value your function returned. Passing all the tests doesn't guarantee full points: the graders run other tests too, and they read your code.
### Submission
Before you submit, make sure your code follows the course's coding style guidelines. Submit on the course's Moodle page, in the Homework 4 assignment. Upload these files only:
```python
algebra.py
my_string.py
```
function | returns | Assumes | points
plus(x1, x2) | x1 + x2 | nothing | 5
minus(x1, x2) | x1 − x2 | nothing | 5
times(x1, x2) | x1 × x2 | nothing | 6
power(x, n) | x to the power of n | n ≥ 0 | 6
div(x1, x2) | the whole part of x1 / x2 | x1 ≥ 0 and x2 > 0 | 6
mod(x1, x2) | the remainder of x1 / x2 | x1 ≥ 0 and x2 > 0 | 6
sqrt(x) | the whole part of √x | x ≥ 0 | 6
function | returns | similar to | points
lower_case(s) | a copy of s in which every capital letter A–Z is made small; all other characters stay as they are | s.lower() | 8
index_of(s, ch, start=0) | the first position of the character ch in s, searching from position start on; −1 if there is none | s.find(ch, start) | 10
last_index_of(s, ch) | the last position of the character ch in s; −1 if there is none | s.rfind(ch) | 8
contains(s1, s2) | True if s2 appears in s1, its characters one after the other; otherwise False | s2 in s1 | 14
compare_to(s1, s2) | −1 if s1 comes before s2 in dictionary order, 0 if they are equal, 1 if s1 comes after s2. Capitals come before small letters (note 5) |  | 12
hash_code(s) | a number computed from the characters of s (see note 6) |  | 8

## From `algebra.py`

### `algebra.py`
```python
# Algebra: whole-number arithmetic, built from adding 1 and subtracting 1.
# The only arithmetic allowed in this file is adding 1, subtracting 1, and -x.


def plus(x1, x2):
    """Return x1 + x2."""
    # Replace the following statement with your code
    return 0


def minus(x1, x2):
    """Return x1 - x2."""
    # Replace the following statement with your code
    return 0


def times(x1, x2):
    """Return x1 * x2."""
    # Replace the following statement with your code
    return 0


def power(x, n):
    """Return x to the power of n. Assumes n >= 0."""
    # Replace the following statement with your code
    return 0


def div(x1, x2):
    """Return the whole part of x1 / x2. Assumes x1 >= 0 and x2 > 0."""
    # Replace the following statement with your code
    return 0


def mod(x1, x2):
    """Return the remainder of x1 / x2. Assumes x1 >= 0 and x2 > 0."""
    # Replace the following statement with your code
    return 0


def sqrt(x):
    """Return the whole part of the square root of x. Assumes x >= 0."""
    # Replace the following statement with your code
    return 0


print(plus(2, 3))          # 5
print(minus(7, 2))         # 5
print(minus(2, 7))         # -5
print(times(3, 4))         # 12
print(plus(2, times(4, 2)))  # 10
print(power(5, 3))         # 125
print(power(3, 5))         # 243
print(div(12, 3))          # 4
print(div(5, 5))           # 1
print(div(25, 7))          # 3
print(mod(25, 7))          # 4
print(mod(120, 6))         # 0
print(sqrt(36))            # 6
print(sqrt(1000))          # 31
print(sqrt(10000))         # 100
```

## From `my_string.py`

### `my_string.py`
```python
# MyString: our own versions of some string methods, written as functions.
# Rules for this file: no string methods (nothing like s.lower() or s.find()),
# no "in" as a test (for ch in s is fine), and no slicing (s[a:b]).


def lower_case(s):
    """Return a copy of s in which every capital letter A-Z is made small."""
    # Replace the following statement with your code
    return ""


def index_of(s, ch, start=0):
    """Return the first position of ch in s, from position start on, or -1."""
    # Replace the following statement with your code
    return 0


def last_index_of(s, ch):
    """Return the last position of ch in s, or -1."""
    # Replace the following statement with your code
    return 0


def contains(s1, s2):
    """Return True if s2 appears in s1, and False otherwise."""
    # Replace the following statement with your code
    return False


def compare_to(s1, s2):
    """Return -1 if s1 comes first in dictionary order, 0 if equal, else 1.

    Characters are compared by their codes, so capitals come before small
    letters: "Zoo" comes before "zoo", and "Banana" before "apple".
    """
    # Replace the following statement with your code
    return 0


def hash_code(s):
    """Return the hash code of s (the assignment, Part B, note 6)."""
    # Replace the following statement with your code
    return 0


print(lower_case("UnHappy"))                # unhappy
print(lower_case("This costs 15 Shekels"))  # this costs 15 shekels
print(index_of("clearly", "l"))             # 1
print(index_of("clearly", "l", 3))          # 5
print(index_of("clearly", "z"))             # -1
print(last_index_of("clearly", "l"))        # 5
print(contains("unhappy", "happy"))         # True
print(contains("historical", "story"))      # False
print(compare_to("apple", "banana"))        # -1
print(compare_to("abc", "abcd"))            # -1
print(compare_to("Zoo", "zoo"))             # -1
print(compare_to("apple", "Banana"))        # 1
print(compare_to("date", "dark"))           # 1
print(hash_code("abc"))                     # 5538
```


# Instructor's notes for the tutor (guidance only: do not quote these to the student as an answer)

# HW4 notes for the tutor

Given after lecture 4-2 (Functions, part 2). Students may use everything up to lecture 4-2: loops, if, strings
(indexing, len, ord, chr, comparing characters), and writing functions (def, parameters, return, default
values, keyword arguments, functions calling functions, docstrings, stubs, assert). Not allowed (the tester checks): lists, sorted,
reversed, split, join, min, max, sum, imports, and any method call. Give hints, not code.

Both files are libraries: each function already has its name, parameters, docstring and a stub body.
The functions get arguments and return a value; they don't read input or print.

## Part A: algebra.py
Rule: the only arithmetic allowed is adding or subtracting 1 (`x += 1`, `x = x + 1`, `x -= 1`,
`x = x - 1`) and `-x`; `for _ in range(n)` with one argument.
Concepts: functions calling functions (each operation is built on the one before), repeating an action
n times, handling negative arguments, sequential search for sqrt (lecture 3-2).
Hint ladder: write plus for positive x2 first; then ask what adding a negative number means; for times,
ask how 3 × 4 can be written with additions; for div, how many times 7 can be subtracted from 25; for
sqrt, which g is the answer for x = 35.
Usual problems: negative arguments give wrong results (a loop over range of a negative number does
nothing); power(x, 0); sqrt off by one; writing everything with += 1 instead of calling the earlier
functions.

## Part B: my_string.py
Rule: no string methods, no `in` / `not in` as a test (`for ch in s` is fine), no slicing.
Concepts: functions vs. methods (lectures 3-1 and 4-2), default parameter values (index_of's start), character
codes with ord and chr (lecture 3-1), backwards loops (lecture 2-2), nested loops with break, dictionary
order (lecture 3-1), the "value = value * base + digit" pattern from binary to decimal (lecture 2-2).
Hint ladder: start from the examples in the statement and the calls at the bottom of the file; for
lower_case, ask what the codes of "A" and "a" are; for contains, ask at which positions s2 could start;
for compare_to, ask what decides the order of "abc" and "abcd", and of "Zoo" and "zoo" (letters
are compared by their codes, without changing case); for hash_code, compute "abc" by hand.
Usual problems: lower_case changing digits or spaces; index_of ignoring start; a backwards loop that
misses position 0; contains running past the end of s1, or failing on contains("aaab", "aab");
compare_to returning 0 when one string is the start of the other, or changing the case
of the letters before comparing.
