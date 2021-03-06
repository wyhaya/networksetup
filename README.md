
# networksetup [![Crates.io](https://img.shields.io/crates/v/networksetup.svg?style=flat-square)](https://crates.io/crates/networksetup)

A rust library for setting up `macOS` networks by calling `networksetup` command

[API Docs](https://docs.rs/networksetup/*/networksetup/)

 ## Usage

Add this in your `Cargo.toml`:

```toml
[dependencies]
networksetup = "*"
```

## Example
 
```rust
use networksetup::{auto_proxy, dns_server, web_proxy, Address, Config, Network};

fn main() {
    // Set PAC Automatic Proxy
    auto_proxy(
        Network::WiFi,
        Config::Value("https://example.com/proxy.pac"),
    );

    // Set HTTP Proxy
    let addr = Address::new("0.0.0.0", "80");
    web_proxy(Network::WiFi, Config::Value(&addr));

    // Set Socks Proxy
    let addr = Address::new("127.0.0.1", "1080");
    web_proxy(Network::Ethernet, Config::Value(&addr));
    // Close
    web_proxy(Network::Ethernet, Config::Off);

    // Set DNS Server
    dns_server(Network::WiFi, &vec!["1.1.1.1", "8.8.8.8"]);
}
```
