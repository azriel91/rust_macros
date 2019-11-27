# Declarative

> **Human:** "Macro, here are some (well-formed) tokens."
>
> **Macro:** "Here are some code tokens." &nbsp;&nbsp; *OR*  
> **Macro:** "No rules expected the token \`..\`"

## Definition

```rust
macro_rules! my_macro {
    (pattern_0) => {
        println!("some tokens");
    };

    (pattern_1) => {
        println!("other tokens");
    };

    // $param_name:param_type
    // $( $repeated_param:param_type ),* // Zero or more, comma delimited
    // $( $repeated_param:param_type ),+ // One or more, comma delimited
    //
    // See <https://danielkeep.github.io/tlborm/book/mbe-macro-rules.html#captures>
    ($name:ident) => {
        println!("{}", stringify!($name));
    };
}
```

## Usage

```rust
macro_rules! my_macro {
    (pattern_0) => { println!("some tokens"); };
    (pattern_1) => { println!("other tokens"); };
    ($name:ident) => { println!("ident: {}", stringify!($name)); };
    (pattern_2) => { println!("even more tokens"); };
}

my_macro!(pattern_0);
my_macro!(pattern_1);
my_macro!(single_identifier);
my_macro!(pattern_2); // note: rules are evaluated in order.
```

---

<details>

<summary>Declarative macros in the wild</summary>

* [`bitflags`](https://github.com/bitflags/bitflags/blob/1.2.1/src/lib.rs#L333):

    ```rust,ignore
    #[macro_use]
    extern crate bitflags;

    bitflags! {
        struct Flags: u32 {
            const A = 0b00000001;
            const B = 0b00000010;
            const C = 0b00000100;
            const ABC = Self::A.bits | Self::B.bits | Self::C.bits;
        }
    }
    ```

* [`lazy_static!`](https://github.com/rust-lang-nursery/lazy-static.rs/blob/1.4.0/src/lib.rs#L166)

    ```rust,ignore
    # #[macro_use]
    # extern crate lazy_static;
    #
    # use std::collections::HashMap;
    #
    lazy_static! {
        static ref HASHMAP: HashMap<u32, &'static str> = {
            let mut m = HashMap::new();
            m.insert(0, "foo");
            m.insert(1, "bar");
            m.insert(2, "baz");
            m
        };
        static ref COUNT: usize = HASHMAP.len();
        static ref NUMBER: u32 = times_two(21);
    }
    #
    # fn times_two(n: u32) -> u32 { n * 2 }
    #
    # fn main() {
    #     println!("The map has {} entries.", *COUNT);
    #     println!("The entry for `0` is \"{}\".", HASHMAP.get(&0).unwrap());
    #     println!("A expensive calculation on a static results in: {}.", *NUMBER);
    # }
    ```

</details>

See also: [The Little Book of Rust Macros](https://danielkeep.github.io/tlborm/book/index.html) (comprehensive guide)
