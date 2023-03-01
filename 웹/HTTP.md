# HTTP 기초
- HTTP는 HTML 문서와 같은 리소스들을 가져올 수 있도록 해주는 프로토콜
- HTTP는 웹에서 이루어지는 모든 데이터 교환의 기초임
- 하나의 완전한 문서는 텍스트, 레이아웃 설명, 이미지, 비디오, 스크립트 등의 하위 문서들로 재구성 됨

    <img src="https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview/http-layers.png" width =300>

- HTTP는 확장가능함
- 애플리케이션 계층
- TCP 등을 통해 전송 됨
- 클라이언트-서버 프로토콜
    - 요청은 사용자에 의해 전송
    - 각각의 개별적인 요청은 서버로 보내지고, 서버는 요청을 처리하고 응답을 제공
    - 요청과 응답 사이에 여러 객체 존재
        > 게이트웨이, 프록시(캐시)
        <img src = https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview/client-server-chain.png>

- 프록시 : 애플리케이션 계층에서 동작함
    - 캐싱
    - 필터링(바이러스 백신 스캔, 유해 컨텐츠 차단 기능 등)
    - 로드 밸런싱(여러 서버들이 서로 다른 요청을 처리하도록 허용)
    - 인증(다양한 리로스에 대한 접근 제어)
    - 로깅(이력 정보를 저장)

---

## HTTP 요청 구조
- Request Line
    - HTTP 메서드를 사용해 서버가 수행해야 할 동작을 나타냄
- Header
- Body
<img src="https://velog.velcdn.com/images%2Fgparkkii%2Fpost%2F0a8a066b-b53b-4c86-a522-32e848c5f54f%2FHTTP_Request.png" width= 500>

## HTTP 응답 구조
- Status Line
    - 프로토콜 버전
    - 상태코드(요청의 성공 여부 등)
    - 상태 텍스트(Not Found)
- Header
- Body
<img src = "https://velog.velcdn.com/images%2Fgparkkii%2Fpost%2Fc5ee6879-e3af-49f9-a8d0-5922b49c53ce%2FHTTP_Response.png" width= 500>

## HTTP 요청 메서드
- CONNECT : 요청한 리소스에 대해 양방향 연결을 시작하는 메서드
    - 클라이언트는 원하는 목적지와의 TCP연결을 HTTP 프록시 서버에 요청
    - 서버는 연결 생성
- DELETE : 지정한 리소스를 삭제
    - 항상 명령 수행을 보장하지 않음
    - 상태코드를 제공함
        >  202(Accepted), 204(No content), 200(OK)
- GET : 특정 리소스를 가져오도록 요청
    - 오직 데이터를 받는 역할만 함
- HEAD : 특정 리소스를 GET 메서드로 요청했을 때 돌아올 헤더를 요청
    - 즉, GET과 동일한 응답을 요구하지만, 응답 본문은 포함하지 않음
        > 리소스가 존재하는지 확인할 때 사용
- OPTIONS : 주어진 URL 또는 서버에 대해 허용된 통신 옵션을 요청함
    - 해당 서버의 지원가능한 메서드를 확인함(GET, POST, ...)
- PUT : 새로운 리소스를 생성하거나, 리소스를 대체함
    - 멱동성을 가짐: 한번 보내도, 여러번 보내도 같은 효과를 나타냄
    - 서버의 상태가 동일함
- PATCH : 리소스의 부분적인 수정할 때 사용 함
- POST : 서버로 데이터를 전송
    - HTML 양식을 통해 서버로 전송하며, 서버에 변경사항을 만듦

<img src = "https://raw.githubusercontent.com/Songwonseok/CS-Study/main/Web/images/HTTP-Mehtod-1.JPG" width = 500>

---

## HTTP응답 상태 코드
- **1xx (조건부 응답)** 
  - 100 - continue
    - 클라이언트가 서버로 보낸 요청에 문제가 없으니 다음 요청을 이어서 보내도 된다는 것을 의미
    - 즉, 웹서버가 해당 응답을 할수 있도록 구현 했다면 100 continue로 응답한다.
- **2xx (성공)** 
  - 200 - OK 
    - 요청 성공(GET성공, POST본문전송완료 등)
  - 201 - Created
    - POST 메서드 성공, 서버에 리소스 생성 완료
  - 202 - Accepted 
    - 요청이 접수되었으나, 아직 해당 요청을 처리중이거나 시작 전임을 의미
- **4xx (요청 오류)** 
  - 400 - Bad Requst / 사용자의 잘못된 요청
  - 401 - Unauthorized / 인증이 필요한 페이지 요청
  - 402 - Payment Required / 예약됨
  - 403 - Foibidden / 접근금지, 관리자가 차단
  - 404 - Not Found / 페이지 없음
  - 405 - Method Not Allowed / 허용되지 않은 HTTP Method 사용
  - 407 - Proxy Authentication Required / 프록시 인증 요구
  - 408 - Request Timeout / 요청 시간 초과
- **5xx (서버 오류)** 
  - 500 - Internal Server Error / 내부 서버 오류
  - 501 - Not Implemented / 웹 서버가 처리할 수 없음
  - 503 - Service Unnailable / 서비스 제공 불가
  - 504 - Gateway Uimeout / 게이트웨이 시간 초과
  - 505 - HTTP Version Not Supported / 해당 http 버전 지원 X


## 참고문헌
- https://developer.mozilla.org/ko/docs/Web/HTTP/Overview