# DB 과목평가 예상문제

## 1. mysql에서 char 자료형과 varchar 자료형의 차이를 설명하고, 사용되는 예시를 한가지씩 쓰시오.

<details>
    <summary>정답</summary>
    <b>char: 고정된 크기만큼을 차지하는 문자열, varchar: 지정된 크기보다 작은 문자열을 저장하면 그만큼 크기를 줄여 저장함</b> <br>
    char: 전화번호, 주민등록번호, ...
    varchar: 아이디, 이름, ...
</details>

## 2. 다음 중 인덱스를 사용하기 가장 좋지 않은 컬럼은?
1. 외래키 컬럼
2. Unique 컬럼
3. 자주 조인되는 컬럼
4. 자주 변경되는 컬럼

<details>
    <summary>정답</summary>
    <b>4</b> <br>
    데이터가 변경될 때마다 인덱스도 함께 변경되어야 하므로 인덱스를 사용하기에 적절하지 않다.
</details>

## 3. 다중 행을 반환하는 서브쿼리의 결과가 모두 만족해야 true를 반환하는 예약어는?

<details>
    <summary>정답</summary>
    <b>ALL</b> <br>
    ALL 예약어는 서브쿼리의 모든 반환 행이 조건을 만족해야 true를 반환한다.
</details>

## 4. From 절에 사용되며, 결과가 테이블처럼 생성되어 임시적으로 자유롭게 참조가능한 서브쿼리의 명칭을 쓰시오.

<details>
    <summary>정답</summary>
    <b>Inline View</b> <br>
    인라인 뷰는 from 절에 사용되어 임시적으로 사용할 수 있는 서브쿼리이다.
</details>

#### - 다음은 회원과 게시글 정보 테이블이다. 이를 이용하여 5~7번 문제를 푸시오.
```mysql
-- 회원 정보 테이블
CREATE TABLE IF NOT EXISTS `member` (
`member_id` VARCHAR(16) NOT NULL,
`member_name` VARCHAR(20) NOT NULL,
`member_password` VARCHAR(64) NOT NULL,
`member_phone` CHAR(13) NOT NULL,
`email_id` VARCHAR(20) NULL DEFAULT NULL,
`email_domain` VARCHAR(45) NULL DEFAULT NULL,
`join_date` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
PRIMARY KEY (`member_id`))
```

```mysql
-- 게시판 정보 테이블
CREATE TABLE IF NOT EXISTS `board` (
  `article_no` INT NOT NULL AUTO_INCREMENT,
  `member_id` VARCHAR(16) NULL DEFAULT NULL,
  `subject` VARCHAR(100) NULL DEFAULT NULL,
  `content` VARCHAR(2000) NULL DEFAULT NULL,
  `hit` INT NULL DEFAULT 0,
  `register_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`article_no`),
  INDEX `board_to_members_member_id_fk` (`member_id` ASC) VISIBLE,
  CONSTRAINT `board_to_members_member_id_fk`
    FOREIGN KEY (`member_id`)
    REFERENCES `member` (`member_id`)
    ON DELETE CASCADE)
```

## 5. 게시글 작성 id가 byh9811인 게시글의 제목을 회원명과 함께 출력하는 SQL을 작성하시오. (각 컬럼명은 회원명, 제목으로 출력한다.)

<details>
    <summary>정답</summary>
    <b>select member_name, subject from member natural join board where member_id = 'byh9811'</b> <br>
    inner join, join 등 여러 방법으로 조인할 수 있다.
</details>

## 6. id가 byh9811 회원이 탈퇴를 신청했다. 관리자는 해당 회원이 작성한 게시글 중 조회수가 높은 10개의 내용을 확인하여 불량한 회원인지 확인한 후 승인하도록 하려고 한다. 관리자에게 필요한 SQL을 작성하시오.

<details>
    <summary>정답</summary>
    <b>select content from member natural join board where member_id = 'byh9811' order by hit desc limit 10</b> <br>
    문장 해석 능력과 order by, limit를 요구하는 문제다.
</details>

## 7. 관리자는 최근 1달간 작성된 게시글 중 조회수 top 3를 뽑아 해당 글을 작성한 유저의 핸드폰번호로 기프티콘을 발송하려고 한다. 관리자에게 필요한 SQL문을 작성하시오. (단, 가입한 이후 글을 10개 이상 작성하지 않은 회원은 제외하고 선정한다.) (동일한 회원이 top3 안에 둘 이상일 경우, 한 번만 검색한다.)

<details>
    <summary>정답</summary>
    <b>select distinct member_phone <br />
    from member <br />
    natural join board <br />
    where article_no in <br />
    (select article_no <br />
    from board <br />
    where register_time >= DATE_SUB(NOW(), INTERVAL 1 MONTH) <br />
    order by hit desc <br />
    limit 3)</b> <br>
    다중 행을 반환하는 서브 쿼리를 사용 능력을 요구하는 문제다.
</details>
