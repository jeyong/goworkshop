## Goroutines

Goroutine은 함수로서 Go 스케쥴러가 독립적으로 실행할 수 있도록 생성 및 스케쥴링을 수행합니다. Go 스케쥴러가 goroutine들을 관리하고 실행을 책임집니다.

## 노트

* Goroutine은 함수이며 독립적으로 실행되도록 스케쥴링됩니다.
* 실행 중인 goroutine들의 정보를 항상 유지해야 하고 정상적으로 shutdown할 수 있어야 한다.
* 동시성은 병렬성이 아니다.(Concurrency is not parallelism)
	* 동시성(Concurrency)은 동시에 여러 일을 다루는(dealing)는 것이다.
	* 병렬성은 동시에 여러 일을 실행(doing)하는 것이다.

## 디자인 가이드라인

* 동시성 관련 [디자인 가이드라인](../../#concurrent-software-design)

## 다이어그램

### 스케쥴러가 동작하는 방식

![](scheduler.png)

### 동시성과 병렬성의 차이 (concurrency vs. parallelism)

![](parallel.png)

## 링크

http://blog.golang.org/advanced-go-concurrency-patterns  
http://blog.golang.org/context  
http://blog.golang.org/concurrency-is-not-parallelism  
http://talks.golang.org/2013/distsys.slide  
[Go 1.5 GOMAXPROCS Default](https://docs.google.com/document/d/1At2Ls5_fhJQ59kDK2DFVhFu3g5mATSXqqV5QrxinasI/edit)  
http://www.goinggo.net/2014/01/concurrency-goroutines-and-gomaxprocs.html  
[The Linux Scheduler: a Decade of Wasted Cores](http://www.ece.ubc.ca/~sasha/papers/eurosys16-final29.pdf)  
[Explanation of the Scheduler](https://news.ycombinator.com/item?id=12460807)  
[15 Years of Concurrency](http://joeduffyblog.com/2016/11/30/15-years-of-concurrency/) - Joe Duffy  
[golang 스케쥴러는 어떻게 동작할까?](https://www.quora.com/How-does-the-golang-scheduler-work/answer/Ian-Lance-Taylor) - Ian Lance Taylor  

## 코드 리뷰

[Goroutines과 동시성](example1/example1.go) ([Go Playground](https://play.golang.org/p/eV4l2JqLZL))  
[Goroutine time slicing](example2/example2.go) ([Go Playground](https://play.golang.org/p/8NwVeZG6IB))  
[Goroutines과 병렬성](example3/example3.go) ([Go Playground](https://play.golang.org/p/5A0VFp03vb))  

## 연습문제

### 연습문제 1

**Part A** 2개 익명 함수를 선언하는 프로그램을 작성합니다. 하나는 100부터 0까지 카운트 다운하고 다른 하나는 0부터 100까지 카운트 업합니다. 각 goroutine에 대해서 개별 식별자로 각 수를 출력합니다. 다음으로 이 함수들로부터 goroutine을 새엇ㅇ하고 goroutine이 완료될 때까지 main이 return되지 않도록 합니다.

**Part B** 이 프로그램을 병렬로 실행시켜 봅시다.

[Template](exercises/template1/template1.go) ([Go Playground](https://play.golang.org/p/kjtlMXkAAv)) | 
[Answer](exercises/exercise1/exercise1.go) ([Go Playground](https://play.golang.org/p/pUV-FPd3CE))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
