## Exporting

패키지는 컴파일 된 코드의 기본 단위를 포함. 내부에 선언한 식별자에 대해서 scope를 정의합니다. exporting은 다른 언어에서 제공하는 public이나 private와 다르다. Go에서 인캡슐레이션을 제공하는 방식이 exporting이다.

## 노트

* Go의 코드는 패키지로 컴파일된 다음 함께 link된다.
* 대소문자에 따라서 식별자가 export되거나 안되거나 결정된다.
* package를 import하여 export된 식별자에 접근할 수 있다.
* Any package can use a value of an unexported type, but this is annoying to use.

## Links

http://www.goinggo.net/2014/03/exportedunexported-identifiers-in-go.html  

## Code Review

[export된 식별자 선언 및 접근 - Pkg](example1/counters/counters.go) ([Go Playground](https://play.golang.org/p/Sb_G1kcn_7))  
[export된 식별자 선언 및 접근 - Main](example1/example1.go) ([Go Playground](https://play.golang.org/p/LkIRp4J93P))  

[unexport된 식별자 선언과 제약 - Pkg](example2/counters/counters.go) ([Go Playground](https://play.golang.org/p/bb4TcZNXwl))  
[unexport된 식별자 선언과 제약 - Main](example2/example2.go) ([Go Playground](https://play.golang.org/p/eeH_xXlbwB))  

[unexport된 식별자의 값에 접근 - Pkg](example3/counters/counters.go) ([Go Playground](https://play.golang.org/p/9cjS2FESNH))  
[unexport된 식별자의 값에 접근 - Main](example3/example3.go) ([Go Playground](https://play.golang.org/p/eEEBo_qlrt))  

[Unexport된 struct type fields - Pkg](example4/users/users.go) ([Go Playground](https://play.golang.org/p/O9hleQ18dT))  
[Unexport된 struct type fields - Main](example4/example4.go) ([Go Playground](https://play.golang.org/p/GRC2z6VvxN))  

[Unexport된 embedded types - Pkg](example5/users/users.go) ([Go Playground](https://play.golang.org/p/RWpldbVNJe))  
[Unexport된 embedded types - Main](example5/example5.go) ([Go Playground](https://play.golang.org/p/yts2fe36ay))  

## Exercises

### Exercise 1
**Part A** Create a package named toy with a single exported struct type named Toy. Add the exported fields Name and Weight. Then add two unexported fields named onHand and sold. Declare a factory function called New to create values of type toy and accept parameters for the exported fields. Then declare methods that return and update values for the unexported fields.

**Part B** Create a program that imports the toy package. Use the New function to create a value of type toy. Then use the methods to set the counts and display the field values of that toy value.

[Template](exercises/template1) |
[Answer](exercises/exercise1)
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
