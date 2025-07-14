---
tags:
  - Tutorial
  - cpp
Status: IN PROGRESS
Website: https://www.learncpp.com/
---
[[C++]] tutorials and learning materials.
# Progress
Skipped around some chapters that aren't necessary for 42 school right now
24.7
# Bookmarks - Stuff to remember
My personal bookmarks are those of someone that comes from a small background of working in C over several months in a wide variety of projects.
This is why I'm not noting everything down, only those things relevant to someone with knowledge of standard C.
If you want to know the specifics of a particular note of mine, or don't understand what I've written, go read the related section of learncpp.com!
## 0 - Introduction
### 0.1
Don't code when you're tired or stressed out. Sort out the things that stress you out or go sleep or something. Then come back and write good code.
Tired/stressed out programmers often write bad code. Sometimes they don't, but most of the time they do. **You aren't that guy.**
### 0.2
> Platforms often provide useful services for the programs running on them. For example, a desktop application might request the operating system give them a chunk of free memory, create a file over there, or play a sound. The running program doesn’t have to know how this is actually facilitated. If a program uses capabilities or services provided by the platform, it becomes dependent on that platform, and cannot be run on other platforms without modification. A program that can be easily transferred from one platform to another is said to be **portable**. The act of modifying a program so that it runs on a different platform is called **porting**.

> Some cool info to be added to [[Assembly]].
> An **assembly language** (often called **assembly** for short) is a programming language that essentially functions as a more human-readable machine language.
> Just like each CPU family has its own machine language, each CPU family also has its own assembly language (which is designed to be assembled into machine language for that same CPU family). This means there are many different assembly languages. Although conceptually similar, different assembly languages support different instructions, use different naming conventions, etc…

