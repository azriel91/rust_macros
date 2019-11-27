# Debugging

## Panic

For `proc-macro`s, well placed `panic!()`s are immensely useful:

```rust,ignore
let token_stream = quote! { .. };

// This method will work even if tokens are invalid
panic!("{}", token_stream.to_string());
```

## Cargo Expand

[`cargo-expand`](https://github.com/dtolnay/cargo-expand) is your friend.

[`cargo-expand`](https://github.com/dtolnay/cargo-expand) will expand macros to code tokens, for both declarative and procedural macros:

```rust
fn main() {
    println!("hello {}, one {:?}, two {:.2}", "hello", 1.1, 2.5);
}
```

Expands to:

```rust,ignore
#![feature(prelude_import)]
#[prelude_import]
use std::prelude::v1::*;
#[macro_use]
extern crate std;
fn main() {
    {
        ::std::io::_print(::core::fmt::Arguments::new_v1_formatted(
            &["hello ", ", one ", ", two ", "\n"],
            &match (&"hello", &1.1, &2.5) {
                (arg0, arg1, arg2) => [
                    ::core::fmt::ArgumentV1::new(arg0, ::core::fmt::Display::fmt),
                    ::core::fmt::ArgumentV1::new(arg1, ::core::fmt::Debug::fmt),
                    ::core::fmt::ArgumentV1::new(arg2, ::core::fmt::Display::fmt),
                ],
            },
            &[
                ::core::fmt::rt::v1::Argument {
                    position: ::core::fmt::rt::v1::Position::At(0usize),
                    format: ::core::fmt::rt::v1::FormatSpec {
                        fill: ' ',
                        align: ::core::fmt::rt::v1::Alignment::Unknown,
                        flags: 0u32,
                        precision: ::core::fmt::rt::v1::Count::Implied,
                        width: ::core::fmt::rt::v1::Count::Implied,
                    },
                },
                ::core::fmt::rt::v1::Argument {
                    position: ::core::fmt::rt::v1::Position::At(1usize),
                    format: ::core::fmt::rt::v1::FormatSpec {
                        fill: ' ',
                        align: ::core::fmt::rt::v1::Alignment::Unknown,
                        flags: 0u32,
                        precision: ::core::fmt::rt::v1::Count::Implied,
                        width: ::core::fmt::rt::v1::Count::Implied,
                    },
                },
                ::core::fmt::rt::v1::Argument {
                    position: ::core::fmt::rt::v1::Position::At(2usize),
                    format: ::core::fmt::rt::v1::FormatSpec {
                        fill: ' ',
                        align: ::core::fmt::rt::v1::Alignment::Unknown,
                        flags: 0u32,
                        precision: ::core::fmt::rt::v1::Count::Is(2usize),
                        width: ::core::fmt::rt::v1::Count::Implied,
                    },
                },
            ],
        ));
    };
}
```
