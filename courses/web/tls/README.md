## Web - TLS

TLS를 사용해서 안전한 어플리케이션 개발하기

## 노트

* 일반적으로 app은 HTTP를 listen하고 Caddy나 Nginx와 같은 로드 밸랜싱을 담당하는 것이 TLS를 종료합니다.
* 여러분이 정말 필요한 경우에는 net/http 패키지의 TLS를 이용합니다.
* crypto/tls 패키지에는 self signed certificates를 생성하는 프로그램이 포함되어 있습니다.

    go run /usr/local/go/src/crypto/tls/generate_cert.go --host localhost

## 링크

https://golang.org/pkg/net/http/  
https://golang.org/pkg/crypto/tls/  
https://golang.org/x/crypto/acme/autocert/  
https://caddyserver.com/  

## 코드 리뷰

TLS support: [Code](example1/main.go)
Automatic TLS with ACME via LetsEncrypt: [Code](example2/main.go)

## 연습문제

### 연습문제 1

TBD
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
