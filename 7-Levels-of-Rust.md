# 7 Levels of Rust

(Source: Instagram @itsnextwork)

## Level 1: Ownership

Every value in Rust has one owner. Rust frees it the instant that owner leaves
scope, replacing a garbage collector with a check the compiler runs before your
code ever reaches production.

Use it for

- catch bugs at compile time
- skip manual free calls
- trust every reference

```rust
let s1 = String::from("rust");
let s2 = s1;

println!("{}", s1);
// error: value borrowed after move
```

## Level 2: Borrowing

Borrowing lets you use a value through a reference without owning it.
Rust allows `many readers` at once, or exactly `one writer`,
never both at the same time.

```
+---------------+
| value: String |
+---------------+
        ↓
many shared readers
+--------------+
| v1 = &value; |
| v2 = &value; |
+--------------+
       (OR)
exactly one writer
+------------------+
| v3 = &mut value; |
+------------------+
```

## Level 3: Enums

An `enum` defines a type as one of several named variants, and Rust's `match`
keyword forces you to handle every variant before code will compile.

```rust
enum Coin {
  Penny,
  Nickel,
  Dime,
  Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
  match coin {
    Coin:Penny => 1,
    Coin:Nickel => 3,
    Coin:Dime => 10,
    Coin:Quarter => 25,
  }
}
```

```rust
// Create an `enum` to classify a web event. Note how both
// names and type information together specify the variant:
// `PageLoad != PageUnload` and `KeyPress(char) != Paste(String)`.
// Each is different and independent.
enum WebEvent {
    // An `enum` variant may either be `unit-like`,
    PageLoad,
    PageUnload,
    // like tuple structs,
    KeyPress(char),
    Paste(String),
    // or c-like structures.
    Click { x: i64, y: i64 },
}

// A function which takes a `WebEvent` enum as an argument and
// returns nothing.
fn inspect(event: WebEvent) {
    match event {
        WebEvent::PageLoad => println!("page loaded"),
        WebEvent::PageUnload => println!("page unloaded"),
        // Destructure `c` from inside the `enum` variant.
        WebEvent::KeyPress(c) => println!("pressed '{}'.", c),
        WebEvent::Paste(s) => println!("pasted \"{}\".", s),
        // Destructure `Click` into `x` and `y`.
        WebEvent::Click { x, y } => {
            println!("clicked at x={}, y={}.", x, y);
        },
    }
}

fn main() {
    let pressed = WebEvent::KeyPress('x');
    // `to_owned()` creates an owned `String` from a string slice.
    let pasted  = WebEvent::Paste("my text".to_owned());
    let click   = WebEvent::Click { x: 20, y: 80 };
    let load    = WebEvent::PageLoad;
    let unload  = WebEvent::PageUnload;

    inspect(pressed);
    inspect(pasted);
    inspect(click);
    inspect(load);
    inspect(unload);
}
```

Use it for:

- model a payment status
- replace null with a real type

## Level 4: Result

Rust has no exceptions. A function that can fail returns a Result, and the compiler
refuses to build until you handle both the `Ok(T)` and the `Err(T)` case.

```rust
fn read_config() -> Result<String, Error> {
  let text = fs::read_to_string("config.toml")?;
  Ok(text)
}
```

```rust
use std::num::ParseIntError;

fn main() -> Result<(), ParseIntError> {
    let number_str = "10";
    let number = match number_str.parse::<i32>() {
        Ok(number)  => number,
        Err(e) => return Err(e),
    };
    println!("{}", number);
    Ok(())
}
```

Use it for:

- handle a failed file read
- surface a bad network response

## Level 5: Traits

A trait defines the behaviour that many different types can share. Generics reuse
that behaviour across every type without ever slowing your program down.

```rust
struct Sheep { naked: bool, name: &'static str }

trait Animal {
    // Associated function signature; `Self` refers to the implementor type.
    fn new(name: &'static str) -> Self;

    // Method signatures; these will return a string.
    fn name(&self) -> &'static str;
    fn noise(&self) -> &'static str;

    // Traits can provide default method definitions.
    fn talk(&self) {
        println!("{} says {}", self.name(), self.noise());
    }
}

impl Sheep {
    fn is_naked(&self) -> bool {
        self.naked
    }

    fn shear(&mut self) {
        if self.is_naked() {
            // Implementor methods can use the implementor's trait methods.
            println!("{} is already naked...", self.name());
        } else {
            println!("{} gets a haircut!", self.name);

            self.naked = true;
        }
    }
}

// Implement the `Animal` trait for `Sheep`.
impl Animal for Sheep {
    // `Self` is the implementor type: `Sheep`.
    fn new(name: &'static str) -> Sheep {
        Sheep { name: name, naked: false }
    }

    fn name(&self) -> &'static str {
        self.name
    }

    fn noise(&self) -> &'static str {
        if self.is_naked() {
            "baaaaah?"
        } else {
            "baaaaah!"
        }
    }

    // Default trait methods can be overridden.
    fn talk(&self) {
        // For example, we can add some quiet contemplation.
        println!("{} pauses briefly... {}", self.name, self.noise());
    }
}

fn main() {
    // Type annotation is necessary in this case.
    let mut dolly: Sheep = Animal::new("Dolly");
    // TODO ^ Try removing the type annotations.

    dolly.talk();
    dolly.shear();
    dolly.talk();
}
```

## Level 6: Async

Rust runs real OS threads for heavy work and an async runtime like Tokio for thousands
of waiting connections, and the compiler still blocks a data race before it runs.

tags: `std::thread`, `tokio`

## Level 7: Unsafe

Unsafe Rust lets you dereference a raw pointer, call C code directly, or write
your own operating system kernel. It is the level 99% of developers never actually
reach in practice.

Use it for:

- wrap a C library
- write a kernel driver
- shave off microseconds
