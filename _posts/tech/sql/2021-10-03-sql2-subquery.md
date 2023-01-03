---
title:  "SQL 2. Sub Query"

categories:
  - sql

toc: true
toc_sticky: true
 
date: 2021-10-03
---



# 1. SUBQUERY

-   가상의 테이블

# 2. SELECT

-   SELECT : [누적합(윈도우함수)](https://github.com/js0221/test/wiki/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%A6%AC%EC%95%88_03_%EC%9C%88%EB%8F%84%EC%9A%B0%ED%95%A8%EC%88%98#2-%EC%A7%91%EA%B3%84%ED%95%A8%EC%88%98)에서 자주 사용
-   SELECT 절에서 연산한 것은 WHERE절에서 바로 사용 못하기때문에, 서브쿼리로 사용해준다.

# 3. FROM

-   FROM
-   `SELECT * FROM (서브쿼리) 이름`

# 4. WHERE

-   WHERE
    
    -   서브쿼리의 내용이 1개일때, = 사용
    -   서브쿼리의 내용이 여러개일때, IN 사용
    
    ```sql
    SELECT *
    FROM table_name
    WHERE column = (서브쿼리)
    
    SELECT *
    FROM table_name
    WHERE column IN (서브쿼리)
    ```
    

# 5. WITH

-   WITH : 재사용이 가능한 테이블, 반복적인 서브쿼리를 대신할 수 있다
-   `WITH with테이블 AS( 서브쿼리 ) SELECT * FROM with테이블`