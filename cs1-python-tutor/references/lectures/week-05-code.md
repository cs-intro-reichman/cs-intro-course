# Week 5 code files

The code files shown in the week 5 lectures.

### `animal_sounds.py`
```python
sounds = {"cow": "moo", "dog": "woof"}

print("A cow goes", sounds["cow"])
sounds["cat"] = "miao"     # adds
sounds["dog"] = "bark"     # replaces
print(sounds)
print(len(sounds))
```

### `column_averages.py`
```python
ratings = [[4, 5, 4, 5, 4],
           [5, 3, 4, 4, 4],
           [3, 4, 3, 5, 3]]
rows = len(ratings)
cols = len(ratings[0])

# the average rating of each movie (a column)
for col in range(cols):
    total = 0
    for row in range(rows):
        total = total + ratings[row][col]
    print(f"movie {col}: {round(total / rows, 2)}")
```

### `format_specs.py`
```python
# [ ] mark the edges of each value
x = 7
r = 2 / 3
n = 1234567
name = "Dana"
print(f"[{x}]")         # [7]
print(f"[{x:4}]")       # [   7]
print(f"[{r:.3f}]")     # [0.667]
print(f"[{r:7.3f}]")    # [  0.667]
print(f"[{n:,}]")       # [1,234,567]
print(f"[{n:>12,}]")    # [   1,234,567]
print(f"[{name:6}]")    # [Dana  ]
```

### `grid_trap.py`
```python
board = [["."] * 3] * 3      # looks like a 3 x 3 grid
board[1][1] = "X"
for row in board:
    print(" ".join(row))

print(board[0] is board[2])
```

### `group_by_letter.py`
```python
words = ["apple", "banana", "avocado",
         "cherry", "blueberry"]

groups = {}
for w in words:
    first = w[0]
    if first not in groups:
        groups[first] = []      # a new, empty list
    groups[first].append(w)

for letter, group in groups.items():
    print(letter, group)
```

### `iterate_dict.py`
```python
sounds = {"cow": "moo", "dog": "woof", "cat": "miao"}

for animal in sounds:
    print(f"{animal} goes {sounds[animal]}")

for animal, sound in sounds.items():
    print(f"{sound} is the sound of a {animal}")

print(list(sounds.keys()))
print(list(sounds.values()))
```

### `make_grid.py`
```python
def make_grid(rows, cols, value):
    """Return a rows x cols grid filled with value."""
    grid = []
    for i in range(rows):
        grid.append([value] * cols)
    return grid

board = make_grid(3, 3, ".")
board[1][1] = "X"
for row in board:
    print(" ".join(row))
```

### `matrix_add.py`
```python
def add(m1, m2):
    """Return m1 + m2. Assumes equal dimensions."""
    result = []
    for i in range(len(m1)):
        row = []
        for j in range(len(m1[0])):
            row.append(m1[i][j] + m2[i][j])
        result.append(row)
    return result
```

### `matrix_demo.py`
```python
from matrix_add import add
from matrix_mult import mult
from matrix_print import print_matrix

a = [[7, 2, 1],
     [3, 6, 1],
     [5, 1, 4]]
b = [[8, 3, 5],
     [1, 4, 1],
     [1, 3, 4]]

print_matrix(add(a, b))
print_matrix(mult(a, b))
print_matrix(mult(a, add(a, b)))   # a x (a + b)
```

### `matrix_mult.py`
```python
def mult(m1, m2):
    """Return m1 x m2. Assumes len(m1[0]) == len(m2)."""
    rows = len(m1)
    cols = len(m2[0])
    inner = len(m2)
    result = []
    for i in range(rows):
        row = []
        for j in range(cols):
            total = 0
            for k in range(inner):
                total = total + m1[i][k] * m2[k][j]
            row.append(total)
        result.append(row)
    return result
```

### `matrix_print.py`
```python
def print_matrix(m):
    """Print m row by row, then a blank line."""
    for row in m:
        for x in row:
            print(f"{x:5}", end="")
        print()
    print()
```

