# Recitation, week 5: Tables, dictionaries and sets

## From `recitation 5.pptx`

## Slide 1
```python
[:]
```
PYTHON COURSE · WEEK 5 · RECITATION 5
Recitation 5
Lists, tuples and tables

## Slide 2
Recitation overview
Warm-up
Comprehensions
Lists
Records
Boards
Extra
Wrap-up
1
Predictions
aliasing, None, comprehensions, and the grid trap
2
One-liners
loops to comprehensions, pairs, and zip
3
Lists and records
mutate or return; a grade book from tuples
4
Boards
tic-tac-toe, in four functions

## Slide 3
Warm-up: lists
Warm-up
Comprehensions
Lists
Records
Boards
Extra
Wrap-up
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

## Slide 4
Warm-up: comprehensions and grids
Warm-up
Comprehensions
Lists
Records
Boards
Extra
Wrap-up
WARM-UP · 4 MIN
Six printed lines. One of them is the most common 2D-list bug there is.
`warmup_grids.py`
```python
nums = [3, 8, 1, 6]
print([x * 2 for x in nums])
print([x for x in nums if x > 2])
words = ["a", "bb", "c"]
print(len([w for w in words if len(w) == 1]))

grid = [[0] * 2] * 2
grid[0][0] = 7
print(grid)
rows = [[0] * 2 for _ in range(2)]
rows[0][0] = 7
print(rows)
print([row[1] for row in rows])
```
```python
The answers
[6, 16, 2, 12]
[3, 8, 6]
2
[[7, 0], [7, 0]]  (one row, two names)
[[7, 0], [0, 0]]
[0, 0]  (column 1)
```

## Slide 5
Exercise 1: Loops to comprehensions
Warm-up
Comprehensions
Lists
Records
Boards
Extra
Wrap-up
EASY · 6 MIN ON YOUR OWN
Task: each of these builds a list with a loop. Rewrite it as one comprehension.
The squares of the odd numbers below 12
The lengths of the words in a list
The words longer than three letters, in uppercase
Column 2 of a table - and then: which one of the four should stay a loop?
```python
terminal
```
```python
[1, 9, 25, 49, 81, 121]
[3, 4, 2, 5, 5]
['RAIN', 'SPAIN', 'FALLS']
[4, 4, 3]
```
Think about
Read from the middle: the loop, then the value, then an if that keeps some items
A loop that prints is not building a list

## Slide 6
Exercise 1: one solution
`comprehensions.py`
```python
words = ["the", "rain", "in", "spain", "falls"]
table = [[4, 5, 4], [5, 3, 4], [3, 4, 3]]

squares = [k * k for k in range(1, 12, 2)]
lengths = [len(w) for w in words]
loud = [w.upper() for w in words if len(w) > 3]
column = [row[2] for row in table]

print(squares)
print(lengths)
print(loud)
print(column)
```
```python
Four shapes
Source: range(1, 12, 2) supplies the odd numbers - no if needed
A call in the value: len(w) for each word
Transform and filter: the value changes the item, the if keeps some
A column: row[2] from every row, in one line
```

## Slide 7
Exercise 1: the run
`comprehensions.py`
```python
words = ["the", "rain", "in", "spain", "falls"]
table = [[4, 5, 4], [5, 3, 4], [3, 4, 3]]

squares = [k * k for k in range(1, 12, 2)]
lengths = [len(w) for w in words]
loud = [w.upper() for w in words if len(w) > 3]
column = [row[2] for row in table]

print(squares)
print(lengths)
print(loud)
print(column)
```
`python comprehensions.py`
```python
[1, 9, 25, 49, 81, 121]
[3, 4, 2, 5, 5]
['RAIN', 'SPAIN', 'FALLS']
[4, 4, 3]
```

## Slide 8
Exercise 2: Pairs
Warm-up
Comprehensions
Lists
Records
Boards
Extra
Wrap-up
EASY · 5 MIN ON YOUR OWN
Task: two lists. Pair the items that sit at the same position, as a list of tuples.
```python
pairs(a, b) returns [(a[0], b[0]), (a[1], b[1]), ...]
Different lengths: pair as far as the shorter list goes
Without zip. If you know it, do not use it yet - a loop over positions, or a comprehension
```
```python
the REPL
```
```python
>>> names = ["dana", "ron"]
>>> grades = [88, 95]
>>> pairs(names, grades)
[('dana', 88), ('ron', 95)]
>>> pairs([1, 2, 3], ["a", "b"])
[(1, 'a'), (2, 'b')]
```
```python
Think about
Position i of both lists: a[i] and b[i] - a loop over range(len(a))
A tuple is built with parentheses: (a[i], b[i])
```

