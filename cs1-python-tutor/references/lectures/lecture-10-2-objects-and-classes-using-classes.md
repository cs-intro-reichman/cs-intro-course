# Lecture 10-2: Objects and classes (using classes) (week 10)

## Slide 1: Objects and Classes
a.b
PYTHON COURSE · WEEK 9 · LECTURE 1
Objects and Classes
Using someone else's classes
Reichman University

## Slide 2: New types
New types
Programs often need types that Python does not have.
Fraction: numbers like 1/2, 1/3, 5/6, exactly
Point: pairs of numbers, like (3, 5)
BankAccount: an id, an owner and a balance
Date, Color, ...: and many more

## Slide 3: Objects and classes
Objects and classes
Class: a type, saying what its values hold and can do
Object: one value of a class, also called an instance
Method: a function that works on an object, like s.upper()
OOP: programming with classes and objects

## Slide 4: One class, many objects
One class, many objects
Each fraction is an object; Fraction is their class.
Fraction
numerator, denominator
a Fraction
```python
numerator
```
```python
2
```
```python
denominator
```
```python
5
```
a Fraction
```python
numerator
```
```python
1
```
```python
denominator
```
```python
3
```
a Fraction
```python
numerator
```
```python
-7
```
```python
denominator
```
```python
19
```
the class
objects

## Slide 5: Three classes, used as a client
Three classes, used as a client
Three parts today.
```python
Fraction
```
```python
BankAccount
```
```python
Point
```

## Slide 6: Example: fractions
Example: fractions
Bob: I need 1/2 + 1/3 exactly, with no rounding.
Alice: I wrote a Fraction class. Take fraction.py.
Bob: How will I know how to use it?
Alice: Read its API. It says what each method does, not how.

## Slide 7: The Fraction API
The Fraction API
`fraction_api.py`
```python
class Fraction:
    """A signed fraction, like 2/3 or -1/5.
    Data: numerator and denominator, kept reduced."""

    def __init__(self, numerator, denominator):
        """The fraction numerator/denominator."""
    def add(self, other):
        """Returns this fraction plus other."""
    def multiply(self, other):
        """Returns this fraction times other."""
    def invert(self):
        """Returns 1 divided by this fraction."""
    def divide(self, other):
        """Returns this fraction divided by other."""
```
the file is in “week 9 code / fraction_api.py”.

## Slide 8: Creating fractions
Creating fractions
```python
python fraction_create.py
2/5
1/2
2 5
```
`fraction_create.py`
```python
from fraction import Fraction

x = 17
a = Fraction(2, 5)
b = Fraction(4, 8)
print(a)
print(b)
print(a.numerator, a.denominator)
```
[LIVE] the file is in “week 9 code / fraction_create.py”.

## Slide 9: Reading the client code
Reading the client code
`fraction_create.py`
```python
from fraction import Fraction

x = 17
a = Fraction(2, 5)
b = Fraction(4, 8)
print(a)
print(b)
print(a.numerator, a.denominator)
```
Fraction(2, 5)
Calls the class: builds a new object.
a = ...
a now refers to that object.
a.numerator
The dot reaches the object's data.

## Slide 10: Names refer to objects
Names refer to objects
x holds a number; a and b each refer to a Fraction object.
```python
x
```
```python
17
```
a Fraction
```python
numerator
```
```python
2
```
```python
denominator
```
```python
5
```
a Fraction
```python
numerator
```
```python
1
```
```python
denominator
```
```python
2
```
```python
a
```
```python
b
```

## Slide 11: What a = Fraction(2, 5) does
What a = Fraction(2, 5) does
1. Make: Python creates a new, empty Fraction object
2. Fill: the class's __init__ method sets up its data
3. Refer: a is set to refer to the new object

## Slide 12: Printing an object
Printing an object
print(a): shows 2/5, because the class says how
Behind it: a method named __str__ in the class
Without it: print shows <fraction.Fraction object at 0x...>

## Slide 13: Fraction methods
Fraction methods
```python
python fraction_demo.py
1/3 + 3/7 = 16/21
1/3 * 3/7 = 1/7
1/3 * (3/7 + 2/5) = 29/105
2/3 : 4/5 = 5/6
```
`fraction_demo.py`
```python
from fraction import Fraction

a = Fraction(1, 3)
b = Fraction(3, 7)
c = Fraction(2, 5)
print(f"{a} + {b} = {a.add(b)}")
print(f"{a} * {b} = {a.multiply(b)}")
d = a.multiply(b.add(c))    # 1/3 * (3/7 + 2/5)
print(f"{a} * ({b} + {c}) = {d}")
e = Fraction(2, 3).divide(Fraction(4, 5))
print("2/3 : 4/5 =", e)
```
[LIVE] the file is in “week 9 code / fraction_demo.py”.

## Slide 14: What s = a.add(b) does
What s = a.add(b) does
A method is called on one object, with another as its argument.
```python
a
```
the object it works on
```python
.add
```
the method
```python
(b)
```
the argument
a new Fraction
```python
numerator
```
```python
16
```
```python
denominator
```
```python
21
```
returned; s refers to it

## Slide 15: What the API tells us
What the API tells us
Methods: functions called on an object, like a.add(b)
Objects in: an object can be an argument, like b
Objects out: a method can return a new object
Unchanged: a and b stay the same after a.add(b)

