# Lecture 5-2: Dictionaries and sets (week 5)

## Slide 1
PYTHON COURSE · WEEK 5 · LECTURE 2
Dictionaries and Sets
Reaching a value by name

## Slide 2
Lecture overview
1
Dictionaries
a value reached by its key
2
Keys
what can be one, and why
3
Patterns
counting, functions, nesting
4
Sets
when only membership matters
Dictionaries
Operators
Keys
Methods & Built-ins
Looping
Functions
Nested
Sets

## Slide 3
Why lists and tuples aren’t enough
Revisiting student records (week 4) – storing dynamic records (name & grade) while enabling fast lookup by name.
`find_student_list.py`
```python
for name, grade in students:
    if name == "Ron Cohen":
        print(name, grade)   # Ron Cohen 95
        break
```
The core problems
Code overhead: Multi-line unpacking code for a basic query.
Sequential search: Must check items one by one until match is found (or not).
```python
"Dana Levi"
```
```python
88
```
```python
"Ron Cohen"
```
```python
95
```
```python
"Yael Bar"
```
```python
73
```
✗
✓
name
position
value
a middleman step we never wanted
```python
students
```
Dictionaries
Operators
Keys
Methods & Built-ins
Looping
Functions
Nested
Sets

## Slide 4
A dictionary
`first_dict.py`
```python
grades = {"Dana Levi": 88, 
	"Ron Cohen": 95,
          "Yael Bar": 73}

print(grades["Ron Cohen"])   # 95
grades["Ron Cohen"] = 100    # one line
```
What changed ?
The same data: Nothing added or dropped.
Direct addressing: Access values via unique keys instead of positions.
No sequential overhead: Bypasses earlier records to jump straight to the key.
```python
"Dana Levi"
```
```python
88
```
```python
"Ron Cohen"
```
```python
95
```
```python
"Yael Bar"
```
```python
73
```
Index-free structure: Eliminates positional middleman steps
    Key (name)
Value (grade)
Dictionary keys must be unique. Real-world systems often use unique identifiers (e.g., Student ID) as keys, storing composite data as values.
```python
grades
```
✓
A collection of key-value pairs, which allows direct access via key.
Item 

## Slide 5
```python
Square brackets [], in and not in
```
Some of a list's operators transfer to a dictionary, and some cannot.
`dict_basics.py`
```python
# grades is the same three students
print(grades["Ron Cohen"])        # 95
print(grades[0])                  # KeyError: 0
print("Ron Cohen" in grades)      # True
print("Tal Shani" not in grades)  # True
print(95 in grades)               # False
print(len(grades))                # 3
```
```python
What transfers, and what does not
The bracket: a key, not a position.
in / not in: about keys, not values.
len: how many pairs.
No slicing, + or *: there is no order.
```
```python
[ ]
```
```python
in
```
```python
not in
```
these transfer
```python
[ : : ]
```
```python
+
```
```python
*
```
a dictionary has none of these
Dictionaries
Operators
Keys
Methods & Built-ins
Looping
Functions
Nested
Sets

## Slide 6
```python
"Dana Levi"
```
```python
88
```
```python
"Ron Cohen"
```
```python
95
```
```python
"Omer Katz"
```
```python
91
```
```python
93
```
The four core dictionary operations
Add, change, remove and check membership.
`dict_ops.py`
```python
grades = {"Dana Levi": 88, "Ron Cohen": 95,
          "Yael Bar": 73}

grades["Omer Katz"] = 91       # add a new pair
grades["Dana Levi"] = 93       # change a value
grades.pop("Yael Bar")         # remove a pair
print("Ron Cohen" in grades)   # True
print(grades)
# {'Dana Levi': 93, 'Ron Cohen': 95,
#  'Omer Katz': 91}
```
```python
"Dana Levi"
```
```python
88
```
```python
"Ron Cohen"
```
```python
95
```
```python
"Yael Bar"
```
```python
73
```
```python
"Omer Katz"
```
```python
91
```
```python
93
```
✗
```python
Common pitfalls
Assignment does both: Adds, or replaces.
in asks about keys: Not about values.
.pop on a missing key: Raises a KeyError.
```
```python
grades
```

