# Machine Info

Get information about your machine and monitor the resources usage.


[![Crates.io][crates-badge]][crates-url]
[![Apache 2 licensed][apache-badge]][apache-url]

[crates-badge]: https://img.shields.io/crates/v/machine-info.svg
[crates-url]: https://crates.io/crates/machine-info
[apache-badge]: https://img.shields.io/badge/license-apache2-blue.svg
[apache-url]: https://github.com/wixet-limited/machine-info-rs/blob/master/LICENSE

[Website](https://wixet.com) |
[API Docs](https://docs.rs/machine-info/latest/machine-info)

## Overview

There are many crates to get information about your system. We actually are using some
of them but this crate adds a feature to constantly monitor the system without a big
overhead. 

You can probe your system for CPU or memory usage once per second and your machine performance will not be affected at all. Other crates consumed like 7-10% of CPU which
is not acceptable. But to be fair, these other creates are doing many other things apart from getting the cpu/memory usage.

This crate focus only on this, nothing else. Limited but lightweight. If you want a full featured crate better use other one.

## Example

Just a simple monitoring

```toml
[dependencies]
machine-info = "1.0.0"
```
Put this in your main.rs:

```rust
use machine_info::Machine;
use anyhow::Result;

use std::{thread, time};


fn main() -> Result<()> {
    let mut m = Machine::new();
    // Please use a real PIDs!
    m.track_process(132801)?;
    m.track_process(32930)?;
    
    for _ in 1..100 {
        let processes = m.processes_status();
        let system = m.system_status();
        let graphics = m.graphics_status();
        println!("{:?} {:?} {:?}", processes, system, graphics);
        
        thread::sleep(time::Duration::from_millis(1000));
    }

    Ok(())
}


```


## Related Projects

In addition to the crates in this repository, the Tokio project also maintains
several other libraries, including:

* [`sysinfo`]: sysinfo is a crate used to get a system’s information.
* [`nvml-wrapper`]: A safe and ergonomic Rust wrapper for the NVIDIA Management Library (NVML)


[`sysinfo`]: https://github.com/GuillaumeGomez/sysinfo
[`nvml-wrapper`]: https://github.com/Cldfire/nvml-wrapper


## License

This project is licensed under the [Apache 2 license].

[Apache 2 license]: https://github.com/wixet-limited/machine-info-rs/blob/master/LICENSE
