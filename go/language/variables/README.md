## Variables

변수는 언어의 핵심으로 메모리에서 읽고 쓰는 기능을 제공합니다. Go에서는 메모리 접근은 type safe한 특성을 가지고 있습니다. 이 말은 컴파일러가 엄격하게 타입을 가지고 선언한 범위 밖으로 변수를 사용하는 것을 허용하지 않는다는 뜻입니다.

## Notes

* 모든 프로그램의 목적 그리고 프로그램의 모든 부분에서 데이터를 옮기는 일을 수행합니다.
* 코드는 주로 메모리에 할당, 읽기, 쓰기를 수행합니다. 
* 타입을 이해해야만 좋은 코드를 작성할 수 있으며 이해할 수 있는 코드를 작성할 수 있습니다.
* 만약 데이터를 이해하지 못했다면, 문제를 이해할 수 없습니다.
* 데이터를 이해한다면 문제를 보다 잘 이해할 수 있습니다.
* 변수가 zero 값으로 선언하는 경우, var 키워드를 사용하세요.
* 변수를 선언하고 초기화할 때, 짧은 변수 선언 연산자를 사용하세요.

## Links

[Built-In Types](http://golang.org/ref/spec#Boolean_types)  
https://golang.org/doc/effective_go.html#variables  
http://www.goinggo.net/2013/08/gustavos-ieee-754-brain-teaser.html  
[What's in a name](https://www.youtube.com/watch?v=sFUSP8Au_PE)

## Code Review

[Declare and initialize variables](example1/example1.go) ([Go Playground](https://play.golang.org/p/B5mjJKPYLh))

## Exercises

### Exercise 1 

**Part A:** 3개 변수를 선언하고 zero 값으로 초기화합니다. 그리고 3개는 literal 값으로 선언합니다. 선언할 변수의 타입은 string, int, bool입니다. 이 변수의 값을 출력합니다. 

**Part B:** 타입 float32로 변수를 선언하고 Pi (3.14) literal 값으로 변환으로 변수를 초기화합니다.

[Template](exercises/template1/template1.go) ([Go Playground](https://play.golang.org/p/JIgjb3Ty3e)) | 
[Answer](exercises/exercise1/exercise1.go) ([Go Playground](https://play.golang.org/p/wNjayRMEcM))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