## Slide 7
Handling missing keys
```python
The KeyError exception and two approaches for safe access.
```
`keyerror.py`
```python
grades = {"Dana Levi": 88, "Ron Cohen": 95}

print(grades["Tal Shani"])
# KeyError: 'Tal Shani'
```
`get.py`
```python
# option 1: in
if "Tal Shani" in grades:        # ask first
    print(grades["Tal Shani"])
# option 2: .get()
print(grades.get("Tal Shani"))           # None
print(grades.get('Tal Shani', 'n/a'))    # 'n/a'
```
```python
Safe retrieval options
Membership check first - in: 
Using    if key in dict:  before accessing a key.
Default fallback - .get()
Returns None (or custom default)   instead of crashing.
```
```python
"Dana Levi"
```
```python
88
```
```python
"Ron Cohen"
```
```python
95
```
```python
grades
```

## Slide 8
Keys must be immutable
`key_types.py`
```python
# a number, a string or a tuple - never a list
grades[("Yael", "Bar")] = 73    # a tuple: fine
grades[["Yael", "Bar"]] = 73    # a list: no
# TypeError: unhashable type: 'list'
```
Why is it so important ? 
The rule: Keys must be immutable (numbers, strings, tuples)
The reason: A key's value determines its lookup position.
If it changed: The new position no longer matches where the data was originally placed.
The result: The stored data becomes unreachable.
0
1
2
3
4
```python
["Yael", "Bar"]
```
```python
73
```
```python
["Yael", "Barr"]
```
```python
?
```
✗
The slot is chosen by a number computed from the key itself. Change the key and the number is different — the pair stays in slot 2, and the key now points at an empty one.
Hypothetical: What if lists were allowed as keys ?
✗
✓
Dictionaries
Operators
Keys
Methods & Built-ins
Looping
Functions
Nested
Sets

## Slide 9
Common dictionary methods
method
what it does
example
```python
.get(k)
```
The value for k, or None when there is no such key.
```python
grades.get("Tal")
```
```python
.keys()
```
Every key, in the order the pairs were put in.
```python
list(grades.keys())
```
```python
.values()
```
Every value, in the same order.
```python
sum(grades.values())
```
```python
.items()
```
Every pair, each one a (key, value) tuple.
```python
list(grades.items())
```
```python
.pop(k)
```
Removes the pair and returns its value; KeyError if absent.
```python
grades.pop("Yael Bar")
```
```python
.update(d2)
```
Copies every pair of dictionary d2 in; a repeated key is 
overwritten.
```python
grades.update(more)
```
```python
.copy()
```
A copy of the dictionary - not a second name for this one.
```python
b = grades.copy()
```
```python
.clear()
```
Empties it, in place. It is the same dictionary.
```python
grades.clear()
```
Dictionaries
Operators
Keys
Methods & Built-ins
Looping
Functions
Nested
Sets

## Slide 10
Built-in functions that work on dictionaries
Functions, not methods: the dictionary goes inside the parentheses.
`builtins.py`
```python
print(len(grades))          # 3
print(sorted(grades))       # the keys
print(min(grades))          # 'Dana Levi'
print(max(grades))          # 'Yael Bar'
print(sum(grades))          # TypeError
print(sum(grades.values())) # 256
```
```python
Every one of them is applied on the keys - sorted, min and max order the keys and never a value. len counts pairs. 
For the values, ask: sum(grades.values()) is 256.
```
the keys
```python
len
```
```python
3
```
```python
sorted
```
```python
a list of the keys
```
```python
min
```
```python
"Dana Levi"
```
```python
max
```
```python
"Yael Bar"
```
```python
"Dana Levi"
```
```python
88
```
```python
"Ron Cohen"
```
```python
95
```
```python
"Yael Bar"
```
```python
73
```
```python
grades
```
```python
sum
```
```python
TypeError
```
the keys are names
sum adds the keys - so they must be numbers.

