# Derive

1. Attached to a struct / enum.
2. Generates *additional* tokens.
3. Can have *helper* attributes.
4. **Cannot** see sibling derives.

```rust,ignore
#[derive(CustomDerive)]
struct Struct; // Can see this.

// Can't see this.
impl Struct {
    // ..
}

#[derive(Clone, Copy, a_crate::CustomDerive)]
#[custom_derive(Debug)] // type level helper attribute
enum Enum {
    #[custom_derive(skip = "true")] // field level helper attribute
    Variant0,
    Variant1 { value: u32 },
}
```

**This is not reflection!**
