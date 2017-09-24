## Interfaces

behavior만 정의한 타입을 선언하는 방식을 제공합니다. 여기서 behavior는 구체적인 타입인 struct나 이름을 가지는 타입과 같이 구체적인 타입으로 method를 통해서 구현할 수 있습니다. 구체적인 타입이 interface에 대한 method의 집합을 구현하는 경우, 구체적인 타입의 값은 interface type의 변수에 할당할 수 있습니다. 인터페이스 값에 대한 method 호출은 실제로 구체적인 값의 동일 method로 호출됩니다. 특정 타입은 어떤 interface로도 구현할 수 있으므로, interface 값에 대한 method call은 자연스럽게 polymorphic이 됩니다.  

## 노트

* 값에 대해서 method를 설정하면, value receiver로 구현된 method만 포함합니다.
* 포인터에 대해서 method를 설정하면, 포인터와 value receiver 모두로 구현하는 method를 포함합니다.
* pointer receiver로 선언한 method는 pointer value로만 interface를 구현합니다.
* value receiver로 선언한 method는 value와 pointer receiver 모두 interface를 구현합니다.
* method set의 원칙은 interface 타입에 적용됩니다.
* interface는 참조 타입이며 pointer를 공유하지 않습니다.
* 이것이 바로 go에서 polymorphic behavior를 생성하는 방법입니다.

## 링크

https://golang.org/doc/effective_go.html#interfaces  
http://blog.golang.org/laws-of-reflection  
http://www.goinggo.net/2014/05/methods-interfaces-and-embedded-types.html  
[Interface Pollution](https://medium.com/@rakyll/interface-pollution-in-go-7d58bccec275)  
[Abstraction Considered Harmful](http://bravenewgeek.com/abstraction-considered-harmful)

## 코드 리뷰

**_"Polymorphism이란 어떤 프로그램을 작성했을 때, 이것의 데이터에 따라서 다른 동작을 하는 것을 말한다." - Tom Kurtz (inventor of BASIC)_**

[Polymorphism](example1/example1.go) ([Go Playground](https://play.golang.org/p/Uag9qj7Pu5))  
[Method Sets](example2/example2.go) ([Go Playground](https://play.golang.org/p/4R3_QVKNli))  
[Address Of Value](example3/example3.go) ([Go Playground](https://play.golang.org/p/hJtuUbNICG))  
[Behavior Changes](example4/example4.go) ([Go Playground](https://play.golang.org/p/OrFNjhTrxv))  
[Storage By Value](example5/example5.go) ([Go Playground](https://play.golang.org/p/9yHyRQUEkW))  

## 고급 코드 리뷰

[Storing Values](advanced/example1/example1.go) ([Go Playground](https://play.golang.org/p/KXvtpd9_29))

## 연습문제

### 연습문제 1

**Part A** speak라는 method 이름을 가지는 interface인 speaker를 선언합니다. english라는 struct를 선언하는데 이는 english를 말하는 사람을 대표합니다. chinese라는 struct는 chinese를 말하는 사람을 대표합니다. 각 struct에 대해서 speaker interface 구현은 receiver 값과 "Hello World"와 "안녕하세요"라는 literal string을 사용합니다. speaker 타입 변수 선언과 english 타입 값의 주소를 할당하고 method를 호출합니다. chinese 타입의 값에 대해서도 다시 해봅니다. 

**Part B** sayHello라는 새로운 함수를 추가하는데 이 함수는 speaker 타입의 값을 받습니다. interface 값에서 speak method를 호출하기 위한 해당 함수를 구현합니다. 다음으로 각 타입의 새로운 값을 생성하고 이 함수를 사용합니다.  

[Template](exercises/template1/template1.go) ([Go Playground](https://play.golang.org/p/adkJ3OvYpr)) |
[Answer](exercises/exercise1/exercise1.go) ([Go Playground](https://play.golang.org/p/06fecJbfE4))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
