---
title: Rust
description: A language empowering everyone to build reliable and efficient software.
published: true
date: 2021-03-03T21:40:08.729Z
tags: rust, language, programmi
editor: markdown
dateCreated: 2021-03-03T19:40:40.140Z
---


![1200px-rust_programming_language_black_logo.svg[1].png](/1200px-rust_programming_language_black_logo.svg[1].png =125x125){.align-left}
Rust is a multi-paradigm programming language **designed for performance and safety**, especially safe concurrency. 
Rust is syntactically similar to C++, but can **guarantee memory safety** by using a borrow checker to validate references. 
Rust was originally designed by *Graydon Hoare* at **Mozilla** Research


---
# Cargo
Cargo is the packages manager of `Rust`, it uses `'crates'` as libraries.
Cargo also build automatically your project folder structure.

## Commands
Cargo uses the following commands:
1.  build command:
```bash
cargo build # this uses the cargo.toml file
```
2. New - creating new folder structure in `{name}` folder:
```bash
cargo new {name} # name of existence
# option:
# --bin Use a binary (application) template [default]
```
3. Run command, this will compile at runtime:
```bash
cargo run ## this runs your (un)compiled code
```
---

## cargo.toml

`cargo.toml` is the main configuration file.
This files i written in toml syntax and contains application information.

Example:
```toml
name = "hello_world"
version = "0.1.0"
authors = ["John Doe <j.doe@proton.com>"]
edition = "1"
```

> See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html
{.is-success}


---
# Basic
Exploring Rust building some basics.
Explanations are mostly in the code as comment

## Function

```rust
fn main() {
    // 'let' declaring a variable
    // 'a' the variable name - location in memory
    // ':' splitting sign between variable name and the type
    // 'u' stands for 'unsigned integer' and has always the value: null(0) or positive(+)
    // '8' is 8 bits (single byte)
    
    let a:u8 = 123;
    println!("a = {}", a);
    // a = 456; / Error: cannot assign twice to immutable variable

    //// Making it mutable
    // 'let' declaring a variable
    // 'mut' making it mutable
    // 'b' the variable name - location in memory
    // ':' splitting sign between variable name and the type
    // 'i' integer 64bit memory
    // '8' 8 bits (single byte) 
    let mut b:i8 = 0;
    println!("b = {}", b);
    b = 42;
    println!("b = {}", b);

    // 
}

```