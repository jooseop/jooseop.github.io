---
title:  "SQL 3. Window Function"

categories:
  - sql

toc: true
toc_sticky: true
 
date: 2021-10-03
---



# 1. 윈도우 함수

-   함수를 사용하는데, 특정조건인 partition과 order을 적용하는 함수

```sql
    함수(함수를 적용할 컬럼) OVER (PARTITION BY 컬럼 ORDER BY 컬럼)
```

1.  PARTITION BY 컬럼 : 컬럼을 기준으로 묶는다. Group By는 새로운 그룹을 만들어 출력하지만, 윈도우 함수는 원래 있는 각 row에 결과물을 출력한다.
2.  ORDER BY 컬럼 : 컬럼을 기준으로 정렬한다.

# 2. 집계함수

-   MAX
-   ```sql
    MAX(컬럼) OVER (PARTITION BY 컬럼 ORDER BY 컬럼) SELECT Id, , Name , Salary , Max(Salary) OVER (PARTITION BY Department) FROM Employee
    ```
-   SUM
    -   누적합(Cummulative SUM) : Order by 넣어야됨
    ```sql
    SUM(컬럼) OVER (ORDER BY 컬럼) AS CumSum
    SUM(컬럼) OVER (ORDER BY 컬럼 PARTITION BY 컬럼)
    
    SUM(컬럼) OVER (ORDER BY 컬럼) AS CumSum
    SUM(컬럼) OVER (ORDER BY 컬럼 PARTITION BY 컬럼)
    
    SELECT Id
         , Name
         , kg
         , Line 
         , SUM(kg) OVER (ORDER BY Line PARTITION BY Id) AS CumSum
    FROM Elevate
    ```
    
    -   MySQL 구버전은 윈도우 함수가 안되므로, SELECT 서브쿼리 & 조인 사용
    
    1.  Join & Group By 활용
    ```sql
    SELECT *
    FROM Elevator e1
    INNER JOIN Elevator e2
       ON e1.Id = e2.Id
      AND e1.Line >= e2.Line
     /*
     ID LINE ID LINE
     A. 1.   A. 1
     A. 2.   A. 1
     A. 2.   A. 2
     A. 3.   A. 1
     A. 3.   A. 2
     A. 3.   A. 3.
     이런 식으로 됨
     */
    
    -- 최종
    SELECT e1.Id
    , e1.Name
    , e1.kg
    , e1.Line
    , SUM(e2.kg) AS CumSum
    FROM Elevator e1
    INNER JOIN Elavator e2
       ON e1.Id = e2.Id
      AND e1.Line >= e2.Line
    GROUP BY 1,2,3,4 -- SELECT 인자
    -- e1.Line을 기준으로 e2.kg이 합산됨
    ```
    
    2.  SELECT 서브쿼리 : JOIN말고, 서브쿼리
    
    ```sql
    SELECT e1.Id
         , e1.Name
         , e1.kg
         , e1.Line
         , (SELECT SUM(e2.kg)
            FROM Elevator e2 -- 테이블의 일부를 가져온다고 생각
            WHERE e1.Id = e2.Id
            AND e1.Line >= e2.Line) AS CumSum
    FROM Elevator e1
    ```
    
-   기타 : AVG, COUNT, MAX... 등 위와 같은 방식으로 사용

# 3. 순위 정하기

-   함수 안에 컬럼 인자 없음, 특별한 계산 없고 순서 정해주는 것이다.
-   ROW\_NUMBER : 내림차순 정렬, 중복순위 없음
-   RANK : 중복순위 있음, 그다음 순위는 허용한 중복 개수만큼 넘긴 순위 적용 (1,1,3,4,4,4,7,...)
-   DENSE\_RANK : 중복순위 있음, 그다음 순위는 바로 다음 순위 적용 (1,1,2,3,3,3,4,...)

```sql
SELECT val
     , ROW_NUMBER() OVER (ORDER BY val) AS 'row_number'
     , RANK() OVER (ORDER BY val) AS 'rank'
     , DENSE_RANK() OVER (ORDER BY val) AS 'dense_rank'
FROM sample
```

# 4. 데이터 위치 바꾸기

-   LAG : 아래로 데이터를 밀어준다. 맨 위 데이터는 NULL이 됨
-   LEAD : 위로 데이터를 당겨준다. 맨 아래 데이터는 NULL이 됨
-   함수(컬럼, 칸수, 디폴트)
    -   칸수 : 몇 칸씩 밀고, 당길지 정해 줄 수 있다.
    -   디폴트 : NULL 대신에 넣을 값

```sql
SELECT ID
     , RecordDate
     , Temperatur
     , LAG(Temperature) OVER (ORDER BY RecordDate) AS 'lag'
     , LEAD(Temperature) OVER (ORDER BY RecordDate) AS 'lead'
FROM sample
```