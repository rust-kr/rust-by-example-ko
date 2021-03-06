# 튜플

튜플은 자료형이 다른 값들의 모음입니다. 괄호`()`로 생성하는데,
나열된 자료형 `(T1, T2, ...)`에 해당하는 값들을 넣을 수 있습니다.
여러 개의 값을 가지기 때문에 함수에서 한개 이상의 값을 리턴할 때 사용할 수 있습니다.

```rust,editable
// 튜플은 함수의 인자나 리턴값에 사용될 수 있습니다.
fn reverse(pair: (i32, bool)) -> (bool, i32) {
    // let 으로 튜플의 요소들을 각각의 변수에 바인딩 할 수 있습니다.
    let (integer, boolean) = pair;

    (boolean, integer)
}

// 실습에 사용할 구조체입니다.
#[derive(Debug)]
struct Matrix(f32, f32, f32, f32);

fn main() {
    // 각기 다른 자료형들로 만들어진 튜플
    let long_tuple = (1u8, 2u16, 3u32, 4u64,
                      -1i8, -2i16, -3i32, -4i64,
                      0.1f32, 0.2f64,
                      'a', true);

    // 인덱스 번호로 튜플 내부의 값을 가져올 수 있습니다.
    println!("첫번째 요소 : {}", long_tuple.0);
    println!("두번째 요소 : {}", long_tuple.1);

    // 튜플도 튜플의 요소로 들어갈 수 있습니다.
    let tuple_of_tuples = ((1u8, 2u16, 2u32), (4u64, -1i8), -2i16);

    // 튜플을 출력해봅니다.
    println!("튜플의 튜플: {:?}", tuple_of_tuples);
    
    // 너무 긴 튜플은 출력할 수 없습니다.
    // let too_long_tuple = (1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13);
    // println!("too long tuple: {:?}", too_long_tuple);
    // TODO ^ 위의 두줄의 코멘트를 없애고 컴파일러 에러를 확인하세요.

    let pair = (1, true);
    println!("pair 의 값은 {:?} 입니다.", pair);

    println!("pair 를 뒤집으면 {:?} 가 됩니다.", reverse(pair));

    // 요소가 하나인 튜플도 만들 수 있습니다. 단순히 괄호로 감싼 변수와 
    // 구분하기 위해 뒤에 쉼표를 하나 넣어줘야 합니다.
    println!("요소 한 개짜리 튜플: {:?}", (5u32,));
    println!("그냥 한 개의 정수: {:?}", (5u32));

    // 튜플은 바인딩으로 분해할 수 있습니다.
    let tuple = (1, "hello", 4.5, true);

    let (a, b, c, d) = tuple;
    println!("{:?}, {:?}, {:?}, {:?}", a, b, c, d);

    let matrix = Matrix(1.1, 1.2, 2.1, 2.2);
    println!("{:?}", matrix);

}
```

### 실습

 1. *복습*: 위의 예제에서 구조체 Matrix 를 위한 `fmt::Display` 트레잇을 추가하고,
    디버깅 포맷 `{:?}` 을 디스플레이 포맷 `{}`으로 변경하고, 다음처럼 출력되게 합니다.

    ```text
    ( 1.1 1.2 )
    ( 2.1 2.2 )
    ```

    앞서 보았던 [예제][print_display]를 참고하세요.
    

 2. `reverse` 함수를 기반으로 `transpose` 함수를 만들고, matrix 를 인자로 
    받도록 해서, 두 요소를 바꿔치기한 matrix 를 리턴하게 하세요.

    ```rust,ignore
    println!("Matrix:\n{}", matrix);
    println!("Transpose:\n{}", transpose(matrix));
    ```

    라고 하면 다음이 출력되게 만드시면 됩니다.

    ```text
    Matrix:
    ( 1.1 1.2 )
    ( 2.1 2.2 )
    Transpose:
    ( 1.1 2.1 )
    ( 1.2 2.2 )
    ```

[print_display]: ../hello/print/print_display.md