## Slide 9
Exercise 2: one solution
`pairs.py`
```python
def pairs(a, b):
    """Pair a[i] with b[i]; the shorter wins."""
    result = []
    for i in range(min(len(a), len(b))):
        result.append((a[i], b[i]))
    return result

names = ["dana", "ron", "omer"]
grades = [88, 95, 51]
for name, grade in pairs(names, grades):
    print(name, grade)
print(pairs([1, 2, 3], ["a", "b"]))
```
```python
Reading it
Positions, not items: range(...) because the same i must reach both lists
The shorter wins: min(len(a), len(b)) keeps b[i] inside b
Double parentheses: append((a[i], b[i])) - the inner pair packs the tuple
Unpacking the result: for name, grade in pairs(...) reads like the records of lecture 4-2
```

## Slide 10
Exercise 2: the run
`pairs.py`
```python
def pairs(a, b):
    """Pair a[i] with b[i]; the shorter wins."""
    result = []
    for i in range(min(len(a), len(b))):
        result.append((a[i], b[i]))
    return result

names = ["dana", "ron", "omer"]
grades = [88, 95, 51]
for name, grade in pairs(names, grades):
    print(name, grade)
print(pairs([1, 2, 3], ["a", "b"]))
```
`python pairs.py`
```python
dana 88
ron 95
omer 51
[(1, 'a'), (2, 'b')]
```

## Slide 11
Meet zip
```python
Python has this function built in. Think of a zipper, not a zip file.
zip(a, b) pairs the items at matching positions
It stops at the shorter list, like our min()
Lazy: list(zip(a, b)) shows the pairs; a for loop walks them
for name, grade in zip(names, grades): - no index in sight
Several lists: zip(a, b, c) gives triples
```
Rule of thumb:
walking two lists side by side? zip. Needing the position number itself? range(len(...)).

## Slide 12
Exercise 2, with zip
`pairs_zip.py`
```python
names = ["dana", "ron", "omer"]
grades = [88, 95, 51]

print(zip(names, grades))
print(list(zip(names, grades)))

for name, grade in zip(names, grades):
    print(name, grade)

print(list(zip([1, 2, 3], ["a", "b"])))
```
```python
The same task, by name
One call: zip(names, grades) replaces the loop, the index and the min()
Lazy: the first print shows a zip object, not the pairs; list() collects them
Unpacking in the header: the pairs come out one at a time, and name, grade takes each apart
The shorter wins: [1, 2, 3] with ['a', 'b'] gives two pairs, as pairs() did
```

## Slide 13
Exercise 2, with zip: the run
`pairs_zip.py`
```python
names = ["dana", "ron", "omer"]
grades = [88, 95, 51]

print(zip(names, grades))
print(list(zip(names, grades)))

for name, grade in zip(names, grades):
    print(name, grade)

print(list(zip([1, 2, 3], ["a", "b"])))
```
`python pairs_zip.py`
```python
<zip object at 0x...>
[('dana', 88), ('ron', 95), ('omer', 51)]
dana 88
ron 95
omer 51
[(1, 'a'), (2, 'b')]
```

## Slide 14
Exercise 3: Mutate or return?
Warm-up
Comprehensions
Lists
Records
Boards
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

## Slide 15
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

## Slide 16
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

## Slide 17
Exercise 4: The grade book
Warm-up
Comprehensions
Lists
Records
Boards
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

## Slide 18
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

## Slide 19
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

## Slide 20
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

## Slide 21
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

## Slide 22
Exercise 5: Tic-tac-toe
Warm-up
Comprehensions
Lists
Records
Boards
Extra
Wrap-up
MID · 12 MIN ON YOUR OWN
Task: the board is a 3 x 3 list of lists. Write the four functions a game needs.
```python
make_board(): a fresh 3 x 3 board of dots
show(board): one row per line
place(board, r, c, mark): writes the mark if the cell is free; returns True or False
winner(board): X, O or None - three in a row, column or diagonal
```
```python
terminal
```
```python
. . .
. X .
O . .

place(board, 1, 1, "O") -> False

winner -> X
```
```python
Think about
A column: [board[r][c] for r in range(3)]
A line wins when its three cells are equal - and not dots
```

