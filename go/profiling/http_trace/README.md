## HTTP Tracing

Go 1.7에서 HTTP client request의 주기동안 세부 정보를 모으는 것을 쉽게하기 위해서 HTTP tracing package를 도입했습니다. HTTP tracing에 대한 지원은 net/http/httptrace package에서 제공합니다. 수집한 정보는 디버깅 지연 문제, 서비스 모니터링, adaptive 시스템 작성 등에 사용할 수 있습니다.

## 노트

httptrace package는 HTTP round trip 동안 다양한 event에 대해서 정보를 수집하기 위해서 많은 hooks을 제공합니다. 이는 event는 다음을 포함합니다 :

* Connection 생성
* Connection 재사용
* DNS lookups
* request 작성
* response 읽기

## Links

[Introducing HTTP Tracing](https://blog.golang.org/http-tracing) - Jaana Burcu Dogan  

## Code Review

[Tracing events](example1/example1.go) ([Go Playground](https://play.golang.org/p/du_s3LRX1s))  
[Tracing with http.Client](example2/example2.go) ([Go Playground](https://play.golang.org/p/CNPz8tjnYj))  

## Exercises

### Exercise 1

TBD
___
All material is licensed under the [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0).
