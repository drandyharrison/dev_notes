% Python tutorial notes

Found at `https://docs.python.org/3/tutorial/index.html`

To run a python script from the python console

		execfile(filename)

# Section 3: An Informal Introduction to Python

operators

* `//` denotes floor division
* `%` returns the remainder (modulo)
* `**` denotes power
* `=` denotes assignment
	
in interactive mode, the last printed expression is assigned to the variable `_`

Python includes int, float, decimal, fraction and complex numeric types - the imaginary part is indicated using `i` or `j`.

### 3.1.2 Strings

`r` before a quote means the string is interpretted as a raw string and characters prefixed by a `\` are not interpretted as special characters

Triple quotes can be used to define string literals that span multiple lines - end of lines are automatically added to the string, unless prevented by ending a line with `\`

strings are concatenated with `+`
and repeated with `*`
adjacent string literals are automatically concatenated, which is useful when breaking long strings - this only works with string literals, not with variables or expresssions - in those cases use `+` to concatenate.

strings can be indexed using `[i]` - starting from zero - there is no character type - just strings
indexes can be negative, starting from right - the last character is `-1` - `-0` is the same as 0
slicing can be used to obtain sub-strings - `word[i:j]`
to include start `s[:i]`, to include `s[i:]` - `s[:i] + s[i:] = s` - can be used with -ve indexes as well
out of range indexes are handled gracefully when slicing

Python strings are immutable - hence assigning to an index position results in an error
it is possible to concatenate a sub-string to create a new string

strings are an instance of sequence types

### 3.1.3 Lists

* lists are an example of a compound data type
* lists are written as comma separated values in brackets
* a slice of a list returns a new list
* lists support concatenation
* lists are mutable
* use `*.append()` method to append values to the list
* assignment to a slice is possible, which can change the size of the list or clear it - `word[:] = []`

The built in function `len()` applies to lists and strings.

Lists of lists are supported - index lists of lists: `x[0][1]`.

## 3.3 First steps to programming

Multiple assignments are supported - `a, b = 0, 1` - assigns `0` to `a` and `1` to `b`
in a multiple assignment, the right-hand side expressions are evaluated first, from left to right; e.g.

		a, b = b, a + be

Indentation is used to group statements

In print, the keyword end can be used to avoid the newline after the output, or end the output with a different string

# 4 Control flow tools

## 4.1 `if` statements

An `if` ... `elif` ... `elif` ... sequence is a substitue for `switch` ... `case` statements found in other languages.

## 4.2 `for` statments

for statements iterate over a sequence

To modify the sequence being iterated over, it is recommended that you first make a copy - the slice notation makes this convenient.

## 4.3 The `range()` function

The `range()` function generates an arithmetic progression - the given end point is never generated

		range([start], stop, [step])

combine `range()` and `len()` to iterate over the indices of a sequence - although it's more convenient to use `enumerate()`

index a sequence `[i]`

The object returned by `range()` is iterable, but does not create a list - so is suitable for functions and constructs that expect something that iterates. The `for` statement is such an iterator. The function `list()` is another, which creates a list from iterables.

## 4.4 `break` and `continue` statements, and `else` clauses on loops

Loop statements may have an `else` clause; it is executed when the loop terminates through exhaustion of the list (with `for`) or when the condition becomes false (with `while`), but not when the loop is terminated by a `break` statement.

When used with a loop, the `else` clause has more in common with the `else` clause of a `try` statement than it does that of `if` statements: a `try` statement’s `else` clause runs when no exception occurs, and a loop’s `else` clause runs when no `break` occurs.

## 4.5 `pass` statments

The `pass` statement does nothing. It can be used when a statement is required syntactically but the program requires no action.

Another place `pass` can be used is as a place-holder for a function or conditional body when you are working on new code, allowing you to keep thinking at a more abstract level. The `pass` is silently ignored

## 4.6 defining functions

The keyword `def` introduces a function definition, and is followed by the function name and a parenthesised list of formal parameters - the statements that form the body of the function definition must be indented

The first statement of the function can be an option string literal, which is the function's `docstring`

Variable references start with a function's local symbol table then the local symbol table of any calling function then finally the global symbol table. So a global variable can only be referenced if named in a global statement

Function arguments are passed using call by value, where the value is an object reference not the value of the object

A function definition introduces the function name into the current sumbol table. The value of the function name has type user-defined function, which can be passed to another name, which can be used as a function.

A function without a `return` statrment returns the value `None`, which is normally supressed but can be seen using `print(fn(...))`.

It's possible to return a list from a function

A `return` statment without an expression returns `None`.

## 4.7 More on defining functions

It is possible to define functions with a variable number of arguments

### 4.7.1 default argument values

There is an `in` operator, which tests whether a sequence contains a given value

Default values are evaluated at the point of definition - if they're variables or expressions

The default value is evaluated once, which is important if the default is a mutable object - such as a list, dictionary of class - as this can mean passed arguments are accumulated over multiple calls; e.g.

		def f(a, L = []):
			L.append(a)
			return L
		
This can be overcome with

		def f(a, L = None):
			if L is None:
				L = []
			L.append(a)
			return L
		
### 4.7.3 Keyword arguments

Keyword arguments are of the form `kwarg = value`, as opposed to a positional argument. Positional arguments must proceed keyword arguments, although the order in which keyword arguments appear doesn't matter.

A function can be called by referring to argument by name; e.g. `areg_name=value`. No argument may receive a value more than once, in a single call.

It's not clear what the difference is between a default value and a keyword argument!

When a final formal parameter of the form `**name` is present, it receives a dictionary containing the keyword arguments except for those corresponding to a formal parameter. This can be combined with a formal parameter of the form `*name`, which contains the list of positional arguments.

A formal parameter is one defined when the function is defined, but `*name` and `**name` formal parameters allows the function to be called with a variable number of arguments. For example,

		def cheeseshop(kind, *arguments, **keywords):

can be called

		cheeseshop("Limburger", "It's very runny, sir.",
			"It's really very, VERY runny, sir.",
			shopkeeper="Michael Palin",
			client="John Cleese",
			sketch="Cheese Shop Sketch")
		
### 4.7.3 Arbitrary argument lists

The least frequently used option is to specify a function that can be called with an arbitrary number of arguments, which will be wrapped into a tuple - `*args` - and which can be preceded by any normal arguments. Such a variadic argument is usually last, as it mops up all remaining arguments passed to the function. Only keyword arguments can be passed after it.

**_How are these three approaches actually different_?**

### 4.7.4 Unpacking argument lists

If a function expects separate postional arguments but the arguments are in a list or a tuple, use the `*` operator to unpack them; e.g.

		args = [3, 6]
		list(range(*args))
	
In the same fashion, a dictionary can deliver keyword arguments using the `**` operator; e.g.

		d = {"voltage": "four million", "state": "bleedin' demised", 
		"action": "VOOM"}
		parrot(**d)
	
### 4.7.5 Lambda expressions

Small anonymous functons can be created using the lambda keyword - they are syntactically restricted to a single expression - like a nested function, a lambda fucntions can reference variables from the containing scope.

A lambda expression can be used for a function to return a function or to pass a function as an argument to a function.

		>>> def make_incrementor(n):
		...     return lambda x: x + n
		...
		>>> f = make_incrementor(42)
		>>> f(0)
		42
		>>> f(1)
		43

		>>> pairs = [(1, 'one'), (2, 'two'), (3, 'three'), (4, 'four')]
		>>> pairs.sort(key=lambda pair: pair[1])
		>>> pairs
		[(4, 'four'), (1, 'one'), (3, 'three'), (2, 'two')]

### 4.7.6 Documentation strings

Documentation strings can be multi-line.

The `__doc__` attribute of a function '_returns_' the documentation string.

### 4.7.7 Function annotations

Function annotations are optional metadata, which are stored in the `__annotations__` attribute as a dictionary.

Parameter annotations are defined by a colon after the name of parameter name followed by an expression which evaluates to an annotation.

Return annotations are defined by the literal `->` followed by an expression between the parameter list and the colon indicating the end of the `def` statement; e.g.

		def f(ham: str, eggs: str = 'eggs') -> str:
		...     print("Annotations:", f.__annotations__)
		...     print("Arguments:", ham, eggs)
		...     return ham + ' and ' + eggs

# 5 Data structures

## 5.1 Lists

Use the `append()` and `pop()` methods to use a list as a stack. `pop()` returns the final element of the list, `pop(i)` returns the item at index if

`insert(0, x)` and `pop(0)` methods can be used to emulate a queue with a list, but it's not efficient. It's more efficient to use `collections.deque`, which supports `popleft()` method e.g.

		from collections import deque
		queue = deque(["Eric", "John", "Michael"])

### 5.1.3 List comprehensions

A list comprehension is a concise way in which to create a list whose elements can be defined based on an expression.

We could calculate a list of squares using a lambda

		squares = list(map(lambda x : x **2, range(10)))
	
or using a list comprehension

		squares = [x**2 for x in range(10)]
	
which has the structure of brackets containing an expression followed by a `for` clause then zero or more `for` or `if` clauses, e.g.

		[(x, y) for x in [1, 2, 3] for y in [3, 1, 4] if x != y]

if the list is a list of tuples then the tuples must be in parentheses

A function can be applied to all elements of an existing list

		[abs(x) for x in vec]

or a method can be applied to elements

		[weapon.strip() for weapon in freshfruit]
	
flatten a list

		[num for elt in vec for num in elt]
	
or even complex expressions or nested functions

		from math import pi
		[str(round(pi, i)) for i in range(1, 6)]
	
### 5.1.4 Nested list comprehensions

A nested list comprehension is evaluated in the context of the for that follows it - nested list comprehensions are evaluated outside in - think about unrolling into loops, to understand.

The preference should be for built-in functions rather than complex flow.

Look at the `zip()` function ...

## 5.2 The `del` statement

The `del` statement removes an element (or slice) from a list based on an index or it can delete entire variables

## 5.3 tuples and sequences

Lists and strings are examples of sequence data types

A tuple consists of comma separated values, which are not necessarily of the same type

Tuples can be nested and are immutable, although the elements of a tuple can be mutable, such as a list, which are mutable and usually compromise homogeneous elements.

An empty tuple is indicated by an empty pair of parentheses - `()` - while a singleton tuple is indicated by a single value followed by a comma - `(value,)`.

* `tu = (x, y, z)` is referred to as tuple packing; and
* `x, y, z = tu` is referred to as tuple unpacking and requires the number of variables on the left to match the number of elements in the tuple
	
## 5.4 Sets

Sets are unorded collections without duplication and support the usual union (`|`), intersection (`&`), difference (`-`), symmetric difference (`^`) - in one but not both sets - and `in` operator.

Sets are created using `set()` or `{}`.

Similar to list comprehensions, set comprehensions are also supported.

## 5.5 Dictionaries

Dictionaries are indexed by keys, which can be of any immutable type - tuples can be used as keys provided all their elements are immutable.

A dictionary should be thought of as key-value pairs with the constraint that keys are unique (within a dictionary)

A pair of braces - `{}` - creates an empty dictionary - initial values are added as comma separated `key:value` pairs

The main dictionary operations are

* add a `key:value` pair;
* extracting the `value` associated with a `key`; or
* deleting a `key:value` pair

Performing `list(d)` on a dictionary, `d`, will return a list of keys in insertion order - to get them sorted use `sorted(d)` - and use in to test whether a key appears in the dictionary.

A dictionary can be built directly from key-value pairs using `dict()`.

Dictionary comprehensions are also supported

		{x : x**2 for x in (2, 4, 6)}
	
## 5.6 Looping techniques

When looping through a dictionary, the key and corresponding value can be retrieved simultaneously using the `item()` method.

		for k, v in knights.items():
			print(k, v)
		
When looping through a sequence, the index and the corresponding value can be retrieved simultaneously using the `enumerate()` method.

To loop over two or more sequences at the same time, entries can be paired with the `zip()` function.

To loop over a sequence in reverse, call the `reversed()` function with the sequence in the forward direction.

It is simpler and safer to create a copy of list rather than changing it as you loop over it.

## 5.7 More on conditions

The operators `in` and `not in` test membership of a sequence.
The operators `is` and `not is` test whether two objects are the same object.
Comparisons can be chained and can be combined with the usual boolean operators - both `and` & `or` stop evaluation as soon as the outcome has been determined, just like `C`.

Unlike `C`, assignment cannot occur within an expression.

## 5.8 Comparing sequences and other types

Sequences can be compared, based on a ographical ordering: first the first two items are compared, and if they differ this determines the outcome of the comparison; if they are equal, the next two items are compared, and so on, until either sequence is exhausted. If two items to be compared are themselves sequences of the same type, the lexicographical comparison is carried out recursively.

# 6 Modules

A module is a file containing Python definitions and statements - the filename is the module name with the suffix `.py` - within a module, the module's name is available as the global variable `__name__`.

Modules - and their definitions - can be imported into another file or the main module.

To determine the current directory

		import os
		os.getcwd()

To use a module - `fibo.py` - and access a function in it (e.g. `fib`)

		import fibo
		fibo.fib(1000)
	
If a function is used repeatedly, it can be convenient to give it a local name: e.g., `fib = fibo.fib`

To check whether a module has been imported

		import sys
	
		modname = 'xxx'
		if modname not in sys.modules :
			print("You haven't imported the {} module".format(modnmae))
		else :
			print("You have imported the {} module".format(modnmae))
		
## 6.1 More on modules

If a module contains executable statements, as well as function definitions, these are executed only the first time a module is encountered in an import statement and are intended to initialise the module.

Each module has its own private symbol table, which is used as the global symbol table by all functions defined in the module. Thus, the author of a module can use global variables in the module without worrying about accidental clashes with a user’s global variables. On the other hand, if you know what you are doing you can touch a module’s global variables with the same notation used to refer to its functions, `modname.itemname`

To import names from a module directly into the importing module's symbol table use

		from modname import name1, name2
	
This does not introduce the module name from which the imports are taken in the local symbol table

To import all names a module defines

		from modname2 import *
	
but this does not import names prefixed with `_` (this is not good practice, as the number of names imported is not known).

If the module name is followed by as, then the name following as is bound directly to the imported module - this can also be used to bind names to specific imported functions with from; e.g.

		from fibo import fib as fibonacci

### 6.1.1. Executing modules as scripts

When you run a Python module with

		python fibo.py <arguments>

the code in the module will be executed, just as if you imported it, but with the `__name__` set to `"__main__"`. That means that by adding this code at the end of your module:

		if __name__ == "__main__":
			import sys
			fib(int(sys.argv[1]))

you can make the file usable as a script as well as an importable module, because the code that parses the command line only runs if the module is executed as the “_main_” file.

### 6.1.2 The module search path

When a module is named, Python first searches the built-in modules then the list of directories given by the variable `sys.path`, which starts with the directory containing the imput script or the current directory ifno file is specified.

### 6..1.3 '_Compiled_' python files

To speed up loading modules, Python caches the compiled version of each module in the `__pycache__` directory under the name `module.version.pyc`, where the version encodes the format of the compiled file; it generally contains the Python version number.

## 6.2 Standard modules

Python comes with a library of standard modules, described in a separate document, the Python Library Reference (“Library Reference” hereafter).

## 6.3 The `dir()` function

The built-in function `dir()` is used to find out which names a module defines. It returns a sorted list of strings.

Without arguments, `dir()` lists the names you have defined currently.

		import builtins
		dir(builtins)

## 6.4 Packages

Packages are a way of structuring Python’s module namespace by using "_dotted module names_". For example, the module name `A.B` designates a submodule named `B` in a package named `A`.

Example package structure

		sound/					Top-level package
			__init__.py			Initialize the sound package
			formats/			Subpackage for file format conversions
				__init__.py
				wavread.py
				  
When importing the package, Python searches through the directories on sys.path looking for the package subdirectory.

The `__init__.py` files are required to make Python treat the directories as containing packages. When importing the package, Python searches through the directories on `sys.path` looking for the package subdirectory.

Users of the package can import individual modules from the package, for example:

		import sound.effects.echo

This loads the submodule `sound.effects.echo`. It must be referenced with its full name.

		sound.effects.echo.echofilter(input, output, delay=0.7, 
		atten=4)

An alternative way of importing the submodule is:

		from sound.effects import echo

This also loads the submodule echo, and makes it available without its package prefix, so it can be used as follows:

		echo.echofilter(input, output, delay=0.7, atten=4)

Yet another variation is to import the desired function or variable directly:

		from sound.effects.echo import echofilter

Again, this loads the submodule `echo`, but this makes its function `echofilter()` directly available:

		echofilter(input, output, delay=0.7, atten=4)

Note that when using from package import item, the item can be either a submodule (or subpackage) of the package, or some other name defined in the package, like a function, class or variable. The import statement first tests whether the item is defined in the package; if not, it assumes it is a module and attempts to load it. If it fails to find it, an `ImportError` exception is raised.

### 6.4.1 Importing * from a package

if a package’s `__init__.py` code defines a list named `__all__`, it is taken to be the list of module names that should be imported when `from package import *` is encountered. It is up to the package author to keep this list up-to-date when a new version of the package is released. Package authors may also decide not to support it, if they don’t see a use for importing `*` from their package. For example, the file `sound/effects/__init__.py` could contain the following code:

		__all__ = ["echo", "surround", "reverse"]

This would mean that `from sound.effects import *` would import the three named submodules of the `sound` package.

Using `from package.module import *` is not recommended.

### 6.4.2 intra-package references

Relative imports are possible; e.g.

		from . import echo
		from .. import formats
		from ..filters import equalizer
	
### 6.4.3 packages in multiple directories

Packages support one more special attribute, `__path__`. This is initialized to be a list containing the name of the directory holding the package’s `__init__.py` before the code in that file is executed. This variable can be modified; doing so affects future searches for modules and subpackages contained in the package.

# 7 Input and Output

## 7.1 Fancier output formatting

As well as writing values using expression statements, the `print()` function and the `write()` method of file objects there are several ways to format output:

* formatted string literals - which begin with an `f` or `F` before the opening quotation mark can include expressions betweeen `{` and `}` that can refer to variables or literal values;

* the `str.format()` string method allows greater control with `{` and `}` indicating where a variable is to be inserted and detailed formatting directives; or

		'{:9} Yes votes {:2.2%}'.format(yes_votes, pct)
	
* string handling can be achieved using string slicing and concatenation.

To just return a variable's value as a string, use `str()` - for human readable output - and `repr()` - for machine readable output. Both are useful for debugging.

### 7.1.1 Formatted string literals

An optional format specifier can follow an expression between `{` and `}` in a formatted string literal - passing an integer after a format specifier that starts with a `:` will cause that field to be a minimum number of characters wide, which is useful for making columns align.

Other modifiers can be used to convert the value before it is formatted. `'!a'` applies `ascii()`, `'!s'` applies `str()`, and `'!r'` applies `repr()`.

To find out more about format specifiers see the format specification mini-language: `https://docs.python.org/3/library/string.html#formatspec`

