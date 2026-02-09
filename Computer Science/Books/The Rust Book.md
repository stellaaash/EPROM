---
tags:
  - book
Status: PAUSED
Website: https://doc.rust-lang.org/book/
---
The official rust tutorial and also a form of documentation.
This is what I'm gonna start with for learning Rust!
# Progress
10.3
# Bookmarks
## 3 - Common programming concepts
### 3.1 - Variables and Mutability
Variables in rust are immutable by default.
You create them with `let`, which creates an immutable variable. Add `mut` (`let mut`) to make it mutable.
___
Constants are a nice way to name hardcoded values to not have "magic numbers" in your codebase.
```rust
const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
```
Usually, constants will be evaluated at compile time.
___
Shadow a variable by calling `let` on the variable's name a second time. You can thus change a variable's type (with the initial value being lost, of course).
```rust
fn main() {
    let x = 5;

    let x = x + 1;

    {
        let x = x * 2;
        println!("The value of x in the inner scope is: {x}");
    }

    println!("The value of x is: {x}");
}
```
 > Shadowing is different from marking a variable as mut because we’ll get a compile-time error if we accidentally try to reassign to this variable without using the let keyword. By using let, we can perform a few transformations on a value but have the variable be immutable after those transformations have been completed.
### 3.2 - Data types 
#### Integers

| Length  | Signed  | Unsigned |
| ------- | ------- | -------- |
| 8-bit   | `i8`    | `u8`     |
| 16-bit  | `i16`   | `u16`    |
| 32-bit  | `i32`   | `u32`    |
| 64-bit  | `i64`   | `u64`    |
| 128-bit | `i128`  | `u128`   |
| arch    | `isize` | `usize`  |
___

