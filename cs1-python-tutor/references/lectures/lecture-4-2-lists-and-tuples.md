# Lecture 4-2: Lists and tuples (week 4)

## Slide 1
PYTHON COURSE · WEEK 3 · LECTURE 2
Lists and Tuples
Sequences that can be changed

## Slide 2
1
Lists
many values under one name
2
Mutability
a list can be changed - a new idea
3
The toolbox
operators, methods and functions
4
Tuples
a sequence that cannot change
Lecture overview
Lists
Operators
Mutability
Aliasing
Methods & Built-ins
Strings & lists
Tuples

## Slide 3
Why lists 
`many_vars.py`
```python
sale0 = 24
sale1 = 37
sale2 = 22
sale3 = 40
sale4 = 32
sale5 = 36
```
The problem: Managing 86 variables
Unmanageable Code: Handling 86 distinct variable names is repetitive and error-prone
Dynamic Changes: Opening or closing a branch requires manually re-editing the code (adding or removing variables).
No Iteration: A numbered sequence of variables (sale0, sale1, sale2...) is not a sequence that a computer can easily iterate through with a loop.
How would you compute the total sales?
How would you find the best branch?
How would you count those above average?
Lists
Operators
Mutability
Aliasing
Methods & Built-ins
Strings & lists
Tuples

## Slide 4
A list
A sequence of values - One name, many values, square brackets, commas between.
`first_list.py`
```python
sales = [24, 37, 22, 40, 32, 36]

print(sales)        # the whole list
print(len(sales))   # 6
```
`list_kinds.py`
```python
names = ["Omer", "Dana", "Yaniv"]
mixed = ["Omer", 21, 92.5, True]
empty = []                 # len 0
```
```python
sales
```
```python
24
```
```python
37
```
```python
22
```
```python
40
```
```python
32
```
```python
36
```
```python
0
```
```python
1
```
```python
2
```
```python
3
```
```python
4
```
```python
5
```
```python
"Omer"
```
```python
21
```
```python
92.5
```
```python
True
```
One picture, four types: a list holds anything.
```python
Three things to notice
len: How many items - as for a string.
print shows brackets: A list as you would type it.
Order is part of it: [24, 37] is not [37, 24].
```
```python
mixed
```

## Slide 5
A list is a sequence
Standard sequence operations apply to both strings and lists.
`sequence_ops.py`
```python
print(sales[0])      # 24
print(sales[-1])     # 36
print(sales[1:4])    # [37, 22, 40]
print(sales[::2])    # [24, 22, 32]
print(22 in sales)   # True
print(sales[6])      # IndexError
```
A slice gives a list; an index gives an item.
```python
P
```
```python
y
```
```python
t
```
```python
h
```
```python
o
```
```python
n
```
```python
0
```
```python
1
```
```python
2
```
```python
3
```
```python
4
```
```python
5
```
```python
24
```
```python
37
```
```python
22
```
```python
40
```
```python
32
```
```python
36
```
```python
s = "Python"
```
```python
sales = [24, …]
```
```python
sales[1:4]
```
```python
What transfers, unchanged
Indexing: From 0; negative from the right.
Slicing: Stop excluded, with a step.
in and len : Membership and length.
Past the end: IndexError, as before.
```
```python
[ ]
```
indexing
```python
[ : : ]
```
slicing
```python
in
```
```python
not in
```
```python
s[1:4] 
```
Lists
Operators
Mutability
Aliasing
Methods & Built-ins
Strings & lists
Tuples

## Slide 6
Looping over a list
Direct vs. Indexed loop
`loop_list.py`
```python
# when you only need the values:
for sale in sales:
    print(sale)

# when you need the position too:
for i in range(len(sales)):
    print("Branch:", i, "sales:", sales[i])
```
By value when the value is all you need,
By position when the index is part of the task.
```python
24
```
```python
37
```
```python
22
```
```python
40
```
```python
32
```
```python
36
```
```python
sale
```
```python
24
```
```python
61
```
```python
83
```
```python
123
```
```python
155
```
```python
191
```
total after each pass — the accumulator, unchanged.
`total.py`
```python
total = 0
for sale in sales:
    total = total + sale
print("Total:", total)    # 191
```