### 7.1.2 The string `format()` method

In basic usage, the `{}` and the characters within them (called format fields) are replaced with the objects passed into the `str.format()` method. A number in the brackets can be used to refer to the position of the object passed into the `str.format()` method.

If keyword arguments are used in the `str.format()` method, their values are referred to by using the name of the argument.

		print('This {food} is {adjective}.'.format(food='spam', 
		adjective='absolutely horrible'))

Keyword and positional arguments can be used together.

The built-in function `vars()`, returns a dictionary containing all local variables.

### 7.1.3 Manual string formatting

The `str.rjust()` method of string objects right-justifies a string in a field of a given width by padding it with spaces on the left. There are similar methods `str.ljust()` and `str.center()`. These methods do not write anything, they just return a new string.

To truncate numbers that are too long, add a slice operation, as in `x.ljust(n)[:n]`

`str.zfill()` pads a numeric string on the left with zeros.

### 7.1.4. Old string formatting

The `%` operator can also be used for string formatting. It interprets the left argument much like a `sprintf()`-style format string; e.g.

		print('The value of pi is approximately %5.3f.' % math.pi)
	
## 7.2 Reading and writing files

The function `open()` returns a file object adn is most commonly used with the arguments filename and mode (based on 'standard' Linux `r/w/a/r+` modes) - mode is optonal and the default is `r`.

