# Why Not Macros

* Compilation time increases.

    - Code tokens have to be generated before the actual-code-to-compile exists.
    - Rust has to compile proc-macro crates, then run it over your crate.
    - Multiple versions of proc-macro crates means multiple compilation.

* Not IDE friendly.

    Generated accessors are not indexed by RLS / Rust analyzer, so you don't get "Jump to definition".
