# Csharp-like-rust — Language Specification (SPEC)

Csharp-like-rust는 **C# 문법을 Rust 의미론으로 변환하는 트랜스파일 언어**입니다.  
목표는 C#처럼 작성하고 Rust처럼 동작하는 GC-free 언어입니다.

---

# 1. Overview

- 문법(Syntax): 최대한 C# 기반
- 의미(Semantics): Rust 소유권/borrow/move 모델 적용
- 메모리 모델: GC 없음, 모든 값은 move 또는 borrow
- 출력: Rust 코드 (1차), C++/NASM 가능 (확장)

---

# 2. Lexical Structure

## 2.1 Keywords




class
static
int
void
string
return
using
var
new
bool
true
false



## 2.2 Identifiers

- C# 규칙 동일  
- 예: `Program`, `Main`, `value1`

## 2.3 Literals

- 정수: `123`, `0`, `42`
- 문자열: `"hello"`
- bool: `true`, `false`

---

# 3. Types

## 3.1 Primitive Types (C# → Rust)

| C# 타입        | Csharp-like-rust 내부 의미 | Rust 출력 |
|----------------|----------------------------|-----------|
| `int`          | 32-bit 정수                | `i32`     |
| `bool`         | 논리값                     | `bool`    |
| `string`       | UTF-8 문자열                | `String`  |
| `void`         | 반환 없음                  | `()`      |

## 3.2 var 추론



var x = 3;     // int → i32
var s = "hi";  // string → String



---

# 4. Memory Model (Rust semantics)

## 4.1 기본: Move semantics



var a = 10;
var b = a;   // a → moved



## 4.2 Borrow
C#의 참조 개념은 Rust borrow로 해석:




ref x → &x
ref mutable x → &mut x



(초기 버전에서는 단순치환 기반)

## 4.3 GC 없음
- 모든 객체는 값 타입 구조체로 재해석
- class는 Rust struct + impl로 변환

---

# 5. Classes

## 5.1 선언
```csharp
class Program {
    static int Add(int a, int b) {
        return a + b;
    }
}



5.2 변환 결과(Rust)


pub struct Program;

impl Program {
    pub fn add(a: i32, b: i32) -> i32 {
        a + b
    }
}




6. Methods


6.1 Static methods


C#:


static int Add(int a, int b) { return a + b; }



Rust 출력:


pub fn add(a: i32, b: i32) -> i32 {
    a + b
}



6.2 Instance methods


초기 버전:

모든 메서드를 static → standalone 함수로 단순화 가능.

확장 버전: impl 구조로 변환.



7. Expressions


7.1 Return


return x;



Rust:


x



7.2 Assignment


a = b + c;



7.3 Function call


Add(1, 2)




8. Statements




ExpressionStatement


ReturnStatement


VariableDeclaration


BlockStatement





9. Main Function


9.1 형태


static void Main() {
    // ...
}



9.2 출력


fn main() {
    // ...
}




10. Using


10.1 단순 변환


C#:


using System;



초기 버전: 무시 (no-op)

확장 버전: Rust use/import로 래핑.



11. Error Handling




기초 레벨: 파서 오류만 제공


확장 계획:



타입 불일치 탐지


borrow/move 충돌 탐지









12. Roadmap Integration


본 언어 스펙은 다음과 연동합니다:




SYNTAX.md


ROADMAP.md


Freeing-the-Lang ProofLedger


Multi-main OS 빌드 시스템





13. Example (Full)


입력


class Program {
    static int Add(int a, int b) {
        return a + b;
    }

    static void Main() {
        var x = Add(3, 4);
        print(x);
    }
}



출력


fn add(a: i32, b: i32) -> i32 {
    a + b
}

fn main() {
    let x = add(3, 4);
    println!("{}", x);
}




14. License


MIT License



---

