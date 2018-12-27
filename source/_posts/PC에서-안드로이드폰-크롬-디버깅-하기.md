---
title: PC에서 안드로이드폰 크롬 디버깅 하기
date: 2018-12-27 13:00:43
categories: Web
tags: Chrome, devtools, Android, Web Debug
---

# 개요
평소 Web개발을 하시는 분들은 빠른 속도와 편리한 도구들이 많은 Chrome devtools를 이용하여 개발 하게 됩니다. 

그중 모바일 페이지를 개발 할때 우리는 2가지 방법을 사용하게 됩니다.
![2018-12-27 1 18 05](https://user-images.githubusercontent.com/6037055/50465815-08b4cd80-09dd-11e9-9109-e64f6383950d.png)

1. devtools > Toggle device Toolbar
2. 크롬 확장 프로그램 `User-Agent Swicher`

위에 소개 된 방식 이외에도 devtools > Remote devicese를 사용 하면 자신의 안드로이드폰의 크롬App을 PC에서 디버깅을 할 수 있습니다.
<!-- more -->
# 준비 할것

USB 디버깅 활성화 된 안드로이드폰, PC와 연결할 USB케이블, PC

> USB 디버깅 활성은 안드로이드폰 개발자 옵션 활성 후 `개발자 옵션 > USB 디버깅`을 활성 하시면 됩니다.

# 사용 방법

![PC Connected Android Phone](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/imgs/remote-debugging.png)
안드로이드폰과 USB케이블을 PC에 연결을 합니다.

`크롬 > devtools > ⋮(More Options) > more Tools > Remote devices` 로 실행 하면 됩니다.

![2018-12-27 2 23 35](https://user-images.githubusercontent.com/6037055/50466872-33098980-09e3-11e9-976e-8ff2c145bebd.png)

이 후엔 `폰기종 Connected`를 클릭 후 안드로이드폰에서 크롬App을 실행 하면  Intercept를 클릭 하시면 안드로이드폰과 PC에 동일한 화면을 공유 하며 디버깅이 가능 합니다.

![2018-12-27 2 32 13](https://user-images.githubusercontent.com/6037055/50467229-3a319700-09e5-11e9-89fa-e04d87af75d1.png)

![2018-12-27 2 37 01](https://user-images.githubusercontent.com/6037055/50467411-39e5cb80-09e6-11e9-8596-936fca931838.png)
