# Week 3 code files

The code files shown in the week 3 lectures.

### `arguments.py`
```python
# lecture 3-1 — arguments.py
s = "Hello"
s.count("l")          # 2
s.replace("l", "L")   # 'HeLLo'

# Prints nothing: both lines are values the REPL would show. .count
# answers 2 and .replace answers 'HeLLo' — and s itself is unchanged.
```

### `bounds.py`
```python
# lecture 3-1 — bounds.py
s = "Python"
print(s[:3])    # Pyt
print(s[3:])    # hon
print(s[:])     # Python

# No start means from the beginning, no stop means to the end, and s[:]
# is the whole string.
```

### `caesar.py`
```python
# lecture 3-1 — caesar.py
text = input("Message: ")
shift = int(input("Shift: "))
result = ""
for ch in text:
    if ch.islower():
        position = ord(ch) - ord("a")
        position = (position + shift) % 26
        ch = chr(position + ord("a"))
    result += ch
print(result)

# $ python caesar.py
# Message: attack at dawn
# Shift: 3
# dwwdfn dw gdzq
```

### `compare.py`
```python
# lecture 3-1 — compare.py
name = input("Name: ")
if name == "Omer":
    print("Hello!")
print("apple" < "banana")   # True
print("car" < "cart")      # True

# $ python compare.py
# Name: Omer
# Hello!
# True
# True
```

### `compare_case.py`
```python
# lecture 3-1 — compare_case.py
print("Zebra" < "apple")    # True

# A capital letter has a smaller code than any small letter, so every word
# that starts with a capital sorts before every word that starts small.
```

### `count_loop.py`
```python
# lecture 3-1 — count_loop.py
word = "Mississippi"   # sample values, so the file runs on its own
target = "s"
count = 0
for ch in word:
    if ch == target:
        count += 1
print(count)

# Counting by hand, one character at a time.
```

### `count_method.py`
```python
# lecture 3-1 — count_method.py
word = "Mississippi"   # sample values, so the file runs on its own
target = "s"
count = word.count(target)
print(count)

# The same count, in one call.
```

### `count_vowels.py`
```python
# lecture 3-1 — count_vowels.py
word = input("Enter a string:")
count = 0
for ch in word:        # loop syntax
    if ch in "aeiou":  # operator
        count += 1
print(count)

# $ python count_vowels.py
# Enter a string:example
# 3
#
# NOTE: the card on the slide stops at count += 1 and never prints the answer,
# and that last line is indented nine spaces instead of eight. Both are fixed
# here; the card wants the same two corrections.
```

### `empty.py`
```python
# lecture 3-1 — empty.py
name = input("Name: ")
if name:
    print("Hello,", name)
else:
    print("You didn't type anything.")

# $ python empty.py
# Name:
# You didn't type anything.
```

### `errors.py`
```python
# lecture 3-1 — errors.py
x = 5
x.upper()     # AttributeError
upper("hi")   # NameError

# ON PURPOSE BROKEN — this is the error demo of the slide.
# x.upper() on an int raises AttributeError, and upper("hi") raises
# NameError: there is no plain function by that name.
```

### `fixed.py`
```python
# lecture 3-1 — fixed.py
s = "Python"
print(id(s))
s = "J" + s[1:]
print(id(s))
print(s)

# The two id() values differ: s = "J" + s[1:] built a new string and
# rebound the name to it. Nothing was changed in place.
```

### `immutable.py`
```python
# lecture 3-1 — immutable.py
s = "Python"
s[0] = "J"
print(s)

# ON PURPOSE BROKEN — this is the error demo of the slide.
# s[0] = "J" raises TypeError: 'str' object does not support item
# assignment. A string cannot be changed in place.
```

### `index.py`
```python
# lecture 3-1 — index.py
s = "Python"
print(s[0])    # P
print(s[5])    # n

# s[i] is the character at position i. The valid indices are 0 to len(s) - 1.
```

### `len.py`
```python
# lecture 3-1 — len.py
s = "As easy "    # the string on this slide, so the file runs on its own
print(len(s))      # 8
print(len("Hi"))   # 2
print(len(""))     # 0

# len() counts characters, not words, and the empty string has length 0.
```

### `letters.py`
```python
# lecture 3-1 — letters.py
for ch in "binary":
    print(ch)

# for ch in s visits the characters in order, without any index.
```

### `membership.py`
```python
# lecture 3-1 — membership.py
print("y" in "Python")       # True
print("z" in "Python")       # False
print("tho" in "Python")     # True
print("q" not in "Python")   # True

# in answers True or False, and it matches a piece as well as one
# character.
```

### `method.py`
```python
# lecture 3-1 — method.py
s = "Python"
print(s.upper())    # PYTHON
print(s.lower())    # python

# A method is called on the value itself: s.upper(), not upper(s).
```

### `negative.py`
```python
# lecture 3-1 — negative.py
s = "Python"
print(s[-1])   # n
print(s[-2])   # o
print(s[-6])   # P

# A negative index counts from the end: -1 is the last character.
```

### `operators.py`
```python
# lecture 3-1 — operators.py
s = "Python"
print("ab" + "cd")      # abcd
print("ab" * 3)         # ababab
print(s[0], s[-1])      # P n
print(s[1:5])           # ytho

# + joins, * repeats, [i] picks one character and [i:j] picks a piece.
```

