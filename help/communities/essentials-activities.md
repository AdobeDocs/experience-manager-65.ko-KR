---
title: 활동 스트림 필수
seo-title: 활동 스트림 필수
description: 구성원이 수행한 최근 활동 목록 또는 컨텐츠 단일 스레드에서 최근 활동 목록
seo-description: 구성원이 수행한 최근 활동 목록 또는 컨텐츠 단일 스레드에서 최근 활동 목록
uuid: 30c5ac08-0af0-4670-9d81-0beb5c93e00a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8714b456-527a-457b-82c4-21bd445dfd9c
docset: aem65
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 1%

---


# 활동 스트림 필수 항목 {#activity-stream-essentials}

포럼이나 블로그에 게시하는 등 커뮤니티 멤버의 서명된 활동은 활동 스트림 구성 요소를 구성하여 다양한 방법으로 필터링되고 표시할 수 있는 스트림에 수집됩니다.

팔로우하는 능력은 커뮤니티 회원이 관심 게시나 다른 커뮤니티 구성원을 따를 때 다른 일련의 활동을 더해줍니다.

모든 [커뮤니티 사이트](/help/communities/overview.md#communitiessites)에는 멤버 활동을 동일한 방식으로 표시하는 로그인한 구성원의 사용자 프로필 페이지가 포함됩니다.

## 개념 {#concepts}

*활동 스트림*&#x200B;은 회원이 수행한 최근 활동 목록 또는 포럼 주제 또는 블로그와 같은 컨텐츠 스레드의 최근 활동 목록입니다.

멤버는 다른 개인 또는 컨텐츠를 팔로우하여 활동 스트림을 팔로우할 수 있습니다.

*뉴스 피드*&#x200B;는 구성원이 뒤에 오는 활동 스트림을 단일 스트림으로 병합하는 것입니다.

*[소셜 그래프](/help/communities/essentials-socialgraph.md)*&#x200B;는 한 멤버에 대한 다음 관계를 다른 멤버에 캡처합니다.

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/activitystreams/components/hbs/activitystreams</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>includable</strong></a></td>
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

## Essentials for Server-Side {#essentials-for-server-side}

* [활동 스트림 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [Activity Streams 리스너 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [서버측 사용자 정의](/help/communities/server-customize.md)

### 활동 스트림 기능 {#activity-stream-function}

[활동 스트림 함수](/help/communities/functions.md#activity-stream-function)를 포함하는 커뮤니티 사이트 구조에는 구성된 `activity streams` 구성 요소가 포함되어 있습니다.
