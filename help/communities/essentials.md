---
title: 구성 요소, 기능 및 기능 핵심 사항
description: 커뮤니티 사이트, 템플릿 및 그룹의 작동 방식
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 15%

---

# 구성 요소, 기능 및 기능 핵심 사항  {#component-function-and-feature-essentials}

AEM(Adobe Experience Manager) 커뮤니티 기능을 사용하려면 콘텐츠를 게시하려면 사이트 방문자가 구성원이 되어 [커뮤니티 사이트](overview.md#communitiessites)에 로그인해야 합니다. 따라서 커뮤니티 사이트가 [생성](sites-console.md)되는 [커뮤니티 사이트 템플릿](sites.md)은(는) 로그인 기능과 사용자 프로필, 메시지, 검색, 중재 및 번역을 포함하도록 디자인되었습니다.

[커뮤니티 그룹 기능](functions.md#groups-function)이 선택한 커뮤니티 사이트 템플릿에 포함되어 있으면 커뮤니티 사이트는 커뮤니티 그룹을 만드는 구성원을 지원합니다.

다음은 커뮤니티 구성 요소, 기능 및 기능에 대한 필수 정보에 대한 링크입니다.

## 기본 구성 요소 {#base-components}

* [댓글](essentials-comments.md)
* [리뷰](reviews-basics.md)
* [Tally](tally.md)

   * [연결](essentials-liking.md)
   * [등급](rating-basics.md)
   * [투표](essentials-voting.md)
   * *투표(더 이상 사용할 수 없음)*

## 기능이 있는 구성 요소 {#components-with-functions}

* [활동 스트림](essentials-activities.md)
* [블로그](blog-developer-basics.md)( `Journal`)

* [달력](calendar-basics-for-developers.md)
* [특별 포함된 컨텐츠](essentials-featured.md)
* [파일 라이브러리](essentials-file-library.md)
* [포럼](essentials-forum.md)
* [그룹](essentials-groups.md)
* [관념화](ideation.md)
* [리더보드](leaderboard.md)
* [질문 및 답변](qna-essentials.md) `(QnA)`

## 기능 {#features}

* [클라이언트 라이브러리](clientlibs.md)
* [커뮤니티 사이트](sites-for-developers.md)
* [구성 요소 OSGi 이벤트](events.md)
* [구성 요소 사이드로드](sideloading.md)
* [메시지](essentials-messaging.md)
* [리치 텍스트 편집기](rte.md)
* [채점 및 배지](configure-scoring.md)
* [검색](search-implementation.md)
* [소셜 그래프](essentials-socialgraph.md)
* [저장소 리소스 공급자](srp-and-ugc.md) `(SRP)`

* [태그 지정](tag.md)

## 자바독스 {#javadocs}

[온라인 javadocs](../../help/sites-developing/reference-materials.md)은(는) AEM 6.3 릴리스에서 사용 가능한 API를 반영합니다.
커뮤니티 API가 `com.adobe.cq.social.*` 패키지에 있습니다.

각 [기능 팩](deploy-communities.md#latestfeaturepack)에 대해 javadoc jar를 사용할 수 있습니다. 자세한 내용은 [커뮤니티용 Maven 사용](maven.md#javadocs)을 참조하세요.

## 추가 정보 {#additional-information}

* [소셜 구성 요소 프레임워크(SCF)](scf.md)

   * [클라이언트측 사용자 지정](client-customize.md)
   * [서버측 사용자 지정](server-customize.md)
   * [저장소 리소스 공급자 개요](srp.md)

* [코딩 지침](code-guide.md)
* [튜토리얼](tutorials.md)
* [문제 해결](troubleshooting.md)
