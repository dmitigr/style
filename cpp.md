# The C++ programming style

The base of the C++ programming style described here is the style of the C++
Standard Library.

## Indentation and braces

Two spaces must be used for indentation.

The opening brace (`{`) should be placed at the next line only when defining a function, for example:

```c++
void foo()
{
  // ...
}
```

In other cases the opening brace should be placed at the same line, for example:

```c++
class Foo {
  // ...
};
```

`else` should follow after the closing brace (`}`) on the same line.

If a branch of `if` consists of only one line (excluding comments) this line
should not be surrounded with braces, for example:

```c++
if (1 == 2) {
  // this branch contains multiple lines of code
  // ...
} else
  // this branch contains single line of code
```

## Naming

Naming - is an art. The main purposes of naming are consistency and readability.

Like the C++ Standard Library the underscore letter (`_`) must be used to
separate the words of identifiers (so-called *snake case*).

The exception is templates arguments, in which the first letter of each word is
capitalized (so-called *camel case*).

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
|Constant name                          |`constant_name`          |
|Variable name                          |`variable_name`          |
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
possible (at least in theory).

The names of conversion functions must begin with `to_`.

Examples: `to_string`, `to_person`.

## Classes and structures

### Class member definition order

When defining a class, its members should be defined in the following order:

  - `public` section;
  - `protected` section;
  - `private` section.

Each section should define its members in the following order:

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
  - swap().
