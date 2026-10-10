# Lecture 5-2: Dictionaries and sets (week 5)

## Slide 1: Dictionaries and Sets
{ }
PYTHON COURSE · WEEK 5 · LECTURE 2
Dictionaries and Sets
Finding things by name
Reichman University

## Slide 2: Finding things by name
Finding things by name
A list finds a value by its position. Often we know a name instead.
Airport codes: TLV leads to Tel Aviv
Word counts: “the” leads to 4
Student records: an ID number leads to a grade
A phone book: a name leads to a number

## Slide 3: A dictionary maps keys to values
A dictionary maps keys to values
Each key leads to exactly one value.
key
value
```python
TLV
```
Tel Aviv
```python
JFK
```
New York
```python
CDG
```
Paris
```python
NRT
```
Tokyo

## Slide 4: Terms
Terms
Key: what we look things up by
Value: what we find there
Entry: one key together with its value
Lookup: d[key] gives the value for that key

## Slide 5: A dictionary in Python
A dictionary in Python
```python
python animal_sounds.py
A cow goes moo
{'cow': 'moo', 'dog': 'bark', 'cat': 'miao'}
3
```
`animal_sounds.py`
```python
sounds = {"cow": "moo", "dog": "woof"}

print("A cow goes", sounds["cow"])
sounds["cat"] = "miao"     # adds
sounds["dog"] = "bark"     # replaces
print(sounds)
print(len(sounds))
```
[LIVE] the file is in “week 5 code / animal_sounds.py”.

## Slide 6: Reading the dictionary
Reading the dictionary
`animal_sounds.py`
```python
sounds = {"cow": "moo", "dog": "woof"}

print("A cow goes", sounds["cow"])
sounds["cat"] = "miao"     # adds
sounds["dog"] = "bark"     # replaces
print(sounds)
print(len(sounds))
```
{ key: value }
Braces around the entries; a colon inside each.
sounds[key]
Looks up the value stored for that key.
sounds[key] = v
Adds the key if it is new, replaces its value if not.

## Slide 7: When the key is not there
When the key is not there
```python
python missing_key.py
False
None
???
Traceback (most recent call last):
  ...
KeyError: 'cat'
```
`missing_key.py`
```python
sounds = {"cow": "moo", "dog": "woof"}

print("cat" in sounds)
print(sounds.get("cat"))
print(sounds.get("cat", "???"))
print(sounds["cat"])
```
[LIVE] the file is in “week 5 code / missing_key.py”.

## Slide 8: Visiting every entry
Visiting every entry
```python
python iterate_dict.py
cow goes moo
dog goes woof
cat goes miao
moo is the sound of a cow
woof is the sound of a dog
miao is the sound of a cat
['cow', 'dog', 'cat']
['moo', 'woof', 'miao']
```
`iterate_dict.py`
```python
sounds = {"cow": "moo", "dog": "woof", "cat": "miao"}

for animal in sounds:
    print(f"{animal} goes {sounds[animal]}")

for animal, sound in sounds.items():
    print(f"{sound} is the sound of a {animal}")

print(list(sounds.keys()))
print(list(sounds.values()))
```
[LIVE] the file is in “week 5 code / iterate_dict.py”.

## Slide 9: The rules for keys
The rules for keys
Unique: one value per key; a new value replaces the old
Unchangeable: str, int and tuple can be keys; a list cannot
Values: anything at all, even a list or a dict
Order: entries keep the order they were added in

## Slide 10: Keys must not change
Keys must not change
```python
python tuple_keys.py
centre
3
Traceback (most recent call last):
  ...
TypeError: unhashable type: 'list'
```
`tuple_keys.py`
```python
names = {(0, 0): "corner", (1, 1): "centre"}
print(names[(1, 1)])

names[(0, 2)] = "corner"
print(len(names))

bad = {[0, 0]: "corner"}
```
[LIVE] the file is in “week 5 code / tuple_keys.py”.

## Slide 11: Dictionaries and sets: the plan
Dictionaries and sets: the plan
Four parts today.
Dictionaries
Counting and grouping
Sets
Why they are fast

## Slide 12: Counting: the idea
Counting: the idea
In pseudocode
start with an empty dictionary
for each word in the text:
seen it before? add 1 to its count
a new word? its count is 1
report the counts
Why a dictionary
A list of counters works only when we count 0, 1, 2, …

A dictionary can count anything: words, names, colours.

## Slide 13: Counting words
Counting words
```python
python word_count.py
the 4
cat 2
saw 2
dog 2
and 1
```
`word_count.py`
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
[LIVE] the file is in “week 5 code / word_count.py”.

