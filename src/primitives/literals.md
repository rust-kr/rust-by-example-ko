# 변수와 연산자

각 자료형들은 정수는 `1`, 실수는 `1.2`, 문자는`'a'`, 문자열은 `"abc"`, 
불리언은 `true` 그리고 유닛 `()`와 같은 문법으로 사용할 수 있습니다.

정수는 16진수나 8진수 또는 2진수로 표시할 수 있으며, 각각의 변수앞에 다음을 
붙여서 표시합니다: `0x`, `0o` or `0b`.

숫자 자료형은 가독성을 높이기 위해 밑줄을 넣을 수 있습니다. 예를 들면,
`1_000` 은 `1000`와 같고, `0.000_001` 는 `0.000001`와 같습니다.

변수를 정의할 때는 컴파일러에게 자료형을 알려주어야 하니다. 여기서는
`u32` 후위 표시를 사용해서 부호없는 32비트 정수형임을 알리고, `i32`로 
부호있는 32비트 정수임을 표시했습니다.

사용가능한 [연산자와 우선순위][rust op-prec]은 다른 [C언어 계열언어][op-prec]과 
비슷합니다.

```rust,editable
fn main() {
    // 정수 덧셈
    println!("1 + 2 = {}", 1u32 + 2);

    // 정수 뺄셈
    println!("1 - 2 = {}", 1i32 - 2);
    // TODO ^ 1i32 를 1u32 로 바꾸고 어째서 자료형이 중요한지 확인해보세요.

    // 불리언 로직
    println!("true AND false is {}", true && false);
    println!("true OR false is {}", true || false);
    println!("NOT true is {}", !true);

    // 비트연산
    println!("0011 AND 0101 is {:04b}", 0b0011u32 & 0b0101);
    println!("0011 OR 0101 is {:04b}", 0b0011u32 | 0b0101);
    println!("0011 XOR 0101 is {:04b}", 0b0011u32 ^ 0b0101);
    println!("1 << 5 is {}", 1u32 << 5);
    println!("0x80 >> 2 is 0x{:x}", 0x80u32 >> 2);

    // 밑줄을 이용해 보기 좋게!
    println!("One million is written as {}", 1_000_000u32);
}
```

[rust op-prec]: https://doc.rust-lang.org/reference/expressions.html#expression-precedence
[op-prec]: https://en.wikipedia.org/wiki/Operator_precedence#Programming_languages
