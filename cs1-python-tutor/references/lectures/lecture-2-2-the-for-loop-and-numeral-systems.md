# Lecture 2-2: The for loop and numeral systems (week 2)

## Slide 1
PYTHON COURSE · WEEK 2 · LECTURE 2
Loops and Numeral Systems
The for loop, loop patterns, and numbers in binary

## Slide 2
Lecture overview
The for loop
Loop patterns
Numeral systems
Binary
1
The for loop
one pass per item
2
Loop patterns
accumulate, carry forward, nest
3
Numeral systems
positional notation, and why binary
4
Binary
converting both ways

## Slide 3
Recapping while: The cost of manual counting
Explicitly state management forces the programmer to handle loop control manually.
```python
i = 0
while i < 5:
    print(i)
    i += 1
```
Manual loop control is where all four classic loop bugs live. Python’s for loop automates all three parts for you.
`count_up_while.py`
```python
Three essential moving parts
Initialization: Set the loop variable (i) before entering the loop.
Condition: Evaluated prior to every iteration. 
Update: Modify the loop variable (i) inside the loop-body to ensure termination.
```
1
2
3

## Slide 4
The core idea of the for loop
The for loop
Loop patterns
Numeral systems
Binary
`count_up_while.py`
```python
i = 0
while i < 5:
    print(i)
    i += 1
```
`count_up_for.py`
```python
for i in [0,1,2,3,4]:
    print(i)
```
```python
Same behavior, zero manual control
The for loop moves through the sequence [0,1,2,3,4] item by item.
On each iteration, Python automatically rebinds i to the next value.
No explicit initialization, condition, or modification of i are needed in code.
```
Replacing explicit loop mechanics with automated sequence iteration.

## Slide 5
The for loop
```python
syntax
```
```python
for variable in sequence:
    statement_1
    statement_2
```
```python
loop block (body) 
# executed once per item
```
```python
for
```
```python
items left ?
```
```python
True
```
```python
variable = next item
```
```python
loop block
```
```python
False
```
next statement
Semantics
1.  Assign the next item in the sequence to the loop variable.
2.  Execute the loop block.
3.  Return to step 1. When no items are left, exit the loop.
Syntax

## Slide 6
Example: a list of names
The loop takes the items one at a time, in order.
```python
"Messi"
```
```python
"Ronaldo"
```
```python
"Neymar"
```
the sequence, before the loop starts
```python
The variable name
On each pass name is bound to the next item: "Messi", then "Ronaldo", then "Neymar".
```
```python
output
```
```python
Hello, Messi
Hello, Ronaldo
Hello, Neymar
```
`names.py`
```python
for name in ["Messi", "Ronaldo", "Neymar"]:
    print("Hello,", name)
```
The square brackets make a list. Lists are next week; today we only need that a list is something a loop can walk through.

## Slide 7
Generating a sequence with range()
Iterating over [0, 1, 2, 3, 4] is easy. But what if we need 100?
`lines.py`
```python
for count in range(100):
    print("I will not argue ...")
```
```python
output
```
```python
I will not argue ...
I will not argue ...
...
```
```python
Why do we need range() ?
No manual enumeration: Writing explicit lists works for a few elements but becomes impossible for large sequences. 
On-demand generation: range(100) generates 100 values dynamically in memory as needed. 
Dynamic Bounds: Allows iterating over variable ranges like range(n) where n is known only at runtime. 
```

## Slide 8
The range() function
Syntax
```python
the three forms
```
```python
range(stop)
range(start, stop)
range(start, stop, step)
```
The three arguments
start - First value in sequence (default: 0)
stop – Bound where sequence terminates (required).
step – Increment between successive values (default: 1).
```python
How the sequence is built
Inclusive start, exclusive stop: Always includes the start value and excludes the stop value
Guaranteed Count: range(n) always produces exactly n numbers (from 0 to n-1).
Counting down: Use a negative step to count backwards.
Empty Ranges: If bounds cannot be met (like range(5,5)), the loop simply never runs.
```

## Slide 9
Visualizing range() execution
Consistent evaluation across common parameter variations
call
produces
```python
range(5)
```
```python
0 1 2 3 4
```
```python
range(2, 6)
```
```python
2 3 4 5
```
```python
range(0, 10, 2)
```
```python
0 2 4 6 8
```
```python
range(5, 0, -1)
```
```python
5 4 3 2 1
```
```python
Default argument resolution
range(5) is equivalent to range(0, 5, 1) with the defaults filled in.
```

