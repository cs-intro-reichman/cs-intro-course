# Lecture 8-1: Computer fundamentals: the Vic computer (week 8)

## Slide 1: Computer Fundamentals
01
INTRO TO CS· WEEK 8 · LECTURE 1
Computer Fundamentals
Inside a simple computer
Reichman University

## Slide 2: Overview
Overview
Goal: understand how a computer works, from the inside
Low level: write programs in the machine's own language
From low to high: from machine language to Python
Tool: Vic, a simple computer you can run

## Slide 3: Computer fundamentals: the plan
Computer fundamentals: the plan
Five parts today.
The Vic computer
Programming Vic
Fetch and execute
Translation
Vic and real computers

## Slide 4: Vic: a simple computer
Vic: a simple computer
I/O
CPU
Memory
input
```python
55
```
```python
12
```
```python
171
```
```python
20
```
← next
output
```python
12
```
```python
67
```
instruction register
```python
900
```
data register (D)
```python
67
```
program counter
```python
0
```
00
```python
800
```
01
```python
490
```
02
```python
800
```
03
```python
491
```
04
```python
190
```
05
```python
900
```
06
```python
000
```
07
08
09
10
11
88
89
90
```python
55
```
91
```python
110
```
92
```python
5
```
93
```python
20
```
94
95
96
97
98
```python
0
```
99
```python
1
```
I/O
Numbers in, numbers out.
CPU
Three registers; D does the work.
Memory
100 cells, 00 to 99.
Try it in the simulator:  faculty.runi.ac.il/vic/software/computer

## Slide 5: The data bus
The data bus
I/O
CPU
Memory
input
```python
55
```
```python
12
```
```python
171
```
```python
20
```
← next
output
```python
12
```
```python
67
```
instruction register
```python
900
```
data register (D)
```python
67
```
program counter
```python
0
```
00
```python
800
```
01
```python
490
```
02
```python
800
```
03
```python
491
```
04
```python
190
```
05
```python
900
```
06
```python
000
```
07
08
09
10
11
88
89
90
```python
55
```
91
```python
110
```
92
```python
5
```
93
```python
20
```
94
95
96
97
98
```python
0
```
99
```python
1
```
```python
read
```
```python
write
```
```python
load
```
```python
store
```

## Slide 6: The instruction set
The instruction set
I/O
CPU
Memory
input
```python
55
```
```python
12
```
```python
171
```
```python
20
```
← next
output
```python
12
```
```python
67
```
instruction register
```python
900
```
data register (D)
```python
67
```
program counter
```python
0
```
00
```python
800
```
01
```python
490
```
02
```python
800
```
03
```python
491
```
04
```python
190
```
05
```python
900
```
06
```python
000
```
07
08
09
10
11
88
89
90
```python
55
```
91
```python
110
```
92
```python
5
```
93
```python
20
```
94
95
96
97
98
```python
0
```
99
```python
1
```
symbolic
code
meaning
```python
read
```
```python
800
```
```python
D = input
```
```python
write
```
```python
900
```
```python
output = D
```
```python
load xx
```
```python
3xx
```
```python
D = M[xx]
```
```python
store xx
```
```python
4xx
```
```python
M[xx] = D
```
```python
add xx
```
```python
1xx
```
```python
D = D + M[xx]
```
```python
sub xx
```
```python
2xx
```
```python
D = D - M[xx]
```
D is the data register; M[xx] is memory cell xx.

## Slide 7: Read
Read
I/O
CPU
Memory
input
```python
55
```
```python
12
```
```python
171
```
```python
20
```
← next
output
```python
12
```
```python
67
```
instruction register
```python
900
```
data register (D)
```python
67
```
program counter
```python
0
```
00
```python
800
```
01
```python
490
```
02
```python
800
```
03
```python
491
```
04
```python
190
```
05
```python
900
```
06
```python
000
```
07
08
09
10
11
88
89
90
```python
55
```
91
```python
110
```
92
```python
5
```
93
```python
20
```
94
95
96
97
98
```python
0
```
99
```python
1
```
symbolic
code
meaning
```python
read
```
```python
800
```
```python
D = input
```
```python
write
```
```python
900
```
```python
output = D
```
```python
load xx
```
```python
3xx
```
```python
D = M[xx]
```
```python
store xx
```
```python
4xx
```
```python
M[xx] = D
```
```python
add xx
```
```python
1xx
```
```python
D = D + M[xx]
```
```python
sub xx
```
```python
2xx
```
```python
D = D - M[xx]
```
```python
800
```
```python
read
```
```python
171
```
← next
after it runs:  D = 171

