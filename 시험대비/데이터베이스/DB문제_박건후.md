# 1. 다음과 같은 결과를 얻기 위해서 SQL문을 완성하시오.
![image](https://user-images.githubusercontent.com/15648142/218261509-d63cc39b-4731-4e6b-b6ec-d161d20caee5.png)
```sql
select employee_id as 사번, first_name 이름, salary "급여", salary*12 "연   봉",
		commission_pct, salary * (________________) *12 "커미션포함연봉"
from employees;
```
<br>

# 2. 이름에 s가 들어간 사람을 조회하는 SQL구문을 완성하시오.
```SQL
select employee_id, first_name
from employees
where first_name ____ _____;
```
<br>  

# 3. SELECT 구문의 수행 순서를 올바르게 작성하시오.
____ > ____ > ____ > ____ > ____ > ____
<br>  
<br>  

# 4. 급여에 따라 등급표시를 검색하는 SQL구문을 완성하시오.
```SQL
select employee_id as 사번, first_name 이름, salary "급여",
		____ 
			____ salary >= 15000 ____ "고액연봉"
			____ salary >= 8000 ____ "평균연봉"
            ____ "저액연봉"
		____ "등급", department_id
from employees;
```

# 5. DB연산자 중 ORDER BY 뒤에 올수 없는 구문은?
1. 항목 INDEX 번호
2. COLUMN 명
3. 수식
4. SELECT 사용한 ALIAS
5. 메서드(함수)

# 6. 쿼리가 끝난 후 현재 시각을 23.Feb.24th 형식으로 출력하는 SQL구문을 작성하시오.
<br>  
<br>  

# 7. 쿼리가 시작한 순간의 현재 시각에서 1시간 뒤의 시간을 2023.2.7. 형식으로 출력하는 SQL 구문을 작성하시오.
<br>  
<br>  

# 8. 숫자 12345를 1의자리 이하를 버리고 출력하는 SQL구문을 작성하시오.
<br>  
<br>  

# 9. 다음 SQL 구문의 수행 결과는?
```SQL
SELECT INSTR('foobar', 'bar');
SELECT INSTR('foobar', 'test');
```
<br>  

# 10. IFNULL, IF, NULLIF의 차이점에 대해 서술하시오.
<br>  
<br>   

# 11. TCL 중 설정된 복구 지점으로 회기하는 명령어를 입력하시오.
<br>  
<br>  

# 12. MySQL에서 입력 시 자동으로 index가 증가되는 명령어를 입력하시오.
<br>  
<br>  

# 13. 다음 중 오류가 나는 SQL 구문은?
```SQL
-- 1
SELECT gender, age
FROM member
GROUP BY gender;

-- 2
SELECT gender, age, name
FROM member
WHERE age like "%w%" and length(name) >= 10
ORDER BY length(name) desc;

-- 3
SELECT gender, age, name
FROM member
LIMIT 10, 10;

-- 4
INSERT INTO ssafy_member(id, gender, age, name)
SELECT id, gender, age, name
from member
where id = 0954126;
```
<br>  

# 14. 다음은 FactoryDao 설계 중 일부분이다. 빈칸에 들어갈 알맞은 말을 입력하시오.
```java
public Connection getConnection() {
		try {
			return ______.______(URL, USER, PASSWORD);
		} catch (SQLException e) {
			e.printStackTrace();
		}
		return null;
	}
```
<br>  

# 15. 다음은 BoardDao 구현 중 일부분이다. 빈칸에 들어갈 알맞은 말을 입력하시오
```java
	public int addBoard(Board dto) {
		Connection conn = null;
		PreparedStatement pstmt = null;
		try {
			conn = factory.getConnection();
			// title, content는 String type, id는 int type, created_at은 long type이다.
			String sql = "INSERT INTO BOARD (title, content, id, created_at) values (?, ?, ?, NOW())";
			pstmt = conn.____________(sql); // #1

			pstmt.__________(_, dto.getTitle()); // #2, #3
			pstmt.__________(_, dto.getContent()); // #2, #4
			pstmt.__________(_, dto.getId()); // #2, #5

			return pstmt.__________(); // #6
			
		} catch(SQLException e) {
			System.out.println("[오류]등록");
			e.printStackTrace();
		} finally {
			// 자원해제
			factory.close(conn, pstmt);
		}
		return 0;
	}
```