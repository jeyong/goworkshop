## Functions

함수는 언어의 핵심이 되는 부분입니다. 별도의 기능을 가지는 부분을 그룹으로 모아서 구조화시키는 메커니즘입니다. 우리가 작성하는 패키지에 대해서 API를 제공하는데 사용하기도 하며 동시성의 핵심 컴포넌트 중에 하나입니다.

## 노트

* 함수는 여러개 값을 반환할 수 있으며 대부분은 하나의 error 값을 반환합니다. 
* error 값은 프로그래밍 로직의 일부로 체크해야만 합니다.
* blank 식별자는 반환값을 무시하는데 사용합니다. 

## 링크

https://golang.org/doc/effective_go.html#functions  
http://www.goinggo.net/2013/10/functions-and-naked-returns-in-go.html  
http://www.goinggo.net/2013/06/understanding-defer-panic-and-recover.html

## 코드 리뷰

[Return multiple values](example1/example1.go) ([Go Playground](https://play.golang.org/p/rJMtATFqPi))  
[Blank identifier](example2/example2.go) ([Go Playground](https://play.golang.org/p/ziCWrNaGWO))  
[Redeclarations](example3/example3.go) ([Go Playground](https://play.golang.org/p/CofPHyVpne))  
[Anonymous Functions/Closures](example4/example4.go) ([Go Playground](https://play.golang.org/p/AhT35gu2fE))

## 고급 코드 리뷰

[Recover panics](advanced/example1/example1.go) ([Go Playground](https://play.golang.org/p/UuT3FNWd7x))

## 연습문제

### 연습문제 1

**Part A** 사용자의 정보를 저장하는 구조체 타입을 선언합니다. 이 타입의 값을 생성하며 이 타입의  
Declare a struct type to maintain information about a user. Declare a function that creates value of and returns pointers of this type and an error value. Call this function from main and display the value.

**Part B** Make a second call to your function but this time ignore the value and just test the error value.

[Template](exercises/template1/template1.go) ([Go Playground](https://play.golang.org/p/i5wI736jpN)) | 
[Answer](exercises/exercise1/exercise1.go) ([Go Playground](https://play.golang.org/p/fabhfnqJ0C))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
