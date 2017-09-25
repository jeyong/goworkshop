## 패키지 기반 디자인 (Package Oriented Design)

_패키지 기반 디자인은 특정 패키지가 어느 Go project에 속하는지를 개발자가 식별할 수 있게 합니다. 디자인 가이드라인은 해당 패키지가 반드시 지켜야 합니다. 해당 Go project가 무엇이며 어떻게 구조화되어 있는지를 정의합니다. 마지막으로 팀 멤버들 사이에 의사소통이 잘 되도록하며 깔끔한 패키지 디자인과 프로젝트 아키텍쳐가 되도록 돕는 역할을 합니다. 

## 링크

https://www.goinggo.net/2017/02/design-philosophy-on-packaging.html  
https://www.goinggo.net/2017/02/package-oriented-design.html  

## 히스토리

2000년에 Mihai Budiu가 진행한 Brian Kernighan와의 인터뷰에서 다음과 같은 질문을 했다: 

**_“당신의 관점에서 C에서 가장 나쁜 특징이 무엇인지 말해주시겠어요”?_**

다음과 같이 Brian이 답변했다:

**_“제가 생각하기에 C가 가진 실제 문제는 큰 프로그램을 구조화하는데 필요한 매커니즘을 제공하지 않는다는 것입니다. 여러 부분들을 별도로 유지하기 위해서는 프로그램 내부에 "firewalls"를 생성해야 하니까요. 이런 것을 모두를 할 수 없다는 뜻은 아닙니다. 이를 시뮬레이션할 수 있지만 컴파일러나 언어 자체가 도움을 주지는 않으니까요.

## 기본 구조

* 패키징은 다른 언어에서 소스 코드를 구조하는 방법과 충돌이 발생한다.
* 다른 언어에서 패키징은 사용하거나 무시할지 선택할 수 있는 특징이다. 
* 소스트리에서 마이크로서비스의 개념을 적용하는 것처럼 패키징을 생각할 수 있다.
* 모든 패키지는 "first class"이며 여러분 프로젝트에서 소스 트리에 정의한 것만 계층을 갖는다.
* 패키지의 일부를 외부로 "오픈"하는 방법이 필요하다.
* 2개 패키지는 서로 import할 수 없다. import는 일방향으로만 존재한다.

## 디자인 철학

* **목적을 분명히 가져야, 패키지는 반드시 목적을 제공해야만 한다. 단순히 포함하는 정도로는 안된다.**
    * 패키지는 반드시 제공하는 것이 무엇인지에 대한 의도를 반드시 이름으로 사용해야만 한다.
    * 패키지는 서로 이질적인 의도를 가진 것을 기반으로 하면 안된다.
* **유용해야, 패키지는 중점을 두는 것에 맞춰서 해당 사용자에 맞게 설계해야만 한다.**
    * 패캐지는 사용하기에 직관적이고 단순해야만 한다.
    * 패키지는 리소스와 성능에 미치는 옇향을 고려해야만 한다.
    * 패키지는 변경에 따른 영향이 전파되지 않도록 사용자의 어플리케이션을 보호해야만 한다.
    * Packages must prevent the need for type assertions to the concrete.
    * Packages must reduce, minimize and simplify its code base.
* **이식하기 좋아야, 패키지는 재사용을 염두에 두고 설계해야만 한다.**
    * 패키지는 이식성을 가장 높은 수준으로 고려해야만 한다.
    * 패키지는 합리적이고 실제적인 경우에 설정 정책을 줄여야만 한다.Packages must reduce setting policy when it’s reasonable and practical.
    * 패키지가 의존성의 유일한 지점이 되면 안된다.

## 프로젝트 구조

```
Kit                     Application

├── CONTRIBUTORS        ├── cmd/
├── LICENSE             ├── internal/
├── README.md           │   └── platform/
├── cfg/                └── vendor/
├── examples/
├── log/
├── pool/
├── tcp/
├── timezone/
├── udp/
└── web/
```

