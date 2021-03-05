# 배열과 슬라이스

배열은 동일한 자료형(`T`)의 모음으로, 연속된 메모리에 저장됩니다. 대괄호 `[]` 
로 정의하고, 길이는 `[T; length]` 로 컴파일 할 때 지정해야합니다.

슬라이스는 배열과 비슷한 개념입니다만, 컴파일 할 때 길이를 지정하지 않는 점이 다릅니다.
대신, 객체 내부에 2개의 워드를 가집니다. 첫번째 워드는 데이터를 가리키는 포인터로 사용하고, 
두번째 워드에는 슬라이스의 길이를 저장합니다. 워드는 usize와 크기가 같은데, 이 값은 CPU 에따라 달라집니다. 
즉 x86-64 CPU에서는 64비트가 됩니다. 배열의 일부를 빌려올 때 사용할 수 있고, 문법은 `&[T]` 입니다.

```rust,editable,ignore,mdbook-runnable
use std::mem;

// 이 함수는 슬라이스의 소유권을 빌려옵니다.
fn analyze_slice(slice: &[i32]) {
    println!("전달된 슬라이스의 첫 요소는 {}입니다.", slice[0]);
    println!("전달된 슬라이스는 {}개의 요소를 가지고 있습니다.", slice.len());
}

fn main() {
    // 길이가 고정된 배열 (추가로 자료형을 지정하지 않아도 됩니다)
    let xs: [i32; 5] = [1, 2, 3, 4, 5];

    // 모든 요소들을 같은 값으로 초기화할 수 있습니다.
    let ys: [i32; 500] = [0; 500];

    // Indexing starts at 0
    println!("first element of the array: {}", xs[0]);
    println!("second element of the array: {}", xs[1]);

    // `len` returns the count of elements in the array
    println!("number of elements in array: {}", xs.len());

    // Arrays are stack allocated
    println!("array occupies {} bytes", mem::size_of_val(&xs));

    // Arrays can be automatically borrowed as slices
    println!("borrow the whole array as a slice");
    analyze_slice(&xs);

    // Slices can point to a section of an array
    // They are of the form [starting_index..ending_index]
    // starting_index is the first position in the slice
    // ending_index is one more than the last position in the slice
    println!("borrow a section of the array as a slice");
    analyze_slice(&ys[1 .. 4]);

    // 아래 문장에서는 index out of bounds 오류가 발생합니다.
    println!("{}", xs[5]);
}
```