## Slide 10
range() supplies the three moving parts
Mapping arguments directly to the loop control mechanics we wrote by hand.
```python
range
```
```python
range(0, 100, 1)
```
```python
start
```
initialization
```python
i = 0
```
```python
stop
```
condition
```python
i < 100
```
```python
step
```
update
```python
i += 1
```
The control tasks didn't disappear - they moved from explicit code into range() arguments.
```python
What you choose vs.      What Python manages
Your decision: Define which values to iterate over - a logical decision based on your problem.
Python's job: Advancing the counter, testing the boundary, and stopping are handled automatically by range() and for.
```

## Slide 11
Assigning to the loop variable
Predict the output:
`no_effect.py`
```python
for i in range(5):
    print(i, end=" ")
    i = 10
    print(i)
```
```python
output
```
```python
0 10
1 10
2 10
3 10
4 10
```
```python
Why ?
range(5) is evaluated once before the loop starts.
At the beginning of each iteration, the for loop rebinds i to the next item in the sequence, completely overwriting any assignment made inside the loop body.
```

## Slide 12
The accumulator pattern
The for loop
Loop patterns
Numeral systems
Binary
Task: sum all the integers from 1 to n.
`sum.py`
```python
total = 0
```
```python
for i in range(1, n + 1):
```
```python
total += i
```
```python
print(total)
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
n = 4 gives 1 + 2 + 3 + 4 = 10.
This pattern is behind sum, average, minimum, maximum and search.
1 · Initialize
Set up the accumulator before the loop, with a starting value.
2 · Update
Change its value inside the loop, once per item.
3 · Use
Read or print it after the loop has finished.

## Slide 13
Tracing the sum accumulator
n = 4. One row per iteration.
pass
i
total += i
total
```python
1
```
```python
1
```
```python
0 + 1
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
1 + 2
```
```python
3
```
```python
3
```
```python
3
```
```python
3 + 3
```
```python
6
```
```python
4
```
```python
4
```
```python
6 + 4
```
```python
10
```
`sum.py`
```python
total = 0
for i in range(1, 5):
    total += i
print(total)   # 10
```
```python
What makes total an Accumulator
total holds the sum of all the numbers seen so far. 
Once the loop finishes, it holds the total sum of all numbers.
```
```python
-
```
```python
-
```
```python
-
```
```python
0
```

## Slide 14
Example: n factorial
Task: compute n! = 1 × 2 × … × n.
`factorial.py`
```python
factorial = 1
```
```python
for i in range(1, n + 1):
```
```python
factorial *= i
```
```python
print(factorial)
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
n = 5 gives 120.
range(1, n + 1), not range(n).
Starting at 0 would zero the product.
1 · Initialize
factorial = 1, not 0. Zero would annihilate every multiplication.
2 · Update
factorial *= i. The result is a product, so each item multiplies rather than adds.
3 · Use
print(factorial) after the loop. Inside it, you would print partial products.

## Slide 15
Example: The harmonic sum
Task: compute 1 + 1/2 + 1/3 + … + 1/n.
`harmonic.py`
```python
total = 0.0
```
```python
for i in range(1, n + 1):
```
```python
total += 1 / i
```
```python
print(total)
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
n = 4 gives 2.083333333333333.
In Python 3, 1 / i is already a float.
The .0 only states the intent.
1 · Initialize
total = 0.0, not 0. The result is a float, and the first line says so.
2 · Update
total += 1 / i. Addition again, but what is added is the reciprocal of the item.
3 · Use
print(total) after the loop, exactly as before. Only the operation changed.

## Slide 16
The same three parts, three problems
One pattern. Only the starting value and the operation change.
problem
initialize
update
result
```python
sum 1..n
```
```python
total = 0
```
```python
total += i
```
```python
total
```
```python
n factorial
```
```python
factorial = 1
```
```python
factorial *= i
```
```python
factorial
```
```python
harmonic sum
```
```python
total = 0.0
```
```python
total += 1 / i
```
```python
total
```
```python
total = 0
```
```python
0
```
Adding 0 changes nothing.
```python
factorial = 1
```
```python
1
```
Multiplying by 1 changes nothing.
```python
total = 0.0
```
```python
0.0
```
A float zero, for a float result.
The starting value
The value that leaves the accumulator unchanged.
Also the right answer for an empty range: sum 0, product 1.

## Slide 17
Two correct programs, different costs
Both print the powers of two. One does far more work.
`powers_a.py`
```python
for i in range(n + 1):
    print(i, 2 ** i)
