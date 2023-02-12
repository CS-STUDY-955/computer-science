# DB 과목평가 예상 문제
## 1. 어느날 회장이 자리를 비워 직속상사가 회장인 직원들은 눈치를 볼 필요가 없어졌다. 그러나 다른 직원들은 직속상사가 존재하기 때문에 여전히 불편한데, 이 때 불편한 직원의 수를 구하려고 한다. 빈칸에 들어갈 함수는? (회장의 id는 100이며 manager_id도 100이라고 가정한다.)
```mysql
select count(___(manager_id, 100)) as freeman
from employees;
```

## 2. 부서별로 연봉이 5000이상인 직원의 수를 검색하려고 한다. 다음 SQL문에서 잘못된 부분은?
```mysql
select department_id, count(*)      -- 1
from employees                      -- 2
group by department_id              -- 3
having salary>=5000;                -- 4
```

## 3. 다음 중 에러가 발생하는 DML 문장은? (employees 테이블은 id와 name만을 필드로 가진다고 가정한다.)
1. insert employees into values(id, name);
2. update employees set id='id', name='name';
3. delete from employees where id='id';
4. select all max(id) from employees where id='id';

## 4. 다음 설명이 의미하는 JDBC 인터페이스를 쓰시오.
- 동일한 SQL 문장이 여러번 반복적으로 수행될 때 사용하는 객체
- 대용량의 문자나 바이너리 타입의 데이터를 저장하기 위해서 사용될 수 있음
- 여러번 반복 수행시 clearParameters() 메서드를 이용해 남겨진 값을 초기화할 수 있음

## 5. 다음은 JDBC를 이용해 입력한 제목을 포함하는 도서목록을 가져오는 코드이다. 잘못된 부분은?
```java
public List<Book> getBooksByTitle(String title) {
    Connection conn = null;
    PreparedStatement pstmt = null;
    ResultSet rs = null;
    List<Book> list = new ArrayList<>();
    try {
        conn = factory.getConnection();
        StringBuilder sb = new StringBuilder("SELECT * FROM book where title like '%?%'");      // 1
        pstmt = conn.prepareStatement(sb.toString());                                           // 2
        pstmt.setString(1, title);
        rs = pstmt.executeQuery();                                                              // 3
        Book dto = null;
        while(rs.next()) {                                                                      // 4
            dto = new Book();
            dto.setIsbn(rs.getString("isbn"));
            dto.setTitle(rs.getString("title"));
            dto.setAuthor(rs.getString("author"));
            dto.setPublisher(rs.getString("publisher"));
            dto.setPrice(rs.getInt("price"));
            dto.setDesc(rs.getString("desc"));
            dto.setPublished_date(rs.getTimestamp("published_date").getTime());
            list.add(dto);
        }
    } catch (SQLException e) {
        System.out.println("[오류]도서 전체 조회");
        e.printStackTrace();
    } finally {
        factory.close(conn, pstmt, rs);
    }

    return list;
}
```

## 6. JDBC는 데이터를 수정하는 DML을 요청하는 executeUpdate() 메서드를 사용한다. 이 메서드는 어떤 타입을 리턴하며, 무엇을 의미하는지 설명하시오.

## 7. 주어진 SQL(1)의 결과가 1일 때, SQL(2)의 결과는 무엇인가?
```mysql
# SQL (1)
select count(2)
from employees
group by department_id
having department_id is null;
```
```mysql
# SQL (2)
select count(not department_id)
from employees
group by department_id
having department_id is null;
```