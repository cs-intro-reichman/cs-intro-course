# Recitation, week 3: Strings and approximation

## From `recitation 3.pptx`

## Slide 1
```python
s[::-1]
```
PYTHON COURSE · WEEK 3 · RECITATION 3
Recitation 3
for loops and strings

## Slide 2
Recitation overview
Warm-up
Text tools
Passwords
Monte Carlo
Ciphers
Extra
Wrap-up
1
Predictions
range, slicing, and the immutability trap
2
Text tools
a username, run-length encoding, a password check
3
Monte Carlo
darts and pi: throw, test, count
4
Ciphers
Vigenere, built on Caesar

## Slide 3
Warm-up: range
Warm-up
Text tools
Passwords
Monte Carlo
Ciphers
Extra
Wrap-up
WARM-UP · 2 MIN
Four loops with for. Write the four lines they print.
`warmup_range.py`
```python
for i in range(2, 11, 3):
    print(i, end=" ")
print()
for i in range(5, 0, -2):
    print(i, end=" ")
print()
for ch in "abc":
    print(ch * 2, end=" ")
print()
for i in range(3, 3):
    print("never")
print("done")
```
```python
The answers
2 5 8
5 3 1
aa bb cc
done (the empty range runs 0 times)
```

## Slide 4
Warm-up: slicing
Warm-up
Text tools
Passwords
Monte Carlo
Ciphers
Extra
Wrap-up
WARM-UP · 4 MIN
One string, eight lines. Write the output of each before we run it.
`warmup_slicing.py`
```python
s = "recitation"
print(s[0], s[-1])
print(s[2:5])
print(s[:3] + s[3:])
print(s[::-1])
print(s[::3])
print(len(s), s[len(s) - 1])
print("cit" in s, "tac" in s)
print(s[10])
```
```python
The answers
r n
cit
recitation
noitaticer
ritn
10 n
True False
IndexError - one past the end
```

## Slide 5
Warm-up: methods and the trap
WARM-UP · 4 MIN
Methods return a new string. Which line forgets that?
`warmup_methods.py`
```python
s = "  Hello, World  "
print(s.strip())
print(s.lower().count("l"))
print(s.find("World"))
print(s.replace("l", "L"))
t = s.strip()
t.upper()
print(t)
print("Zebra" < "apple", "a" < "b")
print(s.isalpha(), "abc".isalpha())
```
```python
The answers
Hello, World
3
9
  HeLLo, WorLd  
Hello, World  (the trap)
True True
False True
```

## Slide 6
Exercise 1: Username and e-mail
Warm-up
Text tools
Passwords
Monte Carlo
Ciphers
Extra
Wrap-up
EASY · 7 MIN ON YOUR OWN
Task: read a full name, 'First Last', and build the university username and e-mail.
The username is the first letter of the first name plus the whole last name, in lowercase
The e-mail is the username followed by @runi.ac.il; the initials are 'D.G.'
Extra spaces at the ends of the input must not matter
```python
terminal
```
```python
Full name:   David German 
Username: dgerman
E-mail: dgerman@runi.ac.il
Initials: D.G.
```
```python
Think about
.find(" ") locates the space; slices take the two halves
.strip() first, .lower() and .upper() where needed
```

## Slide 7
Exercise 1: one solution
`username.py`
```python
full = input("Full name: ").strip()

space = full.find(" ")
first = full[:space]
last = full[space + 1:]

username = (first[0] + last).lower()
print(f"Username: {username}")
print(f"E-mail: {username}@runi.ac.il")
print(f"Initials: {first[0]}.{last[0]}.")
```
```python
Find the seam, cut, assemble
strip() first: the input promise is kept before anything else looks at the text
The seam: find(" ") gives the position of the space; [:space] and [space + 1:] are the halves
Build, then lower: parentheses, so .lower() applies to the whole username
Initials: first[0] and last[0] are strings of length 1, joined with dots in an f-string
```

## Slide 8
Exercise 1: the run
`username.py`
```python
full = input("Full name: ").strip()

space = full.find(" ")
first = full[:space]
last = full[space + 1:]

username = (first[0] + last).lower()
print(f"Username: {username}")
print(f"E-mail: {username}@runi.ac.il")
print(f"Initials: {first[0]}.{last[0]}.")
```
`python username.py`
```python
Full name:   David German 
Username: dgerman
E-mail: dgerman@runi.ac.il
Initials: D.G.
```

