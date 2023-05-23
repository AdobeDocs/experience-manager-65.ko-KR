---
title: 코딩 지침
seo-title: Coding Guidelines
description: 커뮤니티 개발자 지침, 팁 및 요령
seo-description: Communities developer guidelines, tips, and tricks
uuid: 311ef4f7-7f2c-44c3-bcf2-f68713752623
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 244cd43c-a573-495d-b80c-b97ba9d19b75
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# 코딩 지침 {#coding-guidelines}

## 지침, 팁 및 요령 {#guidelines-tips-and-tricks}

AEM Communities을 사용한 작업은 Java Server Pages에 크게 의존하는 방식에서 비즈니스 논리, 스타일 및 페이지 콘텐츠가 서로 구별되는 템플릿 스크립팅 언어를 선택할 수 있는 유연성으로 발전해 왔습니다.

UGC(사용자 생성 컨텐츠)를 사용하여 보다 유연하게 작업할 수 있으려면 SocialResourceProvider API를 통해 다음 사항에 대한 인식이 필요하지 않습니다. [SRP](srp.md) 배포에 대한 옵션이 선택되었습니다.

다음은 AEM Communities 개발자를 위한 다양한 코딩 지침 및 모범 사례입니다.

### 코드 {#code}

* [SRP를 사용하여 UGC에 액세스](accessing-ugc-with-srp.md) - UGC가 JCR(JSRP)에 저장된 경우에만 작동하는 애플리케이션을 작성하지 않는 방법.
* [SocialUtils 리팩터링](socialutils.md) - SocialUtils를 대체하는 SRP의 유틸리티 메서드.
* [이름 지정 규칙](naming-conventions.md) - 사용자 지정 Java 클래스에 대한 이름 지정 규칙입니다.

### 스크립트 {#scripts}

* [Communities 구성 요소 사이드로드](sideloading.md) - 페이지가 로드된 후 구성 요소를 동적으로 추가하는 방법
* [리치 텍스트 편집기 핵심 사항](rte.md) - 콘텐츠를 게시하기 위해 구성원에게 제공되는 서식 있는 텍스트 UI를 사용자 지정하는 방법.

### IDE {#ide}

* [Maven for Communities 사용](maven.md) - Communities API jar를 포함하는 방법
* [SocialUtils 리팩터링](socialutils.md) - SocialUtils를 대체하는 SRP의 유틸리티 메서드.
