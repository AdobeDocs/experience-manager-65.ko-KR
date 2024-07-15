---
title: 개발 커뮤니티
description: 포럼, 사용자 그룹 등과 같은 커뮤니티 기능을 만들고 사용자 지정합니다.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3ed3768a-1b3c-45a1-a34c-61694cd407d9
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 5%

---

# 개발 커뮤니티  {#developing-communities}

## 개요 {#overview}

AEM(Adobe Experience Manager) 커뮤니티는 포럼, 사용자 그룹, 블로그, Q&amp;A, 캘린더, 댓글, 검토, 투표, 등급 및 할당과 같은 커뮤니티 기능을 간편하게 만들고 사용자 지정할 수 있습니다. 이러한 기능을 사용하면 UGC(사용자 생성 컨텐츠)가 게시 환경에 입력됩니다.

[커뮤니티 사이트](overview.md#communitiessites)의 기초는 [소셜 구성 요소 프레임워크](scf.md)(SCF)입니다. 커뮤니티 사이트 만들기는 [커뮤니티 기능](functions.md)(으)로 구성된 [커뮤니티 사이트 템플릿](sites-console.md)을(를) 선택하는 것으로 시작됩니다.

개요 및 시작 튜토리얼을 보려면 다음을 방문하십시오.

* [AEM Communities 개요](overview.md)
* [AEM Communities 시작하기](getting-started.md)

>[!NOTE]
> 
>[최신 릴리스](deploy-communities.md#latest-releases)를 최신 상태로 유지하는 것이 좋습니다.

## 권장 배포 {#recommended-deployments}

* [커뮤니티 콘텐츠 저장소](working-with-srp.md): UGC 공용 저장소에 사용할 수 있는 SRP(소셜 리소스 공급자) 선택 사항에 대해 설명합니다.
* [커뮤니티에 대해 권장되는 토폴로지](topologies.md): 사용 사례 및 SRP 선택에 따라 토폴로지에 대해 설명합니다.

## 소셜 구성 요소 프레임워크 {#social-component-framework}

* [소셜 구성 요소 프레임워크](scf.md): 프레임워크 및 API 개요.
* [SCF Handlebars 도우미](handlebars-helpers.md): 기본 도우미 및 사용자 지정 도우미 작성 방법.
* [클라이언트측 사용자 지정](client-customize.md): 브라우저에서 실행되는 코드를 사용자 지정합니다.
* [서버측 사용자 지정](server-customize.md): 서버에서 실행되는 코드를 사용자 지정합니다.
* [SRP(저장소 리소스 공급자)](srp.md): 커뮤니티 콘텐츠 저장소 개요.
* [코딩 지침](code-guide.md): 지침, 팁 및 요령.
* [커뮤니티 구성 요소 안내서](components-guide.md): 대화형 개발 도구.

## 구성 요소, 기능 및 기능 핵심 사항 {#component-function-and-feature-essentials}

AEM Communities 구성 요소, 함수 및 기능은 [커뮤니티 사이트](sites-console.md)를 위한 기본 구성 요소를 제공합니다.

* [구성 요소, 기능 및 기능 핵심 사항](essentials.md)
* [커뮤니티 구성 요소에 대한 Clientlibs](clientlibs.md)
* [커뮤니티 기능](functions.md)
* [커뮤니티 그룹 템플릿](tools-groups.md)
* [커뮤니티 사이트 템플릿](sites.md)

## 커뮤니티 구성원 {#community-members}

* [사용자 및 사용자 그룹 관리](users.md)
* [facebook 및 Twitter으로 소셜 로그인](social-login.md)

## 커뮤니티 그룹 {#community-groups}

[커뮤니티 그룹](overview.md#communitygroups)은(는) 커뮤니티 구성원이 커뮤니티 사이트 내에서 하위 커뮤니티를 형성할 수 있도록 하는 개념입니다. 커뮤니티 그룹 생성은 게시 또는 작성 환경에서 발생할 수 있습니다.

* [커뮤니티 그룹 기본 사항](essentials-groups.md)
* [그룹 기능](functions.md#groups-function)
* [커뮤니티 그룹 템플릿](tools-groups.md)
* [사용자 및 사용자 그룹 관리](users.md)
* [작성자를 위한 커뮤니티 그룹](creating-groups.md)

## 데이터 관리 {#managing-data}

* [SRP 및 UGC Essentials](srp-and-ugc.md) - SRP API 유틸리티 메서드 및 예제
* [Tag Essentials](tag.md) - 커뮤니티 구성원이 UGC 및/또는 카탈로그 지원 리소스에 태그를 지정할 수 있는 기능

## 튜토리얼 {#tutorials}

* [클라이언트측 자습서](tutorials.md#client-side-customization)
* [서버측 자습서](tutorials.md#server-side-customization)
* [방법 지침](tutorials.md#how-to-instructions)

## 문제 해결 {#troubleshooting}

* [문제 해결](troubleshooting.md)
* [알려진 문제](/help/release-notes/release-notes.md)

## 관련 커뮤니티 설명서 {#related-communities-documentation}

* 권장 배포 및 Dispatcher 구성에 대한 자세한 내용은 [커뮤니티 배포](deploy-communities.md)를 참조하세요.

* [커뮤니티 사이트 관리](administer-landing.md)를 방문하여 커뮤니티 사이트 만들기, 커뮤니티 사이트 템플릿 구성, 커뮤니티 콘텐츠 관리, 구성원 관리 및 메시지 구성에 대해 알아보십시오.

* [커뮤니티 구성 요소 작성](author-communities.md)을 방문하여 커뮤니티 구성 요소를 작성하고 구성하는 방법에 대해 알아보십시오.