```
`powers_b.py`
Version A - Recomputes 2i independently on every iteration.
```python
Version B - The accumulator pattern in action:
1 · Initialize: v = 1
2 · Update: v *= 2
3 · Use: print(i, v) inside the loop.
```
```python
2**0
```
```python
2**1
```
```python
2**2
```
```python
2**3
```
```python
2**4
```
Nothing carries over — the previous value is discarded.
```python
1
```
```python
2
```
```python
4
```
```python
8
```
```python
16
```
```python
× 2
```
```python
× 2
```
```python
× 2
```
```python
× 2
```
One multiplication per iteration, reusing previous values.
```python
v = 1
for i in range(n + 1):
    print(i, v)
    v *= 2
```
`powers_b.py`

## Slide 18
Carrying a value forward
Reusing previous results vs. computing from scratch
```python
The core habit 
Recognize repeated work. Reusing intermediate results is a fundamental optimization technique.
Operations have different costs
Exponentiation (**) performs significantly more low-level work than a single multiplication (*=).
Flexible pattern use
The accumulator pattern isn’t just for calculating a single sum at the end – it’s equally useful for managing running state during iteration.
```

## Slide 19
Iterating over a string
for loops process sequences – and a string is simply a sequence of characters.
`letters.py`
```python
for ch in "binary":
    print(ch)
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
The same diagram as before, carrying characters instead of names.
```python
Direct iteration vs. Indexing
Automatic rebinding: On each iteration, Python automatically rebinds ch to the next character in sequence.
Focus for today: We iterate directly over the characters themselves.
Coming next week: Accessing characters by index, slicing and string methods.
```

## Slide 20
Example: counting one letter
Task: Given a word and a letter, count the number of times the letter appears in the word.
`count_letter.py`
```python
word = input("Enter a word: ")
target = input("Enter a letter to count: ")

count = 0
for ch in word:
    if ch == target:
        count += 1

print(target, "appears", count, "times in", word)
```
```python
output
```
```python
Enter a word: banana
Enter a letter to count: a
a appears 3 times in banana
```
Another variation of the accumulator pattern
Initialize before, update inside, use after.
The sequence is a string now, and the update is conditional.

## Slide 21
Nested for loops
The inner loop completes on every pass of the outer one.
`times_table.py`
```python
n = int(input("n: "))
for i in range(1, n + 1):
    for j in range(1, n + 1):
        print(i * j, end="\t")
    print()
```
```python
n =
```
```python
3
```
```python
i =
```
```python
j =
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
output
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
```python
4
```
```python
6
```
```python
3
```
```python
6
```
```python
9
```
Three things to point at
The inner loop completes on every pass of the outer loop.
end="\t" suppresses the newline and separates cells with a tab.
The bare print() after the inner loop ends the row.

## Slide 22
In a for loop, inner counter resets itself
Eliminating the most common bug in nested while loops
`nested_while.py`
```python
i = 0
while i < 3:
    j = 0   # forget this
    while j < 3:
        print("*", end="")
        j += 1
    print()
    i += 1
```
Forgetting j = 0 caused inner loop to run only once.
`nested_for.py`
```python
for i in range(3):
    for j in range(3):
        print("*", end="")
    print()
```
There is no j = 0 to forget – Python manages the reset..
```python
How Python handles inner loops
range(3) is evaluated afresh every time the inner loop starts.
j is automatically reassigned to 0 at the start of every outer iteration.
```

## Slide 23
The star patterns, written with for
Last lecture's self-practice, re-solved.
`left.py`
```python
for row in range(1, n + 1):
    for star in range(row):
        print("*", end="")
    print()
```
The line that says it
range(row) means "this row has row stars". The inner loop's range depends on the outer loop's variable, and that dependency is the whole pattern.
row
stars printed
```python
1
```
```python
    *
```
```python
2
```
```python
    **
```
```python
3
```
```python
    ***
```
```python
4
```
```python
    ****
