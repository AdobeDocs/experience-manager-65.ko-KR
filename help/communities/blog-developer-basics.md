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
source-git-commit: 272eedc1585dbdea315b49d010e4b1d78cedc360

---


# Blog Essentials {#blog-essentials}

AEM 6.1 Communities의 블로그는 커뮤니티 활동입니다. 블로그 아티클은 이제 게시 환경에서 게시되며, 이전에는 블로그 아티클을 작성 환경에서만 만들고 게시할 수 있었습니다.

이제 권한이 있는 구성원만 제한되지 않는 한 모든 커뮤니티 회원이 블로그 아티클을 만들 수 있습니다.

이 페이지에서는 블로그 기능을 사용하여 작업하는 데 필요한 정보를 제공합니다.

>[!NOTE]
>
>블로그 기능의 기본 인프라는 저널 기능입니다.

## Essentials for Client-Side {#essentials-for-client-side}

블로그 기능은 블로그 기능을 [](/help/communities/functions.md#blog-function) 추가하거나 작성 편집 모드에서 페이지에 구성 요소를 추가하여 사용할 수 있는 두 가지 기본 구성 요소로 구성됩니다.

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
   <td>cq.ckeditor<br /> cq.social.hbs.vocting<br /> cq.social.hbs.journal</td>
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
   <td>블로그 <a href="/help/communities/blog-feature.md">기능 보기</a></td>
  </tr>
 </tbody>
</table>

### 블로그 세로 막대 {#blog-sidebar}

| **resourceType** | social/journal/components/hbs/sidebar |
|---|---|
| [**includable **](/help/communities/scf.md#add-or-include-a-communities-component) | 아니오 |
| [**clientlibs **](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **템플릿** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **속성** | 블로그 [기능 보기](/help/communities/blog-feature.md) |

* [클라이언트측 사용자 정의](/help/communities/client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [블로그 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [블로그 끝점](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [서버측 사용자 정의](/help/communities/server-customize.md)

### 블로그 기능 {#blog-function}

블로그 기능을 [포함하는 커뮤니티 사이트 구조에는 구성](/help/communities/functions.md#blog-function) 및 `Blog` `Blog Sidebar` 구성 요소가 포함됩니다. 블로그 기능은 [권한 있는 구성원 사용자 그룹](/help/communities/users.md#privileged-members-group)식별을 지원합니다.

### 블로그 항목 액세스(UGC) {#accessing-blog-entries-ugc}

UGC는 중재에 대한 표준 방법 중 하나를 사용하여 중재해야 합니다.
사용자 [생성 컨텐츠 중재를 참조하십시오](/help/communities/moderate-ugc.md).

AEM 6.1 Communities의 경우, UGC용 [공용 스토어를](/help/communities/working-with-srp.md) 사용하면 선택한 스토리지 옵션(예: ASRP, MSRP 또는 JSRP)에 상관없이 프로그래머틱 방식으로 UGC에 액세스할 수 있습니다.

**저장소에서 UGC의 위치와 형식은 경고**&#x200B;없이 변경될 수 있습니다.

다음을 참조하십시오.

* [스토리지 자원 공급자 개요](/help/communities/srp.md) - 소개 및 저장소 사용 개요
* [SRP 및 UGC Essentials](/help/communities/srp-and-ugc.md) - SRP 유틸리티 방법 및 예제
* [SRP를 사용하여 UGC](/help/communities/accessing-ugc-with-srp.md) 액세스 - 코딩 지침
* [SocialUtils 리팩토링](/help/communities/socialutils.md) - 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑

## 기본 게시자 {#primary-publisher}

배포가 게시 팜인 경우 게시할 아티클에 대해 폴링할 기본 게시자를 식별해야 합니다.

자세한 [내용은 기본](/help/communities/deploy-communities.md#primary-publisher) 게시자를 참조하십시오.

## 리치 미디어 허용 {#allowing-rich-media}

AEM 플랫폼은

* [XSS(교차 사이트 스크립팅)로부터 보호](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

AEM 6.2부터 이전에 수동으로 수행해야 했던 수정 사항은 기본 AntiSamey 구성 파일에 포함됩니다.

리치 미디어는 `Embed Media from External Sites` 아이콘을 선택하여 블로그 아티클에 임베드됩니다.

![chlimage_1-199](assets/chlimage_1-199.png)

