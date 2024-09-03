[[Tools/Python/IP_List_Gen|IP_List_Gen]]

```rust
use rand::Rng;
use std::fs::File;
use std::io::{self, Write};

fn generate_random_ip() -> String {
    let mut rng = rand::thread_rng();
    format!(
        "{}.{}.{}.{}",
        rng.gen_range(1..=255),
        rng.gen_range(0..=255),
        rng.gen_range(0..=255),
        rng.gen_range(1..=255)
    )
}

fn main() -> io::Result<()> {
    let filename = "ips.txt";
    let mut file = File::create(filename)?;

    for _ in 0..25000 {
        let ip = generate_random_ip();
        writeln!(file, "{}", ip)?;
    }

    println!("Successfully wrote 25,000 IPs to '{}'.", filename);
    Ok(())
}

```

```bash
cargo new generate_ips --bin
cd generate_ips
# Replace the main.rs content with the above Rust script
cargo run
```