## Stack Traces와 Core Dumps

Having some basic skills in debugging Go programs can save any programmer a good amount of time trying to identify problems. I believe in logging as much information as you can, but sometimes a panic occurs and what you logged is not enough. Understanding the information in a stack trace can sometimes mean the difference between finding the bug now or needing to add more logging and waiting for it to happen again. We can also stop a running program and get Core Dump which also generates a stack trace.

## Notes

* Stack traces are an important tool in debugging an application.
* The runtime should never panic so the trace is everything.
* You can see every goroutine and the call stack for each routine.
* You can see every value passed into each function on the stack.
* You can generate core dumps and use these same techniques.

## Stack Traces

These two programs called the built-in function `panic` to produce a stack trace. Stack traces show not only the call stack from the line of code that caused the panic. They also show the values that were passed into each function.

### 예제 1

Build and run the program.

    $ go build
    $ ./example1

Review the stack trace.

    // Stack Trace
    goroutine 1 [running]:
    panic(0x56a60, 0xc82000a110)
        /usr/local/go/src/runtime/panic.go:464 +0x3e6
    main.example(0xc82003bf08, 0x2, 0x4, 0x708a8, 0x5, 0xa)
        /Users/bill/.../stack_trace/example1/example1.go:13 +0x65
    main.main()
        /Users/bill/.../stack_trace/example1/example1.go:9 +0xa5

    // Parameters
    make([]string, 2, 4), "hello", 10

    // main.example(0xc82003bf08, 0x2, 0x4, 0x708a8, 0x5, 0xa)
    Slice Value:   0xc82003bf08, 0x2, 0x4
    String Value:  0x708a8, 0x5
    Integer Value: 0xa

### 예제 2

Build and run the program.

    $ go build
    $ ./example2

Review the stack trace.

    // Stack Trace
    goroutine 1 [running]:
    panic(0x569e0, 0xc82000a110)
        /usr/local/go/src/runtime/panic.go:464 +0x3e6
    main.example(0xc819010001)
        /Users/bill/.../stack_trace/example2/example2.go:12 +0x65
    main.main()
        /Users/bill/.../stack_trace/example2/example2.go:8 +0x2b

    // Parameters
    true, false, true, 25

    // main.example(0xc819010001)
    Bits    Binary      Hex   Value
    00-07   0000 0001   01    true
    08-15   0000 0000   00    false
    16-23   0000 0001   01    true
    24-31   0001 1001   19    25

### 코드 리뷰

[Review Stack Trace](example1/example1.go) ([Go Playground](https://play.golang.org/p/9gkLGCdbNe))  
[Packing](example2/example2.go) ([Go Playground](https://play.golang.org/p/SIiN6Y2jTR))  

### 링크

[Stack traces in Go](http://www.goinggo.net/2015/01/stack-traces-in-go.html)  

## Core Dumps

You can generate a core dump of any running Go program by issuing a SIGQUIT to the program. You can do this by pressing (Ctrl+\\) on your keyboard.

### Core Dump 생성하기

Build and run the example program.

    $ go build
    $ ./godebug

Put some load of the web application.

    $ hey -m POST -c 8 -n 1000000 "http://localhost:4000/sendjson"

Issue a signal quit.

    Ctrl+\

Review the dump.

    2017/05/31 06:24:24 listener : Started : Listening on: http://localhost:4000 : Leak[false]
    ^\SIGQUIT: quit
    PC=0x10564cb m=0 sigcode=0

    goroutine 0 [idle]:
    runtime.mach_semaphore_wait(0xf03, 0x13e2040, 0x7fff5fbff860, 0x1030cda, 0x13e1c30, 0x13e2040, 0x7fff5fbff810, 0x1050ba3, 0xffffffffffffffff, 0x1, ...)
        /usr/local/go/src/runtime/sys_darwin_amd64.s:415 +0xb
    runtime.semasleep1(0xffffffffffffffff, 0x1)
        /usr/local/go/src/runtime/os_darwin.go:413 +0x4b

    ...

    rax    0xe
    rbx    0x13e23a0
    rcx    0x7fff5fbff7b0

Get a larger crash dump by running the program using the GOTRACEBACK env variable.

    $ GOTRACEBACK=crash ./crash

Use `gcore` to write a dump of the running program.

    $ sudo gcore -o core.txt PID

Use Delve to review the dump.

    $ dlv core ./godebug core.txt

    (dlv) bt
    0  0x0000000000457774 in runtime.raise
        at /usr/lib/go/src/runtime/sys_linux_amd64.s:110
    1  0x000000000043f7fb in runtime.dieFromSignal

    (dlv) ls
    > runtime.raise() /usr/lib/go/src/runtime/sys_linux_amd64.s:110 (PC: 0x457774)
    105:		SYSCALL
    106:		MOVL	AX, DI	// arg 1 tid
    107:		MOVL	sig+0(FP), SI	// arg 2
    108:		MOVL	$200, AX	// syscall - tkill
    109:		SYSCALL
    => 110:		RET

### 링크

[Debugging Go core dumps](https://rakyll.org/coredumps/?utm_source=golangweekly&utm_medium=email)  

### 코드 리뷰

[Core Dumps](example3/example3.go) ([Go Playground](https://play.golang.org/p/2fma3AXMmZ))  
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
