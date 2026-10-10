# Lecture 3-1: Strings (week 3)

## Slide 1
PYTHON COURSE · WEEK 3 · LECTURE 1
Strings
Indexing, slicing, immutability and methods

## Slide 2
Lecture overview
Basics
Indexing & slicing
Immutability
Unicode
Operators
Methods
Examples
1
A string
characters in a row, numbered from 0
2
Indexing and slicing
one character, or a piece
3
Immutability
every change builds a new string
4
Methods
upper, strip, find, replace — and the cipher

## Slide 3
Writing a string
Single or double quotes: the result is the same.
`quotes.py`
```python
a = "double quotes"
b = 'single quotes'
c = "it's fine inside double quotes"
d = 'and "quotes" inside single ones'
```
PEP 8 has no preference. Be consistent.
```python
Escape sequences
\n : A new line.
\" and \' : A quote that does not end the string.
\\ : One backslash.
```
`print.py`
```python
print("I don't like\nthe word \"no\"")
```
```python
\
```
```python
n
```
typed
```python
?
```
stored
As how many characters?
```python
terminal
```
```python
I don't like
the word "no"
```
Basics
Indexing & slicing
Immutability
Unicode
Operators
Methods
Examples

## Slide 4
A string is a sequence of characters
Every character in the sequence has a position (index), starting with 0.
```python
A
```
```python
s
```
```python
␣
```
```python
e
```
```python
a
```
```python
s
```
```python
y
```
```python
␣
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
6
```
```python
7
```
```python
len(s) = 8
```
```python
last position = len(s) - 1 = 7
```
`len.py`
```python
print(len(s))      # 8
print(len("Hi"))   # 2
print(len(""))     # 0
```
```python
↵
```
```python
len("\n") = 1
```
```python
A new built-in function: len
len(s) : The number of characters, as an int.
Same family: print, input, int, str: the name, then the value in parentheses.
Spaces count: A string holds exactly what is between the quotes.
Last position: len(s) - 1, since positions start at 0.
```
Each character is itself a number — later in this lecture.

## Slide 5
Direct iteration over strings
A for loop iterates over any sequence, including strings. 
`letters.py`
```python
for ch in "binary":
    print(ch)
```
```python
output
```
```python
b
i
n
a
r
y
```
```python
b
```
```python
i
```
```python
n
```
```python
a
```
```python
r
```
```python
y
```
One character at a time, in order.
```python
Already known
Direct iteration: for ch in s visits every character from left to right (Lecture 2-2).
Limitations: Does not allow picking a specific index (e.g. the 5th or last character) or iterating in a custom order.
```

## Slide 6
The questions we ask about text
Before the tools: what do we actually want to ask?
```python
A
```
```python
A
```
```python
T
```
```python
T
```
```python
T
```
```python
G
```
```python
C
```
```python
A
```
```python
T
```
```python
T
```
```python
C
```
```python
dna = "AATTTGCATTC"
```
What is at
position 4?
Does "TGC" appear anywhere?
What are the last three bases?
How many times does "T" appear?
Where does "G" first appear?
Are these two
sequences equal?
Do they match if we ignore case?
Does "C?T" appear, 
if ? is any base?

## Slide 7
Indexing
```python
s[i] is the character at position i.
```
`index.py`
```python
s = "Python"
print(s[0])    # P
print(s[5])    # n
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
6
```
```python
IndexError
```
What comes back
A string of length 1: There is no separate character type.
```python
One past the end
Valid indices: 0 to len(s) - 1.
s[len(s)]: Raises an IndexError.
```
```python
s[0]
```
```python
P
```
a string of length 1
Basics
Indexing & slicing
Immutability
Unicode
Operators
Methods
Examples

## Slide 8
Negative indices
A negative index counts from the end, starting at -1.
`negative.py`
```python
s = "Python"
print(s[-1])   # n
print(s[-2])   # o
print(s[-6])   # P
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
-6
```
```python
-5
```
```python
-4
```
```python
-3
```
```python
-2
```
```python
-1
```
```python
Why negative indices?
s[-1]: The last character, in the usual form.
s[len(s) - 1]: The same character, longer to write and easier to get wrong.
No -0: Index 0 is always the first character.
```
Two numbering systems, one row of boxes.

