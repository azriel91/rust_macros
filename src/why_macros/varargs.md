# 🚂 Varargs

Rust doesn't support function overloading.

```rust,ignore
// Not supported:
fn my_println<A>(format: &'static str, a: A) -> String { /* .. */ }
fn my_println<A, B>(format: &'static str, a: A, b: B) -> String { /* .. */ }
fn my_println<A, B, C>(format: &'static str, a: A, b: B, c: C) -> String { /* .. */ }
```

Instead, macros can be used to generate a function body:

```rust
macro_rules! my_println {
    ($($token:tt),*) => {
        $(
            println!("{}", $token);
        )*
    };
}

my_println!("hello", "world");
my_println!("hello", "rust", "akl");

// Short for writing:
//
// println!("{}", "hello");
// println!("{}", "world");
// println!("{}", "hello");
// println!("{}", "rust");
// println!("{}", "akl");
```
