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