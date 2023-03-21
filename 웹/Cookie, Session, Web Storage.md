# Cookie, Session, Web Storage

![google-f12](https://user-images.githubusercontent.com/68081743/226602808-197fe4cb-6faf-4eed-993d-177cafff20eb.JPG)

## Cookie

- 클라이언트가 서버에 방문한 정보를 클라이언트의 로컬에 저장하는 작은 파일을 의미함
- 클러이언트 브라우저 메모리 혹은 하드디스크에 저장
- 하나의 사이트에 약 4KB 까지 저장 가능하며 유효기간이 존재
- 웹 사이트에서 쿠키를 설정하면 이후 모든 웹 요청은 쿠키 정보를 포함하여 서버로 전송함
- 클라이언트에 저장되기 때문에 보안에 취약하다는 단점이 있음

```javascript
document.cookie = "name=value; expires=Thu, 21 Mar 2024 12:00:00 UTC; path=/"; // 쿠키 생성

document.cookie = "name=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;"; // 쿠키 삭제
```

<br>

## Session

- 세션은 브라우저가 서버에 연결되어 있는 동안 유지하는 데이터 집합
- 클라이언트는 HTTP Session ID를 메모리에 저장하고있음
- 브라우저 종료시 삭제됨
- 서버의 리소스를 사용함
- 세션 사용시 서버를 확장시키는 것이 어려워짐

<br>

## Web Storage

- 기존 웹 환경의 쿠키와 비슷한 개념
- 클라이언트에 데이터를 저장할 수 있도록 HTML5부터 지원하는 저장소
- Key와 Value의 형태로 데이터를 저장
- 쿠키와 달리 서버에 전송되지 않으므로 서버에 부담이 가지 않음
- 필요한 경우에만 꺼내 쓰는 것이므로 자동 전송의 위험상이 없음
- 약 5MB ~ 10MB까지 저장 가능하며(브라우저 별로 상이함) 유효기간이 존재하지 않음
- Local Storage와 Session Storage가 있음

<br>

## Local Storage

- window.localStorage 객체
- 브라우저를 종료해도 유지되며, 직접 삭제하지 않는 한 영구 저장
- 도메인별로 생성되며 다른 도메인의 로컬 스토리지에는 접근 불가
- 서로 다른 브라우저 탭이라도 동일한 도메인이라면 동일한 로컬 스토리지 사용
- 지속적으로 필요한 정보를 저장하기 좋음 (ex. 자동 로그인)

```javascript
localStorage.setItem("myCat", "Tom"); // 로컬 스토리지 추가
const cat = localStorage.getItem("myCat"); // 읽기
localStorage.removeItem("myCat"); // 삭제
```

<br>

## Session Storage

- window.sessionStorage 객체
- 세션 쿠키와 달리 탭/윈도우 단위로 세션 스토리지 생성
- window 객체와 동일한 유효 범위 및 생존기간을 가짐
- 탭/윈도우를 닫을시 데이터 삭제
- 서로 다른 세션 스토리지는 서로 영향을 주지 않으며 독립적임
- 잠시 동안 필요한 정보를 저장하기 좋음 (ex. 일회성 로그인, 입력 폼 저장)

```javascript
sessionStorage.setItem("key", "value"); // 세션 스토리지 추가
let data = sessionStorage.getItem("key"); // 읽기
sessionStorage.removeItem("key"); // 삭제
```

<br>

## Web SQL

- Web Storage 보다 구조적이고 체계화된 관계형 데이터를 저장하기 적합
- SQLite 기반이며, 클라이언트에 직접 내장되어 있음
- 하지만 W3C(World Wide Web 표준 개발 기구)에서 2010년에 스펙 관리를 중단했으며, 최근 브라우저들에서도 지원이 중단되고 있는 추세이기에 IndexedDB로 전환하는 것이 좋음

<br>

## IndexedDB

- Transaction Database를 사용하고 Key-Value로 데이터를 관리하며, B-Tree구조를 지님
- same-origin policy를 따르기 때문에 프로토콜, 포트, 호스트가 동일해야함
- 데이터는 영구적으로 유지됨
