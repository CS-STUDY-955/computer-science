# SQL Select

## 1. RDBMS & SQL
+ Relational Database Management System
+ Structured Query Language
+ 테이블 기반의 DBMS
    + 데이터를 테이블 단위로 관리
    + 중복 데이터를 최소화 시킴 (정규화)
    + 여러 테이블에 분산되어 있는 데이터 검색시 JOIN 활용
+ DDL, DML, DCL, TCL 로 구분

<br>

***
## 2. DDL
+ 데이터 정의어 (Data Definition Language)
+ 테이블로부터 데이터 구조를 생성, 변경 제거
+ 대상 객체: table, view, index
+ CREATE, DROP, ALTER, TRUNCATE
```SQL
-- CREATE
create database db;
create table tbl ( col1 type1 conditions, ...);
create or replace procedure ( ... );
-- DROP
drop database db;
drop table tbl;
-- ALTER : column 변경, 제약 조건 변경 등
alter table city drop column population;
alter table city add area int null;
alter table city alter column area double null; 
-- TRUNCATE
truncate table tbl;
    -- DB는 삭제 불가
```
```SQL
-- 테이블 구조 확인
desc table_name;
```

> DROP vs TRUNCATE
1. DROP : 테이블 혹은 데이터베이스 자체를 삭제
2. TRUNCATE : 테이블의 데이터를 삭제 (테이블은 남아있음)

<br>

***
## 3. DML
+ 데이터 조작어 (Data Manipulation Language)
+ 테이블의 레코드를 CRUD(Create, Read/Retrive, Update, Delete)
+ INSERT, SELECT, UPDATE, DELETE
```SQL
-- INSERT
INSERT INTO table_name (col1, col2, ...)
    VALUES (val1, val2, ...),
           (valA, valB, ...),
           ...;
```
```sql
-- SELECT 기본 구조
SELECT * | {[ALL | DINTINCT] col_name | expression [alias], ... }
FROM table_name
{WHERE conditions [LIKE expression]};
{ORDER BY col_name [(default)ASC | DESC][, col_name2 ...]}

-- case
select *, 
    case when population > 1000000 then '대도시'
        when population > 200000 then '중도시'
        else '소도시'
    end '도시구분'
from city
limit 10;
```
```sql
-- UPDATE
UPDATE table_name
SET col1 = val1, col2 = val2, ...
[WHERE condition] -- where 절 생략시 모든 레코드 변경
```
```SQL
-- DELETE
DELETE FROM table_name
[WHERE condition] -- where 절 생략시 모든 데이터 삭제
```
<br>

***
## 4. DCL
+ 데이터 제어어 (Data Control Language)
+ DB, Table의 접근 권한이나 CRUD 권한 정의
+ 특정 사용자 별로 권한을 부여하거나 금지
+ GRANT, REVOKE
```SQL
-- GRANT : 권한 부여
grant create user, alter user, drop user
to ssafy with admin option;
-- REVOKE : 권한 해제
revoke create user, alter user, drop user
from ssafy;
```
<br>

***
## 5. TCL
+ 트랜잭션 제어어 (Transaction Control Language)
+ Transaction: 데이터 베이스의 논리적 연산 단위
+ COMMIT, ROLLBACK

```SQL
-- COMMIT : DB에 영구 저장하는 명령어
commit; -- 수행시 하나의 트랜잭션 과정을 종료하는 것.

-- ROLLBACK : 변경사항 취소 명령어
rollback; -- 수행시 마지막 commit 시점으로 복구

-- SAVEPOINT : 임시저장
savepoint s1; -- 트랜잭션의 분할
-- rollback to s1;
