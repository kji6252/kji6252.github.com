---
title: 객체지향 쿼리 언어
date: 2017-01-23 09:47:00
categories:
  - JPA
tags:
  - Java
  - JPA
  - ORM

---
1 JPQL 소개
=============

JPQL(Java Persistence Query Language) : 엔티티 객체를 조회하는 객체지향 쿼리.

* JPQL은 SQL을 추상화해서 특정 데이터베이스에 의존하지 않는다.
* JPQL은 객체지향 쿼리 언어다. 테이블X 엔티티O
* JPQL은 결국 SQL로 변환된다.
<!-- more -->
1.1 기본문법
------------

JPQL도 SQL과 비슷하게 SELECT, UPDATE, DLEETE 문을 사용(INSERT는 EntityManager.persist() 사용)

* 대소문자 구분 : 엔티티와 속성은 대소문자 구분(ex : Member, username). 반면 SELECT, FROM, AS 같은 JPQL 키워드는 대소문자를 구분하지 않음
* 엔티티 이름 : @Entity(name="XXX")로 지정하거나 지정안할시 클래스명을 기본으로 사용
* 별칭은 필수 JPQL 표준은 필수 HQL(Hibernate Query Language)는 생략 가능.

1.2 쿼리 API
--------------

반환타입을 명확히 할수 있는 TypeQuery와

![](https://lh3.googleusercontent.com/8vfqOwI1AcjZ4HwAX6534UrU5EOT35F91gNfO524aKqinMIy6h7FbqmG0x2mKNlfn53S23uMvnPcMXtTFGkLcVkiW3BsTaEg9xJkU5-6Yyz6rBAgTTAbO4Y8FRotdn1KxNs2H5N8)

명확히 지정할 수 없을땐 Query를 사용하면 됨

![](https://lh4.googleusercontent.com/RsoMfsdIw5B9kO6nFfXKIw_AxvFRZmU_BqmxdXyGZNkUKPM-8blAmPkG2QyNN4ye2C9TriJ_aTLZReIiuLvVD7MQPIHNUE4cf6TOwknfikyn-Ady5zzWAZOCY-GZtGWMVIwlUf0o)

1.3 파라미터 바인딩
----------------

이름 기준

```
SELECT m FROM Member m where m.username=:username

query.setParameter("username", usernameParam);
```

위치 기준

```
SELECT m FROM Member m where m.username=?1

query.setParameter(1, usernameParam);
```

1.4 페이징 API
---------------

![](https://lh5.googleusercontent.com/sUJy0ndiig55APOeS5LrAyEwVEUVsn6yJzvlcZbCN8fGhyH4iP1VKhTMO6BriUV20gizfNbGMT5U2V5_HMUAcRglLn84hMvbk35s-ehvgcsleiJX6qE0wGhMyCtfrtI-7gBkabaj)

페이징 API - MySQL 방언

```sql
SELECT
M.ID AS ID,
M.AGE AS AGE,
M.TEAM_ID AS TEAM_ID,
M.NAME AS NAME
FROM
MEMBER M
ORDER BY
M.NAME DESC LIMIT ?, ?
```

페이징 API - Oracle 방언

```sql
SELECT * FROM
( SELECT ROW_.*, ROWNUM ROWNUM_
FROM
( SELECT
M.ID AS ID,
M.AGE AS AGE,
M.TEAM_ID AS TEAM_ID,
M.NAME AS NAME
FROM MEMBER M
ORDER BY M.NAME
) ROW_
WHERE ROWNUM <= ?
)
WHERE ROWNUM_ > ?
```

1.5 집합과 정렬
--------------

```sql
select
COUNT(m),   //회원수
SUM(m.age), //나이 합
AVG(m.age), //평균 나이
MAX(m.age), //최대 나이
MIN(m.age)  //최소 나이
from Member m
GROUP BY, HAVING
ORDER BY
```

1.6 조인
----------

* 내부 조인: SELECT m FROM Member m \[INNER\] JOIN m.team t
* 외부 조인: SELECT m FROM Member m LEFT \[OUTER\] JOIN m.team t
* 세타 조인: select count(m) from Member m, Team t where m.username = t.name

한계: 세타 조인시은 내부 조인만 사용할 수 있다.​

### 페치 조인

* 엔티티 객체 그래프를 한번에 조회하는 방법
* 별칭을 사용할 수 없다.
* JPQL: select m  from Member m join fetch m.team
* SQL: SELECT  M.*, T.* FROM MEMBER T INNER JOIN TEAM T ON M.TEAM_ID=T.ID

예시

![](https://lh6.googleusercontent.com/uZz7CeaYZtnDJchkM8vyR_Pdnlql-B5vBShuplBoaumtekaABcipYMrpUMk0G3yQttPHpKnvaxGt5SeNjldEg7mqMFIKk7aHVikl55dABDf6_7hhK22N8Zlkxd7alFtf9C1SnwE9)

최적화를 위해 글로벌 로딩 전략을 즉시 로딩으로 설정하면 애플리케이션 전체에서 항상 즉시 로딩이 일어난다. 물론 일부는 빠를 수는 있지만 전체로 보면 사용하지 않는 엔티티를 자주 로딩하므로 오히려 성능에 악영향을 미칠 수 있다. 따라서 글로벌 로딩 전략은 될 수 있으면 지연 로딩을 사용하고 최적화가 필요하면 페치 조인을 적용하는 것이 효과적이다.

1.7 JPQL 기타
---------------

* 서브 쿼리 지원 (from절에서 사용안됨)
* EXISTS, IN
* BETWEEN, LIKE, IS NULL

JPQL 기본 함수

* CONCAT 문자열 합침
* SUBSTRING 문자열 자름
* TRIM 빈공간제거
* LOWER, UPPER 소문자로, 대문자로 치환
* LENGTH 길이를 구함
* LOCATE 검색위치부터 문자를 검색 1부터 시작 못찾으면 0반환
* ABS 절대값, SQRT 제곱근, MOD 나머지
* SIZE 컬렉션크기 구함, INDEX 컬렉션의 위치값 구함(JPA 용도)

CASE 식

![](https://lh6.googleusercontent.com/VLOLnFRuB27J5AyS_kUpRuz5Qyo-yIJWq5JNzTjPI_5yv0ELDLEoZCm_YW0FO_zB3M6zh1kPyu-hPBZntRdK7qBqVtIYsF67nTom2jGF55ZalBrzRcmGHeXLKjXMLsqiRd8UFeZy)

![](https://lh3.googleusercontent.com/mfoMorocy1hxklYtF8HwetaPQraDig8e2anEdAQmPOD1paJaYuGiWRojFptNNXCAAOyXhRJcM7T-5QPhKVQvbhK6aEZDapx2NCkfly7Nc199dRlmXQzBssCW0tppI2aOHBGA0EGh)

1.8 Named 쿼리: 정적 쿼리
-----------------------

* 미리 정의해서 이름을 부여해두고 사용하는 JPQL
* 어노테이션, XML에 정의
* 애플리케이션 로딩 시점에 초기화 후 재사용
* 애플리케이션 로딩 시점에 쿼리를 검증

![](https://lh4.googleusercontent.com/2SRgVZWCpn6hQaCqiQP0vziMpEoHHNnpr9J4e2hAnPGK90to6DbgDzvX57_qXT4EIXYPot2Hgi1tbkUlZLGjMkF680b7AY7YW9f5GrMVxVVdUAKlG1nK106Eph-UYEytyyDqUgJw)
