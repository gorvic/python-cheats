#  Modules: `datetime` & `time`

---

### Core

- `datetime.now(tz=None)` Return current local date and time as datetime. If tz is provided, return current time in the given timezone. Preferred method. 
- `datetime.today()` Return current local date and time as datetime. Equivalent to `datetime.now()` without timezone support. _Legacy_
- `datetime.date()` Return a date object (date only, no time)
- `datetime.time()` Return a time object (time only, no date)
- `datetime.combine(date, time)` Combine date and time objects into a datetime.
- `datetime(year, month, day, hour=0, minute=0, second=0, microsecond=0)` Create a datetime object with specified values.
- `datetime.weekday()` Return day of week as integer, Monday=0 ... Sunday=6.

### Timestamp

- `datetime.timestamp()` Return POSIX timestamp (seconds since epoch).
- `datetime.fromtimestamp(ts)` Convert timestamp to local datetime.
- `datetime.utcfromtimestamp(ts)` Convert timestamp to UTC datetime.

### Parsing & formatting

- `datetime.strftime(format)` Format datetime as string according to format codes.
- `datetime.strptime(string, format)` Parse string into datetime using format codes.

### Time zones

- `datetime.astimezone(tz)` Convert datetime to another timezone.
- `datetime.replace(tzinfo=tz)` Assign timezone without conversion.
- `datetime.now(tz)` Return current datetime with timezone.
- `datetime.isoformat()` Return ISO 8601 string including timezone if present.

### ISO 8601

- `datetime.isoformat()` Return ISO 8601 formatted string including timezone if present.
- `datetime.fromisoformat(string)` Parse ISO 8601 string into datetime.
- `datetime.isoweekday()` Return ISO weekday number (_Monday=1 ... Sunday=7_).
- `datetime.isocalendar()` Return tuple (_ISO year, ISO week number, ISO weekday_).

### Timedelta

- `timedelta(days=0, seconds=0, microseconds=0, milliseconds=0, minutes=0, hours=0, weeks=0)` Represent duration between dates/times.
- `datetime + timedelta` Add duration to datetime.
- `datetime - datetime` Return timedelta difference.

##  Time

- `time.time()` Return current time as seconds since epoch.
- `time.sleep(seconds)` Pause execution for given number of seconds.
- `time.ctime([seconds])` Convert timestamp to readable string.
- `time.localtime([seconds])` Convert timestamp to struct_time in local timezone.
- `time.gmtime([seconds])` Convert timestamp to struct_time in UTC.
- `time.perf_counter()` Return high-resolution timer for performance measurement.

### `strftime` / `strptime` format codes


| Code | Description                                 |
|------|---------------------------------------------|
| %Y   | Year with century (e.g., 2023).             |
| %y   | Year without century (e.g., 23).            |
| %m   | Month as zero-padded decimal number.        |
| %d   | Day of month as zero-padded decimal number. |
| %H   | Hour (24-hour clock).                       |
| %I   | Hour (12-hour clock).                       |
| %M   | Minute.                                     |
| %S   | Second.                                     |
| %A   | Full weekday name.                          |
| %a   | Abbreviated weekday name.                   |
| %B   | Full month name.                            |
| %b   | Abbreviated month name.                     |
| %p   | AM or PM.                                   |



# Module: `random`

---

- `random.randint(a, b)` Return a random integer `N` such that `a <= N <= b` (_inclusive_).
- `random.random()` Return a random float `N` such that `0.0 <= N < 1.0`.
- `random.uniform(a, b)` Return a random float `N` such that `a <= N <= b`.
- `random.randrange(start, stop[, step])` Return a random integer from range(_start, stop, step_). Stop is exclusive.
- `random.choice(seq)` Return a random element from a non-empty sequence.
- `random.choices(population, weights=None, cum_weights=None, k=1)` Return a list of `k` elements chosen with replacement. Supports weighted probability.
- `random.sample(population, k)` Return `k` unique elements chosen without replacement.
- `random.shuffle(x)` Shuffle the list `x` in place. Returns `None`.
- `random.seed(x)` Initialize the random number generator for reproducible results.
- `random.getrandbits(k)` Return an integer with `k` random bits.
- `random.gauss(mu, sigma)` Return a random float from a normal (Gaussian) distribution.
- `random.expovariate(lambd)` Return a random float from an exponential distribution.


