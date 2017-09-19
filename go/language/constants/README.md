## Constants

절대 변경되지 않는 값에 대해서 식별할 수 있는 이름을 붙여서 만드는 방식. Go에서 엄청난 유연성을 제공한다. Go에서 상수 구현은 아주 특이하다.

## 노트

* 상수는 변수가 아니다.
* 컴파일하는 시점에만 존재
* 타입을 가지지 않는 상수는 Untyped constants can be implictly converted where typed constants and variables can't.
* 타입이 없는 상수를 Type이 아니라 Kind로 생각하기
* 명시적과 암묵적 변환에 대해서 익히기
* 상수의 강력함을 이해하고 표준 라이브러이에서 어떻게 사용하는지 보기

## Links

https://golang.org/ref/spec#Constants  
http://blog.golang.org/constants  
http://www.goinggo.net/2014/04/introduction-to-numeric-constants-in-go.html

## Code Review

[상수 선언과 초기화](example1/example1.go) ([Go Playground](https://play.golang.org/p/dIJb3S6CIb))  
[병렬 타입 시스템 (Kind)](example2/example2.go) ([Go Playground](https://play.golang.org/p/-DUJAVsTMp))  
[iota](example3/example3.go) ([Go Playground](https://play.golang.org/p/1Y9qjOuPt0))  
[묵시적 변환](example4/example4.go) ([Go Playground](https://play.golang.org/p/QzVFcMdU5S))  

## Exercises

### Exercise 1

**Part A:** untyped와 typed 상수 선언과 값 출력

**Part B:** 2가지 literal 상수를 typed 변수와 값을 출력하는 것으로 나눠보기

[Template](exercises/template1/template1.go) ([Go Playground](https://play.golang.org/p/QMrOCsHjcC)) |
[Answer](exercises/exercise1/exercise1.go) ([Go Playground](https://play.golang.org/p/aUZ-7VPb9H))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
