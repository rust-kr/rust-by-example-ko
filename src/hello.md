# 인사하기

다음은 전통의 Hello World 프로그램 소스입니다.

```rust,editable
// 이 부분은 코멘트라서 컴파일러는 관여하지 않습니다.
// 오른쪽에 "Run" 버튼을 클릭해서 테스트할 수 있습니다.
// 키보드 사용하는 쪽이 편하시면 "Ctrl + Enter" 로 실행 할 수 있습니다.

// 이 코드는 수정하실 수 있습니다. 마음껏 고쳐보세요!
// 원래 코드로 되돌리려면 오른쪽의 "Undo" 버튼을 클릭하세요.

// 다음은 main 함수입니다.
fn main() {
    // 컴파일하고 실행하면, 이곳의 문장들이 실행됩니다.

    // 콘솔에 문자열을 출력합니다.
    println!("Hello World!");
}
```

`println!` 은 문자열을 콘솔에 출력하는 [*macro*][macros] 입니다.

실행 파일은 러스트 컴파일러 `rustc`로 만들 수 있습니다.

```bash
$ rustc hello.rs
```

`rustc`가 실행 파일 `hello`를 만들어 줄 겁니다.

```bash
$ ./hello
Hello World!
```

### 실습

페이지 위쪽의 프로그램 상자에서 "Run" 을 클릭하면 어떤 내용이 출력되는지 확인합니다. 그리고, 한 줄을 추가하고
`println!` 매크로를 한 번 더 사용해서 아래 문자열이 출력되도록 해보세요.

```text
Hello World!
I'm a Rustacean!
```

[macros]: macros.md