The default is to open files in text mode - to open in binary mode append `'b'`.

It is good practice to use the `with` keyword when dealing with file objects. The advantage is that the file is properly closed after its suite finishes, even if an exception is raised at some point. Using with is also much shorter than writing equivalent `try`-`finally` blocks:

		with open('workfile') as f:
		...     read_data = f.read()	

`f.closed` tests whether a file object is closed.

If you’re not using the `with` keyword, then you should call `f.close()` to close the file and immediately free up any system resources used by it.

### 7.2.1 Methods of file objects

The method `read()` reads a file's contents from a file object - and returns it as a string (in text mode) - the optional size argument controls how much is read - if it's omitted or negative, the whole file is read.

`f.readline()` reads a single line from the file; a newline character (`\n`) is left at the end of the string, and is only omitted on the last line of the file if the file doesn’t end in a newline. This makes the return value unambiguous; if `f.readline()` returns an empty string, the end of the file has been reached, while a blank line is represented by `'\n'`, a string containing only a single newline.

For reading lines from a file, you can loop over the file object. This is memory efficient, fast, and leads to simple code:

		f = open('filename')
		for line in f:
			print(line)
		f.close()

If you want to read all the lines of a file in a list you can also use `list(f)` or `f.readlines()`.

`f.write(string)` writes the contents of string to the file, returning the number of characters written.

