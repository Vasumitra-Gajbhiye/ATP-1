# Programming Mid-Sem Notes (ATP-1)

Covers notebooks 1–15, the Warehouse OMS assignments (v1, v2, functions), and the Inventory Tracker.
Convention used below: `# →` shows what a line prints or evaluates to.

---

## 1. Python Basics

### Jupyter essentials

- **Shift + Enter** runs a cell and moves to the next one. **Ctrl/Cmd + Enter** runs it and stays on it.
- `[3]` shows the order cells ran in, and `[*]` means a cell is still running.
- **Restart Kernel** wipes all variables. Use it when results look strange.
- Trap: cells run in the order *you* run them. A variable from an old run can leak in. For example, a `total` you never reset printed 265 instead of 210 for the sum of 1–20.

### Comments

- `#` starts a single-line comment, which the interpreter ignores. Python has no multi-line comment syntax.
- A `"""triple-quoted string"""` at the top of a function is a **docstring**, not a comment.

### print()

```python
print("Python", "is", "fun")          # → Python is fun        (default sep=" ")
print("Hello", "World", sep="___")    # → Hello___World
print("Hello", "World", end="___")    # → Hello World___       (no newline at the end)
print("*" * 25)                       # → *************************
print("Vasu", 560100, True)           # → Vasu 560100 True     (mixed types are fine)
```

### Variables and dynamic typing

- A variable is a **name that refers to a value** in memory: `name = value`.
- **Dynamic typing** means there's no type declaration, and the same name can hold a different type later.

```python
x = 10              # int
x = "now a string"  # now str: allowed
a, b, c = 2, 3, 4   # multiple assignment
a = 2; b = 3        # ; puts two statements on one line
a, b = b, a         # swap with no temp variable (tuple unpacking)
```

### Data types

| Type | Example | Notes |
|---|---|---|
| `int` | `18`, `10**100` | Unlimited size |
| `float` | `5.8`, `1e308` | Double precision, max ≈ 1.8e308 |
| `str` | `"John"`, `'x'`, `"""multi-line"""` | Text, always in quotes |
| `bool` | `True`, `False` | Acts as 1 and 0: `True + True` → `2` |
| `complex` | `3+4j`, `complex(3, 4)` | `.real` → `3.0`, `.imag` → `4.0`, `abs(3+4j)` → `5.0` |
| `NoneType` | `None` | Means "no value" |

- Check a type with `type(x)` or `isinstance(x, int)`.
- Quick check: `10` → int, `"10"` → str, `10.0` → float, `False` → bool, `"True"` → str (quotes make it text), `"₹8.5"` → str.

### Identifiers (naming rules)

- Must start with a **letter or `_`**, followed by letters, digits or `_`. No spaces or symbols.
- **Case-sensitive**: `age` and `Age` are different names.
- **Can't be a keyword.** There are 35 (`import keyword; keyword.kwlist`), including `if elif else for while break continue pass def return class global nonlocal lambda True False None and or not in is import from as try except finally raise with del assert yield async await`.
- `print`, `len` and `list` are **not** keywords, just built-in functions. Assigning to them is legal but breaks them.
- Conventions: `snake_case` for variables and functions, `CapWords` for classes.
- `total_marks` ✅ · `_hidden_value` ✅ · `2nd_attempt` ❌ starts with a digit (SyntaxError) · `Player Score` ❌ has a space · `class` ❌ is a keyword

---

## 2. Operators and Expressions

An **expression** is code that produces a value.

### Arithmetic

| Op | Meaning | Example |
|---|---|---|
| `+` `-` `*` | add, subtract, multiply | `5 * 2` → `10` |
| `/` | division, **always a float** | `10 / 2` → `5.0`, `9 / 2` → `4.5` |
| `//` | floor division (rounds **down**) | `9 // 2` → `4`, `-7 // 2` → `-4` |
| `%` | remainder (modulus) | `10 % 3` → `1` |
| `**` | power | `2 ** 4` → `16` |

- **Precedence**, from high to low: `()` → `**` → `* / // %` → `+ -` → comparisons → `not` → `and` → `or`.
- `3 + 2 * 4` → `11`, while `(3 + 2) * 4` → `20`.
- `n % 2 == 0` tests for even, `n % 10` gives the last digit, and `n // 10` removes the last digit.

### Assignment

`x += 5` is the same as `x = x + 5`. The same works for `-= *= /= //= %= **=`.

```python
value = 100
value /= 4     # → 25.0   (/ makes it a float, and it stays one)
value //= 3    # → 8.0
value **= 2    # → 64.0
```

### Comparison

`==  !=  >  <  >=  <=` all return a bool.

- `=` **assigns** and `==` **compares**.
- `5 == "5"` → `False` because the types differ.
- Chaining is allowed: `12 <= age <= 17`.

### Logical

| `a` | `b` | `a and b` | `a or b` | `not a` |
|---|---|---|---|---|
| True | True | True | True | False |
| True | False | False | True | False |
| False | True | False | True | True |
| False | False | False | False | True |

- `and` is True only if **both** sides are True. `or` is True if **at least one** is. `not` flips the value.
- **Short-circuit**: in `False and X`, X never runs. In `True or X`, X never runs either.

### Bitwise (work on binary digits)

```python
x, y = 2, 3          # 2 = 0b10, 3 = 0b11
print(x & y)         # → 2   AND
print(x | y)         # → 3   OR
print(x ^ y)         # → 1   XOR
print(~x)            # → -3  NOT: ~x is always -(x+1)
print(x << 1)        # → 4   shift left = ×2
print(x >> 1)        # → 1   shift right = //2
```

### Identity vs equality

- `==` asks whether the **values** are the same. `is` asks whether it's the **same object** in memory.

```python
x = [1, 2, 3]; y = [1, 2, 3]; z = x
print(x == y)    # → True   same values
print(x is y)    # → False  two different objects
print(x is z)    # → True   z is just another name for x
```

- Use `is` for `None`: `if result is None:`

### Membership

`in` and `not in` work on str, list, tuple, set and dict (dicts check the **keys**).

```python
print("D" in "Delhi")      # → True
print("D" not in "Delhi")  # → False
```

---

## 3. Input, Type Conversion, Errors

### input()

`input()` **always returns a string**, so convert it before doing maths.

```python
a = input("Enter a number: ")       # user types 4
b = input("Enter another: ")        # user types 5
print(a + b)                        # → 45   (string concatenation!)
print(int(a) + int(b))              # → 9
age = int(input("Enter your age: "))
```

### Type conversion

- **Implicit** (Python does it for you): `4 + 5.5` → `9.5`, since int is promoted to float. `True + 1` → `2`.
- **Explicit** (you do it): `int()`, `float()`, `str()`, `bool()`, `complex()`, `list()`, `tuple()`, `set()`.

| Call | Result |
|---|---|
| `int("12")` | `12` |
| `int(3.9)` | `3` (truncates, does not round) |
| `int("3.5")` / `int("name")` | **ValueError** |
| `float("3.5")` | `3.5` |
| `str(25)` | `"25"` |
| `list("abc")` | `['a', 'b', 'c']` |

### Truthiness

`bool()` and every `if` or `while` condition follow these rules:

- **Falsy:** `0`, `0.0`, `""`, `[]`, `()`, `{}`, `set()`, `None`, `False`
- **Everything else is truthy**, including `"False"`, `"0"`, `" "` and `[0]`.

```python
print(bool(0), bool(1), bool(""), bool("False"))   # → False True False True
```

### Syntax errors vs runtime errors

