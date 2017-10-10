## Web - Posts and Forms

Learn the basics of making POST calls and working with multipart form data.

## 노트

* The standard library has much of what you need to build services and apps.
* The `net/http` package provides the building blocks.
* There are other great packages in the Go ecosystem to help.

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
