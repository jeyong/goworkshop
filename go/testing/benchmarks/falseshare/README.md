## False Sharing

하드웨어가 어떻게 동작하는지 이해하는 것이 성능이 좋은 코드를 작성하는 방법을 이해하는데 핵심이 됩니다. 프로세서 캐싱의 기본을 이해하면 이디엄 코드를 작성하는 범위내에서 더 나은 결정을 내릴 수 있는데 도움이 됩니다.

## Data Races
벤치마크 테스트 내부 상세한 내용에 대해서는 data race 부분을 참조하세요.

[Data Races 문서](../../../concurrency/data_race/README.md)

## 코드 리뷰
  
[False Sharing Test](falseshare_test.go) ([Go Playground](https://play.golang.org/p/wfDk5IEt6k))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