## Slide 11
Iterating over a dictionary
Iterating by keys, values or key-value pairs (items)
`loop_dict.py`
```python
for name in grades:             # the keys
    print(name)

for grade in grades.values():   # the values
    print(grade)

for name, grade in grades.items():   # both
    print(name, grade)
```
```python
"Dana Levi"
```
```python
88
```
```python
"Ron Cohen"
```
```python
95
```
```python
"Yael Bar"
```
```python
73
```
```python
"Dana Levi"
```
```python
"Ron Cohen"
```
```python
"Yael Bar"
```
```python
88
```
```python
95
```
```python
73
```
```python
"Dana Levi"
```
```python
88
```
```python
"Ron Cohen"
```
```python
95
```
```python
"Yael Bar"
```
```python
73
```
```python
Iteration patterns
Directly: you get the keys, not pairs.
Preferred: use .items() for both.
Tuple unpacking: for k, v in d.items()
The number of keys must hold still: never add or remove a key while looping over a dictionary. Loop over list(d) if you must.
```
```python
grades
```
```python
Note: Dictionary views
.keys(), .values() and .items() are dynamic views, not lists, and cannot be indexed.
Use list(d.keys()) if positional access is needed.
```
Dictionaries
Operators
Keys
Methods & Built-ins
Looping
Functions
Nested
Sets

## Slide 12
Dictionary key ordering
Guaranteed insertion order vs. explicit sorting
`ordering.py`
```python
grades["Omer Katz"] = 91   # added last

for name in sorted(grades):   # ask for order
    print(name, grades[name])
# Dana Levi 88
# Omer Katz 91
# Ron Cohen 95
# Yael Bar 73
```
Language vs. conceptual conventions
Official guarantee: Python maintains insertion order as of version 3.7.
Abstract dictionary concept: Assume no order.
```python
Best Practices
Predictable iteration: Iteration order matches entry insertion order.
Explicit sorting: Use sorted(d) when alphabetical or numerical order is required.
sorted(grades): Returns a list of the keys, in order.
```
Print your results sorted - a habit worth building now.

## Slide 13
Class exercise: Counting words
Task: How many times does each word appear in sentence?
`counting_v1.py`
```python
sentence = "The rain in Spain falls mainly in the plain"counts = {}               # create an empty dictionaryfor word in sentence.lower().split():    if word in counts:        counts[word] += 1    else:			        counts[word] = 1  # create a new entryprint(counts)
# {'the': 2, 'rain': 1, 'in': 2, 'spain': 1, 'falls': 1, 'mainly': 1, 'plain': 1}
```
`counting_v2.py`
```python
sentence = "The rain in Spain falls mainly in the plain"counts = {}               # create an empty dictionary
for word in sentence.lower().split():    counts[word] = counts.get(word, 0) + 1
print(counts)
# {'the': 2, 'rain': 1, 'in': 2, 'spain': 1,
#  'falls': 1, 'mainly': 1, 'plain': 1}
```

## Slide 14
Dictionaries alias, exactly like lists
Same picture, same rule, new type.
`dict_alias.py`
```python
a = {"x": 1}
b = a             # not a copy - a second name
b["y"] = 2
print(a)          # {'x': 1, 'y': 2}
print(a is b)     # True

c = dict(a)       # a real copy  (a.copy() too)
c["z"] = 3
print(a)          # {'x': 1, 'y': 2} - untouched
```
```python
"x"
```
```python
1
```
```python
"y"
```
```python
2
```
```python
a
```
```python
b
```
```python
"x"
```
```python
1
```
```python
"y"
```
```python
2
```
```python
"z"
```
```python
3
```
```python
c
```
```python
= gives a second name. dict(d) gives a second dictionary.
```
Dictionaries
Operators
Keys
Methods & Built-ins
Looping
Functions
Nested
Sets