## Slide 9
Exercise 2: Run-length encoding
Warm-up
Text tools
Passwords
Monte Carlo
Ciphers
Extra
Wrap-up
MID · 10 MIN ON YOUR OWN
Task: compress a string by replacing every run of equal characters with the character and its length.
```python
aaabbc becomes a3b2c1; xyz becomes x1y1z1; an empty string stays empty
Then decode: a3b2c1 becomes aaabbc again (counts are single digits)
Walk the positions, not the characters: a run ends where s[i] differs from s[i - 1]
```
```python
terminal
```
```python
Text: aaabbc
Encoded: a3b2c1

Code: a3b2c1
Decoded: aaabbc
```
```python
Think about
Encoding: a counter for the current run, and a result string that grows
Decoding: positions 0, 2, 4, ... hold characters; 1, 3, 5, ... hold counts: range(0, len(code), 2)
```

## Slide 10
The idea: a run ends at a change
aaabbc has three runs. Count a run until the next character differs, then write it down.
```python
1 · Start - the first character opens a run: current = s[0], count = 1
2 · Compare - for each position from 1: same as current? count it. Different? write current and count, start a new run
3 · Finish - after the loop, the last run is still open: write it too
4 · Edge - the empty string has no s[0]: handle it before the loop
```
In pseudocode
result = empty; if s is empty, stop
current = s[0], count = 1
for i from 1 to the end:
      same as current? count += 1
      else: write current and count,
                current = s[i], count = 1
write the last run

## Slide 11
Exercise 2: encoding
`rle_encode.py`
```python
s = input("Text: ")

result = ""
if len(s) > 0:
    current = s[0]
    count = 1
    for i in range(1, len(s)):
        if s[i] == current:
            count += 1
        else:
            result += current + str(count)
            current = s[i]
            count = 1
    result += current + str(count)
print(f"Encoded: {result}")
```
```python
Reading the loop
Positions from 1: s[i] is compared with the run that is open, not with s[i - 1] - same thing, one variable
Two accumulators: result grows a piece at a time; count restarts at 1 whenever a run closes
The last line of the if-block: the last run is written after the loop, always
str(count): a number cannot be joined to a string without it
```

## Slide 12
Exercise 2: the run
`rle_encode.py`
```python
s = input("Text: ")

result = ""
if len(s) > 0:
    current = s[0]
    count = 1
    for i in range(1, len(s)):
        if s[i] == current:
            count += 1
        else:
            result += current + str(count)
            current = s[i]
            count = 1
    result += current + str(count)
print(f"Encoded: {result}")
```
`python rle_encode.py`
```python
Text: aaabbc
Encoded: a3b2c1
```

## Slide 13
Exercise 2: decoding
`rle_decode.py`
```python
code = input("Code: ")

text = ""
for i in range(0, len(code), 2):
    ch = code[i]
    count = int(code[i + 1])
    text += ch * count
print(f"Decoded: {text}")
```
```python
Two positions at a time
range(0, len(code), 2): the step visits 0, 2, 4, ... - the character positions
The count is the next position: code[i + 1], turned into a number with int()
The * operator from week 1: "a" * 3 is aaa
A promise: counts have one digit; a4b12 would need the digits gathered until a letter appears
```
`python rle_decode.py`
```python
Code: a3b2c1
Decoded: aaabbc
```

## Slide 14
Exercise 3: Strong password
Warm-up
Text tools
Passwords
Monte Carlo
Ciphers
Extra
Wrap-up
MID · 10 MIN ON YOUR OWN
Task: read a password and check it against five rules. Print every rule it breaks, or 'Strong'.
```python
At least 8 characters; at least one digit; at least one uppercase and one lowercase letter; no spaces
One pass over the characters with isdigit(), isupper(), islower() and flags
Then: the password must not contain the username (one more line, with in)
```
```python
terminal
```
```python
Password: pw 7
too short
no uppercase letter
contains a space

Password: Reichman2026
Strong
```
Think about
A flag per rule: False at first, True once the loop sees the evidence
Decide after the loop: it discovers, the code after it acts

