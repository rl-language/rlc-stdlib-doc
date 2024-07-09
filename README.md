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
which then can be included in a C/CPP program. You can take a look at the `¶lc` [tests](https://github.com/rl-language/rlc/blob/master/tool/rlc/test/wrappers/action_with_frame_vars.rl) to see how to do so.

Similarly, you can run
```
rlc file.rl --python wrapper.py
rlc file.rl -o lib.so --shared
```
to produce a library you can import from python. Once again refer to the the [examples](https://github.com/rl-language/rlc/blob/master/tool/rlc/test/wrappers/action_with_frame_vars.rl) to see how to achieve this.

## Rulebook language
This section describes the language feature of the `Rulebook` language.

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

