# Python

- [Python](#python)
	- [f strings](#f-strings)
	- [importlib](#importlib)
	- [Code tags](#code-tags)
		- [Mnemonics](#mnemonics)
		- [Fields](#fields)
	- [`__repr__` vs `__str__`](#__repr__-vs-__str__)
	- [property decorator](#property-decorator)
	- [class membery type hinting](#class-membery-type-hinting)
	- [Testing: pytest](#testing-pytest)
		- [Warnings in output](#warnings-in-output)
		- [Test parameterization](#test-parameterization)
		- [Asserting exceptions](#asserting-exceptions)
		- [Logging inside of test functions](#logging-inside-of-test-functions)
		- [Get log messages form units under test](#get-log-messages-form-units-under-test)
		- [Assertions about NumPy arrays](#assertions-about-numpy-arrays)
	- [multiprocessing](#multiprocessing)
	- [GUI](#gui)
	- [Variable scopes](#variable-scopes)

Use [[conda]] for managing Python environments with different packages / versions of packages.

[[Python-Lists.md]] got their own page

## f strings

Nice one for debugging:

```python
>>> x = 12
>>> print(f'{x=}')

x=12
```

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

Get's more Python-specific by referencing [PEP 0350](https://www.python.org/dev/peps/pep-0350/#mnemonics)

The official (by PEP) syntax is `# MNEMONIC: Some (maybe multi-line) commentary. <field field ...>`

### Mnemonics

This list contains only what I use and tries to be sorted by (my) priority.

Tag    | Meaning
-------|----------------------------------------------------------------------------------------------------------
!!!    | In need of immediate attention.
BUG    | Defects
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

### Fields

Useful fields could be:

- `AAA[,BBB]...`
  - List of Originator or Assignee initials
  - (the context determines which unless both should exist).
  - It is also okay to use usernames such as MicahE instead of initials.
  - Initials (in upper case) are the preferred form.
- `YYYY[-MM[-DD]]`
  - The Origination Date indicating when the comment was added,
  - in ISO 8601 [2] format (digits and hyphens only)

## `__repr__` vs `__str__`

Implement `__repr__` for any class you implement. This should be second nature. Implement `__str__` if you think it would be useful to have a string version which errs on the side of readability. quoting https://stackoverflow.com/a/2626364

## property decorator

- getter: `@property`
- setter: `@<PROPERTY NAME>.setter`
- deleter: `@<PROPERTY NAME>.deleter`

```python
class House:

	def __init__(self, price):
		self._price = price

	@property
	def price(self):
		return self._price
	
	@price.setter
	def price(self, new_price):
		if new_price > 0 and isinstance(new_price, float):
			self._price = new_price
		else:
			print("Please enter a valid price")

	@price.deleter
	def price(self):
		del self._price
```

quoting https://www.freecodecamp.org/news/python-property-decorator/

## class membery type hinting

```python
class DataAnalyzer:
    train_data: pd.DataFrame
    test_data: pd.DataFrame

    def __init__(self, train_data, test_data):
        self.train_data = train_data
        self.test_data = test_data
```

see: https://stackoverflow.com/a/59784221

## Testing: pytest

I like [pytest](https://docs.pytest.org/)

### Warnings in output

Suppressing output of warnings: https://docs.pytest.org/en/stable/warnings.html or take [this StackOverflow answer](https://stackoverflow.com/a/58645998). Especially consider

    However, you might apparently still get the warning if it happens during an import of a package outside of a test function. In this case you might need to specify the filter globally as a pytest's argument:

`pytest -W "ignore::DeprecationWarning" ./tests/`

The filter is given by Python's syntax: [Here](https://docs.python.org/3.7/library/warnings.html#describing-warning-filters) and [here  ](https://docs.python.org/3.7/library/warnings.html#warning-filter)

### Test parameterization

Test parameterization is nice: see [this StackOverflow answer](https://stackoverflow.com/a/48360839). And it works with Python's itertools as well: see [here](https://stackoverflow.com/a/22390931)

### Asserting exceptions

[pytest.raises](https://docs.pytest.org/en/reorganize-docs/new-docs/user/pytest_raises.html) and a [little guide](https://dev.to/wangonya/asserting-exceptions-with-pytest-8hl) about it

```python
def test_zero_division():
    with pytest.raises(ZeroDivisionError) as ex:
        1 / 0
    assert str(ex.value) == 'SOME STRING I WANT' # optional
```

### Logging inside of test functions

Use Python's [logging module](https://docs.python.org/3/library/logging.html) as usual and set pytest CLI options `-o log_cli=true` and `--log-cli-level=DEBUG`. See also pytest's doc on [Live Logs](https://docs.pytest.org/en/latest/how-to/logging.html?highlight=live%20logs)

### Get log messages form units under test

Provide [`caplog` fixture](https://docs.pytest.org/en/6.2.x/logging.html#caplog-fixture) to test function and set desired loglevel:

```python
def test_foo(caplog):
    caplog.set_level(logging.DEBUG)
    pass
```

### Assertions about NumPy arrays

To check for equality do not use some kind of the usual `assert arrayX == arrayY` but NumPy's [assert_array_equal](https://numpy.org/doc/stable/reference/generated/numpy.testing.assert_array_equal.html).

## multiprocessing

The `multiprocessing` module produces some headaches with Jupyter Notebooks; at least on Windows. It is necessary to have the usual `if __name__ == '__main__'` stuff **and** import the worker function (e.g. the one used in a `pool.map()` call) from a separate file. The worker can't be defined in the interactive terminal / Jupyter Notebook.

See https://medium.com/@grvsinghal/speed-up-your-python-code-using-multiprocessing-on-windows-and-jupyter-or-ipython-2714b49d6fac

## GUI

[[tkinter]]

## Variable scopes

LEGB Rule.

L, Local — Names assigned in any way within a function (def or lambda)), and not declared global in that function.

E, Enclosing-function locals — Name in the local scope of any and all statically enclosing functions (def or lambda), from inner to outer.

G, Global (module) — Names assigned at the top-level of a module file, or by executing a global statement in a def within the file.

B, Built-in (Python) — Names preassigned in the built-in names module : open,range,SyntaxError,...


Blöcke, z.B. for, while, with, ..., haben keinen eigenen Scope. 

[//begin]: # "Autogenerated link references for markdown compatibility"
[conda]: conda.md "conda"
[Python-Lists.md]: Python-Lists.md "Python Lists"
[tkinter]: tkinter.md "tkinter"
[//end]: # "Autogenerated link references"
