# BE 과목평가 예상 문제
## 1. 서블릿이 생성되고 실행되면서 다음 메서드들이 호출되는 순서를 올바르게 배치하시오.
a. service()  
b. init()  
c. 생성자  
d. doGet()  
e. destroy()  

## 2. 다음 빈칸을 채우고, 액션 태그 <jsp:include>와 JSTL <c:import>의 공통점과 차이점을 설명하시오.
```html
<c:import _1_ = 'nav.jsp' />
<jsp:include _2_ = 'nav.jsp' />
```

## 3. EL은 내장객체를 이용해 Scope를 지정하지 않았을 때, 특정 순서에 따라 자동으로 지정해준다. 우선순위가 높은 순서대로 scope를 서술하시오.

## 4. 다음은 jsp에서 값을 출력하는 방법이다. 다음 중 member의 id가 정상적으로 출력되지 않는 방법은? (member 클래스에는 getId()메서드가 정의되어 있다.)
1. ${member.id}
2. ${member['id']}
3. <% out.print(member.getId()); %>
4. <%= member.getId(); %>

## 5. 다음 중 jsp 기본 내장 객체가 아닌 것은?
1. cookie
2. page
3. config
4. out

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