## Slide 15
Exercise 3: the loop (1 of 2)
```python
password.py (lines 1-12)
```
```python
password = input("Password: ")

has_digit = False
has_upper = False
has_lower = False
for ch in password:
    if ch.isdigit():
        has_digit = True
    if ch.isupper():
        has_upper = True
    if ch.islower():
        has_lower = True
```
```python
Discover
Three flags, one loop: each character can switch a flag on; nothing ever switches one off
Independent ifs, not elif: three separate questions about the same character
Flags start False before the loop - inside it they would be reset on every pass
Length and the space need no loop: len() and in answer them in one call each
```

## Slide 16
Exercise 3: the report (2 of 2)
```python
password.py (lines 14-28)
```
```python
problems = ""
if len(password) < 8:
    problems += "too short\n"
if not has_digit:
    problems += "no digit\n"
if not has_upper:
    problems += "no uppercase letter\n"
if not has_lower:
    problems += "no lowercase letter\n"
if " " in password:
    problems += "contains a space\n"

if problems == "":
    print("Strong")
else:
    print(problems, end="")
```
```python
Act
Five independent ifs: a password can break several rules at once, and every broken rule is reported
A string accumulator: problems collects one line per rule, each ending in \n
The empty string means strong: nothing was added, so nothing was wrong
print(problems, end=""): the newlines are already in the text
```

## Slide 17
Exercise 3: the run
```python
password.py (lines 14-28)
```
```python
problems = ""
if len(password) < 8:
    problems += "too short\n"
if not has_digit:
    problems += "no digit\n"
if not has_upper:
    problems += "no uppercase letter\n"
if not has_lower:
    problems += "no lowercase letter\n"
if " " in password:
    problems += "contains a space\n"

if problems == "":
    print("Strong")
else:
    print(problems, end="")
```
```python
python password.py (lines 14-28)
```
```python
Password: pw 7
too short
no uppercase letter
contains a space
```

## Slide 18
continue: when to reach for it
```python
The password loop had no continue. Where would one help?
A loop that skips - continue jumps to the next pass; the rest of the body is skipped
Clearer than if-else - several reasons to skip before a long body
Not clearer - a plain if around two lines does the same job
break is different - it leaves the loop for good; continue leaves one pass
```
Try it:
rewrite the vowel-removal loop from lecture 3-1 with continue, and decide which version reads better.

## Slide 19
Exercise 4: Darts and pi
Warm-up
Text tools
Passwords
Monte Carlo
Ciphers
Extra
Wrap-up
MID · 10 MIN ON YOUR OWN
Task: throw N random points into the square [-1, 1) x [-1, 1). Count how many land inside the unit circle.
The circle covers pi/4 of the square, so 4 * inside / N is an estimate of pi
Print the estimate for N = 100, 1000, 10000 and 100000 and compare with math.pi
Lecture 2-1's random point in the circle is one dart; now throw N of them
```python
terminal
```
```python
N = 100: 3.24
N = 1000: 3.152
N = 10000: 3.1384
N = 100000: 3.1416
math.pi: 3.1416
```
```python
Think about
A point (x, y) is inside the circle when x * x + y * y <= 1
for n in [100, 1000, 10000, 100000]: walks the four sizes
The accumulator: count the hits
```

## Slide 20
The idea: area as probability
A random point in the square lands inside the circle with probability pi / 4. Count how often it does.
```python
1 · Throw - x = 2 * random.random() - 1, the same for y
2 · Test - inside when x * x + y * y <= 1
3 · Count - hits += 1 for every point inside
4 · Estimate - hits / n is about pi / 4, so pi is about 4 * hits / n
5 · Repeat - more darts, better estimate; the error shrinks slowly
```
In pseudocode
for each size n:
      hits = 0
      repeat n times:
            throw a random point
            if it is inside: hits += 1
      print 4 * hits / n

