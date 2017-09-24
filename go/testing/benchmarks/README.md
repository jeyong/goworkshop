## 벤치마킹(Benchmarking)

Go는 코드의 성능을 테스트하는 기능을 지원합니다.

## 패키지 리뷰

[Basic Benchmarking](basic/basic_test.go)  
[Sub Benchmarks](sub/sub_test.go)  
[Validate Benchmarks](validate/validate_test.go)  
[Prediction](prediction/README.md)  
[Caching](caching/README.md)  
[False Sharing](falseshare/README.md)  

_코드를 [profile](../../profiling/README.md)하기 위한 벤치마킹 사용 방법에 대한 정보는 프로파일 링크를 참고하세요._

## 링크

http://dave.cheney.net/2013/06/30/how-to-write-benchmarks-in-go  
[Profiling & Optimizing in Go / Brad Fitzpatrick](https://www.youtube.com/watch?v=xxDZuPEgbBU)  
[Benchstat computes and compares statistics about benchmarks](https://github.com/rsc/benchstat)  
[Advanced Testing Concepts for Go 1.7](https://speakerdeck.com/mpvl/advanced-testing-concepts-for-go-1-dot-7) - Marcel van Lohuizen  

## 연습문제

### 연습문제 1
integer를 string로 변환에 대해서 3개 벤치마킹 테스트를 작성하세요. 첫번째는 fmt.Sprintf 함수를 사용하고 다음은 strconv.FormatInt 함수를 마지막으로는 strconv.Itoa를 테스트하여 가장 성능이 좋은 것을 찾아봅니다.

[Template](exercises/template1/bench_test.go) ([Go Playground](http://play.golang.org/p/do3XfkNqRt)) | 
[Answer](exercises/exercise1/bench_test.go) ([Go Playground](http://play.golang.org/p/ttqLnSM2q_))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
