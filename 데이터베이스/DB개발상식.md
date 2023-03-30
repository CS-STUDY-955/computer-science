# DB 개발간 SQL 성능 및 API KEY 보안

## Statement vs. PreparedStatement
- SQL을 실행할 수 있도록 하는 객체

## Statement
```java
String sql = "SELECT name, memo FROM TABLE WHERE name =" + num
Statement stmt = conn.createStatement();
ResultSet rst = stmt.executeQuery(sql);
```
1. sql 구문
2. Connection 에서 createStatement() 메서드로 Statement 객체 생성
3. Statement객체의 executeQuery() 함수를 통해 쿼리문 실행
4. 실행 결과로 ResultSet 반환

## PreparedStatement
```java
String sql = "SELECT name, memo FROM TABLE WHERE user_id = ?"
PreparedStatement pstmt = conn.preparedStatement(sql);
pstmt.setInt(1, userId);
ResultSet rst = stmt.executeQuery();
```
- Statement와 동일한 절차
- Statement와 다르게, 처음 컴파일 된 이후로 컴파일 하지 않고 실행하여 속도가 빠름
- 특수문자를 파싱하여 sql injection 같은 공격을 막을 수 있음

<br>

# API KEY 숨기기
- 내 시스템을 배포할 때, API를 사용한다면, API key를 발급받고 사용함
- API service 사용 시 과금, 개인정보 노출 등 보안 이슈 발생

## Spring 에서 API KEY 숨기기
1. application-API-KEY.properties 생성
2. key = value 형식으로 저장
    ```
    kakao_-_admin_-_key = "ABCD1234"
    google_api_key = "AI12Kjs23"
    ```
3. application.properties에 API-KEY를 include
    ```
    spring.profiles.inlcude=API-KEY
    ```
4. Git을 사용한다면 .gitignore에 properties파일 추가
5. 코드에서 @Value annotation 을 사용하여 API key 사용
    ```java
    import org.springframework.beans.factory.annotation.Value;

    public class KaKaoPayService {
	...
    @Value("${kakao-admin-key}")
    private String kakao_admin_key;

        public String kakaoPayReady(Long orderId) {
            
            HttpHeaders headers = new HttpHeaders();
            headers.add("Authorization", "KakaoAK " + kakao_admin_key);

            /*   ~~   */
        }
    }
    ```
