---
title: 해외판 전자정부프레임워크? JHipster에 대해 알아 보자!
date: 2018-07-29 17:23:45
categories:
  - JHipster
tags:
  - JHipster
  - Java
  - Spring
---
# 개요
우리나라에서 공공기관과 민간기업에서 많이 사용하는 전자정부프레임워크가 있습니다. 업데이트도 느리거니와 생성도 불편하다고 생각 됩니다. 그에 반해 해외에서는 Yeoman을 가지고 쉽게 Spring Boot 개발 환경을 만들 수 있고 더불어 편한 유지 보수를 할 수 있게 도와주는 JHipster를 소개 합니다.

해외에서 자바 개발 플랫폼으로 핫한 프로젝트 입니다.

![제이힙스터깃허브](https://user-images.githubusercontent.com/6037055/43363798-c1e66ce4-9347-11e8-9c80-5d0f75f53d36.png)
<!-- more -->
다양한 기업들에서도 JHipster를 사용하고 있습니다.

![제이힙스터사용기업들](https://user-images.githubusercontent.com/6037055/43364341-4d914e8e-9353-11e8-8ea5-c0d427a04592.png)


프로젝트 셋팅부터 시작해서 귀찮은 일은 JHipster가 도 맡아 하고 개발자는 `비즈니스 로직에만 집중` 할 수 있습니다.

JHipster로 할 수 있는것

* Spring Boot + Angular/React 프로젝트
* UML을 통한 Entity+Controler+Service 자동 생성
* MSA 환경 구축
* Docker Image 생성
* Cloud와 통합 기능 제공(Kubernetis, Heroku, AWS 등)

이외에도 여러 오픈소스들을 사용할 수 있게 셋팅이 되어 있으며 입맛이 맞게 골라서 사용 하실 수 있습니다.

# 개인적으로 마음에 드는 부분
Spring Project들을 사용 하면서 공부 할 때 구조를 잘 잡는게 중요하다고 생각 됩니다. 물론 샘플 프로젝트만으로도 만족 할 수 있겠지만, 여러 프로젝트들을 융합 하였을때 복잡성이 증가하고 문맥과 명칭들이 뒤죽박죽 섞여 있어 통일성을 잃기 쉽습니다. 그래서 JHipster의 생성된 프로젝트를 봤을 때 깔끔한 설정과 generator를 사용 하여 일관된 개발을 할 수 있게 도와 줍니다.

# 소개
소개는

* JHipster란? With Sample Project
* JHipster와 생성 도구
* JHipster와 오픈소스
* JHipster MSA With Docker Compose

4 단계로 나눠서 소개를 할까 싶습니다.