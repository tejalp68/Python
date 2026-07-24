# Lists & Tuples

## 1. Lists — the workhorse of Python DSA

```python
lst = [1, 2, 3, "four", 5.0]   # can hold mixed types
empty = []
empty2 = list()
```

**Lists are mutable** — you can change, add, remove elements in place.

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
lst.insert(1, 99)    # [1, 99, 2, 3, 4] — insert at index
lst.extend([5, 6])   # [1, 99, 2, 3, 4, 5, 6] — merge another list in
lst.remove(99)       # removes first occurrence of value (ValueError if not found)
lst.pop()            # removes & returns LAST element
lst.pop(0)           # removes & returns element at index 0
lst.index(3)         # returns index of first occurrence of value
lst.count(2)          # count occurrences of value
lst.sort()            # sorts in place (returns None!)
lst.sort(reverse=True) # descending
lst.reverse()          # reverses in place
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

## 2. Tuples — the immutable sibling

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

### Tuple methods (only 2 — that's the whole point)
```python
t = (1, 2, 2, 3)
t.count(2)     # 2
t.index(3)     # 3
```

### Tuple unpacking (used constantly)
```python
point = (3, 4)
x, y = point           # x=3, y=4

for i, val in enumerate(["a", "b", "c"]):
    print(i, val)        # 0 a / 1 b / 2 c

a, b = 1, 2
a, b = b, a              # swap, revisited

def get_stats():
    return 1, 2, 3         # actually returns a tuple (1, 2, 3)
x, y, z = get_stats()
```

## 3. List vs Tuple — the interview summary table

| Feature | List | Tuple |
|---|---|---|
| Mutable | Yes | No |
| Syntax | `[1, 2, 3]` | `(1, 2, 3)` |
| Speed | Slower | Faster |
| Hashable (usable as dict key) | No | Yes |
| Methods available | Many | Only `count`, `index` |
| Use case | Data that changes | Fixed data, dict keys, function returns |

## 4. Common DSA patterns with lists

```python
# Two-pointer technique setup
lst = [1, 2, 3, 4, 5]
left, right = 0, len(lst) - 1

# Sliding window
window = lst[i:i+k]

# Finding max/min with index
max(lst)                    # value
lst.index(max(lst))         # index of max

# Sum, min, max built-ins
sum(lst), min(lst), max(lst)

# Zip — pair up two lists
names = ["a", "b"]
scores = [90, 80]
list(zip(names, scores))   # [('a', 90), ('b', 80)]

# Enumerate — index + value together
for i, v in enumerate(lst):
    print(i, v)
```

---

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

Want the README for this one, or move to **Point 5: Dictionaries & Sets**?
