# Week 11 code files

The code files shown in the week 11 lectures.

### `bank_account.py`
```python
"""The BankAccount class."""


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

### `class_attribute.py`
```python
from bank_account import BankAccount

a = BankAccount("Ron", 1000)
b = BankAccount("Lisa", 500)
c = BankAccount("Mike", 750)
print(a.get_id(), b.get_id(), c.get_id())
print("next id:", BankAccount._next_id)
```

### `fraction.py`
```python
"""The Fraction class."""


def gcd(x, y):
    """GCD of x and y, by Euclid's algorithm."""
    while y != 0:
        x, y = y, x % y
    return x


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

### `point.py`
```python
"""The Point class."""
import math


class Point:
    """A point in the plane: coordinates x and y."""

    def __init__(self, x, y):
        """Constructs the point (x, y)."""
        self.x = x
        self.y = y

    def __str__(self):
        """The point as "(x, y)"."""
        return f"({self.x}, {self.y})"

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

### `point_demo.py`
```python
from point import Point

p1 = Point(1, 2)
p2 = Point(4, 6)
print(p1, p2)
print(p1.distance_to(p2))
print(p1.add(p2))
```

### `self_demo.py`
```python
from bank_account import BankAccount

alice = BankAccount("Alice")
alice.deposit(100)
BankAccount.deposit(alice, 100)    # the same call
print(alice.get_balance())
```

### `unsafe_client.py`
```python
from bank_account import BankAccount

acc = BankAccount("Mallory", 100)
acc._balance = 1_000_000     # Python allows it...
print(acc)                   # ...and the bank pays
```
