## Web 워크숍

이 자료는 Go로 강건하고 잘 테스트된 HTTP 기반 어플리케이션을 개발하는 방법을 배울려는 개발자를 위한 자료입니다. 이 워크숍을 통해서 Go로 Web, SOA와 API 어플리케이션을 개발하는 방법을 배울 수 있습니다.

## HTTP 기본

web과 HTTP가 어떻게 동작하는지 기본적인 이해하기 위해서, 간단한 “Hello World” app을 작성해 봅시다. Go로 web 서버를 시작하는 방법, request를 받고 response를 반환하는 내용을 다룹니다.

[기본](basics/README.md)

## HTTP 테스팅

코드를 작성해 보았으니 이번에는 HTTP Go 어플리케이션을 테스트하는 방법에 대해서 알아봅시다. HTTP 어플리케이션을 테스팅하는 2가지 방식을 소개합니다.

[Testing](testing/README.md)

## POST Requests

HTTP 어플리케이션은 단순히 content만 제공하는 것뿐만 아니라 content를 가질 수도 있습니다. GET request를 보내고 POST request, form처리, 파일 업로드 처리와 이 모든 것들을 테스트하는 방법을 제공합니다.

[Post Requests](posts/README.md)

## HTML Templates

이제 기본적인 web 앱을 작성하고 테스트할 수 있습니다. 이제 여기에 몇 가지 기능을 추가할 수 있습니다. 이 섹션에서는 Go template를 이용해서 HTML를 생성하기, static 파일 제공, 바이너리로 이 파일을 묶는 방법에 대해서 알아봅니다.

[Templates](templates/README.md)

## Sessions과 Cookies

session과 cookies를 관리하는 것은 모든 web 어플리케이션에서 중요한 부분입니다. 사용자가 "로그인" 상태를 유지하거나 사이트에 방문한 사용자를 추적하는 것과 같은 핵심 개념을 배우게 된다.

[Sessions과 Cookies](sessions_cookies/README.md)

## REST 개요

여기서부터 어플리케이션이 복잡해지기 시작합니다. 여기서부터 web 어플리케이션을 개발하는데 필요한 디자인 패턴에 대해서 알아봅니다. 특히 RESTful 디자인에 대해서 알아봅시다.

[REST](rest/README.md)

## Alternative Muxers

여기서부터 Go의 기본 muxer는 제약이 있습니다.  muxers/routers의 3가지 타입에 대해서 알아봅시다.
The basic muxer in Go has gotten us a long way by this point, but it has its limitations. Let’s tour three very different types of muxers/routers.

[Muxing](muxers/README.md)

## 미들웨어

미들웨어를 사용하여 로깅, 인증 및 다른 타스크와 같이 공통으로 실행하는 코드로 request를 어플리케이션으로 래핑할 수 있습니다.

[미들웨어](middleware/README.md)

## 데이터 직렬화(Data Serialization)

API를 만들기 전에 데이터를 직렬화하는 방법을 이해햐야 합니다. 2가지 공통 데이터 포맷을 살펴봅니다. 여러분의 API의 요구에 맞게 이 포맷을 커스터마이즈하는 방법도 다룹니다.

[Serializers](serializers/README.md)

## APIs

이제는 Go로 모든 기능을 지원하는 HTML 어플리케이션을 만들 수 있어야합니다. 이제는 다른 어플리케이션이 사용할 수 있게 API를 만드는 것에 대해서 눈을 돌려봅시다. API(RESTful & HyperMedia)를 만드는 2가지 방식을 소개합니다. API 버전을 처리하는 방식에 대해서 알아봅시다.

[Web APIs](apis/README.md)

## HTTP APIs 사용하기

API를 제대로 사용하지 못한다면 API가 있어도 쓸모가 없습니다. API, 마샬/언마샨 데이터, request header 설정 등을 사용하기 위해서 Go를 사용하는 방법에 대해서 알아봅시다.

[Consuming APIs](consuming/README.md)

## Web Sockets

web이 변경되고 사용자는 동적이고 빠르고 인터렉티브한 web 어플리케이션을 기대합니다. web socket을 이용해서 프론트-엔드(JavaScript/HTML)와 백-엔드(Go) 사이에 직접적인 양방향 통신이 가능합니다.

[Web Sockets](sockets/README.md)

## Authentication

web 앱에 인증을 추가하는 여러가지 기술과 패키지에 대해서 알아봅시다.

[Authentication](auth/README.md)

## TLS

일반 text로 중요한 데이터를 보내는 것은 좋은 생각이 아닙니다! TLS를 이용해서 여러분의 어플리케이션을 안전하게 하는 방법을 배워봅시다.

[TLS](tls/README.md)

## Shutdown

web 서버를 생성하는 것까지 다뤘습니다. 이제 필요할때 셧다운하는 방법에 대해서 알아봅시다. 안전하게 셧다운하는 방법이 필요합니다.

[Shutdown](shutdown/README.md)