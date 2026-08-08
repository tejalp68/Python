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

## What "truthy" and "falsy" mean

Python doesn't require a value to literally be `True` or `False` to be used in a boolean context (like an `if` statement). Every object in Python has an inherent "truthiness" — Python asks "is this thing empty/zero/nothing, or does it have substance?"

- **Falsy** = treated as `False` when evaluated in a boolean context
- **Truthy** = treated as `True` when evaluated in a boolean context

## The complete list of falsy values

```python
False        # the boolean itself
None         # represents "nothing"
0            # int zero
0.0          # float zero
0j           # complex zero
""           # empty string
''           # empty string (same thing)
[]           # empty list
()           # empty tuple
{}           # empty dict
set()        # empty set
range(0)     # empty range
```

**Everything else is truthy** — including `"0"` (a non-empty string!), `[0]` (a list containing zero), `" "` (a space), and any nonzero number like `-1`.

## Why this matters — how Python checks it

Under the hood, Python calls `bool(x)` on the value. Custom objects can even define their own truthiness by implementing `__bool__()` or `__len__()` (if `__len__()` returns 0, the object is falsy — that's why empty lists/dicts/strings are falsy, they all define `__len__`).

## Where you'll actually use this

**Checking if a collection is empty (the Pythonic way):**

```python
my_list = []

# Bad (works, but not idiomatic)
if len(my_list) == 0:
    print("empty")

# Good (Pythonic)
if not my_list:
    print("empty")
```

**Default value patterns:**

```python
name = ""
display_name = name or "Anonymous"   # "" is falsy, so this picks "Anonymous"
```

**Quick validity checks:**

```python
def process(data):
    if not data:          # catches None, [], "", 0, etc all at once
        return "no data"
    return data[0]
```

## Common traps interviewers use

```python
bool("False")   # True!  — non-empty string, doesn't matter what text it contains
bool("0")       # True!  — non-empty string
bool(0)         # False  — this is the actual number zero
bool([0])       # True!  — list has one element, so it's non-empty
bool(" ")       # True!  — a space is still a character, non-empty string
bool(None)      # False
bool([])        # False
```

The trap pattern: **strings only care about length, not content.** `"False"`, `"0"`, `"no"` — all truthy, because they're non-empty strings.

## `and` / `or` return values, not just True/False (important nuance)

Python's `and`/`or` don't necessarily return `True`/`False` — they return one of the actual operands:

```python
print(3 or 5)        # 3  — returns first truthy value it finds (short-circuits)
print(0 or 5)        # 5  — 0 is falsy, so moves to next
print(3 and 5)       # 5  — both truthy, "and" returns the LAST value
print(0 and 5)       # 0  — short-circuits at first falsy value
print([] or {})      # {} — both falsy, returns the last one
```

This is why `name or "Anonymous"` works the way it does above.

## Quick check to test yourself

What does each line print?

```python
print(bool(" "))    ----->True
print(bool([]) or bool("0")) ---->True
print(0 and "hello")  ----> 0
print("" or [] or "last") ---->'last'
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
# but in my code it is giving true
```

---

Questions to practice
Here's a clean list of questions on **Variables** and **Truthy/Falsy** in Python:

### Variables

1. Create a variable `name` and assign your name to it, then print it.
2. Create two variables `a` and `b` with values `10` and `20`. Swap their values without using a third variable.
3. Store your age in a variable and print it using an f-string.
4. What is the output?
   ```python
   x = 5
   x = x + 1
   print(x)
   ```
5. Assign the same value `100` to three variables `a`, `b`, `c` in a single line.
6. What's the difference between `x = y = 10` and `x, y = 10, 10`?
7. Given `a, b = 5, 10`, swap their values in one line.
8. What is the output?
   ```python
   x = 10
   y = x
   x = 20
   print(y)
   ```
9. Why does this code cause an error?
   ```python
   print(z)
   z = 5
   ```
10. What data type does Python assign to each of these?
    ```python
    a = 10
    b = 10.5
    c = "10"
    d = True
    e = None
    ```
11. Which of these are valid variable names: `1number, _value, my-var, class, total_sum, $price`? Explain.
12. What's the difference between `Name`, `name`, and `NAME` as variable names?
13. What is the output?
    ```python
    a = [1, 2, 3]
    b = a
    b.append(4)
    print(a)
    ```
14. Use `type()` to check the data type of a list, a tuple, and a dictionary.
15. What is the output?
    ```python
    x = 5
    def change():
        x = 10
        print(x)
    change()
    print(x)
    ```
16. Convert the string `"123"` into an integer and add `7` to it.
17. Demonstrate Python's dynamic typing with an example where one variable holds different data types over time.
18. Using `id()`, explain why `a = 5; b = 5` may give `id(a) == id(b)`, but `a = [1,2]; b = [1,2]` does not.

### Truthy / Falsy

19. List all the values in Python that are considered **falsy**.
20. What is the output?
    ```python
    if []:
        print("Yes")
    else:
        print("No")
    ```
21. What is the output?
    ```python
    if "0":
        print("Truthy")
    else:
        print("Falsy")
    ```
22. Is `0.0` truthy or falsy? Verify with code.
23. What is the output?
    ```python
    values = [0, 1, "", "hello", None, [], [0], {}, False, True]
    for v in values:
        print(v, "->", bool(v))
    ```
24. Why is `"False"` (as a string) truthy even though it represents the word "False"?
25. What is the output?
    ```python
    x = 10
    print(bool(x))
    print(bool(-5))
    print(bool(0))
    ```
26. What is the output?
    ```python
    a = []
    b = {}
    c = ()
    print(bool(a), bool(b), bool(c))
    ```
27. Predict the output:
    ```python
    if None:
        print("A")
    elif 0:
        print("B")
    elif "":
        print("C")
    else:
        print("D")
    ```
28. What does `bool(float("nan"))` return? Is `nan` truthy or falsy?
29. Write a function `is_empty(value)` that uses truthy/falsy logic to check if a value is "empty" (works for strings, lists, dicts, numbers).
30. What is the output, and why?
    ```python
    print(bool("False"))
    print(bool("0"))
    print(bool(" "))
    ```
