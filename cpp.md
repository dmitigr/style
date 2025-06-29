# The C++ programming style

The C++ programming style described here is based on the style of the C++
Standard Library.

## Indentation and braces

Two spaces must be used for indentation.

The opening brace (`{`) should be placed at the next line only when defining
a function or labmda, for example:

```c++
void foo()
{
  const auto bar = []{};
}
```

In other cases the opening brace must be placed at the same line, for example:

```c++
class Foo {
  // ...
};
```

`else` or `else if` should follow after the closing brace (`}`) on the same line.

If a branch of `if` consists of only one line (excluding comments) this line
*must* not be surrounded with braces, for example:

```c++
if (a == b) {
  // this branch contains multiple lines of code
  // ...
} else
  // this branch contains single line of code
```

Empty blocks defined by braces must contains nothing, for example

```c++
struct Foo final {};

void bar()
{}

void baz()
try {
  []{}();
} catch (...) {}
```

## Naming

Naming - is an art. The main purposes of naming are *consistency* and
*readability*.

The underscore letter (`_`) must be used to separate the words of identifiers
(so-called *snake case*) except the templates arguments, in which the first
letter of each word is capitalized (so-called *camel case*).for example:

```c++
template<typename TheTemplateArgument>
struct The_struct {
  void the_function()
  {}
};
```

### Abbrebiations

Abbreviations should be avoided whenever possible. But if the length of name
exceeds the one of the [limits](#length-limits) below, intellectual effort
should be made to shorten the name in a way that doesn't compromise both the
consistency and clarity. For example, if in the class scope there are some
methods that are close in meaning, which are already named without using
abbreviations, then adding another method with a similar meaning using
abbreviations will break the naming consistency. Any abbreviation used that
appears during the project should be included into an abbreviation dictionary
for reuse for better consistency.

### Length limits

|Naming unit|Limit (in characters)|
|:----------|:--------------------|
|Namespace  |10                   |
|Type       |20                   |
|Variable   |32                   |
|Constant   |32                   |
|Function   |32                   |

### Patterns

|Naming unit                            |Pattern                  |
|:--------------------------------------|:------------------------|
|Namespace                              |`namespace_name`         |
|Class (either abstract or conrete) name|`Abstract_class`         |
|Abstract class implementation          |`Foo_abstract_class`     |
|Alias (pseudo-name)                    |`Pseudo_name`            |
|Template argument name                 |`TemplateArgumentName`   |
|Block scope constant name              |`constant_name`          |
|Namespace scope constant name          |`constant_name_g`        |
|Block scope variable name              |`variable_name`          |
|Namespace scope variable name          |`variable_name_g`        |
|Protected (private) member name        |`private_member_name_`   |
|Public member name                     |`public_member_name`     |
|Function name                          |`function_name(arg_name)`|

### Namespaces

The namespace name must be a noun (with or without adjectives) or an adjective
in the singular.

#### Namespace `detail`

The namespace `detail` is a special namespace which contains the implementation
details that are not intended to be used by users. The code contained in this
namespace is subject to change at any time without notifying users.

### Classes

Unlike the C++ Standard Library class names must start with upper case letter.

#### Entities

Entities are nouns in the singular (with or without adjectives).

Examples: `Connection`, `Prepared_statement`.

#### Entity characteristics

Entity charactetistics are adjectives in the singular.

Examples: `Modifiable`, `Parameterizable`.

#### Traits

Structure templates that are used to define functions for compile-time
polymorphism (so-called *traits*) are nouns (with or without adjectives) in the
plural.

Examples: `Conversions`.

### Functions

#### Named constructors

In some cases constructors should be defined as static functions. These functions
must begin with `make`.

Examples: `Person::make_from_json_string`.

#### Functions without side effects

Functions that return the result of a computation that don't *logically* cause
side effects are named nouns (with or without adjectives).

Member functions that return a reference or a pointer to an object without the
transfer of ownership are named nouns.

Examples: `cos()`, `password()`, `encrypted_password()`.

#### Functions with side effects

Function names that *logically* cause side effects (including non-constant member
functions) must begin with a verb.

The names of function members that return an object with the transfer of
ownership to the calling code must begin with a most appropriate verb in each
case (such as `take_`, `pop_`, etc).

#### Conversion functions

Conversion functions performs conversions of *data representations* and possibly
(but don't necessarily) the *data types*. As a result of conversion according to
the law `y=to_y(x)`, the reverse conversion according to the law `x=to_x(y)` is
possible.

The names of conversion functions must begin with `to_`.

Examples: `to_string`, `to_person`.

## Classes and structures

Classes (types) are created only for those entities that are directly related to
the project domain  - the *primary entities*. For example, in the network library
the "IP address" is the one of the primary entities, but in the database driver
it's only one of the possible connection settings. For *secondary* entities,
either fundamental types, standard types, or types from third-party libraries
should be used.

### Class member definition order

When defining a class, its members should be defined in the following order:

  - `public` section;
  - `protected` section;
  - `private` section.

The *recommended* order of members definition of the `public` section is as follows:

  - friends (should be in `protected` or `private` sections);
  - usings which are not depends on class internals;
  - enumerations;
  - inner classes;
  - usings which are depends on class internals;
  - constants;
  - destructor;
  - move constructor;
  - copy constructor;
  - move assignment operator;
  - copy assignment operator;
  - constructors;
  - swap();
  - API.

## Functions

If a programmer can check the correctness of function arguments before call,
then the function itself should only `assert` that the arguments are correct.