## Slide 7
Concatenation and repetition
Two more operators carry over, with the same meanings.
`plus_times.py`
```python
print(sales + [50])   # one longer list
print([0] * 4)        # [0, 0, 0, 0]
print([1] + [2])      # [1, 2] — not [3]
print(sales + 50)     # TypeError
```
```python
What they mean
+ : A new, longer list - not a sum.
* : A list of a known size.
Type rule: Only a list adds to a list.
```
```python
24
```
```python
37
```
```python
+
```
```python
50
```
```python
=
```
```python
24
```
```python
37
```
```python
50
```
```python
0
```
```python
* 4
```
```python
0
```
```python
0
```
```python
0
```
```python
0
```
```python
+
```
concatenation
```python
*
```
repetition
What is really inside a cell? Later today.

## Slide 8
Lists are mutable
A list can be changed in place (unlike any other data type seen so far).
nums[0] =
A white board is mutable: Its content can be erased and updated directly.
An e-mail already sent is immutable: Changing it means sending a new e-mail.
The core concepts
Mutable: An object whose content can be modified in place (e.g., list).
Immutable: An object whose value cannot be changed after creation (e.g., string, int, float, bool).
`mutable.py`
```python
s = "Python"
s[0] = "J"        # TypeError

nums = [1, 2, 3]
nums[0] = 99      # no error
print(nums)       # [99, 2, 3]
```
Refused on a string. Accepted on a list — the cell simply holds something else.
1
99
Lists
Operators
Mutability
Aliasing
Methods & Built-ins
Strings & lists
Tuples

## Slide 9
Lists are mutable
Last lecture a change built a new object. Is this the same trick?
`id_same.py`
```python
nums = [1, 2, 3]
print(id(nums))   # 140234618509296
nums[0] = 99
print(id(nums))   # 140234618509296
```
The same number. The very same list.
```python
s
```
```python
P
```
```python
y
```
```python
t
```
```python
h
```
```python
o
```
```python
n
```
```python
J
```
```python
y
```
```python
t
```
```python
h
```
```python
o
```
```python
n
```
A string: the name is moved to a new object.
```python
nums
```
```python
99
```
```python
2
```
```python
3
```
```python
id: unchanged
```
A list: the name never moves. The boxes change.

## Slide 10
Class exercise - squares
Task: Given a list of numbers, replace every item with its square.
```python
my_list = [4, 2, 5, 7]
for num in my_list:
    num = num ** 2
print(my_list)
```
```python
4
```
```python
2
```
```python
5
```
```python
7
```
```python
num
```
```python
16
```
`squares_fixed.py`
```python
my_list = [4, 2, 5, 7]
for i in range(len(my_list)):
    my_list[i] = my_list[i] ** 2
print(my_list)        # [16, 4, 25, 49]
```
```python
4
```
```python
2
```
```python
5
```
```python
7
```
`squares_broken.py`
Incorrect: The temporary loop variable (num) is squared, but the original list is unaffected.
```python
# [4, 2, 5, 7]
```
✗
Correct: Accessing elements by index allows direct modification of the list’s content.
✓
```python
16
```

## Slide 11
Lists are dynamic
Lists allow you to add and remove elements dynamically
`grow.py`
```python
guests = ["Omer"]
guests.append("Dana")      # add at the end
guests.insert(1, "Yael")   # add at a position
guests.remove("Omer")      # remove by value
last = guests.pop()        # remove & return last
print(guests)              # ['Yael']
```
```python
Some details
.remove(x) : Deletes only the first matching element. If x not found, raises a ValueError.
.pop() : Removes and returns last element.
	    
```
```python
"Omer"
```
```python
.append("Dana")
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
"Dana"
```
```python
0
```
```python
1
```
```python
.insert(1, "Yael")
```
```python
"Omer"
```
```python
"Yael"
```
```python
"Dana"
```
```python
0
```
```python
1
```
```python
2
```
Dana was at 1, and is now at 2: the rest shifts right.
`build_loop.py`
```python
squares = []
for i in range(5):
    squares.append(i * i)
print(squares)      # [0, 1, 4, 9, 16]
```
Accumulator pattern that creates a list

