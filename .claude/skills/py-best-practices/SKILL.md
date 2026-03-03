---
name: py-best-practices
description: Use when authoring or reviewing Python code.
---

# Python Best Practices

Look at the proposed code changes and ensure that they conform to the following
rules:

1.  Never use `tuple`. Always prefer a structured and documented type like a
    `dataclass`. `tuple` should only be used if external API contracts require
    it.
2.  `dict` and `list` should only be used when their contents are opaque. In all
    other cases, use a dataclass.
3.  Constructors should be simple and free of side effects, especially disk or
    network access.
4.  Prefer composition to implementation inheritence. Interface inheritance via
    abstract base classes is encouraged.
5.  All methods should have appropriate pytype annotations for arguments and
    return types.
6.  In function bodies, empty dict and list initialization should use
    appropriately generic type annotations (e.g. `foo: list[str] = []`).
7.  Prefer dependency injection/inversion of control. An implementation should
    not construct their dependencies unless those dependencies are a trivial
    implementation detail.
8.  Always use descriptive variable names, even for loop variables.
9.  Write docstrings with argument and return comments for all functions.
10. Write docstrings with attributes comments for all dataclasses.
11. Avoid excessive use of `mock` in tests. `mock` should be reserved for
    difficult to control libraries like `time` and `datetime` or external RPC
    services.
12. Classes and functions should be named for what they do not how they are
    used.
13. Scrutinize the use of `Any` to make sure there are not more specific types
    that would be appropriate.
14. Prefer `|` to `Union`.
15. Private functions, attributes, classes and constants should be prefixed with
    underscore. Scrutinize each symbol to determine if it should be private.
16. Avoid public read/write attributes. Most properties should be either
    completely private or read-only via a @property decorator.
17. Prefer early return/break/continue to avoid unnecessary indentation.
18. IMPORTANT: Prefer propagating exceptions to silencing errors. Functions that
    encounter exceptions should either: allow them to propagate, report partial
    success to the caller via a complex return value (not just log a warning or
    error), or handle an error in a way that preserves the API contract with the
    caller (e.g. retrying an RPC until it succeeds).
19. When creating new files, consider the project structure and existing naming
    conventions. Use file and folder names that are explicit and avoid highly
    general naming like "utils.py" or "types.py".
20. Avoid functions with a large number of arguments. This often suggests that
    refactoring is needed or argument substructures (e.g. a dataclass) may need
    to be introduced.
