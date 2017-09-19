## 동시성 패턴 (Concurrency Patterns)
There are lots of different patterns we can create with goroutines and channels. Two interesting patterns are resource pooling and concurrent searching.

## 노트

* The work code provides a pattern for giving work to a set number of goroutines without losing the guarantee.
* The resource pooling code provides a pattern for managing resources that goroutines may need to acquire and release.
* The search code provides a pattern for using multiple goroutines to perform concurrent work.

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