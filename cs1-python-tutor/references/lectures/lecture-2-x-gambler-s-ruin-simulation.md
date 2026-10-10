# Lecture 2-x: Gambler's ruin (simulation) (week 2)

## Slide 1
Gambler's ruin
Program flow
Conditionals
Loops
Examples
Gambler's ruin
Every flip wins $1 or loses $1. Start at $50, aim for $250.
Same rules, completely different histories. The game ends at $0 or at $250.

## Slide 2
Monte Carlo simulation
The strategy
Flip a coin and see what happens. Repeat many times. Compute statistics.
Why it matters
Used across science, engineering, finance and game design — and often the only tool available when a problem has no formula.
We are not computing an answer. We are estimating one, and the estimate differs every run. That is not a bug.
Seventy games at once — about one in five reaches the goal.

## Slide 3
The simulation in Python
`one_game.py`
```python
cash = start
while 0 < cash < goal:
    if random.random() < 0.5:
        cash += 1
    else:
        cash -= 1
    n_flips += 1
```
`many_games.py`
```python
t = 0
while t < T:
    cash = start
    # ... one game ...
    if cash == goal:
        n_wins += 1
    t += 1
```
We cannot know how many flips — an indefinite loop.
We know exactly how many games — a counted loop.

## Slide 4
Running it
```python
terminal
```
```python
Percentage of winning games: 21.1 %
Average flips per game: 9808.0
```
parameters | coin flips | how long it takes
$50 / $250 / 1000 games | 10 million | under a second
$500 / $2500 / 1000 games | 1 billion | about two minutes
The numbers change every run
That is what estimating looks like. Run it three times and watch the percentage move by a point or two.
Knowing roughly how many operations you are asking for is part of the job — week 8 makes that idea formal.

## Slide 5
Theory and experiment
What the mathematics says
Probability of reaching the goal = start / goal = 50 / 250 = 20%. Expected number of flips = start × (goal − start) = 50 × 200 = 10,000.
What the simulation found
21.1% of games reached the goal, over 9,808 flips per game on average.
The program knew none of that mathematics. It arrived at the same place by flipping coins.
So why simulate, if the formula already answers it?
To validate a theory, or to help reach one. To generate events from a model, for research, training, investing or games. And because in many cases there is no formula at all, and simulation is the only way to get data.
Change 0.5 to 0.49 — a slightly unfair coin — and the mathematics gets much harder. The simulation needs a two-character edit.
