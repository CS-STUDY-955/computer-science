# Back End

### <b>1</b>. 다음 중 기존 Model1 방식과 비교하여 Model2 구조(MVC Pattern)의 장점으로 옳지 않은 것은?

1. 기존에 JSP에서 모두 처리하던걸 기능에 따라 나눔으로써 분업과 유지보수에 용이하다.
2. 구조가 단순하며 직관적이어서 배우기 쉽다.
3. 규모가 커져도 기존의 방식보다 상대적으로 코드가 덜 복잡하다.
4. 확장성이 뛰어나다.

<br>

### <b>2</b>. 세션과 관련된 메서드 중 바인딩된 모든 세션을 삭제하는 메서드명은?

```

```

<br>

### <b>3</b>. 다음 중 나머지와 성격이 다른 JSP 내장 객체는?

1. request
2. response
3. session
4. pageContext

<br>

### <b>4</b>. Servlet의 function 함수를 요청받아 실행했을때, JSP에서 Point 클래스의 print() 메서드를 올바르게 호출하는 EL 문은?

```java
private void function(HttpServletRequest request, HttpServletResponse response) {
    request.setAttribute("point", new Point(3, 5));
    RequestDispatcher dispatcher = request.getRequestDispatcher("/index.jsp");
    dispatcher.forward(request, response);
}
```

```java
static class Point {
    int x, y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public String print() {
        return "("+x+", "+y+")";
    }
}
```

1. ${point.print}
2. ${point.print()}
3. ${request.point.print()}
4. ${requestScope.point.print}

<br>

### <b>5</b>. EL 문으로 객체에 접근할 때, 다음과 같이 property 이름만으로 참조할 경우 객체를 찾는 scope의 순서는?

```java
${userinfo}
```

1. pageScope -> reqeustScope -> sessionScope -> applicationScope
2. pageScope -> applicationScope -> requestScope -> sessionScope
3. pageScope -> applicationScope -> sessionScope -> requestScope
4. pageScope -> requestScope -> applicationScope -> sessionScope

<br>

### <b>6</b>. 세션 사용시, 서버는 클라이언트를 구분하기 위한 쿠키를 생성하여 클라이언트 측에 저장한다. 이 쿠키의 이름(Name)은?

1. SID
2. UUID
3. SESSIONID
4. JSESSIONID

<br>

### <b>7</b>. 다음 중 JSP의 지시자로 설명이 올바르지 않은 것은?

1. page : 현재 페이지에 대한 정보를 제공해주며, 속성으로 contentType, import 등을 사용할 수 있다.
2. taglib : 커스텀 태그를 이용할때 사용한다.
3. include : 특정 jsp 파일을 페이지에 포함할 때 사용한다.
4. session : 페이지의 세션 사용 여부를 설정하며 기본값은 true이다.

<br>
