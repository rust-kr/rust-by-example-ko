# Hello World

다음은 전통의 Hello World 프로그램 소스입니다.

```rust,editable
// 이 부분은 코멘트라서 컴파일러가 관심을 주지 않습니다.
// 오른쪽에 "Run" 버튼을 클릭해서 테스트할 수 있습니다.
// 키보드를 사용하는 편이 좋다면, "Ctrl + Enter" 가 실행키입니다.

// 이 코드는 수정하실 수 있습니다. 마음껏 고쳐보세요!
// 원본코드로 되돌리려면 "Reset" 버튼을 클릭하세요.

// This is the main function
// 다음이 main 함수입니다.
fn main() {
    // 컴파일해서 실행파일을 만들고 실행하면, 이 자리의 문장들이 실행됩니다.

    // 콘솔에 문자열을 출력합니다.
    println!("Hello World!");
}
```

`println!` 은 문자열을 콘솔에 출력하는 [*macro*][macros] 입니다.

실행파일은 러스트 컴파일러 `rustc` 로 만들 수 있습니다.

```bash
$ rustc hello.rs
```

`rustc` 가 `hello` 라는 실행파일을 만들어 줄 겁니다.

```bash
$ ./hello
Hello World!
```

### 실습

위에서 "Run" 을 클릭하고 출력을 확인합니다. 그리고, 한 줄을 추가해서
`println!` 매크로를 한번 더 불러 다음을 출력해보세요.

```text
Hello World!
I'm a Rustacean!
```

[macros]: macros.md
