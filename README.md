# Copy-on-write string utils for Rust

Some [`str`](https://doc.rust-lang.org/std/primitive.str.html) methods
perform destructive transformations and so they allocate, copy into and
return a new
[`String`](https://doc.rust-lang.org/std/string/struct.String.html) even
when no modification is necessary.

This crate provides a helper trait `CowUtils` with drop-in variants of
such methods, which behave in the same way, but avoid extra copies and
allocations when no modification is necessary.

For now it's only implemented for `&str` and returns
[`std::borrow::Cow<str>`](https://doc.rust-lang.org/std/borrow/enum.Cow.html),
but in the future might be extended to other types where even more
efficient handling is possible (e.g. in-place modifications on mutable
strings).

## Usage

First, you need to import `CowUtils` into the scope:

```rust
use cow_utils::CowUtils;
```

Then you can start invoking following `.cow_`-prefixed methods on
strings instead of the regular ones:

- `.cow_replace` instead of [`str::replace`](https://doc.rust-lang.org/std/primitive.str.html#method.replace)
- `.cow_replacen` instead of [`str::replacen`](https://doc.rust-lang.org/std/primitive.str.html#method.replacen)
- `.cow_to_ascii_lowercase` instead of [`str::to_ascii_lowercase`](https://doc.rust-lang.org/std/primitive.str.html#method.to_ascii_lowercase)
- `.cow_to_ascii_uppercase` instead of [`str::to_ascii_uppercase`](https://doc.rust-lang.org/std/primitive.str.html#method.to_ascii_uppercase)
- `.cow_to_lowercase` instead of [`str::to_lowercase`](https://doc.rust-lang.org/std/primitive.str.html#method.to_lowercase)
- `.cow_to_uppercase` instead of [`str::to_uppercase`](https://doc.rust-lang.org/std/primitive.str.html#method.to_uppercase)

Check out the docs for detailed examples.

## License

MIT
