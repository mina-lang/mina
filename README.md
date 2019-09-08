# Minamoto Language
A simple, C-like programming language.


## Variables & Data Types





### Scalar Types
| Size | Signed Integer | Unsigned Integer | Floating Point | Character |
| ------ | ------ | ------ | ------ | ------ |
| 8-bit | `i8` | `u8` | `f8` | `c8` |
| 16-bit | `i16` | `u16` | `f16` | `c16` |
| 32-bit | `i32` | `u32` | `f32` | `c32` |
| 64-bit | `i64` | `u64` | `f64` |
| 128-bit | `i128` | `u128` |
| Architecture | `isize` | `usize` |

Examples of declaring variables:

```rust
i32  integer  = 42;
f64  floating = 3.1415;
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

### Compound Types

#### Array Type
Declaring an array variable
```rust
i16 array_a[]    = [10, 20, 30];  // lenght 3, all set
f64 array_b[5];                   // length 5, all 0
i32 array_c[10]  = [1, 2];        // length 10, first two set, rest 0
u8  array_d[128] = [255, ...];    // length 128, set all to 255

c8  string[] = "Hello!";
```
Getting information about an array
```rust
println("Length of array_a: {}", array_a:len);
```

```mina
array:type	// variable type. i32, f16, ptr-c8, ptr-void, etc..
array:size	// size of whole collection
array:len	// length of collection (always 1 for non-arrays)
array:cap	// capacity of arrays (always 1 for non-arrays)
```

### The Pointer Type
Pointers are defined as a special type `ptr` pointing to some memory. It also contains information about the data it points to like type, length, capacity, etc..

```rust
ptr pointer_a      = null;          // void pointer to null

ptr pointer_b(i32) = &interger_var; // i32 pointer to to some integer value of the same size
ptr pointer_c(f32, 1, 20);          // heap allocates memory for 20 'f32' values at runtime, with current length set to 1
ptr pointer_d(u8, size_var);        // allocates memory at runtime of size size_var

unsafe ptr pointer_e(my_struct, 1024) = 0xFE78A2; // points to memory specified and mappes it as an array of 'my_struct' (this is considered unsafe)
```


