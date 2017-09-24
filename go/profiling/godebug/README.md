## GODEBUG

GODEBUG 환경 변수를 사용해서 heap, gc, 스케쥴러에 관한 구체적인 정보를 얻을 수 있습니다. 변경이 일어나면 해당 스케쥴이 논리 프로세서의 상태에 관한 정보를 발생하게 합니다.

## Schedule Tracing

	$ export GODEBUG=schedtrace=1000

	*scheddetail*: setting schedtrace=X and scheddetail=1 causes the scheduler to emit
	detailed multiline info every X milliseconds, describing state of the scheduler,
	processors, threads and goroutines.

	*schedtrace*: setting schedtrace=X causes the scheduler to emit a single line to standard
	error every X milliseconds, summarizing the scheduler state.

	SCHED 1009ms: gomaxprocs=1 idleprocs=0 threads=3 spinningthreads=0 idlethreads=1 runqueue=0 [4 4]

		gomaxprocs=1:  Contexts configured.
		idleprocs=0:   Contexts not in use. Goroutine running.
		threads=3:     Threads in use.
		idlethreads=0: Threads not in use.
		runqueue=0:    Goroutines in the global queue.
		[4 4]:         Goroutines in each of the logical processors.

### Scheduler Trace 생성하기

단일 논리 프로세서를 사용한 예제 프로그램을 빌드하고 실행합니다.

	$ go build
	$ GOMAXPROCS=1 GODEBUG=schedtrace=1000 ./godebug

웹 어플리케이션의 load를 주고

	$ hey -m POST -c 8 -n 1000000 "http://localhost:4000/sendjson"

논리 프로세서에 load를 살펴봅니다. 실행가능한 goroutine만 볼 수 있습니다. 5초 후에 trace에 더 이상의 goroutine은 보이지 않습니다.

    SCHED 8047ms: gomaxprocs=1 idleprocs=0 threads=4 spinningthreads=0 idlethreads=1 runqueue=0 [62]
    SCHED 9056ms: gomaxprocs=1 idleprocs=0 threads=4 spinningthreads=0 idlethreads=1 runqueue=32 [0]
    SCHED 10065ms: gomaxprocs=1 idleprocs=1 threads=4 spinningthreads=0 idlethreads=1 runqueue=0 [0]
    SCHED 11068ms: gomaxprocs=1 idleprocs=1 threads=4 spinningthreads=0 idlethreads=1 runqueue=0 [0]


예제 프로그램의 leak goroutine을 실행합니다.

	$ GOMAXPROCS=1 GODEBUG=schedtrace=1000 ./godebug leak

웹 어플리케이션의 load를 주고

	$ hey -m POST -c 8 -n 1000000 "http://localhost:4000/sendjson"

논리 프로세서의 load를 살펴봅니다. 실행가능한 goroutine만 볼 수 있습니다. 5초 후에 trace에서 goroutine을 볼 수 있습니다.

    SCHED 13074ms: gomaxprocs=1 idleprocs=0 threads=5 spinningthreads=0 idlethreads=1 runqueue=0 [37]
    SCHED 14084ms: gomaxprocs=1 idleprocs=1 threads=5 spinningthreads=0 idlethreads=1 runqueue=0 [0]
    SCHED 15091ms: gomaxprocs=1 idleprocs=1 threads=5 spinningthreads=0 idlethreads=1 runqueue=0 [0]
    SCHED 16097ms: gomaxprocs=1 idleprocs=0 threads=5 spinningthreads=0 idlethreads=1 runqueue=129 [225]

이제 2개 논리 프로세서로 실행합니다:

	$ GOMAXPROCS=2 GODEBUG=schedtrace=1000 ./godebug

## Memory Tracing

코드로는 leak가 발생했는데 확인할 수 있는 특별한 방법이 없습니다. 메모리 leak이 있는지를 검증하고 어떤 함수나 메소드가 생성시키는질를 확인할 수 있습니다.

**gctrace=1** 설정하면 gc가 표준 error로 하나의 라인을 출력하도록 하며, collect한 메모리의 양과 pause의 길이를 요약해줍니다. gctrace=2 설정은 동일한 요약을 제공하며 각 collection을 되풀이 합니다. 이 라인의 포맷은 변경될 가능성이 높습니다:

    $ export GODEBUG=gctrace=1

    gc # @#s #%: #+...+# ms clock, #+...+# ms cpu, #->#-># MB, # MB goal, # P

필드는 다음과 같습니다:

    gc #        the GC number, incremented at each GC
    @#s         time in seconds since program start
    #%          percentage of time spent in GC since program start
    #+...+#     wall-clock/CPU times for the phases of the GC
    #->#-># MB  heap size at GC start, at GC end, and live heap
    # MB goal   goal heap size
    # P         number of processors used

**wall-clock** time은 시작부터 종료까지 실제 경과 시간을 측정합니다. 여기에는 지연시간이나 리소스를 위해 대기하는 시간까지도 포함됩니다.
https://en.wikipedia.org/wiki/Wall-clock_time

