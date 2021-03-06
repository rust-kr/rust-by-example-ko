# 테스트 케이스: List

내부 요소들이 순서대로 처리되어야 하는 구조체의 경우 `fmt::Display`를 구현하기가 어렵습니다.
각각의 `write!` 들이 `fmt::Result` 를 리턴하는 것이 문제가 됩니다.
적절한 처리를 위해서는 각각의 리턴값을 잘 처리해야 하는데요.
러스트에는 정확히 이때 사용할 수 있는 `?` 연산자가 있습니다.

`write!` 에서 `?` 를 사용하는 방법은 다음과 같습니다.

```rust,ignore
// write! 를 실행하고 오류가 있는지 검사합니다. 만약 오류가 발생하면
// 오류를 리턴하고 아니면 계속 진행합니다.
write!(f, "{}", value)?;
```

연산자 `?` 를 사용하면, `Vec` 의 `fmt::Display` 구현도 쉽게 할 수 있습니다.

```rust,editable
use std::fmt; // fmt 모듈 임포트합니다.

// Vec 을 담고있는 List 구조체를 정의합니다.
struct List(Vec<i32>);

impl fmt::Display for List {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // 튜플(tuple) 인덱싱으로 값을 가져오고, 참조를 vec 에 저장합니다.
        let vec = &self.0;

        write!(f, "[")?;

        // vec 의 요소들을 하나씩 v 로 참조하면서 순환합니다.
        // count 에는 반복 횟수가 들어갑니다.
        for (count, v) in vec.iter().enumerate() {
            // 첫 번째 요소만 빼고 쉼표를 추가합니다.
            // 오류가 발생시 리턴하기 위해 ? 연산자를 사용합니다.
            if count != 0 { write!(f, ", ")?; }
            write!(f, "{}", v)?;
        }

        // 대괄호를 닫고 fmt::Result 를 리턴합니다.
        write!(f, "]")
    }
}

fn main() {
    let v = List(vec![1, 2, 3]);
    println!("{}", v);
}
```

### 실습

코드를 수정해서 각각의 인덱스 번호도 출력되게 해보세요. 다음처럼 출력되면 성공입니다.

```rust,ignore
[0: 1, 1: 2, 2: 3]
```

### 참고

[`for`][for], [`ref`][ref], [`Result`][result], [`struct`][struct],
[`?`][q_mark], and [`vec!`][vec]

[for]: ../../../flow_control/for.md
[result]: ../../../std/result.md
[ref]: ../../../scope/borrow/ref.md
[struct]: ../../../custom_types/structs.md
[q_mark]: ../../../std/result/question_mark.md
[vec]: ../../../std/vec.md
