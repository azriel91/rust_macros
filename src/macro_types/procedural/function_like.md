# Function-Like

1. Takes in any well-formed tokens.
2. Outputs replacement tokens.

```rust,ignore
function_like!("Looks just like `macro_rules!`");
function_like! {
    struct Name {
        field: Type
    }
}

my_vec![];
map! {
    "key_0" => 123,
    "key_1" => 456,
};
```

```rust
println!("hi");
println! { "hi" };
println!["hi"];

let numbers_0 = vec! { 1, 2, 3 };
let numbers_1 = vec!(1, 2, 3);
println!("{:?}", numbers_0);
println! { "{:?}", numbers_1 };
```