* **vendor/**  
Good documentation for the `vendor/` folder can be found in this Gopher Academy [post](https://blog.gopheracademy.com/advent-2015/vendor-folder) by Daniel Theophanes. For the purpose of this post, all the source code for 3rd party packages need to be vendored (or copied) into the `vendor/` folder. This includes packages that will be used from the company `Kit` project. Consider packages from the `Kit` project as 3rd party packages.

* **cmd/**  
All the programs this project owns belongs inside the `cmd/` folder. The folders under `cmd/` are always named for each program that will be built. Use the letter `d` at the end of a program folder to denote it as a daemon. Each folder has a matching source code file that contains the `main` package.

* **internal/**  
Packages that need to be imported by multiple programs within the project belong inside the `internal/` folder. One benefit of using the name `internal/` is that the project gets an extra level of protection from the compiler. No package outside of this project can import packages from inside of `internal/`. These packages are therefore internal to this project only.

* **internal/platform/**  
Packages that are foundational but specific to the project belong in the `internal/platform/` folder. These would be packages that provide support for things like databases, authentication or even marshaling.

## Validation

<u>**Validate the location of a package.**</u>
* `Kit`
    * Packages that provide foundational support for the different `Application` projects that exist.
    * logging, configuration or web functionality.
* `cmd/`
    * Packages that provide support for a specific program that is being built.
    * startup, shutdown and configuration.
* `internal/`
    * Packages that provide support for the different programs the project owns.
    * CRUD, services or business logic.
* `internal/platform/`
    * Packages that provide internal foundational support for the project..
    * database, authentication or marshaling.
    
<u>**Validate the dependency choices.**</u>
* `All`
    * Validate the cost/benefit of each dependency.
    * Question imports for the sake of sharing existing types.
    * Question imports to others packages at the same level.
    * If a package wants to import another package at the same level:
        * Question the current design choices of these packages.
        * If reasonable, move the package inside the source tree for the package that wants to import it.
        * Use the source tree to show the dependency relationships.
* `internal/`
    * Packages from these locations CAN’T be imported:
        * `cmd/`
* `internal/platform/`
    * Packages from these locations CAN’T be imported:
        * `cmd/`
        * `internal/`
        
<u>**Validate the policies being imposed.**</u>
* `Kit`, `internal/platform/`
    * NOT allowed to set policy about any application concerns.
    * NOT allowed to log, but access to trace information must be decoupled.
    * Configuration and runtime changes must be decoupled.
    * Retrieving metric and telemetry values must be decoupled.
* `cmd/`, `internal/`
    * Allowed to set policy about any application concerns.
    * Allowed to log and handle configuration natively.
    
<u>**Validate how data is accepted/returned.**</u>
* `All`
    * Validate the consistent use of value/pointer semantics for a given type.
    * When using an interface type to accept a value, the focus must be on the behavior that is required and not the value itself.
    * If behavior is not required, use a concrete type.
    * When reasonable, use an existing type before declaring a new one.
    * Question types from dependencies that leak into the exported API.
        * An existing type may no longer be reasonable to use.
        
<u>**Validate how errors are handled.**</u>
* `All`
    * Handling an error means:
        * The error has been logged.
        * The application is back to 100% integrity.
        * The current error is not reported any longer.
* `Kit`
    * NOT allowed to panic an application.
    * NOT allowed to wrap errors.
    * Return only root cause error values.
* `cmd/`
    * Allowed to panic an application.
    * Wrap errors with context if not being handled.
    * Majority of handling errors happen here.
* `internal/`
    * NOT allowed to panic an application.
    * Wrap errors with context if not being handled.
    * Minority of handling errors happen here.
* `internal/platform/`
    * NOT allowed to panic an application.
    * NOT allowed to wrap errors.
    * Return only root cause error values.

<u>**Validate testing.**</u>
* `cmd/`
    * Allowed to use 3rd party testing packages.
    * Can have a `test` folder for tests.
    * Focus more on integration than unit testing.
* `kit/`, `internal/`, `internal/platform/`
    * Stick to the testing package in go.
    * Test files belong inside the package.
    * Focus more on unit than integration testing.

<u>**Validate recovering panics.**</u>
* `cmd/`
    * Can recover any panic.
    * Only if system can be returned to 100% integrity.
* `kit/`, `internal/`, `internal/platform/`
    * Can not recover from panics unless:
        * Goroutine is owned by the package.
        * Can provide an event to the app about the panic.
___
모든 자료에 대해서 [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0) 라이센스가 적용됩니다.
