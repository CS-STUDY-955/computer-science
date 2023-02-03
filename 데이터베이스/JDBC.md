# JDBC

## JDBC란?
 - Java DataBase Connectivity
 - 데이터베이스에 종속적이지 않은 자바 표준 API

<img src="https://user-images.githubusercontent.com/50614241/216394697-6f4a9637-b1a3-4295-8f6f-14a5c6b1ea2d.png" width="100%" height="40%" />

## JDBC를 사용하는 이유
 - 여러 DB를 사용하기 위해서는 개발자가 각각의 사용법을 익혀야함
 - 각 DB의 제공사에게 JDBC의 인터페이스를 구현한 드라이버를 요구함으로써 개발이 용이해짐
 - JDBC 사용법만 익히면 여러 DB를 다룰 수 있음

<img src="https://user-images.githubusercontent.com/50614241/216394685-51c60a70-084c-4c74-be9d-4eeb51bef720.png" width="100%" height="40%" />

## PreparedStatement VS Statement

#### MySQL 쿼리 처리 절차
 1. 구문 오류 체크
 2. 공유 영역에서 해당 구문 검색
 3. 권한 체크
 4. 실행 계획 수립
 5. 실행 계획 공유 영역에 저장
 6. 쿼리 실행

#### 두 Statement의 차이점
|    | **PreparedStatement** | **Statement** |
|----|--------|---------|
| 공통점 | SQL문을 실행할 수 있는 객체 ||
| 차이점 | 캐싱 사용 | 캐싱 미사용 |

 - 캐싱 미사용시 1번 ~ 6번 실행 (Hard Parsing)
 - 캐싱을 사용시 2번에서 동일 구문을 찾게되고, 6번으로 건너뜀 (Soft Parsing)
 - 이로 인해 자주 사용되는 구문을 캐싱했을 때 성능이 향상됨
 - 캐싱 용량에 한계가 있기 때문에 모든 구문을 PreparedStatement로 만들 수는 없음
 - 따라서 대부분의 경우 치환 변수(?)를 사용해 SQL구문을 일반화하여 사용함

## ORM이란?
 - JDBC 덕분에 DB 변경시 DB연결을 다루는 문법을 수정하지 않아도 됨
 - But, SQL은 여전히 DB마다 전부 다르므로 여전히 변경해야함
 - DB에서 가져온 데이터를 프로그램에서 사용할 수 있도록 **객체와 매핑**해주는 기술
 - ResultSet같은 고정된 타입으로 받아와 개발자가 일일히 파싱할 필요가 없어짐
 - 선언문, 할당, 종료같은 부수적인 코드를 작성할 필요가 없어짐
 - SQLMapper라는 비슷한 역할을 하는 기술이 있고, myBatis가 대표적

// oracle과 mysql의 sql 비교하는 사진

## JPA란?
 - Java에서 ORM을 구현하기 위해 등장한 API
 - Java Persistence API
 - hibernate, spring-data-jpa가 대표적인 JPA 구현체

// 잘 설명가능한 프로젝트 domain 사진 and JPA repository 사진

<img src="https://user-images.githubusercontent.com/50614241/216394692-123091be-8d9f-4ea3-9eca-fd067932033f.png" width="100%" height="60%" />