# Module: `math`

---

### Constants

- `math.pi`  Mathematical constant π (≈ 3.14159).
- `math.e` Euler’s number (≈ 2.71828).
- `math.tau` Tau constant, equal to 2π (≈ 6.28318).
- `math.inf` Positive infinity.
- `math.nan` Not a Number (NaN).

### Rounding

- `math.ceil(x)` Return the smallest integer `>= x`.
- `math.floor(x)` Return the largest integer `<= x`.
- `math.trunc(x)` Truncate fractional part of `x` (_toward zero_).

### Trigonometry (radians)

- `math.sin(x)` Return sine of `x`.
- `math.cos(x)` Return cosine of `x`.
- `math.tan(x)` Return tangent of `x`.
- `math.asin(x)` Return arcsine of `x`.
- `math.acos(x)` Return arccosine of `x`.
- `math.atan(x)` Return arctangent of `x`.

### Exponential & logarithmic

- `math.exp(x)` Return e raised to the power `x`.
- `math.log(x[, base])` Return logarithm of `x` with given base (_natural log if base not specified_).

### Power & root

- `math.pow(x, y)` Return x raised to the power `y` (_float result_).
- `math.sqrt(x)` Return square root of `x`.

### Other

- `math.fabs(x)` Return absolute value of `x` as float.
- `math.factorial(x)` Return factorial of `x` (_`x` must be non-negative integer_).
- `math.gcd(x, y)` Return greatest common divisor of `x` and `y`.


# String formatting (f-strings)

---

### Numbers

- `f"{value:d}"` Format integer in decimal.
- `f"{value:#x}"` Format integer in hexadecimal with prefix (0x).
- `f"{value:#o}"` Format integer in octal with prefix (0o).
- `f"{value:#b}"` Format integer in binary with prefix (0b).

### Floats

- `f"{value:.2f}"` Format float with 2 decimal places.
- `f"{value:.0%}"` Format as percentage without decimals (_value * 100_).
- `f"{value:<width.precision%}"` Format as percentage with width and precision.

### Alignment (within width)

- `f"{value:<width}"` Left align within given width.
- `f"{value:>width}"` Right align within given width.
- `f"{value:^width}"` Center align within given width.
- `f"{value:=width}"` Align numbers with sign on the left and digits right-aligned.


# Module: `re` (regex)

---

### Capturing

- `re.search(pattern, string[, flags])` Search for the first match. Return Match or None.
- `re.match(pattern, string[, flags])` Match pattern only at the beginning of string.
- `re.fullmatch(pattern, string[, flags])` Match entire string against pattern.
- `re.findall(pattern, string[, flags])` Return list of all non-overlapping matches.
- `re.finditer(pattern, string[, flags])` Return iterator of Match objects for all matches.
- `re.sub(pattern, repl, string[, count, flags])` Replace matches with repl. Optional limit via count.
- `re.split(pattern, string[, maxsplit, flags])` Split string by pattern.

### Match object

- `match.group()` Return entire match.
- `match.group(n)` Return group by index.
- `match.group('name')` Return group by name.
- `match.groups()` Return tuple of all groups.
- `match.groupdict()` Return dict of named groups.
- `match.start()` Return start index of match.
- `match.end()` Return end index of match.

### Groups in patterns

- `(...)` Capture group by index.
- `(?P<name>...)` Capture group by name.
- `(?:...)` Non-capturing group.

### Flags (modifiers)


| Flag            | Alias  | Purpose                                   |
|-----------------|--------|-------------------------------------------|
| `re.IGNORECASE` | `re.I` | Case-insensitive matching.                |
| `re.MULTILINE`  | `re.M` | `^` and `$` match start/end of each line. |
| `re.DOTALL`     | `re.S` | Dot matches newline as well.              |
| `re.VERBOSE`    | `re.X` | Allow whitespace and comments in pattern. |
| `re.ASCII`      | `re.A` | Make `\w`, `\d`, etc. ASCII-only.         |
| `re.UNICODE`    | `re.U` | Unicode matching (_default in Python 3_). |


