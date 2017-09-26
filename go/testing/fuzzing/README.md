## Go Fuzz

Go-fuzz Go 패키지를 테스팅하기 위해 커버리지가 안내하는 방식의 fuzzing 솔루션입니다. Fuzzing는 복잡한 입력을 파싱하는 패키지에 주로 적용됩니다.(text와 binary) 잠재적으로 악의를 가진 사용자로부터의 입력을 파싱하는 시스템을 견고하게 만드는데 특히 유용합니다.(예로 네트워크 상에서 어떤 것을 수신하는 경우)

## 노트

* Fuzzing은 여러분이 작성한 code에서 panic이 일어나는 지점을 찾는 것이 가능하다.
* 일단 panic을 일으키는 데이터 입력을 식별하면 code를 수정할 수 있고 테스트를 생성할 수 있다.
* Table tests는 이런 종류의 입력 데이터 panic에 대해서 훌륭한 선택이 될 수 있다.

## 링크

https://github.com/dvyukov/go-fuzz  
[go-fuzz github.com/arolek/ase](https://medium.com/@dgryski/go-fuzz-github-com-arolek-ase-3c74d5a3150c#.xvq0ol2zj) - Damian Gryski  
[Go Dynamic Tools](https://www.youtube.com/watch?v=a9xrxRsIbSU) - Dmitry Vyukov  
[DNS parser, meet Go fuzzer](https://blog.cloudflare.com/dns-parser-meet-go-fuzzer) - Filippo Valsorda  
[Fuzzing Beyond Security: Automated Testing with go-fuzz](https://www.youtube.com/watch?v=kOZbFSM7PuI) - Filippo Valsorda  

## 코드 리뷰

_데모를 보여줄때는 `workdir/corpus` 아래에 있는 폴더와 `api-fuzz.zip` 파일을 제거하라._

가장 먼저할 일은 Go fuzz 툴을 설치하는 것:

		go get github.com/dvyukov/go-fuzz/go-fuzz
		go get github.com/dvyukov/go-fuzz/go-fuzz-build

문제를 찾고자 하는 코드와 기존 테스트를 리뷰하기:

[Code To Fuzz](example1/example1.go) ([Go Playground](http://play.golang.org/p/6al_yc8YtO))  
[Test For The Code](example1/example1_test.go) ([Go Playground](http://play.golang.org/p/-6QXYkTNm6)) 

Create a corpus file with the initial input data to use and that will be mutated.

[Fuzzing Input Data](example1/workdir/corpus/input.txt) ([Go Playground](http://play.golang.org/p/RkYDgyQsF8))

Create a fuzzing function that takes mutated input and executes the code we care about using it.

[Fuzzing Function](example1/fuzzer.go) ([Go Playground](http://play.golang.org/p/ditM8pfOLm)

Run the `go-fuzz-build` tool against the package to generate the fuzz zip file. The zip file contains all the instrumented binaries go-fuzz is going to use while fuzzing. Any time the source code changes this needs to be re-run.

		go-fuzz-build github.com/ardanlabs/gotraining/topics/go/testing/fuzzing/example1

Perform the actual fuzzing by running the `go-fuzz` tool and find data inputs that cause panics. Run this until you see an initial crash.

		go-fuzz -bin=./api-fuzz.zip -workdir=workdir/corpus

Review the `crashers` folder under the `workdir/corpus` folders. This contains panic information. You will see an issue when the data passed into the web call is empty. Fix the `Process` function and add the table data to the test.

		{"/process", http.StatusBadRequest, []byte(""), `{"Error":"The Message"}`},

Run the build and start fuzzing.

		rm -rf workdir/crashers and workdir/supressions
		go-fuzz -bin=./api-fuzz.zip -dup -workdir=workdir/corpus

Review the `crashers` folder under the `workdir/corpus` folders. This contains panic information. You will see an issue when value of "0" is used. Fix the `Process` function and add the table data to the test.
		
		{"/process", http.StatusBadRequest, []byte("0"), `{"Error":"The Message"}`},

## 연습문제

### 연습문제 1

A function named `UnpackUsers` exists and requires fuzzing. A `Fuzz` function and corpus have also been provided. Use the Go Fuzz tooling to find as many problems as you can. In each case fix the bug and add a test table record to validate the test is fixed.

[연습문제](exercises/exercise1)
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
