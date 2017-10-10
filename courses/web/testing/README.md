## Web - Testing

Learn the basics of testing web services and applications in Go.

## 노트

* The standard library has a package named httptest with good support.
* There are several ways to create unit and integration tests in Go.

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
