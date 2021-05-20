---
title: 커뮤니티 그룹 핵심 사항
seo-title: 커뮤니티 그룹 핵심 사항
description: 동적으로 커뮤니티 사이트 만들기
seo-description: 동적으로 커뮤니티 사이트 만들기
uuid: 168e7aeb-6e9a-468d-8ac4-274007cea252
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4f85cd3c-5158-4f23-abe2-7e375fd0c8d4
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 1%

---

# 커뮤니티 그룹 필수 패키지 {#community-group-essentials}

커뮤니티 그룹 기능은 게시 및 작성 환경에서 인증된 사용자가 커뮤니티 사이트 내에서 하위 커뮤니티를 동적으로 만들 수 있는 기능입니다.

커뮤니티 [기능 팩 1](deploy-communities.md#latestfeaturepack)부터 그룹을 다른 그룹 내에서 중첩할 수 있습니다

## 클라이언트측 {#essentials-for-client-side}에 대한 필수 사항

### 커뮤니티 그룹 구성원 목록 {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/communitygroupmemberlist</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
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
   <td><a href="creating-groups.md">커뮤니티 그룹</a>을 참조하십시오</td>
  </tr>
 </tbody>
</table>

### 커뮤니티 그룹 {#community-groups}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/communitygroups</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
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

## 서버측 {#essentials-for-server-side}에 대한 필수 사항

* [커뮤니티 그룹 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [커뮤니티 그룹 끝점](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [서버측 사용자 지정](server-customize.md)

### 그룹 함수 {#groups-function}

[그룹 함수](functions.md#groups-function)를 포함하는 커뮤니티 사이트 구조는 게시 및 작성 환경에서 새 `community groups` 만들기를 지원합니다. 생성된 커뮤니티 그룹은 그룹의 구성원을 나열하는 `community groups member list` 구성 요소를 포함합니다.

커뮤니티 그룹 페이지의 디자인을 제공하는 [커뮤니티 그룹 템플릿](tools-groups.md) 중 하나 이상은 함수가 [커뮤니티 사이트 템플릿](sites.md)에 추가되거나 커뮤니티 그룹 템플릿 내에서 중첩될 때 그룹 함수에 대해 구성할 수 있습니다.

여러 커뮤니티 그룹 템플릿을 포함하면 작성자를 위한 [커뮤니티 그룹](creating-groups.md)의 섹션에 표시된 대로 커뮤니티 사이트에 대해 새 커뮤니티 그룹이 생성될 때 권한이 있는 사용자에게 디자인을 선택할 수 있습니다.

### 중첩된 그룹 {#nested-groups}

커뮤니티 [FP1](deploy-communities.md#latestfeaturepack)에서는 그룹 함수를 그룹 템플릿 내에 포함할 수 있으므로 중첩 그룹(하위 커뮤니티)에 대해 허용됩니다.

커뮤니티 사이트 또는 그룹 템플릿에 그룹 기능이 포함되는 경우 다음을 수행할 수 있습니다.

* 작성 환경에서 하위 커뮤니티를 만듭니다.

* 게시 환경에서 그룹을 허용하도록 구성된 경우 만듭니다.

작성 환경에서 그룹을 만들 때는 먼저 커뮤니티 사이트를 게시한 다음 해당 그룹을 게시해야 합니다. 커뮤니티 사이트를 게시하면 ACL이 설정된 하위 커뮤니티의 구성원 그룹을 만들지 않고 그룹의 페이지가 게시됩니다. 따라서, 그룹이 명시적으로 게시될 때까지 제한된(비밀) 그룹이 표시될 수 있다.

## 링크 및 관련 정보 {#links-and-related-information}

* [사용자 및 사용자 그룹 관리](users.md)
* [커뮤니티 그룹 콘솔](groups.md)
* [그룹 함수](functions.md#groups-function)
* [그룹 템플릿](tools-groups.md)
