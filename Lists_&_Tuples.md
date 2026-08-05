# Lists & Tuples

## Lists — the workhorse of Python DSA

```python
lst = [1, 2, 3, "four", 5.0]   # can hold mixed data types 
empty = []
empty2 = list()
```

**Lists are [mutable]** — you can change, add, remove elements in place.

### Indexing & Slicing (same rules as strings)
```python
lst = [10, 20, 30, 40, 50]
lst[0]        # 10
lst[-1]       # 50
lst[1:3]      # [20, 30]
lst[::-1]     # [50, 40, 30, 20, 10] — reversed
lst[::2]      # [10, 30, 50]
```

### Core List Methods

```python
lst = [1, 2, 3]

lst.append(4)        # [1, 2, 3, 4] — add to end
lst.insert(1, 99)    # [1, 99, 2, 3, 4] — insert at index #will add 99 at index 1
lst.extend([5, 6])   # [1, 99, 2, 3, 4, 5, 6] — merge another list in add two list together
lst.remove(99)       # removes first occurrence of value (ValueError if not found)
lst.pop()            # removes & returns LAST element
lst.pop(0)           # removes & returns element at index 0
lst.index(3)         # returns index of first occurrence of value
lst.count(2)          # count occurrences of value
lst.sort()            # sorts in place (returns None!)
lst.sort(reverse=True) # descending
lst.reverse()          # reverses in place #no need to store anywhere(will directly make change to the original list)
lst.clear()             # empties the list 
lst.copy()               # shallow copy
```

**Common gotcha:** `sort()` modifies in place and returns `None`. Use `sorted(lst)` if you want a new sorted list without touching the original.

```python
lst = [3, 1, 2]
x = lst.sort()      # x is None! lst is now [1, 2, 3]
y = sorted(lst)      # y is a new sorted list, lst unchanged
```

### Sorting with a custom key (very common in interviews)

```python
words = ["banana", "kiwi", "apple"]
sorted(words, key=len)                  # ['kiwi', 'apple', 'banana'] — by length
sorted(words, key=lambda w: w[-1])       # sort by last character
students = [("Sam", 85), ("Ana", 92)]
sorted(students, key=lambda s: s[1], reverse=True)  # by score, descending
```

### List Comprehensions (must-know, appears everywhere)

```python
squares = [x**2 for x in range(5)]              # [0, 1, 4, 9, 16]
evens = [x for x in range(10) if x % 2 == 0]     # [0, 2, 4, 6, 8]
pairs = [(x, y) for x in range(2) for y in range(2)]  # nested loops
flat = [x for row in matrix for x in row]         # flatten a 2D list
```

### List slicing tricks used in DSA

```python
lst = [1, 2, 3, 4, 5]
lst[1:1] = [99]        # insert without pop/index gymnastics -> [1, 99, 2, 3, 4, 5]
lst[1:3] = []            # delete a slice -> removes indices 1,2
lst[:] = [0]*5             # replace contents in place (same object!)
```

### Copying lists — a classic trap

```python
a = [1, 2, 3]
b = a               # NOT a copy — same object
b.append(4)
print(a)             # [1, 2, 3, 4] — a changed too!

c = a.copy()          # shallow copy — new outer list
c = a[:]                # also a shallow copy
import copy
d = copy.deepcopy(a)     # deep copy — needed for nested lists
```

**Shallow copy gotcha with nested lists:**
```python
nested = [[1, 2], [3, 4]]
shallow = nested.copy()
shallow[0].append(99)
print(nested)   # [[1, 2, 99], [3, 4]] — inner lists still shared!
```

## Tuples — the immutable sibling

```python
t = (1, 2, 3)
single = (5,)        # note the comma — without it, (5) is just an int!
empty = ()
```

**Tuples are immutable** — no append, remove, sort, etc. Once created, contents can't change.

```python
t = (1, 2, 3)
t[0] = 99   # TypeError
```

### Why use tuples over lists?
- Faster than lists (less overhead)
- Immutability means they're **hashable** — can be used as dictionary keys or set elements (lists can't be)
- Signals intent: "this data shouldn't change"

```python
locations = {(0, 0): "origin", (1, 1): "point A"}   # tuple as dict key — works
locations2 = {[0, 0]: "origin"}                        # TypeError — list not hashable
```

### Quick check
```python
a = [1, [2, 3]]
b = a.copy()
b[1].append(4)
print(a)

t = (1, 2, 3)
x, *y = t
print(y)
```
#### Shallow Copy And Deep copy

## Imagine you have a toy box

Think of a list as a **toy box** with toys inside it.

```python
toybox = ["car", "ball", "doll"]
```

Shallow Copy — Making a copy of the BOX, but not the toys

#### Imagine you have a toy box, and you make a brand new box, and then you put the *exact same toys* inside it (not new toys — the same physical toys, just placed in a second box).

```python
toybox = ["car", "ball", "doll"]
new_box = toybox.copy()   # or toybox[:]
```

Now you have **two boxes**, but they hold the **same toys**.

If you add a new toy to `new_box`, it doesn't affect `toybox` — because the boxes themselves are different:
```python
new_box.append("teddy bear")
print(toybox)    # ["car", "ball", "doll"]  — unaffected!
print(new_box)   # ["car", "ball", "doll", "teddy bear"]
```

That part works like you'd expect. **But here's the catch** — what if one of the "toys" is itself a small box (a nested list)?

