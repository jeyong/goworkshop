## 동시성 패턴 (Concurrency Patterns)
goroutine과 channel로 생성할 수 있는 다양한 패턴이 있습니다. 그 중에서 중요한 패턴은 리소스 풀링(resource pooling)과 동시 검색(concurrent searching)입니다.

## 노트

* 동작 코드는 안정적인 동작을 보장하면서 goroutine들에게 작업을 할당하는 패턴을 제공한다.
* 리소스 풀링 코드는 goroutine을 생성하고 릴리즈하기에 필요한 리소스 관리할 수 있는 패턴을 제공한다.
* 검색 코드는 여러 goroutine들을 사용해서 동시에 수행하도록 하는 패턴을 제공합니다.

## 링크

https://github.com/gobridge/concurrency-patterns  
http://blog.golang.org/pipelines  
https://talks.golang.org/2012/concurrency.slide#1  
https://blog.golang.org/context  
http://blog.golang.org/advanced-go-concurrency-patterns  
http://talks.golang.org/2012/chat.slide  

Functional Options : type DialOption func(*dialOptions)  
https://github.com/grpc/grpc-go/blob/master/clientconn.go

## 코드 리뷰

[Chat](chat)  
[Logger](logger)  
[Task](task)  
[Pooling](pool)  
[Kit](https://github.com/ardanlabs/kit)
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.