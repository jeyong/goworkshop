## Web - Middleware

미들웨어를 사용하고 적용하는 방법에 대해서 배워봅니다.

## 노트

* 표준 라이브러리에서 service와 app을 만드는데 필요한 많은 것들을 제공하고 있습니다.
* http 패키지는 빌딩 블록을 제공합니다.
* 써드파티가 제공하는 다른 좋은 패키지들도 많이 있습니다.

## 링크

https://golang.org/pkg/net/http/  
https://golang.org/doc/articles/wiki/  
github.com/urfave/negroni  
github.com/justinas/alice  
github.com/gorilla/handlers  

## 코드 리뷰

Basic middleware: [Code](example1/main.go) | [Test](example1/main_test.go)  
Negroni router: [Code](example2/main.go) | [Test](example2/main_test.go)  
Alice with Gorilla Handlers: [Code](example3/main.go)  
Passing data with context: [Code](example4/main.go) | [Test](example4/main_test.go)  

## 연습문제

### 연습문제 1

Take the Negroni code from example 2 and extend the code by adding a new middleware handler to validate authentication. This call must happen before processing anything else. If authentication fails return a 500 and cancel the processing of the request. If authentication succeeds finish processing the rest of the handlers. Use a query string to cause authentication to succeed or fail.
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
