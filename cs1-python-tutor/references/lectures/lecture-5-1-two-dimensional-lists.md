# Lecture 5-1: Two-dimensional lists (week 5)

## Slide 1: Two-Dimensional Lists
[i][j]
PYTHON COURSE · WEEK 5 · LECTURE 1
Two-Dimensional Lists
Data in rows and columns
Reichman University

## Slide 2: Data in rows and columns
Data in rows and columns
A lot of data comes as tables.
Ratings: reviewers down the side, movies across the top
Images: rows and columns of pixels
Sales: models down the side, quarters across
Game boards: a 3 × 3 tic-tac-toe grid

## Slide 3: A table of ratings
A table of ratings
Each value is found by two numbers: a row and a column.
4
5
4
5
4
5
3
4
4
4
3
4
3
5
3
0
1
2
3
4
0
1
2
movie (column)
reviewer (row)
row 1, column 2  →  reviewer 1 gave movie 2 a 4

## Slide 4: An image is a table
An image is a table
Each number is one pixel: 1 is dark, 0 is light.
0
0
0
0
0
0
0
0
0
0
1
1
1
1
0
0
0
0
0
1
1
1
1
0
0
0
0
0
1
1
1
1
0
0
0
0
0
0
0
0
what the list stores
what the screen shows

## Slide 5: A list of lists
A list of lists
A row: an ordinary list, like [4, 5, 4, 5, 4]
The table: a list whose items are the rows
One value: ratings[row][col], row first, then column
Its size: len(ratings) rows, len(ratings[0]) columns

## Slide 6: Writing a table in Python
Writing a table in Python
```python
python ratings.py
4
[5, 3, 4, 4, 4]
3
5
```
`ratings.py`
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
[LIVE] the file is in “week 5 code / ratings.py”.

## Slide 7: A list of lists in memory
A list of lists in memory
The outer list holds three references, one to each row.
```python
ratings
```
0
1
2
4
5
4
5
4
```python
ratings[0]
```
5
3
4
4
4
```python
ratings[1]
```
3
4
3
5
3
```python
ratings[2]
```

## Slide 8: Reading ratings[1][2]
Reading ratings[1][2]
Two indexes, two steps: first pick a row, then pick a cell.
```python
ratings
```
the table
5
3
4
4
4
ratings[1] picks a row
4
…[2] picks a cell in it

## Slide 9: Two-dimensional lists: the plan
Two-dimensional lists: the plan
Four things to do with a table.
Lists of lists
Visiting every cell
Building grids
Matrix operations

## Slide 10: Printing every cell
Printing every cell
```python
python print_table.py
   4   5   4   5   4
   5   3   4   4   4
   3   4   3   5   3
```
`print_table.py`
```python
ratings = [[4, 5, 4, 5, 4],
           [5, 3, 4, 4, 4],
           [3, 4, 3, 5, 3]]

for row in range(len(ratings)):
    for col in range(len(ratings[row])):
        print(f"{ratings[row][col]:4}", end="")
    print()
```
[LIVE] the file is in “week 5 code / print_table.py”.

## Slide 11: Reading the nested loop
Reading the nested loop
`print_table.py`
```python
ratings = [[4, 5, 4, 5, 4],
           [5, 3, 4, 4, 4],
           [3, 4, 3, 5, 3]]

for row in range(len(ratings)):
    for col in range(len(ratings[row])):
        print(f"{ratings[row][col]:4}", end="")
    print()
```
Outer loop
One pass for each row.
Inner loop
One pass for each column of that row.
end="" and print()
Stay on the line; then end the row.

## Slide 12: Format specs in f-strings
Format specs in f-strings
`format_specs.py`
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
[LIVE] the file is in “week 5 code / format_specs.py”.
```python
Width
{x:4} uses at least 4 characters.
```
```python
Decimal places
{r:.3f} keeps 3 decimal places.
```
```python
Thousands
{n:,} adds a comma every 3 digits.
```
```python
Alignment
Numbers go right, text goes left.
> forces right.
```

## Slide 13: The order of the visits
The order of the visits
Row by row, and left to right inside each row.
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
0
1
2
3
4
0
1
2
The numbers show when each cell is visited: 15 visits in all.