| | Syntax error | Runtime error |
|---|---|---|
| When | Before anything runs, because the grammar is broken | While running, when the code is valid but something fails |
| Examples | missing `:` or `)`, missing quote, `1st_place = 5` | `10 / 0`, `int("abc")`, using an undefined variable |
| Names | `SyntaxError`, `IndentationError` | `ZeroDivisionError`, `ValueError`, `NameError`, `TypeError`, `IndexError`, `KeyError` |

The full error table is in Section 18.

---

## 4. Conditionals

```python
if condition:
    ...          # runs if condition is True
elif other:
    ...          # runs only if everything above was False and this is True
else:
    ...          # runs if nothing above matched
```

- **Indentation** (4 spaces) defines the block. Wrong indentation raises `IndentationError`.
- In an `if/elif` chain, the **first True condition wins** and the rest are skipped, so **at most one block runs**.
- Separate `if` statements are **all checked independently**.

```python
# Grades: check from the top down so each elif already knows the earlier checks failed
if score > 90:
    grade = "A"
elif score >= 75:      # here we already know score <= 90
    grade = "B"
elif score >= 60:
    grade = "C"
else:
    grade = "D"
```

```python
# Two independent questions need two separate if blocks
if number == 0:   print("Zero")
elif number > 0:  print("Positive")
else:             print("Negative")

if number % 2 == 0: print("Even")
else:               print("Odd")
```

### Nested if (login example)

```python
email = input("Email: ")
if email != "ugcampus@iimb.ac.in":
    print("Wrong email id")
else:
    password = input("Password: ")
    if password == "new_campus123":
        print("Success")
    else:
        password = input("Wrong password, try once more: ")
        print("Success" if password == "new_campus123" else "Error")
```

### Non-boolean conditions

A condition can be any value, because Python calls `bool()` on it:

```python
if "":    print("T")
else:     print("F")      # → F
if "Hello": print("T")    # → T
if None:  print("T")
else:     print("F")      # → F
```

### Ternary (conditional expression)

```python
parity = "even" if n % 2 == 0 else "odd"
```

### pass

A block can't be empty, so use `pass` as a do-nothing placeholder:

```python
if n % 2 == 0:
    pass
elif n % 3 == 0:
    print(f"{n} is divisible by 3 but not 2")
```

---

## 5. Loops

### range()

| Call | Gives |
|---|---|
| `range(5)` | 0 1 2 3 4 |
| `range(2, 8)` | 2 3 4 5 6 7 (the stop value is **excluded**) |
| `range(0, 10, 2)` | 0 2 4 6 8 |
| `range(10, 0, -2)` | 10 8 6 4 2 |
| `range(20, -1, -5)` | 20 15 10 5 0 (to include 0 when counting down, stop at -1) |

### for: once per item in a sequence

```python
for i in range(3):
    print("Hi", i)          # → Hi 0 / Hi 1 / Hi 2

for ch in "PYTHON":         # strings, lists, tuples, sets, dicts are all iterable
    print(ch)

total = 0                   # ALWAYS initialise the accumulator
for i in range(1, 21):
    total += i
print(total)                # → 210
```

### while: repeats while the condition is True

```python
count = 0
while count < 5:
    print(count)
    count += 1      # without an update the condition never changes: INFINITE LOOP
```

```python
n = 10
while n > 0:
    print(n, end=" ")
    n -= 3          # → 10 7 4 1
```

**for or while?** Use `for` when you know how many times or are walking through a sequence (the table of 7, every character in a sentence). Use `while` when you're repeating *until* something happens (asking for a password until it's correct, rolling a die until you get a 6).

### break and continue

- `break` **exits the loop** immediately.
- `continue` **skips the rest of this iteration** and moves to the next one.

```python
for i in range(1, 20):
    if i % 7 == 0:
        break
    print(i, end=" ")       # → 1 2 3 4 5 6

for i in range(1, 20):
    if i % 3 != 0:
        continue
    print(i, end=" ")       # → 3 6 9 12 15 18
```

### Converting between for and while

```python
for i in range(1, 6):        # for version
    print(i * i)

i = 1                        # equivalent while version
while i <= 5:
    print(i * i)
    i += 1
```

### Useful helpers

```python
for i, fruit in enumerate(["apple", "kiwi"]):          # index and value together
    print(i, fruit)                                     # → 0 apple / 1 kiwi
for rank, name in enumerate(["A", "B"], start=1): ...   # numbering from 1
for d, t in zip(["Mon", "Tue"], [30, 32]): ...          # walk two sequences in parallel

import random
random.randint(1, 100)          # random int, BOTH ends inclusive
random.sample(my_list, 2)       # 2 distinct random items
```

---

## 6. Strings

### Basics

- Quotes can be `'...'`, `"..."`, or `"""..."""` for multi-line strings.
- Escape sequences: `\'` single quote · `\"` double quote · `\n` newline · `\t` tab · `\\` backslash.
- Code points: `ord('A')` → `65`, `ord('a')` → `97`, `ord('4')` → `52`, `chr(65)` → `'A'`. Uppercase letters sort **before** lowercase ones.
- Operators: `"ab" + "cd"` → `"abcd"`, `"ab" * 3` → `"ababab"`, `"a" in "cat"` → `True`, and `"5" + 5` → **TypeError**.

### Indexing

```
 P   Y   T   H   O   N
 0   1   2   3   4   5
-6  -5  -4  -3  -2  -1
```

```python
word = "PYTHON"
word[0], word[-1], word[-2], len(word)    # → 'P', 'N', 'O', 6
word[len(word)//2]                         # middle character → 'H'
"IIMB"[5]                                  # → IndexError: string index out of range
```

### Slicing: `s[start:stop:step]`

The start is included, the stop is **excluded**, and out-of-range slice values **never raise an error**.

```python
word = "PROGRAMMING"
word[0:4]    # → 'PROG'
word[4:]     # → 'RAMMING'
word[:4]     # → 'PROG'
word[::2]    # → 'PORMIG'
word[::-1]   # → 'GNIMMARGORP'   (reverse)
word[2:100]  # → 'OGRAMMING'     (no error)

d = "2026-08-20"
d[0:4], d[5:7], d[8:10]      # → '2026', '08', '20'
year, month, day = d.split("-")

is_palindrome = w == w[::-1]   # "level" → True, "python" → False
```

### Strings are immutable

```python
s = "Hello"
s[0] = "C"      # → TypeError: 'str' object does not support item assignment
del s[0]        # → TypeError
s = s.replace("H", "C")   # OK: replace builds a NEW string and s now points to it (id(s) changes)
```

**Every string method returns a new string. The original never changes.** `s.upper()` on its own line does nothing useful; write `s = s.upper()`.

### Built-in functions on strings

```python
len("karnataka")       # → 9
max("karnataka")       # → 't'  (highest code point)
min("karnataka")       # → 'a'
sorted("cab")          # → ['a', 'b', 'c']   (returns a LIST)
```

### Methods

