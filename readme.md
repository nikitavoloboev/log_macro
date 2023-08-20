# log_macro [<img alt="crates.io" src="https://img.shields.io/crates/v/log_macro.svg?style=for-the-badge&color=fc8d62&logo=rust" height="20">](https://crates.io/crates/log_macro)

> Macro to print variable name and value only (stripped from release builds)

## Install

```
cargo add log_macro
```

## Use

Add this to top of file:

```rust
#[macro_use]
extern crate log_macro;
```

Then use like so:

```rust
let animals = vec!["cat", "dog", "horse", "zebra"];
let set: std::collections::HashSet<_> = animals.into_iter().collect();
log!(set);
```

Will print:

```
set: {"horse", "dog", "zebra", "cat"}
```
