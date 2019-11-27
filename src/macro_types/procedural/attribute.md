# Attribute

1. See everything about an *item*.
2. Takes in tokens, and outputs *replacement* tokens.

```rust,ignore
// See <https://github.com/azriel91/proc_macro_roids>.
use macro_crate::append_cd;

#[append_cd]
struct StructNamed { a: u32, b: i32 }

// outputs:
struct StructNamed { a: u32, b: i32, c: i64, d: usize }
```

[🚀 Rocket](https://rocket.rs/) framework:

```rust,ignore
#[get("/hello/<name>/<age>")]
fn hello(name: String, age: u8) -> String {
    format!("Hello, {} year old named {}!", age, name)
}

fn main() {
    rocket::ignite().mount("/", routes![hello]).launch();
}
```
