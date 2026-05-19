# Python `Enum` Cheat-Sheet (Python 3.11+)

---

# Basic Usage

```python
from enum import Enum

class Color(Enum):
    RED = 1
    GREEN = 2
    BLUE = 3
```

---

# Accessing Members

```python
Color.RED
```

```python
<Color.RED: 1>
```

---

# Member Properties

```python
Color.RED.name
# 'RED'

Color.RED.value
# 1
```

---

# Comparison

## Identity Comparison

✅ Recommended:

```python
color is Color.RED
```

---

## Equality Comparison

```python
color == Color.RED
```

Also valid.

---

# Enum Iteration

```python
for color in Color:
    print(color)
```

---

# Getting Enum from Value

```python
Color(1)
# Color.RED
```

---

# Getting Enum from Name

```python
Color["RED"]
# Color.RED
```

---

# String Representation

```python
str(Color.RED)
# 'Color.RED'

repr(Color.RED)
# '<Color.RED: 1>'
```

---

# `auto()`

Automatically generates values.

```python
from enum import Enum, auto

class Status(Enum):
    PENDING = auto()
    RUNNING = auto()
    DONE = auto()
```

Generated values:

```python
1
2
3
```

---

# `StrEnum` (Python 3.11+)

Enum where members behave like strings.

```python
from enum import StrEnum

class LogLevel(StrEnum):
    INFO = "info"
    ERROR = "error"
```

---

## Benefits

```python
isinstance(LogLevel.INFO, str)
# True
```

Useful for:

- JSON
- APIs
- configs
- CLI arguments
- serialization

---

# `IntEnum`

Enum compatible with integers.

```python
from enum import IntEnum

class HttpCode(IntEnum):
    OK = 200
    NOT_FOUND = 404
```

---

## IntEnum Comparison

```python
HttpCode.OK == 200
# True
```

⚠ Regular `Enum` does NOT behave like this.

---

# `Flag`

Bitmask-style enum.

```python
from enum import Flag, auto

class Permission(Flag):
    READ = auto()
    WRITE = auto()
    EXECUTE = auto()
```

---

# Combining Flags

```python
perm = Permission.READ | Permission.WRITE
```

---

# Checking Flags

```python
Permission.READ in perm
# True
```

---

# `IntFlag`

Combination of:

- `Flag`
- `int`

Useful for:

- bitmasks
- OS flags
- permissions
- binary protocols

---

# Aliases

```python
class Status(Enum):
    OK = 200
    SUCCESS = 200
```

---

## Alias Behavior

```python
Status.OK is Status.SUCCESS
# True
```

---

# Preventing Aliases

```python
from enum import unique

@unique
class Status(Enum):
    OK = 200
    SUCCESS = 200  # ERROR
```

---

# Custom Methods

```python
class Status(Enum):
    ACTIVE = 1
    DISABLED = 2

    def is_active(self) -> bool:
        return self is Status.ACTIVE
```

---

# Custom Properties

```python
class HttpCode(IntEnum):
    OK = 200
    NOT_FOUND = 404

    @property
    def is_error(self) -> bool:
        return self >= 400
```

---

# Enum with Multiple Values

```python
class HttpStatus(Enum):
    OK = (200, "Success")
    NOT_FOUND = (404, "Not Found")

    def __init__(
        self,
        code: int,
        message: str,
    ) -> None:
        self.code = code
        self.message = message
```

---

# Lookup Tables

```python
class MimeType(StrEnum):
    JSON = "application/json"
    HTML = "text/html"
```

Very common for:

- MIME types
- config values
- API constants
- CLI choices

---

# Enum Membership

```python
Color.RED in Color
# True
```

---

# `__members__`

Returns all enum members.

```python
Color.__members__
```

```python
{
    'RED': <Color.RED: 1>,
    'GREEN': <Color.GREEN: 2>,
    'BLUE': <Color.BLUE: 3>,
}
```

---

# Common Patterns

## Getting All Names

```python
Color.__members__.keys()
```

---

## Getting All Values

```python
[color.value for color in Color]
```

---

## Joining Enum Names

```python
"|".join(Color.__members__)
```

Result:

```python
'RED|GREEN|BLUE'
```

---

# Pattern Matching

```python
match status:
    case Status.ACTIVE:
        ...
    case Status.DISABLED:
        ...
```

---

# Serialization

## JSON-Friendly Enum

```python
class LogLevel(StrEnum):
    INFO = "info"
    ERROR = "error"
```

Recommended for APIs.

---

# Production Recommendations

## Prefer `StrEnum`

For:

- APIs
- configs
- JSON
- CLI
- serialization

---

## Prefer `IntEnum`

For:

- status codes
- protocol constants
- interoperability with integers

---

## Prefer `Flag` / `IntFlag`

For:

- permissions
- bitmasks
- binary flags

---

# Best Practices

## Use UPPER_CASE Names

```python
class Status(Enum):
    ACTIVE = 1
```

---

## Prefer Explicit Values

Especially in public APIs.

---

## Avoid Magic Strings

❌ Bad:

```python
if status == "active":
```

✅ Good:

```python
if status is Status.ACTIVE:
```

---

## Prefer `is` for Comparison

```python
status is Status.ACTIVE
```

---

## Use `@unique`

When aliases are unwanted.

---

## Keep Enum Focused

Enums should represent:

- finite states
- constants
- categories
- modes
- flags

---

# Quick Reference

| Type      | Purpose                 |
|-----------|-------------------------|
| `Enum`    | generic enum            |
| `StrEnum` | string-compatible enum  |
| `IntEnum` | integer-compatible enum |
| `Flag`    | bitmask enum            |
| `IntFlag` | integer bitmask enum    |
| `auto()`  | automatic values        |
| `@unique` | prevent aliases         |

---

# Typical Modern Recommendation

## API / JSON / Configs

```python
from enum import StrEnum

class Status(StrEnum):
    ACTIVE = "active"
    DISABLED = "disabled"
```

---

## Internal Constants

```python
from enum import Enum, auto

class State(Enum):
    IDLE = auto()
    RUNNING = auto()
    STOPPED = auto()
```

---

## Permissions / Flags

```python
from enum import IntFlag, auto

class Permission(IntFlag):
    READ = auto()
    WRITE = auto()
    EXECUTE = auto()
```