Other types of objects need to be converted – either to a string (in text mode) or a bytes object (in binary mode) – before writing them.

`f.tell()` returns an integer giving the file object’s current position in the file represented as number of bytes from the beginning of the file when in binary mode and an opaque number when in text mode.

To change the file object’s position, use `f.seek(offset, from_what)`. The position is computed from adding `offset` to a reference point; the reference point is selected by the `from_what` argument. A `from_what` value of `0` measures from the beginning of the file, `1` uses the current file position, and `2` uses the end of the file as the reference point. `from_what` can be omitted and defaults to `0`, using the beginning of the file as the reference point.

File objects have some additional methods, such as `isatty()` and `truncate()`.

### 7.2.2 Saving structured data with json

Reading numbers from a file is not straightforward, as `read()` returns a string, which will need to be passed to `int()` to convert it into a number. Parsing lists or dictionaries becomes even more complicated. To simplify this, Python supports JSON.

The standard Python json module can convert data hierarchies into string representations - serialising - and reconstruct the data from the string - de-serialising.

The `json.dumps()` method displays the JSON string representation of any object.

The `dump()` method serialises an object to a text file - so to seriaiise an object `o` to a text file object - `f` - that is open for writing: `json.dump(0, f)`. Remember to close the file object or flush buffers to make sure the data are written; otherwise the file may seem empty.

