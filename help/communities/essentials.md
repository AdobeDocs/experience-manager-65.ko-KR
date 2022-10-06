---
title: 구성 요소, 기능 및 기능 핵심 사항
seo-title: Component, Function and Feature Essentials
description: 커뮤니티 사이트, 템플릿 및 그룹이 작동하는 방식
seo-description: How community sites, templates, and groups function
uuid: 6edfca2d-fe5b-4261-b033-51dc2f9dbfd7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 2d308756-79d1-4d69-b51c-d4b6e692a137
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 18%

---

# 구성 요소, 기능 및 기능 핵심 사항  {#component-function-and-feature-essentials}

AEM Communities 기능을 사용하려면 사이트 방문자가 구성원이 되고 로그인해야 합니다 [커뮤니티 사이트](overview.md#communitiessites) 컨텐츠를 게시하기 전에 따라서, [커뮤니티 사이트 템플릿](sites.md): 커뮤니티 사이트가 있는 위치 [생성됨](sites-console.md)은(는) 로그인 기능과 사용자 프로필, 메시징, 검색, 중재 및 번역을 포함하도록 설계되었습니다.

커뮤니티 사이트에서는 [커뮤니티 그룹 기능](functions.md#groups-function) 이 선택한 커뮤니티 사이트 템플릿에 포함되어 있습니다.

다음은 커뮤니티 구성 요소, 기능 및 기능에 대한 필수 정보에 대한 링크입니다.

## 기본 구성 요소 {#base-components}

* [댓글](essentials-comments.md)
* [검토](reviews-basics.md)
* [총계](tally.md)

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
* [구성 요소 테스트로드](sideloading.md)
* [메시지](essentials-messaging.md)
* [리치 텍스트 편집기](rte.md)
* [점수 및 배지](configure-scoring.md)
* [검색](search-implementation.md)
* [소셜 그래프](essentials-socialgraph.md)
* [저장소 리소스 공급자](srp-and-ugc.md) `(SRP)`

* [태깅](tag.md)

## Javadocs {#javadocs}

다음 [온라인 javadocs](../../help/sites-developing/reference-materials.md) AEM 6.3 릴리스에서 사용할 수 있는 API를 반영합니다.
Communities API가 `com.adobe.cq.social.*` 패키지.

각 [기능 팩](deploy-communities.md#latestfeaturepack), javadoc jar를 사용할 수 있습니다. 자세한 내용은 [커뮤니티에 Maven 사용](maven.md#javadocs).

## 추가 정보 {#additional-information}

* [SCF(소셜 구성 요소 프레임워크)](scf.md)

   * [클라이언트측 사용자 지정](client-customize.md)
   * [서버측 사용자 지정](server-customize.md)
   * [저장소 리소스 공급자 개요](srp.md)

* [코딩 지침](code-guide.md)
* [튜토리얼](tutorials.md)
* [문제 해결](troubleshooting.md)
