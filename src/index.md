# 예제로 배우는 러스트 (Rust by Example) 한국어판

러스트는 안전성과 속도 그리고, 병렬 처리에 초점을 맞춘 최신 시스템 프로그래밍 언어
입니다. 또한 가비지 컬렉션 없이 메모리 안전성을 지원합니다.

이 문서는 실행 가능한 예제들로 Rust의 여러가지 개념과 표준 라이브러리를 소개합니다. 
예제들을 활용하기 위해서는 로컬에 러스트를 [설치][install]하고 [공식 문서][std]도 읽어보기 
바랍니다. 관심있는 분은 이 문서의 [소스][home]도 보아주세요.

(역주: 보고 계신 한글판의 번역은 [여기][home-ko]에서 진행하고 있습니다.)

이제 시작할까요!

- [인사하기](hello.md) - 전통의 Hello World 부터 만들어봅시다.

- [기본 자료형](primitives.md) - 부호있는 정수형과 부호없는 정수형, 기타 기본 자료형들에 대해 배웁시다.

- [사용자 정의 자료형](custom_types.md) - `struct` 와 `enum`.

- [변수 바인딩](variable_bindings.md) - mutable bindings, scope, shadowing.

- [자료형](types.md) - Learn about changing and defining types.

- [변환](conversion.md)

- [표현식](expression.md)

- [실행 제어](flow_control.md) - `if`/`else`, `for`, and others.

- [함수](fn.md) - Learn about Methods, Closures and High Order Functions.

- [모듈](mod.md) - Organize code using modules

- [크레이트(Crate)](crates.md) - A crate is a compilation unit in Rust. Learn to create a library.

- [카고(Cargo)](cargo.md) - Go through some basic features of the official Rust package management tool.

- [Attributes](attribute.md) - An attribute is metadata applied to some module, crate or item.

- [Generics](generics.md) - Learn about writing a function or data type which can work for multiple types of arguments.

- [Scoping rules](scope.md) - Scopes play an important part in ownership, borrowing, and lifetimes.

- [Traits](trait.md) - A trait is a collection of methods defined for an unknown type: `Self`

- [Macros](macros.md)

- [Error handling](error.md) - Learn Rust way of handling failures.

- [Std library types](std.md) - Learn about some custom types provided by `std` library.

- [Std misc](std_misc.md) - More custom types for file handling, threads.

- [Testing](testing.md) - All sorts of testing in Rust.

- [Unsafe Operations](unsafe.md)

- [Compatibility](compatibility.md)

- [Meta](meta.md) - Documentation, Benchmarking.


[rust]: https://www.rust-lang.org/
[install]: https://www.rust-lang.org/tools/install
[std]: https://doc.rust-lang.org/std/
[home]: https://github.com/rust-lang/rust-by-example
[home-ko]: https://github.com/rust-lang-ko/rust-by-example-ko