## Slide 8: Write
Write
I/O
CPU
Memory
input
```python
55
```
```python
12
```
```python
171
```
```python
20
```
← next
output
```python
12
```
```python
67
```
instruction register
```python
800
```
data register (D)
```python
171
```
program counter
```python
0
```
00
```python
800
```
01
```python
490
```
02
```python
800
```
03
```python
491
```
04
```python
190
```
05
```python
900
```
06
```python
000
```
07
08
09
10
11
88
89
90
```python
55
```
91
```python
110
```
92
```python
5
```
93
```python
20
```
94
95
96
97
98
```python
0
```
99
```python
1
```
symbolic
code
meaning
```python
read
```
```python
800
```
```python
D = input
```
```python
write
```
```python
900
```
```python
output = D
```
```python
load xx
```
```python
3xx
```
```python
D = M[xx]
```
```python
store xx
```
```python
4xx
```
```python
M[xx] = D
```
```python
add xx
```
```python
1xx
```
```python
D = D + M[xx]
```
```python
sub xx
```
```python
2xx
```
```python
D = D - M[xx]
```
```python
900
```
```python
write
```
```python
171
```
after it runs:  output = 171

## Slide 9: Load
Load
I/O
CPU
Memory
input
```python
55
```
```python
12
```
```python
171
```
```python
20
```
← next
output
```python
12
```
```python
67
```
```python
171
```
instruction register
```python
900
```
data register (D)
```python
171
```
program counter
```python
0
```
00
```python
800
```
01
```python
490
```
02
```python
800
```
03
```python
491
```
04
```python
190
```
05
```python
900
```
06
```python
000
```
07
08
09
10
11
88
89
90
```python
55
```
91
```python
110
```
92
```python
5
```
93
```python
20
```
94
95
96
97
98
```python
0
```
99
```python
1
```
symbolic
code
meaning
```python
read
```
```python
800
```
```python
D = input
```
```python
write
```
```python
900
```
```python
output = D
```
```python
load xx
```
```python
3xx
```
```python
D = M[xx]
```
```python
store xx
```
```python
4xx
```
```python
M[xx] = D
```
```python
add xx
```
```python
1xx
```
```python
D = D + M[xx]
```
```python
sub xx
```
```python
2xx
```
```python
D = D - M[xx]
```
```python
390
```
```python
load 90
```
```python
55
```
after it runs:  D = 55

## Slide 10: Store
Store
I/O
CPU
Memory
input
```python
55
```
```python
12
```
```python
171
```
```python
20
```
← next
output
```python
12
```
```python
67
```
```python
171
```
instruction register
```python
900
```
data register (D)
```python
55
```
program counter
```python
0
```
00
```python
800
```
01
```python
490
```
02
```python
800
```
03
```python
491
```
04
```python
190
```
05
```python
900
```
06
```python
000
```
07
08
09
10
11
88
89
90
```python
55
```
91
```python
110
```
92
```python
5
```
93
```python
20
```
94
95
96
97
98
```python
0
```
99
```python
1
```
symbolic
code
meaning
```python
read
```
```python
800
```
```python
D = input
```
```python
write
```
```python
900
```
```python
output = D
```
```python
load xx
```
```python
3xx
```
```python
D = M[xx]
```
```python
store xx
```
```python
4xx
```
```python
M[xx] = D
```
```python
add xx
```
```python
1xx
```
```python
D = D + M[xx]
```
```python
sub xx
```
```python
2xx
```
```python
D = D - M[xx]
```
```python
491
```
```python
store 91
```
```python
55
```
after it runs:  M[91] = 55

