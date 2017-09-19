## Logging - 표준 라이브러리

Logging은 모든 프로그램에서 중요한 부분 중에 하나입니다. Logs는 마치 눈과 같으면 프로그램이 실행되는 동안 내부에서 일어나는 일을 알려줍니다. 표준 라이브러리로 logging의 기본 기능을 지원하는 log 패키지를 제공합니다. 여러분의 필요에 맞게 logging을 확장 및 커스터마이징할 수 있습니다.

## 노트

* logging 기능은 이미 표준 라이브러리에서 제공하고 있습니다.
* log 패키지는 쉽게 확장이 가능하여 여러분의 필요에 맞출 수 있습니다.

## 링크

http://www.goinggo.net/2013/11/using-log-package-in-go.html

## 코드 리뷰

[Use of log package](example1/example1.go) ([Go Playground](http://play.golang.org/p/UCGUZZ--OP))  
[Customizing your own log](example2/example2.go) ([Go Playground](http://play.golang.org/p/wD06PQAefc))

## 연습문제

### 연습문제 1

log 패키지를 사용하기 위한 새로운 프로그램을 만듭니다. prefix로 여러분의 이름을 사용하며, 각 log 파일에서 코드 파일에 대해서 date와 long path를 보여주도록 합니다.

[Template](exercises/template1/template1.go) ([Go Playground](http://play.golang.org/p/9si47xIX0q)) | 
[Answer](exercises/exercise1/exercise1.go) ([Go Playground](http://play.golang.org/p/ShXBoI1XN-))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.