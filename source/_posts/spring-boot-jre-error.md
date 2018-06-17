---
title: 스프링부트 jre 2개 추가 오류
date: 2016-06-12 05:42:00
categories:
  - 스프링
---
![](/extendedFile/201606121433.png)

최근에 스프링 부트 그래들 프로젝트를 생성시에 jre 2개가 잡히는 문제가 발생하였습니다.

그래서 jdk를 지웠다 다시 설치 해보기도 하였으며 결국 sts를 지우고 다시 깔았지만 동일한 현상이 지속되었습니다.

그러던중 .classpath에 들어가서 확인해보니 자바 라이브러리를 불러오는 부분에서

[?](#)

1

2

`<``classpathentry` `kind``=``"con"` `path``=``"org.eclipse.jdt.launching.JRE_CONTAINER/org.eclipse.jdt.internal.debug.ui.launcher.StandardVMType/JavaSE-1.8"``/>`

`<``classpathentry` `kind``=``"con"` `path``=``"org.eclipse.jdt.launching.JRE_CONTAINER/org.eclipse.jdt.internal.debug.ui.launcher.StandardVMType/JavaSE-1.8/"``/>`

맨뒤 / 가 있고 없는 차이가 있길래 build.gradle에 들어가 이클립스 클래스 패스 설정해주는 부분에 /를 삽입하고 난 뒤 Refresh All 을 하였습니다.

![](/extendedFile/201606121441.png)

jre가 2개 에서 1개로 바뀌었습니다. ㅎ_ㅎ
