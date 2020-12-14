---
title: Blog Essentials
seo-title: Blog Essentials
description: 블로그 개요
seo-description: 블로그 개요
uuid: 714cf70c-76a0-4be6-9163-a31ac6bd1643
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: eece7b8f-6ccd-4037-8713-0cd36cfd9e73
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 2%

---


# 블로그 필수 항목 {#blog-essentials}

AEM 6.1 Communities의 경우 블로그는 커뮤니티 활동입니다. 이제 블로그 아티클이 게시 환경에서 게시되며 이전에는 블로그 아티클을 작성 환경에서만 만들고 게시할 수 있었습니다.

권한이 있는 구성원에게 제한되지 않는 한 이제 모든 커뮤니티 구성원이 블로그 아티클을 만들 수 있습니다.

이 페이지에서는 블로그 기능 작업에 필요한 정보를 제공합니다.

>[!NOTE]
>
>블로그 기능의 기본 인프라가 저널 기능입니다.

## Essentials for Client-Side {#essentials-for-client-side}

블로그 기능은 [블로그 함수](/help/communities/functions.md#blog-function)를 추가하거나 작성 편집 모드에서 페이지에 구성 요소를 추가하여 사용할 수 있는 두 개의 기본 구성 요소로 구성됩니다.

### 블로그 {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/journal/components/hbs/journal</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>includable</strong></a></td>
   <td>아니오</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.vocing<br /> cq.social.hbs.journal</td>
  </tr>
  <tr>
   <td> <strong>템플릿</strong></td>
   <td> /libs/social/journal/components/hbs/journal/journal.hbs<br /> /libs/social/journal/components/hbs/entry_topic/list-item.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/journal/components/hbs/journal/clientlibs/journal.css</td>
  </tr>
  <tr>
   <td><strong> 속성</strong></td>
   <td><a href="/help/communities/blog-feature.md">블로그 기능</a> 참조</td>
  </tr>
 </tbody>
</table>

### 블로그 세로 막대 {#blog-sidebar}

| **resourceType** | social/journal/components/hbs/sidebar |
|---|---|
| [**includable**](/help/communities/scf.md#add-or-include-a-communities-component) | 아니오 |
| [**clientlibs**](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **템플릿** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **속성** | [블로그 기능](/help/communities/blog-feature.md) 참조 |

* [클라이언트측 사용자 지정](/help/communities/client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [블로그 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [블로그 끝점](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [서버측 사용자 정의](/help/communities/server-customize.md)

### 블로그 기능 {#blog-function}

[블로그 함수](/help/communities/functions.md#blog-function)가 포함된 커뮤니티 사이트 구조는 `Blog` 및 `Blog Sidebar` 구성 요소를 구성합니다. 블로그 함수는 [권한이 있는 구성원 사용자 그룹](/help/communities/users.md#privileged-members-group)을 식별하는 것을 지원합니다.

### 블로그 항목 액세스(UGC) {#accessing-blog-entries-ugc}

조정을 위한 표준 방법 중 하나를 사용하여 UGC를 중재해야 합니다.
[사용자 생성 콘텐츠 중재](/help/communities/moderate-ugc.md)를 참조하십시오.

AEM 6.1 Communities의 경우, UGC용 [공통 스토어](/help/communities/working-with-srp.md)를 사용하면 선택한 스토리지 옵션(예: ASRP, MSRP 또는 JSRP)에 상관없이 프로그램 방식으로 UGC에 액세스할 수 있습니다.

**저장소에서 UGC의 위치와 형식은 경고** 없이 변경될 수 있습니다.

다음을 참조하십시오.

* [스토리지 자원 공급자 개요](/help/communities/srp.md)  - 소개 및 저장소 사용 개요.
* [SRP 및 UGC Essentials](/help/communities/srp-and-ugc.md) - SRP 유틸리티 방법 및 예.
* [SRP](/help/communities/accessing-ugc-with-srp.md)  코딩 가이드라인을 사용하여 UGC 액세스
* [SocialUtils 리팩토링](/help/communities/socialutils.md)  - 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.

## 기본 게시자 {#primary-publisher}

배포가 게시 팜인 경우 게시할 아티클에 대해 폴링할 기본 게시자를 식별해야 합니다.

자세한 내용은 [기본 게시자](/help/communities/deploy-communities.md#primary-publisher)를 참조하십시오.

## 리치 미디어 허용 {#allowing-rich-media}

AEM 플랫폼은

* [XSS(교차 사이트 스크립팅)를 통한 Protect](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

AEM 6.2부터 이전에 수동으로 수행해야 했던 수정 사항은 기본 AntiSamy 구성 파일에 포함됩니다.

리치 미디어는 `Embed Media from External Sites` 아이콘을 선택하여 블로그 아티클에 포함됩니다.

![media](assets/media-icon.png)

