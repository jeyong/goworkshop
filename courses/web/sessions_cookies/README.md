## Web - Sessions and Cookies

web 어플리케이션에서 session과 cookies의 동작에 대해서 배워봅시다.

## 노트

* 표준 라이브러리에서 service와 app을 만드는데 필요한 많은 것들을 제공하고 있습니다.
* http 패키지는 빌딩 블록을 제공합니다.
* 써드파티가 제공하는 다른 좋은 패키지들도 많이 있습니다.

## 링크

https://golang.org/pkg/net/http/  
https://golang.org/doc/articles/wiki/  
https://github.com/gorilla/sessions  

## 코드 리뷰

Using Session: [Code](example1/main.go) | [Test](example1/main_test.go)  
Using Cookies: [Code](example2/main.go) | [Test](example2/main_test.go)  

## 연습문제

### 연습문제 1

Take the session example and add support for storing the persons phone number. Save the information in session and make sure it can be retrieved. Then update the tests to validate this is working.
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
