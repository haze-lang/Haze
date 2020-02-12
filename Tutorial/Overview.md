# Overview of Haze

## Procedures

A proceudre consists of a set of statements, where each statement is a high level instruction which may or may not evaluate to a value.

```
PrintLine : String -> Unit
PrintLine str
{
    Print (concat str "\n")
}
```

## Delimited Continuations

See [Continuations Tutorial](Continuations.md) for a brief introduction to topic and detailed explanations.

### Capturing Continuations

Standard library procedure `Shift` captures the continuation upto the nearest enclosing `Reset`. `Shift` has following signature.
```
Shift : ((Unit -> b) -> a) -> a
Shift l
```
`Shift` takes one argument of type `((Unit -> b) -> a)` and returns `a`. The parameter `l` is a procedure or lambda expression which takes the current delimited continuation of type `Unit -> b` and returns `a`, which is then returned by `Shift` itself. For example, consider the following snippet.
```
Main : Unit -> Unit
Main
{
    PrintLine "1"
    Shift (k =>
    {
        PrintLine "2"
        k ()
        PrintLine "3"
    })
    PrintLine "4"
}
```
This produces following output.
```
1
2
4
```
Since there is no delimiter in the above example, the continuation captured by `Shift` is undelimited and is not composable.

### Marking Prompts
For capturing composable continuations, standard library procedure `Reset` marks a prompt which acts as the delimiter for any enclosed reification of continuations. `Reset` has following signature.
```
Reset : (Unit -> a) -> a
Reset c
```
The argument to `Reset` is a procedure or lambda expression which takes `Unit` and may return a useful value, which will be returned by `Reset` itself.

```
Main : Unit -> Unit
Main
{
    PrintLine "1"
    Reset (_ =>
    {
        PrintLine "2"
        Shift (k =>
        {
            PrintLine "3"
            k ()
            PrintLine "4"
        })
        PrintLine "5"
    })
    PrintLine "6"
}
```
The above snippet will produce following output.
```
1
2
3
5
4
6
```

### Multi-prompt Continuations

### Reentrant Continuations

## Asynchronous I/O via Fibers

## Functions & Pure Functional Programming

A function is a mapping from values of one type to values of another type. It is equivalent to a mathematical function for sets.

```
concat : String -> String
concat [] ys = ys
concat (x:xs) ys = construct x (concat xs ys)
```


## Type System

### Algebraic Types

## Pattern Matching