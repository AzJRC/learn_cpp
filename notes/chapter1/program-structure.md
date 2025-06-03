# Program Structure

## Statements

**Statements** are the smallest units of programmable computational actions that can be used in lenguages like C++. A Statement is a high-level intructions that tells the computer *to do something*; namely, iterate over a number or decide between two options.

A statement in C++ is often translated into several machine language instructions: The actual smallest units of programmable computational actions, just above straight binary.

## Functions

Often, statements are grouped into a logical unit called **function**. A function is a collection of statements that get executed sequentially (in order, from top to bottom).

```diff
* Important: Every C++ program must have a special function named main. The main function is where the program always begins and often terminates.
```

Functions are typically written to do a specific job or perform some useful action. For example, `max()` might contain statements that figures out which of two numbers is larger.

When discussing functions, it’s fairly common shorthand to append a pair of parenthesis to the end of the function’s name, like `main()` and `max()`, which are read as the "function main" and the "function max", respectively.

## Characters and text

A **character** is a written symbol or mark, such as a letter, digit, punctuation mark, or mathematical symbol. Then, a sequence of characters is called text, or in programming contexts, a **string**.

### Control Characters

Computers have an additional type of character, called a “control character”. These do not have any special meaning for humans, but instead for computers. For example, in C and C++ the control character `\n` means "new line", and the character `\t` means "tab" (A constant number of spaces).

## Understanding Hello World

```cpp
#include <iostream>

int main()
{
   std::cout << "Hello world!";
   return 0;
}
```

The following list describes what each line of the previous code does:

1. Preprocessor directive; it includes the library `iostrem` to the program, which includes the code needed to use `std::cout`.
2. Blank line for readability.
3. Declaration of `main()`. The name of the function is often refered as the "function identifier", in this case, `main`. Moreover, the function returns a value of type `int`, which means "integer".
4. The open curly brace tells the compiler "here begins the `main()` body". Every statement below this curly braces is considered part of `main()`, until a closing curly brace is detected.
5. Here is where the statement `std::cout` is used. "cout" means "character output". Then, the operator `<<` in this context means we want to output the characters `Hello world` to the console.
6. This is a return statement, which is often mandatory to any function that returns a value. In this case, we are returning the integer 0. The `main()` will be the last part of the program, and therefore, the return value will be read by the operating system. It is a convention to return 0 when the code run successfully and 1 (or any non-zero number) when there was an error.
7. The close curly brace. This tells the compiler "here ends the `main()`".

## Syntax

**Syntax** is the set of rules that describe how specific words (and punctuation) can be arranged to form valid sentences in a programming language like C++. For example, syntax rules for C++ we tells us that we must end every statement with a semicolon, thus, the following statement would be invalid:

```cpp
std::cout << "Hello World",
```

But the following example is a valid statement:

```cpp
return 1;
```

### Syntax error