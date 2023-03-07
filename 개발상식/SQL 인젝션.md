# SQL Injection (SQL 주입)

+ SQL 주입(삽입)은 웹 응용 프로그램의 보안 상의 허점을 이용해 악의적인 SQL문을 악의적으로 실행시켜 데이터베이스를 비정상적으로 조작하는 공격 방법
+ SQL 주입이란 개념은 1998년 12월에 처음으로 정립 되었지만, 현재에도 여전히 SQL Injection에 취약하게 설계되는 어플리케이션이 많으며 웹 애플리케이션의 30% 이상으로 추측됨
+ 따옴표와 OR 문, 주석처리를 통해 사용자의 입력이 항상 참이 되게끔 할 수 있음
+ SQL 질의문을 통하여 데이터베이스에 저장되어 있는 값들을 알 수 있으며 저장된 해시 값을 조회하여 John the Ripper 도구를 통해 비밀번호를 크래킹할 수 있음

<br>

![sql-injection-attack](./img/Example-of-a-SQL-Injection-Attack.png)

<br>

## 예시

<br>

```sql
-- 로그인 쿼리 예시
select * from users where userid = "{userid}" and userpassword = "{userpassword}";
```
+ userid 혹은 userpassword에 악의적인 sql문 삽입 가능

<br>

```sql
select * from users where userid = "jinhyugn" and userpassword = " " OR "1" = "1 ";
```

+ users 테이블에 있는 모든 user의 정보 조회

<br>

```sql
select * from users where userid = " "; drop table users; -- " and userpassword = "";
```

+ users 테이블을 drop 시키기

<br>

## 사례

### 1. 여기어때 해킹
<br>

![sqli-case2](https://user-images.githubusercontent.com/68081743/223422802-82a78434-2744-4dd3-bd04-518200e52f52.JPG)

https://www.joongang.co.kr/article/21628794#home

+ 마케팅센터 웹페이지에 SQL 인젝션 공격을 통해 DB에 저장된 관리자 세션값(세션 아이디)을 탈취
+ 약 99만명의 숙박 예약 정보, 회원 정보 유출

<br>

### 2. 뽐뿌 커뮤니티 개인정보 해킹
<br>

![sqli-case4](https://user-images.githubusercontent.com/68081743/223422951-02278a9b-8faf-468a-b84b-ce7b8b80de14.JPG)

https://www.korea.kr/news/pressReleaseView.do?newsId=156081058

+ 홈페이지에 비정상적인 DB 질의에 대한 검증 절차가 없어 SQL 인젝션 공격에 취약한 페이지가 존재했음
+ 약 196만명의 회원 정보 유출

<br>