## Slide 21
Exercise 4: one solution
`monte_carlo_pi.py`
```python
import random
import math

for n in [100, 1000, 10000, 100000]:
    hits = 0
    for i in range(n):
        x = 2 * random.random() - 1
        y = 2 * random.random() - 1
        if x * x + y * y <= 1:
            hits += 1
    estimate = 4 * hits / n
    print(f"N = {n}: {round(estimate, 4)}")
print(f"math.pi: {round(math.pi, 4)}")
```
```python
Reading the program
Two loops: the outer picks a size, the inner throws that many darts
Reset per size: hits = 0 sits inside the outer loop
A fresh point per dart: both random calls are inside the inner loop
The estimate uses /: a float, printed rounded to 4 digits
```

## Slide 22
Exercise 4: the run
`monte_carlo_pi.py`
```python
import random
import math

for n in [100, 1000, 10000, 100000]:
    hits = 0
    for i in range(n):
        x = 2 * random.random() - 1
        y = 2 * random.random() - 1
        if x * x + y * y <= 1:
            hits += 1
    estimate = 4 * hits / n
    print(f"N = {n}: {round(estimate, 4)}")
print(f"math.pi: {round(math.pi, 4)}")
```
```python
python monte_carlo_pi.py (one run)
```
```python
N = 100: 3.24
N = 1000: 3.152
N = 10000: 3.1384
N = 100000: 3.1416
math.pi: 3.1416
```

## Slide 23
Exercise 4, expansion: how often is it 7?
`sevens.py`
```python
import random

N = 10000
sevens = 0
for i in range(N):
    first = int(random.random() * 6) + 1
    second = int(random.random() * 6) + 1
    if first + second == 7:
        sevens += 1

print(f"Sevens: {sevens} of {N}")
print(f"Share: {round(sevens / N, 3)}")
print(f"Expected: {round(1 / 6, 3)}")
```
Recitation 1's question, answered
Two dice, ten thousand times: the same three-part shape - throw, test, count
Expected: 6 of the 36 combinations add up to 7, so about one roll in six
Your turn: count how often the two dice are equal, and how often the total is 2
```python
python sevens.py (one run)
```
```python
Sevens: 1687 of 10000
Share: 0.169
Expected: 0.167
```

## Slide 24
Exercise 5: The Vigenere cipher
Warm-up
Text tools
Passwords
Monte Carlo
Ciphers
Extra
Wrap-up
HIGH · 12 MIN ON YOUR OWN
Task: Caesar with a key word. Each letter is shifted by its own key letter, and the key repeats.
Key lemon: shifts 11, 4, 12, 14, 13 - the alphabet positions of l, e, m, o, n
attack at dawn with key lemon becomes lxfopv ef rnhr
Only lowercase letters are shifted and use a key letter; the rest is copied
```python
terminal
```
```python
Message: attack at dawn
Key: lemon
lxfopv ef rnhr
```
```python
Think about
Start from the lecture's caesar.py: the shift is now ord(key[j]) - ord("a")
j counts the key letter used so far; it wraps with % len(key) and advances only on letters
```

## Slide 25
Exercise 5: one solution
`vigenere.py`
```python
text = input("Message: ")
key = input("Key: ")

result = ""
j = 0
for ch in text:
    if ch.islower():
        shift = ord(key[j]) - ord("a")
        position = ord(ch) - ord("a")
        position = (position + shift) % 26
        result += chr(position + ord("a"))
        j = (j + 1) % len(key)
    else:
        result += ch
print(result)
```
```python
Caesar, with a moving shift
The shift: ord(key[j]) - ord("a") is the position of the key letter, 0 to 25
The same four lines as Caesar: position, add, wrap with % 26, back to a letter
j: advances only inside the if, so spaces do not consume key letters; % len(key) wraps it
Decryption: subtract the shift instead - (position - shift) % 26 - and the message comes back
```

## Slide 26
Exercise 5: the run
`vigenere.py`
```python
text = input("Message: ")
key = input("Key: ")

result = ""
j = 0
for ch in text:
    if ch.islower():
        shift = ord(key[j]) - ord("a")
        position = ord(ch) - ord("a")
        position = (position + shift) % 26
        result += chr(position + ord("a"))
        j = (j + 1) % len(key)
    else:
        result += ch
print(result)
```
`python vigenere.py`
```python
Message: attack at dawn
Key: lemon
lxfopv ef rnhr
```

