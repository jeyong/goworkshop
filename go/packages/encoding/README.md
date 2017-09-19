## Encoding - 표준 라이브러리

Encoding은 다른 형태로 데이터를 데이터를 마샬링이나 언마샬링하는 것을 말합니다. JSON string 다큐먼트를 받아서 사용자가 정의한 타입의 값으로 변환하는 것으로 최근 많은 go 프로그램에서 흔하게 사용됩니다. encoding을 위해 Go는 많은 지원을 하고 있으면 매번 버전이 올라갈때마다 성능을 개선하고 있습니다. 

## 노트

* JSON과 XML 인코딩/디코딩 지원을 표준 라이브러리에서 제공
* 이 패키지 계속 개선하고 있음

## 링크

http://www.goinggo.net/2014/01/decode-json-documents-in-go.html

## 코드 리뷰

[Unmarshal JSON documents](example1/example1.go) ([Go Playground](http://play.golang.org/p/nwUGs8q2S6))  
[Unmarshal JSON files](example2/example2.go) ([Go Playground](http://play.golang.org/p/WfDYLZ5KeH))  
[Marshal a user defined type](example3/example3.go) ([Go Playground](http://play.golang.org/p/miSv1mPnK5))  
[Custom Marshaler and Unmarshler](example4/example4.go) ([Go Playground](http://play.golang.org/p/tOriq1dE0N))

## 연습문제

### 연습문제 1

**Part A** 사용자의 이름과 이메일을 포함하는 JSON 배열 형태의 파일을 생성합니다. JSON 문서로 매핑되는 struct 타입을 선언합니다. json 패키지를 사용해서, 파일을 읽고 이 struct 타입의 slice를 생성합니다. slice를 출력하세요.  

**Part B** slice를 print string으로 마샬링하고 각 element를 출력하세요.

[Template](exercises/template1/template1.go) ([Go Playground](http://play.golang.org/p/5NNPJhIQDT)) | 
[Answer](exercises/exercise1/exercise1.go) ([Go Playground](http://play.golang.org/p/IyNucru7hi))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
