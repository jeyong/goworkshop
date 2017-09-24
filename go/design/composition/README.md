## 인터페이스와 컴포지션 디자인 (Interface and Composition Design)

컴포지션은 단순히 타입 임베딩(type embeddng)이라고 생각할 수 있지만 그 이상의 의미를 가지고 있습니다. 여러분의 소프트웨어를 안정적으로 유지보수하는데 핵심이 됩니다. 데이터에 따라 적응할 수 있고 변경으로 인한 변화가 일어나더라도 유지보수가 가능합니다.

## 노트

* 단순한 타입 임베딩이 아니다.
* 타입 선언과 컴포니션으로 워크플로우 구현을 고려
* 먼저 해결하고자 하는 문제를 이해한다. 이말은 해당 데이터를 이해해야 한다는 뜻이다.
* 목적은 변경이 연속적으로 일어나는 것을 줄이거나 최소화하는 것이다.
* 인터페이스는 컴포니션의 가장 높은 형태를 제공한다.
* 공통 DNA가 아니라 공통 behavior로 타입을 그룹으로 묶는다

## 인용

_"데이터 일부가 하는 일을 외부에 노출하는 것이 실제로 합당할때 method가 효과적이다."- William Kennedy_

## 디자인 가이드라인

* 컴포지션에 관한 [디자인 가이드](../../#interface-and-composition-design)

## 링크

http://golang.org/doc/effective_go.html#embedding  
[Methods, Interfaces and Embedding](http://www.goinggo.net/2014/05/methods-interfaces-and-embedded-types.html) - William Kennedy  
[Composition In Go](https://www.goinggo.net/2015/09/composition-with-go.html) - William Kennedy  
[Reducing Type Hierarchies](https://www.goinggo.net/2016/10/reducing-type-hierarchies.html) - William Kennedy  
[Avoid Interface Pollution](https://www.goinggo.net/2016/10/avoid-interface-pollution.html) - William Kennedy

## 코드 리뷰

#### Grouping Types

[Grouping By State](grouping/example1/example1.go) ([Go Playground](https://play.golang.org/p/r6to0aMm6I))  
[Grouping By Behavior](grouping/example2/example2.go) ([Go Playground](https://play.golang.org/p/yOj1zJCRlj))  

#### 디커플링 (Decoupling)

[Struct Composition](decoupling/example1/example1.go) ([Go Playground](https://play.golang.org/p/axLYwteYkK))  
[Decoupling With Interface](decoupling/example2/example2.go) ([Go Playground](https://play.golang.org/p/EnzMrT7Fdo))  
[Interface Composition](decoupling/example3/example3.go) ([Go Playground](https://play.golang.org/p/ES4BOnDX6O))  
[Decoupling With Interface Composition](decoupling/example4/example4.go) ([Go Playground](https://play.golang.org/p/ufFSFxCdEs))  
[Remove Interface Pollution](decoupling/example5/example5.go) ([Go Playground](https://play.golang.org/p/a8C4KM9AU2))  

#### Conversion과 Assertions

[Interface Conversions](assertions/example1/example1.go) ([Go Playground](https://play.golang.org/p/GVLf2sZcA1))  
[Runtime Type Assertions](assertions/example2/example2.go) ([Go Playground](https://play.golang.org/p/awq1LSTwXV))

#### Interface 공해

[Create Interface Pollution](pollution/example1/example1.go) ([Go Playground](https://play.golang.org/p/wHDLvxe8hC))  
[Remove Interface Pollution](pollution/example2/example2.go) ([Go Playground](https://play.golang.org/p/s6HAmeT6oT))

#### Mocking

[Package To Mock](mocking/example1/pubsub/pubsub.go) ([Go Playground](https://play.golang.org/p/3a_zYeR8M7))  
[Client](mocking/example1/example1.go) ([Go Playground](https://play.golang.org/p/guvjysMjgb))

## 연습문제

### 연습문제 1

template를 이용해서 실제 type의 집합을 선언합니다. 이 타입은 미리 정의한 interface 타입의 집합을 구현합니다. 다음으로 이 타입의 값을 생성하고 이를 이용해서 미리 정의한 task의 집합을 완성하세요.

[Template](exercises/template1/template1.go) ([Go Playground](https://play.golang.org/p/uY6KMprfMR)) | 
[Answer](exercises/exercise1/exercise1.go) ([Go Playground](https://play.golang.org/p/nbd3gnLlih))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
