## Maps

map은 자료구조로 key/value 쌍의 데이터를 저장 및 관리하는데 사용합니다.

## 노트

* map은 key/value 쌍을 저장하고 꺼내오는 방식을 제공합니다.
* map key는 할당 구문에서 사용할 수 있는 값이여야만 합니다.
* map에서 Iterating에서 순서는 random입니다.

## 링크

http://blog.golang.org/go-maps-in-action  
http://www.goinggo.net/2013/12/macro-view-of-map-internals-in-go.html  
[Keith Randall - Inside the Map Implementation](https://www.youtube.com/watch?v=Tl7mi9QmLns)

## 코드 리뷰

[Declare, initialize and iterate](example1/example1.go) ([Go Playground](https://play.golang.org/p/EHfkoipKYF))  
[Map literals and delete](example2/example2.go) ([Go Playground](https://play.golang.org/p/B2klwmqmPZ))  
[Map key restrictions](example3/example3.go) ([Go Playground](https://play.golang.org/p/LZRHA7FG6s))  

## 연습문제

### 연습문제 1

key와 value로 각각 string과 integer를 가지는 map을 선언해서 생성합니다. 5개 값을 가지는 map을 만들고 iterator를 통해서 map의 key/value 쌍을 출력합니다.

[Template](exercises/template1/template1.go) ([Go Playground](https://play.golang.org/p/E2VFcOY1o6)) |
[Answer](exercises/exercise1/exercise1.go) ([Go Playground](https://play.golang.org/p/uT_pwbOgNc))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
