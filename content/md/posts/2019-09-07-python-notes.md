{:title "Python: Language Features"
 :layout :post
 :toc true
 :tags  ["python" "notes"]}

<em>Some Notes on Python language features, with examples... </em>

<b>Motivation</b>: here I provide some notes made whilst reviewing the book "Python tricks" by Dan Bader, which is a very useful highly recommended book available <a href="https://dbader.org/products/python-tricks-book/" target="_blank">here</a>. Python has become the third most popular programming language behind Java and C, and it continues to become more popular. It is an easy to learn high-level language, that is fun to use and learn. Some of the more advanced and interesting language features are discussed here.

<b>The Zen of Python</b><br>
<em>
Beautiful is better than ugly.<br>
Explicit is better than implicit.<br>
Simple is better than complex.<br>
Complex is better than complicated.<br>
Flat is better than nested.<br>
Sparse is better than dense.<br>
Readability counts.<br>
Special cases aren't special enough to break the rules.<br>
Although practicality beats purity.<br>
Errors should never pass silently.<br>
Unless explicitly silenced.<br>
In the face of ambiguity, refuse the temptation to guess.<br>
There should be one-- and preferably only one --obvious way to do it.<br>
Although that way may not be obvious at first unless you're Dutch.<br>
Now is better than never.<br>
Although never is often better than *right* now.<br>
If the implementation is hard to explain, it's a bad idea.<br>
If the implementation is easy to explain, it may be a good idea.<br>
Namespaces are one honking great idea -- let's do more of those!<br>
</em>
## Miscellaneous:
 
### Variable naming, underscores and dunders
<table>
<thead>
<tr>
<th>Variable name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>_var</code></td>
<td>Hints to a programmer that the variable is intended for internal use, these variables will not be imported with a wildcard e.g. <code>from my_module import *</code> (although this is bad practice to use wildcard imports &quot;explicit is better than implict&quot;).</td>
</tr>
<tr>
<td><code>var_</code></td>
<td>Useful when the name <code>var</code> is already in use and as an alternative to <code>_var</code></td>
</tr>
<tr>
<td><code>__var</code></td>
<td>Names starting with a dunder will be are rewritten to avoid conflicts in a process called name wrangling, such that the class name is added for example <code>_ClassName__var</code>. Name mangling is helpful for letting subclasses override methods without breaking intraclass method calls <a href="https://dbader.org/products/python-tricks-book/" target="_blank"> see here</a>.</td>
</tr>
<tr>
<td><code>__var__</code></td>
<td>For such variables name mangling is not applied, but these are reserved for special use in the language called &#39;magic&#39; methods. This naming convention is best avoided to avoid any future collisions with the Python Language.</td>
</tr>
<tr>
<td><code>_</code></td>
<td>A temporary variable may be used to indicate a standalone or insignificant, temporary variable. This is by convention only, the <code>_</code> is also used REPL to access the last variable, which is very handy.</td>
</tr>
</tbody>
</table>


### Assertion Statements
- The `assert` statement exists in almost every programming language. It helps detect problems early in a program, where the cause is clear, rather than later as a side-effect of some other operation.
- When you do... `assert condition` ... you're telling the program to test that condition, and immediately trigger an error if the condition is false.
- Assertions can include an optional message, and you can disable them when running the interpreter as `python -O script.py`. Since they can be disabled do not use `assert` for data validation.
- To print a message if the assertion fails:  `assert False, "Oh no! This assertion failed!"`
- Do **not** use parenthesis to call `assert` like a function. It is a statement. If you do `assert(condition, message)` you'll be running the `assert` with a `(condition, message)` tuple as first parameter which always evaluates to True.

### Context Managers and the with statement
- The most common use of context managers is to manage resources, and this is why we use them when reading from a file. Opening a file consumes a resource (called a file descriptor), and this resource is limited by the OS. 
- To check on unix the number of files that can be opened see:
```
$ cat /proc/sys/fs/file-max 
1188554
```
- A file descriptor is an integer handle assigned to an open file by the OS rather than accessing the file itself. This is useful to pass references to  files between processes and to maintain kernel security. 
- A file descriptor is leaked by not closing opened files, in python this is done by calling `open()` without a `close()` statement.
- For example, using this statement the `hello.txt` will always be closed:
```python
with open('hello.txt', 'w') as f:
    f.write('hello, world!')
```
- The with statement simplifies exception handling by encapsulating standard uses of `try/finally` statements in context-managers. This ensures the safe  acquisition and release of system resources, acquiring in the with context and leaving releasing when execution leaves the with context.

