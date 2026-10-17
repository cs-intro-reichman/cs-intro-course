# Lecture 6-1: Files (week 6)

## Slide 1: Files
.txt
PYTHON COURSE · WEEK 6 · LECTURE 1
Files
Reading and writing data
Reichman University

## Slide 2: Where a program's data comes from
Where a program's data comes from
So far we used only the first two.
In the code: ratings = [[4, 5, 4], ...]
The keyboard: input(), gone when the program ends
A file: on the disk before and after the run
Another program: its output is our input

## Slide 3: The big picture
The big picture
Programs reach devices through Python and the operating system.
Your program
open, read, print
Python
the input/output library
Operating system
folders, files, drivers
Keyboard
Screen
Disk: files
devices

## Slide 4: Files: the plan
Files: the plan
Four parts today.
Reading a file
Files of data
Writing a file
Standard input and output

## Slide 5: What a text file is
What a text file is
A name: demo.dat, grades.csv, notes.txt
A place: it lives in a folder on the disk
Contents: characters, one line after another
Line breaks: a special character, \n, ends each line

## Slide 6: A file is one long string
A file is one long string
Lines are separated by \n characters.
```python
demo.dat in an editor
4
1 1 2 
0 1 3 0 3
0 1
```
```python
4
```
```python
\n
```
```python
1
```
```python
·
```
```python
1
```
```python
·
```
```python
2
```
```python
·
```
```python
\n
```
```python
0
```
```python
·
```
```python
1
```
```python
·
```
```python
3
```
```python
·
```
```python
0
```
```python
·
```
```python
3
```
```python
\n
```
```python
0
```
```python
·
```
```python
1
```
```python
\n
```
what is stored: 23 characters  ·  “·” is a space, “\n” ends a line

## Slide 7: Reading a whole file
Reading a whole file
```python
python read_whole.py
'4\n1 1 2 \n0 1 3 0 3\n0 1\n'
4
1 1 2 
0 1 3 0 3
0 1
```
`read_whole.py`
```python
with open("demo.dat") as f:
    text = f.read()

print(repr(text))
print(text)
```
```python
repr(s) shows a string the way you would type it in code:
in quotes, with \n for each line break.
print(s) acts on the line breaks; repr(s) shows them.
```

## Slide 8: The with statement
The with statement
`read_whole.py`
```python
with open("demo.dat") as f:
    text = f.read()

print(repr(text))
print(text)
```
open(name)
Finds the file, opens it to read.
with … as f:
Names it f; closes it at the end.
f.read()
The whole contents, as one str.

## Slide 9: Reading line by line
Reading line by line
```python
python read_lines.py
'4\n' ['4']
'1 1 2 \n' ['1', '1', '2']
'0 1 3 0 3\n' ['0', '1', '3', '0', '3']
'0 1\n' ['0', '1']
```
`read_lines.py`
```python
with open("demo.dat") as f:
    for line in f:
        print(repr(line), line.split())
```

## Slide 10: From text to numbers
From text to numbers
Always text: whatever is read from a file is a str
strip(): removes spaces and \n from both ends
split(): cuts a line into words
int() and float(): turn one word into a number
"3" + "4" is "34".
Convert before you compute: int("3") + int("4") is 7.

## Slide 11: Counting the values in a file
Counting the values in a file
```python
python count_values.py
0: 3
1: 4
2: 1
3: 2
```
`count_values.py`
```python
# How often each number appears in demo.dat.
# The first number, n: the rest are 0 .. n-1.

with open("demo.dat") as f:
    tokens = f.read().split()

n = int(tokens[0])
count = [0] * n
for t in tokens[1:]:
    count[int(t)] += 1

for i in range(n):
    print(f"{i}: {count[i]}")
```

## Slide 12: Where Python looks for a file
Where Python looks for a file
A bare name: "demo.dat" is looked for in the current folder
Current folder: where the terminal is when python starts
A path: "data/demo.dat" looks inside data
Run in VS Code: starts in the folder you opened (File > Open Folder)
So: open the folder that holds the program and its data file

## Slide 13: When the file is not there
When the file is not there
```python
python missing_file.py
No such file: demo.txt
```
`missing_file.py`
```python
name = "demo.txt"        # a typo: it is demo.dat
try:
    with open(name) as f:
        print(f.read())
except FileNotFoundError:
    print("No such file:", name)
```

