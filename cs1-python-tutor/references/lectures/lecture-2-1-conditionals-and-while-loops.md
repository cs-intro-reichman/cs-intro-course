# Lecture 2-1: Conditionals and while loops (week 2)

## Slide 1
PYTHON COURSE · WEEK 2 · LECTURE 1
Conditionals and Loops
Control flow, conditionals (if, else, elif) and while loops

## Slide 2
Lecture overview
Program flow
Conditionals
Loops
Examples
1
Program flow
sequence, then branching
2
Conditionals
if, else, elif
3
Loops
while, and the four classic bugs
4
Examples
programs that use both

## Slide 3
Program control flow structures
Program flow
Conditionals
Loops
Examples
Until now
Sequential execution
Runs once, top-to-bottom, and does the same thing every time.
From today
Conditional branching
Iterative execution
Can choose what to do, and can repeat work as many times as needed.
Conditionals let a program respond to its input. 
Loops let a program repeat operations efficiently without code duplication.

## Slide 4
Fundamental program flow structures
The order statements actually run in (not the order they are written).
Sequential
statement 1
statement 2
statement 3
one after another
Conditional
```python
test
```
```python
True
```
```python
False
```
```python
A
```
```python
B
```
the paths rejoin
Iterative (loops)
```python
test
```
```python
True
```
body
```python
False
```
the path goes back
Conditionals branch forwards. Loops branch backwards. 

## Slide 5
The if statement
Program flow
Conditionals
Loops
Examples
`abs_value.py`
```python
x = int(input("Enter a number: "))
if x < 0:
    x = -x
print("Absolute value:", x)
```
```python
terminal
```
```python
Enter a number: -12
Absolute value: 12
```
read x
```python
x < 0
```
```python
True
```
```python
False
```
```python
x = -x
```
```python
print(x)
```
Two inputs, two different routes, one program.

## Slide 6
The if statement
Core components
Condition - A boolean expression.
Colon (:) - Delimits the header from the conditional block.
Block - One or more indented statements executed if and only if condition evaluates to True.
Syntax rules
Unlike Java or C, Python requires no parentheses ( ) around the condition and no curly braces { } for block scope. Indentation defines the execution scope.
`if_syntax.py`
```python
block # executed if True
```
Syntax:

## Slide 7
Common errors: colon & indentation
Missing indentation after the colon
```python
terminal
```
```python
    print("x is positive")
    ^
IndentationError: expected an indented
block after 'if' statement on line 3
```
     Bad indentation
Every line right after the colon must be indented.
Fix: indent the block consistently, usually 4 spaces.
Missing colon after the condition
```python
terminal
```
```python
    if x < 0
            ^
SyntaxError: expected ':'
```
```python
     Missing colon
The colon marks where the header ends and the block begins.
Fix: add ':' at the end of the if line.
```

## Slide 8
Semantic block scoping
In Python, indentation is not a style choice – it determines program semantics.
`version_a.py`
```python
# Block includes print statement
if x < 0:
    x = -x
    print("negative")
```
Both lines run, or neither does.
`version_b.py`
```python
# Block ends before print statement
if x < 0:
    x = -x
print("done")
```
Only the indented line belongs to the if.
The rule
All statements indented to the same level form the conditional block. Returning to the previous indentation level closes the block.
The conventions
Uset four spaces per indentation level (PEP 8 style guide). Never mix spaces and tabs doing so raises a TabError.

## Slide 9
What counts as a condition ?
Any expression that evaluates to True or False (Boolean expression).
```python
Chained comparisons
Python supports mathematical range checks such as 0 0 <= grade <= 100 (evaluates the middle term only once).
```
`chained.py`
```python
if 0 <= grade <= 100:
    print("Valid grade")
```
```python
0
```
```python
100
```
valid
One comparison, not two.
`condition.py`
```python
if score >= 60 and attendance >= 0.8:
    print("Pass")
```
```python
Compound Conditions
Boolean operators (and, or, not) combine multiple expressions into a single True/False result.
```

## Slide 10
The if-else statement
`if_else.py`
Exactly one block runs
The else block executes if and only if the condition evaluates to False.
```python
condition
```
```python
True
```
```python
False
```
```python
if block
```
```python
else block
```
carry on
The two paths rejoin.
```python
if block 
# executed if True
```
```python
else block
# executed if False
```