| Number literals  | Example       |
| ---------------- | ------------- |
| Decimal          | `98_222`      |
| Hex              | `0xff`        |
| Octal            | `0o77`        |
| Binary           | `0b1111_0000` |
| Byte (`u8` only) | `b'A'`        |
___
When compiling in release mode, integer overflows in Rust are wrapped around. That means assigning 257 to an `u8` results in a value of 1.
In debug mode though, integer overflows cause a panic.
#### Floating points
Rust has two floating point types: `f32` and `f64`. I suppose you could treat them as `float` and `double` in C.
Just use `f64` in most cases though.
#### Characters
In rust, the `char` type is 4 bytes and represents a Unicode value.
#### Tuples
Tuples are an assortiment of values of whatever types you want:
```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
}
```
You take out the values of a tuple with pattern matching:
```rust
fn main() {
    let tup = (500, 6.4, 1);

    let (x, y, z) = tup;

    println!("The value of y is: {y}");
}
```
Of course you can also access individual values with `.`:
```rust
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);

    let five_hundred = x.0;

    let six_point_four = x.1;

    let one = x.2;
}
```
`()` is the empty type, denoting the absence of a value. It is called **the unit**.
#### Arrays
Rust also has arrays for stack-allocated, fixed size collection of same-typed values.
```rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
```
There's also vectors, which are basically arrays but resizable.
Arrays can be very useful for constants though.
___
You can init an array of a specific size with all values to the same value by specifying the value, followed by the size of the array:
```rust
let a = [3; 5];
```
This creates an array of size 5, with all slots set to 3.
___
Rust performs array bounds checking at run time, making the thread panic if an out-of-bound access is detected.
### 3.3 - Functions
**Statements** are instructions that perform some action and do not return a value.
**Expressions** evaluate to (and thus return) a constant value.
For example, a variable assignation is a statement, and does not return the value assigned to a variable, contrary to some other languages.
You can't use `let` followed by a statement, for example.
For a special example, scope blocks evaluate to an expression:
```rust
{
    let x = 3;
    x + 1
}
```
This block evaluates to 4. to 4.
The last expression in a scope block is the return value of that block.
**This is also valid for functions: the last expression of a function body is its return value.** Note the absence of a semi-colon on the last line, preventing the expression from becoming a statement.
Of course you can still use `return` to return before the end of the function if needed.
### 3.5 - Control flow
#### Conditions
It's worth noting that rust expects actual bools in conditions, which means number and other types aren't implicitly converted to bools.
You can't just do `if number {`, rust kindly asks for an actual condition like `if number != 0 {`.
___
If statements are **expressions**, not statements, which means you can use them to assign a value to a variable, ternary style:
```rust
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };

    println!("The value of number is: {number}");
}
```
#### Loops
There's three different types of loops: `loop`, and the usual `while` and `for`.
`loop` is really just an infinite loop shorthand.
One of the big changes that follow the style of having a return value for each block of code, is that loops also can return stuff:
```rust
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    println!("The result is {result}");
}
```
This stores the result of the loop (counter * 2 in the `break` statement) inside of the `result` variable.
`break` is basically the `return` statement, but for loops instead (`return` still returns from the current function, regardless of loop depth).
___
You can give **loop labels** to loops to increase readability, but also to give a target to `break` and `continue` statements.
This allows these statements to break or continue loops other than the current one, effectively bypassing levels of loops when doing so.
```rust
fn main() {
    let mut count = 0;
    'counting_up: loop {
        println!("count = {count}");
        let mut remaining = 10;

        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;
    }
    println!("End count = {count}");
}
```
___
Example of a for loop's syntax:
```rust
for number in (1..4).rev() {
```
## 4 - Ownership
### 4.1 - What is ownership?
- **Each value in Rust has an _owner_.**
- **There can only be one owner at a time.**
- **When the owner goes out of scope, the value will be dropped.**
___
Heap-allocated memory in rust is automatically returned when its owner goes out of scope.
The `free` equivalent for rust is `drop`, and it is called on objects that go out of scope.
This function is responsible for calling the destructor for the type that's being dropped.
You can't call it explicitly, instead use `std::mem::drop()`.
___
`String`s are composed of a pointer to the heap allocated buffer, a length and a capacity.
When we copy the string, it only reassigns those three elements on the stack to a new name, invalidating the old reference.
In effect, it **gives ownership of that variable's values to a new one**.
**Any automatic copying will never make a deep copy of data implicitly.** Therefore, any automatic copies can be assumed to be inexpensive.
When you want to do a deep copy of a variable, use the `clone()` method. This makes it explicit when you want to make a deep, expensive copy of underlying heap data (i.e. for strings).
___
When you assign a new value to an existing variable, `drop` is called as well:
```rust
    let mut s = String::from("hello");
    s = String::from("ahoy");

    println!("{s}, world!");
```
Since the original string "hello" goes out of scope by assigning a new one to the same variable, it is automatically dropped.
___
Fundamental types like integers aren't moved when assigning a variable to another, but copied instead.
This is thanks to the `Copy` trait: if a type has it, when you assign a variable of that type to another, its values are deep copied instead of moved.
This is often done on fundamental types and types that are inexpensive to copy.
The `Copy` trait is mutually exclusive with the `Drop` trait, which says a type has a custom destructor (?).
Most fundamental types have the `Copy` trait, because they're stack allocated and their size are known at compile time. Here's a non-exhaustive list:
- All the integer types, such as `u32`.
- The Boolean type, `bool`, with values `true` and `false`.
- All the floating-point types, such as `f64`.
- The character type, `char`.
- Tuples, if they only contain types that also implement `Copy`. For example, `(i32, i32)` implements `Copy`, but `(i32, String)` does not.
___
Functions that have arguments have the same system of copying vs moving depending on whether the values have the `Copy` and `Drop` traits.
That means that if you pass a value that doesn't have the `Copy` trait to a function, that function takes ownership of that variable.
Here's a few examples taken from the Rust book:
```rust
fn main() {
    let s = String::from("hello");  // s comes into scope

    takes_ownership(s);             // s's value moves into the function...
                                    // ... and so is no longer valid here

    let x = 5;                      // x comes into scope

    makes_copy(x);                  // because i32 implements the Copy trait,
                                    // x does NOT move into the function,
    println!("{}", x);              // so it's okay to use x afterward

} // Here, x goes out of scope, then s. But because s's value was moved, nothing
  // special happens.

fn takes_ownership(some_string: String) { // some_string comes into scope
    println!("{some_string}");
} // Here, some_string goes out of scope and `drop` is called. The backing
  // memory is freed.

fn makes_copy(some_integer: i32) { // some_integer comes into scope
    println!("{some_integer}");
} // Here, some_integer goes out of scope. Nothing special happens.
```
___
Returning a value can also transfer its ownership.
```rust
fn main() {
    let s1 = gives_ownership();        // gives_ownership moves its return
                                       // value into s1

    let s2 = String::from("hello");    // s2 comes into scope

    let s3 = takes_and_gives_back(s2); // s2 is moved into
                                       // takes_and_gives_back, which also
                                       // moves its return value into s3
} // Here, s3 goes out of scope and is dropped. s2 was moved, so nothing
  // happens. s1 goes out of scope and is dropped.

fn gives_ownership() -> String {       // gives_ownership will move its
                                       // return value into the function
                                       // that calls it

    let some_string = String::from("yours"); // some_string comes into scope

    some_string                        // some_string is returned and
                                       // moves out to the calling
                                       // function
}

// This function takes a String and returns a String.
fn takes_and_gives_back(a_string: String) -> String {
    // a_string comes into
    // scope

    a_string  // a_string is returned and moves out to the calling function
}
```
___
As an aside, you can return a tuple from a function, effectively returning multiple values:
```rust
fn calculate_length(s: String) -> (String, usize) {
    let length = s.len(); // len() returns the length of a String

    (s, length)
}
```
### 4.2 - References and Borrowing
If you don't want a function taking ownership of your variables (many such cases), you can give your function **a reference** instead.
Unlike pointers, **references are guaranteed to point to a valid value for as long as they exist**.
```rust
fn main() {
    let s1 = String::from("hello");

    let len = calculate_length(&s1);

    println!("The length of '{s1}' is {len}.");
}

fn calculate_length(s: &String) -> usize {
    s.len()
}
```
Because references don't own their pointed values, the latter aren't dropped when their references go out of scope.
You call the action of giving a reference to something **borrowing**.
**References are immutable by default, which means you can't modify the underlying value through them by default.**
Just like regular variables, you need to make references mutable explicitly:
```rust
fn main() {
    let mut s = String::from("hello");

    change(&mut s);
}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}
```
Note that both the reference **and** the underlying variable must be `mut`.
**You cannot have more than one mutable reference to a variable at a time.**
This design decision in Rust prevents data races at compile time.
*To be clear, you can create multiple mutable references to a variable, just not at the same time.*
*Use scope blocks with brackets to keep mutable references's lifetimes short.*
This also applies to non-mutable references: **mutable and immutable references are mutually exclusive, you can't have both at the same time.**
Either multiple immutable refs, or one mutable ref.
This basically means things like mutexes and other such stratagems to prevent multiple modifications at the same time aren't needed, simply because you can't read a variable's value via reference while it's being modified via another, mutable, reference.
___
Note that a reference's scope goes as far as their last usage, which means that past that point you can create a mutable reference if you had immutable ones beforehand:
```rust
    let mut s = String::from("hello");

    let r1 = &s; // no problem
    let r2 = &s; // no problem
    println!("{r1} and {r2}");
    // Variables r1 and r2 will not be used after this point.

    let r3 = &mut s; // no problem
    println!("{r3}");

```
### 4.3 - Slices
Slices are a kind of reference, they don't have ownership.
```rust
    let s = String::from("hello world");

    let hello = &s[0..5];
    let world = &s[6..11];

```
This is an example of **string slices**.
You create a slice by specifying `[starting_index..ending_index]`, where the end index is non-inclusive.
Internally, a slice is composed of the starting position and a length.
If you want your slice to start or end at the tip of the string, you can drop one or both of the values around the `..` part:
```rust
let slice = &s[..2]; // From start to 1
let slice = &s[3..]; // From 3 to end
let slice = &s[..];  // Entire string
```
___
The type representing a string slice is denoted as `&str`, because `str` is for a string slice.
Strings literals are actually slices as well.
In general, you'll want your functions to take in a `&str` instead of a `&String`; this makes your function more flexible: it can both take slices and references or slices of a String.
If you had used `&String`, only references to Strings would be accepted.
```rust
fn main() {
    let my_string = String::from("hello world");

    // `first_word` works on slices of `String`s, whether partial or whole.
    let word = first_word(&my_string[0..6]);
    let word = first_word(&my_string[..]);
    // `first_word` also works on references to `String`s, which are equivalent
    // to whole slices of `String`s.
    let word = first_word(&my_string);

    let my_string_literal = "hello world";

    // `first_word` works on slices of string literals, whether partial or
    // whole.
    let word = first_word(&my_string_literal[0..6]);
    let word = first_word(&my_string_literal[..]);

    // Because string literals *are* string slices already,
    // this works too, without the slice syntax!
    let word = first_word(my_string_literal);
}
```
___
Strings slices are a thing, but you can actually make slices of any array, like integer arrays:
```rust
let a = [1, 2, 3, 4, 5];

let slice: &[i32] = &a[1..3];

assert_eq!(slice, &[2, 3]);

```
## 5 - Structs
### 5.1 - Definition and Instantiating
When using a function to initialize a struct and passing parameters to that function that are going to be assigned to struct fields, name the parameters the same way as the fields themselves.
This will allow you to use a convenient shorthand:
```rust
fn build_user(email: String, username: String) -> User {
    User {
        active: true,
        username,
        email,
        sign_in_count: 1,
    }
}
```
___
You can easily copy a struct's values inside a new instance of that struct type with another shorthand:
```rust
    let user2 = User {
        email: String::from("another@example.com"),
        ..user1
    };
```
This copies all of `user1`'s values, except for the email which is assigned another value.
Careful though, this examples **moves** the username string from user1 to user2, making the first unusable.
___
You can create named tuples by making a tuple struct.
This allows to give a particular combination of types as a struct a name:
```rust
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

fn main() {
    let black = Color(0, 0, 0);
    let origin = Point(0, 0, 0);
}
```
___
You can also declare structs without any fields (called unit-like structs) if you need a type that doesn't contain anything.
___
In theory you want most if not all of your struct fields to be owned by the struct itself, that way when the struct is destroyed, all underlying data is destroyed as well.
### 5.3 - Methods and associated functions
Methods are function that take a `Self` element as a parameter, meaning they take the object they are being called upon as parameter.
They are defined in an `Impl` block for the specific type they're linked to.
```rust
impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }

    fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
}
```
___
Associated functions are methods that don't take `Self` as a parameter, but still are associated with a type (in an `Impl` block).
This is often used for constructors, and they can be accessed with `::` instead of `.`.
```rust
impl Rectangle {
    fn square(size: u32) -> Self {
        Self {
            width: size,
            height: size,
        }
    }
}
```

