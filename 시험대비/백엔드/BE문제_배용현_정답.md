# BE 과목평가 예상 문제
## 1. 서블릿이 생성되고 실행되면서 다음 메서드들이 호출되는 순서를 올바르게 배치하시오.
a. service()  
b. init()  
c. 생성자  
d. doGet()  
e. destroy()  

<details>
    <summary>정답</summary>
    <b>c > b > a > d > e</b> <br>
    doGet()은 service()이후 호출된다.
</details>

## 2. 다음 빈칸을 채우고, 액션 태그 <jsp:include>와 JSTL <c:import>의 공통점과 차이점을 설명하시오.
```html
<c:import _1_ = 'nav.jsp' />
<jsp:include _2_ = 'nav.jsp' />
```
<details>
    <summary>정답</summary>
    <b>1: url, 2: page</b> <br />
    <b>공통점: </b> 다른 페이지의 내용을 현재 페이지에 포함시키는 태그이다. <br>
    <b>차이점1: </b> import와 달리 include는 포함시킨 페이지의 변수를 사용할 수 없다. <br>
    <b>차이점2: </b> import와 달리 include는 외부 jsp파일을 포함시킬 수 없다. <br>
</details>

## 3. EL은 내장객체를 이용해 Scope를 지정하지 않았을 때, 특정 순서에 따라 자동으로 지정해준다. 우선순위가 높은 순서대로 scope를 서술하시오.

<details>
    <summary>정답</summary>
    <b>page > request > session > application</b> <br>
    범위가 작은 scope를 우선순위가 높게 지정한다.
</details>

## 4. 다음은 jsp에서 값을 출력하는 방법이다. 다음 중 member의 id가 정상적으로 출력되지 않는 방법은? (member 클래스에는 getId()메서드가 정의되어 있다.)
1. ${member.id}
2. ${member['id']}
3. <% out.print(member.getId()); %>
4. <%= member.getId(); %>

<details>
    <summary>정답</summary>
    <b>4. <%= member.getId(); %></b> <br>
    expression tag에는 ;가 들어가면 안된다.
</details>

## 5. 다음 중 jsp 기본 내장 객체가 아닌 것은?
1. cookie
2. page
3. config
4. out

<details>
    <summary>정답</summary>
    <b>1. cookie</b> <br>
    cookie는 jsp 내장 객체로 지원되지 않는다. jsp 내장 객체 request의 getCookies()를 이용하거나 el 내장 객체 cookie를 이용해야 한다.
</details>

## 6. 다음은 상품 상세 조회 url과 상품 Controller의 상세 조회 메서드이다. 빈칸에 들어갈 메서드명으로 알맞은 것은?
```html
<a href="${root}/mobile?action=detail&mobileCode=${mobile.mobileCode}">
```
```java
private String detail(HttpServletRequest request, HttpServletResponse response) throws Exception {
    if(!isAuthorized(request)) 
        return "/user?action=mvLogin";
    
    Mobile mobile = mobileService.search(request._____1_____("mobileCode"));
    request._____2_____("mobile", mobile);
    return "/mobile/detailMobile.jsp";
}
```

<details>
    <summary>정답</summary>
    <b>1. getParameter, 2. setAttribute</b> <br>
    클라이언트에서 파라미터로 넘어온 변수는 getParameter로, 클라이언트로 넘겨줄 변수를 세팅할 때는 setAttribute로 지정한다.
</details>