## Slide 27
Exercise 5, expansion: both directions
`vigenere_both.py`
```python
text = input("Message: ")
key = input("Key: ")
mode = input("e to encrypt, d to decrypt: ")
sign = -1 if mode == "d" else 1
result = ""
j = 0
for ch in text:
    if ch.islower():
        shift = ord(key[j]) - ord("a")
        pos = ord(ch) - ord("a")
        pos = (pos + sign * shift) % 26
        result += chr(pos + ord("a"))
        j = (j + 1) % len(key)
    else:
        result += ch
print(result)
```
```python
One program, two directions
A mode and a sign: the conditional expression turns d into -1 and anything else into 1
Negative shifts are safe: % 26 always lands in 0 to 25, as with Caesar's shift -3
Round trip: decrypt lxfopv ef rnhr with lemon, and attack at dawn comes back
```

## Slide 28
Extra 1: Any base
Warm-up
Text tools
Passwords
Monte Carlo
Ciphers
Extra
Wrap-up
EXTRA
Task: generalise the two binary conversions of lecture 2-2 to any base from 2 to 10.
to_base: read a number n >= 0 and a base; print n written in that base (26 in base 3 is 222)
from_base: read a string of digits and a base; print its value (222 in base 3 is 26)
Handle n = 0, and stop with a message if a digit is too big for the base
```python
terminal
```
```python
n: 26
base: 3
222

digits: 222
base: 3
26
```
```python
Think about
In base 2 the loop used % 2 and // 2. What do they become?
Reading back: value = value * base + int(ch) for each character
```

## Slide 29
Extra 1: to any base
`to_base.py`
```python
n = int(input("n: "))
base = int(input("base: "))

digits = ""
if n == 0:
    digits = "0"
while n > 0:
    digits = str(n % base) + digits
    n = n // base
print(digits)
```
```python
Nothing depended on 2
% base peels off the last digit, // base drops it
Last digit first: each new digit is put in front of the ones found so far
Zero: the loop never runs, so the if before it supplies the single digit 0
Sanity check: base 10 must print the number unchanged
```

## Slide 30
Extra 1: the run
`to_base.py`
```python
n = int(input("n: "))
base = int(input("base: "))

digits = ""
if n == 0:
    digits = "0"
while n > 0:
    digits = str(n % base) + digits
    n = n // base
print(digits)
```
`python to_base.py`
```python
n: 26
base: 3
222
```

## Slide 31
Extra 1: from any base
`from_base.py`
```python
text = input("digits: ")
base = int(input("base: "))

value = 0
valid = True
for ch in text:
    digit = int(ch)
    if digit >= base:
        valid = False
        break
    value = value * base + digit
if valid:
    print(value)
else:
    print("not a valid number in that base")
```
```python
Horner, with a guard
Left to right: value * base + digit - everything so far is worth base times more, plus this digit
The guard: a digit that is too big for the base makes the number invalid
Flag and break: the loop discovers, the code after the loop acts (lecture 2-2)
A letter still crashes int(ch) - lecture 3-1's `isdigit()` is the guard to add
```

## Slide 32
Extra 1: the run
`from_base.py`
```python
text = input("digits: ")
base = int(input("base: "))

value = 0
valid = True
for ch in text:
    digit = int(ch)
    if digit >= base:
        valid = False
        break
    value = value * base + digit
if valid:
    print(value)
else:
    print("not a valid number in that base")
```
`python from_base.py`
```python
digits: 222
base: 3
26
```

## Slide 33
Extra 2: The clean palindrome
Warm-up
Text tools
Passwords
Monte Carlo
Ciphers
Extra
Wrap-up
EXTRA
Task: is a sentence a palindrome if case, spaces and punctuation are ignored?
```python
'Rise to vote, sir' and 'A man, a plan, a canal: Panama' both count
Build a cleaned copy with only the letters, in lowercase; then one comparison
Only letters: isalpha() decides, character by character
```
```python
terminal
```
```python
Sentence: Rise to vote, sir
Cleaned: risetovotesir
Palindrome: True
```
```python
Think about
The accumulator for strings: cleaned += ch
word == word[::-1] is the whole test (lecture 3-1)
```