## Slide 9
Example: is it a palindrome?
Task: Given a string, check if it is a palindrome (reads the same forwards and backwards).
The idea: compare the first and last characters, then move inward.
`palindrome_idx.py`
```python
word = input("Enter a word: ")
palindrome = True
for i in range(len(word) // 2):
    if word[i] != word[-1 - i]:
        palindrome = False
        break
if palindrome:
    print(word, "is a palindrome")
else:
    print(word, "is not a palindrome")
```
```python
r
```
```python
a
```
```python
c
```
```python
e
```
```python
c
```
```python
a
```
```python
r
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
6
```
```python
-7
```
```python
-6
```
```python
-5
```
```python
-4
```
```python
-3
```
```python
-2
```
```python
-1
```
```python
e
```
```python
0 ↔ -1
```
```python
1 ↔ -2
```
```python
2 ↔ -3
```
```python
How it works
Pairs: word[i] and word[-1 - i].
Half the word: The middle has no partner.
Mismatch: break stops the loop.
```

## Slide 10
Slicing: s[start:stop]
Creates a new string from start up to, but not including, stop.
`slice.py`
```python
s = "As easy "
print(s[1:5])   # s ea
print(s[0:2])   # As
```
```python
A
```
```python
s
```
```python
␣
```
```python
e
```
```python
a
```
```python
s
```
```python
y
```
```python
␣
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
6
```
```python
7
```
```python
5 - 1 = 4 characters
```
```python
s
```
```python
␣
```
```python
e
```
```python
a
```
A new string, four characters long.
```python
The half-open convention
As in range(): Stop is excluded.
Length: s[a:b] has b - a characters.
A copy: s is unchanged.
```
Basics
Indexing & slicing
Immutability
Unicode
Operators
Methods
Examples

## Slide 11
Omitting a bound
No start: from the beginning. No stop: to the end.
`bounds.py`
```python
s = "Python"
print(s[:3])    # Pyt
print(s[3:])    # hon
print(s[:])     # Python
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
k = 3
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
Nothing lost, nothing duplicated.
```python
Splitting at k
s[:k] + s[k:]: Equals s for any k.
s[-3:]: The last three characters.
```

## Slide 12
The step: s[start:stop:step]
The third number sets the stride.
`step.py`
```python
s = "abcdefgh"
print(s[0:8:2])   # aceg
print(s[::2])     # aceg
print(s[::-1])    # hgfedcba
```
```python
The step
Default: 1 - every character.
Step 2: Every second character.
Step -1: Walks backwards: s[::-1] reverses s.
```
```python
s[::2]
```
```python
a
```
```python
b
```
```python
c
```
```python
d
```
```python
e
```
```python
f
```
```python
g
```
```python
h
```
```python
a
```
```python
c
```
```python
e
```
```python
g
```
```python
s[::-1]
```
```python
a
```
```python
b
```
```python
c
```
```python
d
```
```python
e
```
```python
f
```
```python
g
```
```python
h
```
```python
h
```
```python
g
```
```python
f
```
```python
e
```
```python
d
```
```python
c
```
```python
b
```
```python
a
```

## Slide 13
Strings are immutable
What does this program print?
`immutable.py`
```python
s = "Python"
s[0] = "J"
print(s)
```
```python
terminal
```
```python
TypeError: 'str' object does not support item assignment
```
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
TypeError
```
```python
Why
Immutable: A string cannot be changed after it is created.
Like int, float, bool : None of them can be changed.
```
Basics
Indexing & slicing
Immutability
Unicode
Operators
Methods
Examples

## Slide 14
Every change produces a new string.
`fixed.py`
```python
s = "Python"
print(id(s))
s = "J" + s[1:]
print(id(s))
print(s)
```
```python
terminal
```
```python
9644448
140243618509296
Jython
```
```python
s
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
old
new
```python
What id shows
id(x) : Identifies the object x refers to.
Different id : A different object: a new string.
```
Strings are immutable

## Slide 15
How text is stored
Inside a computer everything is binary. So how is text stored?
what you see
what is stored
what the
hardware holds
```python
H
```
```python
i
```
```python
72
```
```python
105
```
```python
1001000
```
```python
1101001
```
```python
ש
```
```python
ל
```
```python
ו
```
```python
ם
```
```python
1513
```
```python
1500
```
```python
1493
```
```python
1501
```
```python
"שלום"
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
Text is numbers,
with a lookup
table on top.
Character sets
Character set: A table - every character gets a number.
ASCII (1963): 128 codes, English only.
Unicode: Every writing system. Starts with ASCII.
Python: Strings are Unicode. Hebrew works like English.
Basics
Indexing & slicing
Immutability
Unicode
Operators
Methods
Examples

