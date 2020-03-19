---
title: 커뮤니티 개발
seo-title: 커뮤니티 개발
description: 포럼, 사용자 그룹 등과 같은 커뮤니티 기능 만들기 및 사용자 정의
seo-description: 포럼, 사용자 그룹 등과 같은 커뮤니티 기능 만들기 및 사용자 정의
uuid: 51dc54da-9090-4d36-adf9-72d5479062a5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: fbfe8097-3c3f-4a05-97ad-1ce526362a26
translation-type: tm+mt
source-git-commit: 5b8b1544645465d10e7c2018364b6a74f1ad9a8e

---


# 커뮤니티 개발 {#developing-communities}

## 개요 {#overview}

AEM Communities를 사용하면 포럼, 사용자 그룹, 블로그, Q&amp;A, 캘린더, 주석, 평가, 투표, 등급 및 할당과 같은 커뮤니티 기능을 간단하게 만들고 사용자 정의할 수 있습니다. 이러한 기능을 통해 사용자가 생성한 콘텐츠(UGC)가 게시 환경에 입력됩니다.

커뮤니티 사이트의 [기본은](overview.md#communitiessites) 소셜 구성 요소 프레임워크 [](scf.md) (SCF)입니다. 커뮤니티 사이트 만들기는 [커뮤니티 기능으로](sites-console.md) 구성된 [커뮤니티 사이트 템플릿을](functions.md)선택하는 것으로 시작합니다.

개요 및 시작 자습서는 다음을 참조하십시오.

* [AEM Communities 개요](overview.md)
* [AEM Communities 시작하기](getting-started.md)
* [활성화를 위한 AEM Communities 시작하기](getting-started-enablement.md)

>[!NOTE]
>
>[최신 릴리스를](deploy-communities.md#latest-releases)최신 상태로 유지하는 것이 좋습니다.

## 권장 배포 {#recommended-deployments}

* [커뮤니티 컨텐츠 스토리지](working-with-srp.md):UGC 일반 스토어에 사용할 수 있는 SRP에 대해 설명합니다.
* [커뮤니티를 위한 권장 토폴로지](topologies.md):사용 사례 및 SRP 선택에 따라 토폴로지 토론

## 소셜 구성 요소 프레임워크 {#social-component-framework}

* [소셜 구성 요소 프레임워크](scf.md):프레임워크 및 API 개요
* [SCF Handlebars Helpers](handlebars-helpers.md):기본 도움말 및 사용자 정의 도움말 작성 방법
* [클라이언트측 사용자 정의](client-customize.md):브라우저에서 실행되는 코드 사용자 정의
* [서버측 사용자 정의](server-customize.md):서버에서 실행되는 코드 사용자 정의
* [SRP(Storage Resource Provider)](srp.md):커뮤니티 컨텐츠 저장소 개요
* [코딩 지침](code-guide.md):지침, 팁 및 기법
* [커뮤니티 구성 요소 안내서](components-guide.md):인터랙티브한 개발 툴

## 구성 요소, 기능 및 기능 필수 {#component-function-and-feature-essentials}

AEM Communities 구성 요소, 기능 및 기능은 [커뮤니티 사이트를](sites-console.md)위한 기본 요소를 제공합니다.

* [구성 요소, 기능 및 기능 필수](essentials.md)
* [커뮤니티 구성 요소용 Clientlibs](clientlibs.md)
* [커뮤니티 기능](functions.md)
* [커뮤니티 그룹 템플릿](tools-groups.md)
* [커뮤니티 사이트 템플릿](sites.md)

## 커뮤니티 구성원 {#community-members}

* [사용자 및 사용자 그룹 관리](users.md)
* [Facebook 및 Twitter를 사용한 소셜 로그인](social-login.md)

## 커뮤니티 그룹 {#community-groups}

[커뮤니티 그룹은](overview.md#communitygroups) 커뮤니티 구성원이 커뮤니티 사이트 내에서 하위 커뮤니티를 구성할 수 있도록 하는 개념입니다. 커뮤니티 그룹 만들기는 게시 또는 작성 환경에서 발생할 수 있습니다.

* [Community Group Essentials](essentials-groups.md)
* [그룹 함수](functions.md#groups-function)
* [커뮤니티 그룹 템플릿](tools-groups.md)
* [사용자 및 사용자 그룹 관리](users.md)
* [작성자를 위한 커뮤니티 그룹](creating-groups.md)

## 데이터 관리 {#managing-data}

* [SRP 및 UGC Essentials](srp-and-ugc.md) - SRP API 유틸리티 메서드 및 예제
* [Tag Essentials](tag.md) - 커뮤니티 구성원이 UGC 및/또는 카탈로그화된 활성 리소스에 태그를 지정할 수 있는 기능

## 튜토리얼 {#tutorials}

* [클라이언트측 자습서](tutorials.md#client-side-customization)
* [서버측 자습서](tutorials.md#server-side-customization)
* [사용 방법 지침](tutorials.md#how-to-instructions)

## 문제 해결 {#troubleshooting}

* [문제 해결](troubleshooting.md)
* [알려진 문제](/help/release-notes/known-issues.md)

## 관련 커뮤니티 설명서 {#related-communities-documentation}

* 권장 배포 [및](deploy-communities.md) 디스패처 구성에 대해 알아보려면 커뮤니티 배포를 참조하십시오.

* 커뮤니티 사이트 [관리를](administer-landing.md) 방문하여 커뮤니티 사이트 만들기, 커뮤니티 사이트 템플릿 구성, 커뮤니티 콘텐츠 중재, 구성원 관리 및 메시지 구성에 대해 알아보십시오.

* 커뮤니티 [구성 요소를](author-communities.md) 사용하여 작성하고 구성하는 방법을 알아보려면 커뮤니티 구성 요소를 참조하십시오.

