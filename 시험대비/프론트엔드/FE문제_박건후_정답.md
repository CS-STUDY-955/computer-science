# 1. HTML `<a>` tag 사용 시 새로운 창으로 웹페이지를 여는 속성명은?
> _blank

# 2. HTML input type이 아닌 것은?
1. date
2. hidden
3. button
4. file
5. id
> 5

# 3. CSS 중 상속되지 않는 속성이 아닌 것은?
1. position 관련
2. Box model 관련
3. background
4. text 관련
> 4

# 4. CSS BOX-MODEL 중 padding과 margin 의 차이점을 border기준으로 설명하시오.
> 패딩 : border와 contents 사이의 여백  
> margin : border 외부의 여백

# 5. CSS 선택자 우선순위가 높은 순서대로 나열하시오
1. 전체 선택자
2. 클래스 선택자
3. ID 선택자
4. 타입선택자
> 3 2 4 1

# 6. CSS position 속성 중 해당 요소가 보이지 않게 하지만, 공간을 차지 하게 만드는 태그는?
> visibility:hidden  
> display:none과 헷갈림 주의!

# 7. JavaScript Event Handler 중 특정 요소를 클릭했을 때 핸들링하는 방식이다.(빈칸)
```html
<input type="button" id="myBtn">
<script>
    var btn = document.querySelector("#myBtn");
    btn.______ = function(){};
</script>
```
> onclick

# 8. id가 중복선언된 경우 다음코드를 실행한 결과로 올바른 것은?
```javascript
document.querySelector('#id');
```
1. 오류 발생하고 실행되지 않음
2. 오류 발생하고, 1번째 노드만 반환
3. 오류가 발생하지 않고, 1번째 노드만 반환
4. 오류가 발생하지 않고, 모든 노드 list를 반환
> 3

# 9. 다음 코드의 실행 결과를 작성하시오.
```javascript
console.log(num);
var num = 123;
console.log(num)
{
    var num = 456;
}
console.log(num);
```
> undefined  
123  
456

# 10. localStorage를 사용하기 위해 빈칸을 완성하시오
```javascript
let user = {
    userid:"ssafy",
    username: "김싸피",
}
// localStorage에 저장
localStorage.setItem("userInfo", ____________(user));
// localStorage에서 객체로 변환
let userInfo1 = __________(userInfo);
```
> JSON.stringify  
JSON.parse

# 11. localStorage와 sessionStorage의 차이점
> localStorage는 저장한 데이터를 지우지 않는 이상 영구적으로 보관이 가능. 즉, 세션이 끊겨도 사용 가능  
> sessionStorage는 브라우저가 종료되면 데이터도 같이 삭제됨. 즉, 같은 세션만 사용 가능  
> local은 도메인만 같으면 전역적으로 공유 가능  
> session은 같은 사이트의 같은 도메인이라도 브라우저가 다르면 서로 다른 영역으로 인식

# 12. GET방식과 POST방식의 차이점에 대해 서술하시오
> GET방식
- URL에 변수(데이터)를 포함시켜 요청
- 데이터를 Header에 포함하여 전송
- url에 데이터가 노출되어 보안 취약
- 전송 길이 제한
- 캐싱 가능
> POST방식
- URL에 데이터를 노출하지 않고 요청
- 데이터를 body에 포함
- url에 데이터 노출되지 않아 기본 보안
- 전송 길이 제한 없음
- 캐싱 불가

# 13. 다음 Javascript의 실행결과를 작성하시오.
```html
<div id='content'></div>
```
```javascript
function ssafy()  {
  const element = document.getElementById('content');
  element.innerText = "<div style='text-align:center'>A</div>";
}
```
> `<div style='text-align:center'>A</div>` 가 출력된다.