### Object comparisons: `is` vs `==`
- the `==` checks for equality, the `is` operator compares identities.

### Avoiding Long if/else chains
```python
>>> def dispatch_if(operator, x, y):
...     if operator == 'add':
...         return x + y
...     elif operator == 'sub':
...         return x - y
...     elif operator == 'mul':
...         return x * y
...     elif operator == 'div':
...         return x / y
```
with
```python
>>> def dispatch_dict(operator, x, y):
...     return {
...         'add': lambda: x + y,
...         'sub': lambda: x - y,
...         'mul': lambda: x * y,
...         'div': lambda: x / y,
...     }.get(operator, lambda: None)()
```

### Dictionary merging
- In _Python 3.5+_ dictionaries can be merged as `zs = {**xs, **ys}` where duplicate entries are overwritten by the rightmost object in this case `ys`.

## Functions:
### Lexical closures
- Functions that access variables in a parent function are called 'lexical closures'
- A closure remembers the values from its enclosing lexical scope even when the program flow is no longer in that scope.
```python
def get_speak_func(text, volume):
    def whisper():
        return text.lower() + '...'
    def yell():
        return text.upper() + '...'
    if volume > 0.5:
        return yell
    else:
        return whisper
```

### Lambda functions:
- Lambda functions are single-expression functions that are not necessarily bound to a name (anonymous)
- Lambda functions can’t use regular Python statements and always include an implicit return statement.
```python
>>> add = lambda x, y: x + y
>>> add(5, 3)
8
```
or called on one line
```python
>>> (lambda x, y: x + y)(5, 3)
8
```
 - This is conceptually the same as using `def` but written inline.
 
## Decorators functions:
- Extend, and modify the behaviour of callable functions, without modifying 
the callable itself, useful for:
    - logging
    - enforcing access control and authentication
    - instrumentation and timing functions
    - rate-limiting
    - caching
- Decorators take a callable as input and return another callable
- Functions are decorated with the `@` syntax either at definition or at call
- This example decorator gives some useful info for debugging a function:

```python
import functools

def trace(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        print(f'TRACE: calling {func.__name__}() '
              f'with {args}, {kwargs}')
        original_result = func(*args, **kwargs)
        print(f'TRACE: {func.__name__}() '
              f'returned {original_result!r}')
        return original_result
    return wrapper
```
- Applying the `functools.wraps` to the wrapper closure returned by the decorator carries over the docstring and other metadata of the input function.
    
### *args and **kwargs 
- `*args` and `**kwargs` let you write functions with a variable number of arguments in Python.
- `*args` collects extra positional arguments as a tuple. `**kwargs` collects the extra keyword arguments as a dictionary.
- The actual syntax is `*` and `**` . Calling them args and kwargs is just a convention (and one you should stick to).

### The point of no return 
 - Python adds an implicit `None` if a return statement is not written

## Classes, Objects, and OOP
### String conversions with `__str__` and `__repr__`
- To string conversions can be set with `__str__` and `__repr__` dunder class methods
- The results of `__str__` should be readable, and `__repr__` unambiguous.
- Always add a `__repr__` since the default implemntation of `__str__` just calls `__repr__`
```python
class Car:
    def __init__(self, color, mileage):
        self.color = color
        self.mileage = mileage def __repr__(self):

    def __repr__(self):
        return (f'{self.__class__.__name__}('
                f'{self.color!r}, {self.mileage!r})')

    def __str__(self):
        return f'a {self.color} car'
```

### Defining exception classes
- Makes code easier to debug, and states intent
- Can define logically grouped exception hierarchies

```python
class BaseValidationError(ValueError):
    pass

class NameTooShortError(BaseValidationError):
    pass

class NameToolongError(BaseValidationError):
    pass
```

### Cloning Objects
- A _shallow copy_ constructs a new collection object and then populates it with 
references to the child objects found in the original, it is only one level
deep `copy.copy()`
- A _deep copy_ makes the copying process recursive, constructing a new 
collection then populating it with copes of the child objects found in the 
original `copy.deepcopy()`.
```python
import copy
xs = [[1, 2, 3], [4, ,5, 6]]
zs = copy.deepcopy(xs)
```

