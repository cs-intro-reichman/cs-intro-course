# Recitation, week 4: Functions, lists and tuples

## From `recitation 4.pptx`

## Slide 1
```python
def
```
PYTHON COURSE · WEEK 4 · RECITATION 4
Recitation 4
Functions, lists and tuples

## Slide 2
Recitation overview
Warm-up
Functions
Design
Lists
Records
Extra
Wrap-up
1
Predictions
aliasing, None, and tuples
2
Functions
small, named, tested in the REPL
3
Lists
mutate or return, and an alias trap
4
Records
a grade book from tuples, and a module

## Slide 3
Warm-up: functions
Warm-up
Functions
Design
Lists
Records
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
Warm-up: lists
WARM-UP · 4 MIN
Six printed lines. Two of them are traps from lecture 4-2 - which two?
`warmup_lists.py`
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
The answers
[1, 2, 3, 4]   (b is a second name, not a copy)
[1, 2, 3, 4] [99, 2, 3, 4]   (a slice is a copy)
None   (sort changes a and returns nothing)
[1, 2, 3, 4]
2 1
[1, 2, 3] [0, 0, 0]

## Slide 5
Exercise 1: Three small functions
Warm-up
Functions
Design
Lists
Records
Extra
Wrap-up
EASY · 8 MIN ON YOUR OWN
Task: three small functions, each with a docstring, tested in the REPL.
```python
is_even(n): True when n is even
average(nums): the average; 0.0 for an empty list
count_above(nums, limit): how many values exceed limit
Save as small_functions.py; import and call in the REPL
```
```python
the REPL
```
```python
>>> import small_functions as sf
>>> sf.is_even(7)
False
>>> sf.average([80, 90, 100])
90.0
>>> sf.count_above([3, 8, 12, 5], 4)
3
```
Think about
return a value; never print inside these functions
The empty list needs a guard before dividing

## Slide 6
Exercise 1: one solution
`small_functions.py`
```python
def is_even(n):
    """Return True when n is even."""
    return n % 2 == 0

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
```
```python
Three shapes of function
A one-liner: the comparison is the value, so return n % 2 == 0 is the whole body
A guard: return early for the empty list, then the normal case - two returns, one runs
An accumulator: count in a loop, return after the loop; return inside the loop would stop at the first hit
Docstrings: the first line of the body, in triple quotes, says what comes back
```

## Slide 7
Exercise 2: Design before code
Warm-up
Functions
Design
Lists
Records
Extra
Wrap-up
MID · 10 MIN ON YOUR OWN
Task: read one line of whole numbers. Report the largest, the smallest, the average, and how many are above average.
First the design: name the functions, give each a signature and a docstring
Then stubs, so the program runs end to end with wrong answers
Then the bodies, one at a time, each tested in the REPL
```python
terminal
```
```python
Numbers: 12 7 30 5 18
Largest: 30
Smallest: 5
Average: 14.4
Above average: 2
```
```python
Think about
split() gives strings; int() each piece into a new list
Two of the pieces are exercise 1, unchanged
```

## Slide 8
The idea: the pieces, then the diagram
Ask what main needs to know, and name a function for each answer.
1 · read_numbers() - reads the line, splits it, turns every piece into an int, returns the list
2 · average(nums) - exercise 1, unchanged
3 · count_above(nums, limit) - exercise 1, unchanged
4 · max and min - already exist; no function to write
5 · main - calls the pieces and prints the report; it is the only part that prints
The design, written down
read_numbers: returns a list of ints, from one line of input
average: returns a float, 0.0 for an empty list
count_above: returns an int, how many are above limit
main calls all three: the arrows in the diagram point down from main

## Slide 9
Exercise 2: the stubs
`report_stubs.py`
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
```python
It runs, and it is wrong
Every function has its real name, parameters and docstring - and a placeholder body
The program runs end to end: the shape is checked before any hard part is written
This version crashes on max([]) - a stub that returns an empty list exposes the empty case early
Next: fill in one body, run, fill in the next
```

