## Web - Muxers/Routers

가장 널리 알려진 router들과 routing을 지원에 대해서 알아봅시다.

## 노트

* 표준 라이브러리에서 service와 app을 만드는데 필요한 많은 것들을 제공하고 있습니다.
* http 패키지는 빌딩 블록을 제공합니다.
* 써드파티가 제공하는 다른 좋은 패키지들도 많이 있습니다.

## 링크

https://golang.org/pkg/net/http/  
https://golang.org/doc/articles/wiki/  
github.com/gorilla/pat  
github.com/julienschmidt/httprouter  
github.com/labstack/echo  

## 코드 리뷰

Pat router: [Code](example1/main.go) | [Test](example1/main_test.go)  
Httprouter router: [Code](example2/main.go) | [Test](example2/main_test.go)  
Echo router: [Code](example3/main.go) | [Test](example3/main_test.go)  

## 연습문제

### 연습문제 1

Take the CRUD code from example 1 (Pat) and extend the code by adding a `PUT` and `DELETE` route. Make sure the routes for both calls ask for the `id` of the customer. Write two new handler functions and bind them into the service so they can be processed. Finally add tests to validate the new routes are working. For both calls redirect the user back to the index page.
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
