# python

Use [[conda]] for managing Python environments with different packages / versions of packages.

## importlib

`import` won't reload an already loaded Python module by default. To reload use:

```python
>>> import importlib
>>> importlib.reload(mod)
```

Source: https://realpython.com/lessons/reloading-module/

## Code tags

*Not really Python-specific but anyway, here you go*

Personally, I use code tags for code details that need to be improved. So tags are a sign of further work.

Tag    | Meaning
-------|----------------------------------------------------------------------------------------------------------
BUG    | Defects
!!!    | In need of immediate attention.
TODO   | tasks/features that are pending completion.
HACK   | Temporary code to force inflexible functionality, or simply a test change, or workaround a known problem.
FIXME  | In need of refactoring or cleanup: Areas of problematic or ugly code.
RFE    | Requests For Enhancement: Roadmap items not yet implemented.
???    | Questions: Misunderstood details.
TODOC  | Needs Documentation
CAVEAT | Implementation details/gotchas that stand out as non-intuitive.
IDEA   | Possible RFE candidates
PORT   | Workarounds specific to OS, Python version, etc.
NOTE   | Sections which need discussion or further investigation.
SEE    | Pointers to other code, web link, etc.

<br>

Get's more Python-specific by referencing [PEP 0350](https://www.python.org/dev/peps/pep-0350/#mnemonics)

## Testing

I like [pytest](https://docs.pytest.org/)

### Warnings in output

Suppressing output of warnings: https://docs.pytest.org/en/stable/warnings.html or take [this StackOverflow answer](https://stackoverflow.com/a/58645998). Especially consider

    However, you might apparently still get the warning if it happens during an import of a package outside of a test function. In this case you might need to specify the filter globally as a pytest's argument:

`pytest -W "ignore::DeprecationWarning" ./tests/`

The filter is given by Python's syntax: [Here](https://docs.python.org/3.7/library/warnings.html#describing-warning-filters) and [here  ](https://docs.python.org/3.7/library/warnings.html#warning-filter)

### Test parameterization

Test parameterization is nice: see [this StackOverflow answer](https://stackoverflow.com/a/48360839). And it works with Python's itertools as well: see [here](https://stackoverflow.com/a/22390931)