## Slide 10
Exercise 2: the bodies (1 of 2)
```python
report.py (lines 1-6)
```
```python
def read_numbers():
    """Return the ints typed on one line."""
    nums = []
    for piece in input("Numbers: ").split():
        nums.append(int(piece))
    return nums

# average and count_above: exercise 1, unchanged
```
```python
read_numbers, the only new body
split(): one line of text becomes a list of strings, on whitespace
int() each piece: the list that comes back holds numbers, not text
The accumulator for lists: start empty, append in the loop, return after it
The for header: input(...).split() is evaluated once, before the loop starts
```

## Slide 11
Exercise 2: the bodies (2 of 2)
```python
report.py (lines 22-31)
```
```python
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
```python
main: the only part that prints
The guard: the empty line is handled once, at the top, so no function has to
mean is computed once and used twice: printed, and passed as the limit
Built-ins and our functions side by side: max(nums) and average(nums) are called the same way
Two passes over the data: the average must be known before anything can be counted above it
```

## Slide 12
Exercise 2: the run
```python
report.py (lines 22-31)
```
```python
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
```python
python report.py (lines 22-31)
```
```python
Numbers: 12 7 30 5 18
Largest: 30
Smallest: 5
Average: 14.4
Above average: 2
```

## Slide 13
Exercise 3: Mutate or return?
Warm-up
Functions
Design
Lists
Records
Extra
Wrap-up
MID · 10 MIN ON YOUR OWN
Task: remove the negative numbers from a list - twice, in the two ways a function can do it.
```python
remove_negatives(nums) changes the list it is given and returns None
without_negatives(nums) leaves its argument alone and returns a new list
Test both on the same list and print it after each call. What is different?
```
```python
the REPL
```
```python
>>> a = [3, -1, 4, -5, 9]
>>> b = without_negatives(a)
>>> b, a
([3, 4, 9], [3, -1, 4, -5, 9])
>>> remove_negatives(a)
>>> a
[3, 4, 9]
```
```python
Think about
Removing inside a for skips items: use a while with an index and pop(i)
The new-list version is the kept-list pattern
```

## Slide 14
Exercise 3: one solution
`negatives.py`
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
```python
Two contracts
In place: no return - the parameter is a second name for the caller's list
The index advances only when nothing was removed: after pop(i) the next item is already at i
New list: the argument is never touched; the kept list is built and returned
Never both: changing the argument and returning a result confuses every caller
```

## Slide 15
Noa's version does both. What goes wrong?
It mutates and returns. Predict the three prints.
`noa.py`
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
`using_noa.py`
```python
from noa import cleaned

scores = [3, -1, 4, -5, 9]
good = cleaned(scores)
print(good)
print(scores)
good.append(100)
print(scores)
```
```python
[3, 4, 9], then [3, 4, 9] again - scores changed, which the name never suggested. Then [3, 4, 9, 100]: good and scores are one list.
The rule: mutate and return None, or build and return new - never both.
```

## Slide 16
Exercise 4: The grade book
Warm-up
Functions
Design
Lists
Records
Extra
Wrap-up
HIGH · 12 MIN ON YOUR OWN
Task: a class is a list of (name, grade) tuples. Write the report functions.
```python
top_student(students): the record with the highest grade
failing(students, pass_mark): names below pass_mark; default 56
curve(students, points): new records with points added, capped at 100
add_student(students, name, grade): adds a record, in place
```
```python
the REPL
```
```python
>>> top_student(students)
('Ron Cohen', 95)
>>> failing(students)
['Omer Katz']
>>> curve(students, 10)[1]
('Ron Cohen', 100)
```
```python
Think about
Unpack in the for header: for name, grade in students:
A tuple cannot change: curve builds a new one per student
```

