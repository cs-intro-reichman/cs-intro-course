# Python taught in the course, week by week

This list is cumulative. A student in week N knows everything listed for weeks 1 to N. Use it to choose what code you write or suggest. If something isn't listed, the course hasn't taught it (yet), so don't build a hint or an example on it.

The instructor maintains this file. Week numbers follow the current schedule.

## Week 1: Intro and basics (1-1), Types and I/O (1-2)
- Running a program, the REPL, comments (`#`), `print`, `print` with several arguments separated by commas, `end=""`
- Variables and assignment, dynamic typing, `type()`
- Types: `int`, `float`, `str`, `bool`. Casting with `int()`, `float()`, `str()`
- Arithmetic: `+ - * / // % **`, precedence, big integers, float imprecision (comparing floats)
- String `+` and `*`
- Comparisons `== != < <= > >=`, `and`, `or`, `not`
- `input()` (it always returns a string) and converting the result
- f-strings in the plain `{expr}` form only. Format specs are not taught yet.
- `round(x, n)`, `abs`, `import math` (`math.sqrt`, `math.floor`, `math.ceil`, `math.pi`), `import random` (`random.random()` only; a random whole number is made as `int(random.random() * n)`, lecture 1-2 slide 58)
- Kinds of errors (syntax, runtime, logical; lecture 1-1 slide 43) and reading a traceback (1-2)
- Not taught in week 1: `random.randint`, `min`, `max`, `sum` (these first appear in the lists lecture, 4-2)
- Shown only as previews, not yet taught: a `turtle` demo and a `class Dog` example

