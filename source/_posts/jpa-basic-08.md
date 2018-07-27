---
title: 값 타입
date: 2017-01-23 09:30:00
categories:
  - JPA
tags:
  - Java
  - JPA
  - ORM

---
* 기본값 타입basic value type
    * 자바 기본 타입(예: int, double)
    * 래퍼 클래스(예: Integer)
    * String
* 임베디드 타입embedded type(복합 값 타입)
* 컬렉션 값 타입collection value type

# 복합 값 타입

![](https://lh6.googleusercontent.com/cFKZlL4JNdKV7OOHodNXWvVThMwQcfglx_M-_NGNV9w_jhBTsoUNteIPJuzfJUKELdLIB-es0t3LAPabcv5EFwKrPHO66R7FxMV8ZtAHZtTf7Da5aQpDcyNgw0qYKa7TIUuu78Ml)

복합값 정의 : @Embeddable 어노테이션으로 정의
<!-- more -->
![](https://lh5.googleusercontent.com/zjMyPnfvziOQPVFFBUa6akdvuvQolEpd7DPYtacMSejuRFbCuQyz80J-Ha7mFq8eMXXTk2dr6XnxvyA_MXjvXABJP2b1vCwwhfCskB1aJVUOgcg9v3xoanl36bz9X-k4N6uO4F1D)

복합값 적용 : 값으로만 사용시엔 @Embedded로  키로 사용할땐 @EmbeddedID로 사용

![](https://lh3.googleusercontent.com/ybiWfXUO5CAB6ysY_2US_fsWyn7QHbuDiXXlVSFcIgcvjvD4YUWFKkhWmRqKzgEHBJvl31u3doSa8azuk3bkZ4hGPGdjNS66m_JKAT_1s0VDH04a9LKGr08bw-IJkUobPSCZkWmI)

    임베디드 타입과                                                 테이블 매핑

![](https://lh4.googleusercontent.com/sVtWfNrR6NvI72i4S_6JTY_fHU0kpOiFotaUpWMJaIFkZTgopEx5OMF9GWueY7dUo5U99B1BAdkz0tf1PaiN2R8umbfJTwciGB_-76mcIO1ksJWXfgjwJIu7dbTar-ndBBCscEMZ)

![](https://lh6.googleusercontent.com/riGO3K6RQLfVbmy5Y_jFy4DeIc-2jjDJZuGCiJkfPMJw_VmYL5nK7QsHbQMqu_9QBGdPb83YrZYOxMDCwXnyGJU5tEM5sTzojTZZaFGVnYhEshl-Mr19sm8JNDJVXHMfyk_QmTBw)

@AttributeOverride를 통해 컬럼명 변경 가능

# 컬렉션 타입

![](https://lh5.googleusercontent.com/0kvuvVZUu3ZYD9KskRfjFmEnQ_gOTXeuPTLSNb8UDqT5mMFmTQkkOabnAgBvt_5OKIbf7W2k-YqU1Flos34li8fJ_Tfku4BagglZiqsRMIXWAUiJUPpu-dCQ8n1VZMb1fCptpU2D)

![](https://lh5.googleusercontent.com/wWjtdic736w4ks-V-HNchKulPVo-bYPZrsz7YZmkn0SCyHl8MKT9oSlk5L0tkItVtLh5MBmY_yJoFjqhlhl8kPky1hCubI0Ncp8QpvyJ0Ze7aByiH6xtL6MISCtqUjqnVBmJ0Psz)

컬렉션 타입은 기본적으로 영속성 전이 \+ 고아 객체 제거기능을 필수로 가진다.
