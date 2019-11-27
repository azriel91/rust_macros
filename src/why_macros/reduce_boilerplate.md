# 🏗️ Reduce boilerplate

**Scenario:** Newtype that behaves like a number -- math operators work as any numeric type.

<details open>

<summary>No macros</summary>

```rust
use std::ops::{Add, AddAssign, Sub, SubAssign};

/// Character health points.
#[derive(Clone, Copy, PartialEq)]
pub struct HealthPoints(pub u32);

impl Add for HealthPoints {
    type Output = HealthPoints;

    fn add(self, other: HealthPoints) -> HealthPoints {
        HealthPoints(self.0 + other.0)
    }
}

impl AddAssign for HealthPoints {
    fn add_assign(&mut self, other: HealthPoints) {
        *self = HealthPoints(self.0 + other.0);
    }
}

impl Sub for HealthPoints {
    type Output = HealthPoints;

    fn sub(self, other: HealthPoints) -> HealthPoints {
        HealthPoints(self.0 - other.0)
    }
}

impl SubAssign for HealthPoints {
    fn sub_assign(&mut self, other: HealthPoints) {
        *self = HealthPoints(self.0 - other.0);
    }
}
```

</details>

<details>

<summary>Reduction level 1 -- `proc_macro_derive`</summary>

```rust,ignore
/// Character health points.
#[derive(
    derive_more::Add,
    derive_more::AddAssign,
    derive_more::Sub,
    derive_more::SubAssign,
    derive_more::Display,
    derive_more::From,
    Clone,
    Copy,
    PartialEq,
    Eq,
    PartialOrd,
    Ord,
    Hash,
)]
pub struct HealthPoints(pub u32);

/// Character skill points.
#[derive(
    derive_more::Add,
    derive_more::AddAssign,
    derive_more::Sub,
    derive_more::SubAssign,
    derive_more::Display,
    derive_more::From,
    Clone,
    Copy,
    PartialEq,
    Eq,
    PartialOrd,
    Ord,
    Hash,
)]
pub struct SkillPoints(pub u32);
```

</details>

<details>

<summary>Reduction level 2 -- `proc_macro_attribute`</summary>

```rust,ignore
use numeric_newtype_derive::numeric_newtype;

/// Character health points.
#[numeric_newtype]
pub struct HealthPoints(pub u32);

/// Character skill points.
#[numeric_newtype]
pub struct SkillPoints(pub u32);
```

</details>