To decode the object from a text file object open for reading - `x = json.load(f)`

For serialising arbitrary classes - beyond lists and dictionaries - see the json module.

# 8 Errors and exceptions

## 8.3 Handling exceptions

Exceptions are handled by the `try` statement, which works as follows

* first, the `try` clause is executed.

* if no exception occurs, the `except` clause is skipped and execution of the `try` statement is finished.

* if an exception occurs during execution of the `try` clause, the rest of the clause is skipped. Then if its type matches the exception named after the `except` keyword, the `except` clause is executed, and then execution continues after the `try` statement.

* if an exception occurs which does not match the exception named in the `except` clause, it is passed on to outer `try` statements; if no handler is found, it is an unhandled exception and execution stops with a message.

A `try` statement may have more than one `except` clause, to specify handlers for different exceptions. At most one handler will be executed. Handlers only handle exceptions that occur in the corresponding `try` clause, not in other handlers of the same `try` statement. An `except` clause may name multiple exceptions as a parenthesized tuple, for example:

		except (RuntimeError, TypeError, NameError):
			pass

A class in an except clause is compatible with an exception if it is the same class or a base class thereof.

The last except clause may omit the exception name(s), to serve as a wildcard. Use this with extreme caution, since it is easy to mask a real programming error in this way! It can also be used to print an error message and then re-raise the exception (allowing a caller to handle the exception as well); e.g.

		except:
			print("Unexpected error:", sys.exc_info()[0])
			raise

