---
title:  "SQL 4. User Defined Function"

categories:
  - sql

toc: true
toc_sticky: true
 
date: 2021-10-03
---

# 1. 사용자 정의 함수
-   사용자가 함수를 새로 정의하여 사용하는 함수

# 2. 구조

```sql
-- 구조 요약
CREATE  함수이름
    리턴
BEGIN
    DECLARE '변수이름';
    SET 연산;
END

-- 함수 선언
CREATE  FUNCTION '함수이름'(파라미터 이름, 데이터 타입)
    RETURNS '출력타입' (DETERMINISTIC)
    -- DETERMINISTIC은 결과 리턴 값이 항상 고정된 값인 경우 사용, 아닌 경우는 deterministic 안적으면 됨
BEGIN
    DECLARE '변수선언' ; -- 따옴표, 세미콜론 적기
    SET 변수정의 ; -- 세미콜론 적기
    RETURNS
END

-- 함수 사용
SELECT '함수이름'(파라미터)
```