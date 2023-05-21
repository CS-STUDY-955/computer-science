# REST, REST API, RESTful

## REST

### 개요

- Representational State Transfer의 약자
- 자원을 이름으로 구분하여 해당 자원의 상태(정보)를 주고받는 것
  - 자원이란, 해당 소프트웨어가 관리하는 모든 것을 의미
- 기존 웹 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있음
- URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시
- HTTP Method를 통해 CRUD를 적용

### 장점
- HTTP 프로토콜을 사용하므로, 별도의 인프라가 필요 없고, HTTP 표준 프로토콜을 따르는 모든 플랫폼에서 사용할 수 있다.
- 서버와 클라이언트의 역할이 명확하게 분리된다
- URI를 통해 REST API가 의도하는 바를 쉽게 파악할 수 있다.
  
### 단점
- 표준이 없다
- HTTP 메소드의 형태가 제한적이다
- 구형 브라우저에서 지원하지 않는 부분이 존재한다(PUT, DELETE)

### 구성 요소
1. 자원(Resource): URI
  - 자원은 서버에 존재하며, 고유한 ID가 HTTP URI 형식으로 존재한다
2. 행위(Verb): HTTP: Method
  - GET, POST, PUT, DELETE 등의 메서드를 제공한다
3. 표현(Representation)
  - 클라이언트가 자원의 상태에 대한 조작을 요청하면 Server는 응답을 보낸다
  - 보통 JSON, XML의 형태로 데이터를 주고받는 것이 일반적이다.

### REST의 특징
1. Server-Client(서버-클라이언트 구조)
2. Stateless(무상태)
  - HTTP 프로토콜이 Stateless 한것처럼, REST도 역시 Stateless하다.
3. Cacheable(캐시 처리 가능)
  - 이 역시 HTTP 프로토콜이 지원한다
4. Layered System(계층화)
  - REST 서버를 다중 계층으로 구성하여, 비즈니스 로직 앞에 보단, 로드밸런싱, 암호화, 사용자 인증등을 추가시킬 수 있다.

## REST API

- REST 기반으로 서비스 API를 구현한 것
- REST가 HTTP를 기반으로 구현되므로, HTTP를 지원하는 프로그램언어라면 무엇이든 클라이언트와 서버를 구현할 수 있다.

## RESTful

- REST의 원리를 따르는 시스템을 RESTful 하다고 지칭할 뿐, 공식적으로 발표된 용어는 아니다
- 이해하기 쉽고, 사용하기 쉬운 REST API를 만드는 것이 목적
- 단, RESTful한 시스템을 만든다고 해도, 모든 기능을 REST하게 만들 필요는 없다
  - 예를 들어, 로그인의 경우, DB에서 해당하는 ID와 비밀번호를 가진 유저의 정보를 조회하는 것이니 GET방식을 써야 한다.
  - 하지만, GET방식을 사용할 경우, 로그인 정보가 모두 드러나버리는 단점이 존재한다.
  - 이러한 경우, REST라 하더라도 POST를 사용하여 기능을 구현하는 것이 옳다
  - 또는 로그인 과정은 비즈니스단이 아니므로 REST가 아닌 스프링 시큐리티나 Oauth2를 사용하여 분리설계 할 수도 있다.

## 참고 자료

- <https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html>
