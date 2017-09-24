## Embedding

타입들 사이에서 state와 behavior를 공유하고 재사용하는 방식. inner type promotion을 사용해서 inner type의 field와 method는 outer type의 참조로 바로 접근이 가능하다.

## 노트

* type들 사이에서 state나 behavior를 공유하는 방식 제공
* inner type은 자신의 고유한 특징을 절대 잃지 않는다.
* 상속이 아니다.
* promotion을 통해서 inner type의 field와 method는 outer type을 통해서 접근할 수 있다.
* outer type은 inner type의 behavior를 override할 수 있다.

## 링크

http://www.goinggo.net/2014/05/methods-interfaces-and-embedded-types.html

## 코드 리뷰

[Fields 선언](example1/example1.go) ([Go Playground](https://play.golang.org/p/VlB7DYptWo))  
[Embedding types](example2/example2.go) ([Go Playground](https://play.golang.org/p/7Ei_9niqPQ))  
[Embedded types과 interfaces](example3/example3.go) ([Go Playground](https://play.golang.org/p/zD8RFvJ3m5))  
[Outer와 inner type interface 구현](example4/example4.go) ([Go Playground](https://play.golang.org/p/5NyvAgU__u))

## 연습문제

### 연습문제 1

template 코드를 복사합니다. sports 타입을 임베드하는 hockey라는 새로운 타입을 선언합니다. hockey에 대해서 matcher 인터페이스를 구현합니다. hockey의 match method를 구현할 때, 먼저 embedded filed를 검사하기 위해서 embedded sport type의 match method를 호출합니다. 다음으로 matcher의 slice 내부에 2개 hockey value를 생성하고 search를 수행합니다.

[Template](exercises/template1/template1.go) ([Go Playground](https://play.golang.org/p/dK0FnSnnRz)) |
[Answer](exercises/exercise1/exercise1.go) ([Go Playground](https://play.golang.org/p/ZeOIYmIw-r))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
