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

---


# 코딩 지침 {#coding-guidelines}

## 지침, 팁 및 기법 {#guidelines-tips-and-tricks}

AEM Communities를 사용하여 작업하는 것은 Java Server 페이지에 의존하는 것에서 비즈니스 로직, 스타일 및 페이지 컨텐츠가 서로 구분되는 스크립팅 언어를 유연하게 선택할 수 있도록 발전되었습니다.

사용자 생성 컨텐츠(UGC)를 사용하여 작업할 때 더 많은 유연성은 SocialResourceProvider API를 통해 제공되므로 배포를 위해 선택한 SRP [](srp.md) 옵션을 인식할 필요가 없습니다.

다음은 AEM Communities 개발자를 위한 다양한 코딩 지침 및 모범 사례입니다.

### 코드 {#code}

* [SRP를 사용하여 UGC에](accessing-ugc-with-srp.md) 액세스 - UGC가 JCR(JSRP)에 저장된 경우에만 작동하는 애플리케이션을 작성하지 않는 방법
* [SocialUtils 리팩토링](socialutils.md) - SocialUtils를 대체하는 SRP에 대한 유틸리티 메서드입니다.
* [이름 지정 규칙](naming-conventions.md) - 사용자 지정 Java 클래스에 대한 이름 지정 규칙.

### 스크립트 {#scripts}

* [커뮤니티 구성 요소 사이드](sideloading.md) 로드 - 페이지가 로드된 후 구성 요소를 동적으로 추가하는 방법.
* [리치 텍스트 편집기 필수](rte.md) 사항 - 컨텐츠를 게시하기 위해 구성원에게 제공되는 리치 텍스트 UI를 사용자 지정하는 방법.

### IDE {#ide}

* [커뮤니티에 Maven 사용](maven.md) - 커뮤니티 API jar를 포함하는 방법.
* [SocialUtils 리팩토링](socialutils.md) - SocialUtils를 대체하는 SRP에 대한 유틸리티 메서드입니다.

