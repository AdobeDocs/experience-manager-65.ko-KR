---
title: 활동 스트림 Essentials
description: 구성원이 수행한 최근 활동 목록 또는 콘텐츠의 단일 스레드에서 최근 활동 목록
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d98bcbe4-3f80-49ec-b40c-417be0d97350
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 2%

---

# 활동 스트림 Essentials {#activity-stream-essentials}

포럼 또는 블로그에 게시하는 것과 같이, 로그인한 커뮤니티 구성원의 활동은 스트림으로 수집되며, 이 스트림은 활동 스트림 구성 요소의 구성을 통해 다양한 방식으로 필터링 및 표시될 수 있습니다.

팔로우 능력은 커뮤니티 회원이 관심 있는 게시물이나 다른 커뮤니티 회원을 팔로우할 때 또 다른 활동 세트를 추가합니다.

모두 [커뮤니티 사이트](/help/communities/overview.md#communitiessites) 같은 방식으로 구성원 활동을 표시할 로그인한 구성원의 사용자 프로필 페이지를 포함합니다.

## 개념 {#concepts}

An *활동 스트림* 는 구성원이 수행한 최근 활동 목록이나 포럼 주제나 블로그와 같은 컨텐츠의 단일 스레드에 대한 최근 활동 목록입니다.

구성원은 다른 개인 또는 콘텐츠를 팔로우하여 활동 스트림을 팔로우할 수 있습니다.

A *뉴스피드* 는 멤버로 뒤따르는 활동 스트림을 단일 스트림으로 병합하는 것입니다.

A *[소셜 그래프](/help/communities/essentials-socialgraph.md)* 한 구성원과 다른 구성원의 다음 관계를 캡처합니다.

## 클라이언트측 핵심 사항 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/activitystreams/components/hbs/activitystreams</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>포함하기 쉬워</strong></a></td>
   <td>아니요</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.activitystreams</td>
  </tr>
  <tr>
   <td> <strong>템플릿</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/activitystreams.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity-title.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/clientlibs/activitystreams.css</td>
  </tr>
  <tr>
   <td><strong> 속성</strong></td>
   <td>다음을 참조하십시오 <a href="/help/communities/activities.md">활동 스트림 기능</a></td>
  </tr>
 </tbody>
</table>

* [클라이언트측 사용자 지정](/help/communities/client-customize.md)

## 서버측 Essentials {#essentials-for-server-side}

* [활동 스트림 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [Activity Streams 수신기 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [서버측 사용자 지정](/help/communities/server-customize.md)

### 활동 스트림 기능 {#activity-stream-function}

다음을 포함하는 커뮤니티 사이트 구조 [활동 스트림 기능](/help/communities/functions.md#activity-stream-function), 구성된 포함 `activity streams` 구성 요소.
