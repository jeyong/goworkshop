## Context - 표준 라이브러리

context 패키지는 Context 타입을 정의하며, API나 프로세스 사이에서 deadline, cancelation signals 혹은 다른 범위내의 요청 값들을 전달할 수 있습니다.

## 노트

* 서버로 들어오는 요청은 Context를 생성해야만 합니다.
* 서버에서 나가는 호출은 Context를 받아야만 합니다.
* 함수 호출 체인에서 Context를 전달해야만 합니다.
* WithCancel, WithDeadline, WithTimeout, WithValue를 사용해서 Context를 대체합니다.
* Context가 cancel되면, 해당 context에서 나온 모든 context들도 취소됩니다. 
* struct type 내부에 Context를 저장하지 않습니다. 대신에 Context를 명시적으로 이를 필요로 하는 각 함수에 전달합니다.
* nil Context를 전달하지 않습니다. 심지어 함수가 이를 수용하더라도 전달하지 않도록 합니다. 
* 프로세스와 API 사이에서 전달되는 데이터에 대해서만 context 값을 사용합니다. 함수에 옵셔널 인자 전달은 하지 않습니다.
* 다른 goroutine에서 실행되는 함수에 동일한 Context를 전달할 수 있습니다. Context는 여러 goroutine에서 동시 사용에 안전합니다.

## 링크

[Package context](https://golang.org/pkg/context)  
[Go Concurrency Patterns: Context](https://blog.golang.org/context) - Sameer Ajmani  
[Cancellation, Context, and Plumbing](https://vimeo.com/115309491) - Sameer Ajmani  
[Using contexts to avoid leaking goroutines](http://golang.rakyll.org/leakingctx/) -- Jaana Burcu Dogan  

## 코드 리뷰

[Store / Retrieve context values](example1/example1.go) ([Go Playground](https://play.golang.org/p/a3qXpFsQ8_))  
[WithCancel](example2/example2.go) ([Go Playground](https://play.golang.org/p/YfWzzfDqGu))  
[WithDeadline](example3/example3.go) ([Go Playground](https://play.golang.org/p/WVUdqD0Dan))  
[WithTimeout](example4/example4.go) ([Go Playground](https://play.golang.org/p/m4tdoGvn9i))  
[Request/Response](example5/example5.go) ([Go Playground](https://play.golang.org/p/rrIzSU6-H4))  

## 연습문제

### 연습문제 1

template를 사용해서 다음 지시를 따릅니다. mock 데이터베이스 호출을 수행하는 web handler를 작성할려고 합니다. 호출 시간이 너무 길면 context를 기반으로 timeout이 되도록 합니다. 상태를 context로 저장할 수 있습니다.

[Template](exercises/template1/template1.go) ([Go Playground](https://play.golang.org/p/T05C1L8Mu6)) | 
[Answer](exercises/exercise1/exercise1.go) ([Go Playground](https://play.golang.org/p/2L_DF8-pH7))  
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
