# Lecture 11-1: Writing classes (week 11)

## Slide 1: Writing Classes
self
PYTHON COURSE · WEEK 10 · LECTURE 1
Writing Classes
Implementing classes
Reichman University

## Slide 2: Two views of a class
Two views of a class
Client view: how to use the class (last lecture)
Class view: how to write the class (today)
The API: what connects them, the same on both sides

## Slide 3: Three classes, written from inside
Three classes, written from inside
Three parts today.
```python
BankAccount
```
```python
Fraction
```
```python
Point
```

## Slide 4: Bank accounts: requirements
Bank accounts: requirements
What to record becomes attributes; what to do becomes methods.
Things to record
account id
owner
balance
Things to do
open a new account
display it
deposit money
withdraw money
transfer to another account
→ attributes
→ methods

## Slide 5: A class and its constructor
A class and its constructor
`bank_account.py`
```python
class BankAccount:
    """A bank account: an id, an owner and a balance.
    The methods perform no input checks."""

    _next_id = 1         # shared by all accounts

    def __init__(self, owner, balance=0):
        """A new account; ids run 1, 2, 3, ..."""
        self._id = BankAccount._next_id
        BankAccount._next_id += 1
        self._owner = owner
        self._balance = balance
```
lines 4–15 of “week 10 code / bank_account.py”.
_next_id
One counter for the whole class.
__init__
Runs on every BankAccount(...).
self
The new object being set up.

## Slide 6: Inside BankAccount("Alice")
Inside BankAccount("Alice")
the class BankAccount
```python
_next_id
```
```python
2
```
the new object (self)
```python
_id
```
```python
1
```
```python
_owner
```
```python
'Alice'
```
```python
_balance
```
```python
0
```
1. Make
Python creates an empty BankAccount object.
2. Call
__init__(self, "Alice"), with balance = 0.
3. Set
self._id, self._owner, self._balance.
4. Refer
alice now refers to the object.
```python
alice
```

## Slide 7: One counter for all accounts
One counter for all accounts
```python
python class_attribute.py
1 2 3
next id: 4
```
`class_attribute.py`
```python
from bank_account import BankAccount

a = BankAccount("Ron", 1000)
b = BankAccount("Lisa", 500)
c = BankAccount("Mike", 750)
print(a.get_id(), b.get_id(), c.get_id())
print("next id:", BankAccount._next_id)
```
[LIVE] the file is in “week 10 code / class_attribute.py”.

## Slide 8: Methods: __str__ and getters
Methods: __str__ and getters
`bank_account.py`
```python
    def __str__(self):
        """The id, owner and balance, as one line."""
        return (f"{self._id} {self._owner} "
                f"{self._balance}")

    def get_id(self):
        return self._id

    def get_owner(self):
        return self._owner

    def get_balance(self):
        return self._balance
```
lines 17–29 of “week 10 code / bank_account.py”.
self first
Every method gets its object.
__str__
Returns text for print.
get_...
Read access, nothing more.

## Slide 9: Methods that change the object
Methods that change the object
`bank_account.py`
```python
    def deposit(self, amount):
        """Adds amount to this account."""
        self._balance += amount

    def withdraw(self, amount):
        """Takes amount out of this account."""
        self._balance -= amount

    def transfer_to(self, other, amount):
        """Moves amount from this account to other."""
        self.withdraw(amount)
        other.deposit(amount)
```
lines 31–42 of “week 10 code / bank_account.py”.
+= and -=
Change this account only.
other
A second account, passed in.
Reuse
transfer_to calls the others.

## Slide 10: What self is
What self is
```python
python self_demo.py
200
```
`self_demo.py`
```python
from bank_account import BankAccount

alice = BankAccount("Alice")
alice.deposit(100)
BankAccount.deposit(alice, 100)    # the same call
print(alice.get_balance())
```
[LIVE] the file is in “week 10 code / self_demo.py”.

## Slide 11: Python has no private attributes
Python has no private attributes
```python
python unsafe_client.py
1 Mallory 1000000
```
`unsafe_client.py`
```python
from bank_account import BankAccount

acc = BankAccount("Mallory", 100)
acc._balance = 1_000_000     # Python allows it...
print(acc)                   # ...and the bank pays
```
[LIVE] the file is in “week 10 code / unsafe_client.py”.

## Slide 12: The underscore convention
The underscore convention
_balance: means internal, so clients do not touch it
A convention: Python trusts the client to respect it
The API: balances change only via deposit and withdraw
Benefit: checks can be added in one place

## Slide 13: Class design: the usual parts
Class design: the usual parts
Constructor
__init__
Sets every attribute
Defaults instead of overloading
__str__
Text for print
Useful for debugging
Getters
Read access to data
Only what clients need
Domain methods
deposit, withdraw, transfer_to
The language of the domain

