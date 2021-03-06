# 기본 자료형

러스트는 다양한 종류의 `기본 자료형`을 제공합니다. 여기서는 그중 몇가지를 소개합니다.


### 단순 자료형

* 부호있는 정수: `i8`, `i16`, `i32`, `i64`, `i128`, `isize` (포인터 사이즈)
* 부호없는 정수: `u8`, `u16`, `u32`, `u64`, `u128`, `usize` (포인터 사이즈)
* 실수: `f32`, `f64`
* `char` 유니코드 자료형 `'a'`, `'α'`, `'∞'` (각각 4바이트)
* `bool` 자료형: `true` 또는  `false`
* 그리고 비어있는 튜플`()` 만을 값으로 가지는 유닛 자료형 `()`.

유닛 자료형은 튜플이지만, 여러 개의 값을 가지지는 않아서 복합 자료형이 아닙니다.

### 복합 자료형

* `[1, 2, 3]` 과 같은 배열
* `(1, true)` 과 같은 튜플

모든 변수는 *자료형을 지정*할 수 있습니다. 숫자들은 *후위표시(suffix)* 로 
자료형을 표시합니다. 정수는 기본적으로 `i32` 이고 실수는 `f64` 입니다.
러스트는 문맥으로부터 자료형을 추론 할 수 있습니다.


```rust,editable,ignore,mdbook-runnable
fn main() {
    // 변수에는 자료형을 지정할 수 있습니다.
    let logical: bool = true;

    let a_float: f64 = 1.0;  // 보통의 자료형 지정
    let an_integer   = 5i32; // 후위 표시

    // 또는 디폴트 자료형을 사용할 수도 있습니다.
    let default_float   = 3.0; // f64
    let default_integer = 7;   // i32
    
    // 문맥으로부터 자료형을 추론할 수도 있습니다.
    let mut inferred_type = 12; // 다른 행으로부터 i64 자료형으로 추론되었습니다.
    inferred_type = 4294967296i64;
    
    // 가변(mutable) 변수만 값을 변경할 수 있습니다.
    let mut mutable = 12; // 가변형 i32
    mutable = 21;
    
    // 에러! 변수의 자료형은 바뀔 수 없습니다.
    mutable = true;
    
    // 변수는 덮어 쓰여질 수 있습니다. 이것을 셰도우잉(shadowing)이라고 합니다.
    let mutable = true;
}
```

### 참고

[`표준(std)` 라이브러리][std], [`mut`][mut], [`inference`][inference], [`shadowing`][shadowing]

[std]: https://doc.rust-lang.org/std/
[mut]: variable_bindings/mut.md
[inference]: types/inference.md
[shadowing]: variable_bindings/scope.md
