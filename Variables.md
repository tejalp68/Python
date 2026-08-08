# Variables

Python is dynamically typed — no need to declare a type, it's inferred.

```python
x = 10           # int
name = "Sam"     # str
pi = 3.14        # float
is_valid = True  # bool
```

```python
x = 5
y = x  # y gets a copy of the reference, not a new object (matters for mutable types)

# Multiple assignment
a, b, c = 1, 2, 3
a = b = c = 0        # all point to same value
a, b = b, a           # swap without temp variable — very common in interviews

# Unpacking with *
first, *rest = [1, 2, 3, 4]     # first=1, rest=[2,3,4]
*rest, last = [1, 2, 3, 4]      # rest=[1,2,3], last=4
```

**Naming rules:** letters, digits, underscore; can't start with digit; case-sensitive; can't use reserved words (`if`, `class`, `for`, etc).

**Constants:** Python has no true constants — convention is `MAX_VALUE = 100` (all caps) to signal "don't change this."

---

## Truthy / Falsy — Full List

Falsy values: `False`, `None`, `0`, `0.0`, `0j`, `""`, `[]`, `()`, `{}`, `set()`, `range(0)`

Everything else is truthy.

```python
if my_list:        # instead of len(my_list) > 0
    ...
```

---

## `is` vs `==` (very commonly asked)

```python
a = [1, 2, 3]
b = [1, 2, 3]
a == b   # True — same values
a is b   # False — different objects in memory

c = a
c is a   # True — same object

# Small int caching gotcha
x = 256
y = 256
x is y   # True (Python caches small ints -5 to 256)

x = 257
y = 257
x is y   # False (usually — outside cache range)
```

---

## Quick Self-Check

```python
print(bool([]) or bool("0"))
```

*(Work it out using the truthy/falsy rules above before checking an answer.)*