## Slide 16
Crossing between the two: ord and chr
Two built-in functions, one in each direction.
`ord_chr.py`
```python
print(ord("A"))     # 65
print(ord("א"))     # 1488
print(chr(97))      # 'a'
print(chr(1488))    # 'א'

print(chr(ord("a") + 1))    # 'b'
print(ord("e") - ord("a"))  # 4
```
chr(ord(c)) is always c.
```python
a
```
```python
97
```
```python
ord →
```
```python
← chr
```
```python
a
```
```python
97
```
```python
0
```
```python
b
```
```python
98
```
```python
1
```
```python
c
```
```python
99
```
```python
2
```
```python
d
```
```python
100
```
```python
3
```
```python
e
```
```python
101
```
```python
4
```
```python
…
```
```python
…
```
```python
…
```
```python
x
```
```python
120
```
```python
23
```
```python
y
```
```python
121
```
```python
24
```
```python
z
```
```python
122
```
```python
25
```
code
position
Letters are numbered consecutively.
ord(ch) - ord("a") gives the position, 0 to 25.

## Slide 17
String operators we already know
Some are new today; some you have used since lecture 1-2.
```python
+
```
concatenation
```python
*
```
repetition
```python
[ ]
```
indexing
```python
[ : : ]
```
slicing
`operators.py`
```python
s = "Python"
print("ab" + "cd")      # abcd
print("ab" * 3)         # ababab
print(s[0], s[-1])      # P n
print(s[1:5])           # ytho
```
The new ones today: in, not in and the comparisons.
Basics
Indexing & slicing
Immutability
Unicode
Operators
Methods
Examples

## Slide 18
Membership: in & not in
```python
The in operator answers the question: Is one string inside another? 
Boolean operators: the result is True or False, as in lecture 1-2.
```
`membership.py`
```python
print("y" in "Python")       # True
print("z" in "Python")       # False
print("tho" in "Python")     # True
print("q" not in "Python")   # True
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
"tho" matches, so the result is True.
```python
in
```
```python
not in
```

## Slide 19
Class exercise
Task: Given a string, count how many vowels it contains.
```python
Two different types of in
in as a part of a for header: Part of the loop syntax.
in an a part of an expression: An operator that returns True or False.
```
`vowels.py`
```python
word = input("Enter a string:")
count = 0
for ch in word:        # loop syntax
    if ch in "aeiou":  # operator
         count += 1
```
```python
2
```
```python
1
```

## Slide 20
Comparing strings
Character by character, from the left. The result is True or False.
`compare.py`
```python
name = input("Name: ")
if name == "Omer":
    print("Hello!")
print("apple" < "banana")   # True
print("car" < "cart")      # True
```
```python
a
```
```python
p
```
```python
p
```
```python
l
```
```python
e
```
```python
b
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
n
```
```python
a
```
Decided at the first difference: a before b.
```python
c
```
```python
a
```
```python
r
```
```python
c
```
```python
a
```
```python
r
```
```python
t
```
A prefix comes first: "car" < "cart".
Comparison operators:
```python
==
```
equal
```python
!=
```
not equal
```python
<
```
less
```python
<=
```
less
or equal
```python
>
```
greater
```python
>=
```
greater
or equal

## Slide 21
Why capitals come first
Characters are compared by their codes.
`compare.py`
```python
print("Zebra" < "apple")    # True
```
```python
Z
```
```python
e
```
```python
b
```
```python
r
```
```python
a
```
```python
90
```
```python
101
```
```python
98
```
```python
114
```
```python
97
```
```python
a
```
```python
p
```
```python
p
```
```python
l
```
```python
e
```
```python
97
```
```python
112
```
```python
112
```
```python
108
```
```python
101
```
```python
90 < 97
```
```python
Upper and lower case
Codes: A–Z: 65–90. a–z: 97–122.
Result: Capitals sort before lowercase.
Not a dictionary: "Alphabetical" can surprise you.
```
Open question
How do we compare while ignoring case?

## Slide 22
The empty string
"" is a string of length 0.
`empty.py`
```python
name = input("Name: ")
if name:
    print("Hello,", name)
else:
    print("You didn't type anything.")
```
```python
len = 0
```
```python
H
```
```python
i
```
```python
len = 2
```
```python
When it appears
From input(): The user pressed Enter without typing.
In a condition: "" is False; any other string is True.
Short form: if name: means 
  if name != "":
