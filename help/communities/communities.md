---
title: 개발 커뮤니티
seo-title: Developing Communities
description: 포럼, 사용자 그룹 등과 같은 커뮤니티 기능 만들기 및 사용자 지정
seo-description: Create and customize community features such as forums, user groups, and more
uuid: 51dc54da-9090-4d36-adf9-72d5479062a5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: fbfe8097-3c3f-4a05-97ad-1ce526362a26
exl-id: 3ed3768a-1b3c-45a1-a34c-61694cd407d9
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 5%

---

# 개발 커뮤니티  {#developing-communities}

## 개요 {#overview}

AEM Communities을 사용하면 포럼, 사용자 그룹, 블로그, Q&amp;A, 캘린더, 댓글, 검토, 투표, 등급 및 할당과 같은 커뮤니티 기능을 간편하게 만들고 사용자 지정할 수 있습니다. 이러한 기능으로 인해 UGC(사용자 생성 컨텐츠)가 게시 환경에 입력됩니다.

의 기초 [커뮤니티 사이트](overview.md#communitiessites) 은(는) [소셜 구성 요소 프레임워크](scf.md) (SCF). 커뮤니티 사이트 만들기는 의 선택부터 시작됩니다. [커뮤니티 사이트 템플릿](sites-console.md) 다음으로 구성됩니다. [커뮤니티 기능](functions.md).

개요 및 시작 튜토리얼을 보려면 다음을 방문하십시오.

* [AEM Communities 개요](overview.md)
* [AEM Communities 시작하기](getting-started.md)

>[!NOTE]
> 
>를 최신 상태로 유지하는 것이 좋습니다. [최신 릴리스](deploy-communities.md#latest-releases).

## 권장 배포 {#recommended-deployments}

* [커뮤니티 콘텐츠 저장소](working-with-srp.md): UGC 공통 저장소에 사용할 수 있는 SRP 선택 사항에 대해 설명합니다.
* [커뮤니티에 대해 권장되는 토폴로지](topologies.md): 사용 사례 및 SRP 선택에 따른 토폴로지에 대해 설명합니다.

## 소셜 구성 요소 프레임워크 {#social-component-framework}

* [소셜 구성 요소 프레임워크](scf.md): 프레임워크 및 API 개요
* [SCF Handlebars 도우미](handlebars-helpers.md): 기본 도우미 및 사용자 지정 도우미 작성 방법
* [클라이언트측 사용자 정의](client-customize.md): 브라우저에서 실행되는 코드 사용자 지정.
* [서버측 사용자 지정](server-customize.md): 서버에서 실행되는 코드 사용자 지정.
* [저장소 리소스 제공자(SRP)](srp.md): 커뮤니티 콘텐츠 저장소 개요.
* [코딩 지침](code-guide.md): 지침, 팁 및 요령.
* [커뮤니티 구성 요소 안내서](components-guide.md): 대화형 개발 도구.

## 구성 요소, 기능 및 기능 핵심 사항 {#component-function-and-feature-essentials}

AEM Communities 구성 요소, 기능 및 기능은 의 기본 요소를 [커뮤니티 사이트](sites-console.md).

* [구성 요소, 기능 및 기능 핵심 사항](essentials.md)
* [커뮤니티 구성 요소에 대한 Clientlibs](clientlibs.md)
* [커뮤니티 기능](functions.md)
* [커뮤니티 그룹 템플릿](tools-groups.md)
* [커뮤니티 사이트 템플릿](sites.md)

## 커뮤니티 구성원 {#community-members}

* [사용자 및 사용자 그룹 관리](users.md)
* [facebook 및 Twitter을 사용한 소셜 로그인](social-login.md)

## 커뮤니티 그룹 {#community-groups}

[커뮤니티 그룹](overview.md#communitygroups) 는 커뮤니티 구성원이 커뮤니티 사이트 내에서 하위 커뮤니티를 형성할 수 있도록 하는 개념입니다. 커뮤니티 그룹 생성은 게시 또는 작성 환경에서 발생할 수 있습니다.

* [커뮤니티 그룹 기본 사항](essentials-groups.md)
* [그룹 기능](functions.md#groups-function)
* [커뮤니티 그룹 템플릿](tools-groups.md)
* [사용자 및 사용자 그룹 관리](users.md)
* [작성자를 위한 커뮤니티 그룹](creating-groups.md)

## 데이터 관리 {#managing-data}

* [SRP 및 UGC 필수 패키지](srp-and-ugc.md) - SRP API 유틸리티 메서드 및 예제
* [태그 기본 사항](tag.md) - 커뮤니티 구성원이 UGC 및/또는 카탈로그 지원 리소스에 태그를 지정할 수 있는 기능

## 튜토리얼 {#tutorials}

* [클라이언트측 자습서](tutorials.md#client-side-customization)
* [서버측 자습서](tutorials.md#server-side-customization)
* [방법 지침](tutorials.md#how-to-instructions)

## 문제 해결 {#troubleshooting}

* [문제 해결](troubleshooting.md)
* [알려진 문제](/help/release-notes/release-notes.md)

## 관련 커뮤니티 설명서 {#related-communities-documentation}

* 방문 [커뮤니티 배포](deploy-communities.md) 권장 배포 및 dispatcher 구성에 대해 알아봅니다.

* 방문 [커뮤니티 사이트 관리](administer-landing.md) 커뮤니티 사이트 만들기, 커뮤니티 사이트 템플릿 구성, 커뮤니티 콘텐츠 중재, 구성원 관리 및 메시지 구성에 대해 알아봅니다.

* 방문 [커뮤니티 구성 요소 작성](author-communities.md) 커뮤니티 구성 요소를 작성하고 구성하는 방법에 대해 알아봅니다.