## Slide 15
Passing dictionaries to functions
Just like lists, dictionaries are mutable: Modifying them inside a function affects the original object.
`dict_to_function.py`
```python
def add_grade(grades, name, grade):
    scores[name] = grade   # no return

grades_dict = {"Dana Levi": 88}
add_grade(grades_dict, "Ron Cohen", 95)
print(grades_dict)
# {'Dana Levi': 88, 'Ron Cohen': 95}
```
```python
"Dana Levi"
```
```python
88
```
inside add_grade
```python
grades_dict
```
```python
grades
```
```python
"Dana Levi"
```
```python
88
```
```python
"Ron Cohen"
```
```python
95
```

## Slide 16
Class exercise: a bonus for everyone
Task: add the same bonus to every student, and let nobody pass 100.
`add_bonus.py`
```python
def add_bonus(grades, points):
    for name in grades:
        new = grades[name] + points
        grades[name] = min(new, 100)

add_bonus(grades, 7)  # it returns None
print(grades)
# {'Dana Levi': 95, 'Ron Cohen': 100,
#  'Yael Bar': 80}
```
inside add_bonus
```python
"Dana Levi"
```
```python
88
```
```python
95
```
```python
"Ron Cohen"
```
```python
95
```
```python
100
```
```python
"Yael Bar"
```
```python
73
```
```python
80
```
old
new
```python
grades
```
```python
grades
```
the same dictionary
Each slot is re-pointed to a new number. The dictionary itself is never replaced - that is why the caller sees the change.

## Slide 17
Returning a dictionary from a function
Task: Turn the list of records from the first slides into a dictionary.
`build_index.py`
```python
def build_index(students):
    grades = {}
    for name, grade in students:
        grades[name] = grade
    return grades

grades = build_index(students)
print(grades["Ron Cohen"])   # 95
print(students)   # still the list it was
```
inside build_index
```python
"Dana Levi"
```
```python
88
```
```python
"Ron Cohen"
```
```python
95
```
```python
"Yael Bar"
```
```python
73
```
```python
students
```
```python
students
```
the same list
```python
"Dana Levi"
```
```python
88
```
```python
"Ron Cohen"
```
```python
95
```
```python
"Yael Bar"
```
```python
73
```
```python
grades
```
```python
grades
```
a new dictionary
The input list remains untouched. 
The function creates and returns a new dictionary.

## Slide 18
Class exercise: Merging two dictionaries
Task: Merge two dictionaries. If a key is in both, the second dictionary wins.
`merge_bug.py`
```python
def merge(dict1, dict2):
    my_dict = dict1
    for k, v in dict2.items():
        my_dict[k] = v
    return my_dict

salaries = {"Eli": 1000, "Noam": 2000,
            "Shahar": 3000}
raises   = {"Yotam": 1800, "Moshe": 4000,
            "Shahar": 7000}
print(merge(salaries, raises))   # correct!
print(salaries)   # ... and destroyed
```
```python
"Eli"
```
```python
1000
```
```python
"Noam"
```
```python
2000
```
```python
dict1
```
```python
my_dict
```
```python
"Yotam"
```
```python
1800
```
Correct return value, corrupted input data.
```python
The hidden bug: Unexpected mutation
Invisible side effects: The return value looks correct, hiding the fact that input data was changed.
Aliasing bug: my_dict = dict1 creates an alias, not a new dictionary. Changing my_dict will cause dict1 to change too.
The fix: Create a new copy using my_dict = dict1.copy() or my_dict = dict(dict1).
```

## Slide 19
Complex values in dictionaries
Values can store lists, tuples or nested dictionaries – accessed in steps.
`nested_dict.py`
```python
school = {"Noa":  {"History": 90, "Math": 85},
          "Noya": {"History": 95, "Math": 90},
          "Alma": {"History": 82, "CS": 87}}

print(school["Noya"]["Math"])   # 90

for name, courses in school.items():
    for course, grade in courses.items():
        print(name, course, grade)
```
The nested loop is the matrices nested loop from 5-1, with names instead of positions.
```python
"Noa"
```
```python
{...}
```
```python
"Noya"
```
```python
{...}
```
```python
"Alma"
```
```python
{...}
```
```python
school
```
```python
"History"
```
```python
95
```
```python
"Math"
```
```python
90
```
First bracket selects the outer value (a dictionary); second bracket accesses its internal element.
The Noya entry, and inside it the Math entry. Two steps, two pairs of brackets.
Dictionaries
Operators
Keys
Methods & Built-ins
Looping
Functions
Nested
Sets

