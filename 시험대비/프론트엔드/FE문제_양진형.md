# Front End

### <b>1</b>. 다음 중 inline 태그가 아닌것은?

1. a
2. em
3. form
4. img

<br>

### <b>2</b>. 다음은 html과 css 파일의 내용이다. h1 태그와 h2 태그의 내용에 적용되는 색깔은?

```html
<!-- test.html -->
<!DOCTYPE html>
<html>
<head>
  <style type=""text/css">
  @import url(h2-style.css);
  </style>
  <style type="text/css">
  h1 { color: green; }
  h2 { color: yellow; }
  </style>
  <link rel="stylesheet" href="h1-style.css">
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

### <b>3</b>. select 태그를 이용하여 다음과 같은 select box를 만드려고 할 때 빈칸에 들어갈 태그로 옳은 것은?

![q3-select-box](q3-img.JPG)

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

### <b>4</b>. CSS의 position 속성의 값과 설명이 올바르게 연결된 것은?

1. absolute - position 속성의 기본값이다.
2. fixed - 자신의 상위 box속에서 top, left, right, bottom등의 속성으로 절대적인 위치를 지정한다.
3. static - top, left, right, bottom등의 속성을 지정할 수 없다.
4. relative - 일반적인 내용의 흐름으로 top, left 속성으로 거리를 지정할 수 있지만 right, bottom 속성으로 지정할 수 없다.

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

### <b>7</b>. localStorage에 대한 설명으로 옳지 않은 것은?

1. 자바스크립트와 http 헤더를 통해 데이터를 조작할 수 있다.
2. 데이터 저장에 용량 제한이 없지만 문자열 데이터만 저장 가능하다.
3. 유효기간이 없고 영구적으로 이용 가능하다.
4. 프로토콜, 도메인, 포트가 다르면 접근이 불가하며 모바일에서도 이용할 수 있다.

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

### <b>9</b>. 다음 중 GET 방식과 POST 방식에 대한 설명으로 옳지 않은 것은?

1. GET 방식은 데이터를 http 패킷의 헤더 영역에 포함시켜 전송하고, POST 방식은 바디 영역에 포함시켜 전송한다.
2. GET 방식은 데이터 전송 길이에 제한이 있고 POST 방식은 제한이 없다.
3. GET 방식과 POST 방식 모두 캐싱을 이용해 요청을 빠르게 처리한다.
4. GET 방식과 POST 방식 모두 비동기 방식으로 결과를 조회한다.

<br>

### <b>10</b>. fetch에 대한 설명으로 옳지 않은 것은?

1. fetch()는 첫번째 인자로 URL, 두번째 인자로 http 요청 방식, 헤더, 바디 등을 담은 option 객체를 받으며, option 생략시 POST 방식으로 진행된다.
2. 실행 결과를 Promise 타입의 객체로 반환하며, 호츌에 실패한 경우 예외 객체를 reject한다.
3. 응답받은 객체는 text(), json(), blob() 등의 메서드를 제공하여 원하는 타입으로 변환할 수 있다.
4. POST 방식으로 진행한 경우 성공시 응답 코드로 201을 반환한다.

<br>