## Slide 12
The trap: changing a list while looping
Task: Given a list, remove every 2 from it.
```python
nums = [1, 2, 2, 3]
for n in nums:
    if n == 2:
        nums.remove(n)
print(nums)
```
```python
What a for loop really does
By position: Even with no index written.
remove shortens it: Under the loop.
```
```python
1
```
```python
2
```
```python
2
```
```python
3
```
```python
0
```
```python
1
```
```python
2
```
```python
3
```
```python
1
```
position 0: 1 is not a 2.
```python
1
```
```python
2
```
```python
2
```
```python
3
```
```python
0
```
```python
1
```
```python
2
```
```python
3
```
```python
2
```
position 1: a 2 - removed.
```python
1
```
```python
2
```
```python
3
```
```python
0
```
```python
1
```
```python
2
```
```python
3
```
```python
2
```
shifted left: the second 2 is now at 1 - behind us.
```python
1
```
```python
2
```
```python
3
```
```python
0
```
```python
1
```
```python
2
```
position 3 is past the end - the loop stops.
The 2 at position 1 was never examined.
What went wrong ?
`remove2_bug.py`
Incorrect: one of the 2s is still in the list.
✗
```python
# [1, 2, 3]
```

## Slide 13
Two fixes — is each one right?
Same task: remove every 2.
`remove2_v1.py`
```python
nums = [1, 2, 2, 3]
kept = []
for n in nums:
    if n != 2: kept.append(n)
print(kept)
```
```python
# [1, 3]
```
✓
correct
Nothing is removed, so the list being walked never changes.
`remove2_v2.py`
```python
nums = [1, 2, 2, 3]
for n in nums[:]:   # walk a copy
    if n == 2: nums.remove(n)
print(nums)
```
```python
# [1, 3]
```
✓
correct
```python
nums[:] is a copy: the loop walks the copy, and we edit the original.
```

## Slide 14
Another fix - without a copy
Can it be done without a second copy of the list?
`remove_while.py`
```python
nums = [1, 2, 2, 3]
i = 0
while i < len(nums):
    if nums[i] == 2:
        nums.pop(i) # remove by position                    
        # do not advance i
    else: i = i + 1
```
```python
Why it works
Ours to advance: A while loop does not.
Remove, and stay: The next item slid in.
```
```python
1
```
```python
2
```
```python
2
```
```python
3
```
```python
0
```
```python
1
```
```python
2
```
```python
3
```
```python
2
```
i = 1: a 2 — pop(1), and i stays 1.
```python
1
```
```python
2
```
```python
3
```
```python
0
```
```python
1
```
```python
2
```
```python
2
```
i = 1 again: another 2 — pop(1), i stays.
```python
1
```
```python
3
```
```python
0
```
```python
1
```
```python
3
```
i = 1: a 3 — now i becomes 2.
```python
1
```
```python
3
```
```python
0
```
```python
1
```
i = 2 = len(nums): the loop stops.
The result is [1, 3]: nothing skipped, no copy made.
.pop(i): the method from the table, with a position.

## Slide 15
Assigning lists using = operator
Predict: what is lst1, after the third line?
`alias.py`
```python
lst1 = [1, 2, 3]
lst2 = lst1
lst2.append(4)

print(lst1)
print(lst1 is lst2)
```
lst2 = lst1 gives the list labled as lst1 a second name
but doesn’t create a second list.
```python
lst1
```
```python
lst2
```
```python
1
```
```python
2
```
```python
3
```
```python
4
```
```python
1
```
```python
2
```
```python
3
```
```python
1
```
```python
2
```
```python
3
```
```python
4
```
```python
lst1
```
```python
lst2
```
What you might expect – but it is not what happens.
```python
# [1, 2, 3, 4]
```
```python
# True
```
✗
```python
The is operator
a is b: Are a and b the same object?
	Equivalent to id(a) == id(b).
a == b: Do a and b have same values?
```
What it really looks like: One list, two names. Either name can change it.
✓
Lists
Operators
Mutability
Aliasing
Methods & Built-ins
Strings & lists
Tuples

## Slide 16
Making a real copy
If two names is not what you want, ask for a copy.
`copy_list.py`
```python
lst1 = [1, 2, 3]
lst3 = lst1.copy()            # or list(lst1)

print(lst1 == lst3)       # True   - same values
print(lst1 is lst3)       # False  - different objects

lst3.append(5)
print(lst1)            # [1, 2, 3]
```
A slice of everything — which by definition is a new list.
```python
lst1
```
```python
1
```
```python
2
```
```python
3
```
```python
lst3
```
```python
1
```
```python
2
```
```python
3
```
```python
5
```
```python
lst1 == lst3  True
```
```python
lst1 is lst3  False
```
Equal, but not identical
Copy first: If you need the original as well.
Otherwise share: Copying a large list costs time.

