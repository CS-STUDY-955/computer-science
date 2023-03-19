# FE 과목평가 예상 문제
## 1. 다음과 같이 form의 작성 내용을 URL로 요청하기 위해 사용하는 form의 속성을 지정하시오.
```html
<form ____="/submit">
    /* content */
</form>
```

<details>
    <summary>정답</summary>
    <b>action</b> <br>
    method랑 헷갈리라고 적어놨음
</details>

## 2. HTML4와 HTML5의 가장 큰 차이는 시맨틱 태그이다. 시맨틱 태그를 사용했을 때 얻을 수 있는 장점과 div의 역할을 하는 시맨틱 태그의 종류를 3가지만 쓰시오.

<details>
    <summary>정답</summary>
    <b>header, nav, aside, main, section, article, footer</b> <br>
    - 검색엔진최적화(SEO) 🔍 : 검색엔진은 태그를 기반으로 페이지 내 검색 키워드의 우선순위를 판단한다. 따라서 제목은 h1, 중요한 단어는 strong 또는 em을 사용하는 등 의미에 맞는 올바른 태그르 사용하는 것이 중요하다. <br>
    - 시각장애가 있는 사용자가 스크린 리더를 사용하여 페이지를 탐색할 때 도움이 된다. <br>
    - 시맨틱 태그를 사용한 코드 블록을 찾는 것은 끝없는 div(div > div > div ...)를 탐색하는 것보다 훨씬 쉽다. <br>
    - W3C에 따르면 "시맨틱 웹을 사용하면 애플리케이션, 기업 및 커뮤니티에서 데이터를 공유하고 재사용할 수 있다"고 한다. (의미가 있는 요소는 개발자 모두에게 명확한 의미를 전달한다) <br>
    中 택 1
</details>

## 3. block 태그와 inline 태그의 차이점을 설명하고, 1가지씩만 쓰시오.

<details>
    <summary>정답</summary>
    <b>block은 width 속성의 값을 100%로 갖지만, inline은 컨텐츠 영역만큼만 갖는다.</b> <br>
    예시 태그는 알아서..
</details>

## 4. CSS는 요소를 특정하기 위한 여러 선택자가 존재한다. 그 중 ' ' 선택자와 '>'의 공통점과 차이점을 설명하시오.

<details>
    <summary>정답</summary>
    <b>' '는 자손 태그를 가리키고, '>'는 자식 태그를 가리킨다.</b> <br>
</details>

## 5. CSS의 position 속성 중, 속성값이 static이 아닌 자신의 첫 번째 상위 요소를 기준으로 배치되는 속성값은?
1. static
2. relative
3. absolute
4. fixed

<details>
    <summary>정답</summary>
    <b>absolute</b> <br>
</details>

## 6. JS는 여러 전역 객체를 지원한다. 그 중 alert를 메서드로 가지고 있는 전역 객체는?
1. window
2. document
3. screen
4. location

<details>
    <summary>정답</summary>
    <b>window</b> <br>
</details>

## 7. Bootstrap을 사용하면 얻을 수 있는 장점을 1가지만 쓰시오. 

<details>
    <summary>정답</summary>
    <b>디자인을 알고 있다면 반응형 웹을 쉽게 만들 수 있다 or 클래스를 외우고 있다면 쉽게 적당한 웹 사이트를 만들 수 있다</b> <br>
</details>

## 8. JS를 이용해 로그인이 되면 공간을 차지하지 않게 로그인 버튼을 숨기려고 한다. 빈칸을 채우시오.
```javascript
function login() {
    let loginBtn = document.getElementById("loginBtn");

    loginBtn.style.______ = "____";
}
```

<details>
    <summary>정답</summary>
    <b>display, none</b> <br>
</details>

## 9. Bootstrap은 grid 레이아웃을 지원한다. 한 행의 전체 컬럼 길이는 얼마인가?

<details>
    <summary>정답</summary>
    <b>12</b> <br>
</details>

## 10. CSS는 여러 방식으로 속성을 지정할 수 있고, 각 방식에 따른 우선순위가 존재한다. 우선 순위가 높은 순으로 배열하시오.
a. .class
b. #id
c. inline(HTML에 직접 지정)
d. !important
e. 태그 이름

<details>
    <summary>정답</summary>
    <b>d -> c -> b -> a -> e</b> <br>
</details>