## Slide 17
Exercise 4: the class, and the top student
```python
gradebook.py (part 1)
```
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
```
```python
Records in, a record out
The class: a list of tuples, one tuple per student - the shape from lecture 4-2
Running maximum over records: best is a whole tuple; record[1] is the grade inside it
Returns the record, not the grade: the caller can unpack name and grade from it
Empty class: students[0] raises IndexError - a promise to state in the docstring
```

## Slide 18
Exercise 4: failing and curve
```python
gradebook.py (part 2)
```
```python
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
```
```python
Two builders
Unpacking in the header: for name, grade in students takes each tuple apart
A default: pass_mark=56 makes the second argument optional - failing(students) and failing(students, 80) both work
curve builds: a new list, and a new tuple per student - tuples cannot change, so none is
min(grade + points, 100): the cap in one call, with the built-in from lecture 4-2
```

## Slide 19
Exercise 4: add_student, and the report
```python
gradebook.py (part 3)
```
```python
def add_student(students, name, grade):
    """Add one record, in place."""
    students.append((name, grade))

add_student(students, "Noa Peretz", 64)
name, grade = top_student(students)
print(f"Top: {name} with {grade}")
print(f"Failing: {failing(students)}")
print(f"Curved: {curve(students, 10)}")
```
```python
One mutator, then main
add_student mutates: append on the caller's list, no return - the other contract
Unpacking the answer: name, grade = top_student(students) takes the returned tuple apart
The report calls the functions by name; nothing about loops appears here
Next week: looking up one student by name is what a dictionary is for
```

## Slide 20
Exercise 4: the run
```python
gradebook.py (part 3)
```
```python
def add_student(students, name, grade):
    """Add one record, in place."""
    students.append((name, grade))

add_student(students, "Noa Peretz", 64)
name, grade = top_student(students)
print(f"Top: {name} with {grade}")
print(f"Failing: {failing(students)}")
print(f"Curved: {curve(students, 10)}")
```
```python
python gradebook.py (wrapped)
```
```python
Top: Ron Cohen with 95
Failing: ['Omer Katz']
Curved: [('Dana Levi', 98),
  ('Ron Cohen', 100),
  ('Omer Katz', 61),
  ('Yael Bar', 83),
  ('Noa Peretz', 74)]
```

## Slide 21
Exercise 5: A module of text tools
Warm-up
Functions
Design
Lists
Records
Extra
Wrap-up
HIGH · 10 MIN ON YOUR OWN
Task: put four text functions in textstats.py, then use them from a second file, text_report.py.
```python
word_count, longest_word, and unique_words: the distinct words, in order of first appearance
most_common: the pair (word, count) of the most frequent word; the first on a tie
text_report.py imports the module and prints a report for one sentence
```
```python
terminal
```
```python
$ python text_report.py
Words: 8
Longest: rose
Unique: ['a', 'rose', 'is']
Top: ('a', 3)
```
```python
Think about
text.lower().split() gives the words; the rest is loops over that list
unique: append only if not in the list so far; most_common: count() per unique word
```

## Slide 22
Exercise 5: the module (1 of 2)
```python
textstats.py (part 1)
```
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
```
```python
A helper, and two users of it
A docstring for the file: the first line of the module says what it is
words_of: a helper that three other functions call - write the splitting once
longest_word: the running maximum, with len(w) as the measure
Nothing prints: a library returns values, and the user decides what to show
```

## Slide 23
Exercise 5: the module (2 of 2)
```python
textstats.py (part 2)
```
```python
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
```python
The two that need memory
unique_words: the kept-list pattern with a membership test - not in on the list built so far
most_common: a loop over the unique words, count() for each, a running maximum carrying a tuple
First on a tie: > and not >=, so an equal count never replaces the earlier winner
Returning a pair: the tuple is packed in the assignment and unpacked by the caller
```

## Slide 24
Exercise 5: the user
`text_report.py`
```python
import textstats