## Slide 17
What is inside a cell
A cell holds a reference to a value, not the value itself.
`inside_cell.py`
```python
nums = [10, 20, 30]    # an ordinary list
x = nums[0]            # a second name
print(x is nums[0])    # True

nums[0] = 99           # re-point the cell
print(nums)            # [99, 20, 30]
print(x)               # 10  — still the 10
```
Assignment to an item changes the list, never the object it held.
```python
0
```
```python
↓
```
```python
1
```
```python
↓
```
```python
2
```
```python
nums
```
```python
10
```
```python
20
```
```python
30
```
three separate objects
```python
x
```
x is nums[0] — the same object
```python
99
```
Cell 0 now refers to a different object. The 10 is still there, unchanged — which is why x still prints 10.
```python
↓
```

## Slide 18
```python
And under the * operator
```
```python
So what does [0] * 4 actually build?
```
`star_cells.py`
```python
a = [0] * 4

print(a[0] is a[1])   # True

a[0] = 5
print(a)              # [5, 0, 0, 0]
```
Sharing is invisible while the value cannot change.
```python
↓
```
```python
↓
```
```python
↓
```
```python
↓
```
```python
a
```
```python
0
```
one object, four cells
```python
5
```
a[0] = 5 re-points one cell

## Slide 19
Why this matters
Three consequences, and one promise.
```python
Three consequences
A change through one name
is visible through every name: a feature with one shared list, a bug when you thought you had two.
Equality and identity
are different questions. == for values, is for objects.
Strings never posed this
because a string cannot be changed, so aliasing one is invisible.
```
```python
1
```
```python
2
```
```python
3
```
```python
def  ?
```
Next week: a list passed to a function can be changed by it.

## Slide 20
```python
+= and *= operators
```
In-place modification vs. Reassignment
```python
+ and * build a new list
```
```python
+= and *= modify the existing object in-place
```
`new_list.py`
```python
a = [1, 2, 3]
b = a
a = a + [4]

a = [1, 2]
b = a
a = a * 3
```
`in_place.py`
```python
a = [1, 2, 3]
b = a
a += [4]

a = [1, 2]
b = a
a *= 3
```
```python
1
```
```python
2
```
```python
3
```
```python
a
```
```python
b
```
```python
1
```
```python
2
```
```python
3
```
```python
4
```
```python
b
```
```python
1
```
```python
2
```
```python
3
```
```python
a
```
```python
4
```
```python
1
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
1
```
```python
2
```
```python
1
```
```python
2
```
```python
1
```
```python
2
```
```python
b
```
```python
1
```
```python
2
```
```python
a
```
```python
1
```
```python
2
```
```python
1
```
```python
2
```
```python
+=
```
```python
*=
```
```python
+
```
```python
*
```

## Slide 21
Common list methods
method
what it does
example
```python
.append(x)
```
Adds x at the end of the list.
```python
a.append(4)
```
```python
.insert(i, x)
```
Puts x at position i, shifts the rest right. ; error for invalid index.
```python
a.insert(0, 9)
```
```python
.remove(x)
```
Removes the first x; error if there is none.
```python
a.remove(2)
```
```python
.pop(i)
```
Removes the item in index and returns it; error for invalid index.
When called with no parameters (.pop()) – 
Removes the last item and returns it. 
```python
last = a.pop()
first = a.pop(0)
```
```python
.index(x)
```
Position where x first appears; error if absent.
```python
a.index(3)
```
```python
.count(x)
```
How many times x appears, as an int.
```python
a.count(2)
```
```python
.sort()
```
Puts the list in order, in place.
```python
a.sort()
```
```python
.reverse()
```
Turns the list back to front, in place.
```python
a.reverse()
```
All change the list and return nothing — except .pop, .index and .count, which answer a question.
```python
.copy()
```
Creates a shallow copy of the list and returns it.
```python
b = a.copy()
```
Lists
Operators
Mutability
Aliasing
Methods & Built-ins
Strings & lists
Tuples

