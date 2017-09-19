## Methods

Method는 receiver를 가지는 함수입니다. 해당 method는 특정 type에 바딩인됩니다. method는 해당 타입의 값이나 포인터를 기반으로 운영됩니다.

## Notes

* method는 reciever 변수를 선언하는 함수입니다.
* receiver는 method를 타입에 바인딩하고 값이나 포인터를 사용할 수 있습니다.
* 프로그램 영역에서 전달은 값의 복사본을 사용합니다.
* 프로그램 영역에서 포인터는 값의 주소의 복사본을 전달합니다.
* 타입이 주어지는 경우 하나를 선택해서 일정하게 사용합니다.

## Quotes

_"데이터의 일부가 하는 일을 노출해야하는 이유가 합당할때 method가 의미를 가집니다" - William Kennedy_

## Links

https://golang.org/doc/effective_go.html#methods  
http://www.goinggo.net/2014/05/methods-interfaces-and-embedded-types.html

## Code Review

[Declare and receiver behavior](example1/example1.go) ([Go Playground](https://play.golang.org/p/-outqMAJRD))  
[Value and Pointer semantics](example5/example5.go) ([Go Playground](https://play.golang.org/p/cyXulaDNL9))  
[Named typed methods](example2/example2.go) ([Go Playground](https://play.golang.org/p/9WeR1rShIa))  
[Function/Method variables](example3/example3.go) ([Go Playground](https://play.golang.org/p/Ewhk87BiWA))  
[Function Types](example4/example4.go) ([Go Playground](https://play.golang.org/p/EZQPrC9qsx))

## Exercises

### Exercise 1

야구 선수를 나타내는 struct를 선언합니다. 이름, atBats, hit를 포함합니다. 선수의 배팅 평균을 계산하는 method를 선언합니다. 공식은 Hits/AtBats입니다. 이 타입의 slice를 선언하고 여러 선수들로 slice를 초기화합니다. slice를 iterator로 선수 이름과 batting 평균을 출력합니다.

[Template](exercises/template1/template1.go) ([Go Playground](https://play.golang.org/p/IG5uqVRTrc)) |
[Answer](exercises/exercise1/exercise1.go) ([Go Playground](https://play.golang.org/p/1vr9fCLEO8))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.