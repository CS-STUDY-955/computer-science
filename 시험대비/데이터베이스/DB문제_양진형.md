### <b>1</b>. 다음 중 집계 함수가 아닌 것은?
1. COUNT 
2. SUM
3. GREATEST
4. AVG

<br>

### <b>2</b>. 다음 쿼리 문을 실행 시켰을 때 결과로 옳은 것은?

```sql
SELECT * FROM city WHERE population = max(population);
```
1. 인구가 가장 많은 도시 중 기본 정렬순으로 맨 처음 도시 하나의 정보를 반환한다.
2. 인구가 가장 많은 모든 도시들의 모든 정보를 반환한다.
3. 아무것도 출력되지 않는다.
4. 실행되지 않고 에러 코드를 반환한다.

<br>

### <b>3</b>. 다음 쿼리 문을 실행 시켰을 때 결과의 A, B, C의 합은?

```sql
select truncate(1234.5678, -2) as A, round(1234.5678, 2) as B, ceil(-1234.5678) as C;
```
1. &nbsp;1200.56
2. &nbsp;1200.57
3. &nbsp;1201.56
4. &nbsp;1201.57

<br>

### <b>4</b>. Country 테이블의 구조가 다음과 같을 때, 각 대륙 별 최고 인구수를 가진 나라의 모든 정보를 출력하는 쿼리문을 작성하시오.
\* 최고 인구수가 0인 대륙은 제외한다.
|Field|Type|Null|Key|Default|Extra|
|---|---|---|---|---|---|
|Code|char(3)|NO|PRI| | |
|Name|char(52)|NO| | | |
|Continent|char(20)|NO| |Asia| |
|IndepYear|smallint|YES| | NULL| |
|Population|int|NO| |0| |
|GNP|decimal(10,2)|YES| |NULL| |
```


```

<br>

### <b>5</b>. 다음 CREATE문으로 만들어진 테이블에 데이터를 삽입할 때, 올바르게 실행이 되는 쿼리 문으로 옳지 않은 것은?
```sql
drop table if exists product;
create table product (
	code char(4) primary key not null,
    name char(20) not null,
    price int default(0)
);
```
1. insert product value("0017", "Apple", 3000);
2. insert into product values("0022", "Blueberry");
3. insert into product(code, name, price) values("0020", "Kiwi", 5000);
4. insert product(code, name) values("0021", "Mango");

<br>

### <b>6</b>. 다음 쿼리 문들을 순서대로 실행한 결과로 옳은 것은?
```sql
SET autocommit = 0;
DROP TABLE IF EXISTS foo;
COMMIT;
CREATE TABLE foo (
    Number int primary key not null
);
INSERT INTO foo VALUES(10);
ROLLBACK;
INSERT INTO foo VALUES(10);
```
1. Table doesn't exists 오류를 출력한다.
2. Duplicate entry '10' for key 오류를 출력한다.
3. SQL Syntax error 오류를 출력한다.
4. 정상적으로 값이 들어간다.

<br>

### <b>7</b>. "foo"라는 테이블에서 문자열을 저장하는 "bar"라는 Field에 null값이거나 공백인 레코드는 제외하고 출력하려고 한다. 빈칸에 들어갈 구문으로 옳은 것은?
```SQL
SELECT * FROM foo WHERE _________
```
1. LENGTH(bar) != 0 AND bar IS NOT NULL;
2. TRIM(bar) != "" AND bar IS NOT NULL;
3. LENGTH(bar) != 0 AND bar != NULL;
4. TRIM(bar) != "" AND bar != NULL;

<br>

### <b>8</b>. 다음 중 출력 형식이 "NOW()"와 같은 것은?
1. DATE_FORMAT(NOW(), "%y-%m-%d %h:%i:%S");
2. DATE_FORMAT(NOW(), "%y-%m-%d %H:%I:%S");
3. DATE_FORMAT(NOW(), "%Y-%m-%d %H:%i:%s");
4. DATE_FORMAT(NOW(), "%Y-%m-%d %h:%i:%s");

<br>

### <b>9</b>. JDBC를 로딩하는 클래스를 분리 설계했을때, 클래스의 생성자에서 호출되어야 하는 메서드로 옳은 것은?
1. class.forName()
2. DriverManager.getConnection()
3. prepareStatement.executeUpdate()
4. ResultSet.close()

<br>
