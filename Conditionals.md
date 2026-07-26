# Conditionals

## Basic if / elif / else

```python
age = 20

if age < 13:
    print("child")
elif age < 20:
    print("teenager")
else:
    print("adult")
```

- Python uses **indentation** (not braces) to define code blocks — this is strict and matters.
- `elif` is Python's version of "else if" — you can chain as many as you want.
- `else` is optional and only runs if nothing above matched.

## One-line if (no else)

```python
if age > 18: print("adult")
```
Works, but not commonly used in real code — mentioned for completeness.

## Ternary (Conditional) Expression — very commonly tested

```python
age = 20
status = "adult" if age >= 18 else "minor"
```

Syntax: `value_if_true if condition else value_if_false`

Compare to a normal if/else — this is just a compact way to assign a value based on a condition:
```python
# Long way
if age >= 18:
    status = "adult"
else:
    status = "minor"

# Short way (ternary)
status = "adult" if age >= 18 else "minor"
```

Can be nested (use sparingly, gets unreadable fast):
```python
category = "child" if age < 13 else "teen" if age < 20 else "adult"
```

## Nested conditionals

```python
num = 15

if num > 0:
    if num % 2 == 0:
        print("positive even")
    else:
        print("positive odd")
else:
    print("not positive")
```

## Multiple conditions with `and` / `or`

```python
age = 25
has_id = True

if age >= 18 and has_id:
    print("can enter")

if age < 13 or age > 65:
    print("discount applies")
```

## Chained comparisons (Python-specific shortcut)

```python
x = 15

# Instead of:
if x > 10 and x < 20:
    print("in range")

# Python lets you write:
if 10 < x < 20:
    print("in range")
```

## `in` for membership checks inside conditionals

```python
fruit = "apple"
basket = ["apple", "banana", "cherry"]

if fruit in basket:
    print("found it")

vowels = "aeiou"
char = "e"
if char in vowels:
    print("vowel")
```

## Using truthy/falsy directly (Pythonic style — revisit from earlier)

```python
name = ""

# Not Pythonic
if len(name) == 0:
    print("empty")

# Pythonic
if not name:
    print("empty")

data = [1, 2, 3]
if data:               # True if non-empty
    print("has data")
```

## `match` statement — Python's version of switch/case (3.10+, worth knowing)

```python
day = 3

match day:
    case 1:
        print("Monday")
    case 2:
        print("Tuesday")
    case 3:
        print("Wednesday")
    case _:                    # default case, like "else"
        print("Unknown day")
```

You can also match multiple values or patterns:
```python
match day:
    case 1 | 2 | 3 | 4 | 5:
        print("Weekday")
    case 6 | 7:
        print("Weekend")
```

This is newer and less universally expected in interviews than if/elif, but good to mention you know it.

## Common conditional gotchas (interview traps)

```python
# Assignment vs comparison — Python actually prevents this mistake (unlike C)
if x = 5:      # SyntaxError in Python — good, this protects you!
    ...
if x == 5:     # correct
    ...

# Comparing to None — always use "is", not "=="
if x is None:      # correct/Pythonic
if x == None:        # works, but not idiomatic

# Comparing floats directly can be risky
if 0.1 + 0.2 == 0.3:      # False! floating point imprecision
    print("won't print")

# Correct way to compare floats
if abs((0.1 + 0.2) - 0.3) < 1e-9:
    print("close enough")

# Truthy trap — a string "False" is truthy!
if "False":              # this runs! non-empty string is truthy
    print("this prints")
```

---

### Quick check
```python
x = 7
print("even" if x % 2 == 0 else "odd")

name = ""
if not name:
    print("no name given")

y = 15
print(10 < y < 20 and y != 15)
```
