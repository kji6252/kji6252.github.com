---
title: QueryDSL
date: 2017-01-23 09:53:00
categories:
  - JPA
---
### **1 QueryDSL 소개**

*   **JPQL을 코드로 작성할 수 있도록 도와주는 빌더 API**
*   **JPA 크리테리아에 비해서 편리하고 실용적임**
*   **쿼리를 문자가 아닌 코드로 작성해도, 쉽고 간결하며 그 모양도 쿼리와 비슷하게 개발 할 수 있는 프로젝트가 바로 QueryDSL 이다.**
*   **오픈소스**

### **1.1 장점**

*   **문자가 아닌 코드로 작성**
*   **컴파일 시점에 오류 발견**
*   **코드 자동완성**
*   **단순함, 쉬움: 코드 모양이 JPQL과 거의 흡사.**
*   **동적 쿼리**

### **1.2 작동 방식**

**![](https://lh5.googleusercontent.com/AVfAUXPSxor45lTvSanV-IkKLYRLndp7qXOe2dWBKnZjZ8N0PBckegjWNpvXWS3SPj9QpwWMLvl7U7cUj8KM7mY8X4ykbYx2zppPEKfMAe7dRen-Ew4CtUZA2evYtg8GLimWSm5M)**

### **1.3 maven 셋팅**

**![](https://lh6.googleusercontent.com/YdriXl8A1rZH7--lMIoXIcmU6fPPy7JbEsGSKno86ZDLv30joetRMJyeC20hI-EpuM-Bl13kj3clgsQ2bwwIitOaSeks1TqjXppMSVG6Rg8B1OEbmyOQNyEmaly311jAP_PzKUky)**

**![](https://lh6.googleusercontent.com/6oCoJka5d-3cKXoyYdczF7JsamRj1q9H8OzuVgI_AILRrX4jeeddlS2asWCLX1BkBRD1aTFpVx6Mt0c8EOnvd2efe8XAp52whdGbsiDn09uVomS7xHkC6ImkrosW0_8BXb0xNB4N)**

### **1.4 쿼리 타입 생성**

**![](https://lh5.googleusercontent.com/L-gnSon8L1sD9oD9VT-WeghP-ATZN_8YWuZ8-vinQUAmdQvkx0fsoVSLJsGP8HOLklEbxNHIW94JNQYEWrEbJPZJM6umLzlNVkWGv5ZURG2V_nnL012ZyIyMeEgCsYlB76zuLwOm)**

**메이븐 QueryDSL 설정을 하고 나서 mvn compile 명령어를 실행 하면**

**QueryDSL에서 사용할수 있는 Q타입 생성**

**JPQL - Entity**

**QueryDSL - QEntity**

**자동 생성된 쿼리 타입(Q)**

**![](https://lh4.googleusercontent.com/0s2eVZ3ruiRy-E49StfPhuWafTfjthFXcfdzdlBMwZO8IKbNCq5n6LpvmTExW-sRnSx-2Tl2nZGFTrjBj42F2EOdr7JNTfdmPY4XEZmgUj7BkGwSXZF1gFSFNlOsm4ZOI2JhqiBk)**

### **1.5 쿼리 사용**

**![](https://lh6.googleusercontent.com/gXyE-X1dZwfMK_Sf9B_nYyV8hDqF-udj7HNQLT9PQbGAE_daH_PGz0snVs1f646YvbyUM5tye8Opa3_49xFA2bfWsx_BQcZeJHIAKwhxuDjd9XuTe0KpzLNjNnib25voOUXzQKD8)**

**조인**

**![](https://lh6.googleusercontent.com/c7P0-fsN_Xb6d3Td5zEXbFZ5s22S9Tn6xdw37WQlYmUzsjVoGYPLILOx77VWmnc0RiUTy39WcsftCVG3Go5YwQjk4g84_qzTwk1C53GezScGev1-T_UiO_YtffkFbj0ARYGkx-pr)**

**페이징**

**![](https://lh3.googleusercontent.com/lQ1Ws8hnmbUY0RmO6RXvMPK-MFeqyLWxHzxNA9kw4nQDTs-hjlIV2IRe21R_OfNKaIZrRaw0BJJMHb2FmeBURro0ZiT1evP227f2XaJ83EYxtip7_rNVG6SfIQuUkgbuli65N_92)**

**동적쿼리**

**![](https://lh3.googleusercontent.com/o5KMcCgJpWk5rBbLJLCLXk8ny7BDaeoPhveBsHSiuYKVvUhFh1SeRkjcELOYueRODsq7nyylqEv1eJD7kcWItSdc6ICQFiIgIVkM4ugna2kdlBJyoeIgXfsp1Tucg7fV6-V9nmCA)**

### **1.6 기능 정리**

*   **from**
*   **innerJoin, join, leftJoin, fullJoin, on**
*   **where (and, or, allOf, anyOf)**
*   **groupBy**
*   **having**
*   **orderBy (desc, asc)**
*   **limit, offset, restrict(limit + offset) (Paging)**
*   **list**
*   **listResults (list + Paging Info(totalCount))**
*   **iterate**
*   **count**
*   **singleResult, uniqueResult**
