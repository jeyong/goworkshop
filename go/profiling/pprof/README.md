## http/pprof Profiling

http/pprof를 사용하면 웹 어플리케이션과 서비스를 프로파일링하여 성능과 사용하는 메모리를 정확히 확인할 수 있습니다.

### 프로젝트 빌드와 실행

프로파일링에 대해서 더 많이 배울 수 있는 웹사이트가 있습니다. 이 프로젝트에서는 struct 타입 값만 생성하고 이를 JSON으로 마샬링하고 응답으로 사용합니다. 

예제 프로그램을 빌드하고 실행합니다.

	$ go build
	$ ./pprof

동작하는지 테스트합니다.

	http://localhost:4000/sendjson

프로파일링을 실행하면서 해당 서비스에 load를 가합니다. 다음 명령을 실행합니다.

	// Send 1M request using 8 connections.
	$ hey -m POST -c 8 -n 1000000 "http://localhost:4000/sendjson"

### Raw http/pprof

이미 다음과 같은 import를 추가하며 우리 웹 서비스에 프로파일링 라우트를 포함할 수 있습니다.

	import _ "net/http/pprof"

새로운 endpoint로부터 기본 프로파일링 상태를 살펴봅니다.

	http://localhost:4000/debug/pprof

Browser로부터 단일 검색을 실행하고 프로파일 정보를 갱신합니다.

	http://localhost:4000/sendjson

웹 어플리케이션의 load를 가합니다. 다시 raw 프로파일링 정보를 리뷰합니다.

	$ hey -m POST -c 8 -n 1000000 "http://localhost:4000/sendjson"

### Heap 프로파일 살펴보기

	http://localhost:4000/debug/pprof/heap?debug=1

heap 프로파일의 상단에 아래와 같은 정보를 볼 수 있습니다.

	heap profile: 0: 0 [9318: 3545424] @ heap/1048576
	[0:] 		    Currently live objects,
	[0] 		    Amount of memory occupied by live objects
	[9318:] 	    Total number of allocations
	[3545424] 	    Amount of memory occupied by all allocations

heap 프로파일의 밑부분에 아래와 같은 정보를 볼 수 있습니다.

General statistics.

	Alloc      uint64 // bytes allocated and not yet freed
	TotalAlloc uint64 // bytes allocated (even if freed)
	Sys        uint64 // bytes obtained from system (sum of XxxSys below)
	Lookups    uint64 // number of pointer lookups
	Mallocs    uint64 // number of mallocs
	Frees      uint64 // number of frees

Main allocation heap statistics.

	HeapAlloc    uint64 // bytes allocated and not yet freed (same as Alloc above)
	HeapSys      uint64 // bytes obtained from system
	HeapIdle     uint64 // bytes in idle spans
	HeapInuse    uint64 // bytes in non-idle span
	HeapReleased uint64 // bytes released to the OS
	HeapObjects  uint64 // total number of allocated objects

Low-level fixed-size structure allocator statistics.

	// Inuse is bytes used now.
	// Sys is bytes obtained from system.
	StackInuse  uint64 // bytes used by stack allocator
	StackSys    uint64
	MSpanInuse  uint64 // mspan structures
	MSpanSys    uint64
	MCacheInuse uint64 // mcache structures
	MCacheSys   uint64
	BuckHashSys uint64 // profiling bucket hash table
	GCSys       uint64 // GC metadata
	OtherSys    uint64 // other system allocations

Garbage collector statistics.

	NextGC  uint64 // next collection will happen when HeapAlloc ≥ this amount
	PauseNs [256]uint64 // circular buffer of recent GC pause durations, most recent at [(NumGC+255)%256]
	NumGC   uint32 // Number of GC that have run

### Interactive Profiling

#### Heap Profiling

Run the pprof tool.

	$ go tool pprof -<PICK_MEM_PROFILE> ./pprof http://localhost:4000/debug/pprof/heap

Documentation of memory profile options.

    // Useful to see current status of heap.
	-inuse_space  : Allocations live at the time of profile  	** default
	-inuse_objects: Number of bytes allocated at the time of profile

	// Useful to see pressure on heap over time.
	-alloc_space  : All allocations happened since program start
	-alloc_objects: Number of object allocated at the time of profile

If you want to reduce memory consumption, look at the `-inuse_space` profile collected during normal program operation.
	
If you want to improve execution speed, look at the `-alloc_objects` profile collected after significant running time or at program end.

#### CPU Profiling

Run the Go pprof tool in another window or tab to review cpu information.

	$ go tool pprof ./pprof http://localhost:4000/debug/pprof/profile

_Note that goroutines in "syscall" state consume an OS thread, other goroutines do not (except for goroutines that called runtime.LockOSThread, which is, unfortunately, not visible in the profile). Note that goroutines in "IO wait" state also do not consume threads, they are parked on non-blocking network poller (which uses epoll/kqueue/GetQueuedCompletionStatus to unpark goroutines later)._

Explore using the **top**, **list**, **web** and **web list** commands.

### Comparing Profiles

Take a snapshot of the current heap profile. Then do the same for the cpu profile.

    $ curl -s http://localhost:4000/debug/pprof/heap > base.heap

After some time, take another snapshot:

    $ curl -s http://localhost:4000/debug/pprof/heap > current.heap

Now compare both snapshots against the binary and get into the pprof tool:

    $ go tool pprof -inuse_space -base base.heap ./pprof current.heap