# File operations

---

### `open()`

`fh = open(file, mode='r', encoding=None)` Open file and return file object.

`with open(file, mode, encoding='utf-8') as fh` Automatically handle file closing.

| Mode | Purpose                     |
|------|-----------------------------|
| `r`  | read (file must exist)      |
| `w`  | write (create or overwrite) |
| `a`  | append (write to end)       |
| `b`  | binary mode                 |
| `+`  | read and write              |

- `fh.read(size=-1)` Read file content (optionally limited by size).
- `fh.readline()` Read one line.
- `fh.readlines()` Read all lines as list.
- `fh.write(data)` Write string to file.
- `fh.seek(offset)` Move cursor to position.
- `fh.tell()` Return current cursor position.
- `fh.close()` Close file.

### Module: `shutil` (file operations)

- `shutil.copy(src, dst)` Copy file.
- `shutil.copytree(src, dst)` Copy directory recursively.
- `shutil.move(src, dst)` Move file or directory.
- `shutil.rmtree(path)` Remove directory recursively.
- `shutil.disk_usage(path)` Return disk usage statistics.
- `shutil.make_archive(base_name, format, root_dir)` Create archive (zip, tar, gztar, etc).
- `shutil.unpack_archive(filename, extract_dir)` Extract archive.

### Module: `pathlib.Path`

`p = pathlib.Path(path)` Create path object.

- `p.exists()` Check if path exists.
- `p.is_file()` Check if file.
- `p.is_dir()` Check if directory.
- `p.read_text(encoding='utf-8')` Read text file.
- `p.write_text(data, encoding='utf-8')` Write text file.
- `p.read_bytes()` Read binary file.
- `p.write_bytes(data)` Write binary file.
- `p.name` File name.
- `p.suffix` File extension.
- `p.parent` Parent directory.
- `p.with_name(name)` Return new path with changed name.
- `p.with_suffix(ext)` Return new path with changed extension.
- `p.rename(target)` Rename/move file.
- `p.iterdir()` Iterate over directory contents.
- `p.mkdir(parents=False, exist_ok=False)` Create directory.
- `p.rmdir()` Remove empty directory.
- `p.absolute()` Return absolute path.
- `p.relative_to(base)` Return relative path.
- `p / "subdir" / "file.txt"` Join paths.
- `p.stat()` Return file metadata.
- `p.stat().st_size` File size.
- `p.stat().st_ctime` Creation time.
- `p.stat().st_mtime` Modification time.


# Strings

---

- `str.encode(encoding='utf-8', errors='strict')` Convert string to bytes.
- `bytes.decode(encoding='utf-8', errors='strict')` Convert bytes to string.

| Errors    | Purpose              |
|-----------|----------------------|
| `strict`  | raise error          |
| `ignore`  | skip invalid data    |
| `replace` | replace invalid data |

- `bytes` Immutable sequence of bytes (0–255).
- `bytearray` Mutable sequence of bytes.
- `bytes(iterable)` Create bytes from integers (0–255).
- `ord(char)` Return Unicode code point of character.
- `chr(code)` Return character from Unicode code.
- `str.lower()` Convert to lowercase.
- `str.casefold()` Aggressive lowercase for case-insensitive comparison (Unicode-safe).


# Module: `sys`

---

- `sys.argv` List of CLI arguments (all strings).
- `sys.exit([code])` Exit program.
- `sys.path` List of module search paths.
- `sys.modules` Dict of loaded modules.
- `sys.modules.keys()` Return loaded module names.
- `sys.builtin_module_names` Tuple of built-in modules.
- `sys.version` Python version string.
- `sys.platform` Platform identifier.


# `pip` - Package installer

---

```
python -m pip <command>
```
or 
```
python
>> pip <command>
```

- `pip list` List installed packages.
- `pip list` List installed packages.
- `pip install package` Install package.
- `pip install package==version` Install specific version.
- `pip install package>=version` Install version or newer.
- `pip install package<=version` Install version or older.
- `pip uninstall package` Remove package.
- `pip freeze` List installed packages with versions.
- `pip freeze > requirements.txt` Save dependencies.
- `pip install -r requirements.txt` Install from file.