```
Worth setting again
Go back to your own while solutions from last week and rewrite them with for. Comparing two of your own versions of the same program is one of the most useful exercises available this early.

## Slide 24
Counting in Unary: A non-positional numeral system
The for loop
Loop patterns
Numeral systems
Binary
27 goats - one mark per goat.
```python
|||||||||||||||||||||||||||
```
27, in tally marks
A non-positional system
Value = Count: Total value is simply the number of marks.
Position independent: A mark means 1 regardless of where it sits.
Simple & Intuitive: Works perfectly for small, manageable quantities.

## Slide 25
```python
|||||||||||||||||||||||||||||||||||||||
|||||||||||||||||||||||||||||||||||||||
|||||||||||||||||||||||||||||||||||||||
|||||||||||||||||||||||||||||||||||||||
|||||||||||||||||||||||||||||||||||||||
||||||||||||| ...
```
7,053, in tally marks (the first 208)
The limits of Unary
Hard to read & write: Drawing or counting thousands of individual marks is slow and leads to mistakes.
Takes up massive space: Representing large numbers requires an overwhelming number of marks.
Counting in Unary: What happens when quantities grow ?
7,053 goats - one mark per goat.

## Slide 26
Positional numeral system
How base 10 (decimal system) handles 7,053 goats
```python
103
```
```python
7
```
```python
7×103
```
```python
102
```
```python
0
```
```python
0×102
```
```python
101
```
```python
5
```
```python
5×101
```
```python
100
```
```python
3
```
```python
3×100
```
```python
= 7053
```
Base b notation rules (b  2)
The digits: Uses b distinct digits (0 to b-1).
Place values: Position i (from right) determines the value by multiplying the digit by bi.
Decimal system (b=10): Uses digits 0 to 9 and powers of 10.
Why base 10? Driven by human anatomy (10 fingers), not a mathematical requirement.
```python
+
```
```python
+
```
```python
+
```

## Slide 27
The same scheme in base 2 (Binary)
Two digits {0,1}, and positional values that double (powers of 2).
base 10
```python
103
```
```python
7
```
```python
7×103
```
```python
102
```
```python
0
```
```python
0×102
```
```python
101
```
```python
5
```
```python
5×101
```
```python
100
```
```python
3
```
```python
3×100
```
```python
= 7053
```
base 2
```python
23
```
```python
1
```
```python
1×23
```
```python
22
```
```python
1
```
```python
1×22
```
```python
21
```
```python
0
```
```python
0×21
```
```python
20
```
```python
1
```
```python
1×20
```
```python
= 13
```
```python
+
```
```python
+
```
```python
+
```
```python
+
```
```python
+
```
```python
+
```

## Slide 28
Counting in Binary
Zero to fifteen, in both notations.
decimal
binary
```python
0
```
```python
0000
```
```python
1
```
```python
0001
```
```python
2
```
```python
0010
```
```python
3
```
```python
0011
```
```python
4
```
```python
0100
```
```python
5
```
```python
0101
```
```python
6
```
```python
0110
```
```python
7
```
```python
0111
```
decimal
binary
```python
8
```
```python
1000
```
```python
9
```
```python
1001
```
```python
10
```
```python
1010
```
```python
11
```
```python
1011
```
```python
12
```
```python
1100
```
```python
13
```
```python
1101
```
```python
14
```
```python
1110
```
```python
15
```
```python
1111
```
Column patterns & capacity
How bits flip: From right to left, bits alternate every 1, 2, 4 and 8 rows (like an odometer).
Range formula: n bits cover 2n unique values (4 bits cover 24 = 16 values, 0 to 15)

## Slide 29
Why computers use Binary
Minimal
A positional system needs at least two digits. Binary uses exactly two, making it the simplest possible positional system.
Physical
A wire is carrying current or it is not (ON/OFF). That is the only distinction the hardware has to make reliably.
The consequence
People prefer decimal and machines are built on binary, so computers constantly translate between the two representation formats.
Decimal to Binary when inputting a number from the user 
Binary to Decimal when outputting it to the user

## Slide 30
Converting Decimal to Binary
The for loop
Loop patterns
Numeral systems
Binary
Reusing our base-10 digit extraction loop, replacing 10 with 2
`to_binary.py`
```python
x = int(input("n (>= 0): "))
s = ""
while x > 0:
    s = str(x % 2) + s
    x = x // 2
print(s)
```
% 2 gives the next binary digit, // 2 removes it.
```python
Digit extraction in base 2
Extracting digits: n % 2 extracts the last (rightmost) digit.
Removing digits: n // 2 strips the last digit, shrinking n toward 0 to end the loop.
```
```python
Why build a string?
Easier manipulation: string concatenation (+) simply joins digits, avoiding complex positional arithmetic.
Text vs. Number: Storing as a string prevents Python from interpreting 1010 as the decimal number “one thousand and ten”.
```

## Slide 31
Tracing the conversion
x = 26.
pass
x
x % 2
s
x // 2
```python
1
```
```python
26
```
```python
0
```
```python
"0"
```
```python
13
```
```python
2
```
```python
13
```
```python
1
```
```python
"10"
```
```python
6
```
```python
3
```
```python
6
```
```python
0
```
```python
"010"
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
1
```
```python
"1010"
```
```python
1
```
```python
5
```
```python
1
```
```python
1
```
```python
"11010"
```
```python
0
```
```python
16
```
```python
1
```
```python
8
```
```python
1
```
```python
4
```
```python
0
```
```python
2
```
```python
1
```
```python
1
```
```python
0
```
the grid, filled in from the right
```python
26 = 11010
```
the s column, read off the last row
Why the digits are prepended
The loop finds the last digit first: 0, then 1, then 0, then 1, then 1.
Written in that order they would come out backwards, so each new digit joins the front of the string.
26 = 11010.

## Slide 32
What does this print for x = 0?
Read it before you run it.
`to_binary.py`
```python
x = int(input("n (>= 0): "))
s = ""
while x > 0:
    s = str(x % 2) + s
    x = x // 2
