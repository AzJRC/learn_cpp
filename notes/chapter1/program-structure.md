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

1. Preprocessor directive; it includes the library `iostrem` to the program, which includes the code needed to use `std::cout`. This libray comes within the C++ Standard Library. It contains additional functionality to use in your programs.
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

Unlike human languages, which allows for a lot of ambiguity, the syntax rules of C++ are strictly defined and upheld. 

### Syntax error

Syntax errors are common mistakes that violate syntax rules, like the first example above. Fortunately, such errors are typically straightforward to find and fix, as the compiler will generally point you right at them. 

Compilation of a program will only complete once all syntax errors are resolved.

A syntax error message will look like this:

```bash
prog.cc:5:31: error: expected ';' after expression
```

Here, Clang is telling us that on line 5 at the 31st character, the syntax rules require a semicolon, but we did not provide one.

## Comments

A **comment** is a programmer-readable note that is inserted directly into the source code of the program. Comments are not included in the final executable when the compiler inspects the source code.

There are two types of comments in most programming languages: **Single-line comments** and **multi-line comments**.

1. In C++, single-line comments are defined by prepending any text with two slashes (`//`). For example:

```cpp
std::cout << "Hello world!"; // Everything from here to the end of the line is ignored
```

2. In the case of multi-line comments, the character combination pair of `/*` and `*/` denotes a C-style multi-line comment. For example:

```cpp
/* This is a multi-line comment.
   This line will be ignored.
   So will this one. */
```

### Commenting best practices

Comments should be used for three things:

1. To describe what a library, program, or function, does. E.g.

```cpp
// This program calculates the student's final grade based on their test and homework scores.
```

2. To describe how the code is going to accomplish its goal within a library, program, or function.

```cpp
/* To calculate the final grade, we sum all the weighted midterm and homework scores and then divide by the number of scores to assign a percentage, which is used to calculate a letter grade.*/
```

3. Finally, at the statement level, to describe why the code is doing something. This last use case is often done wrong by programmers. **A bad statement comment explains what the code is doing.**

    The following are a bad and a good example of a statement level comments, respectively:

```cpp
// Calculate the cost of the items
cost = quantity * 2 * storePrice;

// This is bad because we can see that this is a cost calculation, but why is quantity multiplied by 2?
```

```cpp
// We need to multiply quantity by 2 here because they are bought in pairs
cost = quantity * 2 * storePrice;

//This is good because now we why this formula makes sense.
```

Moreoever, comments are a great way to remind yourself (or tell somebody else) the reason you made one decision instead of another. E.g.

```cpp
// We decided to use a linked list instead of an array because
// arrays do insertion too slowly.
```

comments should be written in a way that makes sense to someone who has no idea what the code does. Reading individual lines of code is easy. Understanding what goal they are meant to accomplish is not.

```diff
+ Best practice: Comment your code liberally, and write your comments as if speaking to someone who has no idea what the code does. Don’t assume you’ll remember why you made specific choices.
```

### Commenting out

Converting one or more lines of code into a comment is a process called **commenting out**. 

There are quite a few reasons you might want to do this:

1. You’re working on a new piece of code that won’t compile yet, and you need to run the program.
2. You’ve written new code that compiles but doesn’t work correctly, and you don’t have time to fix it until later.
3. To find the source of an error.
4. You want to replace one piece of code with another piece of code.

Commenting out code is a common thing to do while developing, so many IDEs provide support for commenting out a highlighted section of code. For VS Code for example, we can use the key binding `ctrl + /` to comment out selected code.

## Objects and Variables

Programs generate results by manipulating (reading, changing, and writing) data. In computing, **data** is the term used to refer to any information that can be moved, processed, or stored by a computer.

Programs are collections of instructions that manipulate data to produce a desired result. Computer programs also fall under the definition of data; however, we often use the term **code** to mean the program itself  that manipulates the data, and **data** to mean the information that the program works with to produce a result.

In programming, a single piece of data is called a **value** (sometimes called a data value). Examples include numbers (like the number `5` or the number `3.14`), characters (like the character `a` or the control character `\n`), among others.

```
Important: Values that are placed directly into the source code are called literals.
```

### Objects

In C++, direct memory access is discouraged. Instead, we access memory indirectly through an object.

An **object** represents a region of storage (typically RAM or a CPU register) that can hold a value. In C++, everything that occupies memory with a defined type is considered an object. This usage aligns with the ISO C++ standard.

In C++, objects can be unnamed. However, we will often name our objects using an **identifier**. An object with a name is called a **variable**.

```
Important: In higher-level programming languages, the term "object" usually refers to a dynamic collection of key-value pairs. For example, In JavaScript, an object is like a dictionary or JSON. In Python, an object can be anything that is an instance of a class. Here, "object" is strongly tied to OOP (Object-Oriented Programming), not just memory regions.

Do not confuse the concept of objects used in C++ with the OOP object used in more higher-level programming languages.
```

