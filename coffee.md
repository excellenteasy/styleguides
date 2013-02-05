# CoffeeScript Style Guide

This guide is for use in [excellenteasy](http://github.com/excellenteasy) projects and forked from [polarmobile/coffeescript-style-guide](https://github.com/polarmobile/coffeescript-style-guide)

Please note that this is a work-in-progress: there is much more that can be specified.

## Table of Contents

* [The CoffeeScript Style Guide](#coffeescript-style-guide)
    * [Code Layout](#code-layout)
        * [Tabs or Spaces?](#tabs-or-spaces)
        * [Maximum Line Length](#maximum-line-length)
        * [Blank Lines](#blank-lines)
        * [Trailing Whitespace](#trailing-whitespace)
        * [Encoding](#encoding)
    * [Module Imports](#module-imports)
    * [Whitespace in Expressions and Statements](#whitespace)
    * [Comments](#comments)
        * [Block Comments](#block-comments)
        * [Inline Comments](#inline-comments)
    * [Naming Conventions](#naming-conventions)
    * [Functions](#functions)
    * [Strings](#strings)
    * [Conditionals](#conditionals)
    * [Looping and Comprehensions](#looping-and-comprehensions)
    * [Extending Native Objects](#extending-native-objects)
    * [Exceptions](#exceptions)
    * [Annotations](#annotations)
    * [Miscellaneous](#miscellaneous)

## Code layout

### Tabs or Spaces?

Use **spaces only**, with **2 spaces** per indentation level. Never mix tabs and spaces.

### Maximum Line Length

Limit all lines to a maximum of 79 characters.

### Blank Lines

Separate top-level function and class definitions with a single blank line.

Separate method definitions inside of a class with a single blank line.

Use a single blank line within the bodies of methods or functions in cases where this improves readability (e.g., for the purpose of delineating logical sections).

### Trailing Whitespace

Do not include trailing whitespace on any lines.

### Encoding

UTF-8 is the preferred source file encoding.

## Module Imports

If using a module system (CommonJS Modules, AMD, etc.), `require` statements should be placed on separate lines.

```coffee
require 'lib/setup'
Backbone = require 'backbone'
```
These statements should be grouped in the following order:

1. Standard library imports _(if a standard library exists)_
2. Third party library imports
3. Local imports _(imports specific to this application or library)_

## Whitespace in Expressions and Statements

Avoid extraneous whitespace in the following situations:

- Immediately inside parentheses, brackets or braces

    ```coffee
    ($ 'body') # Yes
    ( $ 'body' ) # No
    ```

- Immediately before a comma

    ```coffee
    console.log x, y # Yes
    console.log x , y # No
    ```

Additional recommendations:

- Always surround these binary operators with a **single space** on either side

    - assignment: `=`

        - _Note that this also applies when indicating default parameter value(s) in a function declaration_

           ```coffee
           test: (param = null) -> # Yes
           test: (param=null) -> # No
           ```

    - augmented assignment: `+=`, `-=`, etc.
    - comparisons: `==`, `<`, `>`, `<=`, `>=`, `unless`, etc.
    - arithmetic operators: `+`, `-`, `*`, `/`, etc.

    - _(You can use more than one space if an uninterrupted sequence of assignment statements follows each other.)_

        ```coffee
        # Yes
        x      = 1
        y      = 1
        fooBar = 3
        ```

## Comments

If modifying code that is described by an existing comment, update the comment such that it accurately reflects the new code.

The first word of the comment should be capitalized, unless the first word is an identifier that begins with a lower-case letter.

Comments should be written as full sentences, with proper punctuation.

### Block Comments

Don't use real block comments, unless you intend to pass along the comment to the underlying JS, like a license, or warning.

Block comments apply to the block of code that follows them.

Each line of a block comment starts with a `#` and a single space, and should be indented at the same level of the code that it describes.

Paragraphs inside of block comments are separated by a line containing a single `#`.

```coffee
# This is a block comment. Note that if this were a real block
# comment, we would actually be describing the proceeding code.
#
# This is the second paragraph of the same block comment. Note
# that this paragraph was separated from the previous paragraph
# by a line containing a single comment character.

init()
start()
stop()
```

### Inline Comments

Inline comments are placed on the line immediately above the statement that they are describing. If the inline comment is sufficiently short, it can be placed on the same line as the statement (separated by a single space from the end of the statement).

All inline comments should start with a `#` and a single space.

Do not use inline comments when they state the obvious:

```coffee
# No
x = x + 1 # Increment x
```

However, inline comments can be useful in certain scenarios:

```coffee
# Yes
x = x + 1 # Compensate for border
```

## Naming Conventions

Use `camelCase` (with a leading lowercase character) to name all variables, methods, and object properties.

Use `CamelCase` (with a leading uppercase character) to name all classes. _(This style is also commonly referred to as `PascalCase`, `CamelCaps`, or `CapWords`, among [other alternatives][camel-case-variations].)_

_(The **official** CoffeeScript convention is camelcase, because this simplifies interoperability with JavaScript. For more on this decision, see [here][coffeescript-issue-425].)_

For constants, use all uppercase with underscores:

```coffee
CONSTANT_LIKE_THIS
```

Methods and variables that are intended to be "private" should begin with a leading underscore:

```coffee
_privateMethod: ->
```

## Functions

_(These guidelines also apply to the methods of a class.)_

When declaring a function that takes arguments, always use a single space after the closing parenthesis of the arguments list:

```coffee
foo = (arg1, arg2) -> # Yes
foo = (arg1, arg2)-> # No
```

Do not use parentheses when declaring functions that take no arguments:

```coffee
bar = -> # Yes
bar = () -> # No
```

In cases where method calls are being chained and the code does not fit on a single line, each call should be placed on a separate line and indented by one level (i.e., two spaces), with a leading `.`.

```coffee
[1..3]
  .map((x) -> x * x)
  .concat([10..12])
  .filter((x) -> x < 11)
  .reduce((x, y) -> x + y)
```

When calling functions, choose to omit parentheses. Exceptions are allowed if they optimize for readability. Keeping in mind that "readability" can be subjective, the following examples demonstrate cases where parentheses have been omitted or included:

```coffee
baz 12

brush.ellipse x: 10, y: 20 # Braces can also be omitted or included for readability

foo(4).bar(8)

obj.value(10, 20) / obj.value(20, 10)

print inspect value

new Tag(new Value(a, b), new Arg(c))
```

You will sometimes see parentheses used to group functions (instead of being used to group function parameters). Examples of using this style (hereafter referred to as the "function grouping style"):

```coffee
($ '#selector').addClass 'class'

(foo 4).bar 8
```

This is in contrast to:

```coffee
$('#selector').addClass 'class'

foo(4).bar 8
```

In cases where method calls are being chained, some adopters of this style prefer to use function grouping for the initial call only:

```coffee
($ '#selector').addClass('class').hide() # Initial call only
(($ '#selector').addClass 'class').hide() # All calls
```

The function grouping style is not recommended. However, **if the function grouping style is adopted for a particular project, be consistent with its usage.**

## Strings

Use string interpolation instead of string concatenation:

```coffee
"this is an #{adjective} string" # Yes
"this is an " + adjective + " string" # No
```

Prefer single quoted strings (`''`) instead of double quoted (`""`) strings, unless features like string interpolation are being used for the given string.

## Conditionals

Favor `unless` over `if` for negative conditions.

Instead of using `unless...else`, use `if...else`:

```coffee
# Yes
if true
  ...
else
  ...

# No
unless false
  ...
else
  ...
```

Multi-line if/else clauses should use indentation:

```coffee
# Yes
if true
  ...
else
  ...

# No
if true then ...
else ...
```

## Looping and Comprehensions

Take advantage of comprehensions whenever possible:

```coffee
# Yes
result = (item.name for item in array)

# No
results = []
for item in array
  results.push item.name
```

To filter:

```coffee
result = (item for item in array when item.name is "test")
```

To iterate over the keys and values of objects:

```coffee
object = one: 1, two: 2
alert("#{key} = #{value}") for key, value of object
```

## Extending Native Objects

Do not modify native objects.

For example, do not modify `Array.prototype` to introduce `Array#forEach`.

## Exceptions

Do not suppress exceptions.

## Annotations

Use annotations when necessary to describe a specific action that must be taken against the indicated block of code.

Write the annotation on the line immediately above the code that the annotation is describing.

The annotation keyword should be followed by a colon and a space, and a descriptive note.

```coffee
# FIXME: The client's current state should *not* affect payload processing.
resetClientState()
processPayload()
```

If multiple lines are required by the description, indent subsequent lines with two spaces:

```coffee
# TODO: Ensure that the value returned by this call falls within a certain
#   range, or throw an exception.
analyze()
```

Annotation types:

- `TODO`: describe missing functionality that should be added at a later date
- `FIXME`: describe broken code that must be fixed
- `OPTIMIZE`: describe code that is inefficient and may become a bottleneck
- `HACK`: describe the use of a questionable (or ingenious) coding practice
- `REVIEW`: describe code that should be reviewed to confirm implementation

If a custom annotation is required, the annotation should be documented in the project's README.

## Miscellaneous

`and` is preferred over `&&`.

`or` is preferred over `||`.

`is` is preferred over `==`.

`not` is preferred over `!`.

`or=` should be used when possible:

```coffee
temp or= {} # Yes
temp = temp || {} # No
```

Prefer shorthand notation (`::`) for accessing an object's prototype:

```coffee
Array::slice # Yes
Array.prototype.slice # No
```

Prefer `@property` over `this.property`.

```coffee
return @property # Yes
return this.property # No
```

However, avoid the use of **standalone** `@`:

```coffee
return this # Yes
return @ # No
```

Avoid `return` where not required, unless the explicit return increases clarity.

Use splats (`...`) when working with functions that accept variable numbers of arguments:

```coffee
console.log args... # Yes

(a, b, c, rest...) -> # Yes
```