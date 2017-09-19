## 인터페이스와 컴포지션 디자인 (Interface and Composition Design)

Composition goes beyond the mechanics of type embedding and is more than just a paradigm. It is the key for maintaining stability in your software by having the ability to adapt to the data and transformation changes that are coming.

## 노트

* This is much more than the mechanics of type embedding.
* Declare types and implement workflows with composition in mind.
* Understand the problem you are trying to solve first. This means understanding the data.
* The goal is to reduce and minimize cascading changes across your software.
* Interfaces provide the highest form of composition.
* Don't group types by a common DNA but by a common behavior.
* Everyone can work together when we focus when we do and not what we are.

## Quotes

_"Methods are valid when it is practical or reasonable for a piece of data to expose a capability." - William Kennedy_

## 디자인 가이드라인

* Learn about the [design guidelines](../../#interface-and-composition-design) for composition.

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

#### Conversion and Assertions

[Interface Conversions](assertions/example1/example1.go) ([Go Playground](https://play.golang.org/p/GVLf2sZcA1))  
[Runtime Type Assertions](assertions/example2/example2.go) ([Go Playground](https://play.golang.org/p/awq1LSTwXV))

#### Interface Pollution

[Create Interface Pollution](pollution/example1/example1.go) ([Go Playground](https://play.golang.org/p/wHDLvxe8hC))  
[Remove Interface Pollution](pollution/example2/example2.go) ([Go Playground](https://play.golang.org/p/s6HAmeT6oT))

#### Mocking

[Package To Mock](mocking/example1/pubsub/pubsub.go) ([Go Playground](https://play.golang.org/p/3a_zYeR8M7))  
[Client](mocking/example1/example1.go) ([Go Playground](https://play.golang.org/p/guvjysMjgb))

## 연습문제

### 연습문제 1

Using the template, declare a set of concrete types that implement the set of predefined interface types. Then create values of these types and use them to complete a set of predefined tasks.

[Template](exercises/template1/template1.go) ([Go Playground](https://play.golang.org/p/uY6KMprfMR)) | 
[Answer](exercises/exercise1/exercise1.go) ([Go Playground](https://play.golang.org/p/nbd3gnLlih))
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