### Abstract Base Classes (ABCs)
- ABCs ensure that derived classes implement particular methods from the base 
class at instantiation time.
- Using ABCs can help avoid bugs and makes class hierarchies easier to maintain

```python
from abc import ABC, abstractmethod 
class Animal(ABC): 
    def move(self): 
        pass
  
class Human(Animal): 
    def move(self): 
        print("I can walk and run") 
  
class Snake(Animal): 
    def move(self): 
        print("I can crawl") 
  
class Dog(Animal): 
    def move(self): 
        print("I can bark") 
  
class Lion(Animal): 
    def move(self): 
        print("I can roar") 
```

### Namedtuples
- `collection.namedtuple` is a memory-efficient shortcut to manually define an immutable class in Python.
- Namedtuples can help clean up your code by enforcing an easier to understand structure on your data.
- Immutatble contains, accessed by human readable index.

```python
>>> from collections import namedtuple
>>> Car = namedtuple('Car' , 'color mileage')
```

### Class vs Instance Variables
- **Class variables** are declared inside the class deﬁnition (but outside of any instance methods). They’re not tied to any particular instance of a class. Instead, class variables store their contents on the class itself, and all objects created from a particular class share access to the same set of class variables. This means, for example, that modifying a class variable aﬀects all object instances at the same time.
- **Instance variables** are always tied to a particular object instance. Their contents are not stored on the class, but on each individual object created from the class. Therefore, the contents of an instance variable are completely independent from one object instance to the next. And so, modifying an instance variable only aﬀects one object instance at a time.
```python
class Dog: 
    num_legs = 4 # <- Class variable 
    
    def __init__(self, name): 
        self.name = name # <- Instance variable
```

### Class vs Instance vs Static Methods
- **Instance methods**: the method named `MyClass.method`, is a regular instance method. It takes one parameter, `self`, which points to an instance of `MyClass` when the method is called. Through the self parameter, instance methods can freely access attributes and other methods on the same object. This gives them a lot of power when it comes to modifying an object’s state. Not only can they modify object state, instance methods can also access the class itself through the `self.__class__` attribute. 
- **Class methods**: the `MyClass.classmethod`, marked with a `@classmethod` decorator takes a `cls` parameter that points to the class and not the object instance when the method is called. Since the class method only has access to this cls argument, it can’t modify object instance state. That would require access to self . However, class methods can still modify class state that applies across all instances of the class.
- **Static methods**: the third method, `MyClass.staticmethod` is marked with a `@staticmethod` decorator to flag it as a static method. This type of method doesn’t take a self or a `cls` parameter, although, of course, it can be made to accept an arbitrary number of other parameters. As a result, a static method cannot modify object state or class state. Static methods are restricted in what data they can access they are primarily a way to namespace your methods.
```python
class MyClass:
    def method(self):
        return 'instance method called', self

    @classmethod
    def classmethod(cls):
        return 'class method called', cls

    @staticmethod
    def staticmethod():
        return 'static method called'
```        

## Data Types
### Dictionaries 
- maps, hasmaps, lookup tables, associative arrays
- OrderedDict maintains order of insertion, this is standard as of Python 3.7
- DefaultDict defines a default value for dictionary keys and creates if not available for missing keys
- `collections.ChainMap` groups dictionaries into a single mapping `ChainMap(dict1, dict2)`

### Arrays
- `list` mutable dynamic arrays
- `tuple` - immutable containers
- `array.array('f, [1.0, 8.0]')` space-efficient storage of basic C-style data types, constrained
to a single data type, so are more space efficient than lists or tuples.
- `str` is an immutable store of textual data as unicode characters 
- `bytes` objects are immutable sequences of single bytes, conceptually similar to string objects.
- `bytesarray` - mutable array of single bytes
- `set` an unordered collection of objects that does not allow duplicates
- `frozenset` an immutable version of a set (no insert or deletion)
- `multisets` in `collections.Counter` implements a multiset that allows elements in the set to have more than one occurance
- `stacks` - last-in, first-out (LIFO) semantics, don't allow for random access.
- `queue` - first-in, first-out (FIFO)
- `deque` - a fast double-ended queue doubly linked lists