## Slide 14: The same, with get
The same, with get
```python
python word_count_get.py
4 2 1
0
```
`word_count_get.py`
```python
text = "the cat saw the dog and the dog saw the cat"

counts = {}
for word in text.split():
    counts[word] = counts.get(word, 0) + 1

print(counts["the"], counts["dog"], counts["and"])
print(counts.get("bird", 0))
```
[LIVE] the file is in “week 5 code / word_count_get.py”.

## Slide 15: Grouping: a dictionary of lists
Grouping: a dictionary of lists
```python
python group_by_letter.py
a ['apple', 'avocado']
b ['banana', 'blueberry']
c ['cherry']
```
`group_by_letter.py`
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
[LIVE] the file is in “week 5 code / group_by_letter.py”.

## Slide 16: Dictionaries and sets: the plan
Dictionaries and sets: the plan
Four parts today.
Dictionaries
Counting and grouping
Sets
Why they are fast

## Slide 17: Sets
Sets
No order: {4, 3, 5} and {3, 4, 5} are the same set
No duplicates: adding 4 a second time changes nothing
Membership: x in s is fast for any size of s
Elements: unchangeable values, the same rule as for keys

## Slide 18: Sets in Python
Sets in Python
```python
python set_basics.py
{1, 3, 5, 7}
{9, 1, 7}
True False
3
```
`set_basics.py`
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
[LIVE] the file is in “week 5 code / set_basics.py”.

## Slide 19: Union, intersection, difference
Union, intersection, difference
s1 = {3, 1, 5, 7}    s2 = {7, 9, 1}
```python
s1
```
```python
s2
```
3
5
1
7
9
union: in either
```python
s1 | s2  →  {1, 3, 5, 7, 9}
```
intersection: in both
```python
s1 & s2  →  {1, 7}
```
difference: in s1, not in s2
```python
s1 - s2  →  {3, 5}
```

## Slide 20: Set operations
Set operations
```python
python set_ops.py
{1, 3, 5, 7, 9}
{1, 7}
{3, 5}
True
```
`set_ops.py`
```python
s1 = {3, 1, 5, 7}
s2 = {7, 9, 1}

print(s1 | s2)       # union
print(s1 & s2)       # intersection
print(s1 - s2)       # difference
print({1, 7} <= s1)  # subset
```
[LIVE] the file is in “week 5 code / set_ops.py”.

## Slide 21: Using sets
Using sets
```python
python two_courses.py
['dana', 'maya']
['noam', 'yoni']
5
5 visits, 3 people
```
`two_courses.py`
```python
intro = {"maya", "noam", "dana", "yoni"}
calculus = {"dana", "omer", "maya"}

print(sorted(intro & calculus))    # in both
print(sorted(intro - calculus))    # intro only
print(len(intro | calculus))       # in either

visits = ["maya", "noam", "maya", "dana", "maya"]
print(f"{len(visits)} visits, {len(set(visits))} people")
```
[LIVE] the file is in “week 5 code / two_courses.py”.

## Slide 22: Which container?
Which container?
Choose by the most common operation.
list
In order, by position
Repeats allowed
t[3], t.append(x)
tuple
In order, cannot change
A fixed group of values
Can be a key
dict
Key leads to value
Look up by name
Counting, grouping
set
No order, no repeats
Fast x in s
Union, intersection

## Slide 23: Dictionaries and sets: the plan
Dictionaries and sets: the plan
Four parts today.
Dictionaries
Counting and grouping
Sets
Why they are fast

## Slide 24: A list and a set, timed
A list and a set, timed
```python
one run on a laptop
list: 8.3707 ms
set:  0.0029 ms
```
`membership_speed.py`
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
[LIVE] the file is in “week 5 code / membership_speed.py”.

## Slide 25: How a set works
How a set works
A hash function turns each key into a bucket number.
key : value
```python
63 : 9
```
```python
321 : 6
```
```python
3 : 573
```
```python
7009 : 16
```
```python
143 : 8
```
```python
h(key) = key % 10
```
0
1
2
3
4
5
6
7
8
9
buckets
```python
63 : 9
```
```python
321 : 6
```
```python
3 : 573
```
```python
7009 : 16
```
```python
143 : 8
```

## Slide 26: Why lookup is fast
Why lookup is fast
Store: compute the bucket, put the entry there
Look up: compute the bucket, search only that bucket
The result: lookup time barely depends on the size
The price: a key must never change, or its bucket is wrong

## Slide 27: Dictionaries and sets in one slide
Dictionaries and sets in one slide
dict
{key: value, ...}
d[k] looks up; d[k] = v adds or replaces
d.get(k, default) when k may be missing
for k, v in d.items()
set
set() is empty; {} is a dict
s.add(x), x in s
|  &  -  for union, intersection, difference
set(list) drops the repeats
Patterns
Counting with get(k, 0) + 1
Grouping into a dict of lists
De-duplicating with set()
Fast membership tests
