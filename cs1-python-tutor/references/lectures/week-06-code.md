# Week 6 code files

The code files shown in the week 6 lectures.

### `USA.txt`
(data file, 391,799 bytes, not included)

### `average.py`
```python
import sys

total, count = 0.0, 0
for line in sys.stdin:   # one line at a time
    total += float(line)
    count += 1
print("Average:", total / count)
```

### `count_values.py`
```python
# How often each number appears in demo.dat.
# The first number, n: the rest are 0 .. n-1.

with open("demo.dat") as f:
    tokens = f.read().split()

n = int(tokens[0])
count = [0] * n
for t in tokens[1:]:
    count[int(t)] += 1

for i in range(n):
    print(f"{i}: {count[i]}")
```

### `demo.dat`
```
4
1 1 2 
0 1 3 0 3
0 1
```

### `final_grades.py`
```python
with open("grades.csv") as f:
    f.readline()              # skip the header
    for line in f:
        name, hw, exam = line.strip().split(",")
        final = 0.3 * int(hw) + 0.7 * int(exam)
        print(f"{name:5} {final:5.1f}")
```

### `grades.csv`
```
name,hw,exam
Dana,88,92
Noam,75,64
Maya,95,81
Yoni,52,58
```

### `missing_file.py`
```python
name = "demo.txt"        # a typo: it is demo.dat
try:
    with open(name) as f:
        print(f.read())
except FileNotFoundError:
    print("No such file:", name)
```

### `next_page.py`
```python
import random


def next_page(row):
    """Picks page j with probability row[j]."""
    r = random.random()           # somewhere in [0, 1)
    total = 0.0
    for j in range(len(row)):
        total += row[j]
        if r < total:
            return j
    return len(row) - 1           # in case of rounding
```

### `pagerank.py`
```python
from web_links import read_links
from transition import transition_matrix
from surfer import simulate

links = read_links("web.dat")
p = transition_matrix(links)
for moves in [100, 10_000, 1_000_000]:
    ranks = simulate(p, moves)
    print(f"{moves:>9,}", end="")
    for r in ranks:
        print(f"{r:7.3f}", end="")
    print()
```

### `passed.py`
```python
passed = []
with open("grades.csv") as f:
    f.readline()              # skip the header
    for line in f:
        name, hw, exam = line.strip().split(",")
        if 0.3 * int(hw) + 0.7 * int(exam) >= 60:
            passed.append(name)

with open("passed.txt", "w") as f:
    for name in passed:
        f.write(name + "\n")
print(len(passed), "names written to passed.txt")
```

### `power.py`
```python
from web_links import read_links
from transition import transition_matrix
from power_step import step

p = transition_matrix(read_links("web.dat"))
rank = [1.0, 0.0, 0.0, 0.0, 0.0]  # on page 0
for move in range(1, 31):
    rank = step(rank, p)
    if move in [1, 2, 3, 10, 20, 30]:
        print(f"{move:>3}", end="")
        for r in rank:
            print(f"{r:7.3f}", end="")
        print()
```

### `power_step.py`
```python
def step(rank, p):
    """rank[i]: the chance of being on page i now.
    Returns the chances one move later."""
    n = len(rank)
    new = [0.0] * n
    for i in range(n):
        for j in range(n):
            new[j] += rank[i] * p[i][j]
    return new
```

### `random_numbers.py`
```python
import random
import sys

n = int(sys.argv[1])   # typed after the name
for i in range(n):
    print(random.random())
```

### `read_lines.py`
```python
with open("demo.dat") as f:
    for line in f:
        print(repr(line), line.split())
```

### `read_whole.py`
```python
with open("demo.dat") as f:
    text = f.read()

print(repr(text))
print(text)
```

### `redirection.txt`
```
Terminal transcript (macOS / Linux shell), not a Python file.
% python random_numbers.py 1000 > data.txt
% python average.py < data.txt
Average: 0.49570948891636646
% python random_numbers.py 1000000 | python average.py
Average: 0.5007775704132853
```

### `surfer.py`
```python
from next_page import next_page


def simulate(p, moves):
    """Moves the surfer, starting on page 0. Returns
    the share of the moves that ended on each page."""
    visits = [0] * len(p)
    page = 0
    for _ in range(moves):
        page = next_page(p[page])
        visits[page] += 1
    return [v / moves for v in visits]
```

### `transition.py`
```python
def transition_matrix(links, jump=0.10):
    """p[i][j]: the chance of moving from page i to j.
    Assumes every page has at least one link."""
    n = len(links)
    p = []
    for i in range(n):
        out = sum(links[i])       # links leaving page i
        row = []
        for j in range(n):
            follow = links[i][j] / out
            row.append(jump / n + (1 - jump) * follow)
        p.append(row)
    return p
```

### `usa_map.py`
```python
# Draws the towns of USA.txt as a map of characters.
W, H = 60, 18          # columns and rows

xs, ys = [], []
with open("USA.txt") as f:
    f.readline()       # skip the header
    for line in f:
        x, y = line.split()
        xs.append(float(x))
        ys.append(float(y))

left, right = min(xs), max(xs)
bottom, top = min(ys), max(ys)

grid = [[" "] * W for _ in range(H)]
for i in range(len(xs)):
    col = int((xs[i] - left) / (right - left) * (W - 1))
    row = int((top - ys[i]) / (top - bottom) * (H - 1))
    grid[row][col] = "*"

for row in grid:
    print("".join(row))
```

### `usa_points.py`
```python
# USA.txt: a header line with the bounding box,
# then one "x y" pair per town.

with open("USA.txt") as f:
    header = f.readline().split()
    xs, ys = [], []
    for line in f:
        x, y = line.split()
        xs.append(float(x))
        ys.append(float(y))

print(len(xs), "towns")
print("header:", header)
print(f"x: {min(xs)} to {max(xs)}")
print(f"y: {min(ys)} to {max(ys)}")
```

### `web.dat`
```
5
0 1
1 2  1 2
1 3  1 3  1 4
2 3
3 0
4 0  4 2
```

### `web_links.py`
```python
def read_links(filename):
    """Reads n, then "from to" pairs, from a web file.
    Returns links: links[i][j] counts the i -> j links."""
    with open(filename) as f:
        tokens = f.read().split()
    n = int(tokens[0])
    links = [[0] * n for _ in range(n)]   # n new rows
    for k in range(1, len(tokens), 2):
        links[int(tokens[k])][int(tokens[k + 1])] += 1
    return links
```

### `write_squares.py`
```python
with open("squares.txt", "w") as f:
    for i in range(1, 6):
        f.write(f"{i} {i * i}\n")

with open("squares.txt") as f:
    print(f.read(), end="")
```
