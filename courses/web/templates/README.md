## Web - Templates

template를 사용해서 마크업을 파싱하고 생성.

## 노트

* 표준 라이브러리에서 service와 app을 만드는데 필요한 많은 것들을 제공하고 있습니다.
* http 패키지는 빌딩 블록을 제공합니다.
* 써드파티가 제공하는 다른 좋은 패키지들도 많이 있습니다.

## 링크

https://golang.org/pkg/net/http/  
https://golang.org/doc/articles/wiki/  
https://github.com/GeertJohan/go.rice  

## 코드 리뷰

Basic Template: [Code](example1/main.go) | [Test](example1/main_test.go)  
Data Parsing: [Code](example2/main.go) | [Test](example2/main_test.go)  
Struct Parsing: [Code](example3/main.go) | [Test](example3/main_test.go)  
Escaping: [Code](example4/main.go) | [Test](example4/main_test.go)  
Escaping 2: [Code](example5/main.go) | [Test](example5/main_test.go)  
Complex Markup: [Code](example6/main.go) | [Test](example6/main_test.go)  
Serving Assets: [Code](example7/main.go) | [Test](example7/main_test.go)  
Bundling Assets: [Code](example8/main.go) | [Test](example8/main_test.go) | [Assets](example8/rice-box.go)  

## 연습문제

### 연습문제 1

Take the code from example 6 (Complex Markup) and add a map of key/value pairs that represents the user's roles. Then add a section to the template to render the set of roles a user has.
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