## 6 - Enums and pattern matching
### 6.1 - Enums and optionals
You access enumerators of an enum (called **variants**) by the namespace operator `::`.
Enums are types and can be used to represent their values, in structs for example:
```rust
    enum IpAddr {
        V4(String),
        V6(String),
    }

    let home = IpAddr::V4(String::from("127.0.0.1"));

    let loopback = IpAddr::V6(String::from("::1"));

```
You can put data directly inside of each enum variant. Here, we have a String.
___
The name of each variant becomes a constructor for that variant; this is why you can call `IpAddr::V4()` here.
You can even have multiple variables embedded inside of an enum variant:
```rust
    enum IpAddr {
        V4(u8, u8, u8, u8),
        V6(String),
    }

    let home = IpAddr::V4(127, 0, 0, 1);

    let loopback = IpAddr::V6(String::from("::1"));

```
This means you can basically have enum variants that contain struct detailing the contents of the IP address you want to represent (or whatever else, this is just an example).
___
Enum variants can have named fields, like structs do:
```rust
enum Message {
	Quit,                        // Contains nothing
    Move { x: i32, y: i32 },     // Named fields
    Write(String),               // Contains a string
	ChangeColor(i32, i32, i32),  // Contains 3 integers
}
```
___
Just as with structs, you can make an `impl` block to define methods related to an enum type:
```rust
    impl Message {
        fn call(&self) {
            // method body would be defined here
        }
    }

    let m = Message::Write(String::from("hello"));
    m.call();
```
___
Optionals exist in rust, implemented via the `Option<T>` enum.
```rust
enum Option<T> {
    None,
    Some(T),
}
```
There aren't Null references in rust, instead, you use the `None` variant of `Option`, like this:
```rust
    let some_number: Option<char> = Some(5);
    let some_char: Option<char> = Some('e');

    let absent_number: Option<i32> = None;
```
To be very clear, optional types aren't the same as the underlying type; you can't do operations between the two like addition and stuff for integers.
### 6.2 - The match control flow
Match statements allow to test an expression against a variety of possibilities and execute an associated block of code and/or return a value.
```rust
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => {
            println!("Lucky penny!");
            1
        }
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}
```
___
You access enum variants' contained variables inside of match statements (and everywhere else), like so:
```rust
#[derive(Debug)] // so we can inspect the state in a minute
enum UsState {
    Alabama,
    Alaska,
    // --snip--
}

enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter(UsState),
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter(state) => {
            println!("State quarter from {state:?}!");
            25
        }
    }
}
```
___
You can also use `match` to process `Option<T>`:
```rust
    fn plus_one(x: Option<i32>) -> Option<i32> {
        match x {
            None => None,
            Some(i) => Some(i + 1),
        }
    }

    let five = Some(5);
    let six = plus_one(five);
    let none = plus_one(None);
```
___
Match statements must be exhaustive in the possibilities they cover.
You can add placeholders for statement that must all cover all remaining possibilities:
```rust
    let dice_roll = 9;
    match dice_roll {
        3 => add_fancy_hat(),
        7 => remove_fancy_hat(),
        other => move_player(other),
    }

    fn add_fancy_hat() {}
    fn remove_fancy_hat() {}
    fn move_player(num_spaces: u8) {}
```
Here, `other` represents every other value aside 3 and 7, and is going to be put into `move_player()` (that's why we give it a name).
For all other possibilities that we don't want to use explicitly, Rust also has a pattern to represent that: `_`.
```rust
    let dice_roll = 9;
    match dice_roll {
        3 => add_fancy_hat(),
        7 => remove_fancy_hat(),
        _ => reroll(),
    }

    fn add_fancy_hat() {}
    fn remove_fancy_hat() {}
    fn reroll() {}
```
When you want to discard a value and not do anything with it, you can use the unit value `()` to mean that you're not doing any action with something:
```rust
		_ => (),
```
Here, we replaced `reroll()` with just `()`.
### 6.3 - If let and let else
Instead of using a `match` statement to check if a optional contains a value:
```rust
	let config_max = Some(3u8);  // Assign the value 3 to an u8
    match config_max {
        Some(max) => println!("The maximum is configured to be {max}"),
        _ => (),
    }
```
You can use a `if let` statement to check if a value is a `Some` and extract what's inside:
```rust
    let config_max = Some(3u8);
    if let Some(max) = config_max { // `max` represents what's inside the `Some`.
        println!("The maximum is configured to be {max}");
    }
```
`Some(max)` allows us to extract the optional `config_max` and its value.
In this way, `if let` works essentially like a `match` statement with a unique arm and `_ => ()` for the rest of the values.
Careful though, `if let` only checks for a single possibility, meaning it's not as exhaustive as `match`. Use either of them when appropriate.
There's also `else` statements with `if let`:
```rust
    let mut count = 0;
    if let Coin::Quarter(state) = coin {
        println!("State quarter from {state:?}!");
    } else {
        count += 1;
    }
```
___
Maybe more common is the `let...else` statement, extracting a value from an optional if it exist, or doing something otherwise:
```rust
fn describe_state_quarter(coin: Coin) -> Option<String> {
    let Coin::Quarter(state) = coin else {  // If coin is a Coin::Quarter, extract the state within
        return None;
    };

    if state.existed_in(1900) {
        Some(format!("{state:?} is pretty old, for America!"))
    } else {
        Some(format!("{state:?} is relatively new."))
    }
}
```
## 7 - Packages, Crates and Modules
### 7.1 - Packages and Crates
A **crate** is the smallest group of files to produce a project. This can be single file or an assortiment.
Crates are divided between library and binary crates.
Those are pretty self-explanatory, binaries having a `main()` function and compiling to a program, and libraries defining functionality for use by another program.
You often import those as crates to be used by your program like the `rand` crate.
The **crate root** is the file the rust compiler starts from. It becomes the **root module** of your crate.
___
A **package** is a bundle of crate that provide a set of functionality.
A package contains a *Cargo.toml* that describes how to build the crates together.
Fun fact: Cargo is actually a binary crate that depends on a library crate also called Cargo; it contains the cli tool itself.
A package can contain as many binary crates as needed, but maximum one library crate.
When you run `cargo new`, a new package is created (a Cargo.toml file is present).
### 7.2 - Modules
You can access modules inside of your own create (defined using a `mod` statement) by using `crate::Path::To::Module`.
Often, the path to your module is analogous to the real file path (because you would have the main.rs file in the root folder, and a Garden folder with a mod.rs file representing the Garden module and also another Vegetables folder with a mod.rs file etc...)
Make a module public to its parents with `pub mod`.
___
Modules are private by default, you must choose to make them public explicitly.
### 7.4 - Bring paths into scope with `use`
When including modules' functions, you usually include the parent module itself.
That way,when you use that function, you still have the context of the parent `Module::function()`.
When including other types, you include them directly usually.
___
You can rename stuff you include with the `as` keyword.
```rust
use std::io::Result as IoResult;
```
You can use `pub` with `use` to do a re-export; this exposes the included module/element to all scopes in the current module.
___
You can use nested `uses` to reuse some paths instead of having a bazillion vertical lines:
```rust
use std::cmp::Ordering;
use std::io;
// becomes
use std::{cmp::Ordering, io};
```
```rust
use std::io;
use std::io::Write;
// becomes
use std::io::{self, Write};
```
___
You can also use the glob (wildcart) `*` to use all public items from a given path.
### 7.5 - Splitting modules in different files
Here's an example taken from the Rust book:
___
Here, we create a binary crate named `backyard` that illustrates these rules. The crate’s directory, also named `backyard`, contains these files and directories:

```
backyard
├── Cargo.lock
├── Cargo.toml
└── src
    ├── garden
    │   └── vegetables.rs
    ├── garden.rs
    └── main.rs
```
The crate root file in this case is _src/main.rs_, and it contains:
```rust
use crate::garden::vegetables::Asparagus;

pub mod garden;

fn main() {
    let plant = Asparagus {};
    println!("I'm growing {plant:?}!");
}
```
The `pub mod garden;` line tells the compiler to include the code it finds in _src/garden.rs_, which is:
```rust
pub mod vegetables;
```
Here, `pub mod vegetables;` means the code in _src/garden/vegetables.rs_ is included too. That code is:
```rust
#[derive(Debug)]
pub struct Asparagus {}
```
## 8 - Common Collections
### 8.1 - Vectors
Vectors are dynamic arrays containing many values of the same type.
Easily resizable and modifiable.
### 8.2 - Strings
### 8.3 - HashMaps
Hashmaps are also called dictionaries in other languages.
## 9 - Error handling
### 9.1 - panic!
`panic!` makes the program crash with a given error message.
### 9.2 - Recoverable errors with `Result`
Result is an enum that contains either an `Ok` value wrapping the actual return value of a function, or an `Err` wrapping the error that has been returned.
### 9.3 - When to panic
Panic only when an error could put your program in a very, very bad state.
This means to panic only when unrecoverable errors happen, in the state of your current program.
It's unwise to make library code panic whenever an error occurs; it's probably best to leave that choice to the code calling the function you're making.
## 10 - Generics, Traits and Lifetimes
### 10.1 - Generics
Generics are basically like templates in C++. You replace a type with a placeholder, and when a function, struct or even implementation gets used with that type, the placeholder gets replaced.
### 10.2 - Traits
Traits are groups of methods that pertain to a particular type. If a type implements a trait, it means it implements the methods contained within.
You define method prototypes that this trait implements (name, return value, argument types).
Then, each type implementing that trait has to define all methods specifically (unless a default method is provided).
```rust
pub trait Summary {
    fn summarize(&self) -> String;
}

pub struct NewsArticle {
    pub headline: String,
    pub location: String,
    pub author: String,
    pub content: String,
}

impl Summary for NewsArticle {
    fn summarize(&self) -> String {
        format!("{}, by {} ({})", self.headline, self.author, self.location)
    }
}

pub struct SocialPost {
    pub username: String,
    pub content: String,
    pub reply: bool,
    pub repost: bool,
}

impl Summary for SocialPost {
    fn summarize(&self) -> String {
        format!("{}: {}", self.username, self.content)
    }
}
```
___
There's a rule (called the **orphan rule**) for traits in Rust:
**You can only implement a trait for the type if you own at least one of the two.**
This prevents conflicting implementations where you would implement external traits on external types in ways that weren't intended by the library you're using.
___
You can define default implementations for if an impl block doesn't implement a particular method, that default implementation be used instead.
```rust
pub trait Summary {
    fn summarize(&self) -> String {
        String::from("(Read more...)")
    }
}
```
___
You can use generics to ask for any type that implements a given trait, which is called a **trait bound**.
You can do so using multiple different syntaxes:
```rust
pub fn notify(item: &(impl Summary + Display)) {
```
```rust
pub fn notify<T: Summary + Display>(item: &T) {
```
These two make `T` a type that implements both `Summary` and `Display`.
When multiple trait bounds are present, it can be clearer to use `where` clauses:
```rust
fn some_function<T, U>(t: &T, u: &U) -> i32
where
    T: Display + Clone,
    U: Clone + Debug,
{
```
___
You can also return types that implement a given trait by having a return type be `impl Type`.
This is useful when you know the calling code of your function will only use methods of that given trait, so it doesn't need to care about the concrete type.
Perhaps counter intuitively though, doing so will prevent you from returning different types: **you can only return one concrete type.**
This is a compiler restriction, but there are ways around it. See chapter 18.
___
When using impl statements that work on generics, you can create different methods depending on the type being passed for the generic.
This means when a type contains a certain type, create certains methods, when any other type, don't.
Perhaps this is best explained with another example taken from the book:
```rust
use std::fmt::Display;

struct Pair<T> {
    x: T,
    y: T,
}

impl<T> Pair<T> {
    fn new(x: T, y: T) -> Self {
        Self { x, y }
    }
}

impl<T: Display + PartialOrd> Pair<T> {
    fn cmp_display(&self) {
        if self.x >= self.y {
            println!("The largest member is x = {}", self.x);
        } else {
            println!("The largest member is y = {}", self.y);
        }
    }
}
```
___
You can also implement a trait **for any type that implements another trait**.
This is called a **blanket implementation**; you will see those everywhere in the Rust std library.
As an example, `ToString` is implemented for any type that implements `Display` as well:
```rust
impl<T: Display> ToString for T {
    // --snip--
}
```
This makes sense since to display a type in a readable form, you'd need to convert it to a string!
### 10.3 - Lifetimes
Lifetimes are another kind of generic, but rather than ensuring a type or trait, **they ensure that references stay valid as long as we need them to be**.
Every reference in Rust has a lifetime. A lifetime is **the scope for which that reference is valid.**
Most of the time, like types, lifetimes are implicit and inferred by the compiler.
Sometimes though, you might want to define them explicitly instead!
The main aim of lifetimes is to prevent dangling references.
#### The Borrow Checker
The Rust Compiler has a borrow checker that compares scopes to determine whether all borrows are valid.
Lifetimes are actually compiler annotations that help it check if a reference is valid or dangling at a given point.
___
Lifetime annotations don't actually change how long any of the references live.
Instead, they describe the **relationships of the lifetimes of multiple references to each other** without actually affecting them.
If you want a function to be able to receive any type of lifetime, you can do so using generics (again).
___
You annotate lifetimes using an apostrophe `'`.
```rust
&i32        // a reference
&'a i32     // a reference with an explicit lifetime
&'a mut i32 // a mutable reference with an explicit lifetime
```
One lifetime annotation by itself doesn't do much, since the annotations are meant to tell Rust how generic lifetime parameters of multiple references refer to each other.
___
To use lifetime annotations in a function signature, you need to declare the generic lifetime parameters inside the angle brackets.
```rust
fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() { x } else { y }
}
```
This `'a` lifetime ensures that the returned reference will be valid as long as both `x` and `y` remain valid.
Keep in mind that this doesn't change any lifetimes of either arguments or return value.
Rather, it gives a hint to the borrow checker: "hey, reject any value that doesn't adhere to the `'a` lifetime".
When we pass concrete reference as `x` and `y`, the `'a` lifetime effectively becomes **the duration for which both `x` and `y` are valid**.
As soon as one or both are dropped out of scope, the `'a` lifetime effectively ends, since continuing wouldn't satisfy the conditions we put in the `longest()` function signature.