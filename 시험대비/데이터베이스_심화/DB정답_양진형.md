### <b>1</b>. 다음 중 다른 결과를 출력하는 쿼리는?

1.

```sql
select d.department_id, e.employee_id, e.first_name from employees e
right join (select * from departments where location_id = 1700) d
on d.department_id = e.department_id;
```

2.

```sql
select d.department_id, e.employee_id, e.first_name from departments d
left join employees e on d.department_id = e.department_id
where d.location_id = 1700;
```

3.

```sql
select d.department_id, e.employee_id, e.first_name from employees e, departments d
where e.department_id = d.department_id
and d.location_id = 1700;
```

4.

```sql
select d.department_id, e.employee_id, e.first_name from employees e
right join departments d on e.department_id = d.department_id
where d.department_id in (select department_id from departments where location_id = 1700);
```

<details>
<summary>1번 정답</summary>
<b>3번</b>.<br>
3번의 경우 inner join으로 join되며, location_id가 1700인 부서 중 employees 테이블에서 참조하지 않는 부서는 출력하지 않는다.
</details>

<br>

### <b>2</b>. 다음 쿼리문에 포함되지 않은 개념은?

```sql
select d.department_id, e.employee_id, e.first_name
from (select distinct department_id from employees
	where salary < (select avg(salary) from employees)) d
join employees e
on e.department_id = d.department_id;
```

1. Nested Subquery
2. Inline View
3. Scalar Subquery
4. Aggregate Function

<details>
<summary>2번 정답</summary>
<b>3번</b>. Scalar Subquery<br>
스칼라 서브쿼리는 SELECT 절에 서브쿼리를 사용하는 것을 의미한다.
</details>

<br>

### <b>3</b>. 다음 중 조인에 대한 설명으로 옳지 않은 것은?

1. Inner Join은 Equi Join이라고도 하며 기준 테이블과 조인 테이블 모두에 데이터가 있는 경우만 조회된다.
2. Inner Join은 어느 테이블을 먼저 읽어도 결과가 달라지지 않아 MySQL 옵티마이저가 조인의 순서를 조절할 수 있다.
3. Natural Join은 다른 조인들과 다르게 SELECT절에서 테이블의 이름을 명시하지 않아도 된다.
4. Join은 2개 이상의 컬럼을 Key로 사용하여 조인할 수 있다.

<details>
<summary>3번 정답</summary>
<b>1번</b>. Inner Join은 Equi Join이라고도 하며 기준 테이블과 조인 테이블 모두에 데이터가 있는 경우만 조회된다.<br>
Inner Join과 Equi Join은 다른 개념이다.
</details>

<br>

### <b>4</b>. 서브쿼리의 종류를 3가지 적고 각각이 SQL 구문의 어느 절에 위치하는지 서술하라.

```

```

<details>
<summary>4번 정답</summary>
<b>중첩 서브 쿼리(Nested Subquery)</b>. WHERE 절<br>
<b>인라인 뷰(Inline View)</b>. FROM 절<br>
<b>스칼라 서브 쿼리(Scalar Subquery)</b>. SELECT 절<br>
</details>

<br>

### <b>5</b>. 다음 중 서브쿼리에 대한 설명으로 옳지 않은 것은?

1. 서브 쿼리는 반드시 소괄호로 감싸야 한다.
2. 서브 쿼리는 HAVING 절에 올 수 있다.
3. 서브 쿼리는 CREATE, INSERT, DELETE 문에서 사용할 수 있다.
4. 서브 쿼리가 다중열을 리턴하는 경우 IN, ANY, ALL을 사용할 수 있다.

<details>
<summary>5번 정답</summary>
<b>4번</b>. 서브 쿼리가 다중열을 리턴하는 경우 IN, ANY, ALL을 사용할 수 있다.<br>
다중열을 리턴하는 경우 IN은 사용할 수 있으나 ANY와 ALL은 사용할 수 없다.
</details>

<br>

### <b>6</b>. 식별관계와 비식별관계의 차이점을 서술하시오

```

```

<details>
<summary>6번 정답</summary>
식별관계에서는 부모테이블의 기본키 또는 유니크 키를 자식테이블의 기본키로 사용 하는 것이고, 비식별관계는 부모테이블의 기본키 또는 유니크 키를 기본키가 아닌 외래키로 사용하는 것이다.<br>
ER 다이어그램에서 식별관계는 실선으로, 비식별관계는 점선으로 표현한다.
</details>

<br>
