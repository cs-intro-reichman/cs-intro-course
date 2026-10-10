# Lecture 3-2: Approximation algorithms (week 3)

## Slide 1: Approximation Algorithms
√
PYTHON COURSE · WEEK 4 · LECTURE 1
Approximation Algorithms
Computing approximate answers
Reichman University

## Slide 2: Why approximate?
Why approximate?
Some answers cannot be computed exactly.
Square roots: √2 = 1.41421356…, with endless digits
Equations: x = cos(x) has a solution, but no formula for it
Floats: a fixed number of digits, so results are rounded

## Slide 3: What “close enough” means
What “close enough” means
Guess: g, the current estimate
Tolerance: ε, the allowed error
Stopping rule: stop when |g · g − x| < ε
The answer: a number g with g · g close to x

## Slide 4: The problem
The problem
Input and output.
Input: a number x ≥ 0, and a tolerance ε > 0
Output: a number g such that |g · g − x| < ε

## Slide 5: Three algorithms, one problem
Three algorithms, one problem
Same problem, three methods, different running times.
Sequential search
try every candidate
Bisection
halve the interval
Newton–Raphson
follow the tangent
From about 30,000 steps down to 3.

## Slide 6: Sequential search
Sequential search
Goal: find √16. Try g = 1.0, 1.25, 1.5, … until g · g is close to 16.
1.0
2.0
3.0
4.0
start: g = 1.0
stop when |g · g − 16| < ε
Every step costs one multiplication and one comparison.

## Slide 7: Sequential search: the idea
Sequential search: the idea
In pseudocode
set g to 1.0
while g · g is not close enough:
increase g by increment
report g
Two parameters
epsilon: how close is close enough
increment: how big a step to take

The rest of the algorithm is fixed.

## Slide 8: Sequential search: the program
Sequential search: the program
```python
python sqrt_sequential.py
3.9988 in 29988 steps
```
`sqrt_sequential.py`
```python
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
```
[LIVE] the file is in “week 4 code / sqrt_sequential.py”.

## Slide 9: Reading the loop
Reading the loop
`sqrt_sequential.py`
```python
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
```
epsilon
The allowed error (accuracy).
increment
The step size (speed).
The condition
Loop while the error is too big.

## Slide 10: Sequential search: running time
Sequential search: running time
Accuracy: smaller ε, more accurate answer
Speed: smaller increment, slower program
Cost: fewer than x / increment iterations
In numbers: x = 16 → 29,988 steps; x = 105 → 92,465

## Slide 11: Sequential search: a bug
Sequential search: a bug
Big increment: g jumps past the answer
Infinite loop: the condition stays true forever
The fix: stop once g has passed x
This bug is hard to find.
The program does not crash and prints nothing wrong. It just never stops, and no line is marked as the error.

## Slide 12: Sequential search: bug fixed
Sequential search: bug fixed
`sqrt_sequential_fixed.py`
```python
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
```
[LIVE] the file is in “week 4 code / sqrt_sequential_fixed.py”.

## Slide 13: Three algorithms, one problem
Three algorithms, one problem
Same problem, three methods, different running times.
Sequential search
try every candidate
Bisection
halve the interval
Newton–Raphson
follow the tangent
From about 30,000 steps down to 3.

## Slide 14: Bisection search
Bisection search
Split the interval in two; keep the half that contains the answer.
g = 8.5
itr 0
g = 4.75
itr 1
g = 2.875
itr 2
the answer, 4
Each step halves the interval.

## Slide 15: Bisection: the idea
Bisection: the idea
In pseudocode
set low to 1.0 and high to x
set g to the midpoint
while g · g is not close enough:
too small? move low up to g
too big? move high down to g
set g to the new midpoint
report g
An assumption
We need two numbers that the answer lies between.

For x ≥ 1, √x is between 1 and x.

For x < 1 this does not hold (an exercise).

## Slide 16: Bisection: the program
Bisection: the program
```python
python sqrt_bisection.py
3.9993 in 11 steps
```
`sqrt_bisection.py`
```python
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
```
[LIVE] the file is in “week 4 code / sqrt_bisection.py”.