| Method | Does | Example → result |
|---|---|---|
| `.upper()` `.lower()` | change case | `"Hi".upper()` → `'HI'` |
| `.capitalize()` | first letter only | `'it is raining'` → `'It is raining'` |
| `.title()` | first letter of each word | → `'It Is Raining'` |
| `.swapcase()` | flip the case | `'Hi'` → `'hI'` |
| `.strip()` `.lstrip()` `.rstrip()` | trim whitespace, or the given characters | `"  hi  ".strip()` → `'hi'` |
| `.split(sep)` | break into a **list** (default: any whitespace) | `"a,b".split(",")` → `['a', 'b']` |
| `sep.join(list)` | glue a list into one string | `"-".join(['a','b'])` → `'a-b'` |
| `.replace(old, new)` | replace **all** matches | `"aa".replace("a","b")` → `'bb'` |
| `.find(sub)` | index of first match, **-1 if none** | `"hello".find("l")` → `2` |
| `.count(sub)` | number of occurrences | `"banana".count("a")` → `3` |
| `.startswith()` `.endswith()` | test the start or end | → `True` / `False` |
| `.isalpha()` | only letters? | `"FLAT".isalpha()` → `True` |
| `.isdigit()` `.isdecimal()` | only digits? | `"20".isdigit()` → `True` |
| `.isalnum()` | only letters and digits? | `"FLAT204"` → `True`, `"FLAT20&"` → `False` |
| `.isidentifier()` | valid Python name? | `"Hello World"` → `False`, `"Hello_World"` → `True` |

Method chaining works because each method returns a string: `"   Hello World   ".strip().lower() == "hello world"` → `True`.

### Formatting

```python
name, n = "Sam", 7
print(f"Hi {name}! {n} doubled is {n * 2}.")   # f-string (preferred)
print("The number {} is {}".format(13, "odd"))  # .format()
print(f"{3.14159:.2f}")      # → 3.14   (2 decimal places)
print(f"{5:2}|")             # → " 5|"  (width 2)
print(f"{233:>10}")          # right-align in a width of 10
```

### Mini-programs from class

```python
# Username: first 3 letters of first name + first 3 of last name, lowercase
full = "Aditi Sharma"
first, last = full.split()
print(first[:3].lower() + last[:3].lower())     # → adisha

# Text analyser
p = "Data is everywhere. Learning to work with data is valuable."
len(p)                     # number of characters
len(p.split())             # number of words
p[:20], p[-20:]            # first and last 20 characters
p.lower().count("data")    # case-insensitive count
p.startswith("Data")       # → True

# Is a word present, ignoring case?
"python" in "Python is great".lower().split()    # → True
```

---

## 7. Lists

An **ordered, mutable** collection in `[]`. It allows duplicates and mixed types.

### Create and index

```python
fruits = ["apple", "banana", "cherry", "date", "fig"]
fruits[0], fruits[-1], len(fruits)       # → 'apple', 'fig', 5
mixed  = ["Mark", 16, 5.4, True]
nested = [1, 2, [3, 4, 5]]
nested[2][0]                              # → 3
m = [[[1, 2], [3, 4]], [[5, 6], [7, 8]]]
m[-1][-1][0]                              # → 7
["red", "green", "blue"][3]               # → IndexError: list index out of range
```

### Slicing (same rules as strings)

```python
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
numbers[2:5]    # → [2, 3, 4]
numbers[:3]     # → [0, 1, 2]
numbers[-3:]    # → [7, 8, 9]
numbers[::2]    # → [0, 2, 4, 6, 8]
numbers[::-1]   # → [9, 8, ..., 0]
```

### Traversal

```python
for item in lst:              # by value (most common)
    print(item)
for i in range(len(lst)):     # by index, when you need the position
    print(i, lst[i])
for i, item in enumerate(lst):   # both at once
    ...
```

### Modifying (mutating methods change the list in place and return None)

| Operation | Code | Effect |
|---|---|---|
| Update | `lst[i] = v` | replaces the item; **length unchanged**; IndexError if `i` is out of range |
| Insert | `lst.insert(i, v)` | shifts the rest right; **length + 1**; a too-large `i` just adds at the end (no error) |
| Append | `lst.append(v)` | adds **one** item at the end |
| Extend | `lst.extend(iterable)` | adds **each** item of the iterable |
| Remove by value | `lst.remove(v)` | removes the **first** match; ValueError if absent |
| Remove by index | `lst.pop(i)` / `lst.pop()` | removes **and returns** the item (default: the last one) |
| Delete | `del lst[i]` | removes by index (also works on slices) |
| Empty | `lst.clear()` | → `[]` |
| Sort | `lst.sort()` / `lst.sort(reverse=True)` | sorts in place |
| Reverse | `lst.reverse()` | reverses in place |
| Count / find | `lst.count(v)` / `lst.index(v)` | number of matches / index of first match |

```python
lst = [1, 2, 3]; lst.append([4, 5])   # → [1, 2, 3, [4, 5]]     (length 4)
lst = [1, 2, 3]; lst.extend([4, 5])   # → [1, 2, 3, 4, 5]       (length 5)

items = ["pen", "book", "eraser"]
items.append("ruler")      # ['pen', 'book', 'eraser', 'ruler']
items.insert(0, "pencil")  # ['pencil', 'pen', 'book', 'eraser', 'ruler']
items.remove("book")       # ['pencil', 'pen', 'eraser', 'ruler']
items.pop(1)               # removes 'pen' → ['pencil', 'eraser', 'ruler']
```

### sort() vs sorted()

```python
nums = [3, 1, 2]
new = sorted(nums)     # returns a NEW sorted list; nums is unchanged
nums.sort()            # changes nums itself and returns None
nums = nums.sort()     # ❌ BUG: nums is now None
sorted(nums, reverse=True)
board.sort(key=lambda p: p[1], reverse=True)   # sort [name, score] pairs by score
```

### Functions and operators

```python
len(l), min(l), max(l), sum(l), sorted(l)
[1, 2] + [3, 4]          # → [1, 2, 3, 4]
[0] * 3                  # → [0, 0, 0]
4 in [1, 2, 3, 4]        # → True
[3, 4] in [1, 2, 3, 4]   # → False  (it looks for [3, 4] as a single ELEMENT)
[3, 4] in [1, 2, [3, 4]] # → True
```

### Aliasing vs copying

```python
a = [1, 2, 3]
b = a            # NOT a copy: both names point to the same list
b.append(4)
print(a)         # → [1, 2, 3, 4]   a changed too!
c = a.copy()     # or a[:] or list(a): a real, independent copy
```

### List comprehension

```python
squares = [x**2 for x in nums]                 # build a new list
evens   = [x for x in nums if x % 2 == 0]      # filter
```

---

## 8. Tuples

An **ordered, immutable** collection in `()`. Mixed types and duplicates are allowed.

```python
point = (3, 4)
single = (5,)        # ⚠ a single-item tuple NEEDS the comma; (5) is just the int 5
t = 1, 2, 3          # packing: parentheses are optional
point[0]             # → 3   (indexing and slicing work like lists)
point[0] = 10        # → TypeError: 'tuple' object does not support item assignment
```

### Operations

```python
coords = (10, 20, 30)
len(coords), coords[-1], coords[0:2], 20 in coords   # → 3, 30, (10, 20), True
(1, 2, 3) + (3, 4, 5)     # → (1, 2, 3, 3, 4, 5)
(1, 2) * 3                # → (1, 2, 1, 2, 1, 2)
t = (10, 100, 3, 87, 9, 54.3)
len(t), min(t), max(t), sum(t)   # → 6, 3, 100, 263.3
sorted(t)                 # → [3, 9, 10, 54.3, 87, 100]   ⚠ returns a LIST
t.count(87), t.index(3)   # → 1, 2   (the only two tuple methods)
min((10, 3, "Hello"))     # → TypeError: can't compare str and int
```

### Unpacking

```python
rgb = (255, 0, 100)
red, green, blue = rgb       # the number of names must match, otherwise ValueError
```

### "Changing" a tuple

Convert it to a list, change that, then convert back:

```python
fruits = ("Orange", "Apple")
tmp = list(fruits); tmp.append("Grapes"); fruits = tuple(tmp)
```

### Deleting

You can't remove a single item, but you can delete the whole tuple with `del fruits`. After that, `print(fruits)` raises **NameError**.

### zip pairs items by position and stops at the shortest

```python
tuple(zip((1, 2, 3, 4, 99), (5, 6, 7, 8)))   # → ((1, 5), (2, 6), (3, 7), (4, 8))   99 is dropped
```

### List vs tuple

| | List `[ ]` | Tuple `( )` |
|---|---|---|
| Mutable | Yes | **No** |
| Speed and memory | Slower, more memory | Faster, less memory |
| Use for | data that changes | fixed data: coordinates, records, function returns, dict keys |

Why tuples: immutability protects the data from accidental changes.

---

## 9. Dictionaries

**Key → value** pairs in `{}`. You look values up by key, not by position.

```python
student = {"name": "Bob", "age": 17, "grade": "11th"}
student["name"]                   # → 'Bob'
student["score"]                  # → KeyError: 'score'
student.get("score")              # → None   (safe)
student.get("score", "N/A")       # → 'N/A'  (default value)
```

### Rules

- **No positional indexing.** `d[0]` looks for the *key* `0`.
- **Mutable**, so you can add, change and delete pairs.
- **Keys must be immutable (hashable)**: str, int, float or tuple. `{[1, 2]: "x"}` raises **TypeError: unhashable type: 'list'**.
- **Values can be anything**, including lists, tuples, sets or other dicts.
- **Keys are unique.** If a key repeats, the last value wins: `{"Name": "Nate", "Name": "Paul"}` → `{'Name': 'Paul'}`.
- A tuple key can be accessed as `d[(1, 2, 3)]` or `d[1, 2, 3]`.
- Dicts keep insertion order (Python 3.7+).

### Add, update, delete

```python
s = {"name": "Mark", "age": 17}
s["grade"] = "11th"      # add a new key
s["age"] = 18            # update an existing key
del s["grade"]           # delete a key (KeyError if it's missing)
age = s.pop("age")       # remove the key AND return its value → 18
s.popitem()              # remove the LAST inserted pair
s.clear()                # empty the dict; print(s.clear()) → None
```

### Copying

```python
a = {"age": 17}
b = a            # alias: changes to a show up in b
c = a.copy()     # independent copy
a["age"] = 18
print(b, c)      # → {'age': 18} {'age': 17}
```

### Looping

```python
for key in d:                   # loops over KEYS
    print(key, d[key])
for key, value in d.items():    # key and value together (most useful)
    print(f"{key}: {value}")
list(d.keys()), list(d.values())
"grade" in d                    # checks KEYS only
```

### Nested data

```python
person = {"skills": ["C", "R"], "address": {"street": "Bakshi", "pincode": "560420"}}
person["skills"][0]                      # → 'C'
person["address"]["pincode"]             # → '560420'
person["skills"].append("HTML")          # mutate the list inside the dict
person.get("ship_address", {}).get("street", "Not Found")   # safe chained lookup → 'Not Found'

contacts = {"John": {"phone": "987", "city": "Bengaluru"}}   # dict of dicts
contacts["Kabir"] = {"phone": "901", "city": "Chennai"}       # add a record
contacts["John"]["city"] = "Pune"                             # update a nested field
```

### Built-in functions work on the KEYS

```python
stock = {"Pepsi": 100, "Tropicana": 75, "Slice": 65, "Maaza": 30}
len(stock)                     # → 4
min(stock), max(stock)         # → 'Maaza', 'Tropicana'  (alphabetical KEYS!)
sorted(stock)                  # → ['Maaza', 'Pepsi', 'Slice', 'Tropicana']
sum(stock.values())            # → 270
max(stock, key=stock.get)      # → 'Pepsi'  (the key with the largest VALUE)
min(stock, key=stock.get)      # → 'Maaza'
```

### Building a dict from two lists

```python
days = ["Mon", "Tue"]; temps = [30.5, 32.6]
{d: t for d, t in zip(days, temps)}   # dict comprehension → {'Mon': 30.5, 'Tue': 32.6}
dict(zip(days, temps))                # same result
```

### Tuple vs dict

| | Tuple | Dict |
|---|---|---|
| Accessed by | position | key |
| Mutable | No | Yes |
| Best for | fixed groups: (lat, long), (y, m, d) | labelled records and lookup tables (ID → name) |

---

## 10. Sets

An **unordered** collection of **unique** items in `{}`.

```python
fruits = {"apple", "banana", "apple"}   # → {'apple', 'banana'}  (duplicates dropped)
set([1, 2, 2, 3, 3])                    # → {1, 2, 3}  ← the classic de-duplication trick
empty = set()                           # ⚠ {} creates an empty DICT, not a set
```

### Rules

- **No indexing**: `s[0]` → **TypeError: 'set' object is not subscriptable**. Loop over it, or use `list(s)[0]`.
- **Elements must be immutable**: `{[1, 2], "a"}` and `{{1}, "a"}` raise **TypeError (unhashable)**. Tuples inside a set are fine.
- Order is **not guaranteed**. A printed set may *look* sorted, but don't rely on it.
- `in` checks are **very fast**, much faster than on a list.

### Adding and removing