## Slide 16: Recap: class design
Recap: class design
Requirements: pairs of integers, closed under + and ×
Design: two ints in; the methods return Fractions
The client: needs only the API, never the code

## Slide 17: Three classes, used as a client
Three classes, used as a client
Three parts today.
```python
Fraction
```
```python
BankAccount
```
```python
Point
```

## Slide 18: Example: bank accounts
Example: bank accounts
Bob: My boss wants the customers with negative balances.
Alice: Here every account is a BankAccount object.
Bob: So how do I start?
Alice: Read the BankAccount API, and take it from there.

## Slide 19: BankAccount objects
BankAccount objects
Every account holds an id, an owner and a balance.
```python
BankAccount
id, owner, balance
```
a BankAccount
```python
id
```
```python
1
```
```python
owner
```
```python
'Ron'
```
```python
balance
```
```python
1000
```
a BankAccount
```python
id
```
```python
2
```
```python
owner
```
```python
'Lisa'
```
```python
balance
```
```python
500
```
a BankAccount
```python
id
```
```python
3
```
```python
owner
```
```python
'Mike'
```
```python
balance
```
```python
750
```

## Slide 20: The BankAccount API
The BankAccount API
`bank_account_api.py`
```python
class BankAccount:
    """A bank account: an id, an owner and a balance.
    Also: get_id(), get_owner()."""

    def __init__(self, owner, balance=0):
        """A new account; ids run 1, 2, 3, ..."""
    def get_balance(self):
        """Returns the balance of this account."""
    def deposit(self, amount):
        """Adds amount to this account."""
    def withdraw(self, amount):
        """Takes amount out of this account."""
    def transfer_to(self, other, amount):
        """Moves amount from this account to other."""
```
the file is in “week 9 code / bank_account_api.py”.

## Slide 21: Two ways to open an account
Two ways to open an account
```python
python bank_create.py
1 Alice 0
2 Bob 500
Bob has 500
```
`bank_create.py`
```python
from bank_account import BankAccount

alice = BankAccount("Alice")
bob = BankAccount("Bob", 500)
print(alice)
print(bob)
print(f"{bob.get_owner()} has {bob.get_balance()}")
```
[LIVE] the file is in “week 9 code / bank_create.py”.

## Slide 22: Banking
Banking
```python
python bank_demo.py
1 Alice 1000
2 Bob 1300
1 Alice 600
2 Bob 1700
```
`bank_demo.py`
```python
from bank_account import BankAccount

alice = BankAccount("Alice")
bob = BankAccount("Bob", 500)

alice.deposit(1000)
bob.withdraw(200)
bob.deposit(1000)
print(alice)
print(bob)

alice.transfer_to(bob, 400)
print(alice)
print(bob)
```
[LIVE] the file is in “week 9 code / bank_demo.py”.

## Slide 23: transfer_to changes two objects
transfer_to changes two objects
alice.transfer_to(bob, 400)
alice
```python
id
```
```python
1
```
```python
owner
```
```python
'Alice'
```
```python
balance
```
```python
1000
```
bob
```python
id
```
```python
2
```
```python
owner
```
```python
'Bob'
```
```python
balance
```
```python
1300
```
before
alice
```python
id
```
```python
1
```
```python
owner
```
```python
'Alice'
```
```python
balance
```
```python
600
```
bob
```python
id
```
```python
2
```
```python
owner
```
```python
'Bob'
```
```python
balance
```
```python
1700
```
after

## Slide 24: Mutable and immutable
Mutable and immutable
Mutators: deposit, withdraw, transfer_to change the object
BankAccount: mutable, since balances have to change
Fraction: immutable, so add returns a new fraction
Who decides: the class designer, from the requirements

## Slide 25: Three classes, used as a client
Three classes, used as a client
Three parts today.
```python
Fraction
```
```python
BankAccount
```
```python
Point
```

## Slide 26: The Point API
The Point API
`point_api.py`
```python
class Point:
    """A point in the plane: coordinates x and y."""

    def __init__(self, x, y):
        """Constructs the point (x, y)."""
    def add(self, other):
        """The vector sum of this point and other."""
    def distance_to(self, other):
        """The straight-line distance to other."""
```
the file is in “week 9 code / point_api.py”.

## Slide 27: Using points
Using points
```python
one run (random)
(1, 2) (4, 6) 5.0 (5, 8)
nearest to p1: (2, 2)
```
`point_demo.py`
```python
from random import randint
from point import Point

p1 = Point(1, 2)
p2 = Point(4, 6)
print(p1, p2, p1.distance_to(p2), p1.add(p2))

points = []
for i in range(100):
    points.append(Point(randint(0, 20), randint(0, 20)))
nearest = points[0]
for p in points:
    if p.distance_to(p1) < nearest.distance_to(p1):
        nearest = p
print("nearest to p1:", nearest)
```
[LIVE] the file is in “week 9 code / point_demo.py”.

## Slide 28: Using objects in one slide
Using objects in one slide
Classes, objects
A class is a type
An object is one value of it
Names refer to objects
Creating
Call the class: Fraction(2, 5)
__init__ sets up the data
print uses __str__
Using
a.add(b): a method on a
a.numerator: data on a
Objects in, objects out
Designing
The API is the contract
Mutable or immutable?
Requirements decide
