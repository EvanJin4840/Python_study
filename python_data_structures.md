## List [ ] - Mutable Sequence

* definition: Ordered collection that can be changed. (changeable mixed box)

- Key features:
```python
# Mixed data types are allowed
mixed = [10, "hello", 3.14, True, [1, 2]]

# Indexing (0-based)
mixed[0]     # 10
mixed[-1]    # [1, 2]

# Slicing
mixed[0:2]   # [10, 'hello']
mixed[::-1]  # reverse order

# Mutable operations
mixed[1] = "world"     # Change ✓
mixed.append(99)       # Add ✓  
mixed.extend([4, 5])   # Add multiple ✓
```

## Tuple ( ) - Immutable Sequence

* Definition: Ordered collection that cannot be changed. Faster than list. (fixed mixed box)

- Key features:
```python
# Mixed data types are allowed
point = (10, "hello", 3.14, True)

# Read-only access
point[0]     # 10 ✓
point[1:]    # ('hello', 3.14, True)

# Immutable!
point[0] = 20  # TypeError ❌
```

| Feature     | List [ ]             | Tuple ( )             |
| ----------- | -------------------- | --------------------- |
| Mixed Types | ✅ int+str+float+list | ✅ int+str+float       |
| Mutable     | ✅ Change/Add/Delete  | ❌ Read-only           |
| Speed       | Slower               | Faster                |
| Use Case    | Editable data        | Fixed data, dict keys |

- Both can nest lists. The outer container's mutability controls whether you can replace the inner list, but inner lists remain mutable regardless.

## Dictionary {key: value} - Mutable Mapping

* Definition: Key-value pairs storing mutable mapping. Insertion order preserved (Python 3.7+)

- Key features:
- Mutable: x[1] = "new" ✓
- Keys must be immutable: str, int, tuple (list not allowed)  
- Values can be any type: int, str, list, dict, etc.
- Ordered (3.7+): Maintains insertion order

```python
# Basic creation  
x = {1: "paul", 2: "peter", 3: "john"}  # Lecture example
print(x[2])         # "peter" (access by key)
print(type(x))      # <class 'dict'>

# Add/Change
x[3] = "james"      # {1: 'paul', 2: 'peter', 3: 'james'}
x[5] = "andy"       # {1: 'paul', 2: 'peter', 3: 'james', 5: 'andy'}

# Delete
del x[3]            # {1: 'paul', 2: 'peter', 5: 'andy'}

# Methods
print(x.get(2))     # "peter" (returns None if key missing)
print(x.items())    # dict_items([(1, 'paul'), (2, 'peter'), (5, 'andy')])
```

| Feature    | List [ ]        | Tuple ( )  | Dict { }          |
| ---------- | --------------- | ---------- | ----------------- |
| Access     | Index x[0]      | Index x[0] | Key x['key']      |
| Mutable    | ✅               | ❌          | ✅                 |
| Ordered    | ✅               | ✅          | ✅ (3.7+)          |
| Duplicates | Allowed         | Allowed    | Keys unique       |
| Use Case   | Sequential data | Fixed data | Key-value mapping |

#### Python Data Types in Containers

| Container | Keys (Immutable only)            | Values (Any type)                                 |
| --------- | -------------------------------- | ------------------------------------------------- |
| List [ ]  | N/A                              | int, str, float, bool, list, tuple, dict          |
| Tuple ( ) | N/A                              | int, str, float, bool, list, tuple, dict          |
| Dict { }  | int, str, tuple, bool, frozenset | int, str, float, bool, list, tuple, dict          |
| Set { }   | N/A                              | int, str, tuple, bool, frozenset (immutable only) |