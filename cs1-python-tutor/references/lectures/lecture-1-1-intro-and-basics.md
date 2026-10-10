# Lecture 1-1: Intro and basics (week 1)

## Slide 1
PYTHON COURSE · WEEK 1 · LECTURE 1
Fundamentals
Introduction to Computer Science in Python

## Slide 2
Lecture overview
The course
Computer science
Programming
Problem solving
Pseudocode
Why Python
Syntax
Readability
Edit, Run & Debug
1
The course
what it is, and what it expects
2
Computer science
about problems, not computers
3
Problem to program
thinking first, then pseudocode
4
Python
syntax, readability, and running code

## Slide 3
Course objectives
Basic exposure to Computer Science - as a field, not just a tool
Basic programming skills - specifically, in Python
What will this course give you ?
The course
Computer science
Programming
Problem solving
Pseudocode
Why Python
Syntax
Readability
Edit, Run & Debug

## Slide 4
Sharpen your analytic skills - precise, structured thinking
Appreciate clarity and elegance - in code, not only correctness
Develop a taste for beauty - in science and engineering
Learn how to learn and develop – not only as a programmer, but also as a computer scientist
And along the way you will ...
Course objectives

## Slide 5
Course requirements
Attend:
Two weekly lectures (שיעור)
One weekly recitation (תרגיל)
One weekly workshop (סדנה) 
Submit:
A weekly homework assignments (שיעורי בית)

## Slide 6
Course website (“Moodle”)
Contents:
 Lectures / recitations slides + code
HW documents + code
Course announcements
Important:
The only formal and abiding channel of communications between the course team and the students is the course web site
What is said orally by the course staff about HW, exams, requirements, grading, deadlines – is tentative. What is written in the web site is formal.

## Slide 7
Q&A forum
How to ask questions ?
Find the forum — by week or topic
Read first — check existing posts before asking
Post a question – if needed.
Expect an answer — within a few hours, from a TA or a fellow student
Feel free to answer others — if you think your answer will be useful
Keep it clean — professional tone, in English

## Slide 8
Books and resources
“Python for Everybody” — Severance, free online – py4e.com/book
The official Python tutorial – docs.python.org/3/tutorial
“Think Python” — Downey, 3rd ed., free online – greenteapress.com

## Slide 9
Computer Science is About...
The course
Computer science
Programming
Problem solving
Pseudocode
Why Python
Syntax
Readability
Edit, Run & Debug

## Slide 10
“Computer science is no more about computers than astronomy is about telescopes, biology is about microscopes or chemistry is about beakers and test tubes. Science is not about tools. It is about how we use them, and what we find out when we do.”
Edsger W. Dijkstra
Computer Science is About...

## Slide 11
Computer Science is About...
Theory
Systems
Applications
Common Themes
Programming
The universal language
 of computation
Efficiency
Doing more with less, 
faster and smarter
Beauty
An acquired taste — elegant solutions to hard problems

## Slide 12
High Level Apps & AI
Data Analysis & Simulation
Medical & Imaging systems
E-commerce & Social platforms
AI, Chatbots & NLP
User Products
Mobile & Web applications
Game Development
Productivity & Business tools
Interactive User Interface
Programming is about…
Systems & Core
Operating systems
Compilers
Networks
Cloud & Network protocols
Cyber Security & Cryptography
The course
Computer science
Programming
Problem solving
Pseudocode
Why Python
Syntax
Readability
Edit, Run & Debug

## Slide 13
A taste of programming
Simulate the motion of N heavenly bodies,subject to Newton’s laws of motion and gravity

## Slide 14
A taste of programming
`spiral.py`
```python
import turtle
t = turtle.Turtle()
t.speed(0)
colors = ["#A64B00", "#1B3A5C", "#F5B759"]
for i in range(200):
    t.pencolor(colors[i % 3])
    t.forward(i * 2)
    t.right(91)
turtle.done()
```
Live demo – the file is in “week 1 code / spiral.py”.

## Slide 15
Programming is about…
Writing code that is ...
Correct — produces the right answer, every time
Efficient — makes reasonable use of time and memory
Readable — a human can follow it later – including you

## Slide 16
Good code is ...
Easy to understand — for other people and for yourself
Easy to test — you can check that it does what it claims
Easy to maintain and extend — you can change it easily without breaking it
A pleasure to work with — for whoever touches it next
Programming is about…

## Slide 17
The peanut butter sandwich
Write literal instructions – then watch them followed exactly, not as intended.
Write the steps
→
Read them literally
→
Watch it fail
→
Precision is the point

## Slide 18
From a problem to a program
Every program is the end of this chain.
Problem
An algorithm that solves it
Pseudocode describing the algorithm
A program in a high-level language
The course
Computer science
Programming
Problem solving
Pseudocode
Why Python
Syntax
Readability
Edit, Run & Debug

## Slide 19
What a problem is
In computer science a problem is defined by:
Input — what you are given at the start
Output — the result the process has to produce

