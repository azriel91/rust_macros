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