The `try` ... `except` statement has an optional `else` clause, which, when present, must fillow all `expect` clauses.  It is useful for code that must be executed if the `try` clause does not raise an exception; e.g.

		for arg in sys.argv[1:]:
			try:
				f = open(arg, 'r')
			except OSError:
				print('cannot open', arg)
			else:
				print(arg, 'has', len(f.readlines()), 'lines')
				f.close()

When an exception occurs, it may have an associated value, the exception’s argument. The presence and type of the argument depend on the exception type.

The `except` clause may specify a variable after the exception name. The variable is bound to an exception instance with the arguments stored in `instance.args`. For convenience, the exception instance defines `__str__()` so the arguments can be printed directly without having to reference `.args`. One may also instantiate an exception first before raising it and add any attributes to it as desired.

		try:
			raise Exception('spam', 'eggs')
		except Exception as inst:
			print(type(inst))	# the exception instance
			print(inst.args)	# arguments stored in .args
			print(inst)			# __str__ allows args to be printed directly,
								# but may be overridden in exception subclasses
			x, y = inst.args	# unpack args
			print('x =', x)
			print('y =', y)

Exception handlers don’t just handle exceptions if they occur immediately in the `try` clause, but also if they occur inside functions that are called (even indirectly) in the `try` clause. For example:

	
		def this_fails():
			x = 1/0
	
		try:
			this_fails()
		except ZeroDivisionError as err:
			print('Handling run-time error:', err)	

