---
title: 코딩 지침
seo-title: 코딩 지침
description: 커뮤니티 개발자 지침, 팁 및 기법
seo-description: 커뮤니티 개발자 지침, 팁 및 기법
uuid: 311ef4f7-7f2c-44c3-bcf2-f68713752623
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 244cd43c-a573-495d-b80c-b97ba9d19b75
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# 코딩 지침 {#coding-guidelines}

## 지침, 팁 및 트릭 {#guidelines-tips-and-tricks}

AEM Communities을 사용한 작업은 Java Server 페이지에 따라 결정되는 방식에서 비즈니스 논리, 스타일 및 페이지 컨텐츠가 서로 구분되는 스크립팅 언어를 유연하게 선택할 수 있게 진화했습니다.

사용자 생성 컨텐츠(UGC)를 사용하여 작업할 때 더 많은 유연성은 SocialResourceProvider API를 통해 가능하므로 배포에 대해 [SRP](srp.md) 옵션을 선택했는지 확인할 필요가 없습니다.

다음은 AEM Communities 개발자를 위한 다양한 코딩 지침과 모범 사례입니다.

### 코드 {#code}

* [SRP를 사용하여 UGC에](accessing-ugc-with-srp.md)  액세스 - JSRP(JCR)에 UGC가 저장된 경우에만 작동하는 애플리케이션을 작성하지 않는 방법
* [SocialUtils 리팩토링](socialutils.md)  - SocialUtils를 대체하는 SRP에 대한 유틸리티 메서드입니다.
* [이름 지정 규칙](naming-conventions.md)  - 사용자 지정 Java 클래스에 대한 이름 지정 규칙입니다.

### 스크립트 {#scripts}

* [커뮤니티 구성 요소 사이드 로드](sideloading.md)  - 페이지가 로드된 후 구성 요소를 동적으로 추가하는 방법입니다.
* [리치 텍스트 편집기 필수](rte.md)  사항 - 컨텐츠를 게시하기 위해 구성원에게 제공되는 리치 텍스트 UI를 사용자 지정하는 방법에 대해 설명합니다.

### IDE {#ide}

* [Communities](maven.md) 에 대한 Maven 사용 - 커뮤니티 API jar를 포함하는 방법.
* [SocialUtils 리팩토링](socialutils.md)  - SocialUtils를 대체하는 SRP에 대한 유틸리티 메서드입니다.