## Slide 11
Example: Coin flip
`coin_flip.py`
```python
import random

if random.random() < 0.5:
    print("Heads")
else:
    print("Tails")
```
Dynamic output via randomization
random.random() returns a float in [0, 1) 
(you met it in lecture 1-2).
Heads
Tails
```python
0
```
```python
0.5
```
```python
1
```
Same program - different output each run. 
Run it four or five times.

## Slide 12
Example: The max two values
`max_v1.py`
```python
# 1 — symmetric
if x >= y:
    max_val = x
else:
    max_val = y
```
Version 1: Explicit logic
Evaluates both paths clearly:
if x >= y choose x, otherwise choose y.
`max_v2.py`
```python
# 2 — assume, then correct
max_val = x
if y > max_val:
    max_val = y
```
Version 2: Assume & Correct
Sets a default answer (x), then corrects it only if y turns out to be larger. 

## Slide 13
Example: Guard conditions
Using conditionals to prevent runtime errors.
`quadratic.py`
```python
import math

d = b * b - 4.0 * a * c
if d < 0.0:
    print("No real roots")
else:
    root = math.sqrt(d)
    print("x1 =", (-b + root) / (2*a))
    print("x2 =", (-b - root) / (2*a))
```
Why is the guard needed ?
Passing a negative value to math.sqrt() raises a ValueError 
(as seen in Lecture 1-2).
Preventing runtime crashes
The if statement validates the input first, ensuring math.sqrt() only executes on safe inputs.

## Slide 14
Example: Nested vs. Independent ifs
Both print the same thing. What is the difference?
`nested_if.py`
```python
if a == b:
    print("a equals b")
else:
if a > b:
    print("a is greater")
else:
    print("b is greater")
```
`chained_if.py`
```python
if a == b:
    print("a equals b")
if a > b:
    print("a is greater")
if a < b:
    print("b is greater")
```

## Slide 15
Example: Nested vs. Independent ifs
```python
a == b
```
```python
True
```
"a equals b"
```python
False
```
```python
a > b
```
"a is greater"
"b is greater"
Nested if
The first True exits - remaining tests are skipped.
```python
False
```
```python
True
```
```python
a == b
```
```python
True
```
"a equals b"
```python
a > b
```
"a is greater"
```python
a < b
```
"b is greater"
Independent ifs
Every test runs, every time.
```python
True
```
```python
True
```
```python
False
```
```python
False
```
```python
False
```

## Slide 16
The elif statement
if-elif-else chain
The first True leaves the chain
(Identical to nested if)
`elif.py`
```python
if a == b:
    print("a equals b")
elif a > b:
print("a is greater")
else:
print("b is greater")
```
Same execution flow as nested if, with flat indentation
```python
a == b
```
```python
True
```
"a equals b"
```python
False
```
```python
a > b
```
"a is greater"
"b is greater"
```python
False
```
```python
True
```

## Slide 17
Example: Tax calculation
Task: compute the applicable tax rate, according to income level.
Tax bracket | Income
10% | ₪0 – ₪5,280
14% | ₪5,281 – ₪9,010
21% | ₪9,011 – ₪14,000
31% | ₪14,001 – ₪20,000
34% | ₪20,001 and up
`tax_v1.py`
```python
if income <= 5280:
    rate = 0.10
else:
    if income <= 9010:
        rate = 0.14
    else:
        if income <= 14000:
            rate = 0.21
        else:
            if income <= 20000:
                rate = 0.31
            else:
                rate = 0.34
```
Nested ifs: each level pushes the code further right.

## Slide 18
Example: Tax calculation
Task: compute the applicable tax rate, according to income level.
`tax_v2.py`
```python
if income <= 5280:
    rate = 0.10
elif income <= 9010:
    rate = 0.14
elif income <= 14000:
    rate = 0.21
elif income <= 20000:
    rate = 0.31
else:
    rate = 0.34
```
Chained elif: keeps it flat
Tax bracket | Income
10% | ₪0 – ₪5,280
14% | ₪5,281 – ₪9,010
21% | ₪9,011 – ₪14,000
31% | ₪14,001 – ₪20,000
34% | ₪20,001 and up

## Slide 19
The conditional expression (ternary if)
A one-line if / else that produces a value.
`expression.py`
```python
max_val = a if a >= b else b
```
is exactly the same as
`statement.py`
```python
if a > b:
    max_val = a
else:
    max_val = b
```
Statement vs. Expression
The if statement does something (controls block execution). 
The if expression evaluates to something (a value), so it can appear anywhere a value can.
The word order
Python puts the value first and the condition second. It reads like English: take a, if a >= b, otherwise b.

