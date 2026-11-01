# HW3: Loans and anagrams

Given after week 3.

**Material for this assignment: weeks 1 to 3 only** (lectures 1-1, 1-2, 2-1, 2-2, 3-1, 3-2; recitations 1, 2, 3, and the code files of those weeks). Solve it, hint toward it and point to slides using only this material and the Python listed for weeks 1 to 3 in `python-taught.md`, even if the student is already in a later week. Don't suggest or point to anything from week 4 on.

**This is graded work: guide with the hint ladder, never give solution code.**

# Assignment statement

## From `Introduction to CS - Homework 3.docx`

## Introduction to CS: Homework 3
### Getting started
In this assignment you write, test and submit four programs. Programs 1 and 2 use the approximation algorithms of lecture 3-2 on a real problem: paying back a loan. Programs 3 and 4 practise the strings of lecture 3-1.
Rule: use only what lectures 1-1 to 3-2 teach. In particular, don't define functions (def, lecture 4-1), don't use lists, and don't use sorted, split, join, min, max or random.randint. The tester checks this.
Get the code for this assignment from the course's Moodle page (the file HW3.zip), unzip it, and open the HW3 folder in VS Code. It contains:
- end_balance.py, loan_calc.py, anagram.py, random_anagram.py: the four programs, to complete
- loan calc.xlsx: a spreadsheet for Part A
- test_hw3.py: a tester that checks your programs (see Testing your programs)
Rules for all four programs:
- Input. Read each input with input(), one value per line, in the order the program description gives. Use input() with no prompt message.
- Output. Print exactly the text shown in the examples, the same words, spaces and punctuation.
- No input checks. You can assume that the inputs are valid, as the program description says.
### Part A: Loan calculations (50 points)
Suppose you take a loan of 100,000 shekels at a yearly interest rate of 5%, for 10 years, with equal yearly payments. How much should you pay each year, so that at the end of the 10th year the loan is fully paid?
Say you pay 10,000 shekels a year. At the end of the first year you still owe (100,000 − 10,000) × 1.05 = 94,500. At the end of the second year you owe (94,500 − 10,000) × 1.05 = 88,725. With n equal payments, we repeat this calculation n times and look at the balance at the end. The spreadsheet loan calc.xlsx does exactly this:

If the ending balance is positive, you still owe money so the payment is too low. If it is negative, you paid too much.
Start by playing with the spreadsheet, open it in Excel or Google Sheets and try different payments until the ending balance is close to zero, say a few shekels. That payment is the answer.
Isn't there a formula for this? There is. But building a model and searching for the answer gives a good understanding of the problem, and many financial and scientific problems have no formula at all. They are solved this way, with a model and a search.
### 1. EndBalance (15 points)
The program end_balance.py does what the spreadsheet does. It reads four inputs: the loan, the yearly interest rate in percent, the number of payments n, and the yearly payment. It prints the balance at the end of the n-th year, rounded to 2 decimal places:
```python
% python end_balance.py
100000
5
10
10000
Ending balance: 30821.59
```

```python
% python end_balance.py
100000
5
2
10000
Ending balance: 88725.0
```
Implementation notes:
- Use a loop that repeats the spreadsheet's calculation n times. A rate of 5 percent means multiplying by 1 + 5 / 100.
- Round with round(balance, 2) (lecture 1-2).
- Compare your results with the spreadsheet for a few payments.
### 2. LoanCalc (35 points)
Now the real question: which payment brings the ending balance close to zero? Call the ending balance for a payment x f(x); the loan, the rate and n stay fixed. We want an x for which f(x) is close to 0. Note that f is decreasing: the more you pay each year, the less you owe at the end. Lecture 3-2 showed two ways to solve such a problem: sequential search and bisection search.
The program loan_calc.py reads three inputs (the loan, the interest rate in percent, and n) and finds the payment both ways, to the nearest agora (0.01 shekels). It prints the payment as a whole number, with int(), and the number of steps each search took:
```python
% python loan_calc.py
100000
5
10
Loan = 100000.0, interest rate = 5.0%, periods = 10
Payment by sequential search: 12333, in 233377 steps
Payment by bisection search: 12333, in 24 steps
```
Sequential search. Start with a payment g for which you know that f(g) > 0. Then add a small increment, 0.01 shekels, to g, again and again, until f(g) is no longer positive. That g is the answer: the true solution lies less than one increment below it. In the picture, the guesses are x0, x1, x2, …:

Bisection search. Keep a low value and a high value with the answer between them, and a guess g halfway between. In each step, compute f(g): if it is positive, g is too low, so the answer is between g and high; otherwise it is between low and g. Move low or high to g, and set g to the new middle. Stop when high − low is at most ε = 0.01 shekels.
Implementation notes:
- Where to start. Paying loan / n a year pays back the loan without any interest, so the ending balance is surely positive: a good first guess for sequential search, and a good low value for bisection. Paying the whole loan in each year is surely too much: a good high value.
- Computing f. Each search needs the ending balance for many different payments. Put the loop from program 1 inside each search loop: a loop inside a loop. (In lecture 4-1 we will learn to write it once, as a function.)
- Counting steps. In sequential search, count each time g grows by the increment. In bisection search, count each time the interval is halved. The tester allows a difference of 1.
- The first line prints the inputs. Read the loan and the rate with float(), so that they print as 100000.0 and 5.0.
- Try a bigger loan or more years, and compare the time the two searches take.
### Part B: Anagrams (50 points)
Two programs about anagrams. Program 3 checks whether two phrases are anagrams, and program 4 makes a random one.
### 3. Anagram (30 points)
Two words or phrases are anagrams of each other if they use exactly the same letters, each one the same number of times, only in a different order. For example, "listen" and "silent" are anagrams: both use the letters l, i, s, t, e and n, once each. So are "evil" and "vile".
"aab" and "abb" are not anagrams: both use the letters a and b, but "aab" has two a's and "abb" has only one.
For phrases, we ignore spaces, punctuation and upper or lower case, as we did for palindromes in lecture 3-1. So "William Shakespeare" and "I am a weakish speller" are anagrams: write down the letters of each, and you get the same letters, the same number of times.
The program anagram.py reads two phrases. It prints each phrase with only its letters kept, all in lower case, and then True if the two are anagrams and False if not:
```python
% python anagram.py
William Shakespeare
I am a weakish speller
williamshakespeare
iamaweakishspeller
True
```