# `env` Virtual Environment

---
### Create 
```
python -m venv <dir>
```
### Activate

| Command                      | Shell         |
|------------------------------|---------------|
| `<dir>\Scripts\activate.bat` | Win CMD       |
| `<dir>\Scripts\Activate.ps1` | PowerShell    |
| `source <dir>/bin/activate`  | Linux / macOS |

### Deactivate
```
deactivate
```

# Module: `collections`

---

### `namedtuple` Create tuple subclass with named fields.

```python
from collections import namedtuple

obj = namedtuple(typename, field_names)
```

- `obj.field` Access namedtuple value by field name.
- `obj[index]` Access namedtuple value by index.

### `Counter` Count hashable items from iterable.

```python
from collections import Counter

counter = Counter(iterable)
```

- `counter[item]` Return count for item.
- `counter.items()` Return item/count pairs.
- `counter.most_common()` Return all items sorted by count descending.
- `counter.most_common(n)` Return n most common items.

### `defaultdict` Dictionary with default values

```python
from collections import defaultdict
```

- `defaultdict(default_factory)` Create dict that generates default value for missing keys.
- `defaultdict(list)` Create empty list for missing key.
- `defaultdict(int)` Create 0 for missing key.
- `defaultdict(set)` Create empty set for missing key.

### `UserDict` Base wrapper for custom dictionary behavior.

Create custom dictionary class.
Recommended instead of inheriting directly from dict.

```python
from collections import UserDict

class CustomDict(UserDict):
    ...

custom_dict = CustomDict({...})
```
- `self.data` Internal real dictionary storage.
- `self.data[key] = value` Write value directly to wrapped dictionary.
- `self.get(key)` Safe dictionary value access.

### `UserList` Base wrapper for custom list behavior.

Create custom list class.
Recommended instead of inheriting directly from list.

```python
from collections import UserList

class CustomList(UserList):
    ...

custom_list = CustomList([])
```

- `self.data` Internal real list storage.
- `self.data.append(value)` Append directly to wrapped list.
- `self.data.extend(value)` Extend directly to wrapped list.
- `self.data.remove(value)` Remove directly to wrapped list.

### `UserString` Base wrapper for custom string behavior.

Create custom string class.
Recommended instead of inheriting directly from str.

```python
from collections import UserString

class CustomString(UserString):
    ...

custom_string = CustomString("...")
```

- `self.data` Internal real string storage.


#### Advantages over builtin inheritance

| Compare           |                                            |
|-------------------|--------------------------------------------|
| UserDict vs dict  | Safer customization.                       |
| UserList vs list  | Predictable behavior override.             |
| UserString vs str | Avoid immutable string inheritance issues. |

#### Important notes

UserDict / UserList / UserString store real data in self.data
Main extension point for custom behavior.

Prefer collections wrappers over direct builtin inheritance
Especially for complex overridden behavior.

UserString is mutable through self.data
Unlike normal immutable str.

# Stack, queue 

---

### list

```python
stack = []
```

- `stack.append(x)` Push item to stack.
- `stack.pop()` Pop last item from stack.
- `stack[-1]` Peek top item.
- `not stack` Check if stack is empty.

### collections.deque

```python
from collections import deque
```
#### Create double-ended queue.
```python
queue = deque()
```
#### Create deque from iterable.
```python
queue = deque(iterable)
```
#### Create deque with fixed maximum length.
```python
queue = deque(maxlen=n)
```

- `queue.append(item)` Add item to right side.
- `queue.appendleft(item)` Add item to left side.
- `queue.pop()` Remove and return item from right side.
- `queue.popleft()` Remove and return item from left side.
- `queue[0]` Access first item.
- `queue[-1]` Access last item.
- `len(queue)` Return queue size.


# Module: `decimal`

---

- Create exact decimal number from string.
```python
number = decimal.Decimal("0.1")
```

- Perform exact decimal arithmetic.
```python
number = decimal.Decimal("0.1") + decimal.Decimal("0.2")
```