### `membership_speed.py`
```python
import time

numbers = list(range(1000000))
as_set = set(numbers)

start = time.perf_counter()
found = 999999 in numbers
ms = (time.perf_counter() - start) * 1000
print(f"list: {round(ms, 4)} ms")

start = time.perf_counter()
found = 999999 in as_set
ms = (time.perf_counter() - start) * 1000
print(f"set:  {round(ms, 4)} ms")
```

### `missing_key.py`
```python
sounds = {"cow": "moo", "dog": "woof"}

print("cat" in sounds)
print(sounds.get("cat"))
print(sounds.get("cat", "???"))
print(sounds["cat"])
```

### `print_table.py`
```python
ratings = [[4, 5, 4, 5, 4],
           [5, 3, 4, 4, 4],
           [3, 4, 3, 5, 3]]

for row in range(len(ratings)):
    for col in range(len(ratings[row])):
        print(f"{ratings[row][col]:4}", end="")
    print()
```

### `ratings.py`
```python
# rows are reviewers, columns are movies
ratings = [[4, 5, 4, 5, 4],
           [5, 3, 4, 4, 4],
           [3, 4, 3, 5, 3]]

print(ratings[1][2])     # reviewer 1, movie 2
print(ratings[1])        # all of row 1
print(len(ratings))      # number of rows
print(len(ratings[0]))   # number of columns
```

### `set_basics.py`
```python
s1 = set()
s1.add(3)
s1.add(1)
s1.add(3)              # already there: no change
s1.add(5)
s1.add(7)
s2 = set([7, 9, 1, 9, 1, 7])

print(s1)
print(s2)
print(3 in s1, 4 in s1)
print(len(s2))
```

### `set_ops.py`
```python
s1 = {3, 1, 5, 7}
s2 = {7, 9, 1}

print(s1 | s2)       # union
print(s1 & s2)       # intersection
print(s1 - s2)       # difference
print({1, 7} <= s1)  # subset
```

### `sum_of_rows.py`
```python
import random

table = []
for i in range(5):            # 5 rows of 3 random values
    row = []
    for j in range(3):
        row.append(random.randint(0, 19))
    table.append(row)

for row in table:             # add each row's sum at its end
    row.append(sum(row))

for row in table:
    for x in row:
        print(f"{x:4}", end="")
    print()
```

### `transpose.py`
```python
def transpose(m):
    """Return m with its rows and columns swapped."""
    result = []
    for col in range(len(m[0])):
        new_row = []
        for row in range(len(m)):
            new_row.append(m[row][col])
        result.append(new_row)
    return result

sales = [[10, 12, 20, 12],
         [12, 14, 25, 18]]
for row in transpose(sales):
    print(row)
```

### `tuple_keys.py`
```python
names = {(0, 0): "corner", (1, 1): "centre"}
print(names[(1, 1)])

names[(0, 2)] = "corner"
print(len(names))

bad = {[0, 0]: "corner"}
```

### `two_courses.py`
```python
intro = {"maya", "noam", "dana", "yoni"}
calculus = {"dana", "omer", "maya"}

print(sorted(intro & calculus))    # in both
print(sorted(intro - calculus))    # intro only
print(len(intro | calculus))       # in either

visits = ["maya", "noam", "maya", "dana", "maya"]
print(f"{len(visits)} visits, {len(set(visits))} people")
```

### `word_count.py`
```python
text = "the cat saw the dog and the dog saw the cat"

counts = {}
for word in text.split():
    if word in counts:
        counts[word] = counts[word] + 1
    else:
        counts[word] = 1

for word, n in counts.items():
    print(word, n)
```

### `word_count_get.py`
```python
text = "the cat saw the dog and the dog saw the cat"

counts = {}
for word in text.split():
    counts[word] = counts.get(word, 0) + 1

print(counts["the"], counts["dog"], counts["and"])
print(counts.get("bird", 0))
```
