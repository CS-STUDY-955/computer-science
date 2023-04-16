# DB 과목평가 예상문제

## 1. mysql에서 char 자료형과 varchar 자료형의 차이를 설명하고, 사용되는 예시를 한가지씩 쓰시오.

## 2. 다음 중 인덱스를 사용하기 가장 좋지 않은 컬럼은?
1. 외래키 컬럼
2. Unique 컬럼
3. 자주 조인되는 컬럼
4. 자주 변경되는 컬럼

## 3. 다중 행을 반환하는 서브쿼리의 결과가 모두 만족해야 true를 반환하는 예약어는?

## 4. From 절에 사용되며, 결과가 테이블처럼 생성되어 임시적으로 자유롭게 참조가능한 서브쿼리의 명칭을 쓰시오.

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

## 6. id가 byh9811 회원이 탈퇴를 신청했다. 관리자는 해당 회원이 작성한 게시글 중 조회수가 높은 10개의 내용을 확인하여 불량한 회원인지 확인한 후 승인하도록 하려고 한다. 관리자에게 필요한 SQL을 작성하시오.

## 7. 관리자는 최근 1달간 작성된 게시글 중 조회수 top 3를 뽑아 해당 글을 작성한 유저의 핸드폰번호로 기프티콘을 발송하려고 한다. 관리자에게 필요한 SQL문을 작성하시오. (단, 가입한 이후 글을 10개 이상 작성하지 않은 회원은 제외하고 선정한다.) (동일한 회원이 top3 안에 둘 이상일 경우, 한 번만 검색한다.)
