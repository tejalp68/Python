
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

## List vs Tuple — the interview summary table

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