### `ord_chr.py`
```python
# lecture 3-1 — ord_chr.py
print(ord("A"))     # 65
print(ord("א"))     # 1488
print(chr(97))      # 'a'
print(chr(1488))    # 'א'

print(chr(ord("a") + 1))    # 'b'
print(ord("e") - ord("a"))  # 4

# ord() gives a character its code and chr() goes back.
```

### `palindrome.py`
```python
# lecture 3-1 — palindrome.py
word = input("Enter a word: ")
if word == word[::-1]:
    print(word, "is a palindrome")
else:
    print(word, "is not a palindrome")

# $ python palindrome.py
# Enter a word: racecar
# racecar is a palindrome
```

### `palindrome_idx.py`
```python
# lecture 3-1 — palindrome_idx.py
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

# $ python palindrome_idx.py
# Enter a word: racecar
# racecar is a palindrome
```

### `print.py`
```python
# lecture 3-1 — print.py
print("I don't like\nthe word \"no\"")

# \n starts a new line and \" puts a double quote inside a double-quoted
# string. The file prints two lines.
```

### `quotes.py`
```python
# lecture 3-1 — quotes.py
a = "double quotes"
b = 'single quotes'
c = "it's fine inside double quotes"
d = 'and "quotes" inside single ones'

# Both quote marks make the same string. Use the other kind when the
# text itself contains one, and no escape is needed.
```

### `remove_vowels.py`
```python
# lecture 3-1 — remove_vowels.py
word = input("Enter a word: ")
result = ""
for ch in word:
    if ch not in "aeiou":
        result += ch
print(result)

# $ python remove_vowels.py
# Enter a word: example
# xmpl
```

### `slice.py`
```python
# lecture 3-1 — slice.py
s = "As easy "
print(s[1:5])   # s ea
print(s[0:2])   # As

# s[start:stop] stops one before stop, as range() does.
```

### `sqrt_bisection.py`
```python
# lecture 3-2 — sqrt_bisection.py
# Square root of x by bisection (x >= 1)
x = 16
epsilon = 0.01
low = 1.0
high = x
g = (low + high) / 2
steps = 0
while abs(g * g - x) >= epsilon:
    if g * g < x:
        low = g
    else:
        high = g
    g = (low + high) / 2
    steps = steps + 1
print(f"{round(g, 4)} in {steps} steps")

# Halves the interval each pass. Far fewer steps than the walk.
```

### `sqrt_newton.py`
```python
# lecture 3-2 — sqrt_newton.py
# Square root of x by Newton-Raphson
x = 16
epsilon = 0.01
g = x / 2
steps = 0
while abs(g * g - x) > epsilon:
    g = g - (g * g - x) / (2 * g)
    steps = steps + 1
    print(f"step {steps}: {g}")
print(f"{round(g, 4)} in {steps} steps")

# Follows the tangent. Fewer steps again.
```

### `sqrt_sequential.py`
```python
# lecture 3-2 — sqrt_sequential.py
# Square root of x by sequential search
x = 16
epsilon = 0.01
increment = 0.0001
g = 1.0
steps = 0
while abs(g * g - x) >= epsilon:
    g = g + increment
    steps = steps + 1
print(f"{round(g, 4)} in {steps} steps")

# Walks up from 1.0 in steps of 0.0001 until g * g is within epsilon
# of x.
```

### `sqrt_sequential_fixed.py`
```python
# lecture 3-2 — sqrt_sequential_fixed.py
# Square root of x by sequential search
x = 16
epsilon = 0.01
increment = 0.0001
g = 1.0
steps = 0
while abs(g * g - x) >= epsilon and g <= x:
    g = g + increment
    steps = steps + 1
if g > x:
    print("Use a smaller increment")
else:
    print(f"{round(g, 4)} in {steps} steps")

# The same search, with a guard: without g <= x the loop runs past x
# for ever when the increment is too coarse.
```

### `step.py`
```python
# lecture 3-1 — step.py
s = "abcdefgh"
print(s[0:8:2])   # aceg
print(s[::2])     # aceg
print(s[::-1])    # hgfedcba

# The third number is the stride; -1 walks the string backwards.
```

### `trap.py`
```python
# lecture 3-1 — trap.py
s = "  hello  "
s.strip()
print(s)

# s.strip() returns a new string and the program throws it away, so s is
# still "  hello  ". The fix is s = s.strip().
```

### `vowels_break.py`
```python
# lecture 3-1 — vowels_break.py
word = "programming"   # sample values, so the file runs on its own
result = ""
for ch in word:
    if ch in "aeiou":
        break
    result += ch
print(result)

# Everything before the first vowel, and nothing at all when the word opens on
# one: programming gives pr, python gives pyth, example gives the empty string.
```

### `vowels_continue.py`
```python
# lecture 3-1 — vowels_continue.py
word = "example"   # sample values, so the file runs on its own
result = ""
for ch in word:
    if ch in "aeiou":
        continue
    result += ch
print(result)

# The same result with continue: the vowel ends its pass early and
# nothing is appended.
```

### `vowels_if.py`
```python
# lecture 3-1 — vowels_if.py
word = "example"   # sample values, so the file runs on its own
result = ""
for ch in word:
    if ch not in "aeiou":
        result += ch
print(result)

# The accumulator with an if: a character is appended when it is not a
# vowel.
```
