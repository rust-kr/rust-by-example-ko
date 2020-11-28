# 디버그

어떤 자료형이든 `std::fmt`의 형식 지정자를 사용하려면 출력 기능을
구현해야 합니다. 표준(`std`) 라이브러리의 자료형들은 자동으로 구현이 되어
있지만, 다른 자료형의 경우에는 *반드시* 직접 구현해야만 합니다.

`std::fmt` 의 트레잇들 중 `fmt::Debug` 을 구현하는 것은 그다지 어렵지
않습니다. *모든* 자료형은 `fmt::Debug` 을 파생 구현(`derive`) 할 수 있습니다.

```rust
// 아래 구조체는 fmt::Display 나 fmt::Display 둘 중 어느것으로도 출력할 수 없습니다.
struct UnPrintable(i32);

// derive 속성을 사용하면 fmt::Debug으로 구조체를 출력할 수 있는 코드가 파생 구현됩니다.
#[derive(Debug)]
struct DebugPrintable(i32);
```

또한 모든 `표준(std) 라이브러리`의 자료형들은 `{:?}` 으로 출력이 가능합니다.

```rust,editable
// Structure 구조체를 위해 fmt::Debug를 파생 구현합니다. 
// 이 구조체는 i32 한개만 가지고 있습니다.
#[derive(Debug)]
struct Structure(i32);

// 구조체 Deep의 내부에 Structure를 넣습니다. 역시 출력가능하게 만듭니다.
#[derive(Debug)]
struct Deep(Structure);

fn main() {
    // {:?}는  {}와 비슷하게 동작합니다.
    println!("1년에는 {:?}개월이 있다.", 12);
    println!("{1:?} {0:?}는 {actor:?} 이름이다.",
             "강호",
             "송",
             actor="배우의");

    // Structure 도 출력할 수 있습니다!
    println!("이번에는 {:?} 를 출력하자!", Structure(3));
    
    // 파생 구현(derive)의 단점은 출력 방식을 제어할 수 없다는 것입니다.
    // 다음 코드에서 7 만 출력되게 하려면 어찌해야 할까요.
    println!("이번에는 {:?} 를 출력하자!", Deep(Structure(7)));
}
```

즉 `fmt::Debug` 는 출력은 할 수 있게 해주지만, 우아함은 포기해야합니다.
러스트에는 `{:#?}`를 이용한 "예쁘게 출력하기" 기능도 있습니다.

```rust,editable
#[derive(Debug)]
struct Person<'a> {
    name: &'a str,
    age: u8
}

fn main() {
    let name = "Peter";
    let age = 27;
    let peter = Person { name, age };

    // 예쁘게 출력하기
    println!("{:#?}", peter);
}
```

출력 형식을 바꾸려면 `fmt::Display` 를 직접 구현해야만 합니다.

### 참고:

[`속성(attributes)`][attributes], [`파생 구현(derive)`][derive], [`std::fmt`][fmt],
 [`구조체(struct)`][structs]

[attributes]: https://doc.rust-lang.org/reference/attributes.html
[derive]: ../../trait/derive.md
[fmt]: https://doc.rust-lang.org/std/fmt/
[structs]: ../../custom_types/structs.md