## Slide 11: Add
Add
I/O
CPU
Memory
input
```python
55
```
```python
12
```
```python
171
```
```python
20
```
← next
output
```python
12
```
```python
67
```
```python
171
```
instruction register
```python
900
```
data register (D)
```python
55
```
program counter
```python
0
```
00
```python
800
```
01
```python
490
```
02
```python
800
```
03
```python
491
```
04
```python
190
```
05
```python
900
```
06
```python
000
```
07
08
09
10
11
88
89
90
```python
55
```
91
```python
55
```
92
```python
5
```
93
```python
20
```
94
95
96
97
98
```python
0
```
99
```python
1
```
symbolic
code
meaning
```python
read
```
```python
800
```
```python
D = input
```
```python
write
```
```python
900
```
```python
output = D
```
```python
load xx
```
```python
3xx
```
```python
D = M[xx]
```
```python
store xx
```
```python
4xx
```
```python
M[xx] = D
```
```python
add xx
```
```python
1xx
```
```python
D = D + M[xx]
```
```python
sub xx
```
```python
2xx
```
```python
D = D - M[xx]
```
```python
192
```
```python
add 92
```
```python
60
```
after it runs:  D = 60

## Slide 12: Subtract
Subtract
I/O
CPU
Memory
input
```python
55
```
```python
12
```
```python
171
```
```python
20
```
← next
output
```python
12
```
```python
67
```
```python
171
```
instruction register
```python
900
```
data register (D)
```python
60
```
program counter
```python
0
```
00
```python
800
```
01
```python
490
```
02
```python
800
```
03
```python
491
```
04
```python
190
```
05
```python
900
```
06
```python
000
```
07
08
09
10
11
88
89
90
```python
55
```
91
```python
55
```
92
```python
5
```
93
```python
20
```
94
95
96
97
98
```python
0
```
99
```python
1
```
symbolic
code
meaning
```python
read
```
```python
800
```
```python
D = input
```
```python
write
```
```python
900
```
```python
output = D
```
```python
load xx
```
```python
3xx
```
```python
D = M[xx]
```
```python
store xx
```
```python
4xx
```
```python
M[xx] = D
```
```python
add xx
```
```python
1xx
```
```python
D = D + M[xx]
```
```python
sub xx
```
```python
2xx
```
```python
D = D - M[xx]
```
```python
293
```
```python
sub 93
```
```python
40
```
after it runs:  D = 40

## Slide 13: Computer fundamentals: the plan
Computer fundamentals: the plan
Five parts today.
The Vic computer
Programming Vic
Fetch and execute
Translation
Vic and real computers

## Slide 14: High-level programming
High-level programming
Task: read two numbers and write their sum.
`add_two.py`
```python
x = int(input())
y = int(input())
print(x + y)
```
High level
In Python, without worrying how the machine does it.

## Slide 15: Low-level programming
Low-level programming
The same task, in terms of what the machine can do.
pseudocode
read a number
store it somewhere
read a number
store it somewhere
add the first number
write
stop
implement
```python
symbolic program
00  read
01  store 90
02  read
03  store 91
04  add 90
05  write
06  stop
```
translate
```python
executable code
00  800
01  490
02  800
03  491
04  190
05  900
06  000
```

## Slide 16: Loading and running a program
Loading and running a program
I/O
CPU
Memory
input
```python
5
```
```python
12
```
← next
output
instruction register
```python
0
```
data register (D)
```python
0
```
program counter
```python
0
```
00
```python
800
```
01
```python
490
```
02
```python
800
```
03
```python
491
```
04
```python
190
```
05
```python
900
```
06
```python
000
```
07
08
09
10
11
88
89
90
91
92
93
94
95
96
97
98
```python
0
```
99
```python
1
```
Loaded
The program sits in cells 00–06.
```python
5
```
```python
12
```
```python
17
```
```python
17
```
```python
6
```
After running
17 in the output; PC stopped at 6.

## Slide 17: Branching
Branching
By default, control flows down; a goto sends it elsewhere.
linear
command
command
command
command
command
command
command
command
command
branching
command
label a:
command
if condition: goto b
command
label b:
command
if condition: goto c
command
label c:
goto a