Finally, keep in mind that in C++ the term object has a narrower definition that excludes functions.

### Variables

As we said before, an object with a name is called a **variable**.

In order to use a variable in our program, we need to tell the compiler that we want one. To do so, we use a special kind of declaration statement called **definition**, like in the following example:

```cpp
int x; // define a variable named x (of type int)
double y; // define a variable named y (of type double)
```

At **compile-time**, the compiler will make a note to itself that we want a variable with the name x when it reads the definition. From that point forward, whenever we use the identifier `x` in our code, the compiler will know that we are referring to this variable..

On the other-hand, at **runtime**, each object is given an actual storage location (such as RAM, or a CPU register) that it can use to store values. The process of reserving storage for an object’s use is called **allocation**. 

```diff
+ Best practice: define each variable in a separate statement on its own line (and then use a single-line comment to document what it is used for).
```

### Data types

A **data type** is what determines what kind of value the object will store.

In C++, the type of an object must be known at compile-time (i.e. it must be defined in the source code), and that type can not be changed without recompiling the program. 

In C++, to define a variable, we declare first the datatype and just after the name of the object (also known as variable name): `int myNumber;` Notice that we declared an integer number that still does not have any value assign to it.

### Variable initialization

After a variable has been defined, you can give it a value (in a separate statement) using the `=` operator. This process is called assignment, and the `=` operator is called the **assignment operator**.

```cpp
int a;   // define an integer variable
a = 10;  // assignment of value 5 into variable a
```
Assignment can be used whenever we want to change the value held by a variable. The following code snipped shows a series of operations explained one by one:

```cpp
#include <iostream>

int main()  
{  // Execution of the program begins here, at the top of main()
	int width; // First, the program defines a variable named width and allocates enough space to store any integer
	width = 5; // Second, the program assigns the value 5 to the variable width

	std::cout << width; // This part of the code prints whatever is stored in width variable (an integer value of 5) to the console

	width = 7; // Then, we reassign the integer value of width to 7

	std::cout << width; // This part of the code prints 7 to the console

	return 0;   // Finally, the program exits with status code 0 (success)
}
```

```diff
- Warning: You may know that there is a similar operator `==`. Do not confuse the equality operator (`==`) with the assignment operator (`=`). The former compares if two variables have the same value, while the last assigns a value to a variable.
```

You can combine the variable declaration and variable assignment statements into a one unique instruction often refered as ***variable initialization**: E.g. `int a = 10`. The process of specifying an initial value for an object is called **initialization**, and the syntax used to initialize an object is called an **initializer**.

However, there are several ways to initialize a variable:

```cpp
int a;         // default-initialization (no initializer)

// Traditional initialization forms:
int b = 5;     // copy-initialization (initial value after equals sign)
int c ( 6 );   // direct-initialization (initial value in parenthesis)

// Modern initialization forms (preferred):
int d { 7 };   // direct-list-initialization (initial value in braces)
int e {};      // value-initialization (empty braces)
```

There are even more complex ways of initialization, but those are out-of-scope of the current notes.

The following list presents a few characteristics of the previous listed initialization types:

- **Default Initialization**
   - Occurs when no initializer is provided.
   - Default-initialization performs no initialization.
   - Even though the variable has no value explictly assigned, the variable gets assigned an indeterminate value refered as the **garbage value**.
      - This garbage value is often the cause of many bugs and weird behavior in C/C++ programs.
- **Copy Initialization**
   - Ocurrs when an initial value is assigned using the assignment operator just after the variable declaration, in one statement.
   - This used to be the most common type of initilization used by programmers.
      - Often used for programmers who appreciate its readability.
   - Copies the value on the right-hand side of the equals into the variable being created on the left-hand side.
   - Used whenever values are implicitly copied
      - Return functions
      - Passing arguments to a functions
      - Catching exceptions
- **Direct Initilization**
   - Occurs when an initial value is provided inside parenthesis.
   - Initially introduced to allow more efficient initialization of complex datatypes.
      - Now is being superseded by direct-list-initialization, a most modern way of variable initialization in C++.
   - Is commonly used when values are explicitly cast to another type.
- **List Initialization**
   - This is the modern way to initialize objects in C++.
   - Makes use of curly braces instead of the assignment operator.
   - Also known as **uniform initialization** or **brace initialization**.
   - It comes in two forms:
      - Direct List Initilization do not uses the assignment operator. E.g. `int width { 5 }; `
      - Copy List Initilization uses the assignment operator. E.g. `int width = { 5 };`
         - This one is rarely used
   - List initialization was introduced to provide a initialization syntax that works in almost all cases.
      - List initialization provides a way to initialize objects with a list of values rather than a single value.
   - List Initialization does not allow **narrowing conversions**.

