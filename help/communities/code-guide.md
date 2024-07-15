---
title: 코딩 지침
description: 커뮤니티 개발자 지침, 팁 및 요령
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 1%

---

# 코딩 지침 {#coding-guidelines}

## 지침, 팁 및 요령 {#guidelines-tips-and-tricks}

AEM Communities을 사용한 작업은 Java Server Pages에 크게 의존하는 방식에서 비즈니스 논리, 스타일 및 페이지 콘텐츠가 서로 구별되는 템플릿 스크립팅 언어를 선택할 수 있는 유연성으로 발전해 왔습니다.

UGC(사용자 생성 콘텐츠)를 사용하여 보다 유연하게 작업할 수 있도록 하려면 SocialResourceProvider API를 사용하므로 배포에 대해 [SRP](srp.md) 옵션을 선택한 항목을 인식할 필요가 없습니다.

다음은 AEM Communities 개발자를 위한 다양한 코딩 지침 및 모범 사례입니다.

### 코드 {#code}

* [SRP를 사용하여 UGC에 액세스](accessing-ugc-with-srp.md) - UGC가 JCR(JSRP)에 저장된 경우에만 작동하는 응용 프로그램을 쓰지 않는 방법.
* [SocialUtils 리팩터링](socialutils.md) - SocialUtils를 대체하는 SRP용 유틸리티 메서드입니다.
* [이름 지정 규칙](naming-conventions.md) - 사용자 지정 Java 클래스에 대한 이름 지정 규칙입니다.

### 스크립트 {#scripts}

* [Sideloading Communities 구성 요소](sideloading.md) - 페이지가 로드된 후 구성 요소를 동적으로 추가하는 방법.
* [리치 텍스트 편집기 필수 패키지](rte.md) - 콘텐츠를 게시하기 위해 구성원에게 제공되는 리치 텍스트 UI를 사용자 지정하는 방법.

### IDE {#ide}

* [커뮤니티에 Maven 사용](maven.md) - Communities API Jar를 포함하는 방법.
* [SocialUtils 리팩터링](socialutils.md) - SocialUtils를 대체하는 SRP용 유틸리티 메서드입니다.
