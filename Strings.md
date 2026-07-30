# Strings

## 1. What strings are in Python

Strings are **immutable sequences of characters**. Any "modification" actually creates a new string object.

```python
s = "Hello"
s[0] = "h"   # TypeError: 'str' object does not support item assignment
```

## 2. Creating strings

```python
s1 = 'single quotes'  
s2 = "double quotes"    
s3 = '''triple quotes    
spans multiple lines'''
s4 = "It's a \"quote\""     # escaping
s5 = r"raw\nstring"          # raw string — \n stays literal, not a newline

#throws error when same quote is use inside it
thats why escaping is used ("It's a \"quote\"" )
```

## 3. Indexing & Slicing (core DSA skill)

```python
s = "Hello World"

s[0]        # 'H'  -----> s.__getitem() this is dunder function which get called when we do sliciing   so s[i] = s.__getitem__(i)
s[-1]       # 'd'  (negative index = from end)
s[0:5]      # 'Hello'
s[:5]       # same as above   default 0 as start index
s[6:]       # 'World'      default end +1  as ending
s[:]        # full copy
s[::2]      # every 2nd char -> 'HloWrd'
s[::-1]     # reversed string -> 'dlroW olleH'
s[-3:]      # last 3 chars -> 'rld'
s[2:8:2]    # start:stop:step -> 'lo o'
```

`s[::-1]` for reversal is asked in almost every string interview problem.

Because the step is negative, Python doesn't use the normal defaults (0 to end). Instead, when step < 0:

start defaults to the last index (len(s) - 1)
stop defaults to one before index 0 (conceptually, "off the left edge")

So `s[::-1]` effectively means: "start at the last element, and walk backward to the first element, inclusive."

## 4. String Methods — the ones you'll actually use

**Case:**
```python
s.lower()        # "hello world"
s.upper()        # "HELLO WORLD"
s.title()        # "Hello World"  # capitalize first character of each word
s.capitalize()   # "Hello world"  # capitalize only first character of first word
s.swapcase()     # "hELLO wORLD"  # converts all uppercase characters in a string to lowercase and all lowercase characters to uppercase.
```

**Whitespace/cleanup:**
```python
"  hi  ".strip()    # "hi"   — both sides
"  hi  ".lstrip()   # "hi  " — left only
"  hi  ".rstrip()   # "  hi" — right only
#EX.
str = "299$"
str1 = str.rstrip("$")
print(str) ----> 299
```

**Searching:**
```python
s.find("World")     # 6 (index) or -1 if not found — doesn't raise error
s.index("World")    # 6 (index) or raises ValueError if not found
#returns the index (position) where it first starts — counting from 0.
#thats why it return 0 for hello and 6 for world
s.count("o")        # 2 — number of occurrences
s.startswith("Hello")
s.endswith("ld")
```

**Splitting & Joining (very common in interviews):**
```python
"a,b,c".split(",")        # ['a', 'b', 'c']   auto creates a list to store it in somewhere we have to store it in a variable and type of that variable will be list
"hello world".split()      # ['hello', 'world']  — splits on any whitespace
"a  b   c".split()          # ['a', 'b', 'c']    — collapses extra spaces
",".join(["a","b","c"])      # "a,b,c" , "a-b-c"
"".join(['a','p','p','l','e'])        # "apple"  — common way to build a string from a list of chars
```
**Sorting** 
```python
sorted("dcba")    #---> returns list of soretd letters

```

**Replacing:**
```python
s.replace("World", "Python")     # replaces ALL occurrences
s.replace("o", "0", 1)            # replace only first occurrence
```
right

**Checks (return bool — great for validation logic):**
```python
"123".isdigit()      # True
"abc".isalpha()       # True
"abc123".isalnum()     # True
"   ".isspace()         # True
"Hello".isupper()        # False
"HELLO".isupper()         # True
```

## 5. String Formatting — 3 ways (know all 3, f-strings preferred)

```python
name, age = "Sam", 25   #%s =placeholder for string ,%d =placeholder for digit

# 1. % formatting (old style, still appears in legacy code)
"%s is %d years old" % (name, age)

# 2. .format() method
"{} is {} years old".format(name, age)
"{0} is {1}".format(name, age)   # positional

# 3. f-strings (modern, fastest, preferred)
"                # repr() version, adds quotes: 'Sam'

#Format Specifiers
Specifier	Meaning
%s	        String
%d        	Integer (decimal)
%f        	Floating point number
%x	        Hexadecimal (lowercase)
%X	        Hexadecimal (uppercase)
%o        	Octal
%e        	Scientific notation (lowercase e)
%c	        Single character
%%	        A literal % sign

print("Value: %f" % 3.14159)     # Value: 3.141590
print("Hex: %x" % 255)           # Hex: ff
print("Octal: %o" % 8)           # Octal: 10
print("Percent: %d%%" % 50)      # Percent: 50%

print("%.2f" % 3.14159)   # 3.14  (2 decimal places)
print("%5d" % 3)          # "    3"  (padded to width 5) added to the fifth place
```

