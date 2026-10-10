# Lecture 6-2: PageRank (week 6)

## Slide 1: PageRank
#1
PYTHON COURSE · WEEK 6 · LECTURE 2
PageRank
Ranking pages by their links
Reichman University

## Slide 2: The problem
The problem
A search for “python” matches millions of pages. Which come first?
Relevance: is the page about what was searched for?
Importance: do other pages link to it?
PageRank: a number for importance, from the links alone

## Slide 3: What makes a page important
What makes a page important
Visits: pages people reach often matter more
Who links in: links from important pages count more
The problem: the definition is circular

## Slide 4: History
History
1998: Stanford students Sergey Brin and Larry Page
The idea: rank pages by the links that point to them
What came of it: Google's first ranking method
Brin & Page, “The Anatomy of a Large-Scale Hypertextual Web Search Engine”:  infolab.stanford.edu/~backrub/google.html

## Slide 5: PageRank: the plan
PageRank: the plan
Four steps today.
A model of the web
The transition matrix
Simulating a surfer
Computing it exactly

## Slide 6: A tiny web of five pages
A tiny web of five pages
Each arrow is a link from one page to another.
0
1
2
3
4
×2
×2
```python
web.dat
5
0 1
1 2  1 2
1 3  1 3  1 4
2 3
3 0
4 0  4 2
```
first: the number of pages;
then “from to” pairs, one per link

## Slide 7: The random surfer
The random surfer
A model of one person clicking links.
90% of the time: click one of the page's links, at random
10% of the time: jump to a random page
A page's rank: the share of the time the surfer spends there

## Slide 8: PageRank: the plan
PageRank: the plan
Four steps today.
A model of the web
The transition matrix
Simulating a surfer
Computing it exactly

## Slide 9: Counting the links
Counting the links
links[i][j]: how many links go from page i to page j.
0
1
0
0
0
0
0
2
2
1
0
0
0
1
0
1
0
0
0
0
1
0
1
0
0
0
1
2
3
4
0
1
2
3
4
to page j
from page i
1
5
1
1
2
links out

## Slide 10: Reading the web
Reading the web
`web_links.py`
```python
def read_links(filename):
    """Reads n, then "from to" pairs, from a web file.
    Returns links: links[i][j] counts the i -> j links."""
    with open(filename) as f:
        tokens = f.read().split()
    n = int(tokens[0])
    links = []
    for i in range(n):
        links.append([0] * n)     # a new row each time
    for k in range(1, len(tokens), 2):
        links[int(tokens[k])][int(tokens[k + 1])] += 1
    return links
```
the file is in “week 6 code / web_links.py”.

## Slide 11: From counts to chances
From counts to chances
Row 1: page 1 has five links.
0
0
2
2
1
0
1
2
3
4
```python
links[1]
```
```python
p[1][j]  =  0.10 / 5   +   0.90 × links[1][j] / 5
```
jump anywhere          follow one of the 5 links
0.02
0.02
0.38
0.38
0.20
```python
p[1]
```
0.02 + 0.02 + 0.38 + 0.38 + 0.20 = 1

## Slide 12: The transition matrix
The transition matrix
Row i: where the surfer goes next from page i.
0.02
0.92
0.02
0.02
0.02
0.02
0.02
0.38
0.38
0.20
0.02
0.02
0.02
0.92
0.02
0.92
0.02
0.02
0.02
0.02
0.47
0.02
0.47
0.02
0.02
0
1
2
3
4
0
1
2
3
4
```python
p
```

## Slide 13: Building the transition matrix
Building the transition matrix
`transition.py`
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
the file is in “week 6 code / transition.py”.

## Slide 14: PageRank: the plan
PageRank: the plan
Four steps today.
A model of the web
The transition matrix
Simulating a surfer
Computing it exactly

## Slide 15: The algorithm
The algorithm
Simulating the surfer
visits = 0 for every page
page = 0
repeat T times:
pick the next page, with the chances in p[page]
add 1 to visits[page]
rank of page i = visits[i] / T

