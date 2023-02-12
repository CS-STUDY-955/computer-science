# DB 과목평가 대비
## SELECT 기본 문법
### 사용 예시
```mysql
select department_id, first_name
from employees
where (department_id, salary) in (
    select department_id, max(salary)
    from employees
    group by department_id
)
order by department_id, first_name;
```

### like
- %: 0이상의 문자열
- _: 1개의 문자
```mysql
select employee_id, first_name
from employees
where first_name like '%x%';
```

### null
- null인지 확인하기 위해서는 is null을 사용해야 함
```mysql
select employee_id, first_name, salary
from employees
# where department_id = null      검색 안됨
where department_id is null;
```
- 논리연산에서 null은 알 수 없는 값임
- not null -> null (단, is not null은 null이 아님을 의미)
- true and null -> null, false and null -> false
- true or null -> true, false or null -> null
```mysql
# select department_id, count(department_id)    department_id가 null인 경우 count되지 않아 0으로 출력됨
# select department_id, count(not department_id)     department_id가 null이어도 not null은 null과 같으므로 윗줄과 똑같이 출력됨
select department_id, count(true or department_id)
from employees
group by department_id;
```

### all
- select 절에 등장시 distinct와 반대되는 역할을 함(default가 all)
- where 절에 등장시 주로 비교연산자와 함께 모든 값을 만족해야하는 조건으로 사용됨
- `WHERE (DEPTNO, JOB) IN ((20, 'MANAGER'), (30, 'CLERK'))`과 같이 다중 컬럼으로도 사용할 수 있음

### case when then else end
- select 절에 사용됨
- when절 사이에 , 안오도록 조심
- case로 시작하여 end로 마무리하며 뒤에 alias를 붙일 수 있음
```mysql
select employee_id, first_name, salary,
    case 
        when salary>15000 then '고액연봉'
        when salary>8000 then '평균연봉'
        else '저액연봉'
    end '연봉 등급'
from employees;
```

### select문 수행 순서
1. from
2. where
3. group by
4. having
5. select
6. order by

## 내장함수
### 숫자 내장함수
- abs(x): 절댓값
- ceil(x), ceiling(x): 올림
- floor(x): 내림
- round(x, n): 소수점 아래 n자리까지 표현하도록 반올림
- truncate(x, n): 소수점 아래 n자리까지 표현하도록 내림
- pow(x, n), power(x, n): x의 n승
- mod(x, n): x를 n으로 나눈 나머지
- greatest(a, b, c, ...): a, b, c, ...중 가장 큰 수
- least(a, b, c, ...): a, b, c, ...중 가장 작은 수
#### 주의
- 자리수를 지정해서 올리는 함수는 없음
- floor(-12.2)는 -13이지만, truncate(-12.2, 0)은 -12임

### 문자열 내장함수
- ascii(c): c의 아스키코드 값
- concat(a, b, c, ...): a, b, c를 합친 문자열
- insert(s, idx, n, s2): s의 idx 위치부터 n 위치까지를 s2로 대체
- replace(s, s1, s2): s에 존재하는 모든 s1을 s2로 변경
- instr(s, s1): s에 존재하는 s1의 인덱스
- mid(s, idx, n), substr(s, idx, n), substring(s, idx, n): s에서 idx부터 n만큼 리턴
- ltrim(s): 왼쪽 공백 제거
- rtrim(s): 오른쪽 공백 제거
- trim(s): 양쪽 공백 제거
- lcase(s), lower(s): 소문자로 변경
- ucase(s), upper(s): 대문자로 변경
- left(s, n): s의 왼쪽부터 n개 추출
- right(s, n): s의 오른쪽부터 n개 추출
- reverse(s): 문자열 뒤집기
- length(s): 문자열 길이
#### 주의
- mysql의 인덱스는 1부터 셈
- 매개변수 개수만 맞다면 유효하지 않은 접근도 에러를 뱉지않고 무시함

### 날짜 관련 함수
- now(), current_timestamp(): select 실행되는 순간의 시간
- sysdate(): 함수가 호출될 때의 시간
- curdate(), current_date(): 현재 날짜
- curtime(), current_time(): 현재 시간
- date_add(date, interval), adddate(date, interval): date를 interval만큼 더함
- date_sub(date, interval), subdate(date, interval): date를 interval만큼 뺌
- year(date): 연도
- month(date): 월
- monthname(date): 문자열 월
- dayname(date): 문자열 요일
- dayofmonth(date): 일
- dayofweek(date): 숫자 요일(1:일, 2:월, ...)
- weekday(date): 숫자 요일(0: 월, 1: 화, ...)
- dayofyear(date): 일년 기준 일 수
- week(date): 일년 기준 주 수
- from_days(day): 00년 00월 00일부터 day만큼 경과한 날짜
- to_days(date): 00년 00월 00일부터 date까지의 일 수
- date_format(date, format): date를 format에 맞게 리턴
  - 기본: `%Y-%m-%d %H:%i:%s`
#### 주의
- 모든 date는 "yyyy-mm-dd"이거나 "yyyy-mm-dd hh:mm:ss"임

### if vs ifnull vs nullif
- if(logic, a, b): logic이 참이면 a, 거짓이면 b 반환
- ifnull(a, b): a가 null이면 b 반환, null이 아니면 a 반환
- nullif(a, b): a와 b가 같으면 null 반환, 다르면 a 반환

## DDL
### create

## DML
### insert
- `insert` `into` table(field1, field2, field3, ...) `values`(value1, value2, value3, ...);
- nullable, default, auto increment가 설정된 컬럼은 생략하여 입력 가능

### update
- `update` table `set` field1=value1, field2=value2, ... `where` condition;
- where절이 없을 경우 모든 데이터에 대해 연산이 수행됨

### delete
- `delete` `from` table `where` field1=value1;
- where절이 없을 경우 모든 데이터에 대해 연산이 수행됨

## transaction
- set autocommit = 0으로 자동으로 커밋하게 하는 기능을 해제할 수 있음
- commit: 변경사항 확정
- rollback: 변경사항 취소
- savepoint: 임시저장. rollback으로 돌아갈 수 있음

## JDBC
### ResultSet