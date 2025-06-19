```rust
use std::io;
use std::process::{Command, Stdio};

fn main() -> io::Result<()> {
    // Create the command to run cmd.exe
    let mut child = Command::new("cmd.exe")
        .stdin(Stdio::inherit())   // Hook up standard input
        .stdout(Stdio::inherit())  // Hook up standard output
        .stderr(Stdio::inherit())  // Hook up standard error
        .spawn()?;                 // Start the process

    // Wait for the process to exit
    let status = child.wait()?;

    if status.success() {
        println!("cmd.exe has exited.");
    } else {
        eprintln!("cmd.exe exited with error: {}", status);
    }

    Ok(())
}

```