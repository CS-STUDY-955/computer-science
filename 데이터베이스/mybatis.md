# Mybatis
- 마이바티스는 개발자가 지정한 SQL 등 몇가지 고급 매핑을 지원하는 프레임워크
- JDBC로 처리하는 상당부분의 코드와 파라미터 설정및 결과 매핑을 대신해줌
- 데이터베이스 레코드에 원시타입과 Map 인터페이스를 설정해서 매핑하기 위해 XML과 애노테이션을 사용할 수 있음

## 특징
- 쉬운 접근성과 코드 간결성
- SQL문과 프로그래밍 코드의 분리
- 다양한 프로그래밍 언어로 구현 가능

## 사용
```xml
<select id="viewArticle" parameterType="int" resultType="article">
  SELECT * 
  FROM Article
  WHERE ID = #{id}
</select>
```
- attributes
    - **id** : 이 sql 구문을 구분하기 위한 unique한 식별자
    - **parameterType** : 구문에 전달된 파라미터 패키지 경로를 포함한 전체 클래스명이나 별칭
    - **resultType** : 이 구문에 의해 리턴되는 클래스명이나 별칭
    - **resultMap** : 외부 resultMap의 참조명. resultMap은 마이바티스의 가장 강력한 기능.

- TypeAlias
```xml
<!-- XML설정파일에서 -->
<typeAlias type="com.someapp.model.User" alias="User"/>

<!-- SQL매핑 XML파일에서 -->
<select id="selectUsers" resultType="User">
  select id, username, hashedPassword
  from some_table
  where id = #{id}
</select>
```

- 결과 매핑
```xml
<resultMap id="authorResult" type="Author">
  <id property="id" column="author_id"/>
  <result property="username" column="author_username"/>
  <result property="password" column="author_password"/>
  <result property="email" column="author_email"/>
  <result property="bio" column="author_bio"/>
</resultMap>
```

## 주의사항!!
- DMBS 종류별로 문법의 차이가 존재하니 개발하는 DBMS 종류에 맞는 문법을 확인하고 적용할 것!
- 문자열 비교시 test 문 안에 single/double quatation 구분하여 사용할 것!
    ```xml
    <!-- error code -->
    <if test="name == 'KIM'"> </if>

    <!-- 정상 code -->
    <if test='name == "KIM"'> </if>
    <if test="name == 'K'"> </if>
    ```
- resultMap, resultType으로 사용자 지정 DTO 생성할 경우, 자동으로 mapping해주게 되는데, 사용자가 DTO.java에 사용자지정 생성자를 선언해줬을경우, 반드시 기본 생성자도 생성해주어야 mapping 가능함!



## 참고문헌
- https://mybatis.org/mybatis-3/ko/index.html