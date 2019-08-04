# rustflake

Thread-safe "twitter" snowflakes.

By default the original Twitter snowflake format defines:
- 41 bits are used to store a custom epoch with millisecond precision
- 10 bits are used to store worker and datacenter information
- 12 bits are used to store a sequence number

This crate lets you customize your own epoch and worker/datacenter information.

## Usage
Add this to your `Cargo.toml`:

```toml
[dependencies]
rustflake = "0.1.0"
```

and this to your crate root:

```rs
use rustflake;
```

## Example

```rs
use rustflake::Snowflake;

fn main() {
    let mut snowflake = Snowflake::default();
    println!("{}", &snowflake.generate());
}
```

```rs
use rustflake::Snowflake;

fn main() {
    // Discord Epoch
    // Though those are not "real" discord Ids,
    // because discord increases the sequence
    // for *every* generated Id on that process
    let mut snowflake = Snowflake::new(1420070400000, 1, 1);
    println!("{}", &snowflake.generate());
}
```

```rs
use rustflake::Snowflake;

fn main() {
    // Using a builder approach
    let mut snowflake = Snowflake::default()
        .epoch(1_564_790_400_000)
        .worker_id(2)
        .datacenter_id(3);
    println!("{}", &snowflake.generate());
}
```
