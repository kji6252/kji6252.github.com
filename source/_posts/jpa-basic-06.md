---
title: 고급 매핑
date: 2017-01.17 10:58:00
categories:
  - JPA
---
*   **상속 관계 매핑: 객체의 상속 관계를 데이터베이스에 어떻게 매핑하는지 다룬다.**
    
*   **@MappedSuperclass: 등록일, 수정일 같이 여러 엔티티에서 공통으로 사용하는 매핑 정보만 상속받고 싶으면 이 기능을 사용하면 된다.**
    
*   **복합 키와 식별 관계 매핑: 데이터베이스의 식별자가 하나 이상일 때 매핑하는 방법을 다룬다. 그리고 데이터베이스 설계에서 이야기하는 식별 관계와 비식별 관계에 대해서도 다룬다.**
    
*   **조인 테이블: 테이블은 외래 키 하나로 연관관계를 맺을 수 있지만 연관관계를 관리하는 연결 테이블을 두는 방법도 있다. 여기서는 이 연결 테이블을 매핑하는 방법을 다룬다.**
    
*   **엔티티 하나에 여러 테이블 매핑하기: 보통 엔티티 하나에 테이블 하나를 매핑하지만 엔티티 하나에 여러 테이블을 매핑하는 방법도 있다. 여기서는 이 매핑 방법을 다룬다.**
    

### ******7.1 상속관계 매핑******