> Some cool info to be added to [[Interpreter]].
> Alternatively, an **interpreter** is a program that directly executes the instructions in the source code without requiring them to be compiled first. Interpreters tend to be more flexible than compilers, but are less efficient when running programs because the interpreting process needs to be done every time the program is run. This also means the interpreter must be installed on every machine where an interpreted program will be run.
> A good comparison of the advantages of compilers vs interpreters can be found [here](https://stackoverflow.com/a/38491646).
### 0.4
Take some time to design solutions to problems before diving right in. Go to the drawing board, so to say, and conceptualize.
Maybe make an Obsidian Canvas.
Defining the problem is just as important as designing as solution.
On how to design good solutions to problems :
> Typically, good solutions have the following characteristics:
- They are straightforward (not overly complicated or confusing).
- They are well documented (especially around any assumptions being made or limitations).
- They are built modularly, so parts can be reused or changed later without impacting other parts of the program.
- They can recover gracefully or give useful error messages when something unexpected happens.\

> When you sit down and start coding right away, you’re typically thinking “I want to do ”, so you implement the solution that gets you there the fastest. This can lead to programs that are fragile, hard to change or extend later, or have lots of bugs.
## 1 - C++ Basics
### 1.2 - Comments
There are several types of comments, like the [[Doxygen]] comments found at a function's start for librairies, or the inline comments for specific parts of the code.

> [!WARNING] Good and bad comments
> In general, you'll want as a rule to not so much describe what's happening (what is already understandable by just reading the code), but rather explain **why** a line of code is the way it is.

You can also use comments to explain why a certain approach was used and not another. This prevents you from coming back to your code after a while and going "well why didn't we do it that way?".

> [!SUCCESS] Best practice
> Comment your code liberally, and write your comments as if speaking to someone who has no idea what the code does. Don’t assume you’ll remember why you made specific choices.
> - At the library, program, or function level, use comments to describe _what_.
> - Inside the library, program, or function, use comments to describe _how_.
> - At the statement level, use comments to describe _why_.
### 1.4
Apparently in [[C++]], initialization of variables is a whole thing. It's not just about saying `x = 4` anymore, you can do crazy stuff with braces, parentheseses and more.
```cpp
int a;         // no initializer (default initialization)
int b = 5;     // initializer after equals sign (copy initialization)
int c( 6 );    // initializer in parentheses (direct initialization)

// List initialization methods (C++11)
int d { 7 };   // initializer in braces (direct list initialization)
int e = { 8 }; // initializer in braces after equals sign (copy list initialization)
int f {};      // initializer is empty braces (value initialization)
```
### 1.5
Keep in mind `std::cout` is buffered, which means some output might only appear past a certain point.
`std::cin` is also buffer, which is how C++ extracts variables from the input in cases like `std::cin >> x`.
If there's still valid input in the `cin` buffer, it will extract that value instead of prompting the user for input.
For example, if you want to extract two values, even if there are `std::cin >> x` and `std::cin >> y` on separate lines, if your input contains `4 5`, you'll only have to press enter once for both variables to be filled with 4 and 5 respectively.
> `std::cin` is buffered because it allows us to separate the entering of input from the extract of input. We can enter input once and then perform multiple extraction requests on it.
> Here’s a simplified view of how operator `>>` works for input.
> 1. If `std::cin` is not in a good state (e.g. the prior extraction failed and `std::cin` has not yet been cleared), no extraction is attempted, and the extraction process aborts immediately.
> 2. Leading whitespace characters (spaces, tabs, and newlines at the front of the buffer) are discarded from the input buffer. This will discard an unextracted newline character remaining from a prior line of input.
> 3. If the input buffer is now empty, operator `>>` will wait for the user to enter more data. Any leading whitespace is discarded from the entered data.
> 4. operator `>>` then extracts as many consecutive characters as it can, until it encounters either a newline character (representing the end of the line of input) or a character that is not valid for the variable being extracted to.

> [!ERROR] Failed extractions
> If an extraction fails, the input buffer will be pretty much unusable until it is completely cleared (flushed).
### 1.8
Adopt the style of the project you're currently working in, if it's not yours. Better to work with consistency than with whatever you happen to prefer.
Learn to use your IDE's formatting features so you keep a consistent formatting throughout your project(s). [[clang-format]] is pretty good.
### 1.9
A function is said to have a **side effect** when it does more than just return a value. It could for example modify its arguments, or some other static variable elsewhere.
They aren't a bad thing as the name would suggest, just a way to use and design functions.
### 1.11
Theory crafting a program before getting to start coding it is a good thing, but remember that **you need to write a program once to know how you should have written it in the first place**.
In other words, you will very probably not be able to produce a perfect result first try.
The best way to find how you should write something is to just write it : you'll find the problems with your approach easier that way, rather than staying in front of the white board waiting for the light to illuminate your thoughts.
**Perfection in programming is an iterative process.**

## 2 - Functions
### 2.2
Use `EXIT_SUCCESS` and `EXIT_FAILURE` instead of your own return statuses for the `main()` function. (they're defined in `<stdlib>` btw)
### 2.5
Locality of behavior : **try to define your variables as close to the place they're used as possible**.
Difference between objects and identifiers : identifiers hold the scope (and name) of an object. An identifier tagged onto an object makes a variable.
### 2.6
Remember that **functions should always do one specific task only**.
### 2.9
Do not use `using` directives, since they're here only for including namespaces' entire symbols, it negates the entire point of namespaces. Just don't use them.
### 2.10
It's the pre-processor's job to clean the code for the compilation stage (removing the comments, processing include directives, etc...)
A **translation unit** is a source file after it has been pre-processed.
### 2.11
Source files that have a paired header should include said header.
c++ standard headers are usually in the `<xxx>` format like `<iostream>`, and c standard headers are usually `<xxx.h>` like `<stdio.h>`.
Of course, user defined headers are still formatted like "xxx.h", just like in C.
Some standard headers include other standard headers. **Don't forget to include all headers you need explicitly.**
### [2.13](https://www.learncpp.com/cpp-tutorial/how-to-design-your-first-programs/)
Some great advice on how to design programs and prepare game plans for them before starting to code.
**Break hard problems into small, easier problems.** This advice is also useful when making todo lists.
Don't optimize at the micro level, like a few statements at a time. Optimization is better for maintainability than performance, and a well structured program is better optimized **by design**.
> A complex system that works is invariably found to have evolved from a simple system that worked
—John Gall, Systemantics: How Systems Really Work and How They Fail p. 71

***THE DESIGN STAGE IS VERY IMPORTANT***
## 3 - Debugging
### 3.4
When printf debugging in C++, use `cerr` instead of `cout`. Since `cout` is buffered, it might not output what you want in time (or at all if the program crashes).
### 3.5
There's also `clog` for extended logging capabilities. By default, it writes to stderr but you might find better uses of it with a dedicated logger library.
> Plog is implemented as a set of header files, so it’s easy to include anywhere you need it, and it’s lightweight and easy to use.
### 3.6
```cpp
std::cout << std::unitbuf; // enable automatic flushing for std::cout (for debugging)
```
### 3.7
"set next statement" is a debugger command a bit akin to a goto call, basically makes the execution point jump to another line in the program. You could even go backwards with this little beauty.
### 3.8
Some debuggers allow you to set a breakpoint on a watched variable, which means the execution will be stopped everytime the variable changes.
### 3.9
The Call Stack is the trace of all functions that have been called up until a specific point in execution.
### 3.10
**Defensive programming** is the practice of trying to predict all user misinputs or misuses and mitigating the errors that would be produced (for example inputting alphabetical characters where numbers are expected).
Some good static analysis tools: 
- [clang-tidy](https://clang.llvm.org/extra/clang-tidy/) (you have that in CLion btw)
- [cpplint](https://github.com/cpplint/cpplint)
- [cppcheck](https://cppcheck.sourceforge.io/) (already integrated into Code::Blocks)
- [SonarLint](https://www.sonarsource.com/open-source-editions/)
## 4 - Fundamental data types
### 4.1
**Integral types** are fundamental types that are stored in memory as integers, but don't necessarily display as integers when you print them out (booleans).
### 4.2
**Incomplete types** are types that the compiler cannot figure out a size in bytes just yet.
`void` is the best example.
> [!WARNING] Functions that don't take any arguments
> Unlike in C, the used of `function(void)` to specify that a function doesn't take any arguments is deprecated in C++.
### 4.3
The `sizeof` operator is an operator, not a function, despite what the syntax would lead you to believe.
It cannot be used for dynamically allocated memory.
### 4.4
When dividing two integers, the result will also be an integer. In effect, the decimal part is simply dropped. NO rounding.
### 4.5
You don't need this much optimization to use unsigned integers instead of signed ones. Just use signed integers with everything you do, mkay? When you need more optimization (in cases with thousands of variables, for example), you'll see it and be able to use fixed-width integers.
### 4.6
TLDR : fixed width integers are nice. Use them.
Also use `<cstddef>` for including `size_t`, it's the smallest header that contains it.
>- Prefer int when the size of the integer doesn’t matter (e.g. the number will always fit within the range of a 2-byte signed integer). For example, if you’re asking the user to enter their age, or counting from 1 to 10, it doesn’t matter whether int is 16-bits or 32-bits (the numbers will fit either way). This will cover the vast majority of the cases you’re likely to run across.
>- Prefer std::int_t when storing a quantity that needs a guaranteed range.
>- Prefer std::uint_t when doing bit manipulation or well-defined wrap-around behavior is required (e.g. for cryptography or random number generation).
>Avoid the following when possible:
>- short and long integers (prefer a fixed-width integer type instead).
>- The fast and least integral types (prefer a fixed-width integer type instead).
>- Unsigned types for holding quantities (prefer a signed integer type instead).
>- The 8-bit fixed-width integer types (prefer a 16-bit fixed-width integer type instead).
>- Any compiler-specific fixed-width integers (for example, Visual Studio defines \_\_int8, \_\_int16, etc…)
### [4.7](https://www.learncpp.com/cpp-tutorial/introduction-to-scientific-notation/)
A good scientific notation round up.
Significant digits are the digits that are needed to not lose any information about a number. That includes both digits before and after the decimal point.
### 4.8
`double` is double the precision of the `float`. Basically double the digits after the decimal point (I think).
When assigning with a literal, `x = 3.0` will assume x is a `double`, while `x = 3.0f` assumes a `float` type.
> The precision of a floating point type defines how many significant digits it can represent without information loss.

`std::setprecisions()` allows you to set the precision at which `std::cout` will output floating point variables and literals.
When trying to store a number with 10 significant digits in a type with only 7 digit precision, you end up losing on 3 digits of precision. This applies to not only fractional numbers, but also numbers that are too big for a float could lose some of their precision too (123456789.0f becoming 123456792, for example).
> **Favor double over float unless space is at a premium, as the lack of precision in a float will often lead to inaccuracies.**

Due to the way floating numbers are stored in binary format, even simple numbers such as 0.1 will be stored in a way that loses precision.
In the end, 0.1 is actually something like 0.10000000000000001.
Because of all of this, beware of using floating numbers for critical data like finances or currency stuff, as repeated operations will increase the rounding error that occurs.
### 4.12
Casting in c++ is done via `static_cast`, with the syntax `static_cast<new_type>(expression)`.
Things in angled brackets `<>` are very often types.
## 5 - Constants and Strings
### 5.1
If a variable can be made const, do it. It helps the compiler optimize.
### 5.2
The f character found after float literals like `2.0f` are actually part of a plethora of literal values suffixes. There's one for almost every type out there, but the float one is pretty much the only one you'll use.
### [5.3](https://www.learncpp.com/cpp-tutorial/numeral-systems-decimal-binary-hexadecimal-and-octal/)
Primer on numerical systems like binary, hexadecimal and octal.
Use a `0` prefix on number literals to make them octal literals.
Use a `0x` prefix on number literals to make them hexadecimal literals.
### 5.4
**Profilers** are programs that analyse a program and tells which parts of it takes the longest time to run, or which are impacting performance the most.
> Compile-time evaluation allows the compiler to do work at compile-time that would otherwise be done at runtime. Because such expressions no longer need to be evaluated at runtime, the resulting executables are faster and smaller (at the cost of slightly slower compilation times).
### 5.5
The `constexpr` type modifier asks for an expression to be evaluated at compile-time.
Constant expressions (not the keyword, we mean literals, variables etc that do not change) must be evaluatable at compile-time.
> The compiler is only _required_ to evaluate constant expressions at compile-time in contexts that _require_ a constant expression. It may or may not do so in other cases.

Floats and doubles aren't compile-time constant expressions, because they aren't integrals.
### 5.6
`const` variables are values that cannot be changed after initialization.
`constexpr` variables are values that can be used in constant expressions.
### 5.7
Use `std::string` instead of `char *` when working with strings in C++.
When trying to get a full string as input from `cin`, use `std::getline` (it will keep reading input until a new line is found, which means whitespace is ignored, unlike with `cin`)
Get the length of an `std::string` with the `.length()` member function
Since `std::string` is basically a glorified `char *`, don't pass it by value, pass it by reference (it's expensive to copy a whole string)
You could also use `std::string_view` arguments in functions to prevent passing in the `std::string` directly.
Same thing with returning `std::string` from a function. You can, but try to alloc it and return a pointer to it instead.
### 5.8
`std::string_view` is basically a read-only variable representing a string value.
It's easier to move around and pass by value, so use that whenever you need a read-only string.
Since those are "views", I guess you could kinda see it like a string pointer. It "watches" a string, and if you assign it a new string, instead of modifying the watched string, it just switches the string it's currently watching.
`std::string_view` has full support for `constexpr`.
### 5.9
> In programming, when we call an object an owner, we generally mean that it is the sole owner (unless otherwise specified). Sole ownership (also called single ownership) ensures it is clear who has responsibility for that data.

A view is a read-only representation of an object. It's fine for multiple views of an object to exist. And it's way less expensive to copy. (probably a pointer to the memory being viewed under the hood?)
You can create functions that take a `string_view` as a parameter, for example, and pass it `string`s without any issue. The implicit conversion will create a view of that `string` variable.
> [!WARNING]
> A view is dependent on the object being viewed. If the object being viewed is modified or destroyed while the view is still being used, unexpected or undefined behavior will result.
> Do not initialize a `std::string_view` with a `std::string` literal, as this will leave the `std::string_view` dangling.

> [!ERROR] Modifying the underlying string
> If you modify the string a `string_view` watches, that also breaks the view (since the memory is reallocated somewhere else, the pointer becomes invalid).
> You'll need to reassign it to the `string_view`, or assign it a new string instead.

`std::string_view` can view sub-strings, including removing both a suffix and a prefix if wanted.
This allows you to manipulate sub-strings without making copies of the initial string.
**Not all string views are null-terminated because of this.**
This isn't that big of an issue because string views also have a `.length()` member function you can use instead of looping until the null character.

> [!EXAMPLE] When to use `std::string` or `std::string_view`
> Use a `std::string` variable when:
> - You need a string that you can modify.
> - You need to store user-inputted text.
> - You need to store the return value of a function that returns a `std::string`.
> 
> Use a `std::string_view` variable when:
> - You need read-only access to part or all of a string that already exists elsewhere and will not be modified or destroyed before use of the `std::string_view` is complete.
> - You need a symbolic constant for a C-style string.
> - You need to continue viewing the return value of a function that returns a C-style string or a non-dangling `std::string_view`.

## 6 - Operators
### 6.1 - Operator precedence
| Prec/Ass | Operator                                                                                                                                                                                               | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Pattern                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1 L->R   | ::  <br>::                                                                                                                                                                                             | Global scope (unary)  <br>Namespace scope (binary)                                                                                                                                                                                                                                                                                                                                                                                                                      | ::name  <br>class_name::member_name                                                                                                                                                                                                                                                                                                                                                                                                         |
| 2 L->R   | ()  <br>()  <br>type()  <br>type{}  <br>[]  <br>.  <br>->  <br>++  <br>––  <br>typeid  <br>const_cast  <br>dynamic_cast  <br>reinterpret_cast  <br>static_cast  <br>sizeof…  <br>noexcept  <br>alignof | Parentheses  <br>Function call  <br>Functional cast  <br>List init temporary object (C++11)  <br>Array subscript  <br>Member access from object  <br>Member access from object ptr  <br>Post-increment  <br>Post-decrement  <br>Run-time type information  <br>Cast away const  <br>Run-time type-checked cast  <br>Cast one type to another  <br>Compile-time type-checked cast  <br>Get parameter pack size  <br>Compile-time exception check  <br>Get type alignment | (expression)  <br>function_name(arguments)  <br>type(expression)  <br>type{expression}  <br>pointer[expression]  <br>object.member_name  <br>object_pointer->member_name  <br>lvalue++  <br>lvalue––  <br>typeid(type) or typeid(expression)  <br>const_cast(expression)  <br>dynamic_cast(expression)  <br>reinterpret_cast(expression)  <br>static_cast(expression)  <br>sizeof…(expression)  <br>noexcept(expression)  <br>alignof(type) |
| 3 R->L   | +  <br>-  <br>++  <br>––  <br>!  <br>not  <br>~  <br>(type)  <br>sizeof  <br>co_await  <br>&  <br>*  <br>new  <br>new[]  <br>delete  <br>delete[]                                                      | Unary plus  <br>Unary minus  <br>Pre-increment  <br>Pre-decrement  <br>Logical NOT  <br>Logical NOT  <br>Bitwise NOT  <br>C-style cast  <br>Size in bytes  <br>Await asynchronous call  <br>Address of  <br>Dereference  <br>Dynamic memory allocation  <br>Dynamic array allocation  <br>Dynamic memory deletion  <br>Dynamic array deletion                                                                                                                           | +expression  <br>-expression  <br>++lvalue  <br>––lvalue  <br>!expression  <br>not expression  <br>~expression  <br>(new_type)expression  <br>sizeof(type) or sizeof(expression)  <br>co_await expression (C++20)  <br>&lvalue  <br>*expression  <br>new type  <br>new type[expression]  <br>delete pointer  <br>delete[] pointer                                                                                                           |
| 4 L->R   | ->_  <br>._                                                                                                                                                                                            | Member pointer selector  <br>Member object selector                                                                                                                                                                                                                                                                                                                                                                                                                     | object_pointer->_pointer_to_member  <br>object._pointer_to_member                                                                                                                                                                                                                                                                                                                                                                           |
| 5 L->R   | *  <br>/  <br>%                                                                                                                                                                                        | Multiplication  <br>Division  <br>Remainder                                                                                                                                                                                                                                                                                                                                                                                                                             | expression * expression  <br>expression / expression  <br>expression % expression                                                                                                                                                                                                                                                                                                                                                           |
| 6 L->R   | +  <br>-                                                                                                                                                                                               | Addition  <br>Subtraction                                                                                                                                                                                                                                                                                                                                                                                                                                               | expression + expression  <br>expression - expression                                                                                                                                                                                                                                                                                                                                                                                        |
| 7 L->R   | <<  <br>>>                                                                                                                                                                                             | Bitwise shift left / Insertion  <br>Bitwise shift right / Extraction                                                                                                                                                                                                                                                                                                                                                                                                    | expression << expression  <br>expression >> expression                                                                                                                                                                                                                                                                                                                                                                                      |
| 8 L->R   | <=>                                                                                                                                                                                                    | Three-way comparison (C++20)                                                                                                                                                                                                                                                                                                                                                                                                                                            | expression <=> expression                                                                                                                                                                                                                                                                                                                                                                                                                   |
| 9 L->R   | <  <br><=  <br>>  <br>>=                                                                                                                                                                               | Comparison less than  <br>Comparison less than or equals  <br>Comparison greater than  <br>Comparison greater than or equals                                                                                                                                                                                                                                                                                                                                            | expression < expression  <br>expression <= expression  <br>expression > expression  <br>expression >= expression                                                                                                                                                                                                                                                                                                                            |
| 10 L->R  | ==  <br>!=                                                                                                                                                                                             | Equality  <br>Inequality                                                                                                                                                                                                                                                                                                                                                                                                                                                | expression == expression  <br>expression != expression                                                                                                                                                                                                                                                                                                                                                                                      |
| 11 L->R  | &                                                                                                                                                                                                      | Bitwise AND                                                                                                                                                                                                                                                                                                                                                                                                                                                             | expression & expression                                                                                                                                                                                                                                                                                                                                                                                                                     |
| 12 L->R  | ^                                                                                                                                                                                                      | Bitwise XOR                                                                                                                                                                                                                                                                                                                                                                                                                                                             | expression ^ expression                                                                                                                                                                                                                                                                                                                                                                                                                     |
| 13 L->R  | \|                                                                                                                                                                                                     | Bitwise OR                                                                                                                                                                                                                                                                                                                                                                                                                                                              | expression \| expression                                                                                                                                                                                                                                                                                                                                                                                                                    |
| 14 L->R  | &&  <br>and                                                                                                                                                                                            | Logical AND  <br>Logical AND                                                                                                                                                                                                                                                                                                                                                                                                                                            | expression && expression  <br>expression and expression                                                                                                                                                                                                                                                                                                                                                                                     |
| 15 L->R  | \|  <br>or                                                                                                                                                                                             | Logical OR  <br>Logical OR                                                                                                                                                                                                                                                                                                                                                                                                                                              | expression \| expression  <br>expression or expression                                                                                                                                                                                                                                                                                                                                                                                      |
| 16 R->L  | throw  <br>co_yield  <br>?:  <br>=  <br>*=  <br>/=  <br>%=  <br>+=  <br>-=  <br><<=  <br>>>=  <br>&=  <br>\|=  <br>^=                                                                                  | Throw expression  <br>Yield expression (C++20)  <br>Conditional  <br>Assignment  <br>Multiplication assignment  <br>Division assignment  <br>Remainder assignment  <br>Addition assignment  <br>Subtraction assignment  <br>Bitwise shift left assignment  <br>Bitwise shift right assignment  <br>Bitwise AND assignment  <br>Bitwise OR assignment  <br>Bitwise XOR assignment                                                                                        | throw expression  <br>co_yield expression  <br>expression ? expression : expression  <br>lvalue = expression  <br>lvalue *= expression  <br>lvalue /= expression  <br>lvalue %= expression  <br>lvalue += expression  <br>lvalue -= expression  <br>lvalue <<= expression  <br>lvalue >>= expression  <br>lvalue &= expression  <br>lvalue \|= expression  <br>lvalue ^= expression                                                         |
| 17 L->R  | ,                                                                                                                                                                                                      | Comma operator                                                                                                                                                                                                                                                                                                                                                                                                                                                          | expression, expression                                                                                                                                                                                                                                                                                                                                                                                                                      |
Use redundant parentheses to make it clear what you're doing.
It's better to be clearer with more of them than to be unclear and have to look up this table each time you have doubts about what you were doing.
**Multiple operators on a single line will be evaluated in a different order depending on the [[Compiler]] used.**
### 6.2
When using `operator/` to divide numbers, it will do floating point division only if at least one of the two numbers are floats.
That means that just dividing `5 / 2` will result in `2`, not `2.5`. You'll have to `static_cast` either of them to get a floating result.
### 6.4
When it's not important to the program features, favor `++i` instead of `i++`. It's supposed to be faster.
### 6.7
Don't use exact comparison operators `==` and `!=` when comparing calculated floating point values.
This is because of floating point errors.
To compare calculated floats more precisely, use an epsilon value to determine the margin you're willing to accept.
Try to get a relative epsilon (like a tiny percentage of error margin).

> [!INFO] Research to be done!
> There's a whole optional section about how you could about comparing calculated floats.
## Section O

> [!INFO] Research to be done!
> Everything bit manipulation and bitwise is there. Look into it when it's relevant.
## 7 - Namespaces
### 7.2
You can create namespaces using this syntax :
namespace NamespaceIdentifier
```cpp
namespace NamespaceIdentifier {
    // content of namespace here
}
```
Use `::` without a namespace before it to access the global namespace.
Useful to access the global namespace from inside another one.
Both forward declarations and definition of functions have to be inside of the namespace block.
That also means you can declare the same namescape across multiple header and source files, and everything inside those blocks will be under the same namescape.
### 7.3
An object having linkage means that if it is re-declared in a different scope it will refer to the same object.
### 7.4
Define global variables in a namespace instead of in the global namespace.
Also keep using prefixes for globals like `g_`.
Global variables are like static variables, initialized to 0 by default at the very start of the program.
In general, **just don't use globals**.
### 7.6
An identifier having **internal linkage** means it's only accessible from a single translation unit (or source file).
An identifier having **external linkage** means it is accessible from other files as well.
A good example of this is functions: adding a `static` in front of a declaration prevents it from being accessible in other files.
It's the same for global variables.
`const` and `constexpr` have internal linkage by default.
### 7.7
To make an external linkage identifier or function accessible to another file, you'll need to forward declare it (either in the file or in a header you'll include).
Import global variables from other files with the `extern` keyword with forward declarations.
Make global variables accessible from other files with the same keyword.
### 7.9
`inline` functions are useful for when a function body is so small that the overhead of calling it as a function becomes greater than the runtime of the function body itself.
That means that for tiny functions like one that would calculate a minimum between two values, you can use the `inline` keyword to replace every call of that function with its body directly in the code.
Try to not use `inline` functions with functions that have more than a few statements, this helps make the executable not *too* large.
**Compilers are pretty good at doing that optimization themselves, make it a habit to not use the keyword.**
If you need to use `inline`, you'll know it.
### 7.10
Before C++17, if you need global constants, put them in a namespace in a header file as `constexpr` variables.
Otherwise, use `inline` variables (not functions) inside a header. This allows multiple files to have references to the same (`const` or `constexpr`) variable.
### 7.13
If you reaaaaaally wanna use `using` statement (spoiler, you don't), please declare them in block scope to make their duration not global.
Please.
## 8 - Control flow
### 8.4
In C++17, you can do `constexpr` if statements. Use them if the condition contains only `constexpr` values.
### 8.5
Ideally don't indent `case` labels of `switch` statements.
```cpp
// Preferred version
void printDigitName(int x)
{
    switch (x)
    {
    case 1: // not indented from switch statement
        std::cout << "One";
        return;
    case 2:
        std::cout << "Two";
        return;
    case 3:
        std::cout << "Three";
        return;
    default:
        std::cout << "Unknown";
        return;
    }
}
```
### 8.6
Be careful, if you don't end case statements with a `break`, `return` or something else that stops the flow, **switch fallthrough** will happen.
That means that (in the example of 8.5), if there weren't any `return`s, in case 2, case 2 3 and default would execute back to back.
To document intentional fallthrough in C++17, use the `[[fallthrough]]` tag.
```cpp
#include <iostream>

int main()
{
    switch (2)
    {
    case 1:
        std::cout << 1 << '\n';
        break;
    case 2:
        std::cout << 2 << '\n'; // Execution begins here
        [[fallthrough]]; // intentional fallthrough -- note the semicolon to indicate the null statement
    case 3:
        std::cout << 3 << '\n'; // This is also executed
        break;
    }

    return 0;
}
```
Remember that `case` labels don't define new scope. They're more like jump points.
### 8.10
You can omit statements in `for` loops between parentheses. For example, an infinite `for` loop would look like `for (;;)`.
You can also have multiple init variables as well as multiple actions at the end of the loop (the third field in the for loop parentheses).
Keep the `i j k` counter variables inside `for` loop parenthesis, so their scope is more limited.
### 8.12
`std::exit()` is the function to terminate the program normally.
It can be called by the code explicitly, but returning from the `main()` function also calls it by default.
> `std::exit()` performs a number of cleanup functions. First, objects with static storage duration are destroyed. Then some other miscellaneous file cleanup is done if any files were used. Finally, control is returned back to the OS, with the argument passed to `std::exit()` used as the `status code`.
> The `std::exit()` function does not clean up local variables in the current function or up the call stack.

To make sure your program cleans up after itself when exiting, use the `std::atexit()` function.
### 8.13
An algorithm is called stateful when it retains some information between calls.
The opposite of that is a stateless algorithm.
**Look at this and both the following sections to learn about generating pseudo-random numbers in C++.**
## 9 - Error detection and handling
### 9.1
Use `assert` when doing unit tests for your code.
Test each function individually and then test them working together.
Start at the smallest unit possible (a class or a function) and then work your way up with tests.
### 9.2
When testing code, we need to aim for 100% coverage of the branches (as in, the tests need to cover all possible control flow possibilities in the code.)
That means testing every if branch, and much more.
The same counts for loops : let them run a few times, at least 3, to make sure everything works fine.
When taking input, go wild with the tests. Give floats to functions accepting ints, `nullptr` to those that accept pointers, etc.
### 9.4
> The basic idea is that when an error occurs, an exception is “thrown”. If the current function does not “catch” the error, the caller of the function has a chance to catch the error. If the caller does not catch the error, the caller’s caller has a chance to catch the error. The error progressively moves up the call stack until it is either caught and handled (at which point execution continues normally), or until main() fails to handle the error (at which point the program is terminated with an exception error).

Use `std::cerr` for logs.
### 9.5 - Input error handling
```cpp
std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
```
Use this to ignore everything currently present in the `std::cin` buffer up until the '\n' (useful for clearing the buffer in between `>>` extractions).
- The `std::cin.eof()` function returns `true` if the last input operation (in this case the extraction to `x`) reached the end of the input stream.
- The `std::cin.peek()` function allows us to peek at the next character in the input stream without extracting it.
To put `std::cin` back in normal execution mode (after a failed extraction), use the `.clear()` method.
Don't forget to clear the input buffer if you do that.
You can also check if `std::cin` is in failure mode by comparing it against false, like `if (!std::cin)`.
In C++, `EOF` is an error state, not a character.
### 9.6 - Asserts
**Preconditions** are conditions that stop code from being executed if some conditions aren't met.
They're typically put at the very start of functions to check for edge cases and other invalid input.
> Asserts are used to detect errors while developing and debugging.
> When an assertion evaluates to false, your program is immediately stopped. This gives you an opportunity to use debugging tools to examine the state of your program and determine why the assertion failed. Working backwards, you can then find and fix the issue quickly.
> Asserts are better than comments in the context of required value ranges and other cases, because they have document and enforce a condition. Comments can become stale when the code changes and the comment isn’t updated. An assert that has become out of date is a code correctness issue, so developers are less likely to let them languish.

`assert()` is actually a preprocessor macro.
```cpp
assert(found && "Car could not be found in database");
```
This little trick above allows you to make more descriptive error messages when `assert` fails.
The `NDEBUG` macro disables `assert`. Useful for production release code.
Finally, `static_assert` allows you to assert things at compile time. Failed asserts will cause compilation errors.
Careful, `NDEBUG` doesn't turn off `static_assert`.
Since `assert` terminates the program rather abruptly, be careful using it while doing delicate operations that could result in corruption if stopped in the middle of them.
## 10 - Type conversions
### 10.2 - Numeric and float promotion
The width of a data type is the number of bits it is composed of.
Numeric promotion is the action of promoting a smaller type (like `char` or `short`) to a larger type that will be easier to handle by the target architecture's CPU.
Most often, this is either `int` or `double`.
This means that you could write a function that takes an `int` and give it `short`, `char` or things like `uint16` and it would work fine.
Same thing with floats: a function that takes in `double` as an argument can accept a `float`.
### 10.3 - Numeric conversions
For pretty obvious reasons, be careful when numeric converting stuff.
If you're converting from signed to unsigned, for example, you might lose some information (the sign).
### 10.4 - Narrowing conversions
Narrowing conversions happen when converting a type to a smaller one, potentially losing some information (because the width can't hold everything).
When intentionally doing this, use a `static_cast` to make it clear that it was intentional.
### 10.5 - Arithmetic conversions
Be very careful mixing unsigned and signed values in arithmetic expressions.
As in, **don't.**
If you want to check what's the common type of two types when joined in an arithmetic expression (like addition, subtraction etc), use `std::common_type_t<type1, type2>`.
### 10.6 - Casting
There are 4 different named casts in C++, along the usual C-style casts with parentheses.

| Cast             | Description                                                                                           | Safe?                 |
| ---------------- | ----------------------------------------------------------------------------------------------------- | --------------------- |
| static_cast      | Performs compile-time type conversions between related types.                                         | Yes                   |
| dynamic_cast     | Performs runtime type conversions on pointers or references in an polymorphic (inheritance) hierarchy | Yes                   |
| const_cast       | Adds or removes const.                                                                                | Only for adding const |
| reinterpret_cast | Reinterprets the bit-level representation of one type as if it were another type                      | No                    |
| C-style casts    | Performs some combination of `static_cast`, `const_cast`, or `reinterpret_cast`.                      | No                    |
> Avoid `const_cast` and `reinterpret_cast` unless you have a very good reason to use them.

Generally also avoid C-style casts, as it isn't always clear what it does under the hood.
`static_cast` should usually be your go-to.
### 10.7 - Typedefs and type aliases
You can create a type alias by using the `using` keyword (heh) like this:
```cpp
using Distance = double; // define Distance as an alias for type double
```
When aliasing a type, use the usual C++ convention of using a name with a first capital letter and no suffix (like `_t`).
Since aliasing a type is basically the modern version of `typedef`, use this instead.
Aliases are very useful for making new names for longer types, or making an otherwise unclear type clearer (renaming `int` as `TestScore` for example).
### 10.8 - Type deduction
Use `auto` as a type to let the compiler do the work of figuring out what's the type of a variable.
Seems kinda lazy, but in some cases it might be useful.
Careful, it drops `const` and `constexpr` when assigning from a variable that has those.
### 10.9 - `auto` with functions
Read the title. You can also do `auto` with functions.
Just- don't do that. It's not really worth the trade-offs.
## 11 - Function overloading and templates
### 11.1 - Function overloading
You can create multiple functions with the same name if you change the parameters' type(s).
You might wonder how the compiler figures out which one we wanna use? Well, it's all about the arguments' types.
If you have two add functions that either takes `int` or `double` arguments, the compiler will check if the call you wrote has `double` or `int` and use the right function accordingly.
### 11.2 - Differences between overloaded functions
The differences the compiler checks for are the number of parameters and their types.
**The return type is not checked.**
### 11.4 - Deleting functions
If you don't want an overloaded function to be used anymore, or if you want to forbid a particular use of a function, you can stamp a `= delete` after it's prototype to make the compiler flag it if it finds a use with the specified function signature.
```cpp
void printInt(char) = delete; // calls to this function will halt compilation
void printInt(bool) = delete; // calls to this function will halt compilation
```
> `= delete` means “I forbid this”, not “this doesn’t exist”.
> Deleted function participate in all stages of function overload resolution (not just in the exact match stage). If a deleted function is selected, then a compilation error results.
### 11.5 - Default arguments
In C++, you can provide functions a default value for their arguments.
```cpp
void print(int x, int y=10) // 10 is the default argument
{
    std::cout << "x: " << x << '\n';
    std::cout << "y: " << y << '\n';
}
```
Be careful, **all arguments with default values should be to the right of the arguments list**.
In the above example, you can't have `int x=10, int y` for example.
> If the function has a forward declaration (especially one in a header file), put the default argument there. Otherwise, put the default argument in the function definition.
### 11.6 - Function templates
> Instead of manually creating a bunch of mostly-identical functions or classes (one for each set of different types), we instead create a single _template_. Just like a normal definition, a **template** definition describes what a function or class looks like. Unlike a normal definition (where all types must be specified), in a template we can use one or more placeholder types. A placeholder type represents some type that is not known at the time the template is defined, but that will be provided later (when the template is used).
> Once a template is defined, the compiler can use the template to generate as many overloaded functions (or classes) as needed, each using different actual types!
> Templates can work with types that didn’t even exist when the template was written. This helps make template code both flexible and future proof!

```cpp
template <typename T> // this is the template parameter declaration defining T as a type template parameter
T max(T x, T y) // this is the function template definition for max<T>
{
    return (x < y) ? y : x;
}
```
The `typename` keyword in the example above can technically be replaced with `class`, but `typename` is more recent and thus prefered.
#### More details?
> As an example, the standard library has an overload of `std::max()` that is declared like this:
```cpp
template< class T, class Compare >
const T& max( const T& a, const T& b, Compare comp ); // ignore the & for now, we'll cover these in a future lesson
```
By the way, you would call this a `max<T, Compare>` template.
> Because `a` and `b` are of type `T`, we know that we don’t care what type `a` and `b` are -- they can be any type. Because `comp` has type `Compare`, we know that `comp` must be a type that meets the requirements for a `Compare` (whatever that is).
> When a function template is instantiated, the compiler replaces the template parameters with the template arguments and then compiles the resulting instantiated function. Whether the function compiles depends on how the object(s) of each type are used within the function. Therefore, the requirements for a given template parameter are essentially implicitly defined.
#### Wrapped up
Use names that are pretty obvious are placeholders (single capital letters like `T`) for types that can be anything.
If you have placeholder types that need to be replaced with a specific kind of type, give it a more descriptive name like `Allocator` or `TAllocator`.
Make sure to document what the type is supposed to be so an outsider can use your template.
### 11.7 - Function template instantiation
To use a function template, you kind of call it with an added syntax thing:
```cpp
template<actual_type>(arg1, arg2); // replace actual_type with int, double or whatever you want to replace the type placeholder with
```
When the compiler finds such a use, it chooses which template to take from according to its signature, and creates a new function from it.
This is called **implicit instantiation**.
The result is technically called a specialization, or more commonly a function instance.
If you want, you can leave the <> part entirely and let the compiler have fun figuring out your arguments' type(s) (if you don't already have another function with the same name as your template).
For example:

```cpp
#include <iostream>

template <typename T>
T max(T x, T y)
{
    std::cout << "called max<int>(int, int)\n";
    return (x < y) ? y : x;
}

int max(int x, int y)
{
    std::cout << "called max(int, int)\n";
    return (x < y) ? y : x;
}

int main()
{
    std::cout << max<int>(1, 2) << '\n'; // calls max<int>(int, int)
    std::cout << max<>(1, 2) << '\n';    // deduces max<int>(int, int) (non-template functions not considered)
    std::cout << max(1, 2) << '\n';      // calls max(int, int)

    return 0;
}
```
Just like with function overloading, you can forbid some function templates by preparing a declaration for them and stamping `= delete` afterwards.
That way, if somehow you tell the compiler to create such a function from your template, you'll get an error and will be able to fix it.
Otherwise, you might end up with functions that won't work the way you expect them to work.
```cpp
// Use function template specialization to tell the compiler that addOne(const char*) should emit a compilation error
template <>
const char* addOne(const char* x) = delete;
```
___
Non template parameters in templates can have default values.
___
If you have a `static` in your template, each function created from it will have its own instance (and value).
___
Template types are sometimes called **generic types**.
As such, programming with them is called **generic programming**.
### 11.8 - Function templates with multiple types
If you need placeholder arguments to have different types in templates, use differently named placeholders (like `T`, `U` and `V`) to make their types independent.
This means that they could be different types, but also all the same.
___
In C++20 and above, you can use the `auto` keyword to create abbreviated function templates.
___
You can also overload function templates... if that's something you're into.
```cpp
#include <iostream>

// Add two values with matching types
template <typename T>
auto add(T x, T y)
{
    return x + y;
}

// Add two values with non-matching types
// As of C++20 we could also use auto add(auto x, auto y)
template <typename T, typename U>
auto add(T x, U y)
{
    return x + y;
}

// Add three values with any type
// As of C++20 we could also use auto add(auto x, auto y, auto z)
template <typename T, typename U, typename V>
auto add(T x, U y, V z)
{
    return x + y + z;
}

int main()
{
    std::cout << add(1.2, 3.4) << '\n'; // instantiates and calls add<double>()
    std::cout << add(5.6, 7) << '\n';   // instantiates and calls add<double, int>()
    std::cout << add(8, 9, 10) << '\n'; // instantiates and calls add<int, int, int>()

    return 0;
}
```
### 11.9 - Non-type template parameters
Not only can you define placeholder arguments in templates, you can also define internal values the function will use as placeholders.
```cpp
#include <iostream>

template <int N> // declare a non-type template parameter of type int named N
void print()
{
    std::cout << N << '\n'; // use value of N here
}

int main()
{
    print<5>(); // 5 is our non-type template argument

    return 0;
}
```
Use `N` instead of `T` for naming non-type template parameters.
> Non-type template parameters are used primarily when we need to pass constexpr values to functions (or class types) so they can be used in contexts that require a constant expression.
> The class type `std::bitset` uses a non-type template parameter to define the number of bits to store because the number of bits must be a constexpr value.

### 11.10
Put your templates in header files.
## F - Constexpr functions
### F.1
`constexpr` functions allow you to use them in `constexpr` variables. Usually, functions can't be used as initialization material for variables. Those can.
If the arguments you give to a `constexpr` function aren't `constexpr` themselves, the function will be evaluated at run time (and will lose its `constexpr` return value stamp.)
### F.2
> All constexpr functions should be evaluatable at compile-time, as they will be required to do so in contexts that require a constant expression.
> Always test your constexpr functions in a context that requires a constant expression, as the constexpr function may work when evaluated at runtime but fail when evaluated at compile-time.

`constexpr` functions are implicitly inline functions (since they're evaluated at compile time if you have `constexpr` parameters).
### F.3
In C++20, there's a keyword to force a function to be evaluated at compile-time (`constexpr` isn't always depending on the function's uses) : `consteval`.
### F.4
When should I make function `constexpr`? As soon as you find one that's **pure** (no side effects, always the same return value provided the input stays the same).
> Unless you have a specific reason not to, a function that can be evaluated as part of a constant expression should be made `constexpr` (even if it isn’t currently used that way).
> A function that cannot be evaluated as part of a required constant expression should not be marked as `constexpr`.

## 12 - References and pointers
### 12.1
Each type that is composed of other types is called a **compound type**. That counts functions, too, but also pointers, references, enums, C-style arrays and classes.
### 12.2 - lvalues and rvalues
> The **value category** of an expression (or sub-expression) indicates whether an expression resolves to a value, a function, or an object of some kind.

lvalue and rvalue both stand for left and right value.
An **lvalue** is an expression that evaluates to an identifiable object or function (or bit-field).
___
An **rvalue** is an expression that is not an lvalue.
Rvalue expressions evaluate to a value. Commonly seen rvalues include literals (except C-style string literals, which are lvalues) and the return value of functions and operators that return by value.
Rvalues aren’t identifiable (meaning they have to be used immediately), and only exist within the scope of the expression in which they are used.
> An lvalue will implicitly convert to an rvalue. This means an lvalue can be used anywhere an rvalue is expected.

### 12.3 - lvalue references
References are essentially an alias for an existing object. A bonified pointer of sorts.
There are lvalue and rvalue references. Prior to C++11, there were only lvalue references, so these were simply called references.
___
References are identified by their ampersand : `int&`, `double&` etc.
There's a distinction between lvalue references to const objects and non-const objects.
___
```cpp
#include <iostream>

int main()
{
    int x { 5 };    // x is a normal integer variable
    int& ref { x }; // ref is an lvalue reference variable that can now be used as an alias for variable x

    std::cout << x << '\n';  // print the value of x (5)
    std::cout << ref << '\n'; // print the value of x via ref (5)

    return 0;
}
```
Of course, the ampersand in this case does not mean "address of" like with pointers. It means "lvalue reference to".
You can also modify the underlying object by assigning a new value to the reference.
___
Careful, references in C++ can't be reseated. That means they can't be reassigned to another object.
Once a reference is locked in on an object, it stays on that one for ever until it gets deleted.
```cpp
#include <iostream>

int main()
{
    int x { 5 };
    int y { 6 };

    int& ref { x }; // ref is now an alias for x

    ref = y; // assigns 6 (the value of y) to x (the object being referenced by ref)
    // The above line does NOT change ref into a reference to variable y!

    std::cout << x << '\n'; // user is expecting this to print 5

    return 0;
}
```
Assigning an lvalue to a reference actually transforms that lvalue into a rvalue and assigns the result to the underlying object of the reference.
___
References in C++ aren't actually objects like pointers. They'll often be optimized away by the compiler.
As such, you can't use them where objects are required. That means you can't have a reference to a reference, for example.
```cpp
int var{};
int& ref1{ var };  // an lvalue reference bound to var
int& ref2{ ref1 }; // an lvalue reference bound to var
```
Same as the example a bit above, this `ref2` gets assigned the underlying value of `ref1`, which is `var`. As such, both `ref1` and `ref2` end up as references to the same object.
### 12.4 - lvalue references to const
You can have references to const objects by stamping `const` in front of the reference's type.
If you're certain you won't modify a non-const value through a reference, you can even make the reference `const` while the underlying object isn't.
This is good practice for when you don't need to modify the underlying object through the ref.
___
You can also bind a const reference to a temporary object like a literal.
```cpp
    const int& ref { 5 }; // okay: 5 is an rvalue
```
When you do that, this temporary object isn't discarded at the end of the expression anymore.
Its lifetime becomes bounded to the reference's.
___
Though you can bind a `const int&` to a `short` for example, don't do it.
This would create a temporary `int` converted from the `short`, and modifying the underlying `short` wouldn't modify the temporary object.
A whole mess. Don't do it.
### 12.5 - Pass by lvalue reference
Bigger objects like classes and other big compound types are expensive to copy.
In such cases, it becomes interesting to pass them by reference instead.
Most types provided by the standard library are classes, by the way. That includes `std::string`, too.
```cpp
#include <iostream>
#include <string>

void printValue(std::string& y) // type changed to std::string&
{
    std::cout << y << '\n';
} // y is destroyed here

int main()
{
    std::string x { "Hello, world!" };

    printValue(x); // x is now passed by reference into reference parameter y (inexpensive)

    return 0;
}
```
Notice how we only changed the type of argument in the function prototype? No need to use `&x` or anything like that when passing the argument itself.
Same thing as C, passing by reference allows us to modify the underlying object, something you can't do when passing by value.
### 12.6 - Pass by const lvalue reference
Unlike a reference to non-const, a reference to const can refer to **not only modifiable values, but also non-modifiables values and even rvalues**.
Basically, a reference to const will be able to bind to any type of argument.
```cpp
#include <iostream>

void printRef(const int& y) // y is a const reference
{
    std::cout << y << '\n';
}

int main()
{
    int x { 5 };
    printRef(x);   // ok: x is a modifiable lvalue, y binds to x

    const int z { 5 };
    printRef(z);   // ok: z is a non-modifiable lvalue, y binds to z

    printRef(5);   // ok: 5 is rvalue literal, y binds to temporary int object

    return 0;
}
```
This allows you to pass any value by reference, while making sure the underlying function will be unable to modify it.
Which is most cases.
___
As such, favor passing by const reference rather than non-const.
___
For strings, definitely use `std::string_view` instead of `const std::string&` unless you really need the `std::string` type for some reason.
Of course, if you're using C++14 or older, `std::string_view` isn't available. So a reference it is.
### 12.7 - Pointers
To differentiate from the more recent smart pointers, C style pointers are often called **"raw pointers"**.
When declaring a pointer type, place the asterisk next to the type instead of the name of the variable.
___
Always initialize your pointers, to not keep the garbage address found in them when created.
> There are some other differences between pointers and references worth mentioning:
> - References must be initialized, pointers are not required to be initialized (but should be).
> - References are not objects, pointers are.
> - References can not be reseated (changed to reference something else), pointers can change what they are pointing at.
> - References must always be bound to an object, pointers can point to `NULL`.
> **- References are “safe” (outside of dangling references), pointers are inherently dangerous.**

___
Pointer sizes are directly dependent upon the architecture the executable is compiled (32 bits for 32-bit machines, 64 bits for 64-bit, etc etc).
___
> **Dereferencing an invalid pointer will lead to undefined behavior. Any other use of an invalid pointer value is implementation-defined.**
### 12.8 - Null pointers
Assign your pointers to null if you're not planning to give them a value soon, while waiting for an actual value.
Use `nullptr` to initialize a pointer to null.
___
If a pointer is going to be dangling and its underlying variable gone to the ashes, better set it as `nullptr` so there's less risks.
___
**Use references instead of pointers where possible.**
### 12.9 - Const pointers
There are two ways to use the `const` keyword with pointers :
- A pointer to a `const` value: `const T* ptr = ...`
- A const pointer to a value: `T* const ptr = ...`
The first can also point to non-`const` values, just like references. It'll just prevent modifications of the value through that pointer.
The latter can't have its address changed after initialization.
### 12.10 - Passing by address
Unlike with references (where you can just set a function's argument as a reference in the prototype and passing an lvalue to it that will be converted to a reference automatically), with pointers, you not only have to set the type in the prototype, but you also have to explicitly provide a memory address as the argument.
___
> Prefer pointer-to-const function parameters over pointer-to-non-const function parameters, unless the function needs to modify the object passed in.  
> Do not make function parameters const pointers unless there is some specific reason to do so.
___

In functions that take in a pointer as argument, do an `assert` if this function is NEVER supposed to receive a `nullptr`.
Also do the traditional thing of checking `if (!ptr) {return ;}` before doing anything else in the function, so that in production optimized code, a check is still there (the `assert` will most likely be optimized out).
```cpp
void print(const int* ptr)
{
	assert(ptr); // fail the program in debug mode if a null pointer is passed (since this should never happen)

	// (optionally) handle this as an error case in production mode so we don't crash if it does happen
	if (!ptr)
		return;

	std::cout << *ptr << '\n';
}
```
>**Prefer pass by reference to pass by address unless you have a specific reason to use pass by address.**
### 12.11 - More passing by address
In C++, a common way to use pointers as function parameters is to provide an optional argument:
```cpp
#include <iostream>

void printIDNumber(const int *id=nullptr)
{
    if (id)
        std::cout << "Your ID number is " << *id << ".\n";
    else
        std::cout << "Your ID number is not known.\n";
}

int main()
{
    printIDNumber(); // we don't know the user's ID yet

    int userid { 34 };
    printIDNumber(&userid); // we know the user's ID now

    return 0;
}
```
For most purposes, though, **function overloading is better.**
___
You can actually have a **reference to a pointer** if a function needs to modify a pointer's address itself.
___
In C++, you don't use `0` or `NULL` as null pointer representations, because they're ambiguous in regards to function overloading especially.
Use `nullptr` instead. If you wanna know the specifics, read that optional subsection in 12.11 again.
### 12.12 - Returning by reference/address
Assigning or initializing a variable with a returned reference makes a copy of the underlying value.
```cpp
#include <iostream>
#include <string>

const int& getNextId()
{
    static int s_x{ 0 };
    ++s_x;
    return s_x;
}

int main()
{
    const int id1 { getNextId() }; // id1 is a normal variable now and receives a copy of the value returned by reference from getNextId()
    const int id2 { getNextId() }; // id2 is a normal variable now and receives a copy of the value returned by reference from getNextId()

    std::cout << id1 << id2 << '\n';

    return 0;
}
```
___
> **Prefer return by reference over return by address unless the ability to return “no object” (using `nullptr`) is important.**
### 12.13 - In and out parameters
A function parameter that is used for input to the called function is called an **in parameter**.
A function parameter that is used for output of a called function is called an **out parameter**.
The latter is for cases when you pass something to a function by reference or address, knowing it's going to be modified by it for later use by the caller.
In general, **avoid out parameters**, as they are harder to read and work with generally.
### 12.14 - Type deduction and references/pointers
> A **top-level const** is a const qualifier that applies to an object itself.
> In contrast, a **low-level const** is a const qualifier that applies to the object being referenced or pointed to.
___

Using `auto` on a reference will drop the reference. Const objects also lose their const modifier (but not `constexpr`).
```cpp
#include <string>

std::string& getRef(); // some function that returns a reference

int main()
{
    auto ref1 { getRef() };  // std::string (reference dropped)
    auto& ref2 { getRef() }; // std::string& (reference dropped, reference reapplied)

    return 0;
}
```
### 12.15 - std::optional
```cpp
#include <iostream>
#include <optional> // for std::optional (C++17)

// Our function now optionally returns an int value
std::optional<int> doIntDivision(int x, int y)
{
    if (y == 0)
        return {}; // or return std::nullopt
    return x / y;
}

int main()
{
    std::optional<int> result1 { doIntDivision(20, 5) };
    if (result1) // if the function returned a value
        std::cout << "Result 1: " << *result1 << '\n'; // get the value
    else
        std::cout << "Result 1: failed\n";

    std::optional<int> result2 { doIntDivision(5, 0) };

    if (result2)
        std::cout << "Result 2: " << *result2 << '\n';
    else
        std::cout << "Result 2: failed\n";

    return 0;
}
```
Note that while optionals have the same syntax for dereferencing as pointers, they're not pointers.
## 13 - Enums and structs
### 13.1 - Program defined types introduction
> **Name your program-defined types starting with a capital letter and do not use a suffix like `_t`.**
___

| Type            | Meaning                                                                                                                                                                    | Examples                             |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ |
| Fundamental     | A basic type built into the core C++ language                                                                                                                              | int, std::nullptr_t                  |
| Compound        | A type defined in terms of other types                                                                                                                                     | int&, double*, std::string, Fraction |
| User-defined    | A class type or enumerated type  <br>(Includes those defined in the standard library or implementation)  <br>(In casual use, typically used to mean program-defined types) | std::string, Fraction                |
| Program-defined | A class type or enumerated type  <br>(Excludes those defined in standard library or implementation)                                                                        | Fraction                             |
### 13.2 - Enums
The identifiers contained in enums are called **enumerators**, and are implicitly constexpr.
> Prefer putting your enumerations inside a named scope region (such as a namespace or class) so the enumerators don’t pollute the global namespace.
### 13.3 - Enumerators are integral
The first enumerator of your enums should be the default state, the best default value possible for your enum case.
___
You can specify the underlying type of your enums when really necessary.
```cpp
// Use an 8-bit integer as the enum underlying type
enum Color : std::int8_t
{
    black,
    red,
    blue,
};
```
### 12.5 - Operator overloading introduction
In C++, you can define your own way of using the usual operators like `+-*/ == >> << = etc`.
> Basic operator overloading is fairly straightforward:	
> - Define a function using the name of the operator as the function’s name.
> - Add a parameter of the appropriate type for each operand (in left-to-right order). One of these parameters must be a user-defined type (a class type or an enumerated type), otherwise the compiler will error.
> - Set the return type to whatever type makes sense.
> - Use a return statement to return the result of the operation.

```cpp
#include <iostream>
#include <string_view>

enum Color
{
	black,
	red,
	blue,
};

constexpr std::string_view getColorName(Color color)
{
    switch (color)
    {
    case black: return "black";
    case red:   return "red";
    case blue:  return "blue";
    default:    return "???";
    }
}

// Teach operator<< how to print a Color
// std::ostream is the type of std::cout, std::cerr, etc...
// The return type and parameter type are references (to prevent copies from being made)
std::ostream& operator<<(std::ostream& out, Color color)
{
    out << getColorName(color); // print our color's name to whatever output stream out
    return out;                 // operator<< conventionally returns its left operand

    // The above can be condensed to the following single line:
    // return out << getColorName(color)
}

int main()
{
	Color shirt{ blue };
	std::cout << "Your shirt is " << shirt << '\n'; // it works!

	return 0;
}
```
If you look at the code example above, we're essentially overloading the function `operator<<` which is the function used by the operator of the same name.
### 13.6 - Scoped enums
The main differences of scoped enums with unscoped enums (see previous section) is that their enumerators don't implicitly convert to integrals, and that their scope is limited to the class itself instead of the global scope the enum is defined in.
```cpp
#include <iostream>
int main()
{
    enum class Color // "enum class" defines this as a scoped enumeration rather than an unscoped enumeration
    {
        red, // red is considered part of Color's scope region
        blue,
    };

    enum class Fruit
    {
        banana, // banana is considered part of Fruit's scope region
        apple,
    };

    Color color { Color::red }; // note: red is not directly accessible, we have to use Color::red
    Fruit fruit { Fruit::banana }; // note: banana is not directly accessible, we have to use Fruit::banana

    if (color == fruit) // compile error: the compiler doesn't know how to compare different types Color and Fruit
        std::cout << "color and fruit are equal\n";
    else
        std::cout << "color and fruit are not equal\n";

    return 0;
}
```
___
Despite the use of the `class` keyword, scoped enums **aren't really classes**.
Scoped enums create their own scope, that's why you access enumerators with `enum::enumerators`.
**Favor scoped enums over the unscoped ones usually, unless you need to have one that implicitly converts to ints.**
### 13.7 - Structs, members and member selection
In C++, a **member** is a variable, function or type that **belongs to a struct or class**.
### 13.8 - Aggregate initialization
Like normal variables, data members have garbage values by default.
```cpp
struct Employee
{
    int id {};
    int age {};
    double wage {};
};

int main()
{
    Employee frank = { 1, 32, 60000.0 }; // copy-list initialization using braced list
    Employee joe { 2, 28, 45000.0 };     // list initialization using braced list (preferred)

    return 0;
}
```
If you initialize a struct with a list, and some or all members are missing from the list, they will be set to the default value set in the function, 0, or the default Constructor if it's a class.
You can overload the output operator `<<` to print any type, not just enums, the way you want.
```cpp
#include <iostream>

struct Employee
{
    int id {};
    int age {};
    double wage {};
};

std::ostream& operator<<(std::ostream& out, const Employee& e)
{
    out << e.id << ' ' << e.age << ' ' << e.wage;
    return out;
}

int main()
{
    Employee joe { 2, 28 }; // joe.wage will be value-initialized to 0.0
    std::cout << joe << '\n';

	joe = {2, 29, 10}; // You can also modify multiple members like this

    return 0;
}
```
### 13.9 - Default member initialization
Past C++11, you can give default values to members so that they are set when the struct or class is created.
```cpp
struct Something
{
    int x;       // no initialization value (bad)
    int y {};    // value-initialized by default
    int z { 2 }; // explicit default value
};

int main()
{
    Something s1;             // No initializer list: s1.x is uninitialized, s1.y and s1.z use defaults
    Something s2 { 5, 6, 7 }; // Explicit initializers: s2.x, s2.y, and s2.z use explicit values (no default values are used)
    Something s3 {};          // Missing initializers: s3.x is value initialized, s3.y and s3.z use defaults

    return 0;
}
```
If you can (when you don't use an obsolete version of C++), **always give default values to your members**.
### 13.10 - Passing structs
You can pass a temporary struct to a function, without explicitly assigning it to a variable beforehand.
```cpp
#include <iostream>

struct Employee
{
    int id {};
    int age {};
    double wage {};
};

void printEmployee(const Employee& employee) // note pass by reference here
{
    std::cout << "ID:   " << employee.id << '\n';
    std::cout << "Age:  " << employee.age << '\n';
    std::cout << "Wage: " << employee.wage << '\n';
}

int main()
{
    // Print Joe's information
    printEmployee(Employee { 14, 32, 24.15 }); // construct a temporary Employee to pass to function (type explicitly specified) (preferred)

    std::cout << '\n';

    // Print Frank's information
    printEmployee({ 15, 28, 18.27 }); // construct a temporary Employee to pass to function (type deduced from parameter)

    return 0;
}
```
Careful though, because the temporary object will be destroyed at the end of the line that created it.
Your underlying function shouldn't keep references of this struct's members, as such.
### 13.12 - Accessing members from referenced/struct pointers
Since references are essentially an alias for an object, you don't have to use `->` notation to access members of a struct reference.
### 13.13 - Class templates
You can also do templates of structs, not just functions.
```cpp
#include <iostream>

template <typename T>
struct Pair
{
    T first{};
    T second{};
};

int main()
{
    Pair<int> p1{ 5, 6 };        // instantiates Pair<int> and creates object p1
    std::cout << p1.first << ' ' << p1.second << '\n';

    Pair<double> p2{ 1.2, 3.4 }; // instantiates Pair<double> and creates object p2
    std::cout << p2.first << ' ' << p2.second << '\n';

    Pair<double> p3{ 7.8, 9.0 }; // creates object p3 using prior definition for Pair<double>
    std::cout << p3.first << ' ' << p3.second << '\n';

    return 0;
}
```
In case you really need a pair template, there's one in the standard library, so use it: `std::pair`.
### 13.14 - Class template argument deduction (CTDA)
In modern C++, the compiler can guess what the type of a template initializer's argument is, and create the right struct from that template automatically.
```cpp
#include <utility> // for std::pair

int main()
{
    std::pair<int, int> p1{ 1, 2 }; // explicitly specify class template std::pair<int, int> (C++11 onward)
    std::pair p2{ 1, 2 };           // CTAD used to deduce std::pair<int, int> from the initializers (C++17)

    return 0;
}
```
### 13.15 - Alias templates
You can create aliases for types and templates with `using`:
```cpp
#include <iostream>

template <typename T>
struct Pair
{
    T first{};
    T second{};
};

// Here's our alias template
// Alias templates must be defined in global scope
template <typename T>
using Coord = Pair<T>; // Coord is an alias for Pair<T>

// Our print function template needs to know that Coord's template parameter T is a type template parameter
template <typename T>
void print(const Coord<T>& c)
{
    std::cout << c.first << ' ' << c.second << '\n';
}

int main()
{
    Coord<int> p1 { 1, 2 }; // Pre C++-20: We must explicitly specify all type template argument
    Coord p2 { 1, 2 };      // In C++20, we can use alias template deduction to deduce the template arguments in cases where CTAD works

    std::cout << p1.first << ' ' << p1.second << '\n';
    print(p2);

    return 0;
}
```
## 14 - Classes
### 14.2 - Classes introduction
You define classes much like structs as a starting point, just replacing `struct` with `class` instead.
Most of the C++ standard library is classes.
### 14.3 - Member functions
Member functions are **a class's functions**. They exist to separate attributes and actions related to a class.
You declare member functions inside the class's body, but you can define them either inside or outside, in another file, for example.
Inside a member function, any member identifier that is not prefixed with the member selection operator (.) is associated with the implicit object that is passed by calling the member function.
```cpp
#include <iostream>
#include <string>

struct Person
{
    std::string name{};
    int age{};

    void kisses(const Person& person)
    {
        std::cout << name << " kisses " << person.name << '\n';
    }
};

int main()
{
    Person joe{ "Joe", 29 };
    Person kate{ "Kate", 27 };

    joe.kisses(kate);

    return 0;
}
```
Also. erm. Structs can have member functions too. Yeah.
AND ACTUALLY. Structs can just do everything classes can in C++. Okay. Welp.
Keep your structs simple with only data members though. Classes are here for a reason.
### 14.4 - Const classes and member functions
Class instances that were const initialized can't call non-const member functions.
**A const member function is a member function that guarantees won't change the object or call non-const member functions.**
### 14.5 - Public and private members
Members of a class are either `public`, `private` or `protected`.
**The public** is code not part of the class type, so any other code, basically.
Public members are accessible by the public. Private ones aren't.
**Members of a struct are public by default, and members of a class are private by default.**
Start your private members with a `m_` or just a `_` prefix (that one's my choice).

| Access level | Access specifier | Member access | Derived class access | Public access |
| ------------ | ---------------- | ------------- | -------------------- | ------------- |
| Public       | public:          | yes           | yes                  | yes           |
| Protected    | protected:       | yes           | yes                  | no            |
| Private      | private:         | yes           | no                   | no            |
Usually keep all **data** members of classes private, and write access functions for these.
Keep all structs members public to keep them as aggregates.
___
Classes and struct actually only differ in that their members are public by default for structs, and private by default for classes.
That's their only real difference, but we use the two very differently usually.
### 14.6 - Access functions (getters and setters)
Instead of keeping data members public, you have getter and setter functions to return and/or modify these data members using an interface **you** define.
This makes it cleaner and safer to make classes accessible to users.
Getters are sometimes called accessors, and setters mutators.
You usually make getters `const` so they can be called on const objects.
Getters should give read-only access to their members, so if you're returning a reference (because the private data member is beeg), make sure to make it a reference to const.
### 14.7 - Returning references on data members
Make sure that your getters have the exact type as a reference than the private member, no conversions!
That means no `string_view` for a string, the caller of the getter function can do that conversion themselves if they wish.
### 14.8 - Encapsulation with data hiding
Encapsulation (doing private and public members) allow you to make classes easier to understand from the outside: you expose only relevant fields and functions, the rest is hidden from the caller.
This makes classes you create easier to use in other contexts, as the caller doesn't have to understand everything that it does under the hood.
This is basically the raw concept for an **abstraction**: you hide what is happening under the hood to make the class easier to use.
___
Using setters rather than giving direct access to the data member itself also allows you to check if the data that is asked to be set is correct.
If you have a number that isn't supposed to go over a certain limit, your class' user could just set the data member directly to a wrong value if it was public.
With a getter, on the other hand, you can directly check if the value that is wanted is wrong or not, depending on the interface you want to define.
___
Encapsulation and making abstractions also allows you to make classes that have less breaking changes.
Since users don't have to worry about the details of the implementation (only the getters, setters and other public members), you're free to change the inner workings without much of an issue.
___
Generally, functions that don't have to be member functions **shouldn't be**. This makes them easier to debug and maintain, and makes the interface of your classes smaller.
___
Declare your public members first, then your protected ones, and finally your privates.
This is useful to people reading your code, they're more interested in the public interface than the private workings of it.
### 14.9 - Constructors
> A **constructor** is a special member function that is automatically called after a non-aggregate class type object is created.
> When a non-aggregate class type object is defined, the compiler looks to see if it can find an accessible constructor that is a match for the initialization values provided by the caller (if any).
> If an accessible matching constructor is found, memory for the object is allocated, and then the constructor function is called.
> If no accessible matching constructor can be found, a compilation error will be generated.

___
Constructors themselves don't create the objects, they are merely called on an object that was just instantiated.
### 14.10 - Constructor member initialiser lists
There's a syntax for initializing members with a Constructor:
```cpp
class Foo
{
private:
    int m_x {};
    int m_y {};

public:
    Foo(int x, int y)
        : m_x { x }, m_y { y } // here's our member initialization list
    {
        std::cout << "Foo(" << x << ", " << y << ") constructed\n";
    }

    void print() const
    {
        std::cout << "Foo(" << m_x << ", " << m_y << ")\n";
    }
};
```
___
Members in an initializer list are initialized in the order they are defined in the class.
___
Most often, constructors have empty function bodies, since we only use them to init variables.
Though, if your class involves some stuff to be done at init time, then you might add instructions and function calls inside your constructor's body.
___
> **Throwing an exception is usually the best thing to do when a constructor fails (and cannot recover).**
### 14.11 - Default constructors and arguments
**A default constructor is a constructor that accepts no arguments.**
> **If all of the parameters in a constructor have default arguments, the constructor is a default constructor (because it can be called with no arguments).**

___
When creating a default constructor, you can use `ClassName() = default;` to specify it be a default initializer.
Prefer using that, as it makes it explicitly clear what you're wanting to do.
It also has other benefits, such as initializing members to 0 instead of default (which is garbage values if you haven't set a default value for members).
___
Classes that logically shouldn't have default values (like a class representing a person) shouldn't have a default constructor.
Just have constructors that actually set the values to something meaningful.
### 14.12 - Delegating constructors
As a best practice, don't call a constructor directly from other functions (or worse, other constructors!)
Doing so would create a temporary object, so if you're looking to create a new class instance, just use the standard syntax instead:
`ClassName element;` or, for modern C++: `ClassName element{};`
___
Constructors are allowed to use other constructors (called delegating or chaining constructors).
```cpp
class Employee
{
private:
    std::string m_name { "???" };
    int m_id { 0 };

public:
    Employee(std::string_view name)
        : Employee{ name, 0 } // delegate initialization to Employee(std::string_view, int) constructor
    {
    }

    Employee(std::string_view name, int id)
        : m_name{ name }, m_id { id } // actually initializes the members
    {
        std::cout << "Employee " << m_name << " created\n";
    }

};
```

> [!ERROR]
> **A constructor that delegates to another constructor is not allowed to do any member initialization itself. So your constructors can delegate or initialize, but not both.**

> It is common to have the constructor with fewer parameters delegate to one with more parameters.

___
If you can, use default values in Constructors or member fields directly, instead of chaining constructors. Makes it easier to read.
```cpp
class Employee
{
private:
    static constexpr int default_id { 0 }; // define a named constant with our desired initialization value

    std::string m_name {};
    int m_id { default_id }; // we can use it here

public:

    Employee(std::string_view name, int id = default_id) // and we can use it here
        : m_name { name }, m_id { id }
    {
        std::cout << "Employee " << m_name << " created\n";
    }
};
```
### 14.14 - Copy constructor
When using a class instance to create another instance of that same class, it uses the **copy constructor**.
This creates an exact copy of that instance.
___
If you don't copy an explicit copy constructor, C++ uses the implicit, default one.
This default copy constructor will initialize each member with the corresponding member value on the first instance.
___
You can create your own copy constructor by creating a constructor that takes in **a reference to an instance of that same class**:
```cpp
class Fraction
{
private:
    int m_numerator{ 0 };
    int m_denominator{ 1 };

public:
    // Default constructor
    Fraction(int numerator=0, int denominator=1)
        : m_numerator{numerator}, m_denominator{denominator}
    {
    }

    // Copy constructor
    Fraction(const Fraction& fraction)
        // Initialize our members using the corresponding member of the parameter
        : m_numerator{ fraction.m_numerator }
        , m_denominator{ fraction.m_denominator }
    {
        std::cout << "Copy constructor called\n"; // just to prove it works
    }

    void print() const
    {
        std::cout << "Fraction(" << m_numerator << ", " << m_denominator << ")\n";
    }
};
```
___
In order to let the compiler do optimization thingies, **a copy constructor should do nothing other than copying an object**.
If your copy constructor has other side effects, these might be removed by the compiler when optimization occurs.
Also, when you pass a class instance by value to a function, it's actually the copy constructor that's called.
Same thing for returning a class instance by value.
___
**Unless you have a specific reason to, don't define your own copy constructor.** The default is fine in most cases.
___
In the potential case when you don't want to allow copies of a class instance, make the copy constructor `= delete`.
```cpp
Fraction(const Fraction& fraction) = delete;
```
___
> The **rule of three** is a well known C++ principle that states that if a class requires a user-defined copy constructor, destructor, or copy assignment operator, then it probably requires all three. In C++11, this was expanded to the **rule of five**, which adds the move constructor and move assignment operator to the list.
### 14.15 - Copy elisions
When the compiler optimizes out unnecessary copies, it is called **copy elision**. A copy that has been optimized is called **elided**.
### 14.15 - Explicit conversions in constructors
For user-defined types, you can define the way conversions should happen between types yourself.
You do this by creating a member function that can produce such a conversion:
```cpp
class Foo
{
private:
    int m_x{};
public:
    Foo(int x)
        : m_x{ x }
    {
    }

    int getX() const { return m_x; }
};
```
___
To prevent a constructor to be used a converting constructor (a constructor that takes in other types than required and converts them), you can mark a constructor as `explicit`.
```cpp
#include <iostream>

class Dollars
{
private:
    int m_dollars{};

public:
    explicit Dollars(int d) // now explicit
        : m_dollars{ d }
    {
    }

    int getDollars() const { return m_dollars; }
};

void print(Dollars d)
{
    std::cout << "$" << d.getDollars();
}

int main()
{
    print(5); // compilation error because Dollars(int) is explicit

    return 0;
}
```
> **Make any constructor that accepts a single argument `explicit` by default.** If an implicit conversion between types is both semantically equivalent and performant, you can consider making the constructor non-explicit.
> Do not make copy or move constructors explicit, as these do not perform conversions.

### 14.17 - Constexpr aggregates and classes
You can easily make aggregates (structs and classes with no constructors, only public members and no virtual functions) and their member functions `constexpr`.
When your classes aren't aggregates, though, things get sticky.
___
You can make something `constexpr` if its type is a **literal type**, as in a type that can be used in a constant expression.
This means that an object can't be `constexpr` unless its type qualifies as a literal type.
To make a non-aggregate class `constexpr` (and thus a literal type), we need to give it a **`constexpr` constructor**.
It's also generally more useful to make your member functions for that class type `constexpr` as well, otherwise you won't be able to use them in a constant expression.

## 15 - More on Classes
### 15.1 - The `this` pointer
The `this` pointer is a const pointer that holds the address of the current object being worked on in **non-static member functions**.
___
It's possible to do member function chaining because all non-static member functions return `*this`, allowing the next member function in line to pick up on it and continue.
___
You can reset a class to its default state by **NOT calling the default constructor** (it's not good practice to do so), but setting `*this = {}` to set default initialize the current object.
### 15.2 - Classes and header files
Try to keep the member function's bodies (definitions) in a separate `.cpp` file from the header.
In other words, the declarations with the rough blueprint of the class in the header, and the nitty gritty of the details of the constructors, member functions etc in a separate file.
___
> Put any default arguments for member functions inside the class definition.

### 15.3 - Nested (member) types
You can create member types as part of class. For reasons. It can be useful to limit the scope of a type to only a class to not pollute the global namespace.
Define them at the top of your class types.
### 15.4 - Destructors
The destructor of a class is a member function that is automatically called when a class instance is destroyed.
For stack allocation, that means when the instance goes out of scope.
For heap allocation, it's when `delete()` is called on it.
___
As with constructors, a default destructor with an empty body is added by the compiler if you don't provide one.
### 15.5 - Class templates with member functions
When using a class template, let's call it `Pair<T>`, inside the scope of that class, you can actually use `Pair` as a shorthand name for the `Pair<T>` type.
___
For member function templates, they should be defined below the class definition in the same header file.
### 15.6 - Static member variables
Static member variables are variables that are shared between all instances of a class.
You usually access them not via an instance, but via the name of the class itself: `Class::variable`.
You have to init them outside of the class, in an actual source code file, like globals.
### 15.7 - Static member functions
The same principle applies to member functions.
You can make the static to make them global to all class instances.
### 15.8 - Friend non member functions
By making an external function `friend` inside of a class, you give that function access to private and protected members of that class.
### 15.9 - Friend member functions and classes
The same thing is possible for member functions of a class, and class themselves, allowing them to access all members of another class.
## 16 - Dynamic arrays - `std::vector` \[WIP]
### 16.1 - Containers and arrays
Some types that behave like containers aren't considered ones by the C++ standard, like C-style arrays, `std::string` and `std::vector<bool>`.
### 16.2 - `std::vector` and list constructors

## 17 - `std::array` and C-style arrays \[WIP]
## 18 - Iterators and Algorithms \[WIP]
## 19 - Dynamic Allocation
### 19.1 - new and delete
You can allocate new **single** variables with the `new` keyword followed by a type.
You can also directly allocate that new heap-stored variable to a pointer:
```cpp
int* ptr{ new int };
```
Don't forget to free `new` allocated variables with the `delete` keyword! Keep in mind this only deletes a single variable created with `new`.
**Just `malloc`, `new` can fail. Don't forget to check if the pointer was set correctly if you assign the result to one (which you should).**
### 19.2 - Dynamically allocating arrays
You can also allocate C-style arrays with the `new` keyword:
```cpp
#include <cstddef>
#include <iostream>

int main()
{
    std::cout << "Enter a positive integer: ";
    std::size_t length{};
    std::cin >> length;

    int* array{ new int[length]{} }; // use array new.  Note that length does not need to be constant!

    std::cout << "I just allocated an array of integers of length " << length << '\n';

    array[0] = 5; // set element 0 to value 5

    delete[] array; // use array delete to deallocate array

    // we don't need to set array to nullptr/0 here because it's going out of scope immediately after this anyway

    return 0;
}
```
**Make sure to use `delete[]` instead of `delete`, as these two operators are different and target scalar and array values respectively.**
### 19.3 - Destructors
Destructors are member functions that are executed when an object of that type is dropped.
Destructor names start with a `~` tilde.
If your object is completely stack-allocated, your destructor can have an empty body.
If your object has some heap allocation or other dynamic ressource in its members, though, your destructor will be in charge of freeing that memory.
#### RAII
Ressource Acquisition Is Initialization is a technique where ressource use is directly tied to the lifetime of objects with an automatic duration (non-dynamically allocated objects).
In C++, RAII is implemented with constructors and destructors of classes.
A resource is typically acquired in the Constructor of a class, and typically release in the Destructor of that same class.
This makes the management of ressources for each instance clear and precise, and helps prevents memory leaks.
___
Be wary that `std::exit()` doesn't call any destructor on being called. Leaks are to be expected.
## 20 - Functions \[WIP]
## 21 - Operator Overloading \[WIP]
### 21.1 - Introduction
Since operators in C++ are just functions, you can overload them just like any other function out there.
There are a few exceptions though: conditional (?:), sizeof, scope (::), member selector (.), pointer member selector (.\*), typeid, and the casting operators.
#### Best practices
Overloaded operators should operate on at least one user-defined type.
When overloading operators, it’s best to keep the function of the operators as close to the original intent of the operators as possible.
If the meaning of an overloaded operator is not clear and intuitive, use a named function instead.
Operators that do not modify their operands (e.g. arithmetic operators) should generally return results by value.
Operators that modify their leftmost operand (e.g. pre-increment, any of the assignment operators) should generally return the leftmost operand by reference.
### 21.2 - Using friend functions for arithmetic operators
Since friend functions can access private members of classes, it's one of the easier ways of overloading arithmetic operators like + and -.
You define the function as a friend of a class, and do the operations you need within.
___
Careful, when overloading binary operators like + and -, you need to take into account the cases in which you add or subtract an instance of your class with just an int, for example.
In these case, you could have `Class(5) + 3` and `3 + Class(5)`, resulting in operator functions looking like this:
- `operator+(Class, int)`
- `operator+(int, Class)`
As such, you'll need to overload both these operator functions and the one with both arguments being `Class`.
```cpp
#include <iostream>

class Cents
{
private:
	int m_cents {};

public:
	explicit Cents(int cents) : m_cents{ cents } { }

	// add Cents + int using a friend function
	friend Cents operator+(const Cents& c1, int value);

	// add int + Cents using a friend function
	friend Cents operator+(int value, const Cents& c1);


	int getCents() const { return m_cents; }
};

// note: this function is not a member function!
Cents operator+(const Cents& c1, int value)
{
	// use the Cents constructor and operator+(int, int)
	// we can access m_cents directly because this is a friend function
	return Cents { c1.m_cents + value };
}

// note: this function is not a member function!
Cents operator+(int value, const Cents& c1)
{
	// use the Cents constructor and operator+(int, int)
	// we can access m_cents directly because this is a friend function
	return Cents { c1.m_cents + value };
}

int main()
{
	Cents c1{ Cents{ 4 } + 6 };
	Cents c2{ 6 + Cents{ 4 } };

	std::cout << "I have " << c1.getCents() << " cents.\n";
	std::cout << "I have " << c2.getCents() << " cents.\n";

	return 0;
}
```
___
Don't forget you can use some already overloaded operator functions to simplify the next ones, especially in the case of arithmetic operators.
```cpp
Class operator+(const Class& c1, int value)
{
	return Class { c1.value + value };
}

Class operator+(int value, const Class& c1)
{
	return c1 + value;
}
```
### 21.3 - Using normal functions
If you don't need access to private members of your classes to implement an operator, you can overload it using a normal function instead of a `friend` one.
Those don't need to be declared inside of the class definition, as they aren't member functions at all:
```cpp
class Cents
{
private:
  int m_cents{};

public:
  Cents(int cents)
    : m_cents{ cents }
  {}

  int getCents() const { return m_cents; }
};

// note: this function is not a member function nor a friend function!
Cents operator+(const Cents& c1, const Cents& c2)
{
  // use the Cents constructor and operator+(int, int)
  // we don't need direct access to private members here
  return Cents{ c1.getCents() + c2.getCents() };
}
```
It's preferable to use normal functions instead of friend functions when possible.
If your class implements getters (and setters for operators that modify values), you don't have to use a friend function at all.
### 21.4 - Overloading the I/O operators
#### `<<`
In order to easily print a custom class of yours, you can overload the output `<<` operator.
It's pretty similar to the arithmetic operators, in that they are also binary operators.
The main difference is the types of the parameters and return values:
- Its first argument is a reference to an `std::ostream` instance (usually just `std::cout`)
- Its second argument is the class instance to print
- It returns the first argument, that is the `std::ostream` instance.
___
```cpp
std::ostream& operator<< (std::ostream& out, const Point& point)
{
    // Since operator<< is a friend of the Point class, we can access Point's members directly.
    out << "Point(" << point.m_x << ", " << point.m_y << ", " << point.m_z << ')';

    return out;
}
```
#### `>>`
You can overload the insertion operator much in the same way of the output operator.
Just replace `std::ostream` with `std::istream`, and make sure your class' reference isn't `const` so it can be modified.
```cpp
// note that point must be non-const so we can modify the object
std::istream& operator>> (std::istream& in, Point& point)
{
    // This version subject to partial extraction issues (see below)
    in >> point.m_x >> point.m_y >> point.m_z;

    return in;
}
```
___
In order to protect against partial extraction, you need to make sure your input operation only actually modifies the value if all steps have succeeded.
You can achieve this by extracting every value, checking if everything worked and only then assign these values to the class instance.
```cpp
std::istream& operator>> (std::istream& in, Point& point)
{
    double x{};
    double y{};
    double z{};

    if (in >> x >> y >> z)      // if all extractions succeeded
        point = Point{x, y, z}; // overwrite our existing point

    return in;
}
```
You can also go the route of copying every value gradually, and if one extraction fails, restore everything back to normal.
This would imply keeping a copy of the initial state somewhere, or rolling back all operations performed.
You can also just restore the object to its default state if the extraction fails.
This would put you in line with how the extraction operator works for fundamental types (putting `int` at 0 if it fails, for example).
___
If the values entered in the extraction operator don't match what's supposed to go inside the class, you can set cin to failure mode yourself (just like for fundamental types):
```cpp
std::istream& operator>> (std::istream& in, Point& point)
{
    double x{};
    double y{};
    double z{};

    in >> x >> y >> z;
    if (x < 0.0 || y < 0.0 || z < 0.0)       // if any extractable input is negative
        in.setstate(std::ios_base::failbit); // set failure mode manually
    point = in ? Point{x, y, z} : Point{};

    return in;
}
```
### 21.5 - Using member functions
Overloading using a member function is basically like using `friend`, aside from these details:
- The overloaded operator must be added as a member function **of the left operand.**
- The left operand becomes the **implicit** `*this` object.
- All other operands become function parameters.
```cpp
class Cents
{
private:
    int m_cents {};

public:
    Cents(int cents)
        : m_cents { cents } { }

    // Overload Cents + int
    Cents operator+(int value) const;

    int getCents() const { return m_cents; }
};

// note: this function is a member function!
// the cents parameter in the friend version is now the implicit *this parameter
Cents Cents::operator+ (int value) const
{
    return Cents { m_cents + value };
}
```
___
You can't overload all operators as a member function, because these need to be a member of the left operand.
This isn't possible for the output `<<` operator, for example, or the addition operator that has the class instance as the right operand, and a fundamental type or fixed class as the left one (`int + Class`).
In these cases, you'll prefer using `friend` (ew) or non-member functions instead.
#### When to use normal, friend or member function overloadings
- When overloading a binary operator that don't modify the left operand, use a normal function, since it works on all parameter types, and it's more symmetrical since all operands become explicit parameters instead of an implicit `*this` being slapped in the middle of your pretty class.
- When overloading a binary operator that does modify the left operand, prefer a member function, since in these cases you'll want to apply the changes to `*this` directly.
- Unary operators are usually overloaded with member functions as well, with no parameters (since the only operand is implicit with `*this`.
### 21.6 - Overloading unary operators
You can also overload the unary operators like - and + (modifying the sign of values) and the not ! operator to invert a value.
Since these are unaries, if you do it using a member function, it will take no arguments since only `*this` is required.
That's how you differentiate between the unary - and the binary -.
### 21.7 - Overloading the comparison operators
Comparison operators are pretty straightforward, just like the other operators we've seen so far.
Just two arguments, no modifications to the left operand so they can be implemented using normal functions.
Only overload the < and > operators for a class if it makes sense semantically.
For example, how would you represent a Car being "higher" than another?
It might be useful in the case where you want to be able to easily sort an array of Cars though.
In this case, you would overload the < operator (or >) according to the data member you want to sort from.
Oh and don't forget about <= and >=.
___
Some comparison operators can be implemented using others:
- operator!= can be implemented as !(operator\==)
- operator> can be implemented as operator< with the order of the parameters flipped
- operator>= can be implemented as !(operator<)
- operator<= can be implemented as !(operator>)
Thankfully, that means you actually only have to fully implement == and <! The rest can build upon those.
### 21.8 - Overloading the increment and decrement operators
When overloading the increment and decrement operators, keep in mind two things:
- There are two version of each (prefix and postfix)
- They are unary operators, and since you'll need to modify values, you'll have to implement them as member functions, so they will take no parameters (`*this`)
Also don't forget to return `*this`, because that's what these operators do (so you can chain operators together).
___
Prefix increment and decrement are just the same as the other unaries in terms of overloading.
The postfix ones are different though.
Since their function signatures are the same as the prefix in theory, we have to give them a differentiating factor.
In this case, the compiler knows an increment or decrement operator is postfix if the function takes a dummy `int` parameter.
Here's an example with all operators overloaded:
```cpp
class Digit
{
private:
    int m_digit{};
public:
    Digit(int digit=0)
        : m_digit{digit}
    {
    }

    Digit& operator++(); // prefix has no parameter
    Digit& operator--(); // prefix has no parameter

    Digit operator++(int); // postfix has an int parameter
    Digit operator--(int); // postfix has an int parameter

    friend std::ostream& operator<< (std::ostream& out, const Digit& d);
};

// No parameter means this is prefix operator++
Digit& Digit::operator++()
{
    // If our number is already at 9, wrap around to 0
    if (m_digit == 9)
        m_digit = 0;
    // otherwise just increment to next number
    else
        ++m_digit;

    return *this;
}

// No parameter means this is prefix operator--
Digit& Digit::operator--()
{
    // If our number is already at 0, wrap around to 9
    if (m_digit == 0)
        m_digit = 9;
    // otherwise just decrement to next number
    else
        --m_digit;

    return *this;
}

// int parameter means this is postfix operator++
Digit Digit::operator++(int)
{
    // Create a temporary variable with our current digit
    Digit temp{*this};

    // Use prefix operator to increment this digit
    ++(*this); // apply operator

    // return temporary result
    return temp; // return saved state
}

// int parameter means this is postfix operator--
Digit Digit::operator--(int)
{
    // Create a temporary variable with our current digit
    Digit temp{*this};

    // Use prefix operator to decrement this digit
    --(*this); // apply operator

    // return temporary result
    return temp; // return saved state
}
```
Note that in the case of the postfixes, you don't return `*this` because you want to return the initial value **before** the operation occurred.
Also note that it's easier to prepare the prefix operators, and then reuse them on the postfix ones so it reduces duplicate code.
### 21.9 - Overloading the subscript operator
The subscript operator is the one you use to access array elements `array[10]`.
As such, it can be useful to overload it when your class implements a list or vector or just a great number of elements inside.
The subscript operator **must be overloaded as a member function**, because it needs access to private members like the array you want to access.
If the array wasn't private, you could just access it from anywhere and overloading the subscript operator would make little to no sense at all.
```cpp
class IntList
{
private:
    int m_list[10]{};

public:
    int& operator[] (int index);
};

int& IntList::operator[] (int index)
{
	return m_list[index];
}
```
Don't forget to return a reference to the index instead of copying the value; otherwise the user won't be able to modify the value.
Also don't forget to handle cases with wrong indexes (like -1) inside your overloaded function.
### 21.10 - Overloading the parenthesis operator
The parenthesis operator, usually used to call a function, can be used for a variety of things in OOP C++.
It is one of the rare operators that allows you to modify the number of arguments it takes.
This makes it particularly useful for classes that contain multi dimensional arrays that you want quick access to, like matrices:
```cpp
#include <cassert> // for assert()

class Matrix
{
private:
    double m_data[4][4]{};

public:
    double& operator()(int row, int col);
    double operator()(int row, int col) const; // for const objects
};

double& Matrix::operator()(int row, int col)
{
    assert(row >= 0 && row < 4);
    assert(col >= 0 && col < 4);

    return m_data[row][col];
}

double Matrix::operator()(int row, int col) const
{
    assert(row >= 0 && row < 4);
    assert(col >= 0 && col < 4);

    return m_data[row][col];
}
```
```cpp
#include <iostream>

int main()
{
    Matrix matrix;
    matrix(1, 2) = 4.5;
    std::cout << matrix(1, 2) << '\n';

    return 0;
}
```
You could also overload it so it takes no argument at all, and make it do some action.
___
The bad thing about overusing this very powerful operator is that the `()` syntax really isn't intuitive.
What is it going to do? Execute some code, sure, but to what end? You would have to know the class really well to understand it.
That's a bit too obfuscated, so only use it when it's really useful, like with multidimensional arrays like seen before.
___
You can use the `()` operator to implement functors, which are classes that act like functions.
### 21.11 - Overloading typecasts
In case when you want your classes to be easily convertible to other types like fundamental ones or even other classes entirely, it's useful to overload the casting operators like `static_cast` and others.
Usually, stamping a `()` in front of a type means you're converting to that type the value between parenthesis.
That means you can overload a cast like this: `operator int() const { // do stuff // }`
Note the space between `operator` and the actual type. Also, overloaded typecasts need to be `const` so they can be used on const objects.
Overloaded typecasts don't take any parameters (`*this` still exists though).
```cpp
class Cents
{
private:
    int m_cents{};
public:
    Cents(int cents=0)
        : m_cents{ cents }
    {
    }

    // Overloaded int cast
    operator int() const { return m_cents; }

    int getCents() const { return m_cents; }
    void setCents(int cents) { m_cents = cents; }
};

class Dollars
{
private:
    int m_dollars{};
public:
    Dollars(int dollars=0)
        : m_dollars{ dollars }
    {
    }

    // Allow us to convert Dollars into Cents
    operator Cents() const { return Cents { m_dollars * 100 }; }
};
```
___
You can make your typecasts `explicit` to prevent implicit conversions using them.
Usually, you should do that to make it always explicit when a conversion has to happen.
You should prefer converting constructors usually though.
### 21.12 - Overloading the assignment operator
In contrast to the copy constructor, the copy assignment does not initialize a new object; it merely copies values into an already existing one.
In practice, both do pretty much the same thing.
The copy assignment must be overloaded as a member function to be able to access members.
```cpp
	Fraction& operator= (const Fraction& fraction);
```
In the body of the overloaded operator, don't forget to return `*this` so the operator can be chained.
Also, make sure to **prevent self-assignment**, just like in the copy constructor.
### 21.13 - Shallow vs Deep copying
For simple classes that only have stack allocated members, shallow copying with a default copy constructor and assignment operator is fine.
For more complex classes that have heap allocated members though, you might want to **deep copy** it instead.
This implies copying all memory associated with a given class instance; because if we only did shadow copy, we might copy pointers to memory and have two instances pointing to the same memory, which could lead to loooots of problems.
Deep copying implies allocating memory for all heap-allocated member in the target, and then copying the actual values (not the pointers).
### 21.14 - Overloading operators and function templates
Be careful using templates around your classes, since for example comparing multiple class types, you'd have to create overloaded operators for each of these cases, which could quickly ramp up the number of overloadings.
## 22 - Move Semantics and Smart Pointers \[WIP]
### 22.1 - Introduction

## 23 - Object Relationships \[WIP]
### 23.1 - Object relationships

## 24 - Inheritance
### 24.1 - Introduction
Inheritance is the concept of an object taking properties from another, in effect being "a kind of" this object.
One of the best examples would be a class Fruit that has child classes Apple and Banana.
In practice, when inheriting from a class, you first build that class object, then build your new class **around** it.
This is called a *subobject*, because in memory the base class is embedded within the derived object's memory layout.
This means that since you're effectively building a different class, **you can't access private member of the base class**.
This is also why you can just cast a derived object to its base counterpart: in effect, you're just "looking at" that part of memory embedded within the derived object.

### 24.2 - Basic inheritance in C++
To make a class a derived class of another, you can use this syntax:
```cpp
// BaseballPlayer publicly inheriting Person
class BaseballPlayer : public Person
{
public:
    double m_battingAverage{};
    int m_homeRuns{};

    BaseballPlayer(double battingAverage = 0.0, int homeRuns = 0)
       : m_battingAverage{battingAverage}, m_homeRuns{homeRuns}
    {
    }
};
```
When doing so, BaseballPlayer take all member functions and variables from Person.
It also takes in two new data members, `battingAverage` and `homeRuns`.
### 24.3 - Order of construction of derived classes
C++ constructs derive classes in phases, starting with the most-base class (at the top of the inheritance tree) and finishing with the most-child class (at the bottom of the inheritance tree).
As each class is constructed, the appropriate constructor from that class is called to initialize that part of the class.
The inverse happens when destructing class instances.
### 24.4 - Constructors and initialization of derived classes
```cpp
class Base
{
public:
    int m_id {};

    Base(int id=0)
        : m_id{ id }
    {
    }

    int getId() const { return m_id; }
};

class Derived: public Base
{
public:
    double m_cost {};

    Derived(double cost=0.0)
        : m_cost{ cost }
    {
    }

    double getCost() const { return m_cost; }
};
```
When a `Derived` is initialized, the `Base` constructor is called first, then returning control to the `Derived` constructor which sets the `Derived` part of the class.
### 24.5 - Inheritance and access specifiers
Along `private` and `public` access specifiers, there also exists the **`protected` access specifier**.
This is much like `private`, except it means those members are public to classes **inheriting from the class the members belong to**.
Making a member `protected` has a side-effect: your derived classes will be able to modify the base parts.
This is sometimes unwanted. As such, **you should try to favor `private` member over `protected` ones.**
___
Just as there are three access specifiers, **there are three ways to inherit a class**:
- Publicly
- Protectedly
- Privately
These all change the access specifiers of derived members in the new derived class.
Let's go through all three, one by one.
#### Public inheritance
By far the most used kind of inheritance. It's the most simple one, too, because all members keep their initial access specifiers:

| Access specifier in base class | Access specifier when inherited publicly |
| ------------------------------ | ---------------------------------------- |
| Public                         | Public                                   |
| Protected                      | Protected                                |
| Private                        | Inaccessible                             |
**Use that kind of inheritance unless you have a specific reason not to.**
#### Protected inheritance
With protected inheritance, **the public and protected become protected.**

| Access specifier in base class | Access specifier when inherited protectedly |
| ------------------------------ | ------------------------------------------- |
| Public                         | Protected                                   |
| Protected                      | Protected                                   |
| Private                        | Inaccessible                                |
#### Private inheritance
Same as protected, but they become **private instead**.
> **Note that this does not affect the way that the derived class accesses members inherited from its parent! It only affects the code trying to access those members through the derived class.**

| Access specifier in base class | Access specifier when inherited privately |
| ------------------------------ | ----------------------------------------- |
| Public                         | Private                                   |
| Protected                      | Private                                   |
| Private                        | Inaccessible                              |
Private inheritance is mostly useful for inheriting a class you don't want the interface of accessible through your derived class.
### 24.6 - Adding new functionality to a derived class
When you derive from a class, you'll often want to add functionality to your derived class without modifying the base one.
You can do that by simply declaring new members in your derived class.
### 24.7 - Calling inherited functions and overriding behavior
You can make functions derived from base classes have different behavior by overriding them.
This happens by simply redefining them in your derived class.
When you override a function or data member, its access specifier isn't inherited, you have to redefine it yourself.
A function that was private in the base class can be public or protected in the derived class.
___
