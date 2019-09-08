# Minamoto Language
A simple, C-like programming language.


## Variables & Data Types
Variables are simply declared like this `type name = value;`    
There is no special keyword like 'var' or 'let' beacause what type a variable is should be in focus.

Variables are immutable by default like they are in rust.    
To make a variable mutable use the `mut` keyword like this `i32 mut var = 42;`

You can get information about any variable by using meta handles

| Handle | Description |
| ------ | ------ |
| `var:type` | Variable type, like `i32`, `f16`, `ptr-c8`, `ptr-void`, etc.. |
| `var:size` | Size of whole collection in bytes (size of type for non-arrays) |
| `var:len` | Length of collection (always 1 for non-arrays) |
| `var:cap` | Capacity of arrays (always 1 for non-arrays) |


### Scalar Types
| Size | Signed Integer | Unsigned Integer | Floating Point | Character |
| ------ | ------ | ------ | ------ | ------ |
| 8-bit  | `i8`   | `u8`   | `f8`   | `c8`   |
| 16-bit | `i16`  | `u16`  | `f16`  | `c16`  |
| 32-bit | `i32`  | `u32`  | `f32`  | `c32`  |
| 64-bit | `i64`  | `u64`  | `f64`  |
| 128-bit | `i128` | `u128` |
| Architecture | `isize` | `usize` |

Examples of declaring variables:

```rust
i32  integer   = 42;
f64  floating  = 3.1415;
usize unsigned = 127;    // unsigned integer with the same size as the architecture
```

```rust
c8  character = 'A';  // can hold all ascii characters
c32 character = 'あ'; // can hold any unicode charater
```

#### Boolean Type
The boolean type `bool` can only be the values `true` and `false`, which can also be defined using `0` and `1`.

```rust
bool var_a = true; // 1
bool var_b = 0;    // false
```

### Arrays
Arrays are static, stack allocated collections of scalar variables.
```rust
i16 array_a[]    = [10, 20, 30];  // lenght 3, all set
f64 array_b[5];                   // length 5, all 0
i32 array_c[10]  = [1, 2];        // length 10, first two set, rest 0
u8  array_d[128] = [255, ...];    // length 128, set all to 255
c8  array_e[1, 10];               // Initial length of 1, can be expanded to 10

c8  string[] = "Hello!";
```
You can get information about an array using the meta handles
```rust
println("Length of array_a: {}", array_a:len); // Length of array_a: 3
println("Size of array_a: {}", array_a:size);  // Size of array_a: 6
```


### The Pointer Type
Pointers are defined as a special type `ptr` pointing to some memory. It also contains information about the data it points to like type, length, capacity, etc..

```rust
ptr pointer_x      = null; // void pointer to null
ptr pointer_y(i32) = null; // i32 pointer to null

ptr pointer_a = &interger_var;          // pointer to to some integer value, taking the type
ptr pointer_b(i16, 10);                 // allocates memory at runtime of size 10 * `i16`
ptr pointer_c(f32, 1, 20);              // allocates memory at runtime of size 20 * `f32`, with current length set to 1
ptr pointer_d(u8, size_var) = [255...]; // allocates memory at runtime of size 'size_var' and sets it to 255

unsafe ptr pointer_e(my_struct, 1024) = 0xFE78A2; // points to memory location specified and maps it as an array of type 'my_struct' with a length of 1024 (this is considered unsafe)
```


### String Type
The string type `str` is more or less an alias of `ptr` but limited to characters, and automatically chooses the char size.
```rust
str string_a = "Hello";
string_a.append(", World!");
```