## Slide 22
Built-in functions that work on lists
Functions, not methods: the list goes inside the parentheses.
`builtins.py`
```python
print(len(sales))     # 6
print(sum(sales))     # 191
print(min(sales))     # 22
print(max(sales))     # 40
print(sorted(sales))  # a new list
print(sales)          # unchanged
```
```python
24
```
```python
37
```
```python
22
```
```python
40
```
```python
32
```
```python
36
```
```python
min, max and sorted work on strings too: sorted("banana") is a list of its letters, in order.
```
```python
sales
```
```python
len
```
```python
6
```
```python
sum
```
```python
191
```
```python
min
```
```python
22
```
```python
max
```
```python
40
```
```python
sorted
```
```python
22
```
```python
24
```
```python
32
```
```python
36
```
```python
37
```
```python
40
```

## Slide 23
The sort trap
```python
Methods that modify mutable objects in place, return None.
```
`sort_trap.py`
```python
nums = [3, 1, 2]
nums.sort()
print(nums)        # [1, 2, 3]
result = nums.sort()
print(result)      # None

nums = [3, 1, 2]
result = sorted(nums)
print(result)      # [1, 2, 3]
print(nums)        # [3, 1, 2]  unchanged
```
```python
.sort()
```
```python
None
```
Modified in place
```python
3
```
```python
1
```
```python
2
```
```python
sorted()
```
```python
1
```
```python
2
```
```python
3
```
Returns a new list - must be assigned
```python
In-place vs. Returning functions\methods
In-place modification: If a method modifies the original object directly, it returns None. 
New object creation: If an operation cannot or does not modify the original, it returns a new object.
General rule : Applies across all mutable data types in Python.
```
```python
1
```
```python
2
```
```python
3
```
```python
3
```
```python
1
```
```python
2
```

## Slide 24
The split method
A string method that converts a single string into a list of substrings.
`split.py`
```python
line = "Omer Dana Yaniv"
print(line.split())      # ['Omer', 'Dana', 'Yaniv']

print("24,37,22".split(","))
# ['24', '37', '22']   — on a given separator

print(list('hello'))     # one item per character
```
 Splitting options: default whitespace, explicit delimiter or char-by-char via list()
```python
"Omer"
```
```python
"Dana"
```
```python
"Yaniv"
```
Returns a list of strings
`split_cast.py`
```python
parts = "24,37,22".split(",")
total = 0
for p in parts:
    total += int(p)    # 83
```
Always returns strings; explicit type casting (e.g., int()) is required for numeric processing
```python
O
```
```python
m
```
```python
e
```
```python
r
```
```python
␣
```
```python
D
```
```python
a
```
```python
n
```
```python
a
```
```python
␣
```
```python
Y
```
```python
a
```
```python
n
```
```python
i
```
```python
v
```
Lists
Operators
Mutability
Aliasing
Methods & Built-ins
Strings & lists
Tuples

## Slide 25
The join method
A string method that concatenates a list of strings into a single string using a delimiter.
`join.py`
```python
names = ["Omer", "Dana", "Yaniv"]
print(' '.join(names))    # 'Omer Dana Yaniv'
print(', '.join(names))   # 'Omer, Dana, Yaniv'
print("-".join(["22", "09", "2026"])) # '22-09-2026'
```
```python
Read it as: "delimiter ".join(list) – use this separator to glue these items together.
```
```python
"Omer"
```
```python
"Dana"
```
```python
"Yaniv"
```
```python
The core rules
Separator syntax: .join() is called on the delimiter string, not on the list                         (e.g., " ".join(names), not names.join(" ")).
Every item must be a string: Other types raise a TypeError.
split and join: Inverse operations - cut, work, glue.
```
```python
O
```
```python
m
```
```python
e
```
```python
r
```
```python
␣
```
```python
D
```
```python
a
```
```python
n
```
```python
a
```
```python
␣
```
```python
Y
```
```python
a
```
```python
n
```
```python
i
```
```python
v
```

