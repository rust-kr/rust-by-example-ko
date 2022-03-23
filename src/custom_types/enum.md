# 열거형

`enum` 키워드를 사용하면 몇 가지 variant(열거형의 요소) 중 하나의 값이 되는 타입을 만들 수 있습니다. 구조체로 유효한 모든 variant는 열거형으로도 사용될 수 있습니다.

```rust,editable
// 웹 이벤트를 분류하는 열거형을 만듭니다. 이름과 타입 정보가 어떻게 열거형의 요소를 명시할 수 있는지 다음을 통해 알아보세요.
// `PageLoad != PageUnload`와 `KeyPress(char) != Paste(String)`.
// 이 둘은 서로 다르고 독립적입니다.
enum WebEvent {
    // 열거형은 유사 유닛(unit-like) 형식일 수 있습니다.
    PageLoad,
    PageUnload,
    // like tuple structs,
    // 튜플 구조체나,
    KeyPress(char),
    Paste(String),
    // C언어다운 구조가 그 예입니다. 
    Click { x: i64, y: i64 },
}

// `WebEvent`열거형을 인자로 받고, 아무것도 반환하지 않는 함수를 정의합니다.
fn inspect(event: WebEvent) {
    match event {
        WebEvent::PageLoad => println!("page loaded"),
        WebEvent::PageUnload => println!("page unloaded"),
        // 열거형 내부에서`c`를 비구조화(Destructuring)합니다.
        WebEvent::KeyPress(c) => println!("pressed '{}'.", c),
        WebEvent::Paste(s) => println!("pasted \"{}\".", s),
        // `Click`을 `x`와 `y`로 비구조화합니다.
        WebEvent::Click { x, y } => {
            println!("clicked at x={}, y={}.", x, y);
        },
    }
}

fn main() {
    let pressed = WebEvent::KeyPress('x');
    // `to_owned()`메소드는 스트링 슬라이스를 인자로 받아 소유권이 있는 `String`을 생성합니다.
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

## Type aliases

If you use a type alias, you can refer to each enum variant via its alias.
This might be useful if the enum's name is too long or too generic, and you
want to rename it.

```rust,editable
enum VeryVerboseEnumOfThingsToDoWithNumbers {
    Add,
    Subtract,
}

// Creates a type alias
type Operations = VeryVerboseEnumOfThingsToDoWithNumbers;

fn main() {
    // We can refer to each variant via its alias, not its long and inconvenient
    // name.
    let x = Operations::Add;
}
```

The most common place you'll see this is in `impl` blocks using the `Self` alias.

```rust,editable
enum VeryVerboseEnumOfThingsToDoWithNumbers {
    Add,
    Subtract,
}

impl VeryVerboseEnumOfThingsToDoWithNumbers {
    fn run(&self, x: i32, y: i32) -> i32 {
        match self {
            Self::Add => x + y,
            Self::Subtract => x - y,
        }
    }
}
```

To learn more about enums and type aliases, you can read the
[stabilization report][aliasreport] from when this feature was stabilized into
Rust.

### 참고

[`match`][match], [`fn`][fn], [`String`][str], ["Type alias enum variants" RFC][type_alias_rfc]

[c_struct]: https://en.wikipedia.org/wiki/Struct_(C_programming_language)
[match]: ../flow_control/match.md
[fn]: ../fn.md
[str]: ../std/str.md
[aliasreport]: https://github.com/rust-lang/rust/pull/61682/#issuecomment-502472847
[type_alias_rfc]: https://rust-lang.github.io/rfcs/2338-type-alias-enum-variants.html