## Slide 18: Branching in Vic
Branching in Vic
Three branching instructions decide what runs next.
symbolic
code
meaning
```python
goto xx
```
```python
5xx
```
```python
goto xx
```
```python
gotoz xx
```
```python
6xx
```
```python
if D == 0: goto xx
```
```python
gotop xx
```
```python
7xx
```
```python
if D > 0: goto xx
```
```python
read and write until 0
0  read
1  gotoz 4
2  write
3  goto 0
4  stop
```
```python
executable
0  800
1  604
2  900
3  500
4  000
```

## Slide 19: Max of two numbers
Max of two numbers
Task: read two numbers and write the greater one.
```python
max2 (symbolic)
0  read
1  store x
2  read
3  store y
4  sub x
5  gotop YISMAX
6  load x
7  write
8  stop
9  load y
10  write
11  stop
```
symbolic
code
meaning
```python
goto xx
```
```python
5xx
```
```python
goto xx
```
```python
gotoz xx
```
```python
6xx
```
```python
if D == 0: goto xx
```
```python
gotop xx
```
```python
7xx
```
```python
if D > 0: goto xx
```
YISMAX is line 9
so gotop YISMAX becomes gotop 9.

## Slide 20: Max of two numbers, translated
Max of two numbers, translated
Variables get addresses from 90 onward: x is M[90], y is M[91].
```python
symbolic
0  read
1  store 90
2  read
3  store 91
4  sub 90
5  gotop 9
6  load 90
7  write
8  stop
9  load 91
10  write
11  stop
```
translate
```python
max2 (executable)
0  800
1  490
2  800
3  491
4  290
5  709
6  390
7  900
8  000
9  391
10  900
11  000
```

## Slide 21: Max of two numbers, running
Max of two numbers, running
I/O
CPU
Memory
input
```python
154
```
```python
38
```
← next
output
instruction register
```python
0
```
data register (D)
```python
0
```
program counter
```python
0
```
00
```python
800
```
01
```python
490
```
02
```python
800
```
03
```python
491
```
04
```python
290
```
05
```python
709
```
06
```python
390
```
07
```python
900
```
08
```python
000
```
09
```python
391
```
10
```python
900
```
11
```python
000
```
88
89
90
91
92
93
94
95
96
97
98
```python
0
```
99
```python
1
```
Loaded
max2 in cells 00–11; input 154, 38.
```python
154
```
```python
38
```
```python
154
```
```python
154
```
```python
8
```
After running
154 is written; it stopped at 8.

## Slide 22: Computer fundamentals: the plan
Computer fundamentals: the plan
Five parts today.
The Vic computer
Programming Vic
Fetch and execute
Translation
Vic and real computers

## Slide 23: The fetch-execute cycle
The fetch-execute cycle
the CPU, for ever:
PC = 0
fetch:
IR = M[PC]
if IR == 0: stop
if IR is 5xx, or
IR is 6xx and D == 0, or
IR is 7xx and D > 0:
PC = xx
else:
execute IR
PC = PC + 1
goto fetch
PC
Where the next instruction is.
IR
The instruction being executed.
D
The number being worked on.

## Slide 24: The Vic computer, complete
The Vic computer, complete
Ten instructions, three registers, 100 memory cells.
symbolic
code
meaning
```python
read
```
```python
800
```
```python
D = input
```
```python
write
```
```python
900
```
```python
output = D
```
```python
load xx
```
```python
3xx
```
```python
D = M[xx]
```
```python
store xx
```
```python
4xx
```
```python
M[xx] = D
```
```python
add xx
```
```python
1xx
```
```python
D = D + M[xx]
```
```python
sub xx
```
```python
2xx
```
```python
D = D - M[xx]
```
```python
goto xx
```
```python
5xx
```
```python
goto xx
```
```python
gotoz xx
```
```python
6xx
```
```python
if D == 0: goto xx
```
```python
gotop xx
```
```python
7xx
```
```python
if D > 0: goto xx
```
instruction
a 3-digit number
D
the data register
xx
a 2-digit address
M[xx]
the contents of cell xx

## Slide 25: Computer fundamentals: the plan
Computer fundamentals: the plan
Five parts today.
The Vic computer
Programming Vic
Fetch and execute
Translation
Vic and real computers