## 6. String Concatenation & Repetition

```python
"Hello" + " " + "World"   # "Hello World"
"ab" * 3                    # "ababab"

# Efficient concatenation in a loop — DON'T do this:
result = ""
for word in words:
    result += word           # creates a new string object every time — O(n²)

# DO this instead:
result = "".join(words)      # O(n) — much more efficient, ask about this in interviews
```

## 7. Common DSA String Patterns

```python
# Check palindrome
s = "racecar"
s == s[::-1]     # True

# Count character frequency
from collections import Counter
Counter("aabbbc")   # Counter({'b': 3, 'a': 2, 'c': 1})

# Check anagram
sorted("listen") == sorted("silent")   # True   ## both strings uses the same character with same length

# Remove duplicates while preserving order
list(dict.fromkeys("aabbcc"))    # ['a', 'b', 'c']  #extracts key from dict

# Convert string <-> list of chars
list("hello")          # ['h','e','l','l','o']
"".join(['h','e','l','l','o'])   # 'hello'

# Convert string <-> ASCII
ord('a')     # 97    only takes one argument
chr(97)      # 'a'   # also takes only one argument
```

## 8. String Comparison

Strings compare lexicographically (character by character, using ASCII/Unicode values):
```python
"apple" < "banana"    # True  ('a' < 'b')
"Apple" < "apple"     # True  (uppercase letters have lower ASCII values than lowercase)
"10" < "9"             # True  — string comparison, NOT numeric! ('1' < '9')
```

**Gotcha:** comparing numeric strings compares character-by-character, not by value — a classic interview trap.


**Common escape sequences in Python:**
|  Escape  |  Meaning  |
|----------|-----------|
|\n	|Newline (line break)
|\t	|Tab (horizontal space)
|\\	|Literal backslash \
|\'	|Single quote '
|\"	|Double quote "
|\r	|Carriage return
|\b	|Backspace
|\f	|Form feed
|\v	|Vertical tab
|\0	|Null character
|\a	|Bell/alert sound
|\N{name}	|Unicode character by name
|\uXXXX	|Unicode character (4 hex digits)
|\UXXXXXXXX	|Unicode character (8 hex digits)
|\xXX	|Character by hex value (2 hex digits)

```python

### Examples:

**`\n` — newline:**
```python
print("Hello\nWorld")
```
Output:
```
Hello
World
```

**`\t` — tab:**
```python
print("Name:\tAlice")
```
Output:
```
Name:	Alice
```

**`\\` — literal backslash:**
```python
print("C:\\Users\\Alice")
```
Output:
```
C:\Users\Alice
```

**`\'` and `\"` — quotes inside strings:**
```python
print('It\'s sunny today')
print("She said \"hello\"")
```
Output:
```
It's sunny today
She said "hello"
```

**`\r` — carriage return (moves cursor to line start):**
```python
print("Hello\rWorld")
```
Output:
```
World
```
(`World` overwrites `Hello` because `\r` returns the cursor to the start of the line — mostly noticeable in terminals/live progress bars, not always in simple print output.)

**`\a` — bell (produces a beep sound on some systems):**
```python
print("Alert!\a")
```

**`\xXX` — hex character code:**
```python
print("\x48\x69")   # Hi
```

**`\uXXXX` — unicode character:**
```python
print("\u2764")   # ❤
```

---

## Raw strings (avoiding escape sequences)

Sometimes you *don't* want `\n`, `\t`, etc. to be interpreted — especially with file paths or regex. Use a **raw string** by prefixing with `r`:

```python
path = r"C:\Users\Alice\notes.txt"
print(path)
```
Output:
```
C:\Users\Alice\notes.txt
```

Without the `r`, `\n` and `\t` inside the path would be misinterpreted as newline/tab characters, breaking the path.

---

### Quick summary:
- Escape sequences let you insert special/invisible characters (`\n`, `\t`) or literal characters that would otherwise conflict with string syntax (`\'`, `\"`, `\\`).
- Use `\u` / `\x` / `\N{}` for inserting specific Unicode characters.
- Use raw strings (`r"..."`) when you want backslashes treated literally.
  
---

### Quick check
What do these print?
```python
print("Hello"[1:4])  #can directly write the string value in print and still get the same value
print("abc" * 2)   ----> abcabc
print(sorted("dcba")) ----->['a','b','c','d']
print("  Hi  ".strip().lower()) ---> hi
```
