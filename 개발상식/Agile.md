# Agile

## 애자일 개발 방법론
- 모든 것을 계획하고 개발하는 전통적인 방법론을 대체하기 위해 등장한 이론
- 사업적 가치가 있는 프로젝트는 새로운 시도와 학습을 기반으로 구현되고, 이를 추구하다보면 개발에 불확실성이 높아진다.
- 협력을 통한 빠른 주기의 피드백을 지속적으로 반복하면서 개발하는 여러 방법론을 지칭하는 용어
- TDD, Pair Programming, Scrum 등이 존재

<img src="https://user-images.githubusercontent.com/50614241/217242328-b75066c8-54b8-41c3-a6a2-04d5243939ef.png" width="50%" height="20%" />

## TDD
- 테스트 주도 개발 (Test Driven Development)
- 테스트케이스를 먼저 작성한 이후 이를 통과하기 위한 코드를 개발
- 테스트케이스를 기반으로 코드를 개발하고 이를 리팩토링하는 작업을 반복

| 장점                                | 단점                              |
|-----------------------------------|---------------------------------|
| 개발 도중 사용자 요구사항이 변해도 유연하게 대처할 수 있음 | 테스트 코드와 개발 코드의 잦은 수정으로 생산성이 저하됨 |
| 객체 지향적인 개발을 강제함으로써 코드의 재사용성이 확보됨  | 소프트웨어 납기일이 미뤄질 수 가능성이 높음        |

- Spring에서의 TDD 적용
  - Repository -> Service -> Controller 순서로 개발 진행
  - Repository 계층의 테스트는 H2와 같은 인메모리 데이터베이스 기반의 통합 테스트로 진행
  - Service 계층의 테스트는 Mockito를 사용해 Repository 계층을 Mock하여 진행
  - Controller 계층의 테스트는 SpringTest의 MockMvc를 사용해 진행

<img src="https://user-images.githubusercontent.com/50614241/217242334-74af35f6-631d-43c5-bed5-6e504461d7a1.png" width="50%" height="20%" />

## Pair Programming
- 두 사람이 한 짝이되어 한 컴퓨터로 프로그래밍을 진행하는 애자일 방법
- 한 사람은 오더하고, 한 사람은 코딩하는 작업을 약 10분단위로 역할을 바꿔가며 반복한다.
- 코딩할 때는 문제를 구체적으로 보게되고, 오더할 때는 문제를 전체적으로 보게 되어 통찰이 생긴다.

| 장점                      | 단점                            |
|-------------------------|-------------------------------|
| 둘이서 진행하기 때문에 실수가 감소함    | 2명이서 1인분을 하고 있는 것이므로 생산성이 저하됨 |
| 서로의 약점을 보완하는 프로그래밍이 가능함 | 수평적인 관계가 아니라면 효과가 미미할 수 있음    |

<img src="https://user-images.githubusercontent.com/50614241/217242312-772545e2-978f-4ec3-96be-da8a9a5778ae.jpg" width="50%" height="20%" />

## Scrum
- 스프린트라고 불리는 작업 단위를 사용하여 작업을 추정하는 프로젝트 계획 방법
- 스프린트는 약 1~2시간 단위로 가능한 작은 단위의 개발 사항으로 이루어짐
- 스프린트 기간은 프로그램이나 개발사의 특성에 따라 보통 1~4주 정도 선정
- 스크럼 진행 과정
  1. 제품 백로그(product backlog) 작성
  2. 스프린트 계획 회의
  3. 스프린트 백로그(sprint backlog) 작성 -> 스크럼 보드로 정리
  4. 일일스크럼 미팅(daily scrum meeting)
  5. 실행 가능한 제품 개발
  6. 스프린트 리뷰
  7. 스프린트 회고(sprint retrospective)
  8. 다음 스프린트 시작

<img src="https://user-images.githubusercontent.com/50614241/217242325-a512cd59-4051-417b-a2b6-c8c777e94d47.png" width="100%" height="20%" />