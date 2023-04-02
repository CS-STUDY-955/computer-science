# 1. 웹 애플리케이션의 전역적인 정보를 저장하고 있는 객체로서, 웹 애플리케이션에서 사용할 수 있는 공통 자원, 설정 정보 등을 제공하는 것은?
1. HttpServletRequest
2. HttpSession
3. HttpContext
4. Cookie

<details>
<summary>정답</summary>
3번<br>
Servlet 관련 주요 객체 중 HttpContext에 관련된 설명이다.
</details>
<br>

# 2.  HTTP Servlet life cycle를 순서대로 나열하시오
1. destroy
2. constructor
3. init
4. service

<details>
<summary>정답</summary>
2 3 4 1<br>
Constructor가 init(초기화) 보다 먼저 수행된다. <br>
loading단계에서는 static 변수들이 메모리에 탑재된다.
</details>
<br>

# 3. page이동 시 forward()와 sendRedirect()의 차이점에 대해 서술하시오.
<br>
<details>
<summary>정답</summary>
forward()는 RequestDispatcher 클래스를 통해 request.getRequestDispatcher(path)을 불러오고, dispatcher의 forward(request, response)를 호출하여 실행한다. <br>

- forward가 contextPath를 붙여서 감
- 이동 범위 : 동일 서버 내 경로
- 기존 request, response가 그대로 전달, 이를 통해 데이터를 유지
- 속도 : 비교적 빠름

<br>
sendRedirect는 response.sendRedirect(location)을 통해 수행됨.<br>

- sendRedirect가 contextPath 없이 감
- 이동범위 : 동일 서버 포함 타 url 가능
- 기존 request/response 소멸하고 새로운 request, response생성
- forward()에 비해 느리고, reqeust로는 data저장 불가하여 session이나 cookie를 이용해야 함
</details>
<br>

# 4. 웹 서버에서 요청된 URL에 대해 HTTP 메서드를 허용하지 않을 때 발생하는 에러는?

<details>
<summary>정답</summary>
405<br>
</details>
<br>

# 5. 다음 scriplet 표현 중 올바른 것은?
1. 
```
<%
if( 5>3){
    System.out.println("프린트");
}
%>
```
2. 
```
<%
int num1 = 12;
int num2 = 7;
out.println(num1-num2);
%>
```
3. 
```
<!-- sciplet 주석 입니다. -->
```
4. 
```
<%= num1.length(); %>
```

<details>
<summary>정답</summary>
1, 2번<br>
1번,
2번 : 올바른 표현식<br>
3번 : 주석 형식은 <%--주석 --%> <br>
4번 : 표현식(출력)에 문자열 뒤에는 ; 붙지 않음<br>

</details>
<br>

# 6. EL연산자 중 비어있지 않음을 나타내는 것은?
<details>
<summary>정답</summary>
not empty<br>
</details>
<br>

# 7. 다음 빈칸에 들어갈 알맞은 단어를 작성하시오.
```javascript
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>
  <head>
    <title>Title</title>
  </head>
  <body>
    <table>
      <c:___(1)____ var="item" items="${itemList}"> 
        <tr><td>__(2)__</td></tr>
      </c:___(1)____>
    </table>
  </body>
</html>
```
<details>
<summary>정답</summary>
(1) : forEach <br>
(2) : ${item} 
</details>
<br>

# 8. 다중 조건 비교시 빈칸에 알맞은 단어를 작성하시오
  ```xml
  <c:choose>
    <c:____ ____="${name eq '홍길동'}"> <!-- 1, 2-->
        홍길동
    </c:____> <!-- 1 -->
    <c:____ ____="name eq '이순신' "> <!-- 1, 2 -->
        이순신
    </c:____> <!-- 1 -->
    <c:________>기타</c:________> <!-- 3 -->
  </c:choose>
  ```

<details>
<summary>정답</summary>
(1) : when <br>
(2) : test
(3) : otherwise
</details>
<br>

# 9. 쿠키의 시간을 설정하는 메서드 이름은?

<details>
<summary>정답</summary>
setMaxAge()
</details>
<br>

# 10. 쿠키와 세션에 대한 설명으로 올바른 설명을 고르시오.
1. Cookie는 object 타입으로 저장된다.
2. Cookie 저장 시 사이트당 저장 개수 제한은 없지만, 클라이언트에 저장할 수 있는 총 쿠키의 양은 제한된다.
3. HttpSession을 가져올 때, parameter값을 주지 않을 경우, 세션이 없으면 null을 반환한다.
4. 세션에 정보를 등록할 떄, 타입, 크기, 갯수에 제한이 없다.
5. setCookie() 메서드를 통해 사용자 시스템에 쿠키를 저장한다.

<details>
<summary>정답</summary>
4번<br>

1. 쿠키는 문자열만 가능하다<br>
2. 쿠키는 client browser에 저장되고, 4kb크기제한이 있으며, 사이트당 20개, 클라이언트 당 300개 제한된다.
3. request.getSession()을 통해 HttpSession을 가져올 수 있으며, 값을 주지 않으면 true이다<br>
    - true 일 경우 
        - 세션이 없으면 new 를 통해 새로 생성하여 return
        - 세션이 존재하면 기존 세션 반환
    - false 일 경우
        - 세션이 없으면 null 반환
        - 세션이 존재하면 기존 세션 반환
5. response.addCookie(cookieName); 이다.
</details>
<br>