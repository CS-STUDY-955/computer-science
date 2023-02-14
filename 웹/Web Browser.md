# Web Browser
## 브라우저란?
- 사용자가 선택한 자원(html, pdf, image 등)을 URI를 통해 서버에 요청하여 받은 뒤 화면에 표시하는 프로그램
- 웹 표준화 기구인 W3C의 html과 css에 대한 명세에 따라 html 파일을 해석해서 표시
- 최근 여러 브라우저는 서로를 모방하여 사용자에게 필요한 기능을 갖춤으로써 UI가 어느정도 비슷해짐
- Chrome, Safari, Firefox, MS Edge, Naver whale 등

## 웹 브라우저
<img src="https://user-images.githubusercontent.com/50614241/218496466-6a018758-d2b7-4be4-81a6-9a85ef7177fc.png" width="50%" height="20%" />


- `사용자 인터페이스`: 주소 표시줄, 이전/다음 버튼, 북마크 등 사용자가 활용하는 인터페이스
- `브라우저 엔진`: 사용자 인터페이스와 렌더링 엔진 사이의 동작 제어
- `렌더링 엔진`: 요청한 콘텐츠 파싱 및 표시
- `통신`: HTTP 요청과 같은 네트워크 호출
- `자바스크립트 인터프리터`: JS코드 해석 및 실행
- `UI 백엔드`: select / input 등 기본적인 위젯을 그리는 인터페이스
- `자료 저장소`: 쿠키, 로컬 저장소 등 자원을 하드 디스크에 저장

## 렌더링
- 웹 표준화 기구인 W3C의 명세에 따라 html 파일을 해석해서 표시하는 브라우저의 핵심 기능
- 기본적으로 html, xml, 이미지를 표시할 수 있고, 확장하여 pdf 등 다른 유형도 표시 가능
- 렌더링 엔진은 여러가지가 존재하는데 대표적으로 Webkit 엔진과 Gecko 엔진이 있다.
  - Webkit: 크롬, 사파리가 사용 (우세)
  - Gecko: 파이어폭스가 사용
- DOM: 여러 태그를 JS가 활용할 수 있는 객체로 만든 모델. 웹 브라우저가 HTML 페이지를 인식하는 방식.
- DOM Tree: 웹 상에 나타날 내용을 구성
- Render Tree: 웹에 표시될 요소와 스타일, 위치 등 구성

<img src="https://user-images.githubusercontent.com/50614241/218496473-d82823b1-6e37-4c04-b9a6-332346d8990a.png" width="70%" height="20%" />


<img src="https://user-images.githubusercontent.com/50614241/218496480-17a2f7e1-493c-43f1-9834-2a2768929b34.png" width="70%" height="20%" />


<img src="https://user-images.githubusercontent.com/50614241/218496482-5f034a97-5ea4-4de4-b0f1-734dc85d44b6.png" width="100%" height="20%" />


<img src="https://user-images.githubusercontent.com/50614241/218496486-2885cef3-7085-4ef5-b414-d49163a0329a.png" width="70%" height="20%" />
