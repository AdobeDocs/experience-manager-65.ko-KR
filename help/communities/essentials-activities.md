---
title: 활동 스트림 필수
seo-title: 활동 스트림 필수
description: 구성원이 수행한 최근 활동 목록 또는 단일 컨텐츠 스레드에서 최근 활동 목록
seo-description: 구성원이 수행한 최근 활동 목록 또는 단일 컨텐츠 스레드에서 최근 활동 목록
uuid: 30c5ac08-0af0-4670-9d81-0beb5c93e00a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8714b456-527a-457b-82c4-21bd445dfd9c
docset: aem65
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# 활동 스트림 필수 {#activity-stream-essentials}

포럼 또는 블로그에 게시하고 같이 로그인한 커뮤니티 구성원의 활동은 활동 스트림 구성 요소의 구성을 통해 필터링되어 다양한 방법으로 표시될 수 있는 스트림으로 수집됩니다.

팔로우 기능은 커뮤니티 회원이 관심 있는 게시물이나 다른 커뮤니티 구성원을 팔로우할 때 다른 일련의 활동을 추가합니다.

모든 [커뮤니티 사이트에는](/help/communities/overview.md#communitiessites) 동일한 방식으로 구성원 활동을 표시하는 로그인한 구성원의 사용자 프로필 페이지가 포함됩니다.

## 개념 {#concepts}

활동 *스트림은* 회원이 수행한 최근 활동 목록이나 포럼 주제 또는 블로그와 같은 컨텐츠 단일 스레드에서 최근 활동 목록입니다.

멤버는 다른 개인 또는 컨텐츠를 팔로우하여 활동 스트림을 팔로우할 수 있습니다.

뉴스 피드는 ** 다음에 구성원이 나오는 활동 스트림을 단일 스트림으로 병합하는 것입니다.

소셜 *[그래프는](/help/communities/essentials-socialgraph.md)*한 구성원과 다른 구성원의 다음 관계를 캡처합니다.

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
   <td>활동 <a href="/help/communities/activities.md">스트림 기능 보기</a></td>
  </tr>
 </tbody>
</table>

* [클라이언트측 사용자 정의](/help/communities/client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [활동 스트림 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [Activity Streams 리스너 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [서버측 사용자 정의](/help/communities/server-customize.md)

### 활동 스트림 기능 {#activity-stream-function}

활동 스트림 함수를 포함하는 [커뮤니티 사이트](/help/communities/functions.md#activity-stream-function)구조에는 구성된 `activity streams` 구성 요소가 포함됩니다.