## Slide 23
Exercise 5: the board, show and place
```python
tictactoe.py (part 1)
```
```python
def make_board():
    """Return a 3 x 3 board of dots."""
    return [["."] * 3 for _ in range(3)]

def show(board):
    """Print the board, one row per line."""
    for row in board:
        print(" ".join(row))

def place(board, r, c, mark):
    """Write mark at (r, c) if free."""
    if board[r][c] != ".":
        return False
    board[r][c] = mark
    return True
```
```python
Three small functions
make_board: a comprehension builds three separate rows; [["."] * 3] * 3 would build one row three times
show: " ".join(row) glues one row's three strings; a loop prints the rows
place: a guard, then the write; the boolean tells the caller whether the move happened
place mutates and returns a bool: a yes-or-no answer about what it did, not the board
```

## Slide 24
Exercise 5: the winner
```python
tictactoe.py (part 2)
```
```python
def winner(board):
    """Return X, O, or None."""
    lines = list(board)
    for i in range(3):
        lines.append([row[i] for row in board])
    diag = [board[i][i] for i in range(3)]
    anti = [board[i][2 - i] for i in range(3)]
    lines += [diag, anti]
    for line in lines:
        first = line[0]
        if first != "." and line == [first] * 3:
            return first
    return None
```
```python
Gather the lines, then test each
Eight lines as lists of three cells: list(board) copies the three rows; columns and diagonals are comprehensions
The diagonals: board[i][i] and board[i][2 - i] - the index arithmetic is the whole trick
The test: not a dot, and all three equal - line == [first] * 3
Two kinds of return: a mark as soon as a line is found, None after the loop
```

## Slide 25
Exercise 5: a scripted game
```python
tictactoe.py (part 3)
```
```python
board = make_board()
moves = [(1, 1, "X"), (2, 0, "O"), (0, 0, "X"),
         (1, 1, "O"), (2, 2, "X")]
for r, c, mark in moves:
    ok = place(board, r, c, mark)
    if not ok:
        print(mark, "cannot play at", (r, c))
show(board)
print("winner:", winner(board))
```
```python
Using the four functions
Moves as tuples: (row, column, mark), unpacked in the for header; (r, c) is printed as one
The refused move: O tries the centre, which X holds; place returns False and nothing changes
The diagonal: X at (0, 0), (1, 1), (2, 2) wins
Your turn: replace the list of moves with input() calls and a loop until someone wins
```

## Slide 26
Exercise 5: the run
```python
tictactoe.py (part 3)
```
```python
board = make_board()
moves = [(1, 1, "X"), (2, 0, "O"), (0, 0, "X"),
         (1, 1, "O"), (2, 2, "X")]
for r, c, mark in moves:
    ok = place(board, r, c, mark)
    if not ok:
        print(mark, "cannot play at", (r, c))
show(board)
print("winner:", winner(board))
```
`python tictactoe.py`
```python
O cannot play at (1, 1)
X . .
. X .
O . X
winner: X
```

## Slide 27
Extra 1: Minesweeper numbers
Warm-up
Comprehensions
Lists
Records
Boards
Extra
Wrap-up
EXTRA
Task: a field is a grid of * (a mine) and . (empty). Replace every dot with the number of mines around it.
```python
Around means the eight neighbours; at the edges and corners there are fewer
around(field, r, c): how many mines touch cell (r, c)
numbers(field): a new grid of strings, mines kept, dots replaced by digits
```
```python
the field, and its numbers
```
```python
*...    *100
....    2210
.*..    1*10
....    1110
```
```python
Think about
Neighbours: dr and dc from -1 to 1, in two loops
Count a neighbour only if its row and column are inside the grid
```

## Slide 28
Extra 1: counting around a cell
```python
mines.py (part 1)
```
```python
def around(field, r, c):
    """Count the mines touching cell (r, c)."""
    n = len(field)
    m = len(field[0])
    count = 0
    for dr in [-1, 0, 1]:
        for dc in [-1, 0, 1]:
            nr = r + dr
            nc = c + dc
            inside = 0 <= nr < n and 0 <= nc < m
            if inside and field[nr][nc] == "*":
                count += 1
    return count
```
```python
Eight neighbours, with bounds
The offsets: dr and dc from -1 to 1 give nine positions; the cell itself is a dot, so it never counts
inside: one chained comparison per axis, joined with and
Order matters: inside and ... tests the bounds before the index is used
field[-1] would not crash - it is the last row; the bounds check keeps the edge honest
```

## Slide 29
Extra 1: the whole field
```python
mines.py (part 2)
```
```python
def numbers(field):
    """Dots replaced by mine counts."""
    result = []
    for r in range(len(field)):
        row = ""
        for c in range(len(field[r])):
            if field[r][c] == "*":
                row += "*"
            else:
                row += str(around(field, r, c))
        result.append(row)
    return result

field = ["*...", "....", ".*..", "...."]
for row in numbers(field):
    print(row)
```
```python
Visit every cell, build a new grid
Strings as rows: field[r][c] is one character
Two accumulators: a string per row, a list for the rows; the field itself is never changed
around only for dots: the if keeps the mines
str(...): a count is a number, a row is text
```

