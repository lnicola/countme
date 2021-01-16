A library to quickly get the live/total/max counts of allocated instances.

```rust
#[derive(Default)]
struct Widget {
  _t: countme::Token<Self>,
}

impl countme::CountMe for Widget {
    fn store() -> &'static countme::Store {
        static S: countme::Store = countme::Store::new();
        &S
    }
}

let w1 = Widget::default();
let w2 = Widget::default();
let w3 = Widget::default();
drop(w1);

let counts = countme::get::<Widget>();
assert_eq!(counts.live, 2);
assert_eq!(counts.max, 3);
assert_eq!(counts.total, 3);
```
