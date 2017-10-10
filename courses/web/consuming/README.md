## Web - Consuming Web APIs

web API를 사용하는 방법에 대해서 배워봅시다.

## 노트

* 표준 라이브러리에서 service와 app을 만드는데 필요한 많은 것들을 제공하고 있습니다.
* http 패키지는 빌딩 블록을 제공합니다.
* 써드파티가 제공하는 다른 좋은 패키지들도 많이 있습니다.

## 링크

https://golang.org/pkg/net/http/  
https://golang.org/doc/articles/wiki/  
github.com/dvsekhvalnov/jose2go  

## 코드 리뷰

Default HTTP support: [Test](example1/main_test.go)
POST calls: [Test](example2/main_test.go)
PUT calls: [Test](example3/main_test.go)
Client timeouts: [Test](example4/main_test.go)
Custom transporter: [Test](example5/main_test.go)
Signing requests with JSON Web Tokens: [Code](example6/main.go) | [Test](example6/main_test.go)
Canceling with Context: [Test](example7/main_test.go)

## 연습문제

### 연습문제 1

Call the GitHub API to get a list of contributors for the `ardanlabs/gotraining` repository.

* The API url is https://api.github.com/repos/ardanlabs/gotraining/contributors
* Docs for the API in general are https://developer.github.com/v3/
* Docs for the contributors endpoint are https://developer.github.com/v3/repos/#list-contributors
* To get around rate limiting you must generate a personal access token at https://github.com/settings/tokens

[Exercise Template](exercises/template1/main.go)  
[Exercise Answer](exercises/exercise1/main.go)

___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