```python
% python anagram.py
hello
world
hello
world
False
```
Implementation notes:
- Clean each phrase first. Build a new string with a loop over the characters, keeping only letters (isalpha) and converting them with lower (lecture 3-1).
- Then compare the two cleaned strings. One way: for each letter of the first, find it in the second (you can use the find method of str) and remove it from there with slicing, so it cannot be used twice. If a letter is not found, they are not anagrams. Another way uses count. Either way, think about what happens when the lengths differ.
- Test with "Madam Curie" and "Radium came", with "Tom Marvolo Riddle" and "I am Lord Voldemort", and with pairs that are almost anagrams, like "aab" and "abb".
### 4. RandomAnagram (20 points)
The program random_anagram.py reads a word and prints its letters in a random order. The result is usually not an English word; it only has to use every letter of the input exactly once. Three runs:
```python
% python random_anagram.py
silent
ltnsei
```

```python
% python random_anagram.py
silent
enltsi
```

```python
% python random_anagram.py
silent
silten
```
Implementation notes:
- One way: repeatedly pick a random position in the word, add the letter there to the result, and remove it from the word, until the word is empty.
- A random position from 0 to len(word) - 1 is int(random.random() * len(word)) (lecture 1-2). Removing the letter at position i is a job for slicing.
- Check your results with your Anagram program.
### Testing your programs
First test each program yourself, with the examples above and with inputs of your own. Then run the tester, from the HW3 folder:
```python
% python test_hw3.py
```
It checks the rules, runs each program on several inputs and prints PASS or FAIL for each test; for a FAIL it shows the expected output and yours. Passing all the tests doesn't guarantee full points: the graders run other inputs too, and they read your code.
### Submission
Before you submit, make sure your code follows the course's coding style guidelines. Submit on the course's Moodle page, in the Homework 3 assignment. Upload these files only:
```python
end_balance.py
loan_calc.py
anagram.py
random_anagram.py
```

## From `end_balance.py`

### `end_balance.py`
```python
# Homework 3, program 1: EndBalance
# Prints the balance of a loan at the end of its last period.
# Input: the loan, the interest rate in percent, the number of periods n,
# and the periodical payment, each on its own line.

# Write your code here.
```

## From `loan_calc.py`

### `loan_calc.py`
```python
# Homework 3, program 2: LoanCalc
# Finds the periodical payment that pays off a loan, by sequential search
# and by bisection search.
# Input: the loan, the interest rate in percent, and the number of periods n,
# each on its own line.

increment = 0.01         # sequential search: the step, one agora
epsilon = 0.01           # bisection search: the accuracy, one agora

# Write your code here.
```

## From `anagram.py`

### `anagram.py`
```python
# Homework 3, program 3: Anagram
# Checks whether two phrases are anagrams of each other.
# Input: two phrases, each on its own line.

# Write your code here.
```

## From `random_anagram.py`

### `random_anagram.py`
```python
# Homework 3, program 4: RandomAnagram
# Prints the letters of a word in a random order.
# Input: a word.
import random

# Write your code here.
```


# Instructor's notes for the tutor (guidance only: do not quote these to the student as an answer)

# HW3 notes for the tutor

Given after week 3 (lectures 3-1 Strings and 3-2 Approximation). Students may use everything up to
lecture 3-2: loops, if, strings (indexing, slicing, `in`, `len`, methods such as lower, upper, isalpha,
find, count, replace), and sequential and bisection search. Not allowed yet (the tester checks):
defining functions, lists, `sorted`, `split`, `join`, `min`, `max`, `sum`, `random.randint`.
Input is read with `input()`, one value per line, no prompt. Give hints, not code.

## 1. EndBalance
Concepts: a counted loop that repeats the spreadsheet's calculation, percent as a fraction, round.
Hint ladder: compute the first two years by hand (94,500 and 88,725); compare with the spreadsheet row
by row; check the order of subtracting the payment and adding the interest.

## 2. LoanCalc
Concepts: sequential search and bisection search from lecture 3-2, applied to "ending balance = 0";
a loop inside a loop.
Hint ladder: get program 1 right first; ask which payment is surely too low and which surely too high;
ask what the balance loop must start from each time a new payment is tried; for bisection, ask what a
positive ending balance says about the guess.
Usual problems: the balance is not reset before each try; the wrong end of the interval moves; using
round instead of int for the printed payment.

## 3. Anagram
Concepts: building a string with the accumulator pattern, isalpha and lower, find and slicing (or count).
Hint ladder: first make the cleaned strings print correctly; then ask how to make sure each letter is
used only once; test with "aab" and "abb", and with strings of different lengths.
Usual problems: a check that accepts "aab"/"abb"; no length check.

## 4. RandomAnagram
Concepts: a random position with int(random.random() * n) (lecture 1-2), slicing to remove a character,
a while loop until the string is empty.
Hint ladder: what must happen to the word after a letter is picked? what range of positions is possible?
Usual problems: letters repeat or go missing; the last letter is never picked.
