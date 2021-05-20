---
title: 활동 스트림 핵심 사항
seo-title: 활동 스트림 핵심 사항
description: 구성원이 수행한 최근 활동 목록 또는 단일 컨텐츠 스레드에서 최근 활동 목록
seo-description: 구성원이 수행한 최근 활동 목록 또는 단일 컨텐츠 스레드에서 최근 활동 목록
uuid: 30c5ac08-0af0-4670-9d81-0beb5c93e00a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8714b456-527a-457b-82c4-21bd445dfd9c
docset: aem65
exl-id: d98bcbe4-3f80-49ec-b40c-417be0d97350
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 1%

---

# 활동 스트림 필수 요소인 {#activity-stream-essentials}

커뮤니티 구성원의 활동(예: 포럼 또는 블로그에 게시)은 활동 스트림 구성 요소의 구성을 통해 다양한 방법으로 필터링 및 표시할 수 있는 스트림에 수집됩니다.

팔로우하는 기능은 커뮤니티 구성원이 관심 있는 게시나 다른 커뮤니티 구성원을 따를 때 다른 일련의 활동을 추가합니다.

모든 [커뮤니티 사이트](/help/communities/overview.md#communitiessites)에는 동일한 방식으로 구성원 활동을 표시할 로그인한 구성원의 사용자 프로필 페이지가 포함됩니다.

## 개념 {#concepts}

*활동 스트림*&#x200B;은 구성원이 수행한 최근 활동 목록이나 포럼 주제나 블로그와 같은 단일 컨텐츠 스레드에 있는 최근 활동 목록입니다.

구성원은 다른 개인 또는 콘텐츠를 팔로우하여 활동 스트림을 따를 수 있습니다.

*뉴스 피드*&#x200B;는 구성원이 뒤에 오는 활동 스트림의 병합입니다.

*[소셜 그래프](/help/communities/essentials-socialgraph.md)*&#x200B;는 한 구성원과 다른 구성원의 다음 관계를 캡처합니다.

## 클라이언트측 {#essentials-for-client-side}에 대한 필수 사항

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/activitystreams/components/hbs/activitystreams</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>포함 가능</strong></a></td>
   <td>아니오</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientlibs</strong></a></td>
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
   <td><a href="/help/communities/activities.md">활동 스트림 기능</a>을 참조하십시오.</td>
  </tr>
 </tbody>
</table>

* [클라이언트측 사용자 지정](/help/communities/client-customize.md)

## 서버측 {#essentials-for-server-side}에 대한 필수 사항

* [Activity Streams API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [Activity Streams 리스너 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [서버측 사용자 지정](/help/communities/server-customize.md)

### 활동 스트림 기능 {#activity-stream-function}

[활동 스트림 함수](/help/communities/functions.md#activity-stream-function)를 포함하는 커뮤니티 사이트 구조는 구성된 `activity streams` 구성 요소를 포함합니다.
