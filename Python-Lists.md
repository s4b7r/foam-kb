# Python Lists

## Nested lists

### Transpose

```python
map(list, zip(*a))
```

### Flatten

Using [itertools.chain](https://docs.python.org/3/library/itertools.html#itertools.chain)

```python
from itertools import chain
flat_list = chain(*nested_list)
```

And [some other suggestions](https://stackoverflow.com/a/20112805)