| Code | Effect |
|---|---|
| `s.add(x)` | add one item (no effect if it's already there) |
| `s.remove(x)` | remove x; **KeyError if missing** |
| `s.discard(x)` | remove x; **no error if missing** |
| `s.pop()` | removes and returns an **arbitrary** item |
| `s.clear()` | → `set()` |
| `del s` | delete the whole set |

### Set operations

```python
a = {1, 2, 3, 4, 5}
b = {4, 5, 6, 7, 8}
a | b     # union: in either         → {1, 2, 3, 4, 5, 6, 7, 8}    a.union(b)
a & b     # intersection: in both    → {4, 5}                      a.intersection(b)
a - b     # difference: in a, not b  → {1, 2, 3}                   a.difference(b)
b - a     #                          → {6, 7, 8}
a ^ b     # symmetric difference: in one but NOT both → {1, 2, 3, 6, 7, 8}   a.symmetric_difference(b)
a.isdisjoint(b)   # → False  (True only if there's nothing in common)
len(a | b)        # number of unique items across both
```

- `isdisjoint()` returns a **bool** and stops at the first common item.
- `intersection()` returns a **new set** and has to scan everything.

### frozenset

An immutable set: `v = frozenset("aeiou")`. Calling `v.add("z")` raises **AttributeError**.

### List vs set

| | List | Set |
|---|---|---|
| Ordered | Yes | No |
| Duplicates | Yes | No |
| Indexable | Yes | **No** |
| `in` speed | slow on big data | very fast |
| Use for | sequences where order or repeats matter | uniqueness, fast lookups, set maths |

---

## 11. Choosing the Right Data Structure

```
Labelled fields (name → value)?             → DICT
Need uniqueness or fast "is X in it?"       → SET
Will the data never change?                 → TUPLE
Otherwise (ordered, changes over time)      → LIST
```

| Structure | Ordered | Duplicates | Mutable | Accessed by |
|---|---|---|---|---|
| List | Yes | Yes | Yes | position |
| Tuple | Yes | Yes | **No** | position |
| Dict | Yes (3.7+) | keys: no | Yes | key |
| Set | No | No | Yes | — (no indexing) |

| Scenario | Pick | Why |
|---|---|---|
| 12 months in order | Tuple | fixed and ordered |
| Users currently online | Set | unique, fast membership check |
| Product catalogue (name, price, stock) | Dict | named fields |
| Hourly temperature log | List | ordered, repeats allowed, grows |
| Unique tags across blog posts | Set | removes duplicates automatically |
| GPS of a fixed landmark | Tuple | fixed pair |
| Shopping cart with repeat items | List | duplicates plus add/remove |
| Book (title, author, ISBN) | Tuple | never changes |
| Country code → name | Dict | lookup by key |
| Top-5 leaderboard with updatable scores | List of `[name, score]` | rank order plus mutable |
| Who has submitted an assignment | Set | no double submissions, fast check |
| Patient record (name, age, blood group) | Dict | named fields |

---

## 12. Functions: Defining and Parameters

```python
def function_name(param1, param2):
    """Docstring: what the function does."""
    statements
    return value          # optional

function_name(arg1, arg2)   # the call
```

- **Defining doesn't run it.** Only calling does.
- You must define a function **before** calling it, otherwise NameError.
- Names are case-sensitive: calling `show_Message()` when you defined `show_message` raises NameError.
- `greet.__doc__` returns the docstring.
- Why use functions: avoid repetition, organise code, easier testing and debugging, reuse. In short: **modularity, reusability, readability**.

### Parameters vs arguments

- **Parameter**: the variable named in the `def` line (`def greet(name)`).
- **Argument**: the actual value passed in the call (`greet("Aditi")`).

### Kinds of arguments

```python
# 1. Positional: matched by ORDER
def describe(name, age): print(name, "is", age)
describe("Aditi", 16)        # → Aditi is 16
describe(16, "Aditi")        # → 16 is Aditi   (wrong order, wrong meaning, no error)

# 2. Default: used when the caller leaves it out
def greet(name, greeting="Hello"):
    print(greeting + ",", name + "!")
greet("Aditi")                    # → Hello, Aditi!
greet("Rohan", "Good morning")    # → Good morning, Rohan!

# 3. Keyword: matched by NAME, so order doesn't matter
greet(greeting="Hi", name="John") # → Hi, John!

# 4. Arbitrary positional: *args is packed into a TUPLE
def product(*numbers):
    p = 1
    for n in numbers: p *= n
    print(p)
product(2, 3, 4)   # → 24
product()          # → 1

# 5. Arbitrary keyword: **kwargs is packed into a DICT
def profile(**kwargs):
    for k, v in kwargs.items(): print(f"{k}: {v}")
profile(name="Alice", age=28)
```

### Required order in a definition

1. positional → 2. defaults → 3. `*args` → 4. keyword-only → 5. `**kwargs`

```python
def f(a, b="x", *args, kw_only, kw_def="y", **kwargs): ...
f(1, 2, 3, 4, kw_only=5, city="L")   # a=1, b=2, args=(3, 4), kw_only=5, kwargs={'city': 'L'}
```

- Anything after `*args` is **keyword-only**, so it must be passed by name.
- A non-default parameter after a default one is a **SyntaxError**: `def bad(name, greeting="Hi", age):`

### Common mistakes

```python
def add(a, b): print(a + b)
add(3, 4, 5)   # → TypeError: takes 2 positional arguments but 3 were given
add(3)         # → TypeError: missing 1 required positional argument: 'b'
def 2_total(): ...   # → SyntaxError (a name can't start with a digit)
```

### Unpacking when calling

```python
order = ("C101", 2450, 6)
process(*order)      # same as process("C101", 2450, 6)
print(*[1, 2, 3])    # → 1 2 3
```

### Worked example

```python
def calculate_price(price, discount=0, tax_rate=0.05):
    d = price - discount
    print(d + d * tax_rate)

calculate_price(100)                     # → 105.0
calculate_price(100, 10)                 # → 94.5
calculate_price(100, 10, 0.10)           # → 99.0
calculate_price(price=200, tax_rate=0.0) # → 200.0
```

---

## 13. Functions: Return, Scope, Nested Functions, First-Class Functions

### return vs print

- `return` **sends a value back** to the caller and **exits the function immediately**.
- A function with no `return` returns **`None`**.

```python
def square_print(n):  print(n * n)
def square_ret(n):    return n * n

print(square_print(2))          # → 4 then None   (the function printed, then returned None)
print(square_ret(4) + square_ret(2))   # → 20     (returned values can be reused)

def compute(a, b):
    return a + b, a * b         # several values come back as a TUPLE
s, p = compute(3, 4)            # → 7, 12
```

### Scope: local, enclosing, global

- **Local**: created inside a function and only exists there.
- **Global**: created at the top level of the program. Any function can **read** it.
- Assigning to a name inside a function creates a **new local variable**, which shadows the global one.

```python
x = 5
def show():
    print(x)        # reading a global is fine → 5
show()

total = 100
def reset():
    total = 0       # NEW local total; the global is untouched
    return total
print(reset(), total)   # → 0 100

count = 0
def bad():
    count += 1      # → UnboundLocalError: assigning makes count local, but it has no value yet

def good():
    global count    # "I mean the global one"
    count += 1
good(); good(); print(count)   # → 2
```

Parameters are local too. Reassigning a parameter doesn't affect the caller's variable:

```python
def f(x):
    x += 1
    print("in f:", x)
    return x
x = 3
z = f(x)          # → in f: 4
print(z, x)       # → 4 3
```

Exception: **mutating** a list or dict that was passed in *does* change the caller's copy, because it's the same object (see aliasing in Section 7).

### Nested functions

A function defined inside another one can only be called from inside it. Calling it from outside raises **NameError**.

The inner function can **read** the outer function's variables (the enclosing scope):

```python
def describe_temperature(celsius):
    def to_fahrenheit():
        return celsius * 9/5 + 32       # reads celsius from the enclosing scope
    return f"{celsius}°C is {to_fahrenheit()}°F"
print(describe_temperature(25))         # → 25°C is 77.0°F
```

Assigning to an outer variable inside the inner function creates a new local, **unless you write `nonlocal`**:

```python
def make_counter():
    count = 0
    def increment():
        nonlocal count      # modify the ENCLOSING variable (global is for module level)
        count += 1
        return count
    print(increment(), increment(), increment())   # → 1 2 3
make_counter()
```

```python
def outer(x):
    def inner(x):
        x += 1
        print("inner:", x)
    x += 1
    print("outer:", x)
    inner(x)
    return x
x = 3
z = outer(x)       # → outer: 4 / inner: 5
print(x, z)        # → 3 4   (inner's change stays inside inner)
```

| Keyword | Lets you modify |
|---|---|
| `global x` | a top-level (module) variable |
| `nonlocal x` | a variable of the enclosing function |

### Functions are objects (first-class functions)

```python
def sq(n): return n ** 2
f = sq                    # alias: no () because we're not calling it
f(4)                      # → 16
type(f)                   # → <class 'function'>
lst = [2, 4, sq]
lst[-1](8)                # → 64   (store it in a list, then call it)
p = print; p("Hello")     # → Hello

def run(z):               # pass a function as an argument
    return z()
run(some_function)        # pass the NAME, not some_function()

def maker():              # return a function
    def add(a, b): return a + b
    return add
maker()(3, 4)             # → 7
```

- `lambda` is a one-line anonymous function: `lambda p: p[1]`. It's mostly used as a `key=` for sorting.

---

## 14. Recursion

A **recursive function calls itself** on a smaller version of the problem. It needs two parts:

1. A **base case**: the simplest input, answered directly with **no** further call.
2. A **recursive case**: a call to itself with input that moves **towards** the base case.

If there's no base case, or it's never reached, you get **RecursionError: maximum recursion depth exceeded** (the limit is about 1000 calls).

```python
def factorial(n):
    if n == 1:                  # base case
        return 1
    return n * factorial(n - 1) # recursive case
```

**Trace** (calls stack up, then unwind):

```
factorial(5) = 5 * factorial(4)
             = 5 * (4 * factorial(3))
             = 5 * (4 * (3 * (2 * factorial(1))))
             = 5 * (4 * (3 * (2 * 1)))  = 120
```

```python
def recursive_sum(n):           # 1 + 2 + ... + n
    if n <= 0: return 0
    return n + recursive_sum(n - 1)
recursive_sum(5)                # → 15

def multiply(a, b):             # a * b by repeated addition
    if b == 1: return a         # ⚠ multiply(a, 0) never reaches b == 1 → RecursionError
    return a + multiply(a, b - 1)
multiply(5, 7)                  # → 35
```

### Where the print goes changes the order

```python
def count_down(n):
    if n == 0:
        print("Liftoff!")
    else:
        print(n)                # print BEFORE the call → on the way down
        count_down(n - 1)
count_down(4)                   # → 4 3 2 1 Liftoff!

def count_up(n):
    if n == 0: return
    count_up(n - 1)
    print(n)                    # print AFTER the call → on the way back up
count_up(4)                     # → 1 2 3 4
```

### Fibonacci

```python
def fib(n):
    if n <= 1:
        return n                    # fib(0)=0, fib(1)=1
    return fib(n - 1) + fib(n - 2)
for i in range(7): print(fib(i), end=" ")   # → 0 1 1 2 3 5 8
```

- **Rabbit problem:** start with one newborn pair. A pair matures in a month and then produces one new pair every month, and none die. Pairs per month: **1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144**. That's 144 pairs in month 12.
- **Why it's slow:** the call tree recomputes the same values again and again (`fib(3)` twice, `fib(2)` three times…), so the time grows **exponentially**. Each +1 to n costs about 1.6× more work.
- **Fix: memoization.** Store each answer the first time it's computed:

```python
memo = {}
def fib_memo(n):
    if n in memo: return memo[n]          # already computed → reuse it
    result = n if n <= 1 else fib_memo(n - 1) + fib_memo(n - 2)
    memo[n] = result
    return result
fib_memo(200)    # instant
```

### Iterative vs recursive

| | Iterative (loop) | Recursive |
|---|---|---|
| How | repeats with `for` or `while` | the function calls itself |
| Stops when | the loop condition fails | the base case is reached |
| Risk | infinite loop | RecursionError, repeated work |

---

## 15. OOP Basics: Classes and Objects

- **Everything in Python is an object.** `[30, 10]` is an object (instance) of the class `list`, which is why it has methods like `.append()` and `.sort()`. `isinstance(x, list)` → `True`.
- **OOP** bundles **data (attributes)** and **behaviour (methods)** together.
- **Class** = blueprint, like a cookie cutter. **Object** = an instance built from it, like a cookie. One class can make many objects, and each has its own attribute values.
- Class names use **CapWords**: `Atm`, `BankAccount`.

```python
class Atm:
    def __init__(self):           # constructor: runs AUTOMATICALLY when an object is created
        self.pin = ""             # attributes live on self
        self.balance = 0

    def create_pin(self):         # a method: its first parameter is ALWAYS self
        self.pin = input("Enter your pin: ")
        print("Pin set successfully")

    def deposit(self):
        temp = input("Enter your pin: ")
        if temp == self.pin:
            amount = int(input("Enter the amount: "))
            self.balance = self.balance + amount
            print("Deposit successful")
        else:
            print("Invalid pin")

    def withdraw(self):
        temp = input("Enter your pin: ")
        if temp == self.pin:
            amount = int(input("Enter the amount: "))
            if amount <= self.balance:
                self.balance = self.balance - amount
                print("Operation successful")
            else:
                print("insufficient funds")
        else:
            print("invalid pin")

    def check_balance(self):
        temp = input("Enter your pin: ")
        if temp == self.pin:
            print(self.balance)
        else:
            print("invalid pin")

    def menu(self):
        while True:
            choice = input("1 create pin / 2 deposit / 3 withdraw / 4 balance / other: exit ")
            if choice == "1":   self.create_pin()     # a method calling another method via self
            elif choice == "2": self.deposit()
            elif choice == "3": self.withdraw()
            elif choice == "4": self.check_balance()
            else:
                print("Thank you for transacting with us.")
                break
```

```python
sbi = Atm()              # create an object; __init__ runs now
hdfc = Atm()
sbi.balance = 5000       # access or change an attribute: object.attribute
print(hdfc.balance)      # → 0   (each object has its OWN attributes)
sbi.deposit()            # call a method: object.method()
Atm.deposit(sbi)         # exactly the same: the object before the dot becomes self
```

| Term | Meaning |
|---|---|
| Class | a blueprint or template |
| Object / instance | a concrete thing made from a class |
| Attribute | data stored on the object (`self.balance`) |
| Method | a function defined in a class; it acts on `self` |
| `__init__` | constructor that sets up the attributes |
| `self` | the specific object the method was called on |

**Common mistakes:**

- Forgetting `self` in the method definition raises `TypeError: menu() takes 0 positional arguments but 1 was given`.
- Writing `balance = 0` instead of `self.balance = 0` creates a local variable that vanishes when the method ends.
- Writing `x = Atm` without `()` gives you the class itself, not an object.

---

## 16. Case Study: Warehouse Order Processing System (OMS)

### Rules (the same in every version)

**Shipping cost** = ₹50 base + ₹8 × distance in km

| Rule | Condition | Labels |
|---|---|---|
| Accept the order | value **> 500** AND items **≥ 1** AND distance **≤ 100** | ACCEPTED / REJECTED |
| Free shipping | value **≥ 2000** OR premium member | FREE / ₹cost |
| Priority | marked priority AND value **≥ 1500** | PRIORITY / STANDARD |
| Special handling | fragile OR items **≥ 10** | SPECIAL / NORMAL |

Watch the boundaries: `> 500` excludes 500 itself, while `≥ 2000`, `≥ 1500`, `≥ 10` and `≤ 100` include their limits.

### v1: one order (variables and conditionals)

```python
customer_id = input("Customer ID: ").strip()
order_value = float(input("Order value: "))
num_items   = int(input("Items: "))
distance    = float(input("Distance (km): "))
is_premium  = input("Premium? (Yes/No): ").strip().lower() in ["yes", "y"]   # Yes/No → bool
is_priority = input("Priority? (Yes/No): ").strip().lower() in ["yes", "y"]
is_fragile  = input("Fragile? (Yes/No): ").strip().lower() in ["yes", "y"]

shipping_cost = 50 + 8 * distance
accepted = order_value > 500 and num_items >= 1 and distance <= 100
status   = "ACCEPTED" if accepted else "REJECTED"
shipping = "FREE" if (order_value >= 2000 or is_premium) else "₹" + str(int(shipping_cost))
process  = "PRIORITY" if (is_priority and order_value >= 1500) else "STANDARD"
handling = "SPECIAL" if (is_fragile or num_items >= 10) else "NORMAL"

# Show 2450.0 as 2450
value_display = int(order_value) if order_value == int(order_value) else order_value
print("=" * 35)
print("ORDER PROCESSING RESULT")
print("=" * 35)
print("Customer \t:", customer_id)
print("Order value \t: ₹" + str(value_display))
print("Status \t:", status)
# ... same for Items, Distance, Shipping, Processing, Handling
```

**Sample:** C104, ₹2450, 6 items, 18 km, Premium = Yes, Priority = No, Fragile = Yes gives **ACCEPTED · FREE · STANDARD · SPECIAL**.

### v2: a batch of orders (lists and an end-of-day report)

```python
all_orders = []                             # master list (a list of lists)
n = int(input("How many orders? "))
for i in range(n):
    # ... collect the same 7 fields ...
    order = [customer_id, order_value, num_items, distance_km, is_premium, is_priority, is_fragile]
    all_orders.append(order)

statuses, shipping_statuses, shipping_costs, processings, handlings = [], [], [], [], []
for order in all_orders:
    customer_id, order_value, num_items, distance_km, is_premium, is_priority, is_fragile = order  # unpack
    # ... apply the 4 rules exactly as in v1 ...
    statuses.append(status)                  # PARALLEL LISTS: index i belongs to all_orders[i]
    shipping_statuses.append(shipping_status)
    shipping_costs.append(shipping_cost)
    # ... print this order's summary ...

# End-of-day report
accepted = rejected = revenue = shipping_total = special = priority = 0
highest_index = 0
for i in range(len(all_orders)):
    value = all_orders[i][1]
    if statuses[i] == "ACCEPTED":
        accepted += 1
        revenue += value                              # revenue counts ACCEPTED orders only
        if shipping_statuses[i] != "FREE":
            shipping_total += shipping_costs[i]       # shipping counts accepted AND non-free only
    else:
        rejected += 1
    if value > all_orders[highest_index][1]:
        highest_index = i                             # track the max by index
    if handlings[i] == "SPECIAL":   special += 1
    if processings[i] == "PRIORITY": priority += 1

print("Total orders:", len(all_orders))
print("Highest-value order:", all_orders[highest_index][0], all_orders[highest_index][1])
```

### Functions version (one job per function, plus composition)

```python
def check_order_status(order_value, num_items, distance_km):
    if order_value > 500 and num_items >= 1 and distance_km <= 100:
        print("Status            : ACCEPTED")
    else:
        print("Status            : REJECTED")

def check_shipping_status(order_value, is_premium, distance_km):
    cost = 50 + 8 * distance_km
    if order_value >= 2000 or is_premium: print("Shipping          : FREE")
    else:                                 print(f"Shipping          : Rs. {cost}")

def check_priority_status(is_priority, order_value): ...
def check_handling_status(is_fragile, num_items): ...
def display_order_info(customer_id, order_value, num_items, distance_km): ...

def process_order(customer_id, order_value, num_items, distance_km, is_premium, is_priority, is_fragile):
    print("=" * 35); print("   ORDER PROCESSING RESULT"); print("=" * 35)
    display_order_info(customer_id, order_value, num_items, distance_km)    # composition:
    check_order_status(order_value, num_items, distance_km)                 # one function
    check_shipping_status(order_value, is_premium, distance_km)             # calls the others
    check_priority_status(is_priority, order_value)
    check_handling_status(is_fragile, num_items)
    print("=" * 35)

test_orders = [("C101", 2450, 6, 18, True, False, True),
               ("C102", 300, 2, 50, False, False, False),
               ("C103", 1600, 12, 30, False, True, False),
               ("C104", 5000, 1, 120, True, True, False),
               ("C105", 800, 0, 10, False, False, False)]
for order in test_orders:
    process_order(*order)          # *order unpacks the tuple into 7 arguments
```

| Order | Status | Shipping | Processing | Handling | Why |
|---|---|---|---|---|---|
| C101 | ACCEPTED | FREE | STANDARD | SPECIAL | premium; fragile |
| C102 | REJECTED | Rs. 450 | STANDARD | NORMAL | value ≤ 500 |
| C103 | ACCEPTED | Rs. 290 | PRIORITY | SPECIAL | 12 items |
| C104 | REJECTED | FREE | PRIORITY | NORMAL | distance > 100 |
| C105 | REJECTED | Rs. 130 | STANDARD | NORMAL | 0 items |

### Zone-based shipping (a tuple of tuples, with an early return)

```python
delivery_zones = ((10, 5), (50, 8), (100, 12))     # (max_km, rate_per_km), checked in order

def calculate_shipping_cost(distance):
    for max_distance, rate in delivery_zones:      # unpack each inner tuple
        if distance <= max_distance:
            return distance * rate                 # return exits at the first matching zone
    return None                                    # beyond every zone

# 5 → 25, 10 → 50, 35 → 280, 50 → 400, 75 → 900, 100 → 1200, 120 → None (out of range)
```

### Inventory Tracker (a dict of dicts)

```python
products = {
    "P101": {"name": "Keyboard",     "category": "Electronics", "price": 1200, "quantity": 15},
    "P102": {"name": "Mouse",        "category": "Electronics", "price": 700,  "quantity": 25},
    "P103": {"name": "Notebook",     "category": "Stationery",  "price": 80,   "quantity": 50},
    "P104": {"name": "Pen",          "category": "Stationery",  "price": 20,   "quantity": 100},
    "P105": {"name": "Water Bottle", "category": "Utility",     "price": 450,  "quantity": 20},
}

plist = list(products.values())     # dicts have no positions, so convert to get "the 3rd product"
plist[0]["name"], plist[2]["price"], plist[-1]["quantity"]    # → Keyboard, 80, 20

for pid, d in products.items():     # display every product
    print(f"{pid} - {d['name']} - ₹{d['price']} - {d['quantity']} units")

for pid, d in products.items():     # restock if FEWER than 20 (so 20 itself is fine)
    if d["quantity"] < 20:
        print(pid, d["name"])       # → P101 Keyboard

total = 0                           # inventory value
for pid, d in products.items():
    total += d["price"] * d["quantity"]
print(total)                        # → 50500

def check_order(pid, qty):          # guard clauses: return early on each failure
    pid = pid.strip().upper()
    if pid not in products:
        return "Product not found"
    if qty > products[pid]["quantity"]:
        return "Insufficient stock"
    return "Order accepted"
```

---

## 17. Code Patterns to Know Cold

```python
# Accumulator (sum)
total = 0
for x in nums: total += x

# Counter
count = 0
for x in nums:
    if x > 50: count += 1

# Max/min tracking: start from the FIRST item, not 0 (0 fails if every value is negative)
highest = nums[0]
for x in nums:
    if x > highest: highest = x

# Max in a dict (track the name too)
best_name, best_score = None, -1
for name, score in gradebook.items():
    if score > best_score:
        best_name, best_score = name, score

# Flag search
found = False
for x in nums:
    if x == target:
        found = True
        break
print("Found!" if found else "Not found")

# Filter into a new list
evens = []
for x in nums:
    if x % 2 == 0: evens.append(x)
evens.sort(reverse=True)

# Remove duplicates but KEEP the order (set() loses the order)
unique = []
for x in raw:
    if x not in unique: unique.append(x)

# Frequency count with a dict
freq = {}
for ch in text:
    freq[ch] = freq.get(ch, 0) + 1

# Sum of digits
n, s = 1234, 0
while n > 0:
    s += n % 10      # last digit
    n //= 10         # remove the last digit
# or: sum(int(d) for d in str(1234))

# Factorial with a loop
fact = 1
for i in range(1, n + 1): fact *= i

# Multiplication table
for i in range(1, 11): print(f"{n} x {i} = {n * i}")

# Sum of evens and odds from 0 to n
ev = od = 0
for i in range(n + 1):
    if i % 2 == 0: ev += i
    else:          od += i

# Keep reading input until a sentinel value (0)
total = count = 0
while True:
    num = int(input("Number (0 to stop): "))
    if num == 0: break
    total += num; count += 1
print(total / count if count > 0 else "No numbers")

# Guessing game
import random
secret = random.randint(1, 100)
guess = int(input("Guess: ")); tries = 1
while guess != secret:
    print("Guess higher" if guess < secret else "Guess lower")
    guess = int(input("Guess: ")); tries += 1
print("Correct in", tries, "attempts")

# Build a list from user input
items = []
for i in range(5): items.append(input("Item: "))

# Doubling until over 100
i = 1
while i <= 100:
    print(i); i *= 2            # → 1 2 4 8 16 32 64
```

---

## 18. Error Reference

| Error | Type | Typical cause |
|---|---|---|
| `SyntaxError` | syntax | missing `:` `)` or quote; a name starting with a digit; non-default parameter after a default one |
| `IndentationError` | syntax | block not indented, or inconsistent indentation |
| `NameError` | runtime | undefined or misspelled variable or function; calling a nested function from outside; using something after `del` |
| `TypeError` | runtime | `"5" + 5`; `s[0] = "x"` on a str or tuple; `s[0]` on a set; list as a dict key or set element; wrong number of arguments; `min()` on mixed str and number |
| `ValueError` | runtime | `int("abc")`; `lst.remove(x)` when x is absent; unpacking the wrong number of values |
| `ZeroDivisionError` | runtime | `x / 0`, `x % 0` |
| `IndexError` | runtime | index ≥ len (lists, strings, tuples) |
| `KeyError` | runtime | `d["missing"]`; `del d["missing"]`; `s.remove(x)` on a set when x is missing |
| `AttributeError` | runtime | calling a method the type doesn't have (`frozenset.add`, `tuple.append`) |
| `UnboundLocalError` | runtime | doing `x += 1` on a global inside a function without `global x` |
| `RecursionError` | runtime | no base case, or the base case is never reached |

---

## 19. Top Traps (rapid revision)

1. `input()` returns a **str**: `"4" + "5"` → `"45"`.
2. `/` always gives a float (`10/2` → `5.0`). `//` floors (`-7//2` → `-4`).
3. `range(a, b)` and slices **exclude** the stop value.
4. `bool("False")` → `True`, `bool("")` → `False`, `bool(0)` → `False`.
5. `5 == "5"` → `False`. Use `==` to compare and `=` to assign.
6. `and` needs both sides True, `or` needs one, and both short-circuit.
7. In an `if/elif` chain only the **first** True branch runs.
8. Forgetting to update the loop variable gives an **infinite** `while` loop.
9. Forgetting to initialise an accumulator gives a NameError, or a stale value in Jupyter.
10. Strings and tuples are **immutable**. String methods return **new** strings.
11. `.find()` returns `-1` when nothing is found.
12. List methods `sort/append/extend/insert/reverse/clear` return **None**. `x = lst.sort()` makes x None.
13. `append([4, 5])` adds **one** item. `extend([4, 5])` adds **two**.
14. `b = a` is an **alias**, not a copy. Use `.copy()` or `a[:]`.
15. `lst[i] = v` replaces (IndexError if out of range). `insert(i, v)` shifts (no error).
16. `remove(v)` removes the **first** match only. `pop()` removes and returns the last item.
17. `(5)` is an int and `(5,)` is a tuple. `sorted(tuple)` returns a **list**.
18. `{}` is an empty **dict**. An empty set is `set()`.
19. Sets have **no indexing** and no guaranteed order. Elements and dict keys must be **immutable**.
20. `d["x"]` raises KeyError when x is missing, while `d.get("x")` returns None.
21. `min`, `max`, `sorted`, `in` and `for` on a dict all work on **keys**. Use `max(d, key=d.get)` for the key with the largest value.
22. Duplicate dict keys: the **last** value wins. Duplicate set items are silently dropped.
23. A function without `return` returns **None**, so `print(f())` shows `None`.
24. Assigning inside a function creates a **local** variable. Use `global` or `nonlocal` to modify an outer one.
25. Default parameters come **after** non-default ones. `*args` is a tuple and `**kwargs` is a dict.
26. Pass functions **without** `()` (`run(f)`). `f()` passes the result instead.
27. Recursion needs a base case **that is reached**.
28. Methods need `self` as their first parameter, and attributes are `self.x`. `obj.m()` is the same as `Class.m(obj)`.
29. `~x` is `-(x+1)`. `x is y` checks for the same object, while `x == y` checks for the same value.
30. Watch rule boundaries such as `> 500` vs `≥ 2000`.

---

## 20. Practice: Predict the Output

Try these first, then check the answers below.

```python
# Q1
print(10 % 3, 2 ** 4, 9 // 2, 9 / 2, 3 + 2 * 4)

# Q2
a, b, c = True, False, True
print(a and (b or c), (a and b) or (not c))

# Q3
for i in range(10, 0, -3):
    print(i, end=" ")

# Q4
s = "Learning Python is fun"
print(s[9:15], s[-3:], s[:-4], s[::-1][:3])

# Q5
s = "Data Science and Python Programming"
print(len(s.split()), s.count("a"), s.find("Science"))

# Q6
nums = [10, 20, 30, 40, 50]
print(nums[-3], nums[0] + nums[-1], nums[1:4])

# Q7
x = [1, 2, 3]
y = x
y.append(4)
z = x.copy()
z.append(5)
print(x, len(z))

# Q8
t = (1, 2, 3)
print(t * 2, (5) * 2, (5,) * 2)

# Q9
d = {"a": 1, "b": 2, "a": 3}
print(d, len(d), d.get("c", 0))

# Q10
s = {3, 1, 3, 2}
print(len(s), s | {4}, s & {1, 9})

# Q11
def f(n):
    print(n * n)
r = f(3)
print(r)

# Q12
x = 5
def g():
    x = 10
    return x
print(g(), x)

# Q13
def outer():
    msg = "Original"
    def inner():
        nonlocal msg
        msg = "Changed"
    inner()
    return msg
print(outer())

# Q14
def h(n):
    if n == 0:
        return 0
    return n + h(n - 2)
print(h(6))

# Q15
def p(n):
    if n == 0:
        return
    p(n - 1)
    print(n, end=" ")
p(3)

# Q16
def first():
    def second(a, b):
        return a * b
    return second
print(first()(3, 4))

# Q17
def calc(a, b=2, *args, **kw):
    print(a, b, args, kw)
calc(1, 5, 6, 7, x=8)
```

### Answers

1. `1 16 4 4.5 11`
2. `True False`
3. `10 7 4 1`
4. `Python fun Learning Python is nuf`
5. `5 4 5`
6. `30 60 [20, 30, 40]`
7. `[1, 2, 3, 4] 5`, because y is an alias of x, so x changed too, while z is a separate copy.
8. `(1, 2, 3, 1, 2, 3) 10 (5, 5)`, because `(5)` is just the int 5.
9. `{'a': 3, 'b': 2} 2 0`, because the last duplicate key wins.
10. `3 {1, 2, 3, 4} {1}`
11. `9` then `None`, because f prints but has no return.
12. `10 5`, because g's x is local and the global is untouched.
13. `Changed`
14. `12` (6 + 4 + 2 + 0)
15. `1 2 3`, because the print happens after the recursive call, on the way back up.
16. `12`
17. `1 5 (6, 7) {'x': 8}`
