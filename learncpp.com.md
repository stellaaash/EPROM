---
tags:
  - Tutorial
  - cpp
Website: https://www.learncpp.com/
Status: IN PROGRESS
---
[[C++]] tutorials and learning materials.
# Progress
12.10
# Bookmarks - Stuff to remember
My personal bookmarks are those of someone that comes from a small background of working in C over several months in a wide variety of projects.
This is why I'm not noting everything down, only those things relevant to someone with knowledge of standard C.
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
### 