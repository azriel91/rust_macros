# What Are (Rust) Macros

**<span style="font-size: 0.7em;">(not azriel's)</span> Definition:** Copy-paste code without the pasta. And varargs.

* Shortcode:

    Original:

    ```rust
    use std::ops::Add;

    #[derive(Clone, Copy, PartialEq)]
    pub struct HealthPoints(pub u32);

    impl Add for HealthPoints {
        type Output = HealthPoints;

        fn add(self, other: HealthPoints) -> HealthPoints {
            HealthPoints(self.0 + other.0)
        }
    }
    ```

    Macro-treated:

    ```rust,ignore
    #[derive(derive_more::Add, Clone, Copy, PartialEq)]
    pub struct HealthPoints(pub u32);
    ```

* Varargs:

    ```rust
    let (a, b) = (3., 2.);

    println!();
    println!("hello");
    println!(
        "{a:.1} ÷ {b:.1} = {answer:.2}",
        a = a,
        b = b,
        answer = a / b
    );
    ```
