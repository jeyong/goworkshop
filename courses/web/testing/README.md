## Web - Testing

web service와 어플리케이션을 테스팅하기

## 노트

* 표준 라이브러리 중에 httptest라는 패키지에서 지원하고 있습니다.
* 단위 테스트와 통합 테스트를 생성하는 여러 가지 방법이 있습니다.

## 링크

https://golang.org/pkg/net/http/  
https://golang.org/doc/articles/wiki/  

## 코드 리뷰

[Basic Unit Testing](example1/unit_test.go)  
[Using a http.Handler](example2/unit_test.go)  
[Testing Routes](example3/unit_test.go)  
[Mocking Servers](example4/integration_test.go)  

## 연습문제

### 연습문제 1

Write tests that exercise the different endpoints of the "Hello world" language
exercise from [the basics](../basics/README.md). Do this by combining the mux
with the defined routes with a `httptest.NewServer`.
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
