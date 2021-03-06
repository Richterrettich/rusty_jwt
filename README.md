Rusty JWT
================================================
[![Build Status](https://travis-ci.org/Richterrettich/rusty_jwt.svg?branch=master)](https://travis-ci.org/Richterrettich/rusty_jwt)

This is an active fork of https://github.com/GildedHonour/frank_jwt


Implementation of [JSON Web Tokens](http://jwt.io) in Rust.

## Algorithms and features supported
- [x] HS256
- [x] HS384
- [x] HS512
- [x] RS256
- [x] RS384
- [x] RS512
- [x] ES256
- [x] ES384
- [x] ES512
- [x] Sign
- [x] Verify
- [x] iss (issuer) check
- [x] sub (subject) check
- [x] aud (audience) check
- [x] exp (expiration time) check
- [x] nbf (not before time) check
- [x] iat (issued at) check
- [x] jti (JWT id) check

## Usage

Put this into your `Cargo.toml`:

```toml
[dependencies]
rusty_jwt = "<current version of frank_jwt>"
```

And this in your crate root:

```rust
extern crate rusty_jwt;

use rusty_jwt::{Header, Payload, Algorithm, encode, decode};
```

## Example

```rust
//HS256
let mut payload = Payload::new();
payload.insert("key1".to_string(), "val1".to_string());
payload.insert("key2".to_string(), "val2".to_string());
let header = Header::new(Algorithm::HS256);
let secret = "secret123";

let jwt = encode(header, secret.to_string(), payload.clone());

//public key signatures:

use std::fs::File;
use std::io::Read;

let mut payload = Payload::new();
payload.insert("key1".to_string(), "val1".to_string());
payload.insert("key2".to_string(), "val2".to_string());
let header = Header::new(Algorithm::RS256);


let public_key_path = //... path to your public key, needs to be pem formated.
let mut key_file = File::open(private_key_path).expect("Unable to open private key file");
let mut key_pem: Vec<u8> = Vec::new();
file.read_to_end(&mut key_pem).expect("Unable to read pem from file");

let jwt = encode(header, key_pem, payload);
```

## License

Apache 2.0

## Tests

```shell
cargo test
```
