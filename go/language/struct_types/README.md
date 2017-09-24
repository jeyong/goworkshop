## Struct Types

Struct 타입은 복잡한 타입을 생성하는 방법으로 데이터의 필드들을 그룹으로 묶습니다. 프로그램에서 사용하는 데이터의 구조화하고 공유하는 좋은 방식입니다.

컴퓨터 구조의 잠재적인 성능은 word의 길이(access마다 처리할 수 있는 bit의 수)에 절대적으로 의존합니다. 더 중요한 것은 메모리 사이즈나 word의 갯수입니다. 

## 노트

* struct 타입으로부터 값을 초기화하기 위해서 struct literal 형태를 사용할 수 있습니다.
* (.) 오퍼레이터로 개별 필드 값에 접근할 수 있습니다. 
* 익명 struct를 만들 수도 있습니다.

## 링크

http://www.goinggo.net/2013/07/understanding-type-in-go.html  
http://www.goinggo.net/2013/07/object-oriented-programming-in-go.html  
http://dave.cheney.net/2015/10/09/padding-is-hard  
http://www.geeksforgeeks.org/structure-member-alignment-padding-and-data-packing  
http://www.catb.org/esr/structure-packing

## 코드 리뷰

[Declare, create and initialize struct types](example1/example1.go) ([Go Playground](https://play.golang.org/p/TEmOrIxl_P))  
[Anonymous struct types](example2/example2.go) ([Go Playground](https://play.golang.org/p/x-Dpp9Ts_U))  
[Named vs Unnamed types](example3/example3.go) ([Go Playground](https://play.golang.org/p/QREkSIDAuW))

## 고급 코드 리뷰

[Struct type alignments](advanced/example1/example1.go) ([Go Playground](https://play.golang.org/p/nwOX0grify))

## 연습문제

### 연습문제 1

**Part A:** 사용자 정보(name, email, age)를 저장하기 위한 struct 타입을 선언합니다. 이 타입의 값을 생성하고 값으로 초기화하고 각 필드를 출력합니다.

**Part B:** 익명 struct 타입을 선언하고 초기화합니다. 동일한 3개 필드를 가지도록 합니다. 값을 출력합니다.

[Template](exercises/template1/template1.go) ([Go Playground](http://play.golang.org/p/PvQKHgf9jZ)) | 
[Answer](exercises/exercise1/exercise1.go) ([Go Playground](http://play.golang.org/p/8CtSrnTp-1))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