## Slide 34
Extra 2: one solution
`clean_palindrome.py`
```python
sentence = input("Sentence: ")

cleaned = ""
for ch in sentence.lower():
    if ch.isalpha():
        cleaned += ch

print(f"Cleaned: {cleaned}")
print(f"Palindrome: {cleaned == cleaned[::-1]}")
```
```python
Filter, then test
Lowercase once: the loop walks sentence.lower(), a new string
The filter: isalpha() keeps letters only; digits and punctuation never reach cleaned
The test: cleaned == cleaned[::-1], evaluated inside the f-string
Try: 'Was it a car or a cat I saw?' and your own name
```
`python clean_palindrome.py`
```python
Sentence: Rise to vote, sir
Cleaned: risetovotesir
Palindrome: True
```

## Slide 35
Recitation summary
Warm-up
Text tools
Passwords
Monte Carlo
Ciphers
Extra
Wrap-up
What we practised
Start in, stop out
range(start, stop, step) - and a loop that runs zero times is not an error.
Throw, test, count
Two loops, a counter reset per size: the share of hits estimates a probability.
Find the seam, cut, assemble
find() gives a position; slices take the pieces; + and f-strings rebuild.
Discover, then act
Flags are set inside the loop and read after it; loops over positions when a character must meet its neighbour.
Tools we used
Loops
for, range(start, stop, step), for ch in s, nested for, end=""
Strings
len, s[i], s[a:b:c], in, ==, ord, chr, +=, * and the empty string
Methods
strip, lower, upper, find, replace, count, isalpha, isdigit, isupper, islower
Patterns
accumulator, flags, index loops with a step, continue, % and // peel digits off

## Slide 36
Self practice
AT HOME
Write a program for each of these.
Count the doubles
Count how many times a letter is immediately followed by the same letter: 'bookkeeper' has three.
The middle
Print the middle character of a word, or the middle two if its length is even. Test with lengths 1 to 4.
Title case by hand
Capitalise the first letter of every word in a sentence without using title() or split(): the character after a space is a word start.
The longest chain
Which start below 100 takes the most steps to reach 1 in the 3n + 1 game of recitation 2? A while inside a for, and a running maximum that remembers the start.

## Slide 37
PYTHON COURSE · WEEK 4 · RECITATION 4
Next: Approximation and functions
bisection, Newton, def, return, and modules

## From `clean_palindrome.py`

### `clean_palindrome.py`
```python
sentence = input("Sentence: ")

cleaned = ""
for ch in sentence.lower():
    if ch.isalpha():
        cleaned += ch

print(f"Cleaned: {cleaned}")
print(f"Palindrome: {cleaned == cleaned[::-1]}")
```

## From `cube_root.py`

### `cube_root.py`
```python
x = float(input("x: "))
epsilon = 0.000001
low = 0.0
high = 1.0 if x < 1 else x
guess = (low + high) / 2
steps = 0
while abs(guess ** 3 - x) >= epsilon:
    if guess ** 3 < x:
        low = guess
    else:
        high = guess
    guess = (low + high) / 2
    steps += 1
root = round(guess, 6)
print(f"cube root: {root} in {steps} steps")
```

## From `fixed_point.py`

### `fixed_point.py`
```python
import math
epsilon = 0.000001
low = 0.0
high = 1.0
guess = (low + high) / 2
steps = 0
while abs(math.cos(guess) - guess) >= epsilon:
    if math.cos(guess) - guess > 0:
        low = guess
    else:
        high = guess
    guess = (low + high) / 2
    steps += 1
answer = round(guess, 6)
print(f"cos(x) = x: {answer} in {steps} steps")
```

## From `from_base.py`

### `from_base.py`
```python
text = input("digits: ")
base = int(input("base: "))

value = 0
valid = True
for ch in text:
    digit = int(ch)
    if digit >= base:
        valid = False
        break
    value = value * base + digit
if valid:
    print(value)
else:
    print("not a valid number in that base")
```

## From `monte_carlo_pi.py`

### `monte_carlo_pi.py`
```python
import random
import math

for n in [100, 1000, 10000, 100000]:
    hits = 0
    for i in range(n):
        x = 2 * random.random() - 1
        y = 2 * random.random() - 1
        if x * x + y * y <= 1:
            hits += 1
    estimate = 4 * hits / n
    print(f"N = {n}: {round(estimate, 4)}")
print(f"math.pi: {round(math.pi, 4)}")
```

## From `password.py`

