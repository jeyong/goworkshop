## 코드 프로파일링

go tool을 이용해서 여러분이 작성한 프로그램을 프로파일링할 수 있습니다. 프로파일링은 단순히 조사하는 것 이상의 일입니다. 어플리케이션을 이해하고 어떻게 동작해야하는지에 대해서 알고 있어야 합니다. 프로파일링을 통해 나온 데이터 자체는 그냥 숫자일 뿐입니다. 여기에 의미를 주고 이해하는 작업이 필요합니다.

## 프로파일링 기본

### 프로파일러가 하는 일

프로파일러는 일정 주기로 인터럽트를 걸기 위해서 프로그램으로 운영체제에 설정합니다. SIGPROF를 해당 프로그램에 보내서 프로파일링을 할 수 있습니다. 프로파일러는 각 수행 쓰레드에 대해서 프로그램 카운터를 잡거나 프로그램을 재시작시킬 수도 있습니다.

### Profiling do's and don't's

프로파일을 하기 전에, 반복적인 결과를 얻기 위해서 안정적인 환경을 가지고 있어야 합니다.

* 해당 기계는 반드시 idle 상태여야 합니다 - 하드웨어를 공유하는 기계에서는 프로파일을 하지 않습니다. 벤치마크 실행시간이 길더라도 기다리는 동안 웹브라우저를 사용하지 않습니다.
* 절전모드로 빠지지 않도록 살펴봅니다.
* 가상머신과 클라우드 호스팅은 가급적 피합니다.; 측정에 노이즈가 많아서 측정하기가 쉽지 않습니다.

여유가 있다면 성능 테스트용 하드웨어를 구입합니다. 고정시키고 전원 관리를 비활성화시킵니다. 해당 기계에서 소프트웨어 업데이트를 하지 않도록 합니다.

일정한 결과를 얻기 위해서 여러번 샘플을 실행하도록 합니다.

### 프로파일링 종류

**CPU 프로파일링**  
CPU profiling is the most common type of profile. When CPU profiling is enabled, the runtime will interrupt itself every 10ms and record the stack trace of the currently running goroutines. Once the profile is saved to disk, we can analyse it to determine the hottest code paths. The more times a function appears in the profile, the more time that code path is taking as a percentage of the total runtime.

**Memory profiling**  
Memory profiling records the stack trace when a heap allocation is made. Memory profiling, like CPU profiling is sample based. By default memory profiling samples 1 in every 1000 allocations. This rate can be changed. Stack allocations are assumed to be free and are not tracked in the memory profile. Because of memory profiling is sample based and because it tracks allocations not use, using memory profiling to determine your application's overall memory usage is difficult.

**Block profiling**  
Block profiling is quite unique. A block profile is similar to a CPU profile, but it records the amount of time a goroutine spent waiting for a shared resource. This can be useful for determining concurrency bottlenecks in your application. Block profiling can show you when a large number of goroutines could make progress, but were blocked.

Blocking includes:

* Sending or receiving on a unbuffered channel.
* Sending to a full channel, receiving from an empty one.
* Trying to Lock a sync.Mutex that is locked by another goroutine.
* Block profiling is a very specialised tool, it should not be used until you believe you have eliminated all your CPU and memory usage bottlenecks.

**One profile at at time**  
Profiling is not free. Profiling has a moderate, but measurable impact on program performance—especially if you increase the memory profile sample rate. Most tools will not stop you from enabling multiple profiles at once. If you enable multiple profiles at the same time, they will observe their own interactions and skew your results.

**Do not enable more than one kind of profile at a time.**

### Hints to interpret what you see in the profile

If you see lots of time spent in `runtime.mallocgc` function, the program potentially makes excessive amount of small memory allocations. The profile will tell you where the allocations are coming from. See the memory profiler section for suggestions on how to optimize this case.

If lots of time is spent in channel operations, `sync.Mutex` code and other synchronization primitives or System component, the program probably suffers from contention. Consider to restructure program to eliminate frequently accessed shared resources. Common techniques for this include sharding/partitioning, local buffering/batching and copy-on-write technique.

If lots of time is spent in `syscall.Read/Write`, the program potentially makes excessive amount of small reads and writes. Bufio wrappers around os.File or net.Conn can help in this case.

If lots of time is spent in GC component, the program either allocates too many transient objects or heap size is very small so garbage collections happen too frequently.

* Large objects affect memory consumption and GC time, while large number of tiny allocations affects execution speed.

* Combine values into larger values. This will reduce number of memory allocations (faster) and also reduce pressure on garbage collector (faster garbage collections).

* Values that do not contain any pointers are not scanned by garbage collector. Removing pointers from actively used value can positively impact garbage collection time.

## Rules of Performance

1) Never guess about performance.  
2) Measurements must be relevant.  
3) Profile before you decide something is performance critical.  
4) Test to know you are correct.

## Installing Tools

**hey**  
hey is a modern HTTP benchmarking tool capable of generating the load you need to run tests. It's built using the Go language and leverages goroutines for behind the scenes async IO and concurrency.

	go get -u github.com/rakyll/hey

## Dave Cheney's Profiling Presentation:  

Much of what I have learned comes from Dave and working on solving problems. This slide deck is a great place to start. Much of this material can be found in the material below.

http://go-talks.appspot.com/github.com/davecheney/presentations/seven.slide#1

## Profiling, Debugging and Optimization Reading

Here is more reading and videos to also help get you started.