```

## Slide 23
String methods
A method is an action called directly on a value.
`method.py`
```python
s = "Python"
print(s.upper())    # PYTHON
print(s.lower())    # python
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
.upper()
```
s.upper(): returns a copy of s in uppercase
```python
What is a method ?
Bound to objects: A method is a function tied directly to a specific data type (like strings)
Dot syntax (.): value.method(), asking the value to perform an action using its own data.
Parentheses: Required to call it.
Coming up: How methods differ from functions.
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
.lower()
```
s.lower(): returns a copy of s in lowercase
Basics
Indexing & slicing
Immutability
Unicode
Operators
Methods
Examples

## Slide 24
Common string methods
The first seven return a string or a number; the last four return a bool.
method
what it does
example
```python
.upper()
```
Returns a copy with every letter made a capital.
```python
"Hello".upper()   # "HELLO"
```
```python
.lower()
```
Returns a copy with every letter made small.
```python
"Hello".lower()   # "hello"
```
```python
.strip()
```
Returns a copy without the spaces at the two ends.
```python
"  hi  ".strip()  # "hi"
```
```python
.replace(old, new)
```
Returns a copy with every old swapped for new.
```python
"all".replace("l","L")  # "aLL"
```
```python
.count(sub)
```
Counts how many times sub appears (an int).
```python
"Hello".count("l")  # 2
```
```python
.find(sub)
```
Position where sub first appears, or -1 if absent.
```python
"Hello".find("z")  # -1
```
```python
.index(sub)
```
Same as find, but stops the program if sub is absent.
```python
"Hello".index("l")  # 2
```
```python
.islower()
```
True if every letter is small (and there is a letter).
```python
"abc".islower()  # True
```
```python
.isupper()
```
True if every letter is a capital.
```python
"ABC".isupper()  # True
```
```python
.isdigit()
```
True if every character is a digit 0-9.
```python
"2026".isdigit()  # True
```
```python
.isalpha()
```
True if every character is a letter.
```python
"Hi5".isalpha()  # False
```

## Slide 25
Functions vs. methods
Both take inputs and return a result. They differ in where they live.
```python
a
```
```python
b
```
```python
c
```
```python
len
```
```python
a
```
```python
b
```
```python
c
```
```python
.upper()
```
function
method
how it is called
```python
len(s)
```
```python
s.upper()
```
where it lives
on its own
inside a type
works on
often many types
only its own type
Function: the value goes inside. Method: before the dot.
```python
Rule of thumb (A tendency, not a law)
Many types: Usually a function: len, print, str.
One type: Usually a method: .upper() is only for strings.
```

## Slide 26
A method belongs to its data type
Python enforces where a method lives.
`errors.py`
```python
x = 5
x.upper()     # AttributeError
upper("hi")   # NameError
```
`arguments.py`
```python
s = "Hello"
s.count("l")          # 2
s.replace("l", "L")   # 'HeLLo'
```
The value before the dot is the first input.
```python
5
```
```python
int
```
!
```python
'int' object has no attribute 'upper'
```
An int has no such tool.
```python
upper
```
```python
name 'upper' is not defined
```
No such function.
```python
H
```
```python
e
```
```python
l
```
```python
l
```
```python
o
```
```python
.count()
```
```python
"l"
```
the value acted on
the argument

## Slide 27
The immutability trap
Predict the output
`trap.py`
```python
s = "  hello  "
s.strip()
print(s)
```
```python
Discarded
The new string is built and dropped.
s is unchanged.
```
```python
Kept
s = s.strip() rebinds s to the result.
```
Why?
As mentioned earlier, string is immutable, so it cannot be changed.
```python
# result discarded
# "  hello  "
```
```python
s = s.strip()
print(s)
```
```python
# result kept
# "hello"
```

## Slide 28
Counting a character, revisited
The same count, as a loop and as a method.
`count_loop.py`
```python
count = 0
for ch in word:
    if ch == target:
        count += 1
```
`count_method.py`
```python
count = word.count(target)
```
Both are correct.
```python
Loop or method?
.count(): How many times a substring appears.
The loop: Handles any condition you can write.
```
Basics
Indexing & slicing
Immutability
Unicode
Operators
Methods
Examples

## Slide 29
Removing the vowels
Task: Given a string, print it without any vowels. 
The idea: Using the accumulator pattern on strings.
`vowels.py`
```python
word = input("Enter a word: ")
result = ""
for ch in word:
    if ch not in "aeiou":
        result += ch
print(result)
```
example gives xmpl.
```python
e
```
```python
x
```
```python
a
```
```python
m
```
```python
p
```
```python
l
```
```python
e
```
```python
not in "aeiou"
```
```python
x
```
```python
m
```
```python
p
```
```python
l
```
Vowels are skipped; the rest are appended.
```python
The accumulator, for strings
1 · Initialize: result = ""
2 · Update: result += ch
3 · Use: print(result)
```

## Slide 30
continue: skipping one iteration
```python
break leaves the loop. continue leaves the current pass.
```
`vowels_if.py`
```python
for ch in word:
    if ch not in "aeiou":
        result += ch
