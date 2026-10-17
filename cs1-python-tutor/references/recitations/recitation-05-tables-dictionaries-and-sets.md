# Recitation, week 5: Tables, dictionaries and sets

## From `recitation 5.pptx`

## Slide 1
```python
{ }
```
PYTHON COURSE · WEEK 5 · RECITATION 5
Recitation 5
Tables, dictionaries and sets

## Slide 2
Recitation overview
Warm-up
Comprehensions
Boards
Counting
Sets
Extra
Wrap-up
1
Predictions
comprehensions, the grid trap, keys
2
Boards
tic-tac-toe, in four functions
3
Counting
letter frequencies and anagram groups
4
Sets
who takes what, in one operator

## Slide 3
Warm-up: comprehensions and grids
Warm-up
Comprehensions
Boards
Counting
Sets
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

## Slide 4
Warm-up: dictionaries and sets
WARM-UP · 4 MIN
Eight lines. Three of them are about the difference between keys and values.
`warmup_dicts.py`
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
The answers
{'a': 10, 'b': 2, 'c': 3}
True False   (in asks about keys)
0   (the default, no crash)
3 ['a', 'b', 'c']   (sorted gives the keys)
15   (the values, asked for by name)
3 ['a', 'b', 'n']
{2, 3} True
KeyError - and the program stops

## Slide 5
Exercise 1: Loops to comprehensions
Warm-up
Comprehensions
Boards
Counting
Sets
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
Exercise 2: Tic-tac-toe
Warm-up
Comprehensions
Boards
Counting
Sets
Extra
Wrap-up
MID · 14 MIN ON YOUR OWN
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

## Slide 9
Exercise 2: the board, show and place
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

## Slide 10
Exercise 2: the winner
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

## Slide 11
Exercise 2: a scripted game
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

## Slide 12
Exercise 2: the run
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

## Slide 13
Exercise 3: Letter frequencies
Warm-up
Comprehensions
Boards
Counting
Sets
Extra
Wrap-up
MID · 10 MIN ON YOUR OWN
Task: count how often each letter appears in a text, ignoring case and anything that is not a letter.
```python
letter_counts(text) returns a dictionary letter -> count
Print the counts in alphabetical order, one line each, and then the most frequent letter
Then: positions(text) returns word -> list of the positions where the word appears
```
```python
terminal
```
```python
text: banana!
a 3
b 1
n 2
most frequent: a
```
```python
Think about
Counting: counts[ch] = counts.get(ch, 0) + 1
A dict of lists: create the empty list the first time a word is seen
```

## Slide 14
Exercise 3: the counts
`letters.py`
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
```python
The counting pattern, and a maximum over items
counts.get(ch, 0) + 1: the count so far, or 0 if this letter is new - one line, no if
sorted(counts): the keys in order; the value is fetched by key inside the loop
The maximum over items: best holds a key; counts[best] is its count
best == "" seeds the maximum on the first pass; ties keep the earlier letter
```

## Slide 15
Exercise 3: the run
`letters.py`
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
`python letters.py`
```python
text: banana!
a 3
b 1
n 2
most frequent: a
```

## Slide 16
Exercise 3, expansion: a dictionary of lists
`positions.py`
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
```python
The guard pattern
A list per word: the value is a list, and it must exist before anything is appended to it
Guard, then append: if w not in where: where[w] = [] creates the list the first time; the append always runs
Index loop: the position is the index, so range(len(words)) instead of for w in words
```
```python
python positions.py (wrapped)
```
```python
{'the': [0, 3], 'cat': [1],
 'saw': [2], 'dog': [4]}
```

## Slide 17
Exercise 4: Anagram groups
Warm-up
Comprehensions
Boards
Counting
Sets
Extra
Wrap-up
HIGH · 12 MIN ON YOUR OWN
Task: group a list of words so that words made of the same letters end up together.
```python
listen, silent, enlist and inlets are one group; google and elgoog another; banana is alone
anagram_groups(words) returns a dictionary key -> list of words
Print only the groups with more than one word, one line each
```
```python
terminal
```
```python
listen silent enlist inlets
google elgoog
```
```python
Think about
Two anagrams have the same letters in sorted order: "".join(sorted(word)) is a key that both share
Dictionary of lists: the guard pattern from exercise 3
```

## Slide 18
The idea: a key that anagrams share
listen and silent have the same letters. Sort the letters and they become the same string.
```python
1 · Sort the letters - sorted("listen") is a list of characters: e, i, l, n, s, t
2 · Make it a key - "".join(...) turns the list into the string eilnst; a list cannot be a key, a string can
3 · File each word under its key - the guard creates the list, append adds the word
4 · Report - walk the dictionary; print the lists with more than one word
```
In pseudocode
groups = {}
for each word:
      key = the letters of word, sorted
      if key is new: groups[key] = []
      groups[key].append(word)
