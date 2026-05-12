# Python `dataclass` Cheat-Sheet (Python 3.11+)

---

# Basic Usage

```python
from dataclasses import dataclass

@dataclass
class User:
    name: str
    age: int
```

Automatically generates:

- `__init__`
- `__repr__`
- `__eq__`

---

# `__post_init__`

`dataclass` usually generates `__init__` automatically.

`__post_init__` is a post-constructor hook called automatically **after the generated `__init__` finishes**.

Use it for:

- validation
- normalization
- derived fields
- dependent initialization
- working with `InitVar`

```python
from dataclasses import dataclass

@dataclass
class User:
    name: str

    def __post_init__(self) -> None:
        self.name = self.name.strip()
```

Conceptually, this is similar to:

```python
def __init__(self, name: str) -> None:
    self.name = name
    self.__post_init__()
```

## Important

`__post_init__` is called automatically only when `dataclass` generates `__init__`.

If you define your own `__init__`, `__post_init__` will NOT be called automatically.

```python
@dataclass
class User:
    name: str

    def __init__(self, name: str) -> None:
        self.name = name

    def __post_init__(self) -> None:
        self.name = self.name.strip()
```

In this case, `__post_init__` is ignored unless you call it manually.

## With `frozen=True`

For frozen dataclasses, use `object.__setattr__()` inside `__post_init__`:

```python
from dataclasses import dataclass

@dataclass(frozen=True)
class User:
    name: str

    def __post_init__(self) -> None:
        object.__setattr__(
            self,
            "name",
            self.name.strip(),
        )
```

## With `InitVar`

`InitVar` values are passed into `__post_init__`, but are not stored as instance fields.

```python
from dataclasses import dataclass, InitVar, field

@dataclass
class Config:
    raw_port: InitVar[str]
    port: int = field(init=False)

    def __post_init__(self, raw_port: str) -> None:
        self.port = int(raw_port)
```

---

# Main `@dataclass` Parameters

```python
@dataclass(
    init=True,
    repr=True,
    eq=True,
    order=False,
    unsafe_hash=False,
    frozen=False,
    match_args=True,
    kw_only=False,
    slots=False,
    weakref_slot=False,
)
```

---

# `frozen=True`

Makes object immutable-ish.

```python
@dataclass(frozen=True)
class Point:
    x: int
    y: int
```

```python
p = Point(1, 2)

p.x = 10
# FrozenInstanceError
```

## Use Cases

- immutable objects
- hashable objects
- dictionary keys
- value objects
- DTOs

---

## Important Note

`frozen=True` does NOT protect nested mutable objects:

```python
@dataclass(frozen=True)
class Data:
    items: list[int]

d = Data([1, 2])

d.items.append(3)  # VALID
```

---

## Proper Way to "Modify" Frozen Object

```python
from dataclasses import replace

p2 = replace(p, x=10)
```

---

# `slots=True`

Generates `__slots__`.

```python
@dataclass(slots=True)
class User:
    name: str
    age: int
```

---

# Benefits

## Lower Memory Usage

Especially important for:

- millions of objects
- parsers
- DTO/models
- AST nodes
- caches

---

## Faster Attribute Access

---

## Prevents Random Attributes

```python
u.test = 123
# AttributeError
```

---

# Downsides

## No `__dict__`

```python
u.__dict__
# AttributeError
```

---

## More Complex Inheritance

---

## Some Older Libraries Do Not Work Well with Slots

---

# Recommended Modern Combination

```python
@dataclass(
    frozen=True,
    slots=True,
    kw_only=True,
)
class Config:
    host: str
    port: int
```

---

# `order=True`

Generates:

- `__lt__`
- `__le__`
- `__gt__`
- `__ge__`

```python
@dataclass(order=True)
class Point:
    x: int
    y: int
```

```python
Point(1, 2) < Point(2, 0)
# True
```

---

# `kw_only=True`

Makes all constructor arguments keyword-only.

```python
@dataclass(kw_only=True)
class User:
    name: str
    age: int
```

```python
User(name="John", age=30)
```

NOT:

```python
User("John", 30)
```

---

# `unsafe_hash=True`

Force-generates `__hash__`.

⚠ Use carefully.

Usually:

- mutable object → NOT hashable
- frozen object → hashable

---

# `match_args=True`

Enables `match/case` support.

```python
match user:
    case User(name, age):
        ...
```

---

# `weakref_slot=True`

Adds `weakref` support.

Only useful together with `slots=True`.

---

# `field(...)`

```python
from dataclasses import field
```

---

# `default`

```python
count: int = field(default=0)
```

---

# `default_factory`

For mutable values.

✓ CORRECT:

```python
items: list[str] = field(default_factory=list)
```

✗ WRONG:

```python
items: list[str] = []
```

---

# `repr=False`

Excludes field from `repr()`.

```python
password: str = field(repr=False)
```

---

# `compare=False`

Excludes field from:

- `__eq__`
- ordering methods

```python
cache: dict = field(compare=False)
```

---

# `hash=False`

Excludes field from hash calculation.

---

# `init=False`

Excludes field from constructor.

```python
created_at: float = field(init=False)
```

---

# `kw_only=True` (Field-Level)

```python
name: str = field(kw_only=True)
```

---

# `metadata`

Extra metadata for frameworks/tooling.

```python
field(metadata={"json": "user_name"})
```

---

# `ClassVar`

NOT treated as dataclass field.

```python
from typing import ClassVar

VERSION: ClassVar[str] = "1.0"
```

---

# `InitVar`

Init-only parameter.

NOT stored inside instance.

```python
from dataclasses import InitVar

@dataclass
class User:
    raw: InitVar[str]
```

---

# `__post_init__`

Called after autogenerated `__init__`.

```python
@dataclass
class User:
    name: str

    def __post_init__(self):
        self.name = self.name.strip()
```

---

# Generated Methods

By default dataclass generates:

- `__init__`
- `__repr__`
- `__eq__`

Optionally:

- `__lt__`
- `__le__`
- `__gt__`
- `__ge__`
- `__hash__`

---

# Production Pattern

```python
from dataclasses import dataclass, field

@dataclass(
    frozen=True,
    slots=True,
    kw_only=True,
)
class ApiConfig:
    host: str
    port: int
    timeout: float = 5.0

    headers: dict[str, str] = field(
        default_factory=dict,
    )
```

---

# Best Practices

## Use `slots=True`

When:

- many objects exist
- lightweight models are needed
- memory optimization matters
- performance-sensitive code exists

---

## Use `frozen=True`

When:

- creating value objects
- building DTOs
- immutable configs are needed
- object hashing is required

---

## ALWAYS Use `default_factory`

For:

- list
- dict
- set

---

## Prefer `kw_only=True`

For:

- large constructors
- public APIs
- configs/models

---

## Use `compare=False`

For:

- caches
- runtime state
- internal fields

---

# Quick Reference

| Feature | Purpose |
|---|---|
| `frozen=True` | immutable-ish object |
| `slots=True` | memory optimization |
| `kw_only=True` | safer constructor API |
| `order=True` | sortable objects |
| `default_factory=` | proper mutable defaults |
| `repr=False` | hide sensitive fields |
| `compare=False` | exclude from equality |
| `InitVar` | init-only argument |
| `ClassVar` | class constant |
| `__post_init__()` | post-processing after init |

---

# Typical Modern Recommendation

```python
@dataclass(
    frozen=True,
    slots=True,
    kw_only=True,
)
```

For most modern DTO/value objects this is already a very solid production default.

