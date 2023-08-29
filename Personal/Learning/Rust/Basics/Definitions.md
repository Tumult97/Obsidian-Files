
## Macro

> Fundamentally, macros are a way of writing code that writes other code, which is known as _metaprogramming_.  

### Definition

```rust
#[macro_export]
macro_rules! vec {
    ( $( $x:expr ),* ) => {
        {
            let mut temp_vec = Vec::new();
            $(
                temp_vec.push($x);
            )*
            temp_vec
        }
    };
}
```


### Call

```rust
let v: Vec<u32> = vec![1, 2, 3];
```