for each group with 2+ words:
      print it

## Slide 19
Exercise 4: one solution
`anagrams.py`
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
```python
Ten lines, one idea
The key: "".join(sorted(word)) - two week-4 tools make the week-5 key
The guard, then append: the dictionary-of-lists pattern
.values(): the report never needs the keys, only the lists
Insertion order: groups come out in the order their first word appeared
```

## Slide 20
Exercise 4: the run
`anagrams.py`
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
`python anagrams.py`
```python
listen silent enlist inlets
google elgoog
```

## Slide 21
Exercise 5: Enrolments
Warm-up
Comprehensions
Boards
Counting
Sets
Extra
Wrap-up
HIGH · 10 MIN ON YOUR OWN
Task: a dictionary maps each student to the set of courses they take. Four questions, one operator each.
```python
Who takes both python and calculus? Which of the listed courses does nobody take?
Which two students share the most courses? Who takes exactly the same courses?
<=, -, &, == and len() do the thinking; a loop does the walking
```
```python
terminal
```
```python
both: ['dana', 'ron']
nobody: ['history']
most shared: dana ron 2
same: omer yael
```
```python
Think about
Union of everything: start from set() and |= each student's set
Pairs: two loops over the sorted names, with the second starting after the first
```

## Slide 22
Exercise 5: the data
```python
enrolments.py (part 1)
```
```python
enrolled = {
    "dana": {"python", "calculus", "physics"},
    "ron": {"python", "calculus"},
    "omer": {"python", "art"},
    "yael": {"art", "python"},
}
courses = ["python", "calculus", "physics",
           "art", "history"]
```
The four questions
both: the students who take python and calculus
nobody: the courses in the list that no student takes
most shared: the two students with the most courses in common, and how many
same: the students whose sets of courses are equal

## Slide 23
Exercise 5: both, and nobody
```python
enrolments.py (part 2)
```
```python
both = []
for name, taken in enrolled.items():
    if {"python", "calculus"} <= taken:
        both.append(name)
print("both:", sorted(both))

union = set()
for taken in enrolled.values():
    union |= taken
print("nobody:", sorted(set(courses) - union))
```
```python
A loop walks, an operator thinks
Both: {"python", "calculus"} <= taken - subset, in one comparison
Union of all: set() is the empty set; |= adds each student's courses to it
Nobody: the courses that are not in the union - a set difference
sorted() on a set: for printing in a predictable order
```
```python
python enrolments.py (first half)
```
```python
both: ['dana', 'ron']
nobody: ['history']
```

## Slide 24
Exercise 5: pairs
```python
enrolments.py (part 3)
```
```python
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
```python
Every pair once
The pair loop: j starts at i + 1, so each pair is visited once and never with itself
Shared: len(a & b) - the intersection measured
A running maximum carrying a tuple: the pair and its count move together
Equal sets: == ignores order, so {art, python} and {python, art} match
```

## Slide 25
Exercise 5: the run
```python
enrolments.py (part 3)
```
```python
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
```python
python enrolments.py (second half)
```
```python
most shared: dana ron 2
same: omer yael
```

## Slide 26
Extra 1: Minesweeper numbers
Warm-up
Comprehensions
Boards
Counting
Sets
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

## Slide 27
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

## Slide 28
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

## Slide 29
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

## Slide 30
Recitation summary
Warm-up
Comprehensions
Boards
Counting
Sets
Extra
Wrap-up
What we practised
Read from the middle
A comprehension: the loop, then the value, then the if.
Separate rows
Build a grid with a comprehension; [[x] * m] * n is one row repeated.
Guard, then append
A dictionary of lists: create the list the first time, append always.
A key is a label
Choose it so that things that belong together share it: sorted letters.
Tools we used
Tables
board[r][c], rows as lists or strings, bounds checks, join to print
Dictionaries
d[k], in on keys, .get(k, 0), .items(), .values(), sorted(d)
Sets
set(), {a, b}, &, |, -, <=, ==, |=, sorted(set(...))
From week 4
functions with contracts, sorted, join, records as tuples

## Slide 31
Self practice
AT HOME
Write a program for each of these.
Inventory
A dictionary item -> price and a cart item -> quantity. Print the bill, one line per item, and the total; an item missing from the price list is reported, not crashed on.
```python
Invert
invert(d) turns a dictionary name -> grade into grade -> list of names. The guard pattern; test it with two students on the same grade.
```
```python
Symmetric
is_symmetric(m) returns True when a square matrix equals its transpose - with two loops, and then in one line with the lecture's transpose.
```
Coupons, counted
Run the coupon collector 1000 times and count, in a dictionary, how often each number of boxes came up. Print the five most common counts.

## Slide 32
PYTHON COURSE · WEEK 6 · RECITATION 6
Next: Files
text from outside the program

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
