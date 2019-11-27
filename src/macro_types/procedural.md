# Procedural

Differences from declarative macros:

* 🌲 Parsing AST instead of matching patterns.
* 🔺 Can write procedural logic.
* 🦀 Better diagnostics.
* 💯 Easier to test.
* 📦 Dedicated crate *(not a selling point)*.

Types:

* Function-like
* Derive
* Attribute

    ```rust,ignore
    #[custom_attribute]
    fn do_something() {}

    #[custom_attribute]
    struct Hello;
    ```
