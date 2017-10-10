## Web - Shutdown

안전하게 서버 셧다운하기

## 노트

1.8부터는 `net/http` 패키지에 `Server`가 빌트인으로 셧다운을 지원합니다. 1.8 이전 버전인 경우에는 `github.com/braintree/manners` 을 사용합니다.

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
