# Lecture 5-1: Lists, part 2: comprehensions, lists in action, tables (week 5)

## Slide 1: Lists, Part 2
[i][j]
PYTHON COURSE · WEEK 5 · LECTURE 1
Lists, Part 2
Comprehensions, lists in action, tables
Reichman University

## Slide 2: Today: lists, part 2
Today: lists, part 2
Three parts.
List comprehensions
lists in one line
Lists in action
cards, coupons, primes
Two-dimensional lists
tables and grids

## Slide 3: From a loop to a comprehension
From a loop to a comprehension
```python
python squares.py
[1, 4, 9, 16, 25]
[1, 4, 9, 16, 25]
```
`squares.py`
```python
# The loop way
squares = []
for k in range(1, 6):
    squares.append(k * k)
print(squares)

# The same list, in one line
squares = [k * k for k in range(1, 6)]
print(squares)
```

## Slide 4: Reading a comprehension
Reading a comprehension
Read it from the middle: first the loop, then the value.
`squares.py`
```python
squares = [k * k for k in range(1, 6)]
```
```python
for k in range(1, 6)
The loop: k takes the values 1 to 5, one by one.
```
```python
k * k
The value: computed for each k and put in the list.
```
```python
[ ]
The brackets: the values are collected into a new list.
```

## Slide 5: Keeping only some items
Keeping only some items
```python
python keep_some.py
[4, 2, 8]
['GRID', 'MATRIX', 'CELL']
```
`keep_some.py`
```python
numbers = [4, 9, 15, 2, 8, 23]
evens = [n for n in numbers if n % 2 == 0]
print(evens)

words = ["grid", "row", "matrix", "cell"]
long_words = [w.upper() for w in words if len(w) > 3]
print(long_words)
```

## Slide 6: When to use a comprehension
When to use a comprehension
Use it: to build a new list from a list or a range
Keep it short: if it needs two lines to explain, write the loop
Not for actions: a loop that prints or changes things stays a loop
Same result: a loop with append can build anything it builds

## Slide 7: Today: lists, part 2
Today: lists, part 2
Three parts.
List comprehensions
lists in one line
Lists in action
cards, coupons, primes
Two-dimensional lists
tables and grids

## Slide 8: The coupon collector problem
The coupon collector problem
The story: 100 different baseball cards, one in every cereal box
The question: how many boxes until you have all 100?
In general: draw random numbers from 0 to n − 1 until each has come up
The tool: a list of True and False, one entry per card

## Slide 9: Coupon collector: the algorithm
Coupon collector: the algorithm
In pseudocode
found = n values, all False
count = 0, distinct = 0
while distinct < n:
draw a random card c
add 1 to count
if found[c] is False:
found[c] = True
add 1 to distinct
report count
Why a list?
found[c] answers “do we have card c?” in one step.

The card number is the index into the list.

## Slide 10: Coupon collector: the program
Coupon collector: the program
```python
in the REPL
>>> import coupons
>>> coupons.collect(100)
679
>>> coupons.collect(100)
506
>>> coupons.collect(100)
569
```
`coupons.py`
```python
"""The coupon collector, as a function."""
import random


def collect(n):
    """Return the boxes needed to collect all n cards."""
    found = [False] * n      # found[c]: got card c yet?
    count = 0                # boxes bought
    distinct = 0             # different cards found
    while distinct < n:
        card = int(random.random() * n)
        count += 1
        if not found[card]:
            found[card] = True
            distinct += 1
    return count
```

## Slide 11: Coupon collector: the experiment
Coupon collector: the experiment
```python
python coupon_experiment.py
10 trials: 551.9 boxes
100 trials: 509.7 boxes
10000 trials: 519.8 boxes
theory: 518.7 boxes
```
`coupon_experiment.py`
```python
# How many boxes does it take, on average?
import coupons

n = 100
for trials in [10, 100, 10000]:
    results = [coupons.collect(n) for _ in range(trials)]
    average = sum(results) / trials
    print(f"{trials} trials: {round(average, 1)} boxes")

theory = sum([n / k for k in range(1, n + 1)])
print(f"theory: {round(theory, 1)} boxes")
```