## Slide 26
Worked example: counting words
Task: Given a sentence, count its words and determine the longest word.
```python
The idea: .split() gives the words, len() counts them, then the maximum-pattern loop.
```
`word_count.py`
```python
sentence = input("Sentence: ")
words = sentence.split()
print("Words:", len(words))

longest = words[0]
for word in words:
    if len(word) > len(longest):
        longest = word
print("Longest:", longest)
```
```python
the
```
```python
quick
```
```python
brown
```
```python
elephant
```
```python
ran
```
```python
elephant
```
longest, after the last pass
word
len
longest
```python
the
```
```python
3
```
```python
the
```
```python
quick
```
```python
5
```
```python
quick
```
```python
brown
```
```python
5
```
```python
quick
```
```python
elephant
```
```python
8
```
```python
elephant
```
```python
ran
```
```python
3
```
```python
elephant
```
`word_count.py`
```python
sentence = input("Sentence: ")
words = sentence.split()
print("Words:", len(words))
if len(words) > 0:
    longest = words[0]
    for word in words:
        if len(word) > len(longest):
            longest = word
    print("Longest:", longest)
```
```python
What if the user typed nothing (just Enter)?
words list is empty, so words[0] raises an IndexError.
How to avoid it ?
Check if len(words) > 0 before accessing index 0.
```

## Slide 27
The sales report, finished
Task: Total, average, best branch, how many above average.
The idea: one pass to total, a second pass to count.
`sales_report.py`
```python
sales = [24, 37, 22, 40, 32, 36]
total = sum(sales)
average = total / len(sales)
best = max(sales)
best_branch = sales.index(best)
above = 0
for sale in sales:
    if sale > average: above = above + 1
```
```python
24
```
```python
37
```
```python
22
```
```python
40
```
```python
32
```
```python
36
```
```python
0
```
```python
1
```
```python
2
```
```python
3
```
```python
4
```
```python
5
```
```python
average
```
```python
output
```
```python
Total: 191
Average: 31.833333333333332
Best region: 3 with 40
Regions above average: 4
```

## Slide 28
Class exercise: Reordering by a permutation
```python
Task: build a new list of the items of my_list in the order per dictates.
```
```python
The idea: per holds a permutation of the indices. Each value of per is a position in my_list.
```
`permutation.py`
```python
my_list = [100, 23, 43, 12]
per = [2, 3, 0, 1]

result = []
for i in per:
    result.append(my_list[i])

print(result)    # [43, 12, 100, 23]
```
Indirect iteration (Index-as-Data)
Values as indices: The elements of per serve as indices rather than raw data values.
Indirect lookup : The loop variable i represents a valid index used access my_list[i].
```python
Accumulator pattern: result dynamically grows from empty with .append.
```

## Slide 29
Class exercise: Collapsing repeated runs
Task: Collapse consecutive duplicate items into a single instance
```python
10
```
```python
10
```
```python
10
```
```python
5
```
```python
5
```
```python
6
```
```python
6
```
```python
6
```
```python
6
```
```python
7
```
```python
2
```
```python
2
```
```python
2
```
```python
10
```
```python
10
```
```python
10
```
```python
5
```
```python
6
```
```python
7
```
```python
2
```
```python
10
```
```python
10
```
```python
10
```
The idea: Append an item only if it differs from the last item already added.
`collapse_runs.py`
```python
list2 = [list1[0]]
for elem in list1:
    if elem != list2[-1]:
        list2.append(elem)
```
```python
Key points
list2[-1] : Accesses the last appended item.
Seeded initialization: list2 is initialized with one item (list1[0]) to safely allow list2[-1] access without raising an IndexError on an empty list. 
```

## Slide 30
A tuple
An immutable sequence of values - Round brackets, commas between, fixed once created. Provides storage for heterogeneous data.
`tuple_basics.py`
```python
point = (3, 4)
student = ("Dana Levi", 012345678"", 88)

print(point[0])      # 3
print(len(point))    # 2
print(3 in point)    # True
print(student[0:2])  # ("Data Levi", 012345678"")

point[0] = 5         # TypeError
student.append(5)      # AttributeError
```
```python
Syntax: Round brackets () instead of square [].
Functions, methods and operators: Indexing, slicing, in, len, count, +, * and other read only sequence operations.
```
```python
3
```
```python
4
```
```python
x
```
```python
y
```
```python
(3, 4)
```
```python
"Dana Levi"
```
```python
"012345678"
```
```python
88
```
Lists
Operators
Mutability
Aliasing
Methods & Built-ins
Strings & lists
Tuples