## Slide 17: Bisection: running time
Bisection: running time
Each iteration halves the search interval.
iteration 0   space = x
iteration 1   space = x / 2
iteration 2   space = x / 4
iteration 3   space = x / 8
iteration k   space = x / 2ᵏ
So k is about log₂(x / ε).
For x = 16 and ε = 0.01: 11 steps. For an x 100 times bigger: about 7 more steps.

## Slide 18: Three algorithms, one problem
Three algorithms, one problem
Same problem, three methods, different running times.
Sequential search
try every candidate
Bisection
halve the interval
Newton–Raphson
follow the tangent
From about 30,000 steps down to 3.

## Slide 19: Newton–Raphson: the idea
Newton–Raphson: the idea
Follow tangent lines down to the solution of f(g) = 0.
g
f(g) = g · g − 16
g₀ = 8
g₁ = 5
g₂ = 4.1
Isaac Newton
(1643–1727)

## Slide 20: Newton–Raphson: convergence
Newton–Raphson: convergence
Every step roughly squares the error.
x = 16, first guess 8
step 0: g = 8,  err 48
step 1: g = 5,  err 9
step 2: g = 4.1,  err 0.81
step 3: g = 4.0012,  err 0.0098
3 steps.
Sequential search needed 29,988 steps and bisection 11, for the same x and ε.

## Slide 21: Newton–Raphson: the formula
Newton–Raphson: the formula
The rule: if g is near a solution of f(x) = 0, g − f(g) / f′(g) is nearer
For √x: f(g) = g · g − x, so f′(g) = 2 · g
The next guess: g − (g · g − x) / (2 · g)
Calculus: the derivative, tangent, convergence and limit grew out of such questions

## Slide 22: Newton–Raphson: why the formula works
Newton–Raphson: why the formula works
The next guess is where the tangent line crosses zero.
The tangent line at gₙ:
L(g) = f(gₙ) + f′(gₙ) · (g − gₙ)

The next guess gₙ₊₁ is where L is 0:
0 = f(gₙ) + f′(gₙ) · (gₙ₊₁ − gₙ)

Solve for gₙ₊₁:
gₙ₊₁ = gₙ − f(gₙ) / f′(gₙ)
gₙ
gₙ₊₁
(gₙ, f(gₙ))

## Slide 23: Newton–Raphson: an example
Newton–Raphson: an example
Find √719, the same as solving x · x − 719 = 0.
The rule for √719
f(x) = x · x − 719
f′(x) = 2 · x

If g is close to √719, then
g − (g · g − 719) / (2 · g)
is closer.
Algorithm
ε = 0.01
g = 719 / 2
while |g · g − 719| > ε:
g = g − (g · g − 719) / (2 · g)
report g

## Slide 24: Newton–Raphson: the program
Newton–Raphson: the program
```python
python sqrt_newton.py
step 1: 5.0
step 2: 4.1
step 3: 4.001219512195122
4.0012 in 3 steps
```
`sqrt_newton.py`
```python
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
```
[LIVE] the file is in “week 4 code / sqrt_newton.py”.
```python
with x = 105
step 1: 27.25
step 2: 15.551605504587156
step 3: 11.151659989960418
step 4: 10.283649283522411
step 5: 10.247016247636102
10.247 in 5 steps
```

## Slide 25: Three algorithms compared
Three algorithms compared
Same problem, same ε.
Sequential search
Works for any function
Steps up by a fixed increment
Needs nothing but arithmetic
About x / increment steps (linear)
x = 16 → 29,988 steps
Hangs if increment is too large
Bisection
Works for monotonic functions
Halves an interval holding the answer
Needs a bracket to start from
About log₂(x / ε) steps (logarithmic)
x = 16 → 11 steps
Always finishes
Newton–Raphson
Works for continuous, differentiable functions
Follows the tangent to the next guess
Needs the slope of the function
Squares the error each step (the fastest)
x = 16 → 3 steps
A bad first guess can fail

## Slide 26: Beyond square roots
Beyond square roots
Root finding: all three solve f(x) = 0
The pattern: guess, measure error, improve, stop
The trade-off: more assumptions, fewer steps
Used in: optimization, machine learning, graphics, simulation
