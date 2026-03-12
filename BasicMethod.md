#### Some basic methods related to Strings

1. str(): convert value to string
str(3.5)        # '3.5'
str(10)         # '10'
str(True)       # 'True'

2. Indexing: z[i]  (0-based)
z = "hello world"
z[0]            # 'h'
z[4]            # 'o'
z[-1]           # 'd'  (last character)

3. Slicing: z[start:end]
z[0:5]          # 'hello'   (0 ~ 4)
z[6:11]         # 'world'   (6 ~ 10)
z[:5]           # 'hello'   (start omitted → from 0)
z[6:]           # 'world'   (end omitted → to end)
z[::2]          # 'hlowrd'  (step 2)

### Immutability of Strings (e.g., x = 'X' # illegal)
- Strings in Python are immutable, which means once you create a string, you cannot change its characters in place.
- So if x is a string, doing x[3] = 'X' tries to modify the 4th character of x, and Python will raise a TypeError because strings do not allow item assignment.

- If you want to “change” a character, you must create a new string, for example:

```python 
x = "hello"
x = x[:3] + "X" + x[4:]   # result: "helXo"
```