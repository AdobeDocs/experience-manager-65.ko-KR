---
title: 구성 요소, 기능 및 기능 필수
seo-title: 구성 요소, 기능 및 기능 필수
description: 커뮤니티 사이트, 템플릿 및 그룹 기능
seo-description: 커뮤니티 사이트, 템플릿 및 그룹 기능
uuid: 6edfca2d-fe5b-4261-b033-51dc2f9dbfd7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 2d308756-79d1-4d69-b51c-d4b6e692a137
translation-type: tm+mt
source-git-commit: 941ffeb40805c991eec6a601d01796cfc2cc95e4

---


# 구성 요소, 기능 및 기능 필수 {#component-function-and-feature-essentials}

AEM Communities 기능을 사용하려면 먼저 사이트 방문자가 구성원이 되고 [커뮤니티 사이트에](overview.md#communitiessites) 로그인해야 합니다. 따라서 커뮤니티 사이트를 [만드는](sites.md)커뮤니티 사이트 템플릿은 [](sites-console.md)로그인 기능뿐만 아니라 사용자 프로필, 메시지, 검색, 중재 및 번역 기능이 포함되도록 디자인되었습니다.

커뮤니티 사이트는 [커뮤니티 그룹 기능이](functions.md#groups-function) 선택한 커뮤니티 사이트 템플릿에 포함될 때 커뮤니티 그룹을 만드는 구성원을 지원합니다.

다음은 커뮤니티 구성 요소, 기능 및 기능에 대한 필수 정보에 대한 링크입니다.

## 기본 구성 요소 {#base-components}

* [댓글](essentials-comments.md)
* [검토](reviews-basics.md)
* [Tally](tally.md)

   * [연결](essentials-liking.md)
   * [등급](rating-basics.md)
   * [투표](essentials-voting.md)
   * *투표(더 이상 사용할 수 없음)*

## 함수가 있는 구성 요소 {#components-with-functions}

* [활동 스트림](essentials-activities.md)
* [할당](essentials-assignments.md)
* [블로그](blog-developer-basics.md) ( `Journal`)

* [달력](calendar-basics-for-developers.md)
* [카탈로그](catalog-developer-essentials.md)
* [특별 포함된 컨텐츠](essentials-featured.md)
* [파일 라이브러리](essentials-file-library.md)
* [포럼](essentials-forum.md)
* [그룹](essentials-groups.md)
* [관념화](ideation.md)
* [리더보드](leaderboard.md)
* [질문과 대답](qna-essentials.md) `(QnA)`

## 기능 {#features}

* [클라이언트 라이브러리](clientlibs.md)
* [커뮤니티 사이트](sites-for-developers.md)
* [구성 요소 OSGi 이벤트](events.md)
* [구성 요소 사이드로드](sideloading.md)
* [메시지](essentials-messaging.md)
* [리치 텍스트 편집기](rte.md)
* [점수 및 배지](configure-scoring.md)
* [검색](search-implementation.md)
* [소셜 그래프](essentials-socialgraph.md)
* [저장소 리소스 공급자](srp-and-ugc.md)`(SRP)`

* [태깅](tag.md)

## Javadocs {#javadocs}

온라인 [javadocs](../../help/sites-developing/reference-materials.md) 는 AEM 6.3 릴리스에서 사용할 수 있는 API를 반영합니다.
Communities API는 `com.adobe.cq.social.*` 패키지에 있습니다.

각 [기능 팩에](deploy-communities.md#latestfeaturepack)대해 javadoc jar를 사용할 수 있습니다. 자세한 내용은 커뮤니티에 대한 [Maven 사용을 참조하십시오](maven.md#javadocs).

## 추가 정보 {#additional-information}

* [SCF(소셜 구성 요소 프레임워크)](scf.md)

   * [클라이언트측 사용자 정의](client-customize.md)
   * [서버측 사용자 정의](server-customize.md)
   * [저장소 리소스 공급자 개요](srp.md)

* [코딩 지침](code-guide.md)
* [튜토리얼](tutorials.md)
* [문제 해결](troubleshooting.md)