## Slide 20
Class exercise: Inverting a nested dictionary
Task: from student → course → grade, build course → student → grade.
`invert.py`
```python
by_course = {}

for name, courses in school.items():
    for course, grade in courses.items():
        if course not in by_course:
            by_course[course] = {}
        by_course[course][name] = grade

print(by_course)
```
`expected.txt`
```python
# {'History': {'Noa': 90, 'Noya': 95, 'Alma': 82},
#  'Math':    {'Noa': 85, 'Noya': 90},
#  'CS':      {'Alma': 87}}
```
```python
Avoiding KeyError
Initialization guard: Check if inner dictionary exists. If not, create it, empty.
Why: You cannot assign values to a key inside a non-existent dictionary.
```
by_course
```python
"History"
```
```python
"Noa"
```
```python
90
```
```python
"Noya"
```
```python
95
```
```python
"Alma"
```
```python
82
```
```python
"Math"
```
```python
"Noa"
```
```python
85
```
```python
"Noya"
```
```python
90
```
```python
"CS"
```
```python
"Alma"
```
```python
87
```
Noa is first: both her courses are new, so the guard creates an empty dictionary for each.
Noya: both courses already exist, so the guard is skipped.
Alma: History exists, but CS is new - the guard fires again, on the last pass.

## Slide 21
A set
An unordered collection of unique, immutable elements (dictionary without values, only keys).
`first_set.py`
```python
basket = {"apple", "orange", "apple",
          "pear", "orange"}
print(basket)             # in no set order
print(len(basket))        # 3
print("pear" in basket)   # True

empty_set  = set()   # the empty set
empty_dict = {}      # a DICTIONARY
```
```python
{} was taken by dictionaries first, so the empty set needs the word set().
```
```python
"apple"
```
```python
"orange"
```
```python
"apple"
```
```python
"pear"
```
```python
"orange"
```
✗
✗
```python
"apple"
```
```python
"orange"
```
```python
"pear"
```
Dictionaries
Operators
Keys
Methods & Built-ins
Looping
Functions
Nested
Sets
```python
basket
```
Key characteristics
Uniqueness: Duplicate elements are automatically removed upon creation.
Unordered: Sets do not guarantee positional index access.
Immutability: Elements inside a set must be immutable (like dictionary keys).

## Slide 22
Set operations
Operators and methods sets
`set_ops.py`
```python
s = {"milk", "bread"}
s.add("eggs")
s.remove("bread")   # KeyError if absent

set1 = {1, 5, 8, 2, 10}
set2 = {3, 6, 5, 2, 12}

print(set1 | set2)  # {1, 2, 3, 5, 6, 8, 10, 12}
print(set1 & set2)  # {2, 5}
print(set1 - set2)  # {1, 8, 10}
print(set1 ^ set2)  # {1, 3, 6, 8, 10, 12}
```
operator
method
union  
```python
|
```
```python
.union()
```
intersection  
```python
&
```
```python
.intersection()
```
difference    \
```python
-
```
```python
.difference()
```
symmetric difference
	
```python
^
```
```python
.symmetric_difference()
```
```python
set1 | set2
```
1
2
union
```python
set1 & set2
```
1
2
intersection
```python
set1 - set2
```
1
2
difference
```python
set1 ^ set2
```
1
2
one or the other
The shaded part is what the expression returns.

## Slide 23
Set comparisons
Comparison and membership operators and the methods for sets
`set_compare.py`
```python
a, b = {1, 2}, {1, 2, 3}
c = {3, 4}
nums = [1, 2, 3]

print(a <= b, a < b)        # True  True
print(b <= b, b < b)        # True  False
print(b >= a, a == {2, 1})  # True  True
print(a <= c, c <= a)       # both False
print(3 in b, 3 not in a)   # both True

print(a.isdisjoint(c))      # True - no overlap
print(a.issubset(nums))     # a list works
print(a <= nums)            # TypeError
```
operator
method
subset   
```python
<=
```
```python
.issubset()
```
proper subset  
```python
<
```
none
superset  
```python
>=
```
```python
.issuperset()
```
proper superset   
```python
>
```
none
equal    =
```python
==
```
none
disjoint
none
```python
.isdisjoint()
```
not equal
```python
!=
```
none
not member  
```python
not in
```
```python
.isdisjoint()
```
member  	
```python
in
```
none

