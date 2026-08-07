# Dictionaries & Sets

## Dictionaries

### What a dictionary is

A dictionary stores data as **key-value pairs** — instead of accessing items by position (like a list), you access them by a unique label (the key).

```python
student = {"name": "Sam", "age": 25, "city": "NYC"}
```

### Creating dictionaries

```python
d1 = {"a": 1, "b": 2}
d2 = dict(a=1, b=2)
d3 = dict([("a", 1), ("b", 2)])
empty = {}
empty2 = dict()
```

### Accessing values

```python
d = {"name": "Sam", "age": 25}

d["name"]           # "Sam"  — raises KeyError if key doesn't exist
d.get("name")        # "Sam"  — safer, returns None if key doesn't exist
d.get("job", "N/A")   # "N/A" — custom default if key missing
```

**This is a big interview gotcha:** always use `.get()` when the key might not exist, to avoid crashing your program.

### Adding / Updating / Removing

```python
d = {"name": "Sam"}

d["age"] = 25              # add new key
d["name"] = "Ravi"          # update existing key
d.update({"city": "NYC"})    # add/update multiple keys at once

del d["age"]                  # remove a key (KeyError if missing)
d.pop("city")                   # remove & return value (KeyError if missing, unless default given)
d.pop("nokey", "default")        # returns "default" instead of crashing
d.popitem()                        # removes & returns the LAST inserted key-value pair
d.clear()                            # empties the dict
```

### Checking existence

```python
d = {"name": "Sam"}

"name" in d        # True — checks KEYS, not values
"Sam" in d          # False
"Sam" in d.values()   # True — explicitly check values
```

### Looping through a dictionary

```python
d = {"a": 1, "b": 2, "c": 3}

for key in d:              # loops over keys by default
    print(key)

for key in d.keys():         # explicit keys
    print(key)

for value in d.values():       # just values
    print(value)

for key, value in d.items():     # both together — most commonly used
    print(key, value)
```

### Dictionary comprehensions

```python
squares = {x: x**2 for x in range(5)}
# {0:0, 1:1, 2:4, 3:9, 4:16}

# Filter while building
evens = {x: x**2 for x in range(10) if x % 2 == 0}

# Swap keys and values
d = {"a": 1, "b": 2}
swapped = {v: k for k, v in d.items()}   # {1: 'a', 2: 'b'}
```

### Important: Dictionary keys MUST be immutable/hashable

```python
d = {(1, 2): "point"}    # OK — tuple is hashable
d = {[1, 2]: "point"}     # TypeError — list is NOT hashable
```

### `Counter` — the DSA MVP for frequency problems

```python
from collections import Counter

s = "aabbbc"
count = Counter(s)
# Counter({'b': 3, 'a': 2, 'c': 1})

count.most_common(1)     # [('b', 3)] — top 1 most frequent
count.most_common(2)      # top 2

words = ["a", "b", "a", "c", "b", "a"]
Counter(words)              # Counter({'a': 3, 'b': 2, 'c': 1})
```

This is used constantly for "find the most frequent element", "check anagram", "find duplicates" type problems.

### `defaultdict` — avoids KeyError headaches

```python
from collections import defaultdict

d = defaultdict(int)      # default value is 0 for missing keys
d["a"] += 1                 # no KeyError, starts at 0 automatically
d["a"] += 1
print(d)                      # defaultdict(<class 'int'>, {'a': 2})

d2 = defaultdict(list)         # default value is an empty list
d2["fruits"].append("apple")     # no need to check if key exists first
```

Massively useful for grouping problems:
```python
words = ["bat", "tab", "eat", "tea", "tan"]
groups = defaultdict(list)
for w in words:
    key = "".join(sorted(w))
    groups[key].append(w)
# groups the anagrams together
```

---
### Quick check

```python
from collections import Counter
print(Counter("mississippi").most_common(2))

a = {1, 2, 3}
b = {3, 4, 5}
print(a ^ b)

d = defaultdict(int)
for ch in "hello":
    d[ch] += 1
print(dict(d))
```
