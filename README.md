# str_tools

`str_tools` is a Rust library that provides zero copy string iterators for working with string slices. The library offers iterators similar to standard Rust string methods such as `lines`, `split_whitespace`, and `split`, but returns references to the original string without allocating new memory. This makes it efficient for large strings or performance critical applications.  

## Features

* StrLines – iterate over lines in a string  
* StrWords – iterate over words separated by whitespace  
* StrSplitN – split a string by a delimiter with a maximum number of splits  
* StrRSplit – split a string in reverse order  
* StrMatches – iterate over all occurrences of a substring  

All iterators are zero copy and use lifetimes to reference the original string safely.  

## Installation

To use `str_tools` locally, add the path to your `Cargo.toml` dependencies:

```toml
[dependencies]
str_tools = { path = "../str_tools" }
```

## Usage

```rust
use str_tools::*;

fn main() {
    let text = "hello world\nRust is efficient\nzero copy iterators";

    for word in StrLines::new(text).flat_map(StrWords::new) {
        println!("{}", word);
    }

    let s = "a,b,c,d,e";
    let mut iter = StrSplitN::new(s, ",", 3);
    for part in iter {
        println!("{}", part);
    }

    let path = "a/b/c/d";
    for part in StrRSplit::new(path, "/") {
        println!("{}", part);
    }

    let text = "banana";
    for m in StrMatches::new(text, "an") {
        println!("{}", m);
    }
}
```

## Testing

```rust
cargo test 
```
