# 1. HTML `<a>` tag 사용 시 새로운 창으로 웹페이지를 여는 속성명은?
>  

# 2. HTML input type이 아닌 것은?
1. date
2. hidden
3. button
4. file
5. id
>  

# 3. CSS 중 상속되지 않는 속성이 아닌 것은?
1. position 관련
2. Box model 관련
3. background
4. text 관련
>  

# 4. CSS BOX-MODEL 중 padding과 margin 의 차이점을 border기준으로 설명하시오.
>  

# 5. CSS 선택자 우선순위가 높은 순서대로 나열하시오
1. 전체 선택자
2. 클래스 선택자
3. ID 선택자
4. 타입선택자
> 

# 6. CSS position 속성 중 해당 요소가 보이지 않게 하지만, 공간을 차지 하게 만드는 태그는?
>  

# 7. JavaScript Event Handler 중 특정 요소를 클릭했을 때 핸들링하는 방식이다.(빈칸)
```html
<input type="button" id="myBtn">
<script>
    var btn = document.querySelector("#myBtn");
    btn.______ = function(){};
</script>
```
>  

# 8. id가 중복선언된 경우 다음코드를 실행한 결과로 올바른 것은?
```javascript
document.querySelector('#id');
```
1. 오류 발생하고 실행되지 않음
2. 오류 발생하고, 1번째 노드만 반환
3. 오류가 발생하지 않고, 1번째 노드만 반환
4. 오류가 발생하지 않고, 모든 노드 list를 반환
>  

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
>  

# 10. localStorage를 사용하기 위해 빈칸을 완성하시오
```javascript
let user = {
    userid:"ssafy",
    username: "김싸피",
}
// localStorage에 저장
localStorage.setItem("userInfo", ____________(user));  // 1
// localStorage에서 객체로 변환
let userInfo1 = __________(userInfo); // 2
```
> 1  
> 2  

# 11. localStorage와 sessionStorage의 차이점
> localStorage는 저장한 데이터를 지우지 않는 이상 영구적으로 보관이 가능. 즉, 세션이 끊겨도 사용 가능  
>  
>  
>  

# 12. GET방식과 POST방식의 차이점에 대해 서술하시오
>   
>  

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
>   