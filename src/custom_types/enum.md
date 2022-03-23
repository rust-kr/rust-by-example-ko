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

## 타입 별칭

타입 별칭(alias)을 사용하면, 열거형의 모든 variant를 별칭으로 참조할 수 있습니다.
열거형의 이름이 너무 길거나 일반적이고 이름을 변경하고 싶다면 타입 별칭이 유용할 수 있습니다. 

```rust,editable
enum VeryVerboseEnumOfThingsToDoWithNumbers {
    Add,
    Subtract,
}

// 타입 별칭을 만듭니다.
type Operations = VeryVerboseEnumOfThingsToDoWithNumbers;

fn main() {
    // 이제 길고 불편한 이름을 사용하지 않고, 각각의 variant를 별칭을 통해 참조할 수 있습니다.
    let x = Operations::Add;
}
```

타입 별칭을 가장 흔히 보시게 될 곳은 `Self` 별칭을 사용한 `impl`블록일 것입니다.

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

타입 별칭에 대해 더 자세히 알아보려면, 이 기능이 Rust로 안정되었을 때의 [안정화 보고서][aliasreport]를 참고하세요.

### 참고

[`match`][match], [`fn`][fn], [`String`][str], ["Type alias enum variants" RFC][type_alias_rfc]

[c_struct]: https://en.wikipedia.org/wiki/Struct_(C_programming_language)
[match]: ../flow_control/match.md
[fn]: ../fn.md
[str]: ../std/str.md
[aliasreport]: https://github.com/rust-lang/rust/pull/61682/#issuecomment-502472847
[type_alias_rfc]: https://rust-lang.github.io/rfcs/2338-type-alias-enum-variants.html
