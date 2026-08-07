# Sets

### What a set is

A set is an **unordered collection of unique values** — no duplicates allowed, and no indexing (since there's no defined order).

```python
s = {1, 2, 3, 3, 2}
print(s)   # {1, 2, 3} — duplicates automatically removed
```

**Note:** `{}` creates an empty **dict**, not a set. For an empty set, you must use `set()`.

### Core set operations

```python
s = {1, 2, 3}

s.add(4)          # {1, 2, 3, 4}
s.remove(4)         # removes value, raises KeyError if not found
s.discard(4)          # removes value, NO error if not found (safer)
s.pop()                 # removes & returns an ARBITRARY element (sets have no order)
s.clear()                 # empties the set
```

### Set math — the real power of sets

```python
a = {1, 2, 3}
b = {2, 3, 4}

a | b      # union            -> {1, 2, 3, 4}
a & b      # intersection      -> {2, 3}
a - b      # difference         -> {1}         (in a, not in b)
b - a      # difference          -> {4}         (in b, not in a)
a ^ b      # symmetric difference -> {1, 4}     (in either, but not both)

a.issubset(b)      # is a fully contained in b?
a.issuperset(b)      # does a contain all of b?
a.isdisjoint(b)        # True if no overlap at all
```

### Why sets matter for interviews: O(1) lookup

```python
lst = [1, 2, 3, 4, 5]
s = set(lst)

3 in lst    # O(n) — checks every element one by one
3 in s      # O(1) average — hash-based lookup, much faster
```

**Classic use case: removing duplicates fast**
```python
nums = [1, 2, 2, 3, 3, 3]
unique = list(set(nums))     # [1, 2, 3] — order not guaranteed
```

**Classic use case: finding duplicates**
```python
def has_duplicate(nums):
    seen = set()
    for n in nums:
        if n in seen:
            return True
        seen.add(n)
    return False
```

### Set comprehension

```python
squares = {x**2 for x in range(5)}   # {0, 1, 4, 9, 16}
```

### `frozenset` — the immutable version

```python
fs = frozenset([1, 2, 3])
fs.add(4)    # AttributeError — frozensets can't be modified
```
Used when you need a set that's hashable itself (e.g., as a dictionary key or inside another set).

---

## Dict vs Set — quick distinction

| | Dictionary | Set |
|---|---|---|
| Stores | key-value pairs | just values |
| Syntax | `{"a": 1}` | `{1, 2, 3}` |
| Ordered (insertion order preserved)? | Yes (3.7+) | No guaranteed order |
| Duplicates | keys unique, values can repeat | all values unique |
| Lookup speed | O(1) average | O(1) average |

---