## Slide 31
string, list or tuple: how to choose?
str
list
tuple
How it is written
```python
"Hi"
```
```python
[1, 2]
```
```python
(1, 2)
```
What it holds
characters
any values 
(usually homogeneous)
any values
(usually heterogeneus)
Can be changed (Mutable)
✗
✓
✗
Methods that change it
none
```python
.append .sort ...
```
none
Indexing, slicing, in, len, for
the same
the same
the same
Its size
fixed
dynamic
fixed
Choose a list when
Homogeneous collection: Storing sequence items of the same conceptual type (e.g., branches, scores, words).
Mutability required: Add, remove or sort in-place.
Dynamic size: Collection length changes over time.
Choose a tuple when
Heterogeneous collection: Grouping fixed attributes of a single entity (e.g., (x,y) coordinates, date, student's record).
Immutability guarantee: Preventing accidental modifications.

## Slide 32
Class exercise: how immutable is immutable?
Predict the output:
`tuple_with_list.py`
```python
my_tuple = ("Bennie", 47,
            ["Bernard", "Aaliyah"])
my_tuple[2].append("Sydney")
print(my_tuple)
```
```python
The core principle: Shallow immutability
A tuple guarantees its own shape: How many items, and which objects they refer to.
It guarantees nothing about what those objects contain. If an element in a tuple is mutable (e.g., a list), the underlying object itself can still be mutated in-place.
Reassignment vs. Mutation: 
my_tuple[2].append(...) mutates the inner object (allowed).
my_tuple[2] = [] attempts to reassign the tuple’s reference (TypeError).
```
```python
# ('Bennie', 47,
```
```python
#  ['Bernard', 'Aaliyah', 'Sydney'])
```
```python
my_tuple[2] = []
```
```python
                      # TypeError
```
```python
my_tuple
```
```python
0
```
```python
1
```
```python
2
```
```python
"Bennie"
```
```python
47
```
```python
"Bernard"
```
```python
"Aaliyah"
```
```python
"Sydney"
```
```python
list
```
```python
int
```
```python
string
```

## Slide 33
Packing & unpacking
The feature that makes tuples worth their slide.
`pack-unpack.py`
```python
point = 3, 4      # packing
x, y = point      # unpacking
print(x, y)       # 3 4

# unpacking lists
data = "Elazar Haim Ruti"
name1, name2, name3 = data.split()
```
```python
3
```
```python
4
```
```python
3
```
```python
4
```
```python
point
```
packing: the comma builds one tuple
```python
3
```
```python
4
```
```python
x
```
```python
y
```
unpacking: one name per item

## Slide 34
The swap, two ways
The same exchange, with a temporary variable or with packing & unpacking.
`swap_temp.py`
```python
x, y = 3, 4

temp = x
x = y
y = temp
print(x, y)       # 4 3
```
`swap.py`
```python
3
```
```python
4
```
```python
4
```
```python
3
```
packing
```python
4
```
```python
3
```
unpacking
x
y
x
y
```python
x, y = y, x       # the swap: packing & unpacking
print(x, y)       # 4 3
```
```python
x
```
```python
y
```
```python
temp
```
```python
3
```
```python
4
```
```python
—
```
```python
x, y = 3, 4
```
```python
3
```
```python
4
```
```python
3
```
```python
temp = x
```
```python
4
```
```python
4
```
```python
3
```
```python
x = y
```
```python
4
```
```python
3
```
```python
3
```
```python
y = temp
```

## Slide 35
```python
"Yael Bar"
```
Class exercise: Parallel lists
Task: Maintain dynamic student records (name, ID, grade) through additions and deletions.
`parallel_lists.py`
```python
names = ["Dana Levi", "Ron Cohen", "Yael Bar"]
ids = ["012345678", "305128744", "211980365"]
grades = [88, 95, 73]

print(names[1], ids[1], grades[1])
# Ron Cohen 305128744 95
```
`parallel_lists.py`
```python
names.remove("Ron Cohen")   # a student leaves
print(names[1], ids[1], grades[1])
# Yael Bar 305128744 95
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
"012345678"
```
```python
"305128744"
```
```python
"211980365"
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
names
```
```python
ids
```
```python
grades
```
```python
"Dana Levi"
```
Structural flaws
Manual sync required: Adding or removing data requires modifying three separate lists in exact order. 
Index shift: Deleting an element from one list shifts its indices, causing complete cross-list misalignment. 
The requirement: We need a single atomic structure that binds related fields together. 
Desynchronization error: Yael Bar now pairs with Ron Cohen's ID and grade

## Slide 36
```python
"Dana Levi"
```
```python
"012345678"
```
```python
88
```
```python
0
```
```python
"Yael Bar"
```
```python
"211980365"
```
```python
73
```
```python
1
```
Class exercise: The solution - a list of tuples
`List_of_tuples.py`
```python
students = [("Dana Levi", "012345678", 88),
            ("Ron Cohen", "305128744", 95),
            ("Yael Bar", "211980365", 73)]

print(students[1])  # ('Ron Cohen ', '305128744', 95)
```
```python
"Dana Levi"
```
```python
"012345678"
```
```python
88
```
```python
0
```
```python
"Ron Cohen"
```
```python
"305128744"
```
```python
95
```
```python
1
```
```python
"Yael Bar"
```
```python
"211980365"
```
```python
73
```
```python
2
```
```python
students
```
Atomic record benefits
Encapsulation: Name, ID, and grade are coupled into a single, inseparable tuple.
Safe Operations: Adding or removing an entry affects the entire tuple, preventing partial shifts or mismatched fields.
Immutability: Tuple immutability guarantees that fields within a record cannot be accidentally mixed up.
Task: Maintain dynamic student records (name, ID, grade) through additions and deletions.
`List_of_tuples.py`
```python
students.pop(1)   # Ron Cohen leaves
print(students[1]) # ('Yael Bar ', '211980365', 73)
```

## Slide 37
Class exercise: Processing records
Task: Print the name and grade of the student with the highest score.
The idea: apply maximum finding pattern to track the top record.
`top_student.py`
```python
students = [("Dana Levi", "012345678", 88),
            ("Ron Cohen", "305128744", 95),
            ("Yael Bar", "211980365", 73)]

best = students[0]
for student in students:
    if student[2] > best[2]:
        best = student
name, sid, grade = best   # unpacking
print(name, grade)        # Ron Cohen 95
```
```python
"Dana Levi"
```
```python
"012345678"
```
```python
88
```
```python
0
```
```python
"Ron Cohen"
```
```python
"305128744"
```
```python
95
```
```python
1
```
```python
"Yael Bar"
```
```python
"211980365"
```
```python
73
```
```python
2
```
```python
students
```
```python
best
```
No shortcuts for maximum
Finding the maximum requires going through every student.

## Slide 38
Task: Find and print Ron Cohen's grade (by name).
`find_student.py`
```python
for name, sid, grade in students:
    if name == "Ron Cohen":
        print(grade)          # 95
        break
```
The goal: Access records directly by name without intermediate position searches.
Coming up in Week 5 ...
```python
"Dana Levi"
```
```python
"012345678"
```
```python
88
```
```python
0
```
```python
"Ron Cohen"
```
```python
"305128744"
```
```python
95
```
```python
1
```
```python
"Yael Bar"
```
```python
"211980365"
```
```python
73
```
```python
2
```
✗
✓
Finding a record by name – the cost
Unlike finding a maximum, accessing one student shouldn’t require looking at others.
Lists only support positional indices, forcing us to scan items sequentially.
Absent target forces an unnecessary pass through the entire list
Class exercise: Looking up a record by name
name
position
value
a middleman step we never wanted
```python
students
```

## Slide 39
Lecture summary
```python
The new ideas
A list
a mutable sequence of elements (usually homogeneous)
Lists are mutable
a[0] = x, the methods and += change the list itself.
b = a does not copy
one list, two names; a[:] copies it.
A cell holds a reference
re-points the cell, not the object.
A tuple
an immutable sequence of elements (usually heterogeneous)
```
Working with lists & tuples
```python
list
```
```python
tuple
```
Operators
```python
[], [:], in, +, *
+= and *=
```
```python
[], [:], in, +, *
+= rebinds, as on a string
```
```python
join, packing,
unpacking
```
Functions
```python
len, sum, min, max
sorted
```
```python
len, sum, min, max
sorted
```
Methods
```python
append, insert, remove
pop, sort, reverse
index, count
```
```python
index, count
```
More
```python
split, join, unpacking
```
Lists
Operators
Mutability
Aliasing
Methods & Built-ins
Strings & lists
Tuples

## Slide 40
PYTHON COURSE · WEEK 4 · LECTURE 1
Next: Functions
Naming a piece of work, and reusing it