## Slide 14: Files: the plan
Files: the plan
Four parts today.
Reading a file
Files of data
Writing a file
Standard input and output

## Slide 15: A file of records
A file of records
One line per student; commas separate the fields.
```python
grades.csv
name,hw,exam
Dana,88,92
Noam,75,64
Maya,95,81
Yoni,52,58
```
The header
line 1 names the columns
A record
every other line: one student
Fields
line.split(",") separates them

## Slide 16: Reading the records
Reading the records
```python
python final_grades.py
Dana   90.8
Noam   67.3
Maya   85.2
Yoni   56.2
```
`final_grades.py`
```python
with open("grades.csv") as f:
    f.readline()              # skip the header
    for line in f:
        name, hw, exam = line.strip().split(",")
        final = 0.3 * int(hw) + 0.7 * int(exam)
        print(f"{name:5} {final:5.1f}")
```

## Slide 17: USA.txt: the first lines
USA.txt: the first lines
A header line, then one line per town.
```python
USA.txt
669905.0 247205.0 1244962.0 700000.0
 1097038.8890   245552.7780
 1103961.1110   247133.3330
 1104677.7780   247205.5560
 1108586.1110   249238.8890
 1109713.8890   250111.1110
...
```
The header
line 1, four numbers that give the box the map fits in
A town
each line after it holds one town's two coordinates
13,510 lines
the header, then 13,509 towns

## Slide 18: A bigger file: 13,509 towns
A bigger file: 13,509 towns
```python
python usa_points.py
13509 towns
header: ['669905.0', '247205.0',
         '1244962.0', '700000.0']
x: 669905.556 to 1244961.111
y: 245552.778 to 490000.0
```
`usa_points.py`
```python
# USA.txt: a header line with the bounding box,
# then one "x y" pair per town.

with open("USA.txt") as f:
    header = f.readline().split()
    xs, ys = [], []
    for line in f:
        x, y = line.split()
        xs.append(float(x))
        ys.append(float(y))

print(len(xs), "towns")
print("header:", header)
print(f"x: {min(xs)} to {max(xs)}")
print(f"y: {min(ys)} to {max(ys)}")
```

## Slide 19: Drawing the map: the plan
Drawing the map: the plan
W and H: the size of the map, 60 columns by 18 rows
The grid: H rows of W spaces, a 2D list as in 5-1
Each town: puts a * in one cell of the grid
Columns: west to east, from 0 to W - 1
Rows: north to south, from 0 at the top to H - 1

## Slide 20: From a town to a cell
From a town to a cell
Worked example: the first town in USA.txt.
The map, west to east
```python
left = 669905.556
```
```python
right = 1244961.111
```
```python
1097038.889
```
The columns of the grid
```python
0
```
```python
59
```
```python
43
```
The same share of the way across: 0.743
```python
the arithmetic
x = 1097038.889
(x - left) / (right - left) = 0.743
0.743 * (W - 1) = 43.8
col = int(43.8) = 43

y = 245552.778, the smallest y
(top - y) / (top - bottom) = 1.0
1.0 * (H - 1) = 17.0
row = 17, the bottom line
```

## Slide 21: usa_map.py: reading the towns
usa_map.py: reading the towns
```python
usa_map.py (lines 1 to 10)
```
```python
# Draws the towns of USA.txt as a map of characters.
W, H = 60, 18          # columns and rows

xs, ys = [], []
with open("USA.txt") as f:
    f.readline()       # skip the header
    for line in f:
        x, y = line.split()
        xs.append(float(x))
        ys.append(float(y))
```
W, H
the map's size, 60 by 18 characters
readline()
skips the header line
xs, ys
one entry per town, as in usa_points.py

## Slide 22: usa_map.py: drawing the towns
usa_map.py: drawing the towns
```python
usa_map.py (lines 12 to 22)
```
```python
left, right = min(xs), max(xs)
bottom, top = min(ys), max(ys)

grid = [[" "] * W for _ in range(H)]
for i in range(len(xs)):
    col = int((xs[i] - left) / (right - left) * (W - 1))
    row = int((top - ys[i]) / (top - bottom) * (H - 1))
    grid[row][col] = "*"

for row in grid:
    print("".join(row))
```
left ... top
the edges of the map, from the data
col, row
the cell, as in the worked example
The last loop
prints the grid, one row per line