**CPU time** (혹은 프로세스 time)은 CPU가 프로그램 명령을 수행하는데 사용한 시간의 양 혹은 OS가 저전력(idle)모드나 I/O 연산을 기다리는 시간의 양을 말합니다.
https://en.wikipedia.org/wiki/CPU_time

**gcpacertrace=1** flag를 추가하면 보다 상세한 정보를 얻을 수 있습니다. 이렇게 하면 gc가 동시성 pacer의 내부 상태에 관한 정보를 출력하게 합니다.

    $ export GODEBUG=gctrace=1,gcpacertrace=1

동일 출력:

    gc 5 @0.071s 0%: 0.018+0.46+0.071 ms clock, 0.14+0/0.38/0.14+0.56 ms cpu, 29->29->29 MB, 30 MB goal, 8 P
    pacer: sweep done at heap size 29MB; allocated 0MB of spans; swept 3752 pages at +6.183550e-004 pages/byte
    pacer: assist ratio=+1.232155e+000 (scan 1 MB in 70->71 MB) workers=2+0
    pacer: H_m_prev=30488736 h_t=+2.334071e-001 H_T=37605024 h_a=+1.409842e+000 H_a=73473040 h_g=+1.000000e+000 H_g=60977472 u_a=+2.500000e-001 u_g=+2.500000e-001 W_a=308200 goalΔ=+7.665929e-001 actualΔ=+1.176435e+000 u_a/u_g=+1.000000e+000

노트:

		C++에서 memory leak은 참조하는 메모리를 읽어버린 경우
		Go에서 memory leak은 참조하는 메모리를 보유하는 경우   

### GC Trace 생성

예제 프로그램을 빌드하고 실행합니다.

    $ go build
    $ GODEBUG=gctrace=1 ./godebug

웹 어플리케이션에 load를 주고

    $ hey -m POST -c 8 -n 1000000 "http://localhost:4000/sendjson"

gc trace를 살펴봅니다.

    gc 318 @36.750s 0%: 0.022+0.27+0.040 ms clock, 0.13+0.60/0.43/0.031+0.24 ms cpu, 4->4->0 MB, 5 MB goal, 8 P
    gc 319 @36.779s 0%: 0.019+0.24+0.035 ms clock, 0.15+0.43/0.26/0+0.28 ms cpu, 4->4->0 MB, 5 MB goal, 8 P
    gc 320 @36.806s 0%: 0.023+0.34+0.035 ms clock, 0.18+0.63/0.49/0.014+0.28 ms cpu, 4->4->0 MB, 5 MB goal, 8 P
    gc 321 @36.834s 0%: 0.026+0.20+0.044 ms clock, 0.18+0.50/0.34/0.001+0.31 ms cpu, 4->4->0 MB, 5 MB goal, 8 P
    gc 322 @36.860s 0%: 0.022+0.29+0.055 ms clock, 0.13+0.54/0.47/0+0.33 ms cpu, 4->4->0 MB, 5 MB goal, 8 P

    gc 318      : First GC run since program started.
    @36.750s    : Nine milliseconds since the program started.
    0%          : One percent of the programs time has been spent in GC.

    // wall-clock
    0.022ms     : **STW** Sweep termination - Wait for all Ps to reach a GC safe-point.
    0.27ms      : Mark/Scan
    0.040ms     : **STW** Mark termination - Drain any remaining work and perform housekeeping.

    // CPU time
    0.13ms      : **STW** Sweep termination - Wait for all Ps to reach a GC safe-point.
    0.60ms      : Mark/Scan - Assist Time (GC performed in line with allocation)
    0.43ms      : Mark/Scan - Background GC time
    0.031ms     : Mark/Scan - Idle GC time
    0.24ms      : **STW** Mark termination - Drain any remaining work and perform housekeeping.

    4MB         : Heap size at GC start
    4MB         : Heap size at GC end
    0MB         : Live Heap
    5MB         : Goal heap size
    8P          : Number of logical processors

## 링크

[Tour of Go's env variables](http://dave.cheney.net/2015/11/29/a-whirlwind-tour-of-gos-runtime-environment-variables)   
[Debugging performance issues in Go programs](https://software.intel.com/en-us/blogs/2014/05/10/debugging-performance-issues-in-go-programs)  
[Scheduler tracing in Go](http://www.goinggo.net/2015/02/scheduler-tracing-in-go.html)  

[Go runtime package](http://golang.org/pkg/runtime/)  
[GC Runtime Source Code](https://golang.org/src/runtime/mgc.go)  

[Finding memory leaks in Go](https://www.hakkalabs.co/articles/finding-memory-leaks-go-programs)  
[Visualising the Go garbage collector](http://dave.cheney.net/2014/07/11/visualising-the-go-garbage-collector)  
[Understanding Go memory usage](https://deferpanic.com/blog/understanding-golang-memory-usage)  
[Visualising garbage collection algorithms](https://spin.atomicobject.com/2014/09/03/visualizing-garbage-collection-algorithms/)

## 코드 리뷰

[Web Service](godebug.go) ([Go Playground](https://play.golang.org/p/cLfl3dZYLf))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
