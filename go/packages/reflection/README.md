## Reflection - 표준 라이브러리

Reflection은 유도한 타입이나 다른 메타-데이터에 대한 값을 살펴볼 수 있는 기능입니다. 프로그램 내에서 타입이 다른 데이터와 동작하는 경우에도 엄청난 유연성을 제공합니다. 특히 데이터의 encoding/decoding에서 아주 중요한 역할을 합니다.  

## 노트

* reflection package는 타입을 살펴보는 것이 가능하다.
* 메타-데이터를 사용하고 저장하기 위해서 struct 필드에 "tags"를 추가할 수 있다.
* encoding package가 reflection을 사용한다.

## 링크

http://blog.golang.org/laws-of-reflection

## 코드 리뷰

### Interfaces

interface 값 내부에 저장한 struct 타입 값에 대해서 reflection을 사용하는 방법 예제. 
[Struct Types](interface/struct/struct.go) ([Go Playground](https://play.golang.org/p/kHC6nuHYty))  

interface 값 내부에 저장한 struct 타입 값의 slice에 대해서 reflection을 사용하는 방법 예제.
[Slices](interface/slice/slice.go) ([Go Playground](https://play.golang.org/p/UyRIlkjVjW))  

interface 값 내부에 저장한 struct 타입 값의 map에 대해서 reflection을 사용하는 방법 예제.
[Maps](interface/map/map.go) ([Go Playground](https://play.golang.org/p/-_niEdmavG))  

interface 값 내부에 저장한 struct 타입 포인터에 대해서 reflection을 사용하는 방법 예제.
[Pointers](interface/pointer/pointer.go) ([Go Playground](https://play.golang.org/p/itFSg3BL0o))  

### Tags

tag를 가지는 struct 타입에 대해서 reflection을 사용하는 방법 예제.
[Tags](tag/tag.go) ([Go Playground](https://play.golang.org/p/s6FE6J58Es))  

### Inspection / Decoding

struct 필드를 살펴보고 필드 이름, 타입, 값을 출력하는 방법 예제.
[Struct Types](inspect/struct/struct.go) ([Go Playground](https://play.golang.org/p/ahHLMtun9y))  

integer를 디코딩하기 위해서 reflection을 사용하는 방법 예제.
[Integers](inspect/integer/integer.go) ([Go Playground](https://play.golang.org/p/LmVkzpm57a))  

## 연습문제

### 연습문제 1
고객의 invoice 요청을 표현하는 struct 타입을 선언합니다. CustomerID와 InvoiceID 필드가 필요합니다. 요청이 유효한지 확인하는데 사용하는 tag를 정의합니다. ID가 유효하기 위해 사용하는 length와 range를 지정하는 tag를 정의합니다. validate라는 이름의 함수를 선언해서 특정 타입의 값을 받고 해당 tag를 처리하도록 합니다. 유효한지 결과를 출력합니다. 

[Template](exercises/template1/template1.go) ([Go Playground](http://play.golang.org/p/LKWPS9cN_n)) | 
[Answer](exercises/exercise1/exercise1.go) ([Go Playground](http://play.golang.org/p/pDTvc6jEjt))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