## Slide 23: The map, printed
The map, printed
Each * is one or more towns.
```python
python usa_map.py
********************************** *
***************** **********************                 **
********* * *******************************       ***** ****
**** * ** ******* **************************  *************
*****    ***********************************************
***** * *** ********************************************
*******  *  ****************************************
 *******  **** ************************************
  *****  *****************************************
   ***** ** ***************************************
    ************ *******************************
       ***************************************
             ***  * *************************
                    *** ************** ******
                        ******            ****
                         ****             ****
                           *               ***
                                           *
```

## Slide 24: The points, plotted
The points, plotted
Each of the 13,509 points is one town.

## Slide 25: Files: the plan
Files: the plan
Four parts today.
Reading a file
Files of data
Writing a file
Standard input and output

## Slide 26: Writing a file
Writing a file
open(name, "w"): creates the file for writing
open(name, "a"): adds to the end of an existing file
f.write(s): writes exactly s; add \n yourself
print(x, file=f): prints into the file, not the screen
"w" empties the file first.
Opening an existing file with "w" deletes its contents.

## Slide 27: Writing, then reading back
Writing, then reading back
```python
python write_squares.py
1 1
2 4
3 9
4 16
5 25
```
`write_squares.py`
```python
with open("squares.txt", "w") as f:
    for i in range(1, 6):
        f.write(f"{i} {i * i}\n")

with open("squares.txt") as f:
    print(f.read(), end="")
```

## Slide 28: Read, decide, write
Read, decide, write
```python
python passed.py
3 names written to passed.txt

passed.txt:
Dana
Noam
Maya
```
`passed.py`
```python
passed = []
with open("grades.csv") as f:
    f.readline()              # skip the header
    for line in f:
        name, hw, exam = line.strip().split(",")
        if 0.3 * int(hw) + 0.7 * int(exam) >= 60:
            passed.append(name)

with open("passed.txt", "w") as f:
    for name in passed:
        f.write(name + "\n")
print(len(passed), "names written to passed.txt")
```

## Slide 29: Files: the plan
Files: the plan
Four parts today.
Reading a file
Files of data
Writing a file
Standard input and output

## Slide 30: Standard input and output
Standard input and output
Standard output: print writes there; the screen, by default
Standard input: input() reads it; the keyboard, by default
sys.stdin: standard input, as a file
sys.argv: the words typed after python file.py

## Slide 31: A program that writes numbers
A program that writes numbers
```python
python random_numbers.py 3
0.4234137005317864
0.2984657006398488
0.7456080688315734
```
`random_numbers.py`
```python
import random
import sys

n = int(sys.argv[1])   # typed after the name
for i in range(n):
    print(random.random())
```

## Slide 32: A program that reads numbers
A program that reads numbers
```python
python average.py
100
200
100
300
<Ctrl-D>
Average: 175.0
```
`average.py`
```python
import sys

total, count = 0.0, 0
for line in sys.stdin:   # one line at a time
    total += float(line)
    count += 1
print("Average:", total / count)
```

## Slide 33: Redirection and pipes
Redirection and pipes
The terminal can send input and output to files or programs.
```python
>
```
`random_numbers.py`
`data.txt`
output goes into a file
```python
<
```
`data.txt`
`average.py`
input comes from a file
```python
|
```
`random_numbers.py`
`average.py`
one feeds the next
light boxes are programs; tinted boxes are files

## Slide 34: Redirection: examples
Redirection: examples
With a file, and with a pipe.
```python
terminal
% python random_numbers.py 1000 > data.txt
% python average.py < data.txt
Average: 0.49570948891636646
% python random_numbers.py 1000000 | python average.py
Average: 0.5007775704132853
```

## Slide 35: One program, different inputs
One program, different inputs
The keyboard: python average.py
A file: python average.py < data.txt
A pipe: … | python average.py
The code: unchanged

## Slide 36: Files in one slide
Files in one slide
Read
with open(name) as f
f.read(): the whole file
for line in f: line by line
f.readline(): one line
Convert
Everything read is a str
strip(), then split()
int() and float() on each word
Write
open(name, "w") erases first
open(name, "a") appends
write adds no line break
Standard I/O
print and input
sys.stdin, sys.argv
>  <  |  in the terminal
