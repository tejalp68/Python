\# Type Casting — Full Table



```python

int("42")          # 42

int("42", 2)        # base 2 -> 34 (base conversion, interview favorite)

int(42.9)             # 42 (truncates toward zero)

float(42)               # 42.0

str(42)                   # "42"

list("abc")                 # \['a', 'b', 'c']

tuple(\[1,2,3])                 # (1, 2, 3)

set(\[1,1,2,3])                    # {1, 2, 3} — dedupes

dict(\[("a",1),("b",2)])              # {'a': 1, 'b': 2}

```



\*\*Common errors to know:\*\*



```python

int("abc")            # ValueError

int("3.5")             # ValueError — can't directly convert decimal string to int

int(float("3.5"))         # 3 — must go through float first

```



\---





