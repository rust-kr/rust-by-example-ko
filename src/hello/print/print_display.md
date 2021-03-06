# Display

`fmt::Debug`의 출력은 별로 깔끔하지 않기 때문에, 출력 형태를 별도로 구현해야 하는
경우가 많습니다. 이때는 [`fmt::Display`][fmt] 트레잇을 구현하면 `{}` 마커로 
출력할 수 있습니다. 구현하는 방법은 다음과 같습니다.

```rust
// fmt 모듈을 사용하기 위해 use 키워드로 임포트합니다.
use std::fmt;

// fmt::Display 를 구현할 구조체입니다. Structure 라는 구조체에 한 개의 i32만 넣었습니다.
struct Structure(i32);

// {} 를 이용해 출력하려면 해당 자료영에 대해 fmt::Display 트레잇이 구현되어 있어야 합니다.
impl fmt::Display for Structure {
    // 이 트레잇에는 정확한 형식의 fmt 함수가 있어야 합니다.
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // 첫번째 요소를 출력 버퍼 f 에 씁니다.
        // 리턴값은 fmt::Result 인데, 동작의 성공 여부를 나타냅니다. 
        // write! 는 println! 과 유사한 문법을 사용합니다.
        write!(f, "{}", self.0)
    }
}
```

`fmt::Display` 를 쓰는 편이 `fmt::Debug` 의 경우 보다 더 깔끔합니다만, 
`표준(std) 라이브러리`에 구현하기에는 어려움이 있습니다. 출력 형식을 지정하기 애매한 자료형 때문입니다.
예를 들어, 표준 라이브러리에서 모든 `Vec<T>` 에 대해 출력방식을 구현한다면
어떤 식으로 해야 할까요? 다음 두가지 중에 어느쪽이 적절할까요?

* `Vec<path>`: `/:/etc:/home/username:/bin` (`:` 로 나눠서 표시하기)
* `Vec<number>`: `1,2,3` (`,` 로 나눠서 표시하기)

둘 다 안됩니다. 모든 자료형을 위한 이상적인 한가지 출력형식이란 있을 수 없고, 
표준라이브러리가 어떤 한가지 방식을 강제해서도 안되기 때문입니다. `fmt::Display` 는 
`Vec<T>` 나 다른 제네릭 컨테이너에 대해서는 구현되어있지 않습니다. 이런 경우에는 
`fmt::Debug`를 사용하면 됩니다.

이것이 큰 문제는 되지 않습니다. 제네릭이 *아닌* 모든 새로운 *컨테이너* 자료형은
 `fmt::Display`를 구현하면 되기 때문입니다.

```rust,editable
use std::fmt; // fmt를 임포트합니다.

// 숫자 두개를 가진 구조체입니다. Debug 파생 구현도 만들어서, Display 구현과
// 비교해봅시다.
#[derive(Debug)]
struct MinMax(i64, i64);

// MinMax 를 위한 Display 구현입니다.
impl fmt::Display for MinMax {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // self.number로 해당 위치의 데이터를 가리킵니다.
        write!(f, "({}, {})", self.0, self.1)
    }
}

// 비교를 위해 이름이 있는 필드들로 구조체를 만듭시다.
#[derive(Debug)]
struct Point2D {
    x: f64,
    y: f64,
}

// 역시 Point2D 의 Display 도 구현합니다.
impl fmt::Display for Point2D {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // x와 y만 표시하도록 합니다.
        write!(f, "x: {}, y: {}", self.x, self.y)
    }
}

fn main() {
    let minmax = MinMax(0, 14);

    println!("구조체의 출력을 비교해봅시다 :");
    println!("Display: {}", minmax);
    println!("Debug: {:?}", minmax);

    let big_range =   MinMax(-300, 300);
    let small_range = MinMax(-3, 3);

    println!("넓은 범위는 {big}이고, 좁은 범위는 {small}입니다.",
             small = small_range,
             big = big_range);

    let point = Point2D { x: 3.3, y: 7.2 };

    println!("포인트 구조체도 비교합시다 :");
    println!("Display: {}", point);
    println!("Debug: {:?}", point);

    // 다음 코드에서는 컴파일 오류가 납니다. Debug와 Display는 구현되었지만,
    // {:b}는 fmt::Binary 구현이 필요하기 때문입니다. 
    // println!("Point2D 를 이진수로 출력하면 어떻게 될까: {:b}?", point);
}
```

`fmt::Display` 는 구현했지만 `fmt::Binary` 는 안했기 때문에 `{:b}` 는 사용할 수 없습니다.
`std::fmt` 에는 많은 [`트레잇(traits)`][traits] 이 있고 각각을 구현해주어야 합니다.
더 자세한 사항은 [`std::fmt`][fmt] 을 보아주세요.

### 실습

위의 출력을 확인하시고, `Point2D` 구조체를 참고해서 복소수(Complex 라고 명명하세요) 
구조체를 만들어서 출력하면 다음처럼 나오도록 구현해보세요.

```txt
Display: 3.3 + 7.2i
Debug: Complex { real: 3.3, imag: 7.2 }
```

### 참고:

[`파생 구현(derive)`][derive], [`std::fmt`][fmt], [`매크로(macros)`][macros], 
[`구조체(struct)`][structs], [`트레잇(trait)`][traits], [`use`][use]

[derive]: ../../trait/derive.md
[fmt]: https://doc.rust-lang.org/std/fmt/
[macros]: ../../macros.md
[structs]: ../../custom_types/structs.md
[traits]: ../../trait.md
[use]: ../../mod/use.md
