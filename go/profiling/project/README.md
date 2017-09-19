## 대규모 웹 서비스 프로파일링하기

웹 서비스를 확장하는 웹 어플리케이션이 있다면 이 어플리케이션을 이용해서 프로파일링하고 어떻게 동작하는지 이해하도록 해봅시다.

### 프로젝트 빌드 및 실행

프로파일링에 대해서 좀더 익히고 경험해 볼 수 있는 웹사이트로 RSS 피드용 검색 엔진 프로젝트가 있습니다.

웹사이트를 실행하고 동작을 검증합니다.

	$ go build
	$ ./project

	http://localhost:5000/search

### load 추가하기

서비스에 load를 추가하기 위해서 프로파일링을 실행하는 동안 다음 명령을 실행할 수 있습니다.

	// Send 10k request using 100 connections.
	$ hey -m POST -c 100 -n 10000 "http://localhost:5000/search?term=trump&cnn=on&bbc=on&nyt=on"

### GODEBUG

#### GC Trace

null 장치로 stdout(logs)를 리다이렉팅하는 웹사이트를 실행합니다. 런타임으로부터 trace 정보를 볼 수 있습니다.

	$ GODEBUG=gctrace=1 ./project > /dev/null

#### GOGC

GOGC는 heap이 커지는 방식을 변경합니다. 이 값을 변경시키면 발생하는 GC의 수를 감소시킬 수 있습니다.

다시 load를 추가해서 웹사이트 실행합니다. GOGC 값을 달리해서 GC의 페이스를 살펴봅니다.

	$ GODEBUG=gctrace=1 ./project > /dev/null  
	$ GODEBUG=gctrace=1 GOGC=200 ./project > /dev/null  
	$ GODEBUG=gctrace=1 GOGC=500 ./project > /dev/null

#### Scheduler Trace

null 장치로 stdout(logs)를 리다이렉팅하는 웹사이트를 실행합니다. 런타임으로부터 trace 정보를 볼 수 있습니다.

	$ GODEBUG=schedtrace=1000 ./project > /dev/null

### PPROF

이미 다음과 같은 import를 추가하였으므로, 웹 서비스에 프로파일링 라우트를 포함할 수 있습니다.

	import _ "net/http/pprof"

#### Raw http/pprof

새로운 endpoint의 기본 프로파일링 상태를 살펴봅니다.

	http://localhost:5000/debug/pprof

heap 프로파일을 캡쳐:

	http://localhost:5000/debug/pprof/heap

cpu 프로파일을 캡쳐:

	http://localhost:5000/debug/pprof/profile

#### Interactive Profiling

Go pprof tool을 실행해서 heap 정보를 리뷰하기

	$ go tool pprof -alloc_space ./project http://localhost:5000/debug/pprof/heap

메모리 프로파일 옵션 문서.

    // Useful to see current status of heap.
	-inuse_space  : Allocations live at the time of profile  	** default
	-inuse_objects: Number of bytes allocated at the time of profile

	// Useful to see pressure on heap over time.
	-alloc_space  : All allocations happened since program start
	-alloc_objects: Number of object allocated at the time of profile

메모리 사용량을 줄이기 원한다면, 일반적인 프로그램 동작 동안 모은 `-inuse_space` 프로파일을 살펴봅니다.

실행 속도를 개선하기 위해서는 주요 실행 시간이나 프로그램 끝난 후에 수집한 `-alloc_objects` 프로파일을 살펴봅니다.

Go pprof tool을 실행해서 cpu 정보를 리뷰합니다.

	$ go tool pprof ./project http://localhost:5000/debug/pprof/profile

_Note that goroutines in "syscall" state consume an OS thread, other goroutines do not (except for goroutines that called runtime.LockOSThread, which is, unfortunately, not visible in the profile). Note that goroutines in "IO wait" state also do not consume threads, they are parked on non-blocking network poller (which uses epoll/kqueue/GetQueuedCompletionStatus to unpark goroutines later)._

Explore using the **top**, **list**, **web** and **web list** commands.

#### Comparing Profiles

Take a snapshot of the current heap profile. Then do the same for the cpu profile.

    $ curl -s http://localhost:5000/debug/pprof/heap > base.heap

After some time, take another snapshot:

    $ curl -s http://localhost:5000/debug/pprof/heap > current.heap

Now compare both snapshots against the binary and get into the pprof tool:

    $ go tool pprof -inuse_space -base base.heap memory_trace current.heap

#### Flame Graphs

Go-Torch is a tool for stochastically profiling Go programs. Collects stack traces and synthesizes them into a flame graph.

	https://github.com/uber/go-torch

Put some load of the web application and run the torch tool and visualize the profile.

	$ go-torch -u http://localhost:5000/

### Benchmark Profiling

Run the benchmarks and produce a cpu and memory profile.

	$ cd $GOPATH/src/github.com/ardanlabs/gotraining/topics/go/profiling/project/search

	$ go test -run none -bench . -benchtime 3s -benchmem -cpuprofile cpu.out
	$ go tool pprof ./search.test cpu.out
	(pprof) web list rssSearch

	$ go test -run none -bench . -benchtime 3s -benchmem -memprofile mem.out
	$ go tool pprof -inuse_space ./search.test mem.out
	(pprof) web list rssSearch

### Trace Profiles

#### Trace Web Application

Capture a trace file for a brief duration.

	$ curl -s http://localhost:5000/debug/pprof/trace?seconds=2 > trace.out

Run the Go trace tool.

	$ go tool trace trace.out

Use the RSS Search test instead to create a trace.

	$ cd $GOPATH/src/github.com/ardanlabs/gotraining/topics/go/profiling/project/search
	$ go test -run none -bench . -benchtime 3s -trace trace.out
	$ go tool trace trace.out

## Expvar

Package expvar provides a standardized interface to public variables, such as operation counters in servers. It exposes these variables via HTTP at /debug/vars in JSON format.

### Adding New Variables

	import "expvar"

	// expvars is adding the goroutine counts to the variable set.
	func expvars() {

		// Add goroutine counts to the variable set.
		gr := expvar.NewInt("Goroutines")
		go func() {
			for _ = range time.Tick(time.Millisecond * 250) {
				gr.Set(int64(runtime.NumGoroutine()))
			}
		}()
	}

	// main is the entry point for the application.
	func main() {
		expvars()
		service.Run()
	}

### Expvarmon

TermUI based Go apps monitor using expvars variables (/debug/vars). Quickest way to monitor your Go app.

	$ go get github.com/divan/expvarmon

Running expvarmon

	$ expvarmon -ports=":5000" -vars="requests,goroutines,mem:memstats.Alloc"
