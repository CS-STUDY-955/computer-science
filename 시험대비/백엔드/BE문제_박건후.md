# 1. 웹 애플리케이션의 전역적인 정보를 저장하고 있는 객체로서, 웹 애플리케이션에서 사용할 수 있는 공통 자원, 설정 정보 등을 제공하는 것은?
1. HttpServletRequest
2. HttpSession
3. HttpContext
4. Cookie

<br>

# 2.  HTTP Servlet life cycle를 순서대로 나열하시오
1. destroy
2. constructor
3. init
4. service

<br>

# 3. page이동 시 forward()와 sendRedirect()의 차이점에 대해 서술하시오.
<br>

# 4. 웹 서버에서 요청된 URL에 대해 HTTP 메서드를 허용하지 않을 때 발생하는 에러는?
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

<br>

# 6. EL연산자 중 비어있지 않음을 나타내는 것은?

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
<br>

# 9. 쿠키의 시간을 설정하는 메서드 이름은?
<br>

# 10. 쿠키와 세션에 대한 설명으로 올바른 설명을 고르시오.
1. Cookie는 object 타입으로 저장된다.
2. Cookie 저장 시 사이트당 저장 개수 제한은 없지만, 클라이언트에 저장할 수 있는 총 쿠키의 양은 제한된다.
3. HttpSession을 가져올 때, parameter값을 주지 않을 경우, 세션이 없으면 null을 반환한다.
4. 세션에 정보를 등록할 떄, 타입, 크기, 갯수에 제한이 없다.
5. setCookie() 메서드를 통해 사용자 시스템에 쿠키를 저장한다.

<br>