## Slide 24
Class exercise: Is one set a subset of another?
Task: Implement a function that that checks whether set1  set2 
`subset_loop.py`
```python
def is_subset(set1, set2):
    subset = True
    for item in set1:
        if item not in set2:
            subset = False
            break
    return subset

set1 = {"apple", "orange", "pear"}
set2 = {"apple"," pear"}
print(is_subset(set1, set2)     # False
print(is_subset(set2, set1)     # True
```
Additional self practice: implement the following
.
Union
set1  set2
Proper superset
set1  set2
 
Difference
set1 \ set2
Not equal
set1  set2

## Slide 25
Primary use case: Deduplication
Removing duplicates in a single, clean step
`dedup.py`
```python
names = ["Omer", "Dana", "Omer", "Yaniv", "Dana"]
unique = set(names)

print(len(unique))      # 3
print(sorted(unique))
# ['Dana', 'Omer', 'Yaniv']
```
```python
Quick clean-up
Passing a list through set() automatically discards all repeated 
With a list: A program you give up on.
Use sorted(set(names)) to display the unique list in order.
```
```python
"Omer"
```
```python
"Dana"
```
```python
"Omer"
```
```python
"Yaniv"
```
```python
"Dana"
```
✗
✗
```python
unique
```
```python
"Dana"
```
```python
"Omer"
```
```python
"Yaniv"
```

## Slide 26
Instant lookups: Is it in ?
Checking membership without searching one-by-one
Searching a list vs. searching a set
List: Scans items one-by-one from start to finish.
Set: Calculates the exact spot and jumps directly to it.
Bottom line: If your code frequently asks "is it in the collection?", use a set instead of a list.
`in_cost.py`
```python
import time

def how_long(collection, asks):
    t = time.perf_counter()
    for w in asks:
        w in collection
    return time.perf_counter() - t

words = [str(i) for i in range(100_000)]
asks  = words[::10]                # 10,000 questions

print(how_long(words, asks))       # ~3 seconds
print(how_long(set(words), asks))  # ~0.001 seconds
```

## Slide 27
Lecture summary
list
dictionary
set
Syntax
```python
[1, 2]
```
```python
{"a": 1, "b": 2}
```
```python
{1, 2}
```
Element types
Any values
 (mutable or immutable)
Keys: Immutable
Values: any type
Immutable elements 
only
Access method
```python
Positional index (lst[i])
```
```python
Key lookup (d["a"])
```
```python
Membership check 
(elem in s) or iteration
```
Duplicates
Allowed
Keys must be unique
Not allowed
Ordering
Insertion order
Insertion order (since Python 3.7)
Unordered / Non-positional
Empty syntax
```python
[]
```
```python
{}
```
```python
set()
```
Use a dictionary when
Lookup a value by key: Each item has a unique identifier (name, ID) you search by (and not 0, 1, 2,...).
Counting & frequency: Tracking occurrences where items serve as lookup keys.
Use a set when
Existence checks: You only care if an item is in there, or not.
Duplicates must go: set(items) drops them all.
Set operation: union, intersection, difference...
Dictionaries
Operators
Keys
Methods & Built-ins
Looping
Functions
Nested
Sets

## Slide 28
What is coming
Files
Week 6: Everything today gets more interesting when the text comes from a real file.
Recursion
Week 7: A dictionary that remembers answers already computed turns a slow function into a fast one.
Efficiency
Week 9: "Essentially does not get slower" finally gets its proper name.

## Slide 29
PYTHON COURSE · WEEK 6 · LECTURE 1
Next: Files
Reading text from outside the program
