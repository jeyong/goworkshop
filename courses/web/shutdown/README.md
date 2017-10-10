## Web - Shutdown

Learn how to gracefully shut a server down.

## 노트

Since 1.8 the `Server` from `net/http` package has built in support for graceful shutdown. Prior to 1.8 use `github.com/braintree/manners`.

## 링크

https://golang.org/pkg/net/http/  
https://github.com/rakyll/hey  

## 코드 리뷰

[Graceful Shutdown](example1/main.go)  

## 연습문제

### 연습문제 1

Use `hey` to generate load against the server in example 1. Close the server with ctrl-c while `hey` is running. Change the timeout value in the shutdown code to 100 milliseconds and repeat the exercise.
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
