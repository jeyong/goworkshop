## Slices - Arrays, Slices 그리고 Maps

Slice는 Go에서 아주 중요한 자료구조입니다. 유연성, 성능, 동적인 방식으로 데이터를 관리하고 처리하는데 있어서 기본이 됩니다. Go 프로그래머라면 모두 slice를 사용하는 방법을 숙지해야만 합니다. 

## 노트 

* Slice는 특별한 기능을 가지면서 built-in으로 제공되는 동적 array와 비슷합니다.
* slice의 length와 capacity 는 다른 의미이며 각각의 목적을 가지고 있습니다.
* Slice는 동일한 array에 대해서 다양한 "관점"을 제공합니다. 
* Slice는 built-in 함수인 append를 통해서 늘리는 것이 가능합니다. 

## Links

http://blog.golang.org/go-slices-usage-and-internals  
https://blog.golang.org/strings  
http://blog.golang.org/slices  
http://www.goinggo.net/2013/08/understanding-slices-in-go-programming.html  
http://www.goinggo.net/2013/08/collections-of-unknown-length-in-go.html  
http://www.goinggo.net/2013/09/iterating-over-slices-in-go.html  
http://www.goinggo.net/2013/09/slices-of-slices-of-slices-in-go.html  
http://www.goinggo.net/2013/12/three-index-slices-in-go-12.html  
https://github.com/golang/go/wiki/SliceTricks  

## Code Review

[Declare and Length](example1/example1.go) ([Go Playground](https://play.golang.org/p/lDKravTEqF))  
[Reference Types](example2/example2.go) ([Go Playground](https://play.golang.org/p/MuqPFwvDux))  
[Appending slices](example4/example4.go) ([Go Playground](https://play.golang.org/p/xiI54S0bSN))  
[Taking slices of slices](example3/example3.go) ([Go Playground](https://play.golang.org/p/Wq9JbadHkC))  
[Slices and References](example5/example5.go) ([Go Playground](https://play.golang.org/p/zYT3ls_DuV))  
[Strings and slices](example6/example6.go) ([Go Playground](https://play.golang.org/p/x0Q5ByzxGS))  
[Variadic functions](example7/example7.go) ([Go Playground](https://play.golang.org/p/TkJxbZKFRl))
[Range mechanics](example8/example8.go) ([Go Playground](https://play.golang.org/p/cve_NbA6Qn))  

## Advanced Code Review

[Three index slicing](advanced/example1/example1.go) ([Go Playground](https://play.golang.org/p/QZQIdaTgtG))

## Exercises

### Exercise 1

**Part A** 정수의 nil slice를 선언합니다. 이 slice에 10개 값을 append하는 loop을 생성합니다. slice를 iterate하고 각 값을 화면에 출력합니다. 

**Part B** 5개 문자열의 slice를 선언하고 문자열 literal 값을 가지는 slice를 초기화합니다. 모든 element들을 출력합니다. 인덱스가 1과 2인 slice를 가지며 새 slice에서 index의 위치와 각 element의 값을 출력합니다. 

[Template](exercises/template1/template1.go) ([Go Playground](https://play.golang.org/p/sE06PRtw7h)) | 
[Answer](exercises/exercise1/exercise1.go) ([Go Playground](https://play.golang.org/p/3WKISOXA-L))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