## Slide 14: Sum of each row
Sum of each row
```python
one run (random)
   7   9   3  19
  12  15   4  31
   2   2   0   4
  12  17   9  38
   1   7  16  24
```
`sum_of_rows.py`
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
[LIVE] the file is in “week 5 code / sum_of_rows.py”.

## Slide 15: Rows and columns
Rows and columns
A row: already a list; for row in table gives it
A column: no list holds it; we have to collect it
Solution: loop over the rows, take [col] from each

## Slide 16: Average of each column
Average of each column
```python
python column_averages.py
movie 0: 4.0
movie 1: 4.0
movie 2: 3.67
movie 3: 4.67
movie 4: 3.67
```
`column_averages.py`
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
[LIVE] the file is in “week 5 code / column_averages.py”.

## Slide 17: Two-dimensional lists: the plan
Two-dimensional lists: the plan
Four things to do with a table.
Lists of lists
Visiting every cell
Building grids
Matrix operations

## Slide 18: Building a grid
Building a grid
```python
python make_grid.py
. . .
. X .
. . .
```
`make_grid.py`
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
[LIVE] the file is in “week 5 code / make_grid.py”.

## Slide 19: A common bug: one row, three times
A common bug: one row, three times
```python
python grid_trap.py
. X .
. X .
. X .
True
```
`grid_trap.py`
```python
board = [["."] * 3] * 3      # looks like a 3 x 3 grid
board[1][1] = "X"
for row in board:
    print(" ".join(row))

print(board[0] is board[2])
```
[LIVE] the file is in “week 5 code / grid_trap.py”.

## Slide 20: Why every row changed
Why every row changed
Multiplying the outer list copies the reference, not the row.
0
1
2
```python
board
```
.
X
.
the one and only row
Multiplying a list repeats references, not rows.
Build every row separately, inside a loop, as make_grid does.

## Slide 21: Two-dimensional lists: the plan
Two-dimensional lists: the plan
Four things to do with a table.
Lists of lists
Visiting every cell
Building grids
Matrix operations

## Slide 22: Matrices
Matrices
A matrix: a rectangular table of numbers
Addition: add matching cells; same shape needed
Multiplication: a row of the left times a column of the right
The condition: columns of the left = rows of the right

## Slide 23: Multiplying two matrices
Multiplying two matrices
One cell of the answer: a row of a, times a column of b.
7
2
1
3
6
1
5
1
4
```python
a
```
8
3
5
1
4
1
1
3
4
```python
b
```
59
32
41
31
36
25
45
31
42
```python
c
```
×
=
c[0][0]  =  7 · 8  +  2 · 1  +  1 · 1  =  59
row 0 of a, times column 0 of b

## Slide 24: Adding two matrices
Adding two matrices
`matrix_add.py`
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
the file is in “week 5 code / matrix_add.py”.

## Slide 25: Multiplying two matrices
Multiplying two matrices
`matrix_mult.py`
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
the file is in “week 5 code / matrix_mult.py”.

## Slide 26: Printing a matrix
Printing a matrix
`matrix_print.py`
```python
def print_matrix(m):
    """Print m row by row, then a blank line."""
    for row in m:
        for x in row:
            print(f"{x:5}", end="")
        print()
    print()
```
the file is in “week 5 code / matrix_print.py”.

## Slide 27: Using the matrix functions
Using the matrix functions
```python
python matrix_demo.py
   15    5    6
    4   10    2
    6    4    8

   59   32   41
   31   36   25
   45   31   42

  119   59   54
   75   79   38
  103   51   64
```
`matrix_demo.py`
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
[LIVE] the file is in “week 5 code / matrix_demo.py”.

## Slide 28: Transpose
Transpose
```python
python transpose.py
[10, 12]
[12, 14]
[20, 25]
[12, 18]
```
`transpose.py`
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
[LIVE] the file is in “week 5 code / transpose.py”.

## Slide 29: Two-dimensional lists in one slide
Two-dimensional lists in one slide
Create
Write the rows inside [ ]
Or build each row in a loop
Never [[x] * m] * n
Read
t[r][c]: row first, then column
len(t) is the number of rows
len(t[0]) is the number of columns
Traverse
Outer loop over the rows
Inner loop over the columns
Columns need indexes
Compute
add: cell by cell
mult: row times column
transpose: swap r and c
