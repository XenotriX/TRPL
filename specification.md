# Language Specification for TRPL

Status: Draft

Version: 1.0

[TOC]

##  Identifier

An **Identifier** is a unique name. An identifier must begin with a letter or and underscore.

```
✔	myVar
✔	myVar1324
✔	_1234
✖	1myVar
✖	1324
```

## Variables

**Variables** are values stored in memory that can be accessed by an **Identifier**. A **Variable** can be of any Data Type.

## Typing

### Data Types

Variables are dynamically typed.

#### Number

Represents any number.

Numbers are stored as 64-bit floating-point numbers.

Number literals can be written as an integer without a decimal point:

```
1234
```

or as a decimal:

```
1234.567
```


#### Boolean

Binary value.

Either `true` or `false`.

> Non-boolean variables cannot be "truthy"

#### String

Represents an array of characters.

String can be concatenated using the `+` operator.

```
"Hello, World!"
```

> Note that the `+` operator used to concatenate Strings is not the same as the one used when adding Numbers.

#### Array

Stores a list of variables of any data type. Elements of an array are accessed using a numeric value.

```
[ 1, 2, 4.5, 10 ]
```

```
[ "Hello,", "World!" ]
```

#### Object

Stores a list of key-value pairs. The key must be an Identifier.
```
{
    firstname: "John",
    lastname : "Doe"
}
```

#### Function

Functions have no side-effect. They have no access to variables except the ones given as arguments.

Since this is a functional language, functions can be stored in any variable.

When an Identifier referring to a **Function** is immediately followed by `()`, the function will be executed. The arguments must be placed between the parenthesis.

```
var myFunc = (x) -> {
    print (x 5 +)
}

var myVar = 5
myFunc(myVar) // prints 10 in the terminal
```

### Type casting

There is no implicit typecasting, when mixing variables of different types, they must be explicitly cast to the same data type.

Type casting is done by using a colon followed by the desired data type immediately after the variable that is to be converted.

```
var x = 5
print "The value of x is: " + x
```

In case a cast should no be possible, the resulting value will be `undefined`.

#### Valid casts

| To\From  | Number | Boolean | String | Array | Object | Function |
| -------- | :----: | :-----: | :----: | :---: | :----: | :------: |
| Number   |   ✔    |    ✔    |   〜   |   ✖   |   ✖    |    ✖     |
| Boolean  |   ✔    |    ✔    |   〜   |   ✖   |   ✖    |    ✖     |
| String   |   ✔    |    ✔    |   ✔    |   ✔   |   ✔    |    ✖     |
| Array    |   ✖    |    ✖    |   *    |   ✔   |   ✖    |    ✖     |
| Object   |   ✖    |    ✖    |   *    |   ✖   |   ✔    |    ✖     |
| Function |   ✖    |    ✖    |   ✖    |   ✖   |   ✖    |    ✔     |

✔	: Always possible

✖	: Not possible

〜	: Only when the string represents a number or a boolean.

\*	: Not possible but might be implemented later.

## Arithmetic

The [Reverse Polish notation](https://en.wikipedia.org/wiki/Reverse_Polish_notation) is used for arithmetic.

```
4 5 +
```

```
func(x 2 +) 5 -
```

> The advantage of using the RPN is that the order of operation does not need to be inferred

> Only Numbers and Booleans can be used in arithmetic operations.

## Operators

 `+`, `-`, `*`, `/`, `==`, `!=`, `>`, `<`, `>=`, `<=`

## Built-in commands

Unlike Functions, commands are *"hard-coded"* in the interpreter. They are not written in the language itself, giving them the possibility to do things other functions cannot.

Syntactically, they differ from functions in that they do not require parenthesis to be called.

### Print

The `print` command can be used to print text in the console.

```
print "Hello World"
```

```
print 1234
```

### Type of

The `typeOf` command returns the type of the Expression given as argument.

```
typeOf "Hello, world!" // "String"
```

```
var x = 5
var y = x 2 +
typeOf y // "Number"
```

### Load

The `load` command can be used to load and execute code from a file.

```
load "script.rs"
```

### Exit

The `exit` command terminates the program.

```
exit
```

## Assignments

There are two ways of assigning variables:

### By value

When assigning by value, the expression on the right-hand side is evaluated and the result of the evaluation is assigned to the identifier on the left.

```
Identifier := Expression
```

### By expression

When assigning by expression, the expression on the right-hand side itself is assigned to the identifier on the left.

```
Identifier = Expression
```

## Declarations

There are two types of declarations:

### Variables

Variables can change during runtime.

```
var Identifier

var Identifier = Expression

var Identifier := Expression

var Identifier := (x) -> {
    Print x
}
```

### Constants

Once declared, constants cannot be changed. Trying to change a constant results in an error.

```
const Identifier := Expression
```

## Flow Control

### If Statement

The `if` statement can be used to execute code **conditionally**. It consists of a **condition**, a **then** block and optionally an **else** block. When executed, the condition is evaluated and if it results to true, the then block is executed and in case it results to false or undefined, the else block is executed.

```
if (Expression) {
	// code
}
else {
	// code
}
```

> Else if statements are not part of the version of the language but will probably be implemented in a later point in time.

### While loop

The `while` loop can be used to **repeatedly** execute a block of code while a **condition** is `true`. 

```
while (Expression) {
    // Code
}
```

## Comments

Lines can be commented out using `//`.
