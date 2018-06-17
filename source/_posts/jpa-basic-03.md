---
title: 엔티티 매핑
date: 2016-08-10 12:02:00
categories:
  - JPA
---
*   **객체와 테이블 매핑** : @Entity, @Table
*   **기본 키 매핑** : @Id
*   **필드와 컬럼 매핑** : @Column
*   **연관관계 매핑** : @ManyToOne, @JoinColumn

**@Entity(클래스)** : 테이블과 매핑할 클래스, JPA가 관리함

**@Table(클래스)** : 엔티티와 매핑할 테이블 (생략시 엔티티명으로 적용)

*   uniqueConstraints(DDL) : DDL생성시 유니크 제약조건 만듬.

**@Column(필드)** : 칼럼을 매핑한다.

*   **nullable(DDL)** : false 시 not null 기본값(true)
*   **length(DDL)** : 문자 길이 제약조건, String 타입에만 사용한다. 기본값(255)
*   **precision,scale(DDL)** : BigDecimal(BigInteger) 타입 사용 precision은 소수점 포함 전체길이, scale은 소수의 자릿수 double,float엔 적용 안됨

**@Enumerated(필드)** : 자바의 enum 타입을 매핑한다.

*   EnumType.ORDINAL enum 순서를 DB 저장 (0,1,2,3)
*   EnumType.STRING enum 이름을 DB 저장 (COUNT,ID,AGE)

**@Temporal(필드)** : 날짜 타입을 매핑한다.

*   TemporalType.DATE (yyyy-mm-dd)
*   TemporalType.TIME (HH-MM-ss)
*   TemporalType.TIMESTAMP (yyyy-mm-dd HH-MM-ss)

**@Lob(필드)** : BLOB, CLOB 타입을 매핑한다.(속성없이 자바타입으로 결정)

*   CLOB : String, char\[\], java.sql.CLOB
*   BLOB : byte\[\], java.sql.BLOB

**@Transient(필드)** : 특정 필드를 데이터베이스에 매핑하지 않는다.

**데이터베이스 스키마 자동 생성**
====================

persistence.xml 에 create, create-drop, update, validate, none 등의 값을 삽입 할수 있다.

개발이나 테스트에서 쉽게 디비스키마를 자동 생성할 수 있다.

[?](#)

1

`<``property` `name``=``"hibernate.hbm2ddl.auto"` `value``=``"create"``/>`

*   **create** : drop create 실행
*   **create-drop** : drop create drop 실행
*   **update** : 변경분만 적용 (테이블 추가, 칼럼추가, 제약조건 추가 등)
*   **validate** : 디비정보와 비교하여 다를시 프로그램 종료
*   **none** : 아무일도 하지 않음

[?](#)

1

`<``property` `name``=``"hibernate.ejb.naming_strategy"` `value``=``"org.hibernate.cfg.ImprovedNamingStrategy"``/>`

이 옵션 추가시 자바에선 카멜식 디비에선 언더스코어 표기법으로 매핑 된다.

#### 엔티티 매핑 정리

*   이 장을 통해 객체와 테이블 매피으 기본키 매핑, 필드와 컬럼매핑에 대해 알아보았다. 그리고 데이터베이스 스키마 자동 생성하기 기능도 알아보았는데, 이 기능을 사용하면 엔티티 객체를 먼저 만들고 테이블은 자동으로 생성할 수 있다.
*   JPA는 다양한 기본 키 매핑 전략을 지원한다. 기본 키를 애플리케이션에서 직접 할당하는 방법부터 데이터베이스가 제공하는 기본 키를 사용하는 SEQUENCE, IDENTITY, TABLE 전략에 대해서도 알아보았다.
*   이 장에서 다룬 회원 엔티티는 다른 엔티티와 관계가 없다. 회원이 특정 팀에 소속해야 한다면 어떻게 해야 할가? 다음 장을 통해 연관관계가 있는 엔티티들을 어떻게 매핑하는지 알아보자.
*   그 전에 다음 실전 예제를 꼭 따라해보자. 실전 예제는 이 장에서 학습한 내용을 소화할 수 있게 도와준다. 그리고 JPA를 사용해서 실제 엔티티를 어떻게 모델링해야 할지 감을 잡을 수 있게 해준다. 실전 예제의 도메인 모델은 각 장을 진행할 때마다 점진적으로 성장한다. 그리고 이렇게 완성한 도메인 모델로 11장의 웹 애플리케이션을 개발한다. 그러므로 실전 예제는 꼭 실행해보자.

출처 : 자바 ORM 표준 JPA 프로그래밍 (김영한)