## Slide 20
Three problems, as input and output
Only what goes in and what must come out — never how.
A natural number
Is it prime?
Two real numbers
Their average
A list of integers
The same list, sorted

## Slide 21
What makes problem-solving computational
An algorithm is a finite, unambiguous procedure that is correct for every valid input.
Precision — every step is spelled out; nothing is left implied
Finiteness — the procedure has to stop, not run forever
Generality — it works for the whole class of inputs, not just the case you tried by hand

## Slide 22
Computational thinking: four habits of mind
Jeannette Wing, 2006 — a general problem-solving skill
Break it into pieces
Spot the repeating pattern
Keep only what matters
Write the precise step

## Slide 23
Pseudocode: the step before code
Human communication: Uses natural language, intuition, and high-level concepts.
Computer execution: Requires strict, step-by-step instructions with zero ambiguity.
Pseudocode as a bridge: Separates what to do from how to write it - reducing cognitive load.
The course
Computer science
Programming
Problem solving
Pseudocode
Why Python
Syntax
Readability
Edit, Run & Debug

## Slide 24
Pseudocode: a worked example
The algorithm - in pseudocode
read n from the user
set i to 0
while i is less than or equal to n:
    print i
    increase i by 1
print "Done"
The problem
Input: a whole number n
Output: the numbers from 0 to n

## Slide 25
Which language should you learn?
Java, Python, C, JavaScript… - every serious language has real strengths
There is no single right answer - the “best” language depends on the job
What transfers is the thinking – 
not the syntax of any one language

## Slide 26
Why Python ?
Clean and minimal syntax – A first working program takes a single line: 
High industry demand – Leading language in AI\ML, Data Science, Backend and Automation.
Extensive ecosystem – Built in tools for immediate use (math, random) plus industry-standard libraries (numpy, pandas).
18
```python
print("Hello World")
```
The course
Computer science
Programming
Problem solving
Pseudocode
Why Python
Syntax
Readability
Edit, Run & Debug

## Slide 27
The intro language at leading CS programs (MIT, Berkeley, Harvard, Stanford).
Interactive and beginner-friendly - Immediate feedback via REPL, with clear readable error messages (Python 3.10+)
Balanced trade-offs – Prioritized readability and expressiveness over raw execution speed – ideal for learning fundamental concepts.
Why Python ?

## Slide 28
Our approach
Teach a meaningful subset of Python - Master essential Python concepts deeply, without getting lost in exhaustive feature lists.
Build problem-solving skills – Develop algorithmic thinking patterns that directly apply to any programming language.
Foundation for future growth - Make learning other languages faster and more intuitive.
Concepts over syntax - Focus on how to think like a computer scientist, not just how to code in Python. 

## Slide 29
Python program example
The algorithm - in pseudocode
set i to 0
while i is less than 6:
    print i
    increase i by 1
print "Done"
2
`count_to_five.py`
```python
# Declares a variable and sets it to 0
i = 0
while i < 6:
    # Prints i, and increments it
    print(i)
    i = i + 1
print("Done")
```
Python implementation
The task: print the numbers 0 to 5

## Slide 30
Python syntax elements - Words
`count_to_five.py`
```python
# Declares a variable and sets it to 0
i = 0
while i < 6:
    # Prints i, and increments it
    print(i)
    i = i + 1
print("Done")
```
Reserved words
Belong to the
language - you cannot
use them as names.
In this example: while
Identifiers
User defined names. 
In this example: i  
The course
Computer science
Programming
Problem solving
Pseudocode
Why Python
Syntax
Readability
Edit, Run & Debug

## Slide 31
```python
False
```
```python
None
```
```python
True
```
```python
and
```
```python
as
```
```python
assert
```
```python
async
```
```python
await
```
```python
break
```
```python
class
```
```python
continue
```
```python
def
```
```python
del
```
```python
elif
```
```python
else
```
```python
except
```
```python
finally
```
```python
for
```
```python
from
```
```python
global
```
```python
if
```
```python
import
```
```python
in
```
```python
is
```
```python
lambda
```
```python
nonlocal
```
```python
not
```
```python
or
```
```python
pass
```
```python
raise
```
```python
return
```
```python
try
```
```python
while
```
```python
with
```
```python
yield
```
Python syntax elements – Reserved words
`count_to_five.py`
```python
# Declares a variable and sets it to 0
i = 0
while i < 6:
    # Prints i, and increments it
    print(i)
    i = i + 1
print("Done")
```

