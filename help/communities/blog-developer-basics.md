---
title: 블로그 기본 사항
description: 로그인한 커뮤니티 구성원이 블로그 문서를 게시할 수 있도록 페이지에 블로그 기능을 추가하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 51f616e8-4aba-47f6-b948-d5147d84bbb6
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 2%

---

# 블로그 기본 사항 {#blog-essentials}

AEM 6.1 커뮤니티에서 블로그는 커뮤니티 활동입니다. 이제 블로그 기사는 게시 환경에서 게시되며, 이전에는 작성 환경에서만 블로그 기사를 만들고 게시할 수 있었습니다.

이제 권한이 있는 구성원으로 제한되지 않는 한 모든 커뮤니티 구성원이 블로그 문서를 만들 수 있습니다.

이 페이지에서는 블로그 기능을 사용하는 데 필요한 기본 정보를 제공합니다.

>[!NOTE]
>
>블로그 기능의 기본 인프라는 저널 기능입니다.

## 클라이언트측 핵심 사항 {#essentials-for-client-side}

블로그 기능은 [블로그 기능](/help/communities/functions.md#blog-function)을 추가하거나 작성자 편집 모드에서 페이지에 구성 요소를 추가하여 사용할 수 있는 두 가지 기본 구성 요소로 구성됩니다.

### 블로그 {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/journal/components/hbs/journal</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>포함 가능</strong></a></td>
   <td>아니요</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.journal</td>
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
   <td><a href="/help/communities/blog-feature.md">블로그 기능</a> 보기</td>
  </tr>
 </tbody>
</table>

### 블로그 세로 막대 {#blog-sidebar}

| **resourceType** | social/journal/components/hbs/sidebar |
|---|---|
| [**포함 가능**](/help/communities/scf.md#add-or-include-a-communities-component) | 아니요 |
| [**clientllibs**](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **템플릿** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **속성** | [블로그 기능](/help/communities/blog-feature.md) 보기 |

* [클라이언트측 사용자 지정](/help/communities/client-customize.md)

## 서버측 Essentials {#essentials-for-server-side}

* [블로그 API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [블로그 끝점](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [서버측 사용자 지정](/help/communities/server-customize.md)

### 블로그 기능 {#blog-function}

[블로그 기능](/help/communities/functions.md#blog-function)을 포함하는 커뮤니티 사이트 구조에 `Blog` 및 `Blog Sidebar` 구성 요소가 구성되어 있습니다. 블로그 기능은 [권한이 있는 구성원 사용자 그룹](/help/communities/users.md#privileged-members-group)을(를) 식별할 수 있도록 지원합니다.

### UGC(블로그 게시물 액세스) {#accessing-blog-entries-ugc}

UGC는 중재에 대한 표준 방법 중 하나를 사용하여 중재되어야 합니다.
[사용자 생성 콘텐츠 중재](/help/communities/moderate-ugc.md)를 참조하십시오.

AEM 6.1 커뮤니티에서 UGC에 대한 [일반 저장소](/help/communities/working-with-srp.md)를 사용하면 선택한 저장소 옵션(예: ASRP, MSRP 또는 JSRP)에 관계없이 UGC에 프로그래밍 방식으로 액세스할 수 있습니다.

**저장소에서 UGC의 위치 및 형식은 경고 없이 변경될 수 있습니다**.

를 참조하십시오.

* [저장소 리소스 공급자 개요](/help/communities/srp.md) - 소개 및 저장소 사용 개요.
* [SRP 및 UGC Essentials](/help/communities/srp-and-ugc.md) - SRP 유틸리티 메서드 및 예제.
* [SRP를 사용하여 UGC에 액세스](/help/communities/accessing-ugc-with-srp.md) - 코딩 지침.
* [SocialUtils 리팩터링](/help/communities/socialutils.md) - 더 이상 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.

## 기본 게시자 {#primary-publisher}

배포가 게시 팜인 경우 게시가 예정된 문서를 폴링하는 기본 게시자를 식별해야 합니다.

자세한 내용은 [기본 게시자](/help/communities/deploy-communities.md#primary-publisher)를 참조하십시오.

## 리치 미디어 허용 {#allowing-rich-media}

AEM 플랫폼은에 설명된 대로 XSS 공격을 방지하기 위해 다른 웹 사이트에서 링크를 차단합니다.

* [XSS(크로스 사이트 스크립팅)에 대한 Protect](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

AEM 6.2부터는 이전에 수동으로 수행해야 했던 수정 사항이 기본 AntiSamy 구성 파일에 포함되어 있습니다.

리치 미디어는 `Embed Media from External Sites` 아이콘을 선택하여 블로그 문서에 포함됩니다.

![미디어](assets/media-icon.png)