## Slide 30
Extra 1: the run
```python
mines.py (part 2)
```
```python
def numbers(field):
    """Dots replaced by mine counts."""
    result = []
    for r in range(len(field)):
        row = ""
        for c in range(len(field[r])):
            if field[r][c] == "*":
                row += "*"
            else:
                row += str(around(field, r, c))
        result.append(row)
    return result

field = ["*...", "....", ".*..", "...."]
for row in numbers(field):
    print(row)
```
`python mines.py`
```python
*100
2210
1*10
1110
```

## Slide 31
Extra 2: Permutations
Warm-up
Comprehensions
Lists
Records
Boards
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

## Slide 32
Extra 2: is it a permutation?
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

## Slide 33
Extra 2: the inverse
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

## Slide 34
Recitation summary
Warm-up
Comprehensions
Lists
Records
Boards
Extra
Wrap-up
What we practised
Read from the middle
A comprehension: the loop, then the value, then the if.
Mutate or return
Change the argument and return None, or build and return new - never both.
Records
A list of tuples; unpack in the for header; carry a whole tuple in a maximum.
Separate rows
Build a grid with a comprehension; [[x] * m] * n is one row repeated.
Tools we used
Lists
append, pop(i), [x] * n, in, not in, slicing copies, len, sum, min, max, sorted
Tuples
packing, unpacking, (name, grade) records, min(a, b) for a cap
Tables
board[r][c], rows as lists or strings, bounds checks, join to print
zip
zip(a, b) pairs matching positions, stops at the shorter; list(zip(...))

## Slide 35
Self practice
AT HOME
Write a program for each of these.
Rotate
rotate(nums, k) returns a new list with the last k items moved to the front: [1, 2, 3, 4, 5] by 2 gives [4, 5, 1, 2, 3]. Slices do all the work.
Merge
merge(a, b) returns one sorted list from two sorted lists, walking both with an index - never using sort or sorted.
Symmetric
is_symmetric(m) returns True when a square matrix equals its transpose - with two loops, and then in one line with the lecture's transpose.
A module of text tools
textstats.py: word_count, longest_word and unique_words (the distinct words, in order of first appearance), each a few lines over text.lower().split(); use them from a second file.

## Slide 36
PYTHON COURSE · WEEK 6 · RECITATION 6
Next: Dictionaries, sets and files
counting by key, membership, and text from a file

## From `anagrams.py`

### `anagrams.py`
```python
def anagram_groups(words):
    """Return sorted letters -> words."""
    groups = {}
    for word in words:
        key = "".join(sorted(word))
        if key not in groups:
            groups[key] = []
        groups[key].append(word)
    return groups

words = ["listen", "silent", "enlist",
         "google", "banana", "inlets", "elgoog"]
for group in anagram_groups(words).values():
    if len(group) > 1:
        print(" ".join(group))
```

## From `comprehensions.py`

### `comprehensions.py`
```python
words = ["the", "rain", "in", "spain", "falls"]
table = [[4, 5, 4], [5, 3, 4], [3, 4, 3]]

squares = [k * k for k in range(1, 12, 2)]
lengths = [len(w) for w in words]
loud = [w.upper() for w in words if len(w) > 3]
column = [row[2] for row in table]

print(squares)
print(lengths)
print(loud)
print(column)
```

## From `enrolments.py`

### `enrolments.py`
```python
enrolled = {
    "dana": {"python", "calculus", "physics"},
    "ron": {"python", "calculus"},
    "omer": {"python", "art"},
    "yael": {"art", "python"},
}
courses = ["python", "calculus", "physics",
           "art", "history"]

both = []
for name, taken in enrolled.items():
    if {"python", "calculus"} <= taken:
        both.append(name)
print("both:", sorted(both))

union = set()
for taken in enrolled.values():
    union |= taken
print("nobody:", sorted(set(courses) - union))

names = sorted(enrolled)
best = 0
for i in range(len(names)):
    for j in range(i + 1, len(names)):
        a, b = names[i], names[j]
        shared = len(enrolled[a] & enrolled[b])
        if shared > best:
            best = shared
            pair = (a, b)
print("most shared:", pair[0], pair[1], best)

for i in range(len(names)):
    for j in range(i + 1, len(names)):
        a, b = names[i], names[j]
        if enrolled[a] == enrolled[b]:
            print("same:", a, b)
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

## From `letters.py`

### `letters.py`
```python
def letter_counts(text):
    """Return a dict of letter -> count."""
    counts = {}
    for ch in text.lower():
        if ch.isalpha():
            counts[ch] = counts.get(ch, 0) + 1
    return counts

