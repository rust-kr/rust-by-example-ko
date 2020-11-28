# 형식을 지정하는 출력

출력은 [`std::fmt`][fmt] 에 정의된 [`macro`][macros] 들로 처리합니다.

* `format!`: 형식 지정된 문자열을 [`String`][string] 에 출력합니다.
* `print!`: `format!` 과 동일하지만, 문자열을 콘솔 (io::stdout) 에 출력합니다.
* `println!`: `print!` 과 동일하지만, 개행 문자를 덧붙여줍니다.
* `eprint!`: `format!` 과 동일하지만, 문자열을 표준 오류 스트림 (io::stderr) 에 출력합니다.
* `eprintln!`: `eprint!`과 동일하지만, 개행 문자를 덧붙여줍니다.

이들은 모두 동일한 방식으로 문자열을 처리합니다. 러스트에서는 컴파일 시점에
형식지정이 올바른지 여부도 검사됩니다.


```rust,editable,ignore,mdbook-runnable
fn main() {
    // 일반적으로, {}는 자료형에 관계없이 주어진 인자로 대치됩니다.
    // 이때, 인자들은 문자열로 변환됩니다.
    println!("{} 번째 날", 31);

    // 자료형 표시(suffix)가 없으므로 31은 i32 형이 됩니다. 31 의 자료형을 바꾸려면
    // 자료형 표시(suffix)를 해주면 됩니다. 31i64 라고 하면 i64 형이 됩니다.

    // 중괄호를 이용해서 다양한 방법으로 형식을 지정할 수 있는데, 다음처럼
    // 인자의 위치를 이용할 수도 있습니다.
    println!("{0}야 얘는 내 친구 {1}야. {1}야 이쪽은 {0}야", "영희", "철수");

    // 이름을 줄 수도 있습니다.
    println!("{subject} {verb} {object}",
             object="the lazy dog",
             subject="the quick brown fox",
             verb="jumps over");

    // 역주) 한글도 잘 됩니다.
    println!("{주어} {목적어} {동사}.", 동사="한다", 주어="내가", 목적어="코딩을");

    // `:` 의 뒤에 특별한 형식을 지정할 수도 있습니다.
    println!("{:b}명의 사람들 중 {}명 만이 이진법을 알고, 나머지 반은 모른다", 2, 1);

    // 폭을 지정해서 오른편 정렬을 할 수도 있습니다. 다음 코드의 출력은
    // "     1" 이 됩니다. 즉, 공백문자 5개가 나온 후에 "1"이 출력됩니다.
    println!("{number:>width$}", number=1, width=6);

    // 공백대신 숫자 0을 넣을 수도 있습니다. 다음 코드는 "000001"을 출력합니다.
    println!("{number:>0width$}", number=1, width=6);

    // 역주) 역시 한글도 잘 됩니다.
    println!("{숫자:>폭$}", 숫자=1, 폭=6);
    println!("{숫자:>0폭$}", 숫자=1, 폭=6);

    // Rust는 필요한 인자의 숫자가 맞는지 검사도 해줍니다.
    println!("내 이름은 {0}요. {1} {0}.", "본드");
    // FIXME ^ 위 코드에서 빠진 인자 "제임스"를 추가해주세요.

    // 한개의 `i32` 를 가지고 있는 `Structure`라는 구조체를 생성해봅니다.
    #[allow(dead_code)]
    struct Structure(i32);

    // 하지만, 이런 사용자 정의 자료형을 출력하려면 추가 작업이 필요합니다.
    // 다음 코드는 동작하지 않을겁니다.
    println!("이 구조체 {}는 출력되지 않을겁니다.", Structure(3));
    // FIXME ^ 위 코드를 코멘트로 막아주세요.
}
```

[`std::fmt`][fmt] 에는 문자열 출력에 관련된 많은 [`트레잇(traits)`][traits] 
이 있습니다. 다음은 그 중 중요한 두 가지 트레잇입니다.

* `fmt::Debug`: `{:?}` 를 처리합니다. 디버깅에 사용합니다.
* `fmt::Display`: `{}` 를 처리합니다. 보기 편하게 출력 형식을 지정하는데 사용합니다.

여기서는 표준 라이브러리가 지원하는 자료형들을 출력했기 때문에 `fmt::Display`를 사용했습니다.
사용자 정의 자료형을 위해서는 추가 작업이 필요합니다.

`fmt::Display` 트레잇을 구현하면, 자동으로 [`ToString`] 트레잇이 구현되고, 
해당 자료형을 [`String`][string]으로 [`변환(convert)`][convert] 할 수 있게됩니다.

### Activities

 * 위 코드에서 두 개의 이슈(FIXME 라고 된 부분들)를 수정하고 오류없이 실행되게 해보세요.
 * `println!` 매크로의 소수점 표시 기능을 이용해서 `원주율의 근사치는 3.142이다.` 를 출력해보세요.
   실습을 위한 파이값은 `let pi = 3.141592` 라고 정의해주세요. (힌트: [`std::fmt`][fmt] 
   문서에서 소수점 표시(Precision) 항목을 참고하세요.)

### 참고:

[`std::fmt`][fmt], [`매크로(macros)`][macros], [`구조체(struct)`][structs], 
[`트레잇(traits)`][traits]

[fmt]: https://doc.rust-lang.org/std/fmt/
[macros]: ../macros.md
[string]: ../std/str.md
[structs]: ../custom_types/structs.md
[traits]: https://doc.rust-lang.org/std/fmt/#formatting-traits
[`ToString`]: https://doc.rust-lang.org/std/string/trait.ToString.html
[convert]: ../conversion/string.md
