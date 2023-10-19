---
title: 커뮤니티 그룹 기본 사항
description: 승인된 사용자가 커뮤니티 그룹 기능을 사용하여 커뮤니티 사이트 내에 하위 커뮤니티를 동적으로 만드는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 1%

---

# 커뮤니티 그룹 기본 사항  {#community-group-essentials}

커뮤니티 그룹 기능은 게시 및 작성자 환경의 승인된 사용자가 커뮤니티 사이트 내에서 하위 커뮤니티를 동적으로 만들 수 있는 기능입니다.

커뮤니티 기준 [기능 팩 1](deploy-communities.md#latestfeaturepack), 그룹은 다른 그룹 내에 중첩될 수 있습니다.

## 클라이언트측 핵심 사항 {#essentials-for-client-side}

### 커뮤니티 그룹 구성원 목록 {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/communitygroupmemberlist</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>템플릿</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/communitygroupmemberlist.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/memberList.css</td>
  </tr>
  <tr>
   <td><strong>속성</strong></td>
   <td>다음을 참조하십시오 <a href="creating-groups.md">커뮤니티 그룹</a></td>
  </tr>
 </tbody>
</table>

### 커뮤니티 그룹 {#community-groups}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>소셜/그룹/구성 요소/hbs/커뮤니티 그룹</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>템플릿</strong></td>
   <td> /libs/social/group/components/hbs/communitygroups/communitygroups.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/communitygroups.css</td>
  </tr>
 </tbody>
</table>

* [클라이언트측 사용자 지정](client-customize.md)

## 서버측 Essentials {#essentials-for-server-side}

* [커뮤니티 그룹 API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [커뮤니티 그룹 엔드포인트](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [서버측 사용자 지정](server-customize.md)

### 그룹 기능 {#groups-function}

다음을 포함하는 커뮤니티 사이트 구조 [그룹 기능](functions.md#groups-function) 는 새 항목 만들기를 지원합니다. `community groups` 게시 및 작성 환경. 생성된 커뮤니티 그룹에는 다음이 포함됩니다. `community groups member list` 그룹 구성원을 나열하는 구성 요소입니다.

하나 이상 [커뮤니티 그룹 템플릿](tools-groups.md)커뮤니티 그룹 페이지의 디자인을 제공하는 는 그룹 기능에 대해 구성할 수 있습니다. 이는 함수가 에에 추가되는 경우에 적용됩니다 [커뮤니티 사이트 템플릿](sites.md) 또는 커뮤니티 그룹 템플릿 내에 중첩됩니다.

여러 커뮤니티 그룹 템플릿을 포함하면 선택할 수 있습니다. 즉, 커뮤니티 사이트에 대해 커뮤니티 그룹이 생성될 때 인증된 사용자에게 디자인의 선택 사항이 표시됩니다. 의 섹션을 참조하십시오. [커뮤니티 그룹](creating-groups.md) 작성자용.

### 중첩 그룹 {#nested-groups}

커뮤니티 기준 [FP1](deploy-communities.md#latestfeaturepack), 그룹 함수를 그룹 템플릿 내에 포함할 수 있으므로 중첩된 그룹(하위 커뮤니티)을 사용할 수 있습니다.

커뮤니티 사이트 또는 그룹 템플릿에 그룹 기능이 포함되어 있는 경우 다음과 같은 작업을 수행할 수 있습니다.

* 작성 환경에서 하위 커뮤니티를 만듭니다.

* 그룹을 허용하도록 구성된 경우 게시 환경에 그룹을 만듭니다.

작성 환경에서 그룹을 만들 때 먼저 커뮤니티 사이트를 게시한 다음 그룹을 게시해야 합니다. 커뮤니티 사이트를 게시하면 ACL이 설정된 하위 커뮤니티의 구성원 그룹을 만들지 않고 그룹의 페이지가 게시됩니다. 따라서 제한된(비밀) 그룹은 그룹이 명시적으로 게시될 때까지 표시될 수 있습니다.

## 링크 및 관련 정보 {#links-and-related-information}

* [사용자 및 사용자 그룹 관리](users.md)
* [커뮤니티 그룹 콘솔](groups.md)
* [그룹 기능](functions.md#groups-function)
* [그룹 템플릿](tools-groups.md)