## Slide 12: Prime numbers
Prime numbers
A prime: a whole number above 1 whose only divisors are 1 and itself
They thin out: 8 primes below 20, but only 983, 991 and 997 from 980 to 1000
They never run out: Euclid proved it, around 300 BCE
October 2024: a new prime was found, with 41,024,320 digits

## Slide 13: The sieve of Eratosthenes
The sieve of Eratosthenes
Cross out the multiples of each prime. What is left is prime.
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
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
1
1 is not prime
4
6
8
10
12
14
16
18
20
22
24
26
28
30
p = 2
9
15
21
27
p = 3
25
p = 5
2
3
5
7
11
13
17
19
23
29
10 primes

## Slide 14: The sieve: the program
The sieve: the program
```python
python sieve.py
2 3 5 7 11 13 17 19 23 29 
10 primes up to 30
```
`sieve.py`
```python
n = 30
is_prime = [True] * (n + 1)    # is k still in?
is_prime[0] = False
is_prime[1] = False
for p in range(2, n + 1):
    if is_prime[p]:
        # cross out the multiples of p
        for m in range(2 * p, n + 1, p):
            is_prime[m] = False

primes = [k for k in range(n + 1) if is_prime[k]]
for p in primes:
    print(p, end=" ")
print()
print(f"{len(primes)} primes up to {n}")
```

## Slide 15: The thinning of the primes
The thinning of the primes
```python
python thinning.py
100: 25 primes, 25%
10000: 1229 primes, 12%
1000000: 78498 primes, 8%
```
`thinning.py`
```python
def count_primes(n):
    """Return the number of primes from 2 to n."""
    is_prime = [True] * (n + 1)
    is_prime[0] = False
    is_prime[1] = False
    for p in range(2, n + 1):
        if is_prime[p]:
            for m in range(2 * p, n + 1, p):
                is_prime[m] = False
    return len([k for k in range(n + 1) if is_prime[k]])


for n in [100, 10000, 1000000]:
    count = count_primes(n)
    share = round(100 * count / n)
    print(f"{n}: {count} primes, {share}%")
```

## Slide 16: Building a deck of cards
Building a deck of cards
```python
python deck.py
52 cards
2 of Clubs
2 of Diamonds
2 of Hearts
2 of Spades
3 of Clubs
...
Ace of Spades
```
`deck.py`
```python
ranks = ["2", "3", "4", "5", "6", "7", "8", "9", "10",
         "Jack", "Queen", "King", "Ace"]
suits = ["Clubs", "Diamonds", "Hearts", "Spades"]

deck = []
for rank in ranks:
    for suit in suits:
        deck.append(f"{rank} of {suit}")

print(f"{len(deck)} cards")
for card in deck[:5]:
    print(card)
print("...")
print(deck[-1])
```

## Slide 17: Shuffling
Shuffling
```python
python shuffle.py   (one run)
['4', '2', '3', 'A', '5', '6']
['4', '5', '3', 'A', '2', '6']
['4', '5', '6', 'A', '2', '3']
['4', '5', '6', '3', '2', 'A']
['4', '5', '6', '3', 'A', '2']
```
`shuffle.py`
```python
import random

deck = ["A", "2", "3", "4", "5", "6"]
n = len(deck)
for i in range(n - 1):
    # pick a random position r, from i to n - 1
    r = i + int(random.random() * (n - i))
    # swap the cards at positions i and r
    deck[i], deck[r] = deck[r], deck[i]
    print(deck)
```

## Slide 18: A fair shuffle
A fair shuffle
Fair: every order of the deck is equally likely
This algorithm: swap each position with a random later one, or itself
A common mistake: swapping with any random position is not fair
It matters: players beat a poker site that shuffled badly

