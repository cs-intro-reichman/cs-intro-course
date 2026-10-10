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
- `round(x, n)`, `abs`, `import math` (`math.sqrt` etc.), `import random` (`random.random()`, `random.randint`)
- Shown only as previews, not yet taught: a `turtle` demo and a `class Dog` example

## Week 2: Conditionals and while loops (2-1), for loops and numeral systems (2-2)
- `if` / `elif` / `else`, indentation as block structure, chained comparisons (`0 <= x <= 100`)
- `while`, the loop's three parts (initialise, test, update), augmented assignment (`+=`, `-=`, ...)
- Common loop bugs, nested loops, `break`, the `while True: ... break` pattern
- `for x in sequence`, `range(stop)`, `range(start, stop)`, `range(start, stop, step)`, `_` as an unused loop variable
- Loop patterns: counter, accumulator (sum, product, max/min), flag (`found = True/False`)
- Binary and other bases, conversion between decimal and binary by hand and in a loop
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
- List methods: `append`, `insert`, `pop`, `remove`, `sort`, `reverse`, `copy`. Built-ins: `sorted`, `max`, `min`, `sum`
- Strings and lists: `split`, `join`
- Building a list with an accumulator (`result = []` then `append` in a loop)
- Not modifying a list while looping over it (loop over a copy instead)
- Tuples: literals, indexing, immutability, unpacking (`for name, sid, grade in students:`)

## Week 5: Two-dimensional lists (5-1), Dictionaries and sets (5-2)
- Lists of lists, `grid[r][c]`, nested loops over rows and columns, row sums and column averages
- Building a grid correctly (and the `[[0] * n] * m` aliasing bug)
- Matrices: add, multiply, transpose, printing
- **Format specs in f-strings** (`{x:4}`, `{r:.3f}`, `{n:,}`, `>` alignment), taught on 5-1 slide 12, usable from here on
- Dictionaries: literals, `d[key]`, adding and updating, `in`, `KeyError`, `get`, `keys`, `values`, `items`, looping over a dict
- Rules for keys (immutable keys). Counting with a dict, grouping (a dict of lists)
- Sets: literals, `set()`, `add`, `in`, union, intersection, difference. Choosing a container
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
List comprehensions, `lambda`, `enumerate`, `zip`, conditional expressions (`a if c else b`), `*args`/`**kwargs`, generators/`yield`, decorators, `global`, inheritance (unless a later lecture adds it), type hints in code.