## Slide 14: Three classes, written from inside
Three classes, written from inside
Three parts today.
```python
BankAccount
```
```python
Fraction
```
```python
Point
```

## Slide 15: The Fraction constructor
The Fraction constructor
`fraction.py`
```python
class Fraction:
    """A signed fraction, like 2/3 or -1/5, kept
    reduced, with the sign in the numerator."""

    def __init__(self, numerator, denominator):
        """A reduced fraction: (6, -9) gives -2/3."""
        if denominator < 0:    # sign goes on top
            numerator = -numerator
            denominator = -denominator
        g = gcd(abs(numerator), denominator)
        self.numerator = numerator // g
        self.denominator = denominator // g
```
lines 11–22 of “week 10 code / fraction.py”.
Sign
Moves to the numerator.
gcd
Divides both: reduced.
//
Integer division: ints stay ints.

## Slide 16: Fraction(6, -9), step by step
Fraction(6, -9), step by step
start
```python
(6, -9)
```
sign on top
```python
(-6, 9)
```
gcd(6, 9)
```python
3
```
divide by 3
```python
-2/3
```
`fraction.py`
```python
def gcd(x, y):
    """GCD of x and y, by Euclid's algorithm."""
    while y != 0:
        x, y = y, x % y
    return x
```
lines 4–8 of “week 10 code / fraction.py”.

## Slide 17: Printing and adding
Printing and adding
`fraction.py`
```python
    def __str__(self):
        """As "n/d", or just "n" for whole numbers."""
        if self.denominator == 1:
            return str(self.numerator)
        return f"{self.numerator}/{self.denominator}"

    def add(self, other):
        """Returns this fraction plus other."""
        n = (self.numerator * other.denominator
             + other.numerator * self.denominator)
        d = self.denominator * other.denominator
        return Fraction(n, d)
```
lines 24–35 of “week 10 code / fraction.py”.
__str__
2/1 prints as 2.
other.numerator
The other fraction's data.
Fraction(n, d)
New; __init__ reduces it.

## Slide 18: 1/3 + 3/7, inside add
1/3 + 3/7, inside add
a.add(b), with self = 1/3 and other = 3/7
```python
n
```
```python
1 · 7  +  3 · 3  =  16
```
```python
d
```
```python
3 · 7  =  21
```
```python
result
```
```python
Fraction(16, 21)  →  16/21
```

## Slide 19: multiply, invert, divide
multiply, invert, divide
`fraction.py`
```python
    def multiply(self, other):
        """Returns this fraction times other."""
        n = self.numerator * other.numerator
        d = self.denominator * other.denominator
        return Fraction(n, d)

    def invert(self):
        """Returns 1 divided by this fraction."""
        return Fraction(self.denominator,
                        self.numerator)

    def divide(self, other):
        """Returns this fraction divided by other."""
        return self.multiply(other.invert())
```
lines 37–50 of “week 10 code / fraction.py”.
multiply
The same pattern as add.
invert
Swaps the two numbers.
divide
Multiplies by the inverse.

## Slide 20: Three classes, written from inside
Three classes, written from inside
Three parts today.
```python
BankAccount
```
```python
Fraction
```
```python
Point
```

## Slide 21: Point: data and printing
Point: data and printing
`point.py`
```python
class Point:
    """A point in the plane: coordinates x and y."""

    def __init__(self, x, y):
        """Constructs the point (x, y)."""
        self.x = x
        self.y = y

    def __str__(self):
        """The point as "(x, y)"."""
        return f"({self.x}, {self.y})"
```
lines 5–15 of “week 10 code / point.py”.

## Slide 22: Point: methods
Point: methods
```python
python point_demo.py
(1, 2) (4, 6)
5.0
(5, 8)
```
`point.py`
```python
    def add(self, other):
        """The vector sum of this point and other."""
        return Point(self.x + other.x,
                     self.y + other.y)

    def distance_to(self, other):
        """The straight-line distance to other."""
        dx = self.x - other.x
        dy = self.y - other.y
        return math.sqrt(dx * dx + dy * dy)
```
lines 17–26 of “week 10 code / point.py”.

## Slide 23: Procedural and object-oriented
Procedural and object-oriented
Python programs mix both styles; choose by what the code is about.
Procedural
A module is a library of functions
Data passed in as arguments
add(m1, m2) from week 5
Object-oriented
A class represents a kind of thing
Methods work on self and arguments
a.add(b) from this week

## Slide 24: Writing classes in one slide
Writing classes in one slide
A class
class Name:
Methods are defs inside it
self is the object
Constructor
__init__ sets attributes
Called by Name(...)
Defaults, not overloading
Attributes
self.x: one per object
Name.x: one per class
_x: internal, hands off
Methods
__str__ for print
Getters to read
Return new objects, or mutate