print(s)
```
And what does it print for a negative number?

## Slide 33
The zero case
The condition is false immediately, so nothing is printed.
`fixed.py`
```python
x = int(input("n (>= 0): "))
s = ""
if x == 0:
    s = "0"
else:
    while x > 0:
        s = str(x % 2) + s
        x = x // 2
print(s)
```
```python
       How to spot it
The loop body never runs, s keeps its empty value, and the program prints a blank line. The right answer is 0.
Nothing crashes — the output is simply missing.
```
      How to fix it
Handle zero before the loop, and let the loop handle everything else.
A negative number prints nothing too, which is correct only because the prompt asks for a non-negative integer.

## Slide 34
Converting Binary to Decimal
The other direction, and the one that needs a string.
`to_decimal.py`
```python
s = input("Binary number: ")
value = 0
for ch in s:
    value = value * 2 + int(ch)
print(value)
```
1011 gives 11.
```python
8
```
```python
4
```
```python
2
```
```python
1
```
```python
1
```
```python
0
```
```python
1
```
```python
1
```
```python
1
```
```python
2
```
```python
5
```
```python
11
```
value, doubling at each step
Why it works
Each new digit means everything so far is worth twice as much, plus this digit.
The method has a name: Horner's method, and it comes back in later courses.

## Slide 35
When the input is not binary
Checking input validity
`to_decimal_safe.py`
```python
valid = True
for ch in s:
    if ch != "0" and ch != "1":
        valid = False
        break
    value = value * 2 + int(ch)
if valid:
    print(value)
else:
    print("Not a binary number.")
```
What went wrong without it
"hello" raised ValueError on int(ch).
"1021" was accepted in silence and produced nonsense.
The valid flag
A bool that records something learned inside the loop and is read after it.
The loop’s job is to discover. The code after it acts.

## Slide 36
The built-in conversions
`to_binary.py`
```python
x = 26
s = ""
while x > 0:
    s = str(x % 2) + s
    x = x // 2
print(s)
```
`builtin.py`
```python
x = 26
print(bin(x))    # 0b11010
```
`builtin.py`
```python
s = "11010"
print(int(s, 2)) # 26
```
`to_decimal.py`
```python
s = "11010"
value = 0
for ch in s:
    value = value * 2 + int(ch)
print(value)
```
Decimal to Binary
Binary to Decimal
Built-in functions
Our implementations

## Slide 37
Where binary goes from here
Today was one corner of a large subject.
Non-negative integers in binary
today
✓
Binary to decimal
today
✓
Negative integers: two's complement
later
Real numbers: floating point
later
Images, sound, compression, transmission
other courses
Arithmetic implemented in binary
other courses

## Slide 38
Lecture summary
```python
The for loop
Sequence iteration
Runs once per item in a sequence (not just a counter loop). 
The range() function
Generates numbers using range(start, stop, step)- includes start, excludes stop. 
for vs. while
Use for when iterating over a known sequence. 
Use while when waiting for a condition to become true. 
```
Patterns and numbers
The Accumulator Pattern
Initialize before the loop, update inside, use after. 
Efficiency 
Carrying a running value forward beats recalculating it from scratch. 
Positional Systems 
The positional principle works in any base  2; binary is simply base 2. 
Converting between bases
% 2 and // 2 peel the digits off; value = value * 2 + digit reads them back in.
The for loop
Loop patterns
Numeral systems
Binary

## Slide 39
Self practice
Write a program for each of these.
Rewrite with for
Take your while solutions to last week's star patterns and write them with for.
Powers of a base
Read a base b and a count n, and print b⁰ to bⁿ without recomputing a power from scratch.
Count the digits
Read a non-negative integer and print how many digits it has, using % 10 and // 10.
Binary, both directions
Print the binary form of every number from 0 to 15, then read a binary string back and print its decimal value.

## Slide 40
PYTHON COURSE · WEEK 3 · LECTURE 1
Next: Strings, Lists and Tuples
Where for comes into its own, and binary back to decimal
