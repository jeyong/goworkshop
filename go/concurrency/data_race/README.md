## Data Races

data race는 2개 이상의 goroutine이 동일한 리소스에 동시에 읽기나 쓰기를 시도하는 경우입니다. race 조건은 완전히 랜덤하게 발생하여 버그가 될 수 있고 데이터를 오염시키지만 드러나지 않을 수 있습니다. atomic 함수와 mutex는 goroutine들 사이에서 공유 리소스에 접근을 동기화시키는 방식입니다.

## 노트

* goroutine들을 순서를 조정하여 동기화가 필요하다.
* 2개 이상 goroutine이 동일 리소스에 접근하고자 하는 경우에 data race가 된다.
* atomic 함수와 mutex는 필요한 지원을 제공한다.

## Cache Coherency and False Sharing
아래 정보는 2014년에 Dive에서 Scott Meyers가 이야기한 내용:

[CPU Caches를 왜 신경써야하나 (30:09-38:30)](https://youtu.be/WDIkqP4JbkE?t=1809)  
[Code Example](../../testing/benchmarks/falseshare/README.md)

![figure1](figure1.png)

## Cache Coherency와 False Sharing 노트

* Thread memory access matters.
* If your algorithm is not scaling look for false sharing problems.

## 링크

[False Sharing 제거하기](http://www.drdobbs.com/parallel/eliminate-false-sharing/217500206)

[The Go Memory Model](https://golang.org/ref/mem)  
http://blog.golang.org/race-detector  
http://www.goinggo.net/2013/09/detecting-race-conditions-with-go.html  
https://golang.org/doc/articles/race_detector.html

## 다이어그램

### 예제1에서의 Data Race 관점

![](data_race.png)

## 코드 리뷰

[Data Race](example1/example1.go) ([Go Playground](https://play.golang.org/p/yXiOONCG-2))  
[Atomic Increments](example2/example2.go) ([Go Playground](https://play.golang.org/p/SbWFzQT1zu))  
[Mutex](example3/example3.go) ([Go Playground](https://play.golang.org/p/_4TYRcZ2vP))  
[Read/Write Mutex](example4/example4.go) ([Go Playground](https://play.golang.org/p/uMU7Crx6ZY))

## 고급 코드 리뷰

[Interface Based Race Condition](advanced/example1/example1.go) ([Go Playground](https://play.golang.org/p/m08N8yYlpr))

## 연습문제

### 연습문제 1
다음 프로그램에서 race detector를 사용해서 data race 찾고 이를 수정하세요.

	// https://play.golang.org/p/F5DCJTZ6Lm

	// Fix the race condition in this program.
	package main

	import (
		"fmt"
		"math/rand"
		"sync"
		"time"
	)

	// numbers maintains a set of random numbers.
	var numbers []int

	// init is called prior to main.
	func init() {
		rand.Seed(time.Now().UnixNano())
	}

	// main is the entry point for the application.
	func main() {
		// Number of goroutines to use.
		const grs = 3

		// wg is used to manage concurrency.
		var wg sync.WaitGroup
		wg.Add(grs)

		// Create three goroutines to generate random numbers.
		for i := 0; i < grs; i++ {
			go func() {
				random(10)
				wg.Done()
			}()
		}

		// Wait for all the goroutines to finish.
		wg.Wait()

		// Display the set of random numbers.
		for i, number := range numbers {
			fmt.Println(i, number)
		}
	}

	// random generates random numbers and stores them into a slice.
	func random(amount int) {
		// Generate as many random numbers as specified.
		for i := 0; i < amount; i++ {
			n := rand.Intn(100)
			numbers = append(numbers, n)
		}
	}

[Template](exercises/template1/template1.go) ([Go Playground](http://play.golang.org/p/G7_rJAK8YR)) | 
[Answer](exercises/exercise1/exercise1.go) ([Go Playground](http://play.golang.org/p/GC12H2acgO))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