- Set decimal precision to `n` significant digits.
```python
decimal.getcontext().prec = n
```

- Round Decimal to two decimal places.
```python
number.quantize(decimal.Decimal("0.00"))
```

- Round Decimal using specified rounding mode.
```python
number.quantize(decimal.Decimal("0.00"), rounding=ROUND_DOWN)
```

| Mode              | Purpose                                  |
|-------------------|------------------------------------------|
| `ROUND_FLOOR`     | Round toward negative infinity           |
| `ROUND_CEILING`   | Round toward positive infinity           |
| `ROUND_HALF_DOWN` | Round to nearest; ties go down           |
| `ROUND_HALF_UP`   | Round to nearest; ties go up             |
| `ROUND_UP`        | Round away from zero                     |
| `ROUND_DOWN`      | Round toward zero                        |
| `ROUND_HALF_EVEN` | Round to nearest; ties go to even number |



# Generators

---

- **generator function** - Function containing yield.
- **lazy evaluation** - Generate values one by one without storing full sequence.
- `exception StopIteration` Raised when generator has no more values.
- `for item in generator` Iterate generator safely until exhausted.
- `yield value` Return value and pause generator state.
- `next(generator)` Return next generated value.


# First-class functions

---

- `function_ref = function_name` Store function reference in variable.
- `function_ref()`  Call function through variable.
- `func(arg_func)`  Pass function as argument.
- `return inner_func`  Return function from another function.
- `dict[str, Callable]`  Store functions in dictionary.
- `Callable[[arg_types], return_type]` Type hint for callable object.


# Closures
### functions that remembers variables from outer lexical scope.

---

- Create closure.
```python
def outer(): 
    def inner(): 
        ... 
    return inner
```

- Store returned inner function.
```python
inner_func = outer(...)
```

- Allow inner function to modify variable from outer scope.
```python
nonlocal variable
```

# Currying

---

- Convert multi-argument logic into chain of functions.
```python
def func(a): return inner
```

- Create specialized function with fixed first argument.
```python
curried = func(a)
```

- Call specialized function with remaining argument.
```python
curried(b)
```

# Decorators

---

- `decorator(func)` Function that receives function and returns wrapped function.
- `@decorator` Apply decorator to function.
- `wrapper(*args, **kwargs)` Common wrapper signature for flexible decorators.
- `return func(*args, **kwargs)` Call original function inside wrapper.
- `functools.wraps(func)` Preserve original function metadata.
- `func.**name**` Function name metadata.


# Comprehensions

---

#### `list`

- `[new_item for item in iterable]` Create list from iterable.
- `[new_item for item in iterable if condition]` Create filtered list.
- `[x ** 2 for x in numbers]` Create list of transformed values.

#### `set`

- `{new_item for item in iterable}` Create set from iterable.
- `{new_item for item in iterable if condition}` Create filtered set.

#### `dict`

- `{key: value for item in iterable}` Create dictionary from iterable.
- `{key: value for item in iterable if condition}` Create filtered dictionary.


# lambda

---

- `lambda arguments: expression` Create anonymous one-expression function.
- `lambda x: x * x` One-argument lambda.
- `lambda x, y: x + y` Multi-argument lambda.

# map

---

- `map(function, iterable)` Apply function to each iterable item.
- `map(function, iterable1, iterable2)` Apply function to items from multiple iterables.
- `list(map(...))` Convert map iterator to list.

# filter

---

- `filter(function, iterable)` Keep items for which function returns True.
- `list(filter(...))` Convert filter iterator to list.

# zip

---

- `zip(iterable1, iterable2)` Iterate paired items from multiple iterables.
- `[x + y for x, y in zip(a, b)]` Combine values from two iterables.

# any

---

- `any(iterable)` Return True if at least one item is truthy.
- `any(condition for item in iterable)` Return True if at least one item matches condition.

# all

---

- `all(iterable)` Return True if all items are truthy.
- `all(condition for item in iterable)` Return True if all items match condition.
- `all([])` Returns True for empty iterable.


# Magic methods `__method__`

---

