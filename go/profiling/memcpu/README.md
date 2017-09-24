## Benchmark Profiling

벤치마크를 사용하면 프로그램을 프로파일링할 수 있고 정확한 성능이나 사용하는 메모리를 볼 수 있습니다.

## Profiling Commands

#### CPU Profiling

벤치마크를 수행합니다.

    $ go test -run none -bench . -benchtime 3s -benchmem -cpuprofile cpu.out

pprof 툴을 수행합니다.

    $ go tool pprof benchmarks.test cpu.out

pprof 명령을 수행합니다.

    (pprof) list algOne
    (pprof) web list algOne

_Note "syscall" 상태에 있는 goroutine은 OS thread를 사용하며, 다른 goroutine은 그렇지 않습니다.(runtime.LockOSThread에서 호출되는 goroutine은 제외되는데 프로파일에서 보이지 않기 때문) "IO wait" 상태에 있는 goroutine은 thread를 사용하지 않으며, non-blocking network poller에 둡니다.(나중에 goroutine을 unpark하기 위해서 epoll/kqueue/GetQueuedCompletionStatus를 사용합니다)_

#### Memory Profiling

벤치마크 수행합니다.

    $ go test -run none -bench . -benchtime 3s -benchmem -memprofile mem.out

pprof 툴을 실행합니다.

    $ go tool pprof -<PICK_MEM_PROFILE> benchmarks.test mem.out

pprof 명령을 실행합니다.

    (pprof) list algOne
    (pprof) web list algOne

memory 프로파일 옵션 내용

    // Useful to see current status of heap.
	-inuse_space  : Allocations live at the time of profile  	** default
	-inuse_objects: Number of bytes allocated at the time of profile

	// Useful to see pressure on heap over time.
	-alloc_space  : All allocations happened since program start
	-alloc_objects: Number of object allocated at the time of profile

메모리 사용을 줄이고자 한다면, 일반 프로그램 동작하는 동안 수집한 `-inuse_space` 프로파일을 살펴봅니다.

실행 속도를 개선하고자 한다면, 주요한 실행 시간이나 프로그램 종료시에 수집한 `-alloc_objects` 프로파일을 살펴봅니다.

## 코드 리뷰

[Profiling](stream.go) ([Go Playground](https://play.golang.org/p/n_SzF4Cer4)) |
[Profiling Test](stream_test.go) ([Go Playground](https://play.golang.org/p/TnXrxJVfLV))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
