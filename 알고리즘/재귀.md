# 입/출력 처리
## BufferedReader vs. Scanner
- Scanner : 간결하고 편리하지만 시간 소요 문제
- BufferedReader : 키보드 입력 시 buffer에 담고 버퍼가 차면 내용 전송
    <img src="https://blog.kakaocdn.net/dn/bYIB07/btqw78Z308y/KsqnoZaTZlLkuQ0TeGhXe1/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbYIB07%2Fbtqw78Z308y%2FKsqnoZaTZlLkuQ0TeGhXe1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="860" data-origin-height="427">
- 프로그램별 입출력 속도 비교
<img src="https://blog.kakaocdn.net/dn/cQ5Gea/btqw7vnT1W1/Kz6nIUKoQjKK8iKKws7yjK/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcQ5Gea%2Fbtqw7vnT1W1%2FKz6nIUKoQjKK8iKKws7yjK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="604" data-origin-height="434">
## StringBuilder vs. String 
- String Builder
    - String은 + 연산도 사실 새롭게 생성해서 더해줌
    - 메모리 낭비 방지 차원에서 append() 메서드 지원

# **재귀**
- 전제조건 : 전체문제를 작은 부분문제로 해결가능할 때
- 함수의 역할 명확히 정의!(What)
- 함수의 결정요인을 매개변수로 정의
- 기저조건 확인
    - **재귀함수는 특정 입력에 대해 자신을 호출하지 않고 종료해야 함!(무한반복)**
- 한 함수가 자기 자신을 여러번 호출 
    - 자신이 처리할 내용과 다음 재귀로 넘길 내용 잘 구분
    <img src="https://blog.kakaocdn.net/dn/Q9RtI/btrlyjyvFoC/QORd2OKQGPu6kBKmcaqaA0/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FQ9RtI%2FbtrlyjyvFoC%2FQORd2OKQGPu6kBKmcaqaA0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1814" data-origin-height="993">
- **모든 재귀함수는 재귀구조 없이 조건문으로 구현 가능**
- 재귀는 사용자 편의(가독성), 간결한 코드 구조를 위해 사용
- 모든 경우의 수 다 시도 > 시간, 메모리 소요
- 작은 문제의 답을 저장하여 중복호출을 제거 => Dynamic Programming(DP)
- 즉, 재귀 : 하향식, DP : 상향식
- DP 조건
    - 중복 호출 중 겹치는 부분 문제
        - 동일한 작은 문제들이 반복해서 나타나야 함
    - 최적 부분 구조
        - 부분문제에서 구한 최적 결과가 전체문제에도 동일하게 적용되어 결과가 변화되지 않아야 함


## DFS(Depth Fisrt Search)
완전탐색(브루트 포스) >= 깊이우선탐색(DFS) > 백트래킹(가지치기)

