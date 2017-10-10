## Web - TLS

Learn about securing your application using TLS.

## 노트

* Usually apps just listen for HTTP and offload TLS termination to a load balancer like Caddy or Nginx.
* The net/http package provides support for TLS if you really need it
* The crypto/tls package comes with a program for generating self signed certificates

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
