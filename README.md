# Csharp-like-rust

C# 문법을 Rust 의미론으로 재해석하는 실험적 언어 프로젝트입니다.  
GC 없이, VM 없이, C#처럼 작성하지만 Rust처럼 동작하는 형태를 목표로 합니다.

---

## 🚀 목표

- C# 구문(class, static, using 등)을 유지
- Rust의 소유권·Borrow·Move 모델 적용
- GC 없는 C# 스타일 언어 구현
- 출력 타깃:
  - Rust 코드
  - (확장 가능) C++ / NASM / Pure-Rust-No-LLVM 백엔드

---

## 🧩 언어 컨셉

### 입력(C#)
```csharp
class Program {
    static int Add(int a, int b) {
        return a + b;
    }

    static void Main() {
        var x = Add(3, 4);
        print(x);
    }
}



변환 결과(Rust)


fn add(a: i32, b: i32) -> i32 {
    a + b
}

fn main() {
    let x = add(3, 4);
    println!("{}", x);
}




🔧 프로젝트 구조(초기 버전)


src/
 ├─ lexer.rs
 ├─ parser.rs
 ├─ ast.rs
 ├─ transpiler.rs
 └─ main.rs

examples/
 └─ hello.cs

docs/
 ├─ SPEC.md
 ├─ SYNTAX.md
 └─ ROADMAP.md




🏃 실행 예시


cargo run examples/hello.cs




📜 로드맵




[ ] class → struct/impl 변환


[ ] static method 매핑


[ ] using → Rust 모듈 변환


[ ] var 타입 추론


[ ] void → ()


[ ] async/await 간단 구현


[ ] Pure-Rust-No-LLVM 백엔드 연동


[ ] ProofLedger 연동





---
