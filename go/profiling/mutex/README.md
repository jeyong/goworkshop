## Mutex Profiling

Testing과 Tracing으로 mutex 프로파일을 볼 수 있습니다.

## Mutex 프로파일 기반 테스트 실행

테스트를 실행해서 mutex 프로파일을 얻을 수 있습니다.

테스트를 실행해서 mutex 프로파일을 생성합니다.

	$ go test -mutexprofile mutex.out

pprof tool을 실행해서 mutex 프로파일을 볼 수 있습니다.

	$ go tool pprof mutex.test mutex.out

TestMutexProfile 함수를 살펴봅니다.

	$ list TestMutexProfile

## Links

[Mutex profile](https://rakyll.org/mutexprofile) - Burcu Dogan  

## Code Review

[Mutex Trace](mutex_test.go) ([Go Playground](https://play.golang.org/p/P1eOVX6D7u))
___
All material is licensed under the [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0).