## Slide 20
The conditional expression (ternary if)
Syntax
```python
Syntax
```
```python
expression_1 if condition else expression_2
```
```python
Semantics
If the condition is True -  the expression evaluates to expression_1
Else - the expression evaluates to expression_2.
```

## Slide 21
When to use the conditional expression
`plural.py`
```python
count = 3
word = "items" if count > 1 else "item"
print(f"You bought {count} {word}")
```
```python
terminal
```
```python
You bought 3 items
```
When to use
Use the conditional expression for short, single-line assignments where both outcomes are simple values.
Keeps code simple when used appropriately, but can reduce readability if overused.
When to avoid
Use standard if-else statement if either branch involves complex logic, multiple operations or requires explanation.

## Slide 22
The while loop
Program flow
Conditionals
Loops
Examples
`count_up.py`
```python
n = int(input())
count = 0
while count < n:
    print(count)
    count = count + 1
```
```python
n = int(input())
```
```python
count = 0
```
```python
count < n
```
```python
True
```
```python
print(count)
```
```python
count = count + 1
```
```python
False
```
Count from 0 to n-1

## Slide 23
The while loop
`while.py`
while
```python
condition
```
```python
loop block
```
```python
Semantics
Evaluate condition (True \ False)
If True – execute the loop block and return to step 1.
If False – exit the loop and continue to the next statement.
```
```python
loop block (body) 
# executed while True
```
Syntax
```python
False
```
```python
True
```

## Slide 24
`count_up.py`
```python
n = int(input())
count = 0
while count < n:
    print(count)
    count = count + 1
```
print | count < n | count | n
0 | True | 0 | 3
1 | True | 1 | 3
2 | True | 2 | 3
loop ends | False | 3 | 3
Tracing a loop
By hand, on paper, with small numbers. Here n = 3.

## Slide 25
Always check the edges
What does the loop print for each of these?
n = 3
```python
0
1
2
```
n = 1
```python
0
```
n = 0
n = -3
n = 1000
```python
0
1
2
...
999
```
Two of them print nothing at all. When you write a loop, ask what it does for zero, for one, and for a negative input.

## Slide 26
`count_up.py`
```python
n = int(input())
count = 0
while count < n:
    print(count)
    count = count + 1
```
```python
Three essential moving parts
Initialization: Set the loop variable (count) before entering the loop.
Condition: Evaluated prior to every iteration. 
Update: Modify the loop variable (count) inside the loop-body to ensure termination.
```
The anatomy of a while counted loop
1
2
3

## Slide 27
Augmented assignment
`augmented.py`
```python
count = count + 1     # what we wrote
count += 1            # the same thing
```
Shortcut syntax for updating variable values.
```python
Underlying mechanism
Python evaluates count + 1 first, then re-binds the variable count to the result.
This is standard variable re-binding (as covered in Lecture 1-2).
```
```python
No increment (++) operator
Python does not support i++ or i-- like other languages (C, Java).             Always use i += 1 or i -= 1.
```
```python
+= works for any type supporting addition, including floats and strings.
```
From here on we write it the short way.
The augmented operators
```python
+=
```
```python
-=
```
```python
*=
```
```python
/=
```
```python
//=
```
```python
%=
```
```python
**=
```

## Slide 28
What happens here?
`infinite.py`
```python
count = 10
while count > 0:
    print(count)
    count += 1
```
The intention is to count down from 10 to 1.
Read it before you run it.

## Slide 29
Loop Bug 1 – Infinite loops
`infinite.py`
```python
count = 10
while count > 0:
    print(count)
    count += 1   # wrong way
```
```python
terminal
```
```python
10  11  12  13  14  ...
KeyboardInterrupt
```
The update moves count the wrong way, so the condition never fails.
How to fix it
Make sure the body updates a variable the condition tests, and that the update moves towards ending the loop.
How to spot it
The program prints forever, and the values run away from the bound instead of towards it. Ctrl-C stops it.

## Slide 30
What will this print?
`bug_updates.py`
```python
i = 0
v = 1
while i <= n:
    print(i, v)
i += 1
v *= 2
```
Take n = 3. What appears on the screen?
Read it before you run it.

