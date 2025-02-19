# rust_risc_v_cross_comp
Cross compilation and emulation of RISC-V Rust programs

## making obj files:
Compile with `cargo rustc -- --emit=obj` will emit `.o` files.

## Exposing Rust code:
You must use `#[no_mangle]` to not mangle the symbols when compiling and
then use the `extern "C"` prefix for the function to expose it as a C ABI.
```rs
#[no_mangle]
pub extern "C" fn rust_fn() -> () { }
```

## Cargo.TOML
If the crate is a library, one can define it as a static library in the `Cargo.toml`:
```toml
[lib]
crate-type = ["staticlib"]
```

This will compile the program to an archive file `.a` containing all the object files.
If we want to extract the object files, one can use `ar -x lib.a`. (see `C/Makefile`)

## Compiling C and Rust programs:
See the `C/Makefile`.

