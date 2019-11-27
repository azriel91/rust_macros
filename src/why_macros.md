# Why Macros

Mainly to increase development ergonomics:

* 👥 Reduce duplication.
* 🏗️ Reduce boilerplate.
* 🚂 Varargs.

<details>

<summary>Not because you can do this</summary>

```rust
# macro_rules! java {
#     (static void $name:ident($($_:tt)+) { $($body:tt)+ }) => {
#         fn $name() { java!($($body)+); }
#     };
#
#     ($_:ident.$__:ident.$fn_name:ident($args:tt);) => {
#         println!($args);
#     };
# }
#
java! {
    static void main(String[] args) {
        System.out.println("jRust!");
    }
}
#
# // Need to do this to get playpen to detect main function.
# #[cfg(test)]
# fn main() {}
```

</details>
