# Hello World
As you may have noticed the code on main page, the hello world program is as follows.
```
Main : Unit -> Unit
Main
{
    PrintLine "Hello, World!"
}
```
The first line, `Main : Unit -> Unit` defines the type signature of procedure `Main`. The notation is borrowed from functions in mathematics, and is read as "`Main` is a procedure which accepts `Unit` and returns `Unit`". The `Unit` type is a sepcial type which is used to denote the absence of a useful value, and can be viewed as `void` in C.

The second line lists the name of procedure and its parameters (none in this case), and the braces delimit the scope of the body of the proceudre.

Inside the body of `Main`, the first line is a call to a procedure `PrintLine` with string argument `"Hello, World!"`. `PrintLine` is a procedure in Haze standard library and is similar to C's `printf`.