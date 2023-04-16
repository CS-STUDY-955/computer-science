# 1. 다음 index에서 PK 컬럼으로 설정되는 컬럼명은?
```sql
create table test(
	c1 int unique,
	c2 int unique,
	c3 int not null unique
);
```
> 3

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
> add constraints

# 3. Inner join 의 종류 4가지와 각각의 특징과 차이점에 대해 서술하시오.
> 1. table alias : 각 테이블의 alias name을 설정해주고, 컬럼명을 지정해주면 된다.
```sql
     -- talbe alias : alias 지정하면 반드시 alias-name.컬럼명 지정해야함, 테이블명.컬러명 사용시 오류
    SELECT d.deptno, d.dname, e.empno, e.ename, e.job, e.sal
    FROM emp e JOIN dept d
    WHERE e.deptno = d.deptno;
```
> 2. ON : where절을 사용하지 않고 join 의 제약조건을 on으로 설정하고, where는 추가 제약조건으로 설정할 수 있다.
```sql
    SELECT 	d.deptno, d.dname, e.empno, e.ename, e.job, e.sal
    FROM 	emp e INNER JOIN dept d
    ON 		e.deptno = d.deptno 
    WHERE 	e.deptno = 10;
```
> 3. ALTER : 컬럼명이 동일할 경우 USING 을 사용하여 join할 수 있다. 이때, 컬럼명으 ㄹ괄호로 묶어주어야 한다.
```sql
    SELECT 	deptno, d.dname, e.empno, e.ename, e.job, e.sal
    FROM 	emp e JOIN dept d
    USING 	(deptno);
```
> 4. Natural join : join column이 하나만 존재할 때 자동으로 join해준다.
```sql
    SELECT 	deptno, d.dname, e.empno, e.ename, e.job, e.sal
    FROM 	emp e NATURAL JOIN dept d;
```

# 4. employees table에서 이름이 s로 끝나는 쿼리의 일부분이다. 추가로 뒤에 작성해야 하는 쿼리문을 작성하시오. employees에 이름 컬럼은 name이다.
```sql
SELECT * FROM employees
WHERE deptno 
__________________ ;
```
> IN (SELECT deptno FROM employees WHERE name LIKE '%s')

# 5. outer join 중 ansi join의 일부분이다. 빈칸을 채우시오.
```sql
SELECT e.deptno, e.ename, e.sal
from emp e ____ (SELECT deptno, MAX(sal) max_sal FROM emp GROUP BY deptno) m
_____ (deptno) where e.sal = m.max_sal;
```
> join, using

# 6. 다음 index에서 PK 컬럼으로 설정되는 컬럼명은?
```sql
create table test(
	c1 int not null unique,
	c2 int not null unique,
	c3 int not null unique
);
```
> c1

# 7. 자동으로 생성되는 index가 아닌 것은?
1. Primary key
2. Foreign key
3. Not null
4. Unique

> 3

# 8. 다음 데이터 모델링 종류를 순서대로 나열하시오
1. 논리적 모델링
2. 물리적 모델링
3. 개념적 데이터 모델링

> 3 1 2(개논물)

# 9. Index 생성 전략 중 틀린것은?
1. 인덱스는 열 단위에서 생성
2. 조인에 자주 사용되는 열에는 인덱스를 생성하는 것이 좋음
3. where절에서 사용되는 열에 생성
4. 외래키를 설정한 열은 추가적으로 제약 조건 추가

> 4 자동으로 넘어감

# 10. View 에 대한 설명중 틀린것은?
1. 삽입, 삭제, 갱신 작업에 많은 제한 사항을 가짐
2. View는 자신만의 인덱스를 가질 수 없음
3. 쿼리를 재사용할 수 있음
4. 물리적으로 저장됨
5. view를 생성한 기존 테이블의 data를 업데이트하면 view의 내용도 업데이트 됨

> 4. 물리적으로 저장되지 않는다