### `password.py`
```python
password = input("Password: ")

has_digit = False
has_upper = False
has_lower = False
for ch in password:
    if ch.isdigit():
        has_digit = True
    if ch.isupper():
        has_upper = True
    if ch.islower():
        has_lower = True

problems = ""
if len(password) < 8:
    problems += "too short\n"
if not has_digit:
    problems += "no digit\n"
if not has_upper:
    problems += "no uppercase letter\n"
if not has_lower:
    problems += "no lowercase letter\n"
if " " in password:
    problems += "contains a space\n"

if problems == "":
    print("Strong")
else:
    print(problems, end="")
```

## From `rle_decode.py`

### `rle_decode.py`
```python
code = input("Code: ")

text = ""
for i in range(0, len(code), 2):
    ch = code[i]
    count = int(code[i + 1])
    text += ch * count
print(f"Decoded: {text}")
```

## From `rle_encode.py`

### `rle_encode.py`
```python
s = input("Text: ")

result = ""
if len(s) > 0:
    current = s[0]
    count = 1
    for i in range(1, len(s)):
        if s[i] == current:
            count += 1
        else:
            result += current + str(count)
            current = s[i]
            count = 1
    result += current + str(count)
print(f"Encoded: {result}")
```

## From `sevens.py`

### `sevens.py`
```python
import random

N = 10000
sevens = 0
for i in range(N):
    first = int(random.random() * 6) + 1
    second = int(random.random() * 6) + 1
    if first + second == 7:
        sevens += 1

print(f"Sevens: {sevens} of {N}")
print(f"Share: {round(sevens / N, 3)}")
print(f"Expected: {round(1 / 6, 3)}")
```

## From `to_base.py`

### `to_base.py`
```python
n = int(input("n: "))
base = int(input("base: "))

digits = ""
if n == 0:
    digits = "0"
while n > 0:
    digits = str(n % base) + digits
    n = n // base
print(digits)
```

## From `username.py`

### `username.py`
```python
full = input("Full name: ").strip()

space = full.find(" ")
first = full[:space]
last = full[space + 1:]

username = (first[0] + last).lower()
print(f"Username: {username}")
print(f"E-mail: {username}@runi.ac.il")
print(f"Initials: {first[0]}.{last[0]}.")
```

## From `vigenere.py`

### `vigenere.py`
```python
text = input("Message: ")
key = input("Key: ")

result = ""
j = 0
for ch in text:
    if ch.islower():
        shift = ord(key[j]) - ord("a")
        position = ord(ch) - ord("a")
        position = (position + shift) % 26
        result += chr(position + ord("a"))
        j = (j + 1) % len(key)
    else:
        result += ch
print(result)
```

## From `vigenere_both.py`

### `vigenere_both.py`
```python
text = input("Message: ")
key = input("Key: ")
mode = input("e to encrypt, d to decrypt: ")
sign = -1 if mode == "d" else 1
result = ""
j = 0
for ch in text:
    if ch.islower():
        shift = ord(key[j]) - ord("a")
        pos = ord(ch) - ord("a")
        pos = (pos + sign * shift) % 26
        result += chr(pos + ord("a"))
        j = (j + 1) % len(key)
    else:
        result += ch
print(result)
```

## From `warmup_methods.py`

### `warmup_methods.py`
```python
s = "  Hello, World  "
print(s.strip())
print(s.lower().count("l"))
print(s.find("World"))
print(s.replace("l", "L"))
t = s.strip()
t.upper()
print(t)
print("Zebra" < "apple", "a" < "b")
print(s.isalpha(), "abc".isalpha())
```

## From `warmup_range.py`

### `warmup_range.py`
```python
for i in range(2, 11, 3):
    print(i, end=" ")
print()
for i in range(5, 0, -2):
    print(i, end=" ")
print()
for ch in "abc":
    print(ch * 2, end=" ")
print()
for i in range(3, 3):
    print("never")
print("done")
```

## From `warmup_slicing.py`

### `warmup_slicing.py`
```python
s = "recitation"
print(s[0], s[-1])
print(s[2:5])
print(s[:3] + s[3:])
print(s[::-1])
print(s[::3])
print(len(s), s[len(s) - 1])
print("cit" in s, "tac" in s)
print(s[10])
```
