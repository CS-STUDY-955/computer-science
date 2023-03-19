# Front End

### <b>1</b>. 다음 중 inline 태그가 아닌것은?

1. a
2. em
3. form
4. img

<br>

<details>
<summary>1번</summary>
<b>3번</b>. form<br>
form 태그는 block 태그이다.
</details>

<br>

### <b>2</b>. 다음은 html과 css 파일의 내용이다. h1 태그와 h2 태그의 내용에 적용되는 색깔은?

```html
<!-- test.html -->
<!DOCTYPE html>
<html>
  <head>
    <style type="text/css">
      @import url(h2-style.css);
    </style>
    <style type="text/css">
      h1 {
        color: green;
      }
      h2 {
        color: yellow;
      }
    </style>
    <link rel="stylesheet" href="h1-style.css" />
  </head>
  <body>
    <h1>h1 text</h1>
    <h2>h2 text</h2>
  </body>
</html>
```

```css
/* h1-style.css */
h1 {
  color: blue;
}
```

```css
/* h2-style.css */
h2 {
  color: red;
}
```

1. h1: blue, h2: red
2. h1: blue, h2: yellow
3. h1: green, h2: red
4. h1: green, h2: yellow

<br>

<details>
<summary>2번</summary>
<b>2번</b>. h1: blue, h2: yellow<br>
외부 스타일 시트와 내부 스타일 시트는 가장 아래쪽에 있는 스타일 시트가 반영된다.
</details>

<br>

### <b>3</b>. select 태그를 이용하여 다음과 같은 select box를 만드려고 할 때 빈칸에 들어갈 태그로 옳은 것은?

