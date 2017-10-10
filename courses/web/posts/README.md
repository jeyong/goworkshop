## Web - Posts and Forms

POST 호출을 만들고 multipart form data 동작에 관한 내용을 알아봅시다.

## 노트

* 표준 라이브러리에서 service와 app을 만드는데 필요한 많은 것들을 제공하고 있습니다.
* `net/http` 패키지는 빌딩 블록을 제공합니다.
* 써드파티가 제공하는 다른 좋은 패키지들도 많이 있습니다.

## 링크

https://golang.org/pkg/net/http/  
https://golang.org/doc/articles/wiki/  

## 코드 리뷰

Basic POST: [Code](example1/main.go) | [Test](example1/main_test.go)  
Simple Form: [Code](example2/main.go) | [Test](example2/main_test.go)  
Structured Form Parsing: [Code](example3/main.go) | [Test](example3/main_test.go)  
Multipart Forms: [Code](example4/main.go) | [Test](example4/main_test.go)  

## 연습문제

### 연습문제 1

Take the multipart writer example and add support for a new form field that would specify the name of the folder to use for the uploaded image. If it does not exist use the current directory as the default. Then update the test to validate the code change.
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