## Slide 31
Loop Bug 2 — Out-of-block updates
`bug_updates.py`
```python
i = 0
v = 1
while i <= n:
    print(i, v)
i += 1
v *= 2
```
`fixed.py`
```python
i = 0
v = 1
while i <= n:
    print(i, v)
    i += 1
    v *= 2
```
prints 0 1 forever
it ends
The update sits outside the loop body, so nothing advances.
How to spot it
The same output line repeats forever. The body is shorter than you meant — read the indentation, not the intention.
How to fix it
Indent every line that belongs to the loop to the same level under the while.

## Slide 32
How many times does each loop run?
`a.py`
```python
i = 0
while i < 4:
    i += 1
```
`b.py`
```python
i = 0
while i <= 4:
    i += 1
```
Same body, one character apart. What is i when each loop ends?
Read it before you run it.

## Slide 33
Loop Bug 3 – Off-by-one errors
Neither < nor <= is wrong. Using one when you meant the other is.
```python
while i < 4
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
while i <= 4
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
How to spot it
The last item is missing, or one extra is included.
How to fix it
Trace the first and the last pass with small values, and check the boundary.

## Slide 34
What is total at the end?
`bug_reinit.py`
```python
while i < n:
    total = 0
    total += i
    i += 1
```
Take i = 0 and n = 4. What does total hold?
Read it before you run it.

## Slide 35
Loop Bug 4 – Variable re-initialization
`correct.py`
```python
total = 0
while i < n:
    total += i
    i += 1
```
`bug_reinit.py`
```python
while i < n:
    total = 0
    total += i
    i += 1
```
total survives
total resets
How to spot it
The answer is plausible but wrong — usually the value of the last pass alone. Nothing crashes.
The accumulator is initialized inside the loop, so it resets.
How to fix it
Initialize before the loop, not inside it. Ask of every line: should this happen once, or every time?

## Slide 36
Example: Powers of two
Program flow
Conditionals
Loops
Examples
`powers.py`
```python
n = int(input("n: "))
i = 0
v = 1
while i <= n:
    print(i, v)
    i += 1
    v *= 2
```
```python
terminal
```
```python
0 1
1 2
2 4
3 8
4 16
5 32
6 64
```
i counts, v doubles — and these are the column values of binary.
Task: print powers of two 20, 21, 22, ..., 2n

## Slide 37
Example: Digit sum
Task: Add up the digits of a given number. E.g., 4913 outputs 4 + 9 + 1 + 3 = 17.
`digit_sum.py`
```python
n = int(input("Number: "))
total = 0
while n > 0:
    digit = n % 10
    total += digit
    n = n // 10    # or n //= 10
print("Digit sum:", total)
```
n | digit | total
4913 | 3 | 3
491 | 1 | 4
49 | 9 | 13
4 | 4 | 17
```python
Digit extraction in base 10
Extracting digits: n % 10 extracts the last (rightmost) digit.
Removing digits: n // 10 strips the last digit, shrinking n toward 0 to end the loop.
```
What does it do for n = 0? 

## Slide 38
```python
Minimum finding pattern
First input as baseline: smallest must start with an actual value from the stream.
Priming read: Fetching input outside the loop enables direct smallest = x initialization.
Order matters: Updating x at the end of the loop keeps sentinel checks reliable.
```
Example: Minimum value
Processing a sequence of unknown length using a sentinel-controlled loop
`smallest.py`
```python
x = int(input("Number (-1 to finish): "))
smallest = x
while x != -1:
    if x < smallest:
        smallest = x
    x = int(input("Number (-1 to finish): "))
if smallest == -1:
    print("No numbers were entered.")
else:
    print("Smallest:", smallest)
```
```python
Sentinel loop pattern
Stream control: Using while to process data stream of unpredictable length, until a stop value (-1) is met.
Named Constant: Define END = -1 to avoid magic numbers and improve readability.
```
Task: Read non-negative numbers until a sentinel value (-1) is entered. 
Output the minimum value, or report if no input was provided.
```python
END = -1 
```
```python
END: 
```
```python
END: 
```

## Slide 39
The run for 8, 3, 9, 1, 6, -1
```python
The line never rises: smallest can only go down, and no bar ever reaches below it.
Then -1 arrives, the loop ends, and the line is the answer.
```
```python
8
```
```python
8
```
```python
3
```
```python
3
```
```python
9
```
```python
3
```
```python
1
```
```python
1
```
```python
6
```
```python
1
```
smallest
Input numbers
smallest
`smallest.py`
```python
x = int(input("Number (-1 to finish): "))
smallest = x
while x != -1:
    if x < smallest:
        smallest = x
    x = int(input("Number (-1 to finish): "))
