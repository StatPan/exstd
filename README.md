# exstd

`exstd` is a Rust library that provides a set of commonly used extensions for the Rust standard library. It includes a variety of popular crates that cover essential functionalities such as serialization, asynchronous programming, HTTP requests, logging, error handling, and more.

## Features

- **Serialization**: Easily serialize and deserialize data with `serde` and `serde_json`, `serde_yaml`.
- **Asynchronous Programming**: Utilize `tokio` for asynchronous programming.
- **HTTP Requests**: Perform HTTP requests with `reqwest`.
- **Logging**: Implement logging with `log` and `env_logger`.
- **Date and Time**: Work with dates and times using `chrono`.
- **Regular Expressions**: Use regular expressions with `regex`.
- **Command Line Interface**: Parse command line arguments with `clap`.
- **Environment Variables**: Manage environment variables with `dotenv`.

## Installation

Add `exstd` to your `Cargo.toml`:

```toml
[dependencies]
exstd = "0.1.2"
```

## Usage

Here's an example of how to use exstd in your project:

```rust
extern crate exstd;

use exstd::serde::{Serialize, Deserialize};
use exstd::tokio::main as tokio_main;
use exstd::reqwest::get;
use log::info;
use anyhow::Result;

#[derive(Serialize, Deserialize, Debug)]
struct MyStruct {
    name: String,
    age: u32,
}

#[tokio_main]
async fn main() -> Result<()> {
    env_logger::init();

    let my_struct = MyStruct {
        name: "John Doe".to_string(),
        age: 30,
    };

    let json = serde_json::to_string(&my_struct)?;
    info!("Serialized JSON: {}", json);

    let response = get("https://httpbin.org/get").await?.text().await?;
    info!("HTTP GET Response: {}", response);

    Ok(())
}

```