## Slide 32
Python syntax elements – Literals (constants)
`count_to_five.py`
```python
# Declares a variable and sets it to 0
i = 0
while i < 6:
    # Prints i, and increments it
    print(i)
    i = i + 1
print("Done")
```
Numbers
0, 6, 1, 3.14, -5
Strings
Text wrapped in quotes
("Done“ or 'Done')
Booleans & None 
True, False - logical values None - represents absence of value

## Slide 33
Python syntax elements - Symbols
`count_to_five.py`
```python
# Declares a variable and sets it to 0
i = 0
while i < 6:
    # Prints i, and increments it
    print(i)
    i = i + 1
print("Done")
```

## Slide 34
```python
# Declares a variable and sets it to 0
i = 0
while i < 6:
    # Prints i, and increments it
    print(i)
    i = i + 1
print("Done")
```
Python program structure
A statement
A complete instruction that performs an action
A block
A group of statements executed together as a single unit, defined strictly by indentation
A program
A sequence of statements executed in logical order, directed by control flow (like loops and conditions).
`count_to_five.py`

## Slide 35
```python
class Dog:
    def __init__(self, name):
        self.name = name
    def bark(self):
        print(self.name + " says woof")
rex = Dog("Rex")
rex.bark()
```
Python program structure
`dog.py`
A function
A named, reusable block of code that performs a task
A method
A function that belongs to a class, and acts on its object
A class
A blueprint for creating objects, bundling data and methods together.

## Slide 36
Program readability
`count_to_five.py`
```python
# Declares a variable and sets it to 0
i = 0
while i < 6:
    # Prints i, and increments it
    print(i)
    i = i + 1
print("Done")
```
Comments (#)
Notes for developers, completely skipped during execution..
White Spaces  
Blank lines and spaces between operators—used to improve clarity, ignored during execution
Syntax Highlighting
Visual color-coding provided by the editor to make code easier to read
The course
Computer science
Programming
Problem solving
Pseudocode
Why Python
Syntax
Readability
Edit, Run & Debug

## Slide 37
Program readability
“Any fool can write
code that a computer
understands. Good
programmers write code
that humans understand.”
- Martin Fowler
`count_to_five_bad.py`
```python
i=0;
while i<6:print(i);i=i+1
print("Done")
```
Same output. Same program, as far as Python is concerned.
Same code, written badly
PEP 8 - The community style guide. A set of conventions (not strict rules), to make Python code clean and readable.

## Slide 38
Aspects of any language 
`count_to_five.py`
```python
# Declares a variable and sets it to 0
i = 0
while i < 6:
    # Prints i, and increments it
    print(i)
    i = i + 1
print("Done")
```
Semantics
What you want to say or do.
Meaning / intention
Syntax
How to say it. 
The rules of the language: vocabulary and grammar
Style
How well you say it.

## Slide 39
Natural language vs. programming language
Natural languages
Hebrew, English, and other human languages
Allow breaking syntax rules
Occasionally more than one meaning to a sentence
Programming languages
Syntax is sacred
Only one semantic interpretation - no ambiguity

## Slide 40
Ways to execute Python code
Interactive Mode
```python
>>> python
```
Evaluates one expression at a time directly in the terminal (REPL).
Instant execution & feedback
Ideal for testing code snippets
Script Mode
`python myprog.py`
Runs a whole .py file in one command – no separate build step.
Permanent, reusable code
Standard for production software
Notebooks
```python
Jupyter / Colab
```
Combines code cells, docs, and inline visualizations.
Standard in Data Science & AI
Interactive step-by-step flow
The course
Computer science
Programming
Problem solving
Pseudocode
Why Python
Syntax
Readability
Edit, Run & Debug

## Slide 41
The REPL (Read-Eval-Print Loop)
```python
python (interactive)
```
```python
>>> 2 ** 10
1024
>>> "spam" + "eggs"
'spameggs'
>>> print("hello")
hello
>>> 1 / 0
ZeroDivisionError: division by zero
```
Demo this live – no file needed; transcript: “week 1 code / repl_session.txt”.

## Slide 42
Popular IDEs for Python: 
VS Code — free, lightweight, cross-platform
PyCharm — full-featured, Python-dedicated IDE
Jupyter / Colab — interactive, browser-based notebook environments
Integrated Development Environments (IDEs)
What is an IDE ? An all-in-one workspace featuring a code editor, compiler, build tools, debugger and more...

## Slide 43
Debugging – Finding and fixing bugs in your code
Syntax Errors
```python
missing colon :
```
Code violates grammar rules; caught before execution starts, e.g. an unmatched parenthesis.
Runtime Errors
```python
ZeroDivisionError
```
Occur while running; Python calls these exceptions (try/except in Week 4).
Logical Errors
```python
wrong answer
```
The program runs to completion without crashing, but the answer is wrong due to flawed logic.
Murphy's Law: “Anything that can possibly go wrong, will.”

## Slide 44
Before next lecture
Visit the course website — [TBD]
Install Python – python.org/downloads
Set up VS Code (???) — setup guide [TBD]
Homework 1 — play with an existing python program, break it on purpose, then fix it; then write a few of your own. 
Further instructions: see the course website.

## Slide 45
PYTHON COURSE · WEEK 1 · LECTURE 2
Next: Data Types, Input and Output
Variables, dynamic typing, expressions, I/O