```python
toybox = ["car", ["small", "toys"]]
new_box = toybox.copy()
```

Now `new_box` has its own big box, but the **small box inside is literally the SAME small box** — not a copy of it! If you open the small box in `new_box` and add something:

```python
new_box[1].append("marble")
print(toybox)    # ["car", ["small", "toys", "marble"]]  — CHANGED! 
print(new_box)   # ["car", ["small", "toys", "marble"]]
```

Both boxes show the change — because they were sharing that one small inner box the whole time. **A shallow copy only copies the outer box, not what's inside if it's another container.**

## Deep Copy — Making a copy of EVERYTHING, even the toys inside boxes inside boxes

A deep copy says: "Copy the big box, AND copy every single toy inside it, AND if a toy is itself a box, copy that box too, and everything inside THAT."

```python
import copy

toybox = ["car", ["small", "toys"]]
new_box = copy.deepcopy(toybox)

new_box[1].append("marble")
print(toybox)    # ["car", ["small", "toys"]]        — unaffected!
print(new_box)   # ["car", ["small", "toys", "marble"]]
```

Now the two boxes are **completely independent**. Nothing you do to one ever affects the other, no matter how deep the nesting goes.

## The simple rule to remember

- **Shallow copy** = new outer box, same inner boxes (shared)
- **Deep copy** = new outer box, AND new inner boxes too (fully separate)

```python
a = [1, [2, 3]]

b = a.copy()              # shallow — b[1] is the SAME list as a[1]
c = copy.deepcopy(a)       # deep — c[1] is a totally NEW list

b[1].append(99)
print(a)   # [1, [2, 3, 99]]  — changed because b[1] and a[1] are the same list

c[1].append(100)
print(a)   # [1, [2, 3, 99]]  — unaffected, c is fully independent
```

## When do you need which?

- If your list only has simple things (numbers, strings) → shallow copy (`.copy()` or `[:]`) is enough, since there's nothing nested to worry about.
- If your list has lists inside lists (or dicts inside lists, etc.) → use `deepcopy()` if you need them to be truly independent.

---

Quick check for you:
```python
a = [[1, 2], [3, 4]]
b = a.copy()
b[0][0] = 99
print(a[0][0])   # what does this print?
```

## What is a lambda function?

A **lambda** is a tiny, throwaway function you write in a single line, without giving it a name using `def`. It's meant for quick, simple operations you'll use once (or pass into another function) — not for anything complex.

```python
# Normal function
def square(x):
    return x ** 2

# Same thing as a lambda
square = lambda x: x ** 2

square(5)   # 25
```

**Syntax:**
```python
lambda arguments: expression
```
- No `return` keyword — the expression's result is automatically returned.
- Can take any number of arguments, but only **one expression** (no multi-line logic, no loops, no `if/else` blocks — just one expression).

```python
add = lambda a, b: a + b
add(3, 4)   # 7

is_even = lambda x: x % 2 == 0
is_even(4)  # True
```

**Now, what if you want something more custom than a built-in function like `len`?** That's exactly where lambda comes in — you write a tiny custom function inline, right there in the `key` argument, instead of separately defining one with `def`.

```python
words = ["banana", "kiwi", "apple"]

# Sort by the LAST character of each word
sorted(words, key=lambda w: w[-1])
```

Walking through what happens:
1. Python takes each word one at a time
2. For each word `w`, it runs `lambda w: w[-1]` → gives back the last character
3. Python sorts the words based on those last characters, not the words themselves

## The "why not just use def?" question

You *could* write this instead:
```python
def last_char(w):
    return w[-1]

sorted(words, key=last_char)
```

Both do the exact same thing. But lambda saves you the trouble of naming and defining a whole function just to use it once, right in that one line. It's a shortcut for simple, single-use logic.

## More sorting examples with lambda

```python
students = [("Sam", 85), ("Ana", 92), ("Ravi", 78)]

# Sort by score (2nd item in each tuple)
sorted(students, key=lambda s: s[1])
# [('Ravi', 78), ('Sam', 85), ('Ana', 92)]

# Sort by score, highest first
sorted(students, key=lambda s: s[1], reverse=True)
# [('Ana', 92), ('Sam', 85), ('Ravi', 78)]

# Sort by name length
sorted(students, key=lambda s: len(s[0]))

# Sort a list of dicts by a specific field
people = [{"name": "Sam", "age": 25}, {"name": "Ana", "age": 22}]
sorted(people, key=lambda p: p["age"])
```

## What's actually happening conceptually

Think of `key=lambda x: ...` as saying: **"Before comparing two items to decide their order, first run them through this tiny function, and compare the results instead of the raw items."**

```python
nums = [-5, 3, -2, 8, -1]

# Sort by absolute value, ignoring sign
sorted(nums, key=lambda x: abs(x))
# [-1, -2, 3, -5, 8]
```

Here, Python doesn't compare `-5` and `3` directly — it compares `abs(-5)=5` and `abs(3)=3`, and orders based on that.

## Where else lambda shows up (quick mention)

```python
# map() — apply a function to every item
list(map(lambda x: x**2, [1,2,3]))     # [1, 4, 9]

# filter() — keep items where lambda returns True
list(filter(lambda x: x % 2 == 0, [1,2,3,4]))   # [2, 4]
```

---

Quick check for you:
```python
words = ["dog", "elephant", "cat", "fox"]
result = sorted(words, key=lambda w: len(w))
print(result)
```
