---
title:  "SQL 5. Group by & Having"

categories:
  - sql

toc: true
toc_sticky: true
 
date: 2021-10-03
---


# Group By

1.  SELECT는 테이블을 조회만 하는 것이다. 새로 만드는 것이 아님.
2.  Group By에 넣은 그 속성끼리 같은 것을 일단 묶는다.위의 sql문은, groupby를 하여 단지 묶은것 뿐이다. 테이블의 조회하려는 목록은 없는 것이다.
3.  `select * group by 속성1`
4.  따라서 그룹화를 사용한 경우, 무엇인가 보고 싶다면, GROPU BY에도 넣어준 속성을 SELECT에 넣어서 볼 수 있다.  
      
    즉, SELECT에서 속성을 넣어 보고 싶다면 GROUP BY에 넣어준다.
5.  `select 속성1 group by 속성1`
6.  연산하여 조회하는 것은 GROUP BY에 넣어주지 않아도 된다.
7.  `select count(*) group by 속성1`

-   Group By 기준 컬럼 여러개 참고 : [https://inf.run/sVX5](https://inf.run/sVX5)

# Having

-   group by를 사용한 결과물을 가지고 연산하고 싶을 때 사용

```sql
select Email
from Person
group by Email
having count(ID) >= 2
```

```sql
select Email
      ,Count(Id) AS cnt
from Person
group by Email
```

| Email | cnt |
| --- | --- |
| [a@b.com](mailto:a@b.com) | 2 |
| [c@d.com](mailto:c@d.com) | 1 |

-   SELECT절에서 사용한 AS를 WHERE절에서는 사용 못하지만, HAVING절에서는 사용 가능