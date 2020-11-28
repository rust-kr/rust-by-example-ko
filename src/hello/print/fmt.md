# 출력 형식

출력 형식을 지정할 때 *형식 지정 문자열*을 사용하는 것을 앞에서 보았습니다.

* `format!("{}", foo)` -> `"3735928559"`
* `format!("0x{:X}", foo)` ->
  [`"0xDEADBEEF"`][deadbeef]
* `format!("0o{:o}", foo)` -> `"0o33653337357"`

동일한 변수(`foo`)도 `X`, `o` 등 형식 지정에 따라 다르게 출력됩니다.

형식을 지정하는 기능은 트레잇을 통해서 구현고, 인자의 자료형에 따라 트레잇이
한가지씩 있습니다. 가장 자주 쓰이는 트레잇은 `Display` 이고, 형식을 지정하지
않는 경우 `{}` 를  담당합니다.

```rust,editable
use std::fmt::{self, Formatter, Display};

struct City {
    name: &'static str,
    // 위도(Latitude)
    lat: f32,
    // 경도(Longitude)
    lon: f32,
}

impl Display for City {
    // 여기서 f 는 버퍼이며, 이 함수는 형식이 처리된 문자열을 버퍼에 출력해야 합니다.
    fn fmt(&self, f: &mut Formatter) -> fmt::Result {
        let lat_c = if self.lat >= 0.0 { 'N' } else { 'S' };
        let lon_c = if self.lon >= 0.0 { 'E' } else { 'W' };

        // write! 는 format! 과 비슷하지만 문자열을 버퍼 (첫번째 인자)에 출력합니다.
        write!(f, "{}: {:.3}°{} {:.3}°{}",
               self.name, self.lat.abs(), lat_c, self.lon.abs(), lon_c)
    }
}

#[derive(Debug)]
struct Color {
    red: u8,
    green: u8,
    blue: u8,
}

fn main() {
    for city in [
        City { name: "Dublin", lat: 53.347778, lon: -6.259722 },
        City { name: "Oslo", lat: 59.95, lon: 10.75 },
        City { name: "Vancouver", lat: 49.25, lon: -123.1 },
    ].iter() {
        println!("{}", *city);
    }
    for color in [
        Color { red: 128, green: 255, blue: 90 },
        Color { red: 0, green: 3, blue: 254 },
        Color { red: 0, green: 0, blue: 0 },
    ].iter() {
        // fmt::Display 를 구현한 다음에 {} 로 변경해보세요.
        println!("{:?}", *color);
    }
}
```

[`std::fmt`][fmt] 문서에 [형식지정 트레잇 전체 목록][fmt_traits]과 인자들이 
있습니다.

### 실습

`Color` 구조체를 위한 `fmt::Display` 트레잇을 구현해서 다음처럼 출력되게 해보세요.

```text
RGB (128, 255, 90) 0x80FF5A
RGB (0, 3, 254) 0x0003FE
RGB (0, 0, 0) 0x000000
```

다음을 참고하시면 구현할 수 있습니다. :
 * [각각의 색상을 한번 이상 표시하기][named_parameters],
 * `:02` 로 [0을 붙여서 2글자로 출력하기][fmt_width].

### 참고:

[`std::fmt`][fmt]

[named_parameters]: https://doc.rust-lang.org/std/fmt/#named-parameters
[deadbeef]: https://en.wikipedia.org/wiki/Deadbeef#Magic_debug_values
[fmt]: https://doc.rust-lang.org/std/fmt/
[fmt_traits]: https://doc.rust-lang.org/std/fmt/#formatting-traits
[fmt_width]: https://doc.rust-lang.org/std/fmt/#width
