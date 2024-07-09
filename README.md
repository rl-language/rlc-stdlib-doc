# RLC language reference

This document explain the language feature of `Rulebook` and the features of the `rlc` compiler.
The generated documentation of the `rlc` standard library can be found in this repository as well.

This is a technical document intended for advanced programers.
If you are new user of Rulebook refer instead to the [rlc repository page](https://github.com/rl-language/rlc), and to the [black jack tutorial](https://github.com/rl-language/rlc?tab=readme-ov-file).

## RLC

`rlc` is the rulebook compiler. It has a command line interface similar to the one of gcc and clang. Given a minimal `rl` file:
```
# example.rl
import serialization.print

fun main() -> Int:
    print("hello world")
```

you can compile it from command line with

```bash
rlc example.rl -o compiled
```

and then test that it works with

```
# linux / macos
./compiled
# windows
./compiled.exe
```

The compilation pipeline works as follow:
* The file passed onto the command line (example.rl in this case), is parsed and so recursivelly are all the files named by `import` statements appearing in the input file.
* The program composed of all imported files is then compiled.
* The program is then linked against the rlcruntime lib, yeilding a executable file.


### Static and shared libraries
If you only wish to compile the program but not link it against the standard library, you can use instead the following command.

```
rlc example.rl -o example.a --compile # -o example.lib on windows
```

which will produce a static library that will only depends on symbols exposed by the rlc runtime, as well as malloc and free. The compiled program will contain the symbol `rl_main`, but will not contain symbol `main`, allowing you to redefine it if you wish. A pure `rl` program does not require to invoke global functions before or after its execution. Therefore you can you can just link a pure rl program in any program of your own and simply use its funcions.

If you wish to create a dynamic library, you can do so with the command
```
rlc example.rl -o example.so --shared # -o example.dll on windows
```
This command will link the runtime library into the so file, generating a dependency onto whaterver libc rlc finds in the system. The command will not define a `main` symbol, allowing you to use the shared object as you wish.


### C/CPP and python wrappers
At the moment `rlc` can automatically generate C/CPP and python wrappers, to allow you to use rlc programs from those languages.
* C headers can be generated with
```
rlc file.rl --header -o file.h
```
which then can be included in a C/CPP program. You can take a look at the `rlc` [tests](https://github.com/rl-language/rlc/blob/master/tool/rlc/test/wrappers/action_with_frame_vars.rl) to see how to do so.

Similarly, you can run
```
rlc file.rl --python wrapper.py
rlc file.rl -o lib.so --shared
```
to produce a library you can import from python. Once again refer to the the [examples](https://github.com/rl-language/rlc/blob/master/tool/rlc/test/wrappers/action_with_frame_vars.rl) to see how to achieve this.

### Optimization level and debug symbols
Optimizations can be enabled with the flag `-O2`
```
rlc file.rl -o file.exe # no optimizations
rlc file.rl -o file.exe -O2 # optimizations
```

debug symbols can be emitted with `-g`.

## Rulebook language
This section describes the language feature of the `Rulebook` language.

### Rulebook types

Rulebook types is composed of primitive types, array types, alternative types, function types, enum types, and class types. `rlc` types have the same ABI as `C` types, making them interoperable.

Primitive types are
* **Int**, a signed 64 bits integer (`int64_t` in c)
* **Float**, a 64 bits floating point number (`double` in c)
* **Byte**, a signed 8 bit integer (`int8_t` in c)
    * For this numeric types, usual operations such as `+`, `-`, `*`, `/`, `%` are defined as builtin operations.
* **Bool**, a 8 bit type with the same behaviour as c++ bool.
    * for bool types the following builtin operations are defined: `and`, `or`, `!`. `and` and `or` are short circuiting.
* **StringLiteral**, a reference to a zero terminated string literal.
* **OwningPtrType**, a special type used to implement the standard library ToDo: explain how it works

### Enum types
Enum types are declared with enum declarations, and the are converted to a class type that contains a signle `Int` called `value`.

The syntax of enums is:
```
enum Color:
  red
  blue

fun return_enum() -> Color:
  return Color::red

fun red_value() -> Int:
  return Color::red.value
```

Enums can declare functions in their body as well.
```
enum Color:
  red
  blue
  fun name()-> String:
    if self == Color::red:
       return "red"s
    if self == Color::blue:
       return "blue"s
    return "unrechable"

fun red_name() -> String:
  return Color::red.name()
```

Finally, enums have a special syntax to write code such as the one of the last snippet faster. You can specify a enum member clause in each field of a enum.

```
enum Color:
  red
    String name = "red"s
  blue:
    String name = "blue"s

fun red_name() -> String:
  return Color::red.name()
```

The last two snippet generate the same code.

### Array types
Array types are composed of a compile time know size, and a underlying type
```
  let x : Int[10]
  x[2] = 1
  x[1] = x[2] + 2
```
Array accesses are checked by default on optimization level 0, and not checked on optimization level 2. The check can be enabled and disabled with `--emit-bound-checks=true/false`.

### Alternative types
Alternative types are used to describe objects that can be of two different types. For example a object that can be a `Float` or a `Int` can be declared as
```
let x : Float | Int
```

Declaration statements such as this one will initialize x to be a alternative that contains the first possible type of the list, in this case the content will be `0.0`.

Objects of type alternative can be assigned from any right hand operand that is either a alternative type with the same alternatives, or any of the possible types of the alternative.
For example

```
let x : Float | Int
x = 0 # valid
x = 1.0 # valid
x = true # invalid

let y : Float | Int
y = 3 # valid
x = y # valid
```

Alternative types can be upcasted with the use of typeguards. For example the following snippet of code is valid, and will ensure that y will be always of type float.
```
let x : Float | Int
if x is Float:
  using T = type(x)
  let y : T
  y = 0.0
```

### Class types

Class types are the most common type of user defined type. A class include both members and methods. For example, a tic tac toe board can be defined as follow.
```
cls Board:
    BInt<0, 3>[3][3] slots
    Bool player_turn
```

Member variables which name starts with `_`, such as `_player_turn` are not accessible from outside of the file in which they have been declared.

The default value of member when a object is constructed can be overridden by defining the methods init.

```
class IntegerThatStartsAt3:
  Int x
  fun init():
    self.x = 3

fun main() -> Int:
  let x : IntegerThatStartsAt3
  print(x) #prints:  {x: 3}
  return 0
```

If you override the init method, you will need to invoke the init method of all the member fields yourself.

The default destruction behaviour can be overriden by defining a custom drop member function. This should be done if only if you are doing some kind of low level programming. If you override the destructor, you will need to call the destructor of the member fields yourself.


### Function types
ToDo, explain how they work


### Functions

RLC functions can be declared only in the global scope of a program. The simples function that can be declared is a function with no arguments and no return values.
```
fun NAME():
  return
```
The previous snippet declares a function called NAME, with no parameters, and no return value, that does nothing.

Function that return a value must declare their intention by specifying the return type before the `:` in their signature.

```
fun return_5() -> Int:
  return 5
```

The previous snippet declares a function called `return_5` with no arguments, that returns a integer.

Functions can have arguments, by specifying them as a comma separated list in the signature brackets.
```
fun sum(Int first, Int second) -> Int:
  return first + second
```

Function arguments have a type and a name, and the type must be specified before the name.

All arguments of functions are passed by reference. Function return types may be marked with `ref`. If they do, the value returned by the function is not returned by copy, but by reference. More on this later, in the call expressions section.

#### Visibility
Function which have a name that start with `_`, such as `_add` are not visible from outside the file in which have been declared.

#### Template functions
# ToDo


### Return statements
Functions with a return type must include at least a return statement, and such return statement must have a expression, as it does in the following snippet.
```
fun sum(Int first, Int second) -> Int:
  return first + second
```

The expression that appears in a return statement must have the same type as the type indicated by the function signature.

When a return statement is encoutered, the execution of the function immediatly terminates, and statements that follow the return statement are not executed.

### If statements
If statments have two forms, with `else-branch` or without `else-branch`.
If statements wihtout `else-branch` have the following syntax

```
if bool_returning_expression():
  some_call1()
  some_call2()
some_call3()
```

The `true-branch` of the if statement (in the example, the calls `some_call()` and `some_call2()`) is executed if and only if the condition expression evaluates to true (`bool_returning_expression()`).

If statements with `else-branch` have the following syntax.
```
if bool_returning_expression():
  some_call1()
  some_call2()
else:
  some_call3()
```
The `else-branch` is executed only if the `true-branch` is not.

### While statments
While statements have the following syntax
```
while bool_returning_expression():
    call1()
    call2()
call3()
```

The body of the while loop keeps being executed until the condition expression (`bool_returning_expression` in the example) evaluates to false.

#### Break statements
When a break statement is encountered, the nearest control flow jump to the statement following the nearest while statement. For example the following snippet of code will print `1`, but not `0`.

```
let x = 0
while x != 2:
    while x != 2:
        if x == 0:
            break
        else:
            print(x)
    x = x + 1
```


#### Continue statements
When a continue statement is encountered, the nearest control flow jump to the statement following the nearest while statement. For example the following snippet of code will print `2`, but not `1`.

```
let x = 0
while x != 2:
    while x != 2:
        x = x + 1
        if x == 1:
            continue
        else:
            print(x)
```

### Using statements
Type alias can be introduced with the usage of alias statements. For example.
```
fun main() -> Int:
	using T = type(6)
	let asd : T
	asd = 10
	return asd - 10
```

using statements can be used both at the function scope or at the globla scope.
Aliases introduced this way do not generate a new type, instead they simply redirect all the use of the alias type to the aliased type.

Aliasies offer the following syntax as well, which deduces the aliased typef rom the expression appearing inside the type() clause.
```
	using T = type(6)
```

### Declaration statements
In rl there are 2 flavors of declaration statements, and 3 types of storage qualifiers.
The simplest declaration statement is a assign declaration statement, in the form
```
let x = exp()
```
which deduces the type of `x` from the expression `exp()`, and removes a reference qualifier from the type if there is any, that is: it makes a copy of `exp()` result if it was a reference.

Alternativelly declaration statments can be construction declaration statements, in the form
```
let x : Int
```
construction declaration statements allocates a variable of the type specified after the colons, and initialize them, by invoking the member function `init` on them.

### Reference declaration statments
Instead of declarting a variable with the keyword let, ref can be used instead
```
ref x = ref_returning_exp()
```

In this case x is not a new variable, but a reference to the variable returned by `ref_returning_exp()`.

### Frame declarations statements
This special declaration statements are explained in the action function section.

### declaration statements destruction
When declaration statements go out of scope, they are destroyed by invoking the member function `drop`.