## Slide 26: Symbolic programming
Symbolic programming
Task: sum up a series of numbers that ends with a zero.
pseudocode
sum = 0
LOOP:
read x
if x == 0: goto END
sum = sum + x
goto LOOP
END:
write sum
stop
write
```python
sum.asm
  load zero
  store sum
LOOP:
  read
  store x
  gotoz END
  load sum
  add x
  store sum
  goto LOOP
END:
  load sum
  write
  stop
```

## Slide 27: Program translation
Program translation
Number the lines, build a symbol table, look it all up.
```python
sum.asm, numbered
0  load zero
1  store sum
   LOOP:
2  read
3  store x
4  gotoz END
5  load sum
6  add x
7  store sum
8  goto LOOP
   END:
9  load sum
10  write
11  stop
```
```python
symbol table
zero  98
one   99
sum   90
x     91
LOOP   2
END    9
```
translate
```python
sum.vic
0  398
1  490
2  800
3  491
4  609
5  390
6  191
7  490
8  502
9  390
10  900
11  000
```

## Slide 28: Why symbolic code
Why symbolic code
Easier: to write, read, debug and maintain than numbers
Mechanical: translation follows fixed rules
Automatic: a program can do it: an assembler

## Slide 29: From source to executable
From source to executable
Write in an editor; an assembler produces the executable.
editor
a person writes
```python
sum.asm
symbolic code
```
assembler
a program translates
```python
sum.vic
executable code
```
Vic computer
loads and runs it
tinted boxes are files; the others do the work

## Slide 30: The Vic assembler
The Vic assembler
1. Load
an .asm file into the left box.
2. Translate
the executable code appears on the right.
3. Save
the .vic file, and load it into Vic.
faculty.runi.ac.il/vic/software/compilation/assembler

## Slide 31: A real example: C to RISC-V
A real example: C to RISC-V
A C compiler does the same for a real processor.
```python
a C program
int main() {
    int image[4][4];
    for (int i = 0; i < 4; ++i)
        for (int j = 0; j < 4; ++j)
            image[i][j] = rand();
    return 0;
}
```
```python
RISC-V:  address · instruction (hex) · symbolic
  d0:  ff010113   addi  sp,sp,-16
  d4:  00812423   sw    s0,8(sp)
  d8:  00112623   sw    ra,12(sp)
  dc:  00400413   li    s0,4
  e0:  00000097   auipc ra,0x0
  e4:  054080e7   jalr  84(ra)
  ...
 104:  fc041ee3   bnez  s0,e0
 108:  00c12083   lw    ra,12(sp)
 118:  00008067   ret
```

## Slide 32: Computer fundamentals: the plan
Computer fundamentals: the plan
Five parts today.
The Vic computer
Programming Vic
Fetch and execute
Translation
Vic and real computers

## Slide 33: From Vic to the real thing
From Vic to the real thing
How Vic compares to a real computer.
Vic
a typical computer
1 data register
32 data registers
3-digit words
64-bit words
100 memory cells
billions of memory cells
1 memory unit
RAM, ROM, cache
no secondary storage
disk
1 input unit
keyboard, mouse, disk, network
1 output unit
screen, speakers, disk, network
10 instructions
100–300 instructions
1 program
many programs at once
1 instruction per cycle
parallel processing
Same design, bigger.
Each one is an extension of Vic.

## Slide 34: The basic model
The basic model
All computers are variations of this basic model.
bus
input device
output device
processor
main memory
(short term)
external memory
(long term)

## Slide 35: A real computer
A real computer
The same model, with more of each part.
I/O devices
keyboard, mouse, scanner
screen, speakers, printer
network interface card
Processing
several processors
cache memory beside each
one bus connecting it all
Main memory
system programs
several apps at once
parts of files, paged in
External storage
hard disks
memory sticks
the network

## Slide 36: Abstraction
Abstraction
Computer science: logical operations
Electrical engineering: physical implementation
Vic: a simplified model

## Slide 37: Computer fundamentals in one slide
Computer fundamentals in one slide
The machine
Input, output, CPU, memory
D, IR, PC registers
Everything passes through D
Instructions
Each is a 3-digit number
First digit: what to do
Last two: which cell
Control
Fetch, then execute, for ever
goto, gotoz, gotop jump
000 stops
Translation
Symbolic code for people
Symbol table: names to addresses
An assembler does it for us
