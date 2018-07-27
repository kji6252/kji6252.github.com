---
title: 프록시와 연관관계 관리
date: 2017-01-22 12:10:00
categories:
  - JPA
tags:
  - Java
  - JPA
  - ORM

---
* [프록시](https://ko.wikipedia.org/wiki/%ED%94%84%EB%A1%9D%EC%8B%9C_%ED%8C%A8%ED%84%B4) : 연관된 객체를 실제 사용하는 시점에 데이터베이스에서 조회 하는 기술
* 지연로딩: 연관된 객체를 실제 사용하는 시점에 불러 오는것
* 즉시로딩 : 연관된 객체를 조인을 통하여 함께 불러오는것
* 영속성 전이 : 연관된 객체를 함께 저장하거나 삭제
* 고아 객체 : 부모객체가 삭제시 홀로 남겨지는 객체

# 8.1 프록시

엔티티를 조회할 때 연관된 엔티티들이 항상 사용되는 것은 아니다.

JPA는 엔티티가 실제 사용될 때까지 데이터베이스 조회를 지연하는 방법을 제공하는데 이것을 지연 로딩이라 한다.

지연 로딩 기능을 사용하려면 실제 엔티티 객체 대신에 데이터베이스 조회를 지연할 수 있는 가짜 객체가 필요한데 이것을 [프록시](https://ko.wikipedia.org/wiki/%ED%94%84%EB%A1%9D%EC%8B%9C_%ED%8C%A8%ED%84%B4) 객체라 한다.
<!-- more -->
## 8.1.1 프록시 기초

```java
//즉시 로딩
Member member = em.find(Member.class, “member1”);

//지연 로딩
Member member = em.getReference(Member.class, “member1”);
```

em.getReference()  사용시 JPA는 데이터베이스를 조회하지 않고 실제 엔티티 객체도 생성하지 않는다. 대신에 데이터베이스 접근을 위임한 [프록시](https://ko.wikipedia.org/wiki/%ED%94%84%EB%A1%9D%EC%8B%9C_%ED%8C%A8%ED%84%B4) 객체를 반환한다.

![JPA_8_1.png](https://lh4.googleusercontent.com/TFbaSRwKdNOGcqXLzZbPwkziCRR20msoGXUZyBpaIYj-jFUgItX9nkPXRtTaK069VPtZUxX7gsiFDQM7C23UZEFD4IxCDsKeQin7eXOC0o3kBhvs39bgjT7zWONJbVrM_cll4o7N)

프록시 초기화

프록시의 특징

* 프록시 객체는 처음 사용할 때 한 번만 초기화된다.
* 프록시 객체를 초기화한다고 프록시 객체가 실제 엔티티로 바뀌는 것은 아니다. 프록시 객체가 초기화되면 프록시 객체를 통해서 실제 엔티티에 접근할 수 있다.
* 프록시 객체는 원본 엔티티를 상속받은 객체이므로 타입 체크 시에 주의해서 사용해야 한다.
* 영속성 컨텍스트에 찾는 엔티티가 이미 있으면 데이터베이스를 조회할 필요가 없으므로 em.getReference()를 호출해도 프록시가 아닌 실제 엔티티를 반환한다.
* 초기화는 영속성 컨텍스트의 도움을 받아야 가능하다. 따라서 영속성 컨텍스트의 도움을 받을 수 없는 준영속 상태의 프록시를 초기화하면 문제가 발생한다. 하이버네이트는 org.hibernate.LazyInitializationException예외를 발생시킨다.

## 8.1.2 프록시와 식별자

프록시는 식별자 값을 가지고 있으므로 식별자 값을 조회해도 초기화하지 않는다 엔티티 접근 방식 설정으로 초기화 유무를 결정 할 수 있다.

@Access(AccessType.PROPERTY) : 식별자(getID())메소드 호출시 초기화 하지 않음

@Access(AccessType.FIELD)  : 식별자(getID())메소드 호출시 초기화 함

8.1.3 프록시 확인

JPA가 제공하는 PersistenceUnitUtil.isLoaded(Object Entity) 메소드를 사용하면 프록시 인스턴스의 초기화 여부를 확인할 수 있다.

```java
em.getEntityManagerFactory()
.getPersistenceUnitUtil().isLoaded(entity);
```

# 8.2 즉시 로딩과 지연 로딩

즉시 로딩(EAGER) : 연관된 엔티티를 즉시 조회한다. 하이버네이트는 가능하면 SQL 조인을 사용해서 한 번에 조회한다. @ManyToOne(fetch=FetchType.EAGER)

지연 로딩(LAZY) : 연관된 엔티티를 프록시로 조회한다. 프록시를 실제 사용할 때 초기화하면서 데이터베이스를 조회한다. @ManyToOne(fetch=FetchType.LAZY)

## 8.2.1 즉시 로딩

대부분 JPA 구현체는 즉시 로딩을 최적화하기 위해 가능하면 조인 쿼리를 사용한다.

NULL제약 조건에 따라 내부 조인(INNER JOIN)이나 외부 조인(LEFT OUTER JOIN)을 사용

* @JoinColunm(nullable=true) : NULL 허용(기본값), 외부 조인 사용
* @JoinColunm(nullable=false) : NULL 허용하지 않음, 내부 조인 사용
* 또는 @ManyToOne(fetch=FetchType.EAGER, optional=false)

## 8.3.2 JPA 기본 패치 전략

fetch 속성의 기본 설정값은 다음과 같다.

@ManyToOne, @OneToOne : 즉시 로딩(FetchType.EAGER)

@OneToMany, @ManyToMany : 지연 로딩(FetchType.LAZY)

JPA의 기본 페치 전략은 연관된 엔티티가 하나면 즉시 로딩을, 컬렉션이면 지연 로딩을 사용 한다. 컬렉션을 로딩하는 것은 비용이 많이 들고 잘못하면 너무 많은 데이터를 로딩할 수 있기 때문이다.

## 8.3.3 컬렉션에 FetchType.EAGER 사용시 주의점

* 컬렉션을 하나 이상 즉시 로딩하는 것은 권장하지 않는다.
* 컬렉션 즉시 로딩은 항상 외부 조인(OUTER JOIN)을 사용한다.
* @ManyToOne, @OneToOne
    * (optional=false) : 내부 조인
    * (optional=true) : 외부 조인
* @OnetoMany, @ManyToMany
    * (optional=false) : 외부 조인
    * (optional=true) : 외부 조인

일대다 다대다시엔 값이 없을경우도 조회를 해야 해서 무조건 외부조인으로 가져온다.

# 8.4 영속성 전이: CASCADE

특정 엔티티를 영속 상태로 만들 때 연관된 엔티티도 함께 영속 상태로 만들고 싶으면 영속성 전이(transitive persistence)기능을 사용하면 된다.

## 8.4.1 영속성 전이: 저장

```java
@OneToMany(mappedBy=”parent”, cascade=CascadeType.PERSIST)
```

부모를 영속화할때 연관된 자식들도 함께 영속화하라고 cascade=CascadeType.PERSIST 옵션을 설정했다.

```java
//영속성 전이:저장X
em.persist(parent);

//연관관계 매핑 코드
em.persist(child1);

//연관관계 매핑 코드
em.persist(child2);
```

```java
//영속성 전이: 저장
//child와 parent연관관계 추가
em.persist(parent);
```

![JPA_8_2.png](https://lh6.googleusercontent.com/leZt4Zl1Dt8a658-c-AcYyjn395VqESdyuAumv5PcKhq-NhNE7R5MiovP1Dh_XtgW6SfWT5Gk5ZUOQNZEmL-pQ89kTKpEbe5nJX5YSIMmuropAZswPhr6n9H-OZlL8aGiSQgDkYo)

CASCADE 실행

```java
//영속성 전이: 삭제X
em.remove(findChild1);
em.remove(findChild2);
em.remove(findParent);
```

```java
//영속성 전이: 삭제
em.remove(findParent);
```
  
 

엔티티를 영속화 하거나 제거 시 연관된 엔티티도 같이 처리 하는 편리함을 제공 한다.

## 8.4.3 CASCADE의 종류

```java
public enum CascadeType{
ALL, //모두 적용
PERSIST, //영속
MERGE, //병합
REMOVE, //삭제
REFRESH, //REFRESH
DETACH //DETACH
}
```
# 8.5 고아 객체(ORPHAN)

JPA는 부모 엔티티와 연관관계가 끊어진 자식 엔티티를 자동으로 삭제하는 기능을 제공하는데 이것을 고아 객체 제거라 한다.

```java
@OneToMany(mappedBy=”parent”, orphanRemoval=true)
```

orphanRemoval=true 을 설정하면 사용 가능 하다.

```java
Parent parent1 = em.find(Parent.class, id);

//한개만 제거
parent1.getChildren().remove(0); //자식 엔티티를 컬렉션에서 제거

//모두 제거
parent1.getChildren().clear();
```

출처 : 자바 ORM 표준 JPA 프로그래밍 김영한
