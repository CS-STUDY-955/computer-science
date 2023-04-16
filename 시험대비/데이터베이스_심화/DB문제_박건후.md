# 1. 다음 index에서 PK 컬럼으로 설정되는 컬럼명은?
```sql
create table test(
	c1 int unique,
	c2 int unique,
	c3 int not null unique
);
```
> 

# 2. 다음 테이블에서 제약을 추가하려고 할 때, 빈칸에 알맞은 단어를 작성하시오.
```sql
create table test(
	b1 int primary key,
    a1 int not null,
    b3 int unique not null
    );
-- 제약 추가 : a1 컬럼에 test1(a1) 참조키 (FK) 제약 추가 설정
alter table test2 ___ ________ fk_test1_a1 foreign key(a1) references test1(a1);
```
> 

# 3. Inner join 의 종류 4가지와 각각의 특징과 차이점에 대해 서술하시오.


# 4. employees table에서 이름이 s로 끝나는 쿼리의 일부분이다. 추가로 뒤에 작성해야 하는 쿼리문을 작성하시오. employees에 이름 컬럼은 name이다.
```sql
SELECT * FROM employees
WHERE deptno 
__________________ ;
```
> 

# 5. outer join 중 ansi join의 일부분이다. 빈칸을 채우시오.
```sql
SELECT e.deptno, e.ename, e.sal
from emp e ____ (SELECT deptno, MAX(sal) max_sal FROM emp GROUP BY deptno) m
_____ (deptno) where e.sal = m.max_sal;
```
> 

# 6. 다음 index에서 PK 컬럼으로 설정되는 컬럼명은?
```sql
create table test(
	c1 int not null unique,
	c2 int not null unique,
	c3 int not null unique
);
```
> 

# 7. 자동으로 생성되는 index가 아닌 것은?
1. Primary key
2. Foreign key
3. Not null
4. Unique

> 

# 8. 다음 데이터 모델링 종류를 순서대로 나열하시오
1. 논리적 모델링
2. 물리적 모델링
3. 개념적 데이터 모델링

> 

# 9. Index 생성 전략 중 틀린것은?
1. 인덱스는 열 단위에서 생성
2. 조인에 자주 사용되는 열에는 인덱스를 생성하는 것이 좋음
3. where절에서 사용되는 열에 생성
4. 외래키를 설정한 열은 추가적으로 제약 조건 추가

> 

# 10. View 에 대한 설명중 틀린것은?
1. 삽입, 삭제, 갱신 작업에 많은 제한 사항을 가짐
2. View는 자신만의 인덱스를 가질 수 없음
3. 쿼리를 재사용할 수 있음
4. 물리적으로 저장됨
5. view를 생성한 기존 테이블의 data를 업데이트하면 view의 내용도 업데이트 됨

> 
