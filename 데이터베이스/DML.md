# DDL, DML, DCL, TCL
<img src="https://blog.kakaocdn.net/dn/6UmKz/btqDcyrwCkf/ByishJj3nnfGK4jY0SxHB0/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F6UmKz%2FbtqDcyrwCkf%2FByishJj3nnfGK4jY0SxHB0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1562" data-origin-height="704">

## DDL(Data Definition Language)
- 데이터 구조 정의에 사용되는 명렁어
- CREATE, ALTER, DROP, RENAME, TRUNCATE

## DML(Data Manipulation Language)
- 데이터를 조회, 삽입, 수정, 삭제 하기 위한 명령어
- SELECT, INSERT, UPDATE, DELETE
```sql
SELECT * FROM tableName;

INSERT INTO tableName[(col_name1, col_name2, col_name3,...)]
VALUES(val1, val2, val3, ...)[, ...];

UPDATE tableName
SET col1 = val1, ...
WHERE 조건식;

DELETE [FROM] tableName
WHERE 조건식;
```
## DCL(Data Control Language)
- 데이터베이스에 접근하고 객체들을 사용할 권한 부여/회수 명령어
- GRANT, REVOKE

## TCL(Transaction Control Language)
- Transaction : 최소 업무(작업) 단위
- 논리적 작업의 단위를 트랜잭션 별로 제어하는 명령어
- COMMIT, ROLLBACK, SAVEPOINT
```sql
savepoint 복구지점명;
rollback to 복구지점명; -- 복구 지점까지 일부 복구됨
```
---

## 숫자 관련 함수
| function name | desc |
| --- | --- |
| ABS(숫자) | 절대값 |
| CEILING(숫자) | 올림 |
| FLOOR(숫자) | 내림 |
| ROUND(숫자, 자리수) | 반올림 |
| TRUNCATE(숫자, 자리수) | 버림 |
| POW(X, Y) | 제곱승 |
| MOD(X, Y) | 나머지 |
| GREATEST(a,b,c) | 최대값 |
| LEAST(a,b,c) | 최소값 |

## 문자 관련 함수
| function name | desc |
| --- | --- |
| ASCII(문자) | 아스키값|
| CONCAT | 문자열 붙임 |
| INSERT | 문자열 삽입 |
| REPLACE | 문자열 교체 |
| INSTR('문자열', '찾는문자열') | 위치값 리턴 |
| MID('문자열', 시작위치, 개수) | 문자열 중 시작위치부터 개수만큼 리턴|
| SUBSTRING('문자열', 시작위치, 개수) | |
| LTRIM('문자열') | 문자열 중 왼쪽 공백 제거 |
| RTRIM('문자열') | |
| TRIM('문자열') | 양쪽모두의 공백 제거 |
| LCASE('문자열') or LOWER('문자열') | 소문자변경 |
| UCASE('문자열') or UPPER('문자열') | |
| LEFT('문자열', 개수) | 문자열 중 왼쪽에서 개수만큼 추출 |
| RIGHT ('문자열', 개수) |  |
| REVERSE('문자열') | 문자열을 반대로 나열
| LENGTH('문자열') | | 

## 날짜 관련 함수
```SQL
now(), sysdate() -- 2023-02-02-09:57    
curdate(), curtime() -- 2023-02-02, 09:58:12  
date_format(now(), '%y-%m-%d %h:%i:%s')
```

## **논리 관련 함수**
| function name | desc |
| --- | --- |
| IF(논리식, 값1, 값2) | 참:값1, 거짓값2 |
| **IFNULL(값1, 값2)** | 값1:NULL이면 값2로 대치 / 아니면 값1 |
| NULLIF(값1, 값2) | 값1=값2 ? null : 값1 |
```sql
select if(1>2, 'true', 'false');
> false

select ifnull(null, '널 출력');
> 널 출력

select ifnull(1, '널 출력');
> 1

select isnull(null);
> 1

select isnull(1);
> 0

select nullif(1, 1);
> NULL

select nullif(1, 2);
> 1
```
<br>

---

# Aggregation Function
## 집계 함수
- count, sum, avg, max, min  
- count: null을 제외한 개수

<br>

---

# GROUP BY clause
- 형식 :  **실행순서** 
    | 구문 | 조건       | 실행순서 |  
    | --- | --- | --- |
     select|colums|5|
     from|table name|1|
     where|conditions|2|
     group by|column|3|
     having|conditions|4|
     order by|col[desc]|6|

- join()기능 </span>**
- **다중컬럼 subquery 이용**

## HAVING clause
- group by 한 결과에 조건을 추가할 경우 having절을 사용
- query 실행은 where가 group by 보다 먼저 실행되기 때문에 aggregation 조건은 having 절 사용
```sql
select user_name, count(*)
from employees
group by department_id
having hire_date = '2017-01-01 00:00:00';
```
<br>

---

## Inline View
- FROM 절에서 사용되는 서브쿼리
- 인라인뷰는 SQL문이 실행될 때에만 일시적으로 생성되는 동적 VIEW
```SQL
SELECT *
FROM (
    SELECT *
    FROM employees
    WHERE department_id = 100
) a, employees e
WHERE a.id = e.id;
```

## 번외
### SQL vs. NoSQL
1. SQL
    - 정해진 데이터 스키마에 따라 테이블에 저장
    - 관계를 통해 여러 테이블에 분산
    - 즉, 스키마를 준수하지 않은 레코드는 테이블에 추가 불가
    - 데이터 중복을 피하기 위해 '관계'를 이용
2. NoSQL
    - 스키마 x, 관계 x
    - 여러 테이블을 나누지 않고 하나에 저장
    - 여러 테이블 조인할 필요없이 완전한 문서를 작성하는 것
    - 즉, Join()을 사용하지 않고, 자주 변경되지 않는 데이터일 때 효율적

| 구분 | 장점 | 단점 | 활용 |
| --- | --- |--- | --- |
| SQL | 명확하게 정의된 스키마<br> 무결성보상 <br> 관계는 각 데이터를 중복없이 한번만 저장 | 데이터 스키마 사전 정의 <br> 수정 불편(관계 때문에 유연하지 않음) | *관계*를 맺는 데이터가 자주 변경될 때 |
| NoSQL | 스키마가 없어서 유연함, 새로운 데이터/필드 추가 용이<br> 처리속도 빠름, 많은 양 데이터 처리 가능 <br> 수직 및 수평 확장 가능 | 데이터 중복이 가능하기 때문에 수정 시 모든 컬렉션에서 수행해야 함 | 정확한 데이터 구조를 알지 못하거나, 변경/확장 가능성이 존재할 때 <br> 변경이 자주 일어나지 않고, 조회만 많이 할 때 <br> 실시간 처리가 요구되는 컨텐츠를 사용할 때 |