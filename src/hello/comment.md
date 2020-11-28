# 코멘트

모든 프로그램에는 코멘트가 필요합니다. 러스트에서 지원하는 코멘트들은 
다음과 같습니다.

* *일반 코멘트* 는 컴파일러가 관여하지 않습니다.:
   * `// 한 줄 코멘트는 해당 줄의 끝까지 무시됩니다.`
   * `/* 블럭 코멘트는 종료 표시가 나올 때까지 무시됩니다. */`
* *Doc comments* which are parsed into HTML library
  [documentation][docs]:
   * `/// Generate library docs for the following item.`
   * `//! Generate library docs for the enclosing item.`

```rust,editable
fn main() {
    // This is an example of a line comment
    // There are two slashes at the beginning of the line
    // And nothing written inside these will be read by the compiler

    // println!("Hello, world!");

    // Run it. See? Now try deleting the two slashes, and run it again.

    /* 
     * This is another type of comment, a block comment. In general,
     * line comments are the recommended comment style. But
     * block comments are extremely useful for temporarily disabling
     * chunks of code. /* Block comments can be /* nested, */ */
     * so it takes only a few keystrokes to comment out everything
     * in this main() function. /*/*/* Try it yourself! */*/*/
     */

    /*
    Note: The previous column of `*` was entirely for style. There's
    no actual need for it.
    */

    // You can manipulate expressions more easily with block comments
    // than with line comments. Try deleting the comment delimiters
    // to change the result:
    let x = 5 + /* 90 + */ 5;
    println!("Is `x` 10 or 100? x = {}", x);
}

```

### See also:

[Library documentation][docs]

[docs]: ../meta/doc.md
