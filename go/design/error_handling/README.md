## 에러 핸들링 디자인 (Error Handling Design)

에러 핸들링은 신뢰할 수 있는 프로그램으로 만드는데 핵심이 됩니다. 적절한 에러 값이란 구체적이며 정보를 포함하고 있어야 합니다. 이렇게 하면 호출자에게 발생한 에러에 대한 처리를 할 수 있도록 할 수 있습니다. Go에서는 에러 값을 생성하는 여러 방법이 있습니다. 제공해야할 context의 양에 따라 달라집니다. 

## 노트

* 정적이고 단순한 포맷 메시지에 대해서는 기본 에러 값을 사용한다.
* 호출자가 특정 에러를 식별할 수 있도록 에러 변수를 생성하고 반환한다.
* 에러의 컨텍스트가 복잡하다면 커스텀 에러 타입을 생성한다.
* Go에서 에러 값은 특별한 것이 아니다. 그냥 값일 뿐이다. 따라서 원하는대로 처리할 수 있다.

## 인용

_사람이 실수 없이 수백만 라인의 코드를 작성할 수 있을 것이라고 가정하고 시스템을 개발할 수 없으며, 신뢰할 수 있는 시스템을 개발하는 디버깅만이 효과적인 방법도 아니다. - Al Aho (inventor of AWK)_

## 링크

http://blog.golang.org/error-handling-and-go  
http://www.goinggo.net/2014/10/error-handling-in-go-part-i.html  
http://www.goinggo.net/2014/11/error-handling-in-go-part-ii.html  
https://www.goinggo.net/2017/05/design-philosophy-on-logging.html  
http://clipperhouse.com/2015/02/07/bugs-are-a-failure-of-prediction/  
http://dave.cheney.net/2014/12/24/inspecting-errors  
http://dave.cheney.net/2016/04/27/dont-just-check-errors-handle-them-gracefully  
https://dave.cheney.net/2016/06/12/stack-traces-and-the-errors-package  
[Errors are handled in return values](https://plus.google.com/+RussCox-rsc/posts/iqAiKAwP6Ce)  

## 코드 리뷰

[Default Error Values](example1/example1.go) ([Go Playground](https://play.golang.org/p/aSjTxzNfP2))  
[Error Variables](example2/example2.go) ([Go Playground](https://play.golang.org/p/-vBG0m1Scs))  
[Type As Context](example3/example3.go) ([Go Playground](https://play.golang.org/p/FeR2nE3eAH))  
[Behavior As Context](example4/example4.go) ([Go Playground](https://play.golang.org/p/Aylgou6Gq0))  
[Find The Bug](example5/example5.go) ([Go Playground](https://play.golang.org/p/0AUU_sJsec)) | 
[The Reason](example5/reason/reason.go) ([Go Playground](https://play.golang.org/p/TCANdwroOi))  
[Wrapping Errors](example6/example6.go) ([Go Playground](https://play.golang.org/p/VfqgeCH-v2))  

## 연습문제

### 연습문제 1
2개 에러 변수를 생성합니다. 하나는 ErrInvalidValue고 다른 하나는 ErrAmountTooLarge입니다. 각 변수에 대해서 정적 메시지를 제공합니다. 다음으로 checkAmount라는 함수를 작성하며 이 함수는 float64 타입 값을 받아서 에러 값을 반환합니다. $1,000보다 큰 값인지 체크하고 만약 그렇다면 ErrAmountTooLarge를 반환합니다. main 함수를 작성해서 checkAmount 함수를 호출하고 반환하는 에러 값을 검사합니다. 화면에 적절한 메시지를 출력하세요.

[Template](exercises/template1/template1.go) ([Go Playground](https://play.golang.org/p/Ltxl8Hkrkl)) | 
[Answer](exercises/exercise1/exercise1.go) ([Go Playground](https://play.golang.org/p/WHmYkHwYjf))

### 연습문제 2
커스텀 에러 타입으로 appError를 생성합니다. 여기에는 3개 필드로 err error, message string 그리고 code int가 있습니다. 이 3개 필드를 이용해서 여러분의 메시지를 제공하는 error interface를 구현하세요. code 필드의 값이 9이면 false를 반환하는 temporary라는 이름의 2번째 method를 구현하세요. 만약 값이 false이면 여러분이 커스텀 에러 타입으로 초기화했던 포인터를 반환합니다. 만약 값이 true이면, default error를 반환합니다. checkFlag 함수를 호출하는 main 함수를 작성하고 temporary interface를 사용해서 error를 체크하세요. 

[Template](exercises/template2/template2.go) ([Go Playground](http://play.golang.org/p/9nEdNSMa_j)) | 
[Answer](exercises/exercise2/exercise2.go) ([Go Playground](http://play.golang.org/p/7iX9wZX6WP))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
