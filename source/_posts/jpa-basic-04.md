---
title: 연관관계 기초
date: 2017-01-15 09:14:00
categories:
  - JPA
---
**객체의 참조와 테이블의 외래 키를 매핑하는 것이 이 장의 목표다.**

#### **핵심 키워드**

*   **방향(Direction): \[단방향, 양방향\]이 있다. 한 쪽만 참조하는 것을 단방향 관계라 하고, 양쪽 모두 서로 참조하는 것을 양방향 관계라 한다. 방향은 객체관계에만 존재하고 테이블 관계는 항상 양방향이다.**
    
*   **다중성(Multiplicty): \[다대일(N:1), 일대다(1:N), 일대일(1:1), 다대다(N:M)\] 다중성이 있다.**
    
*   **연관관계의 주인(Owner): 객체를 양방향 연관관계로 만들면 연관관계의 주인을 정해야 한다.**
    

### **5.1 단방향 연관관계**

**![JPAEx5.png](https://lh3.googleusercontent.com/tsFHJw7DMbEwVx5FW6vnITNwv50vgWy3ZfSIvn6y4RLHDpZhf4Sjo9WUt-JqBJJt0iSm-RxLDe82Hi5nJ9Wg25oocilkdCUJETUn1WXPgG_djddhrulrVu5SKAqjkfPl3k4Wygce)**

*   **객체 연관관계 : 회원 객체는 Member.team 필드(멤버변수)로 팀 객체와 연관관계를 맺는다. (단방향)**
    
*   **테이블 연관관계 : 회원 테이블은 TEAM_ID 외래 키로 팀 테이블과 연관관계를 맺는다. (양방향)**
    

#### **객체 연관관계와 테이블 연관관계의 가장 큰 차이**

**참조를 통한 연관관계는 언제나 단방향이다. 객체간에 연간관계를 양방향으로 만들고 싶으면 반대쪽에도 필드를 추가해서 참조를 보관해야 한다. 결국 연관관계를 하나 더 만들어야 한다. 이렇게 양쪽에서 서로 참조하는 것을 양방향 연관관계라 한다. 하지만 정확히 이야기하면 이것은 양방향 관계가 아니라 서로 다른 단방향 관계 2개다. 반면에 테이블은 외래 키 하나로 양방향으로 조인할 수 있다.**

### **5.1.3 객체 관계 매핑**

**![JPAEx5_2.png](https://lh3.googleusercontent.com/LWQnn2t9XiTo3s50XQflfgaI9B7E2OLoAPa0EsjeagvTCE6PjJJPNd5an4J9M52jtbamTVvZKT1llzxGTF9xdzwoUgTskIUzUVkq2fXjMDdFeVrA4sjAI7gsedrZ6wOtGkCieeYC)**

**![](https://lh6.googleusercontent.com/L5TGN1r-Or_T4pR2vmq0mBuYU5p3-8ThfT3HlaCHesUQBQWInBv4pV5McTSEQA8zRLYlm3h3dICuB3Zh2TdXhSr0x2cRuumbPUDD_Q_amhj3hWu7AmNQsRyIENUUShArQ0hqfDYi)**

**![](https://lh5.googleusercontent.com/y_98NYwiMx3pdv1u2wvWtYPPaH9eUeD2cFcWRqk3aVpYUEmEZp9vYUia2p2vK-86KSoWmctsDErG2XXzopNNTXxi2ZdW3f5F2b9EwU1HTDa5G_8y5hgP8biXQNpfpRL97qgD_nNd)**

*   **객체 연관관계: 회원 객체의 Member.team 필드 사용**
    
*   **테이블 연관관계: 회원 테이블의 MEMBER.TEAM_ID 외래 키 컬럼을 사용**
    
*   **@ManyToOne: 이름 그대로(N:1) 관계라는 매핑 정보다. 회원과 팀은 다대일 관계다. 연관관계를 매핑할 때 이렇게 다중성을 나타내는 어노테이션을 필수로 사용해야 한다.**
    
*   **@JoinColumn: 조인 컬럼은 외래 키를 매핑할 때 사용한다. name 속성에는 매핑할 외래 키 이름을 지정한다. 회원과 팀 테이블은 TEAM_ID 외래 키로 연관관계를 맺으므로 이 값을 지정하면 된다. 이 어노테이션은 생략할 수 있다.**
    

### **5.3 양방향 연관관계**

**![JPAEx5_3.png](https://lh6.googleusercontent.com/aCeR3Jrxq3Sd5B0hS-tgodsmKRi059sZ87CvdWL4M3ZSlv5tqbir_LWpBzu-qW9mPfN5C9IIT11FWv8cDlQzmvu8z5NUkK14JfICWqXvL7kTMruxqeMLN1k7rk0eOWsOlAWhGQcS)**

**단방향 연관관계에서 Team 객체에 List members를 추가 하였다.**

**![](https://lh5.googleusercontent.com/uqAY0CC6EHRRtWxO21DOJxbMJOjMTNPLcgHKpx1iqTpBR5D7qu2g5Mz8OHRo6KkX9olYlf8mwP5MG4VGqMvVYFAS_G-_RVE1inCzTlfBCdPbMxWIySH1NGI_9BL4nVsGaBQOJOJg)**

**Member에서는 @ManyToOne을 했으므로 반대편인 Team에서는 @OneToMany를 주어 양방향 연관관계를 지정 하였다.**

**엄밀히 이야기하면 양방향 연관관계 라는 것은 없다. 서로 다른 단방향 연관관계 2개를 잘 묶어 양방향인 것처럼 보이게 할 뿐이다.**

**엔티티를 양방향 연관관계로 설정하면 객체의 참조는 둘인데 외래 키는 하나다. 따라서 둘 사이에 차이가 발생한다.**

**두 객체 연관관계 중 하나를 정해서 테이블의 외래 키를 관리해야 하는데 이것을 연관관계의 주인 이라 한다.**

#### **연관관계 주인에 대해**

*   **연관관계의 주인이 아닌쪽에 mappedBy 속성을 넣어줘서 주인이 아님을 표시 하면 된다.**
    
*   **연관관계의 주인은 외래키를 관리 하며 등록,수정,삭제가 가능하고 아닌쪽은 읽기만 가능하다.**
    

**기능\\연관관계**

**주인**

**주인X**

**읽기**

**O**

**O**

**등록,수정,삭제**

**O**

**X**

**외래키**

**O**

**X**

#### 참고

**데이터베이스 테이블의 다대일, 일대다 관계에서는 항상 다 쪽이 외래 키를 가진다. 다 쪽인 @ManyToOne은 항상 연관관계의 주인이 되므로 mappedBy를 설정할 수 없다. 따라서 @ManyToOne에는 mappedBy 속성이 없다.**

#### 연관관계 기초 정리

**양방향의 장점은 반대방향으로 객체 그래프 탐색 기능이 추가된 것뿐이다.**

*   단방향 매핑만으로 테이블과 객체의 연관관계 매핑은 이미 완료 되었다.
*   단방향을 양방향으로 만들면 반대방향으로 객체 그래프 탐색 기능이 추가된다.
*   양방향 연관관계를 매핑하려면 객체에서 양쪽 방향을 모두 관리해야 한다.

**출처 : 자바 ORM 표준 JPA 프로그래밍 김영한**
