# Python Guidelines

These guidelines that are used within First Impression are derived from the PEP 8 style guide, which can be found on https://www.python.org/dev/peps/pep-0008/. The guidelines below are a collection of the most important guidelines from that guide that must be followed by every Python developer within the organisation.

## Table of contents

1. [Indentation](#Indentation)
2. [Maximum Line Length](#Maximum-Line-Length)
3. [Imports](#Imports)
4. [String Quotes](#String-Quotes)
5. [Comments](#Comments)
6. [Naming Conventions](#Naming-Conventions)
7. [Function/Method Annotations](#Function-and-Method-Annotations)
8. [Programming Recommendations](#Programming-Recommendations)

## Indentation

Use 4 spaces per indentation level instead of one tab.

Continuation lines should align wrapped elements either vertically using Python's implicit line joining inside parentheses, brackets and braces, or using a *hanging indent* [[1\]](#Footnotes).  When using a hanging indent the following should be considered; there should be no arguments on the first line and further indentation should be used to clearly distinguish itself as a continuation line:

```python
# Correct:

# Aligned with opening delimiter.
foo = long_function_name(var_one, var_two,
                         var_three, var_four)

# Add 4 spaces (an extra level of indentation) to distinguish arguments from the rest.
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)

# Hanging indents should add a level.
foo = long_function_name(
    var_one, var_two,
    var_three, var_four)
```

```python
# Wrong:

# Arguments on first line forbidden when not using vertical alignment.
foo = long_function_name(var_one, var_two,
    var_three, var_four)

# Further indentation required as indentation is not distinguishable.
def long_function_name(
    var_one, var_two, var_three,
    var_four):
    print(var_one)
```

## Maximum Line Length

Limit all lines to a maximum of 99 characters.

For flowing long blocks of text with fewer structural restrictions (docstrings or comments), the line length should be limited to 72 characters.

Limiting the required editor window width makes it possible to have several files open side by side, and works well when using code review tools that present the two versions in adjacent columns.

## Imports

Imports should usually be on seperate lines:

```python
# Correct:
import os
import sys
```

```python
# Wrong:
import sys, os
```

It's okay to say this though:

```python
# Correct:
from subprocess import Popen, PIPE
```

Imports are always put at the top of the file, just after any module comments and docstrings, and before module globals and constants.

Imports should be grouped in the following order:

1. Standard library imports.
2. Related third party imports.
3. Local application/library specific imports.

You should put a blank line between each group of imports.

##### Wildcard imports

Wildcard imports (`from <module> import *`) should be avoided, as they make it unclear which names are present in the namespace, confusing both readers and many automated tools. There is one defensible use case for a wildcard import, which is to republish an internal interface as part of a public API (for example, overwriting a pure Python implementation of an interface with the definitions from an optional accelerator module and exactly which definitions will be overwritten isn't known in advance).

## String Quotes

In Python, single-quoted strings and double-quoted strings are the same. In this organisation we use single quotes:

```python
# Correct:
aaa = 'aaa'
```

```python
#Wrong:
aaa = "aaa"
```

## Comments

Use the least possible amount of comments possible. Make your code clear by giving good names to variables and don't try to put as much code on one line. 

## Naming Conventions

The naming conventions of Python's library are a bit of a mess, so we'll never get this completely consistent -- nevertheless, here are the currently recommended naming standards.  New modules and packages (including third party frameworks) should be written to these standards, but where an existing library has a different style, internal consistency is preferred.

#### Overriding Principle

Names that are visible to the user as public parts of the API should follow conventions that reflect usage rather than implementation.

#### Descriptive: Naming Styles

There are a lot of different naming styles.  It helps to be able to recognize what naming style is being used, independently from what they are used for.

The following naming styles are commonly distinguished:

- `b` (single lowercase letter)

- `B` (single uppercase letter)

- `lowercase`

- `lower_case_with_underscores`

- `UPPERCASE`

- `UPPER_CASE_WITH_UNDERSCORES`

- `CapitalizedWords` (or CapWords, or CamelCase -- so named because of the bumpy look of its letters.  This is also sometimes known as StudlyCaps.

  Note: When using acronyms in CapWords, capitalize all the letters of the acronym.  Thus HTTPServerError is better than HttpServerError.

- `mixedCase` (differs from CapitalizedWords by initial lowercase character!)

- `Capitalized_Words_With_Underscores` (ugly!)

There's also the style of using a short unique prefix to group related names together.  This is not used much in Python, but it is mentioned for completeness.  For example, the `os.stat()` function returns a tuple whose items traditionally have names like `st_mode`, `st_size`, `st_mtime` and so on.  (This is done to emphasize the correspondence with the fields of the POSIX system call struct, which helps programmers familiar with that.)

The X11 library uses a leading X for all its public functions.  In Python, this style is generally deemed unnecessary because attribute and method names are prefixed with an object, and function names are prefixed with a module name.

In addition, the following special forms using leading or trailing underscores are recognized (these can generally be combined with any case convention):

- `_single_leading_underscore`: weak "internal use" indicator. E.g. `from M import *` does not import objects whose names start with an underscore.

- `single_trailing_underscore_`: used by convention to avoid conflicts with Python keyword, e.g.

  ```
  tkinter.Toplevel(master, class_='ClassName')
  ```

- `__double_leading_underscore`: when naming a class attribute, invokes name mangling (inside class FooBar, `__boo` becomes `_FooBar__boo`; see below).

- `__double_leading_and_trailing_underscore__`: "magic" objects or attributes that live in user-controlled namespaces. E.g. `__init__`, `__import__` or `__file__`.  Never invent such names; only use them as documented.

#### Names to Avoid

Never use the characters 'l' (lowercase letter el), 'O' (uppercase letter oh), or 'I' (uppercase letter eye) as single character variable names.

In some fonts, these characters are indistinguishable from the numerals one and zero.  When tempted to use 'l', use 'L' instead.

#### Package and Module Names

Modules should have short, all-lowercase names.  Underscores can be used in the module name if it improves readability.  Python packages should also have short, all-lowercase names, although the use of underscores is discouraged.

When an extension module written in C or C++ has an accompanying Python module that provides a higher level (e.g. more object oriented) interface, the C/C++ module has a leading underscore (e.g. `_socket`).

#### Class Names

Class names should normally use the CapWords convention.

The naming convention for functions may be used instead in cases where the interface is documented and used primarily as a callable.

Note that there is a separate convention for builtin names: most builtin names are single words (or two words run together), with the CapWords convention used only for exception names and builtin constants.

#### Function and Variable Names

Function names should be lowercase, with words separated by underscores as necessary to improve readability.

Variable names follow the same convention as function names.

mixedCase is allowed only in contexts where that's already the prevailing style (e.g. threading.py), to retain backwards compatibility.

#### Function and Method Arguments

Always use `self` for the first argument to instance methods.

Always use `cls` for the first argument to class methods.

If a function argument's name clashes with a reserved keyword, it is generally better to append a single trailing underscore rather than use an abbreviation or spelling corruption.  Thus `class_` is better than `clss`.  (Perhaps better is to avoid such clashes by using a synonym.)

#### Method Names and Instance Variables

Use the function naming rules: lowercase with words separated by underscores as necessary to improve readability.

Use one leading underscore only for non-public methods and instance variables.

To avoid name clashes with subclasses, use two leading underscores to invoke Python's name mangling rules.

Python mangles these names with the class name: if class Foo has an attribute named `__a`, it cannot be accessed by `Foo.__a`.  (An insistent user could still gain access by calling `Foo._Foo__a`.) Generally, double leading underscores should be used only to avoid name conflicts with attributes in classes designed to be subclassed.

#### Constants

Constants are usually defined on a module level and written in all capital letters with underscores separating words.  Examples include `MAX_OVERFLOW` and `TOTAL`. **It is important that the values of constants are never changed**

## Function and Method Annotations

Use annotations whenever possible. Function annotations look like this:

```python
def greeting(name: str) -> str:
    return 'Hello ' + name
```

This states that the expected type of the `name` argument is `str`.  Analogically, the expected return type is `str`.

Expressions whose type is a subtype of a specific argument type are also accepted for that argument.

## Programming Recommendations

- Comparisons to singletons like None should always be done with `is` or `is not`, never the equality operators.

  Also, beware of writing `if x` when you really mean `if x is not None` -- e.g. when testing whether a variable or argument that defaults to None was set to some other value.  The other value might have a type (such as a container) that could be false in a boolean context!

- Use `is not` operator rather than `not ... is`.  While both expressions are functionally identical, the former is more readable and preferred:

  ```python
  # Correct:
  if foo is not None:
  ```

  ```python
  # Wrong:
  if not foo is None:
  ```

- When catching exceptions, mention specific exceptions whenever possible instead of using a bare `except:` clause:

  ```python
  try:
      import platform_specific_module
  except ImportError:
      platform_specific_module = None
  ```

  A bare `except:` clause will catch SystemExit and KeyboardInterrupt exceptions, making it harder to interrupt a program with Control-C, and can disguise other problems.  If you want to catch all exceptions that signal program errors, use `except Exception:` (bare except is equivalent to `except BaseException:`).

  A good rule of thumb is to limit use of bare 'except' clauses to two cases:

  1. If the exception handler will be printing out or logging the traceback; at least the user will be aware that an error has occurred.
  2. If the code needs to do some cleanup work, but then lets the exception propagate upwards with `raise`.  `try...finally` can be a better way to handle this case.

- Additionally, for all try/except clauses, limit the `try` clause to the absolute minimum amount of code necessary.  Again, this avoids masking bugs:

  ```python
  # Correct:
  try:
      value = collection[key]
  except KeyError:
      return key_not_found(key)
  else:
      return handle_value(value)
  ```

  ```python
  # Wrong:
  try:
      # Too broad!
      return handle_value(collection[key])
  except KeyError:
      # Will also catch KeyError raised by handle_value()
      return key_not_found(key)
  ```

- When a resource is local to a particular section of code, use a `with` statement to ensure it is cleaned up promptly and reliably after use. A try/finally statement is also acceptable.

- Be consistent in return statements.  Either all return statements in a function should return an expression, or none of them should.  If any return statement returns an expression, any return statements where no value is returned should explicitly state this as `return None`, and an explicit return statement should be present at the end of the function (if reachable):

  ```python
  # Correct:
  
  def foo(x):
      if x >= 0:
          return math.sqrt(x)
      else:
          return None
  
  def bar(x):
      if x < 0:
          return None
      return math.sqrt(x)
  ```

  ```python
  # Wrong:
  
  def foo(x):
      if x >= 0:
          return math.sqrt(x)
  
  def bar(x):
      if x < 0:
          return
      return math.sqrt(x)
  ```

- Use `''.startswith()` and `''.endswith()` instead of string slicing to check for prefixes or suffixes.

  startswith() and endswith() are cleaner and less error prone:

  ```python
  # Correct:
  if foo.startswith('bar'):
  ```

  ```python
  # Wrong:
  if foo[:3] == 'bar':
  ```

- Object type comparisons should always use isinstance() instead of comparing types directly:

  ```python
  # Correct:
  if isinstance(obj, int):
  ```

  ```python
  # Wrong:
  if type(obj) is type(1):
  ```

- For sequences, (strings, lists, tuples), use the fact that empty sequences are false:

  ```python
  # Correct:
  if not seq:
  if seq:
  ```

  ```python
  # Wrong:
  if len(seq):
  if not len(seq):
  ```

- Don't compare boolean values to True or False using `==`:

  ```python
  # Correct:
  if greeting:
  ```

  ```python
  # Wrong:
  if greeting == True:
  ```

  ```python
  # Worse:
  if greeting is True:
  ```

## Footnotes

| [[1\]](https://www.python.org/dev/peps/pep-0008/#id3) | *Hanging indentation* is a type-setting style where all the lines in a paragraph are indented except the first line.  In the context of Python, the term is used to describe a style where the opening parenthesis of a parenthesized statement is the last non-whitespace character of the line, with subsequent lines being indented until the closing parenthesis. |
| ----------------------------------------------------- | ------------------------------------------------------------ |
|                                                       |                                                              |

