# Rust throttle_timer
Simple Rust library to throttle events and record event stats

[![Docs](https://docs.rs/throttle-timer/badge.svg)](https://docs.rs/throttle-timer)
[![Build Status](https://travis-ci.org/benjaminmcdonald/rust-throttle_timer.svg?branch=master)](https://travis-ci.org/benjaminmcdonald/rust-throttle_timer)
[![Coverage Status](https://coveralls.io/repos/github/benjaminmcdonald/rust-throttle_timer/badge.svg?branch=master)](https://coveralls.io/github/benjaminmcdonald/rust-throttle_timer?branch=master)
[![Current Crates.io Version](https://img.shields.io/crates/v/throttle-timer.svg)](https://crates.io/crates/throttle-timer)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/rust-lang/docs.rs/master/LICENSE)


## Install Cargo.toml
```
throttle-timer = "1.0.0"
```

## Example use
```rust
use std::time::Duration;
use throttle_timer::ThrottleTimer;

let mut throttled_fn = ThrottleTimer::new(Duration::from_secs(10_u64), &"throttled_fn");
let mut val = 0_u8;

// timers always run when no previous runs
throttled_fn.run(&mut || val += 1);
for _ in 0..100 {
    // timer will not run as 10 secs has not passed
    // do run will return false
    throttled_fn.run(&mut || val += 1);
}

throttled_fn.print_stats();
// throttled_fn called 0/sec, total calls 1, has been running for 10us

assert_eq!(throttled_fn.total_calls(), &1);
assert_eq!(val, 1_u8);
```