```
`vowels_continue.py`
```python
for ch in word:
    if ch in "aeiou":
        continue
    result += ch
```
```python
for ch in word:
```
```python
if ch in "aeiou":
```
```python
    continue
```
```python
result += ch
```
the loop ends normally
```python
break
```
```python
continue
```
```python
break vs. continue
break: Exits the loop.
continue: Skips to the next item.
When to use it: Many cases to skip, or a long body. Otherwise a plain if is clearer.
```

## Slide 31
Palindrome recognition: revisited
`palindrome.py`
```python
word = input("Enter a word: ")
if word == word[::-1]:
    print(word, "is a palindrome")
else:
    print(word, "is not a palindrome")
```
```python
One line
word[::-1]: The word reversed.
==: Compares it with the original.
```
```python
r
```
```python
a
```
```python
c
```
```python
e
```
```python
c
```
```python
a
```
```python
r
```
```python
r
```
```python
a
```
```python
c
```
```python
e
```
```python
c
```
```python
a
```
```python
r
```
racecar: every pair matches.
```python
s
```
```python
e
```
```python
a
```
```python
s
```
```python
s
```
```python
a
```
```python
e
```
```python
s
```
seas: the second pair differs.
Task: Given a string, check if it is a palindrome (reads the same forwards and backwards).
The idea: reverse the input string and compare to the original.
word
Reversed word
word
Reversed word

## Slide 32
Class exercise: the Caesar cipher
Shift every lowercase letter a fixed number of places.
```python
terminal
```
```python
Message: hello, world
Shift: 3
khoor, zruog
```
Five questions, in pairs
1
Loop and build a new string?
2
```python
Is ch a lowercase letter?
```
3
Letter → position 0 to 25?
4
Shift, wrapping from z to a?
5
Position → letter?
```python
a
```
```python
d
```
```python
b
```
```python
e
```
```python
c
```
```python
f
```
```python
d
```
```python
g
```
```python
e
```
```python
h
```
```python
f
```
```python
i
```
```python
g
```
```python
j
```
```python
h
```
```python
k
```
```python
i
```
```python
l
```
```python
j
```
```python
m
```
```python
k
```
```python
n
```
```python
l
```
```python
o
```
```python
m
```
```python
p
```
```python
n
```
```python
q
```
```python
o
```
```python
r
```
```python
p
```
```python
s
```
```python
q
```
```python
t
```
```python
r
```
```python
u
```
```python
s
```
```python
v
```
```python
t
```
```python
w
```
```python
u
```
```python
x
```
```python
v
```
```python
y
```
```python
w
```
```python
z
```
```python
x
```
```python
a
```
```python
y
```
```python
b
```
```python
z
```
```python
c
```
outer: plain
inner: shift 3
```python
x
```
```python
23
```
```python
26
```
```python
0
```
```python
a
```
Test first: xyz with shift 3 must give abc.

## Slide 33
The Caesar cipher: one solution
`caesar.py`
```python
text = input("Message: ")
shift = int(input("Shift: "))
result = ""
for ch in text:
    if ch.islower():
        position = ord(ch) - ord("a")
        position = (position + shift) % 26
        result += chr(position + ord("a"))
    else:
        result += ch
print(result)
```
1
2
3
4
5
```python
Decryption
Shift -3: Run it on khoor, zruog: the original comes back.
Why: -3 % 26 is 23. % keeps the result in 0 to 25.
```
```python
If you finish early
Uppercase: A second branch, with ord("A").
ROT13: Shift 13, twice, gives the original. Why?
```

## Slide 34
Lecture summary
```python
Strings as sequences
A sequence
Numbered from 0. len(s) counts it.
Slicing and Indexing
s[i], s[start:stop:step]
Immutability
Every "change" builds a new string.
Unicode
Characters are numbers.
```
```python
Working with strings
Functions 
  len, id, ord, chr
Operators
[], [::], in, not in and comparison operators.
Methods
upper, lower, strip, find, replace, count…
```
Basics
Indexing & slicing
Immutability
Unicode
Operators
Methods
Examples

## Slide 35
Self practice
Write a program for each of these.
```python
Initials
Read a first and last name and print the initials. Use .find() to locate the space.
```
Palindrome, the hard way
Ignore case, spaces and punctuation, so "Rise to vote, sir" counts.
Count the doubles
Count how many times a letter is followed by the same letter.
The middle
Print the middle character of a word — or the middle two, if its length is even.

## Slide 36
PYTHON COURSE · WEEK 3 · LECTURE 2
Next: Lists and Tuples
Sequences that can be changed