## 8.4 Raising exceptions

The `raise` statement allows the programmer to force a specified exception to occur. For example:

		raise NameError('HiThere')

The sole argument to raise indicates the exception to be raised. This must be either an exception instance or an exception class (a class that derives from Exception). If an exception class is passed, it will be implicitly instantiated by calling its constructor with no arguments.

	
If you need to determine whether an exception was raised but don’t intend to handle it, a simpler form of the `raise` statement allows you to re-raise the exception.

## 8.5 User-defined exceptions

Programs may name their own exceptions by creating a new exception class, which should typically be derived from the `Exception` class, either directly or indirectly.

Exception classes can be defined which do anything any other class can do, but are usually kept simple, often only offering a number of attributes that allow information about the error to be extracted by handlers for the exception. When creating a module that can raise several distinct errors, a common practice is to create a base class for exceptions defined by that module, and subclass that to create specific exception classes for different error conditions:

		class Error(Exception):
			"""Base class for exceptions in this module."""
			pass

		class InputError(Error):
			"""Exception raised for errors in the input.

			Attributes:
				expression -- input expression in which the error occurred
				message -- explanation of the error
			"""

			def __init__(self, expression, message):
				self.expression = expression
				self.message = message

Most exceptions are defined with names that end in “_`Error`_”, similar to the naming of the standard exceptions.

## 8.6 Define clean-up actions

The `try` statement has another optional `finally` clause which is intended to define clean-up actions that must be executed under all circumstances. A more complicated example:

		def divide(x, y):
			try:
				result = x / y
			except ZeroDivisionError:
				print("division by zero!")
			else:
				print("result is", result)
			finally:
				print("executing finally clause")

In real world applications, the finally clause is useful for releasing external resources (such as files or network connections), regardless of whether the use of the resource was successful.

## 8.7 Pre-defined clean-up actions

Some objects define standard clean-up actions to be undertaken when the object is no longer needed, regardless of whether or not the operation using the object succeeded or failed. Look at the following example, which tries to open a file and print its contents to the screen.

		for line in open("myfile.txt"):
			print(line, end="")

The problem with this code is that it leaves the file open for an indeterminate amount of time after this part of the code has finished executing. This is not an issue in simple scripts, but can be a problem for larger applications. The with statement allows objects like files to be used in a way that ensures they are always cleaned up promptly and correctly.

		with open("myfile.txt") as f:
			for line in f:
				print(line, end="")

After the statement is executed, the file `f` is always closed, even if a problem was encountered while processing the lines.

### Syntax of print

		print(object(s), separator=separator, end=end, file=file,
		flush=flush)


| Parameter          |           | Description |
| -------------------|:---------:|-------------|
| `object(s)`        |           | Any object, and as many as you like. | 
|                    |           | Will be converted to string before printed |
| `sep='separator'`  | Optional  | Specify how to separate the objects, |
|                    |           | if there is more than one. |
|                    |           | Default is `''` |
| `end='end'`        | Optional  | Specify what to print at the end. |
|                    |           | Default is `'\n'` (line feed) |
| `file`             | Optional  | An object with a write method. |
|                    |           | Default is sys.stdout |
| `flush`            | Optional  | A Boolean, specifying if the output |
|                    |           | is flushed (True) or buffered (False). | 
|                    |           | Default is False |

Colon to define justification - in a table example!

| Serial  | Value  |
|--------:|-------:|
| 1       | 2.10   |
| 2       | 37.5   |

Some inline maths $x^{2} + y_{1}^{3} = \aleph$ **and it works!**.

I just need to have a go at adding some HTML next!