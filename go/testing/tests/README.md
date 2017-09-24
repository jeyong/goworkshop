## Testing

테스팅은 go tool과 표준 라이브러리로 제공하고 있습니다. 테스팅은 프로젝트 개발 프로젝트의 시간을 엄청나게 줄여주기 때문에 개발 프로세스에서 중요한 부분입니다. 테스팅 기능과 함께 벤치마킹은 매우 강력한 도구입니다. 작성한 코드의 일부의 성능을 리뷰할 수 있습니다. 프로파일링은 함수 사이에 상호작용을 살펴보고 어떤 함수가 가장 많이 사용되는지 볼 수 있습니다.

## Notes

* Go에서 tool로 테스팅과 벤치마킹을 지원합니다.
* tool이 매우 유연해서 다양한 옵션을 줄 수 있습니다.
* 개발과 나란히 테스트를 작성합니다.
* 예제 코드는 테스트와 문서의 역할을 합니다.
* 개발, QA, 릴리즈 단계에서 벤치마킹을 할 수 있습니다.
* 성능 문제를 발견하면, 코드를 프로파일링해새ㅓ 어떤 함수에 집중되는지를 볼 수 있습니다.
* tool은 서로 영향을 줄 수 있습니다. 정밀한 메모리 프로파일링은 CPU 프로파일, goroutine blocking 프로파일링이 스케쥴러 trace에 영향을 미친다. 각 필요한 프로파일링 모드에 대해서 테스트를 재실행합니다.

## Links

http://golang.org/pkg/testing/  
http://dave.cheney.net/2013/06/30/how-to-write-benchmarks-in-go  
http://saml.rilspace.org/profiling-and-creating-call-graphs-for-go-programs-with-go-tool-pprof  
http://golang.org/pkg/net/http/pprof/  
https://software.intel.com/en-us/blogs/2014/05/10/debugging-performance-issues-in-go-programs  
https://github.com/dvyukov/go-fuzz  
https://talks.golang.org/2015/dynamic-tools.slide#1  
https://vimeo.com/141698770  
[Structuring Tests in Go](https://medium.com/@benbjohnson/structuring-tests-in-go-46ddee7a25c#.b2m3nziyb) - Ben Johnson  
[고급 테스팅 컨셉 Go 1.7](https://speakerdeck.com/mpvl/advanced-testing-concepts-for-go-1-dot-7) - Marcel van Lohuizen  
[Parallelize your table-driven tests](http://golang.rakyll.org/parallelize-test-tables/) - rakyll  
[고급 테스팅 Go - Video](https://www.youtube.com/shared?ci=LARb45o5TpA) - Mitchell Hashimoto  
[고급 테스팅 Go - Deck](https://speakerdeck.com/mitchellh/advanced-testing-with-go) - Mitchell Hashimoto  
[The tragedy of 100% code coverage](http://labs.ig.com/code-coverage-100-percent-tragedy) - Daniel Lebrero's  

## 코드 리뷰

[Basic Unit Test](example1/example1_test.go) ([Go Playground](https://play.golang.org/p/bYkkr3uQcp))  
[Table Unit Test](example2/example2_test.go) ([Go Playground](https://play.golang.org/p/hhavdseEPj))  
[Mocking Web Server Response](example3/example3_test.go) ([Go Playground](https://play.golang.org/p/JJ_2VIL_R6))  
[Testing Internal Endpoints](example4/handlers/handlers_test.go) ([Go Playground](https://play.golang.org/p/HwuD-eNAOg))  
[Example Test](example4/handlers/handlers_example_test.go) ([Go Playground](https://play.golang.org/p/6V2J5gr7GC))  
[Sub Tests](example5/example5_test.go) ([Go Playground](https://play.golang.org/p/d4ZVYkZUGr))  

_코드를 [profile](../../profiling/README.md)하기 위한 벤치마킹 사용 방법에 대한 정보는 프로파일 링크를 참고하세요._

## 커버리지(Coverage)

여러분이 작성한 테스트가 코드의 가능한 많은 부분을 커버한다는 것은 중요합니다. Go의 테스팅 도구로 모든 테스트가 실행하는 코드에 대해서 프로파일을 생성하는 것이 가능합니다. 그리고 무엇을 하는지 그리고 커버되지 않는 부분을 시각적으로 표현할 수 있습니다.

	go test -coverprofile cover.out
	go tool cover -html=cover.out

![figure1](testing_coverage.png)
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