text = input("text: ")
counts = letter_counts(text)
for letter in sorted(counts):
    print(letter, counts[letter])
best = ""
for letter, count in counts.items():
    if best == "" or count > counts[best]:
        best = letter
print("most frequent:", best)
```

## From `mines.py`

### `mines.py`
```python
def around(field, r, c):
    """Count the mines touching cell (r, c)."""
    n = len(field)
    m = len(field[0])
    count = 0
    for dr in [-1, 0, 1]:
        for dc in [-1, 0, 1]:
            nr = r + dr
            nc = c + dc
            inside = 0 <= nr < n and 0 <= nc < m
            if inside and field[nr][nc] == "*":
                count += 1
    return count

def numbers(field):
    """Dots replaced by mine counts."""
    result = []
    for r in range(len(field)):
        row = ""
        for c in range(len(field[r])):
            if field[r][c] == "*":
                row += "*"
            else:
                row += str(around(field, r, c))
        result.append(row)
    return result

field = ["*...", "....", ".*..", "...."]
for row in numbers(field):
    print(row)
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

## From `pairs.py`

### `pairs.py`
```python
def pairs(a, b):
    """Pair a[i] with b[i]; the shorter wins."""
    result = []
    for i in range(min(len(a), len(b))):
        result.append((a[i], b[i]))
    return result

names = ["dana", "ron", "omer"]
grades = [88, 95, 51]
for name, grade in pairs(names, grades):
    print(name, grade)
print(pairs([1, 2, 3], ["a", "b"]))
```

## From `pairs_zip.py`

### `pairs_zip.py`
```python
names = ["dana", "ron", "omer"]
grades = [88, 95, 51]

print(zip(names, grades))
print(list(zip(names, grades)))

for name, grade in zip(names, grades):
    print(name, grade)

print(list(zip([1, 2, 3], ["a", "b"])))
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

## From `positions.py`

### `positions.py`
```python
def positions(text):
    """Return word -> list of its positions."""
    where = {}
    words = text.lower().split()
    for i in range(len(words)):
        w = words[i]
        if w not in where:
            where[w] = []
        where[w].append(i)
    return where

text = "the cat saw the dog"
print(positions(text))
```

## From `tictactoe.py`

### `tictactoe.py`
```python
def make_board():
    """Return a 3 x 3 board of dots."""
    return [["."] * 3 for _ in range(3)]

def show(board):
    """Print the board, one row per line."""
    for row in board:
        print(" ".join(row))

def place(board, r, c, mark):
    """Write mark at (r, c) if free."""
    if board[r][c] != ".":
        return False
    board[r][c] = mark
    return True

def winner(board):
    """Return X, O, or None."""
    lines = list(board)
    for i in range(3):
        lines.append([row[i] for row in board])
    diag = [board[i][i] for i in range(3)]
    anti = [board[i][2 - i] for i in range(3)]
    lines += [diag, anti]
    for line in lines:
        first = line[0]
        if first != "." and line == [first] * 3:
            return first
    return None

board = make_board()
moves = [(1, 1, "X"), (2, 0, "O"), (0, 0, "X"),
         (1, 1, "O"), (2, 2, "X")]
for r, c, mark in moves:
    ok = place(board, r, c, mark)
    if not ok:
        print(mark, "cannot play at", (r, c))
show(board)
print("winner:", winner(board))
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

## From `warmup_dicts.py`

### `warmup_dicts.py`
```python
d = {"a": 1, "b": 2}
d["c"] = 3
d["a"] = 10
print(d)
print("b" in d, 2 in d)
print(d.get("z", 0))
print(len(d), sorted(d))
print(sum(d.values()))
s = set("banana")
print(len(s), sorted(s))
print({1, 2, 3} & {2, 3, 4}, {1, 2} <= {1, 2, 3})
print(d["z"])
```

## From `warmup_grids.py`

### `warmup_grids.py`
```python
nums = [3, 8, 1, 6]
print([x * 2 for x in nums])
print([x for x in nums if x > 2])
words = ["a", "bb", "c"]
print(len([w for w in words if len(w) == 1]))

grid = [[0] * 2] * 2
grid[0][0] = 7
print(grid)
rows = [[0] * 2 for _ in range(2)]
rows[0][0] = 7
print(rows)
print([row[1] for row in rows])
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
