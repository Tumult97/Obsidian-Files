
```toc
```


## Println

```rust
println!("The value of x is invalid");
//println is a macro indicated by the ! in teh mathod call
```


## If-else

```rust
let n = 45;

if n < 30 {
	println!("The value of x is: {}", n);
}

else {
	println!("The value of x is invalid");
}
```


## Variable assignment

- [k] Variables are *immutable* and cant be reasssigned and changed by default
```rust
let x = 45;
```

- [k] To ammend this when a variable need to be able to chnage value youi declare it as such
```rust
let mut x = 85;
x = 65;
```




## Loops

### Infinite loop

```rust
fn main() {
    let mut n = 0;

    loop {
        println!("{}", n);
        n += 1;
    }
}
```

### While loop

```rust
fn main() {
    let mut x = 0;

    while x <= 1000000 {
        println!("{}", x);
        x += 1;
    }
}
```



### For loop

```rust 
let start = 0;
let end = 1000; 

for i in start..end {
	println!("{}", i);
}
```
## Enums

```rust 
enum Direction {
    Up,
    Down,
    Left,
    Right
}

fn main() {

    let mut x: Direction = Direction::Up;

    match x {
        Direction::Up => println!("The player is heading up!"),
        Direction::Down => println!("The player is heading down!"),
        Direction::Left => println!("The player is heading upleft!"),
        Direction::Right => println!("The player is heading right!")
    }
    
}
```