if smallest == -1:
    print("No numbers were entered.")
else:
    print("Smallest:", smallest)
```
```python
END: 
```
```python
END: 
```
```python
END = -1 
```
Tracing the minimum value

## Slide 40
Example: Input validation
Repeat until valid input is entered.
`validate.py`
```python
grade = int(input("Grade (0-100): "))
while not (0 <= grade <= 100):
    print("That is not a valid grade.")
    grade = int(input("Grade (0-100): "))
print("Grade recorded:", grade)
```
Unknown number of iterations
The number of iterations is unknown in advance - it depends on runtime user input. A fixed counter cannot handle this pattern.
Code duplication note
Notice the input() line appears twice (before and inside the loop). How can we avoid it ?

## Slide 41
The break statement
Exiting a loop directly from within its body
`validate_break.py`
```python
while True:
    grade = int(input("Grade (0-100): "))
    if 0 <= grade <= 100:
        break
    print("That is not a valid grade.")
print("Grade recorded:", grade)
```
```python
Semantics
break terminates the innermost enclosing loop immediately. Execution jumps directly to the first statement following the loop, skipping any remaining loop tests.
```
```python
The while True pattern
Creates an intentional infinite loop whose exit condition is dynamically evaluated inside the loop body using break.
```
Use while condition when the exit test is known before the pass; 
use while True with break when the exit test occurs mid-iteration.

## Slide 42
Example: a random point inside the circle
Task: Generate a random point that lands inside the unit circle (radius 1, centered at the origin). 
`point.py`
```python
import random

while True:
    # generate random x,y in [-1,1)
    x = 2.0 * random.random() - 1.0
    y = 2.0 * random.random() - 1.0
    if x * x + y * y <= 1.0:
        break
print("Inside:", x, y)
```
Accepted and rejected
Navy dots landed inside the circle and end the loop. 
Orange crosses are thrown away.

## Slide 43
Nested loops
`square.py`
```python
i = 0
while i < 3:
    j = 0
    while j < 3:
        print("*", end="")
        j += 1
    print()
    i += 1
```
```python
*
```
```python
*
```
```python
*
```
```python
*
```
```python
*
```
```python
*
```
```python
*
```
```python
*
```
```python
*
```
three rows of three
j is reset inside the outer loop
The inner loop runs to the end on every pass of the outer one. 
Putting j = 0 in the wrong place is the classic nested-loop bug.
```python
end="" leaves out the newline; print() supplies it.
```

## Slide 44
Tracing the nested loop
Nine passes of the inner loop, three of the outer.
pass
i
j
prints
```python
1
```
```python
0
```
```python
0
```
```python
*
```
```python
2
```
```python
0
```
```python
1
```
```python
*
```
```python
3
```
```python
0
```
```python
2
```
```python
*   then a newline
```
```python
4
```
```python
1
```
```python
0
```
```python
*
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
*
```
```python
6
```
```python
1
```
```python
2
```
```python
*   then a newline
```
```python
7
```
```python
2
```
```python
0
```
```python
*
```
```python
8
```
```python
2
```
```python
1
```
```python
*
```
```python
9
```
```python
2
```
```python
2
```
```python
*   then a newline
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
j
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
*
```
```python
*
```
```python
*
```
```python
*
```
```python
*
```
```python
*
```
```python
*
```
```python
*
```
```python
*
```
```python
i
```

## Slide 45
Self practice
Write programs that output the following:
square
נ
```python
***
***
***
```
left
```python
*
**
***
```
right
```python
  *
 **
***
```
centered
```python
  *  
 *** 
*****
```
The outer structure never changes. Only the number of stars per row, and where the row starts.
✓

## Slide 46
Lecture summary
Conditional
if
if-else
elif
The conditional expression
Sequential
Execution line-by-line in order.
Fundamental program flow structures
Iterative (loops)
while
for (in next lecture)
statement 1
statement 2
statement 3
```python
test
```
```python
True
```
```python
False
```
```python
A
```
```python
B
```
```python
test
```
```python
True
```
body
```python
False
```
Program flow
Conditionals
Loops
Examples

## Slide 47
PYTHON COURSE · WEEK 2 · LECTURE 2
Next: Loops and numeral systems
for and range(), loop patterns, and numbers in binary
