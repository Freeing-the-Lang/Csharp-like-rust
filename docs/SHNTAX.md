# Csharp-like-rust — Syntax Specification

Csharp-like-rust는 C# 문법을 기반으로 하되 Rust 의미 구조를 목표로 한다.  
이 문서는 **문법(Syntax)** 을 중심으로 정의한다.

---

# 1. 기본 구조

Csharp-like-rust 프로그램은 아래 순서를 따른다:

- using 구문 (선택)
- class 선언 (하나 이상)
- Main 함수 포함 클래스 하나 필요

예:
```csharp
using System;

class Program {
    static void Main() {
        print("Hello");
    }
}




2. using 구문


using <Identifier>;



현재 의미적 기능 없음 (초기 버전에서는 무시).


예:


using System;
using MyLib;




3. 클래스 선언


class <Identifier> {
    <class_members...>
}



예:


class MathUtil {
    static int Add(int a, int b) {
        return a + b;
    }
}




4. 메서드 문법


4.1 정적 메서드 (static)


static <return_type> <Identifier>(<params>) {
    <statements>
}



예:


static int Add(int a, int b) {
    return a + b;
}



4.2 반환 타입




int


bool


string


void





5. 파라미터


<int_or_ident> <Identifier>



예:


static int Sum(int a, int b)



여러 개:


(int a, int b, string name)




6. Main 함수


static void Main() {
    <statements>
}



예:


static void Main() {
    var x = Add(1, 2);
    print(x);
}




7. 변수 선언


7.1 명시적 타입


int x = 3;
string s = "hi";
bool ok = true;



7.2 var 타입 추론


var x = 10;
var msg = "hello";




8. 표현식 (Expressions)


8.1 기본 연산


a + b
a - b
a * b
a / b



8.2 함수 호출


Add(3, 4)
Print(message)



8.3 리터럴


123
true
"hello"




9. 문장(Statements)


9.1 Expression statement


Print(x);



9.2 Variable declaration


var x = 3;
int y = 10;



9.3 Return


return x + 1;



9.4 Block


{
    var a = 1;
    var b = 2;
}




10. 제어문(초기 버전: 지원 안 함)


현재 버전에서는 다음 제어문은 비활성화(추후 확장):




if


for


while


switch




로드맵 단계에서 활성화 예정.



11. 문자열


기본 C# 스타일:


"hello"




12. 이름 규칙


Identifier = [A-Za-z_][A-Za-z0-9_]*



예:


Program
Math
value1
_doSomething




13. 주석


C# 주석 그대로 지원:


// single-line comment

/*
 multi-line
 comment
*/




14. 전체 예제


using System;

class Program {

    static int Add(int a, int b) {
        return a + b;
    }

    static void Main() {
        var x = Add(3, 4);
        print(x);
    }
}




15. 출력 예시 (Rust)


fn add(a: i32, b: i32) -> i32 {
    a + b
}

fn main() {
    let x = add(3, 4);
    println!("{}", x);
}




---
