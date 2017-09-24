## Blocking Profiling

Testing과 Tracing을 통해서 blocking profiles을 볼 수 있습니다.

## Blocking Profile 기반 테스트 수행

test를 수행해서 blocking profile을 얻을 수 있습니다.

테스트를 수행해서 block profile를 생성.

	$ go test -blockprofile block.out

blocking profile을 보기 위해서 pprof 툴을 실행합니다.

	$ go tool pprof blocking.test block.out

TestLatency 함수를 리뷰합니다.

	$ list TestLatency

## Trace 수행

go test tool로 **-trace trace.out** 옵션을 사용한 테스트가 있어야 합니다.

test를 실행해서 trace를 생성합니다.

	$ go test -trace trace.out

trace를 리뷰하기 위해서 trace tool을 실행합니다.

	$ go tool trace trace.out

## 링크


## 코드 리뷰

[Blocking Trace](blocking_test.go) ([Go Playground](https://play.golang.org/p/cjqIVeAwHz))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