## Week 2: Conditionals and while loops (2-1), for loops and numeral systems (2-2)
- `if` / `elif` / `else`, indentation as block structure, chained comparisons (`0 <= x <= 100`)
- The conditional expression `a if condition else b` (lecture 2-1, slide 19)
- `while`, the loop's three parts (initialise, test, update), augmented assignment (`+=`, `-=`, ...)
- Common loop bugs, nested loops, `break`, the `while True: ... break` pattern
- `for x in sequence`, `range(stop)`, `range(start, stop)`, `range(start, stop, step)`, `_` as an unused loop variable
- Loop patterns: counter, accumulator (sum, product, max/min), flag (`found = True/False`)
- Binary and other bases, conversion between decimal and binary by hand and in a loop, `bin()`
- Simulation with `random` (Gambler's ruin)

## Week 3: Strings (3-1), Approximation algorithms (3-2)
- Strings as sequences: indexing, negative indices, `len`, slicing `s[a:b]`, `s[a:b:step]`, `s[::-1]`
- `in` / `not in`, iterating over a string with `for ch in s`
- Strings are immutable. `id()`
- String methods: `upper`, `lower`, `strip`, `find`, `index`, `count`, `replace`, `isalpha`, `isdigit`, `islower`, `isupper`
- `ord`, `chr`
- `continue` (and when to prefer a plain `if`)
- Approximation: sequential (exhaustive) search, bisection search, Newton–Raphson, tolerance ε (`epsilon`), counting iterations

## Week 4: Functions (4-1), Lists and tuples (4-2)
- `def`, parameters and arguments, `return`, functions calling functions, the order of events in a call
- Default parameter values, keyword arguments
- Type hints are shown once (4-1 slide 19) and then not used. Don't use them.
- Docstrings, `help()`, modules: putting functions in a file and importing it (`import mymath`)
- Stubs, top-down design, decomposition
- Lists: literals, indexing, slicing, `in`, `+`, `*`, `len`, `list()`
- Lists are mutable: item assignment, aliasing (`b = a`), copying (`a[:]`, `a.copy()`)
- List methods: `append`, `insert`, `pop`, `remove`, `sort`, `reverse`, `copy`. Built-ins: `sorted`, `max`, `min`, `sum` (first taught here)
- Strings and lists: `split`, `join`
- Building a list with an accumulator (`result = []` then `append` in a loop)
- Not modifying a list while looping over it (loop over a copy instead)
- Tuples: literals, indexing, immutability, unpacking (`for name, sid, grade in students:`)

## Week 5: Lists, part 2: comprehensions, lists in action, tables (5-1), Dictionaries and sets (5-2)
- Lists of lists, `grid[r][c]`, nested loops over rows and columns, row sums and column averages
- Building a grid correctly (and the `[[0] * n] * m` aliasing bug)
- **List comprehensions** (start of 5-1; the grid and table forms come after the grid bug): `[k * k for k in range(1, 6)]`, with a filter (`[n for n in xs if n % 2 == 0]`), building a grid with `[["."] * cols for _ in range(rows)]`, a column `[row[c] for row in t]`, `[sum(row) for row in t]`, a nested comprehension for transpose. Rule taught: use one only to build a list, keep it short, never for actions like printing
- **Lists in action** (5-1, second part): coupon collector (a list of booleans `found = [False] * n`, a `while` loop, `int(random.random() * n)`, a function in a module, averaging many trials), the sieve of Eratosthenes (`is_prime = [True] * (n + 1)`, `range(2 * p, n + 1, p)`), building a deck of cards with nested loops and shuffling it (swap with `deck[i], deck[r] = deck[r], deck[i]`). Note: these are lecture examples, so don't point a student to them when their homework is the same problem
- Matrices: add, multiply, transpose, printing
- `random.randint` appears in 5-1 (filling a grid with random numbers); before that, random whole numbers are made with `int(random.random() * n)`
- **Format specs in f-strings** (`{x:4}`, `{r:.3f}`, `{n:,}`, `>` alignment), taught on 5-1 slide 30 (in the two-dimensional part), usable from there on
- Dictionaries: literals, `d[key]`, adding and updating, `in`, `KeyError`, `get`, `keys`, `values`, `items`, looping over a dict
- Rules for keys (immutable keys). Counting with a dict, grouping (a dict of lists)
- `dict()`, `update`, `clear`, sorting a dictionary's items with `sorted`
- Sets: literals, `set()`, `add`, `in`, union, intersection, difference, symmetric difference (operators and methods), `issubset`, `issuperset`, `isdisjoint`. Choosing a container
- Timing code with `time.perf_counter()`, and why set and dict lookup is fast (hashing, high level only)

## Week 6: Files (6-1), PageRank (6-2)
- Text files: `open`, the `with` statement, `read`, `readline`, iterating over lines, `strip` and `split` on each line, converting to numbers
- Files of records (CSV-like), checking the data and skipping a header
- Writing files: `open(name, "w")`, `write`. Read, decide, write
- Where Python looks for a file (the working directory), `FileNotFoundError` with `try` / `except`
- Standard input and output, redirection (`<`, `>`) and pipes (`|`)
- PageRank: reading a graph from a file, a transition matrix as a 2D list, random-surfer simulation, computing the probabilities by repeated matrix-vector steps

## Week 7: Recursion (7-1), midterm
- (to be filled in when the lecture is added)

## Week 8: Computer fundamentals, the Vic computer (8-1), AI agents for coding (8-2)
- Vic: registers, memory, instruction set, fetch-execute cycle, branching, translating simple programs to Vic code, symbolic programming and assemblers
- 8-2: (to be filled in)

## Week 9: Software engineering, Complexity
- (to be filled in)

## Week 10: Searching and sorting (10-1), Objects and classes 1 (10-2)
- 10-1: (to be filled in)
- 10-2, using classes as a client: objects, constructors (`Fraction(2, 5)`), methods (`a.add(b)`), names refer to objects, printing an object, mutable vs immutable objects, reading an API

## Week 11: Writing classes (11-1), Image processing (11-2)
- `class`, `__init__`, `self`, attributes, methods, `__str__`, getters, methods that change the object
- Class variables (a counter shared by all objects), the underscore convention for "private" attributes
- Procedural vs object-oriented design
- 11-2: (to be filled in)

## Week 12: Advanced data structures
- (to be filled in)

## Never taught in this course (avoid unless the student asks)
`lambda`, `enumerate`, `zip`, dictionary and set comprehensions, `*args`/`**kwargs`, generators/`yield`, decorators, `global`, inheritance (unless a later lecture adds it), type hints in code.