******![JPA_Ex7_1.png](https://lh3.googleusercontent.com/3mNucKokBmtY-H9PpW0600QFxX2lxXfegLTjVxWKB9N6riIimJSni0It0qCnSLNEEZ1DgeOHWlj06RNObNyp-iZf-IA6E_e7e1j4o2s7BfFhUj6XIo_yufU5TEsngeBZqxJLE1xC)******

******객체 상속 모델******

******JPA에서는 상속관계를 총 3가지로 제공******

*   ******조인 전략 : @Inheritance(strategy=InheritanceType.JOINED)******
*   ******단일 테이블 전략 : @Inheritance(strategy=InheritanceType.SINGLE_TABLE)******
*   ******구현 클래스마다 테이블 전략 : @Inheritance(strategy=InheritanceType.TABLE\_PER\_CLASS)******

#### ******조인 전략******

******![JPA_Ex7_2.png](https://lh3.googleusercontent.com/qhkotbW50hmApzamYVeWxxluUd5CUwUb64sFKze6ddIGLtwEXpQAARfDure2sNzIVatLwm0QRbNuqqxNkzdBLTBnzR4QCxlCINWg-T9DYFYkaJ_XmAgmUrZaMZRmmLe-VH8qoxMF)******

******![](https://lh6.googleusercontent.com/T5atnTM9sbabH_-mrJK1UQjHM_ZQfkXVCQRNCwjrh7GH8NHLdu4_uyirJCjpSxCY0lQMOXt-S4mg1ePC84trF6Vq2ZWEz5VT1446X3vPEHuYo9g5N28P_J2P-jNE8rdunOI8ZySH)******

******![](https://lh5.googleusercontent.com/orXf3maC0IxF-yGh7i_kDEsG6SL0k0QlIdYlqYxihiRvyxiG2IrvR9gBn-BDhQSViegSff1JlSEUvpSa7dIwcRuRnyuRiUaNbLBzq0ItbnWZKFCYc7wlmOLSne6GV-kIUKW7P_XH)******

******![](https://lh4.googleusercontent.com/zY8uB7N_1z8gxJ6oAbYrZRb35B7nA-KlH1J9WzAJ_vUt_stGwb7kG_D3_i0vOOZNe3_fz7EkOcg17I6qUowAwSQoxpPw7_UXCtMCqtIBLjFeAzPq2-udjB021Wj9rGT-7XHGZavz)******

******![](https://lh5.googleusercontent.com/P81lE4xCJuzQaN5v5Xg-VBnMJn3K64t_HAW0MA7Acb0iJXiItk4x0g7sUk7oGCuMVe76t_tBdQM3X7oNzW1X5HP9Zj23EECG65PoIVSep_IyMO3ID8rotRDKzBQA_-JkABMwCDMX)******

******부모 테이블의 기본 키를 받아서 기본 키 \+ 외래 키로 사용하는 전략******  
******객체는 타입이 있지만 테이블은 없기에 DTYPE 이라는 컬럼을 구분 컬럼으로 사용해야함******

#### ******단일 테이블 전략******

******![JPA_Ex7_3.png](https://lh3.googleusercontent.com/BL90rKP26Z-pOloh-8ov-nrHPWs_vxEnn-Qs0wqfUeh7fPOZYn7IPbn1Z5YK4741_VYJ0Fh99aydF8AFYEihZVoSzlZ2s_W6TmiDc30syIK2zNOS8obOnLOLRHKQMvS3PYCXhjL5)******

******![](https://lh3.googleusercontent.com/GPuTuXo48Qa7u9wQQevvc5gr35aPbxTG1XSS70b09iKcISNMDQzyiFW3vIB7oEm2eF3FoGZjV9U1y6e2X_k9jdhG9n7uFdVxXqz7EuT8vZPGwicSyJgFWj_gftlWUXU9tMRN84DO)******

******![](https://lh5.googleusercontent.com/orXf3maC0IxF-yGh7i_kDEsG6SL0k0QlIdYlqYxihiRvyxiG2IrvR9gBn-BDhQSViegSff1JlSEUvpSa7dIwcRuRnyuRiUaNbLBzq0ItbnWZKFCYc7wlmOLSne6GV-kIUKW7P_XH)******

******![](https://lh4.googleusercontent.com/zY8uB7N_1z8gxJ6oAbYrZRb35B7nA-KlH1J9WzAJ_vUt_stGwb7kG_D3_i0vOOZNe3_fz7EkOcg17I6qUowAwSQoxpPw7_UXCtMCqtIBLjFeAzPq2-udjB021Wj9rGT-7XHGZavz)******

******![](https://lh5.googleusercontent.com/P81lE4xCJuzQaN5v5Xg-VBnMJn3K64t_HAW0MA7Acb0iJXiItk4x0g7sUk7oGCuMVe76t_tBdQM3X7oNzW1X5HP9Zj23EECG65PoIVSep_IyMO3ID8rotRDKzBQA_-JkABMwCDMX)******

******전략을 싱글테이블로 바꾸면된다.******

******![](https://lh4.googleusercontent.com/7zgeTIdiAThVeKkCAGHOzniVHvqP2nGOIBxrqkV6ovjGLjy3Xyby40gAuAN_0lZDjufszlFK5J5Ent-HVxfmxIWCWmW9Ia_aoHE_t_rqaPQxUWt2h5Ur20YWUOawjQByexwDiYqH)******

******추가로 자식엔티티에서 기본키 칼럼명이 다르면 @PrimaryKeyJoinColumn을 쓴다.******

#### ******구현 클래스마다 테이블 전략******

******![JPA_Ex7_4.png](https://lh3.googleusercontent.com/7qkqhiBRjOuzIjb11X6Qp6OPt7w6bkMCEZFhBHOYVLquDPjW14nWoX0OVTsby8Cc_xN9grBcCUWi1p9fh3pqYqujYiYDQDhmmxt9ZcOCoYDoN8KlHW4j4qAhsPThOvLjVSVsXt3u)******

******![](https://lh3.googleusercontent.com/ZSxzpRR2wwkgIOMA9LNFhtMLNFNkuxK1hNCWGivRetqV5xWQhyf65vahnE_8UH0Rqyqc9T1SMpRvQBC2hUARtI43_M7z9zWFEXRyjkSqEZmn2clCBPOOr95xes1Pug-WSc5pj_dQ)******

******![](https://lh3.googleusercontent.com/ASEnoYzIbhfryNr3dDgopQP4DDvTrpa4b4m0X-lJSkX-TAeQGLvwQsWuDbhowgoMSEwcUNIjZZH0lQHqxn0FszT4hGntuh7WBpt2g65XsJNKHQs-qZ-oJ2QJJD26X71TE3lsnoE3)******

******![](https://lh3.googleusercontent.com/3xMJj7zH4ao41IpcRZFZkHBGQRH0cfzrrjaE1ZdN_RQgiVb3N4H5muEpMlGySIkBOGPWLXjcKu8Tc7b-KTkskreZJkKIoSTscbmNBv5oLESMJgL3GIx_Nl72ukl6M8HgQOekm6Ck)******

******![](https://lh6.googleusercontent.com/BlvJM-OyrB9l7DuYzomKnMSLPlGQyY_rM4QHLQyVgaVPY8DuBWv5aVOJjp-HorNyvldGGYtg1Asn4wkRZjw3lOSmpHq0t052y3aV7CrzcozceQH5ACX7IZhD81x0q5KFfdB58bQf)******

******이전략은 이름도 길어서 제일 안쓸거 같다.. 책에서는 데이터베이스 설계자와 ORM 전문가 둘 다 추천하지 않은 전략이라고 함******

### ******7.2 @MappedSuperclass******

******7.1에선 테이블과의 상속관계를 다뤘는데 이건 순수히 객체의 상속만을 할땐 @MappedSuperclass를 씀 추상 클래스와 비슷하다고 생각하면 됨******

******![Copy of Untitled Diagram.png](https://lh5.googleusercontent.com/Dk8hGT_YGKzn7zKWLOWBsuID4F0iaG4MeRSvvwu1278cWQVtlQ_bTUfmrxqb2QN5JqH3wYLAevw-g-sGNNXW5dE0Kn8p-C4acNwLK7TESbu-4ZQJLca0JAIdULKrFdB8fWHbLpye)******

[?](#)

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

`@MappedSuperclass`

`public` `class` `BaseEntity {`

`@Id` `@GeneratedValue`

`private` `Long id;`

`private` `String name;`

`}`

`@Entity`

`public` `class` `Member` `extends` `BaseEntity {`

`//ID 상속`

`//NAME 상속`

`private` `String email;`

`}`

`@Entity`

`@AttributeOverride``(name=``"id"``, column=``@Column``(``"MEMBER_ID"``))`

`public` `class` `Seller` `extends` `BaseEntity {`

`//ID 상속`

`//NAME 상속`

`private` `String shopName;`

`}`

[?](#)

1

2

3

`@AttributeOverride`

`@AttributeOverrides`

******어노테이션을 통해 상속받은 칼럼명을 재정의 할수도 있음.******

### ******7.3 복합 키와 식별 관계 매핑******

******![JPA_7_6.png](https://lh4.googleusercontent.com/AjeFwgRZIzKPOtTUU7BA4c4XslYOYtKyi31Ds_pr4K5rQi6VmzMR4V6ajzSzAeUr4rhy3CzEJt7AQ90gUylMTi7oA6Y-f1sJYgpMtnazY_Ox9dJfbfTkYLxlKQgf6Jwbwo-xEjpo)******

******식별 관계******

******![JPA_7_7.png](https://lh3.googleusercontent.com/P5JfoFJHZTQPIoaX8QVyQVLG0ZSAfaenz9rFNO-6imhLHct1Z0PXOHmtCWex9EJEDEt42KXV-BIVKEz_VtmtCdtQalw5ufH7DW3nWAIb9wawTGmfVEjYeyj_5dNpqoCcur2FWXR4)******

******비식별 관계******

******@IdClass와 @EmbeddedId 방식 2가지가 존재 한다.******

******@IdClass는 테이블 친화적이고 @EmbeddedId는 객체 친화적******

[?](#)

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

25

26

27

28

29

30

31

32

33

34

35

36

37

38

39

40

41

42

43

44

45

46

47

48

49

50

51

52

`식별관계 IdClass`

`@Entity`

`public` `class` `Parent {`

`@Id` `@Column``(name=``"PARENT_ID"``)`

`private` `String id;`

`private` `String name;`

`}`

`@Entity`

`@IdClass``(ChildId.``class``)`

`public` `class` `Child{`

`@Id`

`@ManyToOne`

`@JoinColumn``(name=``"PARENT_ID"``)`

`public` `Parent parent;`

`@Id` `@Column``(name=``"CHILD_ID"``)`

`private` `String ChildId;`

`private` `String name;`

`}`

`//자식ID`

`public` `class` `ChildId` `implements` `Serializable{`

`//Child.parent 매핑`

`private` `String parent;`

`//Child.childId 매핑`

`private` `String childId;`

`//equals, hashcode`

`}`

`@Entity`

`public` `class` `GrandChild{`

`@Id`

`@ManyToOne`

`@JoinColumns``({`

`@JoinColumn``(name=``"PARENT_ID"``)`

`,``@JoinColumn``(name=``"CHILD_ID"``)`

`})`

`private` `Child child;`

`@Id` `@Column``(name=``"GRANDCHILD_ID"``)`

`private` `String id;`

`private` `String name;`

`}`

`//손자 ID`

`public` `class` `GrandChildId` `implements` `Serializable{`

`//GrandChild.child 매핑`

`private` `ChildId child;`

`//GrandChild.id 매핑`

`private` `String Id;`

`//equals, hashcode`

`}`

[?](#)

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

25

26

27

28

29

30

31

32

33

34

35

36

37

38

39

40

41

42

43

44

45

46

47

48

49

50

51

52

53

54

`식별관계 EmbeddedId`

`@Entity`

`public` `class` `Parent {`

`@Id` `@Column``(name=``"PARENT_ID"``)`

`private` `String id;`

`private` `String name;`

`}`

`@Entity`

`public` `class` `Child{`

`@EmbeddedId`

`private` `ChildId id;`

`//ChildId.prentId 매핑`

`@MapsId``(``"prentId"``)`

`@ManyToOne`

`@JoinColumn``(name=``"PARENT_ID"``)`

`public` `Parent parent;`

`private` `String name;`

`}`

`//자식ID`

`@Embeddable`

`public` `class` `ChildId` `implements` `Serializable{`

`//@MapsId("parentId")로 매핑`

`private` `String parentId;`

`@Column``(name=``"CHILD_ID"``)`

`private` `String id;`

`//equals, hashcode`

`}`

`@Entity`

`public` `class` `GrandChild{`

`@EmbeddedId`

`GrandChildId id;`

`//GrandChildId.childId 매핑`

`@MapsId``(``"childId"``)`

`@ManyToOne`

`@JoinColumns``({`

`@JoinColumn``(name=``"PARENT_ID"``)`

`,``@JoinColumn``(name=``"CHILD_ID"``)`

`})`

`private` `Child child;`

`private` `String name;`

`}`

`//손자 ID`

`@Embeddable`

`public` `class` `GrandChildId` `implements` `Serializable{`

`//@MapsId("childId") 매핑`

`private` `ChildId childId;`

`@Column``(name=``"GRANDCHILD_ID"``)`

`private` `String Id;`

`//equals, hashcode`

`}`

[?](#)

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

25

26

27

28

29

30

31

32

33

34

35

36

`비식별 관계`

`@Entity`

`public` `class` `Parent {`

`@Id` `@GeneratedValue`

`@Column``(name=``"PARENT_ID"``)`

`private` `Long id;`

`private` `String name;`

`}`

`@Entity`

`public` `class` `Child{`

`@Id` `@GeneratedValue`

`@Column``(name=``"CHILD_ID"``)`

`private` `Long id;`

`//ChildId.prentId 매핑`

`@ManyToOne`

`@JoinColumn``(name=``"PARENT_ID"``)`

`public` `Parent parent;`

`private` `String name;`

`}`

`@Entity`

`public` `class` `GrandChild{`

`@Id` `@GeneratedValue`

`@Column``(name=``"GRANDCHILD_ID"``)`

`private` `Long id;`

`@ManyToOne`

`@JoinColumn``(name=``"CHILD_ID"``)`

`private` `Child child;`

`private` `String name;`

`}`

******식별 관계인 경우는 복합키가 필요함으로 키관련 클래스들도 생성해야 하지만 비식별관계는 키가 1개임으로 복합키클래스를 만들 필요가 없다.******

******참고로 키가 1개일 경우만 @GeneratedValue 를 사용할수 있다.******

******책에서는 비식별 관계를 사용하고 기본 키는 LONG 타입의 대리 키를 사용 하는것이 좋다고 소개 되어있습니다. 그 이유는 비즈니스와 관련이 없어 변경시에 유연한 대처가 가능 Long 타입의 경우 약 920경의 숫자를 담을수 있음.******

******나머지 조인테이블과 엔티티 하나에 여러 테이블 매핑이 있지만 비주류라서 소개 하지 않겠습니다.******

**출처 : 자바 ORM 표준 JPA 프로그래밍 김영한**
