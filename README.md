# rust-throttle_timer
Throttle events and record event stats with a simple library

[![Build Status](https://travis-ci.org/benjaminmcdonald/rust-throttle_timer.svg?branch=master)](https://travis-ci.org/benjaminmcdonald/rust-throttle_timer) [![Coverage Status](https://coveralls.io/repos/github/benjaminmcdonald/rust-throttle_timer/badge.svg?branch=master)](https://coveralls.io/github/benjaminmcdonald/rust-throttle_timer?branch=master)

```rust
use std::time::Duration;

let mut break_timer: ThrottleTimer = ThrottleTimer::new(Duration::from_secs(1_u64), &"Break");
let do_break_flag = break_timer.do_run();

// Timers always run when no previous runs
assert!(do_break_flag == true);
if do_break_flag {
    println!("timer do run flag is set to true")
}

// Run flag false as no time has passed
assert!(break_timer.do_run() == false);
```


Repo:
https://github.com/benjaminmcdonald/rust-throttle_timer
