# log_macro [<img alt="crates.io" src="https://img.shields.io/crates/v/log_macro.svg?style=for-the-badge&color=fc8d62&logo=rust" height="20">](https://crates.io/crates/log_macro) [<img alt="docs.rs" src="https://img.shields.io/badge/docs.rs-log_macro-66c2a5?style=for-the-badge&labelColor=555555&logo=docs.rs" height="20">](https://docs.rs/log_macro)

> Macro to print variable(s) with values nicely (stripped from release builds)

## Install

```
cargo add log_macro
```

## Use

Add this to top of file:

```rust
use log_macro::log;
```

Possible uses and outputs:

```rust
// print string only
log!("hello"); // -> hello

// print variable
let animals = vec!["cat", "dog"];
log!(animals); // -> animals: ["cat", "dog"]

// print multiple variables
let animals = vec!["cat", "dog"];
let fish = vec!["salmon", "tuna"];
log!(animals, fish);
// each variable logged on new line
// -> animals: ["cat", "dog"]
// -> fish: ["salmon", "tuna"]
```

Variables will be in green color to stand out.

## Implementation

Exported macro code is in [src/lib.rs](src/lib.rs):

```rust
#[macro_export]
macro_rules! log {
    // Single literal string case
    ( $val:expr $(,)? ) => {{
        #[cfg(debug_assertions)]
        {
            if ::std::stringify!($val).starts_with("\"") {
                // Remove quotes for string literals
                ::std::eprintln!("{}", ::std::stringify!($val).trim_matches('\"'));
            } else {
                // Print using a reference to avoid moving the value
                ::std::eprintln!("\x1B[32m{}\x1B[0m: {:?}", ::std::stringify!($val), &$val);
            }
        }
    }};

    // Multiple variables case
    ( $($val:expr),+ $(,)? ) => {{
        #[cfg(debug_assertions)]
        {
            $(
                $crate::log!($val);
            )+
        }
    }};
}
```

## Run

Will run tests in [src/lib.rs](src/lib.rs).

```
cargo watch -q -- sh -c "tput reset && cargo test -q --lib"
```

## Contributing

Always open to useful ideas or fixes in form of issues or PRs.

Can [open new issue](../../issues/new/choose) (search [existing ones](../../issues) for duplicates first) or start discussion on [GitHub](../../discussions) or [Discord](https://discord.com/invite/TVafwaD23d).

Can submit draft PRs with good ideas/fixes. You will get help along the way to make it merge ready.

Ask for help if you're stuck. You will be unblocked fast.

[![Discord](https://go.nikiv.dev/badge-discord)](https://go.nikiv.dev/discord) [![X](https://go.nikiv.dev/badge-x)](https://x.com/nikitavoloboev) [![nikiv.dev](https://go.nikiv.dev/badge-nikiv)](https://nikiv.dev)
