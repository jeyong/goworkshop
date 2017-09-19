## io - 표준 라이브러리

데이터를 스트림으로 전달하는 것은 중요합니다. 데이터는 소켓, 파일, 장치 등을 통해서 우리가 작성한 프로그램으로 일정하게 들어옵니다. 이런 데이터는 여러 차례 하나의 스트림으로부터 이동해야할 수도 있습니다. 어떤 경우에는 안전하게 유지하기 위해서 암호화하거나 해쉬를 이용하기도 합니다. Writer와 Reader interface는 가장 많이 사용되며 표준 라이브러리와 커뮤니티에서도 지원합니다. 

## 노트

* 표준 라이브러리는 데이터로 스트림처리에 필요한 모든 인프라를 제공하고 있습니다.
* Reader와 Writer interface를 우리 타입으로 구현하는 경우, 제공하는 기능을 그대로 사용할 수 있습니다.
* 기존 기능에 대해서 인터페이스를 구현하는 것은 개발 시간과 버그를 줄여 줍니다.

## 문서

[Interface Declarations](documentation/interfaces.md)

## 링크

http://golang.org/pkg/io/  
[io package](https://medium.com/@benbjohnson/go-walkthrough-io-package-8ac5e95a9fbd#.d2ebstv0q) - Ben Johnson  

## 코드 리뷰

[Standard Library Working Together](example1/example1.go) ([Go Playground](https://play.golang.org/p/Ikm0s6vjoi))  
[Simple curl with io.Reader and io.Writer](example2/example2.go) ([Go Playground](https://play.golang.org/p/b_BxHFATti))  
[MultiWriters with curl example](example3/example3.go) ([Go Playground](https://play.golang.org/p/3UeN6iAE-k))  
[Stream processing](example4/example4.go) ([Go Playground](https://play.golang.org/p/9h53-8jZUW))  

## 고급 코드 리뷰

[TeeReader and io composition](advanced/example1/example1.go) ([Go Playground](https://play.golang.org/p/9QSXbjtPxe))  
[Gzip and Md5 support with curl example](advanced/example2/example2.go) ([Go Playground](https://play.golang.org/p/kN97kdqRGy))

## 연습문제

### 연습문제 1

웹에서 문서를 다운받고 터미널로 내용을 출력하고 동시에 파일에 씁니다.

[Template](exercises/template1/template1.go) ([Go Playground](http://play.golang.org/p/ZCqK8ek58U)) | 
[Answer](exercises/exercise1/exercise1.go) ([Go Playground](http://play.golang.org/p/bogTavYBEx))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