- `a + b` = `a.__add__(b)`
- `print(obj)` = `obj.__str__()`
- `repr(obj)` = `obj.__repr__()`
- `obj[key]` = `obj.__getitem__(key)`
- `obj[key] = value` = `obj.__setitem__(key, value)`

# Object lifecycle

__init__(self, ...)
Object initialization method.

self.attribute = value
Create instance attribute.

self.method()
Call internal methods during initialization.

Initialization logic
Validation, preprocessing, derived fields, logging.

# String representation

__str__(self)
Human-readable object representation.

__repr__(self)
Official/debug representation.

print(obj)
Uses __str__().

str(obj)
Uses __str__().

repr(obj)
Uses __repr__().

Interactive console
Usually displays __repr__() result.

Fallback behavior
If __str__ is absent, Python uses __repr__.

# Good __repr__ practice

__repr__
Should ideally recreate object.

eval(repr(obj))
Can reconstruct object if representation is valid Python code.

return f"Point(x={self.x}, y={self.y})"
Typical constructor-like representation.

eval()
Dangerous with untrusted input.

# Container behavior

__getitem__(self, key)
Customize object[key] access.

__setitem__(self, key, value)
Customize object[key] assignment.

self.__data
Private internal storage convention.

Custom containers
Can mimic dict/list behavior.

# UserList / UserDict

UserList
Wrapper for custom list behavior.

UserDict
Wrapper for custom dictionary behavior.

super().__setitem__(...)
Reuse base container implementation.

self.data
Internal wrapped storage.

Prefer UserList/UserDict
Instead of direct list/dict inheritance.

#### Operator overloading

Operator overloading
Redefine operator behavior for custom classes.

#### Math operators

| method                      | operator    |
|-----------------------------|-------------|
| `__add__(self, other)`      | `+`         | 
| `__sub__(self, other)`      | `-`         | 
| `__mul__(self, other)`      | `*`         | 
| `__rmul__(self, other)`     | Reverse `*` | 
| `__truediv__(self, other)`  | `/`         | 
| `__floordiv__(self, other)` | `//`        | 
| `__mod__(self, other)`      | `%`         | 
| `__pow__(self, other)`      | `**`        | 

#### Comparison operators

| method                | operator |
|-----------------------|----------|
| `__eq__(self, other)` | `==`     |         
| `__ne__(self, other)` | `!=`     | 
| `__lt__(self, other)` | `<`      |  
| `__le__(self, other)` | `<=`     | 
| `__gt__(self, other)` | `>`      |  
| `__ge__(self, other)` | `>=`     | 

Correct unsupported comparison behavior.
```python
return NotImplemented
```

# @property

`@property`
Getter. Create accessed like attribute.
Controls read access.

@field.setter
Setter. Create for same property.
Controls write access and validation.

self._field
Protected attribute convention.

self.__field
Private attribute convention.

# Property validation pattern

self.__value = None
Initialize internal field safely.

self.value = value
Use setter inside __init__.

Setter validation
Single centralized validation point.

raise ValueError(...)
Reject invalid assignments.

# Encapsulation

Encapsulation
Hide internal implementation details.

Properties
Expose controlled public API.

Internal fields
Should not be modified directly externally.

# Static methods

@staticmethod
Method without self or cls.

Static method
Utility/helper related to class.

Class.method(...)
Preferred static method call style.

No instance state access
Cannot use self.

# Class methods

@classmethod
Method receiving cls automatically.

cls
Current class reference.

return cls(...)
Factory constructor pattern.

Alternative constructor
Common classmethod usage.

from_string(cls, value)
Typical parsing factory pattern.

# staticmethod vs classmethod

`@staticmethod`
No access to class or instance state.
Utility/helper functions.

`@classmethod`
Access to class via cls.
Factories, alternate constructors, polymorphic creation.

# OOP design notes

Magic methods
Integrate custom classes with Python syntax.

Operator overloading
Improves readability and expressiveness.

@property
Cleaner than explicit get_/set_ methods.

UserList/UserDict
Safer than inheriting builtin containers directly.

NotImplemented
Preferred over manual TypeError in comparisons.
::: 
