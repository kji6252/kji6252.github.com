---
title: JPA 소개 JPA 시작
date: 2016-08-03 09:47:00
categories:
  - JPA
---
**1\. JPA 소개**
==============

하이버네이트 오픈소스 ORM 프레임워크가 나온 후 자바빈이 버려지고 하이버네이트, 이클립스링크등의 ORM 프레임워크로 자바 ORM 표준을 정한것이 JPA 이다.

[**JPA(Java Persistent API) : **](https://ko.wikipedia.org/wiki/JPA)관계형 [데이터베이스](https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4 "데이터베이스")에 접근하기 위한 표준 [ORM](https://ko.wikipedia.org/wiki/ORM "ORM") 기술을 제공하며, 기존에 [EJB](https://ko.wikipedia.org/wiki/EJB "EJB")에서 제공되던 엔터티 빈(Entity Bean)을 대체하는 기술이다. JPA는 JSR 220에서 정의된 EJB 3.0 스펙의 일부로 정의가 되어 있지만, JPA는 EJB 컨테이너에 의존하지 않으며 EJB, 웹 모듈 및 [Java SE](https://ko.wikipedia.org/wiki/Java_SE "Java SE") 클라이언트에서 모두 사용이 가능하다. 또한, JPA는 사용자가 원하는 퍼시스턴스 프로바이더 구현체를 선택해서 사용할 수 있다.

[ORM(Object Relational Mapping) :](https://ko.wikipedia.org/wiki/%EA%B0%9D%EC%B2%B4_%EA%B4%80%EA%B3%84_%EB%A7%A4%ED%95%91) 관계형 데이터베이스를 객체에 매핑.

왜 JPA를 사용해야 하는가?

1.  생산성 : 지루하고 반복적인 CRUD 코드를 직접 작성하지 않아도 된다.
2.  유지보수 : 엔티티에 필드를 하나만 추가해줘도 등록, 수정, 조회 자동으로 매핑 된다.
3.  패러다임의 불일치 해결 : 관계형 DB로 객체지향적인 코딩이 가능해 진다.
4.  성능 : 한번 조회한건 캐시를 사용함으로 똑같은걸 2번 조회 하지 않는다.(1차캐시)
5.  데이터 접근 추상화와 벤더 독립성 : 방언을 통해 자유자제로 다른 DB로 변경이 가능 하다.
6.  표준 : 자바 진영의 ORM 표준이다.

#### JPA 소개 정리

지금까지 SQL을 직접 다룰 때 발생하는 다양한 문제와 객체지향 언어와 관계형 데이터베이스 사이의 패러다임 불일치 문제를 설명했다. 그리고 JPA가 각 문제를 어떻게 해결하는지 알아보았다. 마지막으로 JPA가 무엇인지 설명하고 JPA의 장점을 소개했다. JPA에 관한 자세한 내용은 책 전반에 걸쳐서 차근차근 살펴보기로 하고, 우선은 다음 장에서 테이블 하나를 등록/수정/삭제/조회하는 간단한 JPA 애플리케이션을 만들어보자.

**2\. JPA 시작**
==============

책에서는 이클립스로 하지만 이책의 마지막 예제가 스프링인만큼 미리 STS를 깔아서 시작하겠습니다.

IDE : [https://spring.io/tools/sts/all](https://spring.io/tools/sts/all)  
github : [https://github.com/holyeye/jpabook](https://github.com/holyeye/jpabook)  
H2 DB : [http://www.h2database.com/html/download.html](http://www.h2database.com/html/download.html)  
JDK : [http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

JDK 가 없으신분들은 JDK 를 다운로드 받아서 설치 합니다.

IDE를 다운로드 받아서 압축을 해제 한 후

![](/extendedFile/jpa1.png)

퍼시펙티브에서 GIT를 열어줍니다.

![](/extendedFile/jpa2.png)

![](/extendedFile/jpa3.png)

![](/extendedFile/jpa4.png)

![](/extendedFile/jpa5.png)

![](/extendedFile/jpa6.png)

메이븐 프로젝트로 추가 하면 됩니다.

그 후 H2 DB를 인스톨 한 후 H2 Consol 을 실행 합니다.

![](/extendedFile/jpa7.png)

![](/extendedFile/jpa8.png)

![](/extendedFile/jpa9.png)

![](/extendedFile/jpa10.png)

![](/extendedFile/jpa11.png)

![](/extendedFile/jpa12.png)

![](/extendedFile/jpa13.png)

셋팅을 완료 후 Crtl \+ F11 키를 눌러서 실행 하여 콘솔창에 실행 된 예제를 확인 하실 수 있습니다.

아래의 예제 프로젝트 목록에서 공부 하고 싶은 부분의 프로젝트를 보면서 공부 하면 좋을거 같습니다.  
github : [https://github.com/holyeye/jpabook](https://github.com/holyeye/jpabook)

구분

예제

설명

시작하기

ch02-jpa-stat1

JPA시작

 

ch04-jpa-stat2

JPA 시작 예제에 매핑 추가

도메인 모델 설계

ch04-model1

테이블과 엔티티 기본 매핑

 

ch05-model2

일대다, 다대일 연관관계 매핑

 

ch06-model3

일대일, 다대다 연관관계 매핑

 

ch07-model4

상속 관계 매핑

 

ch08-model5

지연 로딩, 영속성 전이 설정

 

ch09-model6

값 타입 매핑

활용

ch11-jpa-shop

JPA와 스프링 프레임워크를 사용해서 실제 동작하는 웹 애플리케이션 개발

 

ch12-springdata-shop

앞 예제에 스프링 데이터 JPA와 QueryDSL을 추가

#### JPA 시작 정리

JPA를 사용하기 위한 개발 환경을 설정하고, JPA를 사용해서 객체 하나를 테이블에 등록/수정/삭제/조회하는 간단한 애플리케이션을 만들어 보았다. JPA가 반복적인 JDBC API와 결좌 값 매핑을 처리해준 덕분에 코드량이 상당히 많이 줄어든 것은 물론이고 심지어 SQL도 작성할 필요가 없었다. 하지만 코드량을 줄이고 SQL을 자동 생성하는 것은 JPA가 제공하는 전체 기능 중 일부에 불과하다. 다음 장을 통해 JPA의 핵심 기능인 영속성 관리에 대해 알아보자.