## Slide 19: Today: lists, part 2
Today: lists, part 2
Three parts.
List comprehensions
lists in one line
Lists in action
cards, coupons, primes
Two-dimensional lists
tables and grids

## Slide 20: Data in rows and columns
Data in rows and columns
A lot of data comes as tables.
Ratings: reviewers down the side, movies across the top
Images: rows and columns of pixels
Sales: models down the side, quarters across
Game boards: a 3 × 3 tic-tac-toe grid

## Slide 21: A table of ratings
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

## Slide 22: An image is a table
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

## Slide 23: A list of lists
A list of lists
A row: an ordinary list, like [4, 5, 4, 5, 4]
The table: a list whose items are the rows
One value: ratings[row][col], row first, then column
Its size: len(ratings) rows, len(ratings[0]) columns

## Slide 24: Writing a table in Python
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

## Slide 25: A list of lists in memory
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

## Slide 26: Reading ratings[1][2]
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

## Slide 27: Two-dimensional lists: the plan
Two-dimensional lists: the plan
Four things to do with a table.
Lists of lists
Visiting every cell
Building grids
Matrix operations

## Slide 28: Printing every cell
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

## Slide 29: Reading the nested loop
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

## Slide 30: Format specs in f-strings
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

## Slide 31: The order of the visits
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

## Slide 32: Sum of each row
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

## Slide 33: Rows and columns
Rows and columns
A row: already a list; for row in table gives it
A column: no list holds it; we have to collect it
Solution: loop over the rows, take [col] from each

## Slide 34: Average of each column
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

## Slide 35: Two-dimensional lists: the plan
Two-dimensional lists: the plan
Four things to do with a table.
Lists of lists
Visiting every cell
Building grids
Matrix operations

## Slide 36: Building a grid
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

## Slide 37: A common bug: one row, three times
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

## Slide 38: Why every row changed
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
Build every row separately, with a loop or a comprehension.

## Slide 39: Building a grid, the short way
Building a grid, the short way
```python
python grid_comprehension.py
. . . .
. X . .
. . . .
False
```
`grid_comprehension.py`
```python
rows, cols = 3, 4
board = [["."] * cols for _ in range(rows)]
board[1][1] = "X"
for row in board:
    print(" ".join(row))

print(board[0] is board[2])
```

## Slide 40: Comprehensions on a table
Comprehensions on a table
```python
python table_comprehension.py
[4, 4, 3]
[22, 20, 18]
[4, 5, 3]
[5, 3, 4]
[4, 4, 3]
[5, 4, 5]
[4, 4, 3]
```
`table_comprehension.py`
```python
ratings = [[4, 5, 4, 5, 4],
           [5, 3, 4, 4, 4],
           [3, 4, 3, 5, 3]]

# one column: movie 2
print([row[2] for row in ratings])

# one number per row: each reviewer's total
print([sum(row) for row in ratings])

# transpose: column c becomes row c
flipped = [[row[c] for row in ratings]
           for c in range(len(ratings[0]))]
for row in flipped:
    print(row)
```

## Slide 41: Two-dimensional lists: the plan
Two-dimensional lists: the plan
Four things to do with a table.
Lists of lists
Visiting every cell
Building grids
Matrix operations

## Slide 42: Matrices
Matrices
A matrix: a rectangular table of numbers
Addition: add matching cells; same shape needed
Multiplication: a row of the left times a column of the right
The condition: columns of the left = rows of the right

## Slide 43: Multiplying two matrices
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

## Slide 44: Adding two matrices
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

## Slide 45: Multiplying two matrices
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

## Slide 46: Printing a matrix
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

## Slide 47: Using the matrix functions
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
```python
from matrix_add import add brings in just the name add.
So we call add(a, b), not matrix_add.add(a, b).
```

## Slide 48: Transpose
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

## Slide 49: Two-dimensional lists in one slide
Two-dimensional lists in one slide
Create
Write the rows inside [ ]
Or build each row in a loop
Or use a comprehension
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
