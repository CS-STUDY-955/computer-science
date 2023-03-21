## 1. 아래의 테이블을 작성하시요<br>
![문제 1](https://user-images.githubusercontent.com/63623597/226173894-3c2f192c-6d14-43b6-8950-4ec899a46ed9.PNG)

```html
<table>
  <thead>
    <th>헤드1</th><th>헤드2</th><th>헤드3</th><th>헤드4</th>
  </thead>  
  <tbody>  
    <tr>
      <th>바디헤드1</th>
      <td colspan="2">내용1</td>
      <td rowspan="2">내용2</td>
    </tr> 
    <tr>
      <th>바디헤드2</th>
      <td>내용3</td>
      <td>내용4</td>
    </tr>
  </tbody>
</table>
```

## 2. 다음중 inline 속성이 아닌 html 태그는?
   1. span
   2. a
   3. button
   4. table
   5. img

정답: table은 block 태그다

## 3. 다음중 원시타입의 종류와 typeof가 올바르게 짝지어지지 않은 것은?
   1. 숫자형: number
   2. null: NaN
   3. undefined: undefined
   4. 문자열형: string
   5. boolean: boolean

정답: null의 typeof 값은 object다

## 4. let, var, const의 차이에 대해 설명하시오

var는 변수의 선언을 나타내는 키워드로, 어느 종류의 변수에도 사용할 수 있으며, 함수내에 존재하면 그 함수 안에서만, 밖에 있다면 전역변수로 사용할 수 있다.<br>
let은 변수의 선언을 나타내지만, 해당 블록에서만 사용할 수 있다.<br>
const는 상수의 선언에 사용하며, 값을 바꾸려고 하면 error가 발생한다.<br>

## 5. 다음중 JS 객체의 속성값 조회 방법으로 올바르지 않은 것은?
   1. member.age
   2. member.user-name
   3. member["age"]
   4. member.address (단, member에 address 속성은 없다)
   5. member.age || 'none'

정답: 2번. 중간에 연산자가 들어갈 경우, [""]방식으로만 조회할 수 있다. 객체에 없는 속성은 undefined를 반환하니 에러는 나지 않는다. 5번의 경우, age의 값이 false 또는 false가 될 수 있는 값이라면 'none'이 반환된다

## 6. 다음중 JS에서 false가 아닌 것은?
   1. 0
   2. "0"
   3. []
   4. null
   5. NaN

답은 "0". 빈스트링인 ""일때 false가 나온다.

## 7. 다음 JS 코드의 출력값은?
```javascript
console.log(0 == "0");
console.log(0 == []);
console.log("0" == []);
```

출처 참조: https://brunch.co.kr/@swimjiy/37