![q3-img](https://user-images.githubusercontent.com/68081743/226174266-5274d169-4809-4d9c-84e8-c9452736c8a8.JPG)

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <select>
    <________ label="주류">
      <option value="soju">소주</option>
      <option value="beer">맥주</option>
    </________>
    <________ label="음료">
      <option value="cola">콜라</option>
      <option value="cider">사이다</option>
    </________>
  </select>
</body>
</html>
```

1. li
2. opt
3. optg
4. optgroup

<br>

<details>
<summary>3번</summary>
<b>4번</b>. optgroup
</details>

<br>

### <b>4</b>. CSS의 position 속성의 값과 설명이 올바르게 연결된 것은?

1. absolute - position 속성의 기본값이다.
2. fixed - 자신의 상위 box속에서 top, left, right, bottom등의 속성으로 절대적인 위치를 지정한다.
3. static - top, left, right, bottom등의 속성을 지정할 수 없다.
4. relative - 일반적인 내용의 흐름으로 top, left 속성으로 거리를 지정할 수 있지만 right, bottom 속성으로 지정할 수 없다.

<br>

<details>
<summary>4번</summary>
<b>3번</b>. static - top, left, right, bottom등의 속성을 지정할 수 없다.<br>

|          |                                                                                                                                             |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| static   | 기본값으로 일반적인 내용물의 흐름. top, left, right, bottom 속성은 무시된다.                                                                |
| relative | 일반적인 내용물의 흐름이지만 top, left 속성으로 거리를 지정. bottom, right로도 지정할 수 있지만 각각 top, left 속성이 있는 경우엔 무시된다. |
| absolute | static을 제외한 자신의 상위 요소 속에서의 top, left, right, bottom등의 절대적인 위치를 지정.                                                |
| fixed    | 스크롤이 일어나도 항상 화면상의 지정된 위치에 있다.                                                                                         |

</details>

<br>

### <b>5</b>. 다음 코드를 실행 했을 때, true의 개수는?

```javascript
console.log(1 == "1");
console.log(0 === false);
console.log(null == undefined);
console.log("" == false);
console.log(15 == true);
console.log(NaN == false);
console.log(!"");
```

1. 3개
2. 4개
3. 5개
4. 6개

<br>

<details>
<summary>5번</summary>
<b>2번</b>. 4개<br>
위에서부터 순서대로 true, false, true, true, false, false, true이다.
비어있는 문자열, null, undefined, 숫자 0, NaN은 false로 간주된다.<br>
(null은 값이 없거나 비어있음(프로그램 레벨), undefined는 값이 초기화되지 않았음(시스템 레벨)을 의미)<br>
이 중 비어있는 문자열과 숫자 0은 false와 비교연산('==')을 했을 때 true를 반환하고 나머지는 false를 반환한다.<br>
숫자 또한 0을 제외한 모든 숫자들은 true로 간주되나 1을 제외하고는 true와 비교연산을 했을 때 false를 반환한다.
</details>

<br>

### <b>6</b>. 다음 코드를 실행했을 때 출력 결과로 옳은 것은?

```javascript
console.log(var1);
console.log(let1);
var var1;
let let1;
var1 = "var1";
let1 = "let1";
{
  var var1 = "var2";
  let let1 = "let2";
}
console.log(var1);
console.log(let1);
```

\* 보기에서 줄바꿈은 " - " 로 표현함.

1. undefined - undefined - var1 - let1
2. undefined - unedfined - var2 - let2
3. undefined - undefined - var2 - let1
4. 에러 메세지를 출력하며 정상적으로 실행되지 않는다.

<br>

<details>
<summary>6번</summary>
<b>4번</b>. 에러 메세지를 출력하며 정상적으로 실행되지 않는다.<br>
Hoisting은 var 키워드에서 적용되며, 변수 선언이 어디에 있든 다른 코드보다 먼저 실행된다.<br>
let 키워드와 const 키워드는 Hoisting을 지원하지 않아 변수 선언보다 먼저 사용할 수 없다.<br>
선언 전 var 변수를 출력하면 undefined를 출력하지만, let 변수는 "Cannot access before initialization" 에러를 출력한다.<br>
(+) var는 함수 레벨 스코프를 갖고 let, const는 블록 레벨 스코프를 갖는다. 문제에서 첫 두줄을 지우고 실행하면 출력 결과는 "var2 - let1"이 된다.<br>

|                        | let                     | const                            |
| ---------------------- | ----------------------- | -------------------------------- |
| 변수 중복 선언         | 불가                    | 불가                             |
| 선언시 초기화          | undefined로 자동 초기화 | 자동 초기화X, 선언시 초기화 필수 |
| 변수 재할당(값 바꾸기) | 가능                    | 불가                             |

\* const의 경우 객체의 원소를 재할당하는 것은 가능

</details>

<br>

### <b>7</b>. localStorage에 대한 설명으로 옳지 않은 것은?

1. 자바스크립트와 http 헤더를 통해 데이터를 조작할 수 있다.
2. 데이터 저장에 용량 제한이 없지만 문자열 데이터만 저장 가능하다.
3. 유효기간이 없고 영구적으로 이용 가능하다.
4. 프로토콜, 도메인, 포트가 다르면 접근이 불가하며 모바일에서도 이용할 수 있다.

<br>

<details>
<summary>7번</summary>
<b>1번</b>. 자바스크립트와 http 헤더를 통해 조작할 수 있다.<br>
localStorage는 자바스크립트로만 조작할 수 있으며 http 헤더로는 조작할 수 없다.
</details>

<br>

### <b>8</b>. 다음과 같은 코드를 실행했을 때, div3영역을 클릭한 경우 alert으로 호출하는 값의 순서로 옳은 것은?

\* 가장 하위 자식인 div3은 div2 영역 내에 있으며, div2는 div1 영역 내에 있다.

```html
<script type="text/javascript">
  var div1 = document.getElementById("div1");
  var div2 = document.getElementById("div2");
  var div3 = document.getElementById("div3");

  div1.addEventListener(
    "click",
    function (e) {
      alert("1");
    },
    true
  );
  div2.addEventListener(
    "click",
    function (e) {
      alert("2");
    },
    true
  );
  div3.addEventListener(
    "click",
    function (e) {
      alert("3");
    },
    true
  );
</script>
```

1. 1 > 2 > 3
2. 2 > 1 > 3
3. 3 > 2 > 1
4. 2 > 3 > 1

<br>

<details>
<summary>8번</summary>
<b>1번</b>. 1 > 2 > 3<br>
함수의 세번째 인자값이 true면 캡쳐링, false면 버블링이다.<br>
문제는 캡쳐링이므로 부모 요소부터 검사하여 1 > 2 > 3 순서가 된다.
</details>

<br>

### <b>9</b>. 다음 중 GET 방식과 POST 방식에 대한 설명으로 옳지 않은 것은?

1. GET 방식은 데이터를 http 패킷의 헤더 영역에 포함시켜 전송하고, POST 방식은 바디 영역에 포함시켜 전송한다.
2. GET 방식은 데이터 전송 길이에 제한이 있고 POST 방식은 제한이 없다.
3. GET 방식과 POST 방식 모두 캐싱을 이용해 요청을 빠르게 처리한다.
4. GET 방식과 POST 방식 모두 비동기 방식으로 결과를 조회한다.

<br>

<details>
<summary>9번</summary>
<b>3번</b>. GET 방식과 POST 방식 모두 캐싱을 이용해 요청을 빠르게 처리한다.<br>
GET 방식은 캐싱을 할 수 있지만 POST 방식은 캐싱을 할 수 없다.

</details>

<br>

### <b>10</b>. fetch에 대한 설명으로 옳지 않은 것은?

1. fetch()는 첫번째 인자로 URL, 두번째 인자로 http 요청 방식, 헤더, 바디 등을 담은 option 객체를 받으며, option 생략시 POST 방식으로 진행된다.
2. 실행 결과를 Promise 타입의 객체로 반환하며, 호츌에 실패한 경우 예외 객체를 reject한다.
3. 응답받은 객체는 text(), json(), blob() 등의 메서드를 제공하여 원하는 타입으로 변환할 수 있다.
4. POST 방식으로 진행한 경우 성공시 응답 코드로 201을 반환한다.

<br>

<details>
<summary>10번</summary>
<b>1번</b>. fetch()는 첫번째 인자로 URL, 두번째 인자로 http 요청 방식, 헤더, 바디 등을 담은 option 객체를 받으며, option 생략시 POST 방식으로 진행된다.<br>
option 생략시 GET 방식으로 진행된다.

</details>

<br>