[Profiling Go Programs](http://golang.org/blog/profiling-go-programs) - Go Team  
[Profiling & Optimizing in Go](https://www.youtube.com/watch?v=xxDZuPEgbBU) - Brad Fitzpatrick  
[Go Dynamic Tools](https://www.youtube.com/watch?v=a9xrxRsIbSU) - Dmitry Vyukov  
[How NOT to Measure Latency](https://www.youtube.com/watch?v=lJ8ydIuPFeU&feature=youtu.be) - Gil Tene  
[Go Performance Tales](http://jmoiron.net/blog/go-performance-tales) - Jason Moiron  
[Debugging performance issues in Go programs](https://software.intel.com/en-us/blogs/2014/05/10/debugging-performance-issues-in-go-programs) - Dmitry Vyukov  
[Reduce allocation in Go code](https://methane.github.io/2015/02/reduce-allocation-in-go-code) - Python Bytes  
[Write High Performance Go](http://go-talks.appspot.com/github.com/davecheney/presentations/writing-high-performance-go.slide) - Dave Cheney  
[Static analysis features of godoc](https://golang.org/lib/godoc/analysis/help.html) - Go Team   
[Seven ways to profile a Go program](https://www.bigmarker.com/remote-meetup-go/Seven-ways-to-profile-a-Go-program) - Dave Cheney   
[runtime: goroutine execution stalled during GC](https://github.com/golang/go/issues/16293) - Caleb Spare  
[Go's execution tracer](http://www.thedotpost.com/2016/10/rhys-hiltner-go-execution-tracer) - Rhys Hiltner  
[Using Instruments to profile Go programs](https://rakyll.org/instruments) - rakyll  
[Fighting latency: the CPU profiler is not your ally](https://www.youtube.com/watch?v=nsM_m4hZ-bA&t=973s) - Filippo Valsorda  
[go tool trace](https://making.pusher.com/go-tool-trace/) - Will Sewell  

## Go와 OS Tooling

### time

**time** 명령으로 프로그램의 성능을 가름할 수 있는 정보를 제공합니다.

**time** 명령을 사용해서 프로그램을 build하는 시간을 볼 수 있습니다.
	$ cd $GOPATH/src/github.com/ardanlabs/gotraining/topics/go/profiling/project
	$ /usr/bin/time -lp go build		-- Mac OS X
	$ /usr/bin/time -v go build		-- Linux

### perf

만약 리눅스 사용자에게 perf(1)는 어플리케이션을 프로파일링하는데 있어서 훌륭한 툴입니다. 이제 frame pointer를 가지고 perf는 Go 어플리케이션을 프로파일링할 수 있습니다.

	$ go build -toolexec="perf stat" cmd/compile/internal/gc
	# cmd/compile/internal/gc

 	Performance counter stats for '/home/dfc/go/pkg/tool/linux_amd64/compile -o $WORK/cmd/compile/internal/gc.a -trimpath $WORK -p cmd/compile/internal/gc -complete -buildid 87cd803267511b4d9e753d68b5b66a70e2f878c4 -D _/home/dfc/go/src/cmd/compile/internal/gc -I $WORK -pack ./alg.go ./align.go ./bexport.go ./bimport.go ./builtin.go ./bv.go ./cgen.go ./closure.go ./const.go ./cplx.go ./dcl.go ./esc.go ./export.go ./fmt.go ./gen.go ./go.go ./gsubr.go ./init.go ./inl.go ./lex.go ./magic.go ./main.go ./mpfloat.go ./mpint.go ./obj.go ./opnames.go ./order.go ./parser.go ./pgen.go ./plive.go ./popt.go ./racewalk.go ./range.go ./reflect.go ./reg.go ./select.go ./sinit.go ./sparselocatephifunctions.go ./ssa.go ./subr.go ./swt.go ./syntax.go ./type.go ./typecheck.go ./universe.go ./unsafe.go ./util.go ./walk.go':

       7026.140760 task-clock (msec)         #    1.283 CPUs utilized          
             1,665 context-switches          #    0.237 K/sec                  
                39 cpu-migrations            #    0.006 K/sec                  
            77,362 page-faults               #    0.011 M/sec                  
    21,769,537,949 cycles                    #    3.098 GHz                     [83.41%]
    11,671,235,864 stalled-cycles-frontend   #   53.61% frontend cycles idle    [83.31%]
     6,839,727,058 stalled-cycles-backend    #   31.42% backend  cycles idle    [66.65%]
    27,157,950,447 instructions              #    1.25  insns per cycle        
                                             #    0.43  stalled cycles per insn [83.25%]
     5,351,057,260 branches                  #  761.593 M/sec                   [83.49%]
       118,150,150 branch-misses             #    2.21% of all branches         [83.15%]

       5.476816754 seconds time elapsed

## Basic Go Profiling

Learn the basics of reading Stack Traces.  
[Stack Traces and Core Dumps](stack_trace/README.md)

Learn the basics of using GODEBUG.  
[GODEBUG](godebug/README.md)

Learn the basics of using memory and cpu profiling.  
[Memory and CPU Profiling](memcpu/README.md)

Learn the basics of using http/pprof.  
[pprof Profiling](pprof/README.md)

Learn the basics of blocking profiling.  
[Blocking Profiling](blocking/README.md)

Learn the basics of mutex profiling.  
[Mutex Profiling](mutex/README.md)

Learn the basics of tracing.    
[Tracing](trace/README.md)

Learn the basics of profiling and tracing a larger application.  
[Real World Example](project/README.md)

## Godoc Analysis

The `godoc` tool can help you perform static analysis on your code.

	// Perform a pointer analysis and then run the godoc website.
	$ godoc -analysis pointer -http=:8080

[Static analysis features of godoc](https://golang.org/lib/godoc/analysis/help.html) - Go Team

## HTTP Tracing

HTTP tracing은 HTTP client request의 주기동안 세부 정보를 모을 수 있습니다.

[HTTP Tracing Package](http_trace/README.md)

___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
