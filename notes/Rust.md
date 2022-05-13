# Rust

- [[프로그래밍 언어]]

- [[Mozilla Foundation]] 재단에서 개발했으며, 현재는 Rust 재단 소속 프로젝트

- [[MIT (License)]]와 [[Apache 2.0 (License)]]로 듀얼 라이센싱 된 [[오픈소스]] 프로젝트
  - [https://github.com/rust-lang/rust]

- 멀티 패러다임, [[Functional Programming]], [[Object-Oriented Programming]]

- Zero-cost abstraction
  - [Abstraction without overhead: traits in Rust | Rust Blog](https://blog.rust-lang.org/2015/05/11/traits.html)
    - **Generics are compiled away, resulting in static dispatch**. That is, as with C++ templates, the compiler will generate __two copies__ of the `print_hash`
    - method to handle the above code, one for each concrete argument type. That in turn means that the internal call to `t.hash()` -- the point where the abstraction is actually used -- has zero cost: it will be compiled to a direct, static call to the relevant implementation:
    - **But, unlike with [[C++]] templates, clients of traits are fully type-checked in advance**. That is, when you compile `HashMap` in isolation, its code is checked __once__ for type correctness against the abstract `Hash` and `Eq` traits, rather than being checked repeatedly when applied to concrete types. That means earlier, clearer compilation errors for library authors, and less typechecking overhead (i.e., faster compilation) for clients.
    - Static and dynamic dispatch are complementary tools, each appropriate for different scenarios. **Rust's traits provide a single, simple notion of interface that can be used in both styles, with minimal, predictable costs**. Trait objects satisfy Stroustrup's "pay as you go" principle: you have vtables when you need them, but the same trait can be compiled away statically when you don't.
  - [Zero-cost futures in Rust · Aaron Turon](https://aturon.github.io/blog/2016/08/11/futures/)
    - This is non-blocking code that moves through several states: first we do an RPC call to acquire an ID; then we look up the corresponding row; then we encode it to json; then we write it to a socket. **Under the hood, this code will compile down to an actual state machine which progresses via callbacks (with no overhead)**, but we get to write it in a style that’s not far from simple __blocking__ code. (Rustaceans will note that this story is very similar to `Iterator` in the standard library.) Ergonomic, high-level code that compiles to state-machine-and-callbacks: that’s what we were after!

- 강력한 [[타입 시스템]]
  - [[Hindley-Milner Type System]] 기반 타입 추론

- 소유권(Ownership) 개념을 통한 메모리 관리 메커니즘
  - 복사가 아닌 이동(Move Semantic)이 기본
  - 객체의 수명주기를 정적으로 검사하는 또 하나의 타입 시스템
  - 객체의 수명이 종료되는 지점에서 자동으로 메모리를 수거
  - 명시적으로 의도하지 않는 이상 컴파일된 프로그램에 메모리 누수나 비정상 메모리 참조가 없음을 보장함