The term **narrowing conversion** refers to the situation when the value of a variable has to change to another data type to be suitable for the original variable's data type. For example, a fractional value is rounded when it is converted to an integral type, and a numeric type being converted to Boolean is reduced to either `True` or `False`.

```cpp
int main()
{
    // An integer can only hold non-fractional values.
    // Initializing an int with fractional value 4.5 requires the compiler to convert 4.5 to a value an int can hold.
    // Such a conversion is a narrowing conversion, since the fractional part of the value will be lost.

    int w1 { 4.5 }; // compile error: list-init does not allow narrowing conversion

    int w2 = 4.5;   // compiles: w2 copy-initialized to value 4
    int w3 (4.5);   // compiles: w3 direct-initialized to value 4

    return 0;
}
```

Note that this restriction on narrowing conversions only applies to the list-initialization, not to any subsequent assignments to the variable.

There is one final type of basic initialization called **value-initialization**. When a variable is initialized using an empty set of braces, this will implicitly initialize the variable to zero (or whatever value is closest to zero for a given type). When zeroing occurs, this is called **zero-initialization**.

```diff
+ Best Practice: Prefer direct-list-initialization or value-initialization to initialize your variables. This form of initialization is generally preferred over the other initialization forms because it works in most cases (and is therefore most consistent).
```

### Direct List Initialization vs Value Initialization (or Zero Initialization)

Use direct-list-initialization when you’re actually using the initial value. Otherwise, use value-initialization when the object’s value is temporary and will be replaced.

```cpp
int x { 0 };    // direct-list-initialization with initial value 0
std::cout << x; // we're using that 0 value here

int x {};      // value initialization
std::cin >> x; // we're immediately replacing that value so an explicit 0 would be meaningless
```

At the end of the day, you may stick to one kind all the time and it shouldn't impact your code at all. However, using it as described before will make your code more compliant to the actual use cases of each initialization type (It just makes it look cleaner).

Just make sure that you initialize your variables upon creation.

### instantiation

There is another fancy term called **instantiation** that means a variable has been created (allocated) and initialized (this includes default initialization). There is nothing important about this concept beyond enriching your vocabulary.

### Initializing multiple variables

It is possible to define multiple variables of the same type in a single statement.

```cpp
int a, b; // create variables a and b, but do not initialize them
```

```diff
- Bad Practice: Often, declaring variables in one line isn't prefered because it affects the readability. However, many programs makes use of this syntax just to make the code more compact.
```

You can also initialize multiple variables defined on the same line:

```cpp
int a = 5, b = 6;          // copy-initialization
int c ( 7 ), d ( 8 );      // direct-initialization
int e { 9 }, f { 10 };     // direct-list-initialization
int i {}, j {};            // value-initialization
```

Notice that each variable has its own initializer, and that's a common pitfall when declaring multiple initialized variables in one statement.

```cpp
int a, b = 5;     // wrong: a is not initialized to 5!
int a = 5, b = 5; // correct: a and b are initialized to 5
```

The first statement above may or may not cause your compiler to complain. In the second case, this will be a great example of how bugs in programs start to happen.

If for some reason you need to use this syntax, remember that *each variable can only be initialized by its own initializer*.

### `[[maybe_unused]]` Attribute

Is important to note that unused initialized variables in your C++ programs will trigger warnings (or errors if "treat warnings as errors" `-Werror` flag is included when compiling).

You may either solve this by just using the unused variables, or removing them, but sometimes this is not the correct way to act.

For such cases when removing unused variables isn't appropiate (because we may use them later), C++17 introduced the `[[maybe_unused]]` attribute, which allows us to tell the compiler that we’re okay with a variable being unused.

```cpp
#include <iostream>

int main()
{
    // Don't complain if pi is unused
    [[maybe_unused]] double pi { 3.14159 };

    // Don't complain if phi is unused
    [[maybe_unused]] double phi { 1.61803 }; 

    // Don't complain if gravity is unused
    [[maybe_unused]] double gravity { 9.8 }; 

    std::cout << pi << '\n';  // pi used
    std::cout << phi << '\n'; // phi used
                              // gravity not used

    // but the compiler will no warn about gravity not being used

    return 0;
}
```

Additionally, the compiler will likely optimize these variables out of the program, so they have no performance impact.

## Final notes

-  Difference between initialization and assignment
   - Initialization gives a variable an initial value at the point when it is created. Assignment gives a variable a value at some point after the variable is created (`int a {10};`).
- Difference between default-initialization and value-initialization
   - Default initialization is when a variable is initialized without a initializer (somewhat contraintuitive, but is as it is), like `int a;`. In most cases, this left the variable with an indeterminate value.
   - Value-initialization is when a variable initialization has an empty brace initializer, like `int a {}`. In most cases, this will cause a zero-initialization.
   - You should prefer value-initialization, as it initializes the variable to a consistent value.