text = "a rose is a rose is a rose"
print("Words:", textstats.word_count(text))
print("Longest:", textstats.longest_word(text))
print("Unique:", textstats.unique_words(text))
print("Top:", textstats.most_common(text))
```
```python
The caller sees names and promises
import textstats: the file name without .py, from the same folder
Module name, dot, function: textstats.word_count(text) - the calling syntax of lecture 4-1
The report knows what, not how: nothing about split, loops or count appears here
A tie: a and rose both appear three times; the first one wins, as the docstring promised
```
`python text_report.py`
```python
Words: 8
Longest: rose
Unique: ['a', 'rose', 'is']
Top: ('a', 3)
```

## Slide 25
Extra 1: Permutations
Warm-up
Functions
Design
Lists
Records
Extra
Wrap-up
EXTRA
Task: a permutation of n holds every number from 0 to n - 1 exactly once.
```python
is_permutation(per): True for [2, 0, 1]; False for [2, 2, 0], [2, 3, 0], [0, 1, 5]
inverse(per): undoes per - if per sends 0 to 2, the inverse sends 2 to 0
Check: reorder with per, then with inverse(per), gives the list back
```
```python
the REPL
```
```python
>>> is_permutation([2, 0, 1])
True
>>> is_permutation([2, 2, 0])
False
>>> inverse([2, 0, 1])
[1, 2, 0]
```
```python
Think about
[False] * n remembers which numbers were seen
Out of range first: a value must be a valid index before it is used as one
```

## Slide 26
Extra 1: is it a permutation?
```python
permutations.py (part 1)
```
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
```
```python
A list as memory
seen: one slot per value; the value itself is the index - index-as-data, from the lecture
Two early returns: out of range, or seen before - either settles the answer
Order matters: the range check comes first, so seen[value] is only read with a valid index
A missing value is never checked: n slots, n values, no repeat - nothing can be missing
```

## Slide 27
Extra 1: the inverse
```python
permutations.py (part 2)
```
```python
def inverse(per):
    """Return the permutation undoing per."""
    inv = [0] * len(per)
    for i in range(len(per)):
        inv[per[i]] = i
    return inv
```
```python
Write at the destination
inv[per[i]] = i: per says where position i goes; the inverse records, there, where it came from
A list of the right size first: [0] * len(per), then every slot is overwritten
Trace [2, 0, 1]: 0 goes to 2, so inv[2] = 0; 1 goes to 0, so inv[0] = 1; 2 goes to 1 - giving [1, 2, 0]
A promise: with a list that is not a permutation, the result is wrong or an IndexError
```
```python
the REPL
```
```python
>>> inverse([2, 0, 1])
[1, 2, 0]
>>> is_permutation([2, 3, 0])
False
```

## Slide 28
Recitation summary
Warm-up
Functions
Design
Lists
Records
Extra
Wrap-up
What we practised
A function per job
One job, a good name, a docstring, tested alone in the REPL.
Design, stubs, bodies
Name the pieces, make it run, then fill in one body at a time.
Mutate or return
Change the argument and return None, or build and return new - never both.
Records
A list of tuples; unpack in the for header; carry a whole tuple in a maximum.
Tools we used
Functions
def, return, None, defaults, docstrings, import module, module.function()
Lists
append, pop(i), [x] * n, in, not in, slicing copies, len, sum, min, max
Tuples
packing, unpacking, (name, grade) records, min(a, b) for a cap
Strings to lists
split(), lower(), count() on a list

## Slide 29
Self practice
AT HOME
Write a program for each of these.
```python
Rotate
rotate(nums, k) returns a new list with the last k items moved to the front: [1, 2, 3, 4, 5] by 2 gives [4, 5, 1, 2, 3]. Slices do all the work.
```
```python
Second largest
second_largest(nums) returns the second largest value without sorting: two running variables, updated together.
```
```python
Merge
merge(a, b) returns one sorted list from two sorted lists, walking both with an index - never using sort or sorted.
```
```python
Run-length, as data
encode(s) returns a list of (character, count) tuples; decode(pairs) turns it back into the string. Last week's exercise, as two functions.
```

## Slide 30
PYTHON COURSE · WEEK 5 · RECITATION 5
Next: Tables, dictionaries and sets
lists of lists, dictionaries and sets

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

## From `small_functions.py`

### `small_functions.py`
```python
def is_even(n):
    """Return True when n is even."""
    return n % 2 == 0

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