## Slide 16: Picking a random page
Picking a random page
Put the probabilities in a row; pick a random number in [0, 1).
0
1
2
3
4
page
0.38
0.38
0.20
0
0.04
0.42
0.80
1.00
r = 0.63 falls between 0.42 and 0.80  →  page 3

## Slide 17: Picking a page in Python
Picking a page in Python
`next_page.py`
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
the file is in “week 6 code / next_page.py”.

## Slide 18: The surfer
The surfer
`surfer.py`
```python
from next_page import next_page


def simulate(p, moves):
    """Moves the surfer, starting on page 0. Returns
    the share of the moves that ended on each page."""
    visits = [0] * len(p)
    page = 0
    for t in range(moves):
        page = next_page(p[page])
        visits[page] += 1
    ranks = []
    for v in visits:
        ranks.append(v / moves)
    return ranks
```
the file is in “week 6 code / surfer.py”.

## Slide 19: Putting it together
Putting it together
```python
python pagerank.py   (moves, then pages 0–4)
      100  0.250  0.260  0.150  0.280  0.060
   10,000  0.276  0.267  0.143  0.246  0.068
1,000,000  0.273  0.266  0.146  0.247  0.068
```
`pagerank.py`
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
[LIVE] the file is in “week 6 code / pagerank.py”.

## Slide 20: The ranks
The ranks
A million moves: the share of time spent on each page.
0.273
page 0
0.266
page 1
0.146
page 2
0.247
page 3
0.068
page 4

## Slide 21: PageRank: the plan
PageRank: the plan
Four steps today.
A model of the web
The transition matrix
Simulating a surfer
Computing it exactly

## Slide 22: Computing the probabilities directly
Computing the probabilities directly
Instead of one surfer: keep the chance of being on each page
At the start: all of it on page 0, [1, 0, 0, 0, 0]
One move: new[j] = the sum over i of rank[i] × p[i][j]
Repeat: until the numbers stop changing

## Slide 23: One move, in numbers
One move, in numbers
Each new row is the previous row times the transition matrix.
0
1
2
3
4
1
0
0
0
0
after 0 moves
0.020
0.920
0.020
0.020
0.020
after 1 move
0.047
0.038
0.360
0.369
0.186
after 2 moves
pages 0 to 4

## Slide 24: One move, in Python
One move, in Python
`power_step.py`
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
the file is in “week 6 code / power_step.py”.

## Slide 25: Repeating the move
Repeating the move
```python
python power.py   (moves, then pages 0–4)
  1  0.020  0.920  0.020  0.020  0.020
  2  0.047  0.038  0.360  0.369  0.186
  3  0.436  0.062  0.117  0.358  0.027
 10  0.284  0.240  0.148  0.261  0.067
 20  0.272  0.265  0.147  0.248  0.068
 30  0.273  0.266  0.146  0.247  0.068
```
`power.py`
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
[LIVE] the file is in “week 6 code / power.py”.

## Slide 26: Simulation vs. exact computation
Simulation vs. exact computation
Simulation
One surfer, many random moves
Easy to explain and to write
Approximate: a million moves for 3 digits
Different every run
Repeated multiplication
A crowd, spread by the matrix
One move costs n × n steps
Exact: 30 moves for 3 digits here
The same answer every run

## Slide 27: Limitations
Limitations
Dead ends: a page with no links makes out zero
The usual fix: from a dead end, jump to any page
The 10%: the 1998 paper jumped 15% of the time
Scale: billions of pages, a few links on each

## Slide 28: PageRank in one slide
PageRank in one slide
Model
Pages and links
web.dat: n, then from–to pairs
links[i][j] counts them
Transition matrix
p[i][j]: jump, or follow a link
Rows sum to 1
Simulation
Pick the next page with given chances
Count the visits
More moves, steadier ranks
Exact
new[j] = Σ rank[i] × p[i][j]
Repeat until it stops changing
