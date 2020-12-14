---
title: Tag Essentials
seo-title: Tag Essentials
description: 태그 개요
seo-description: 태그 개요
uuid: a5d52319-f821-4608-b0ab-abc8a1374343
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d355a3ee-c8a8-4a07-8d28-d1a99bda315c
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 3%

---


# 태그 필수 항목 {#tag-essentials}

AEM Communities 구성 요소가 태그 지정이 활성화되어 있으면 커뮤니티 구성원은 게시 환경에서 게시하는 컨텐츠에 태그를 지정할 수 있습니다.

게시 환경에 적용된 태그의 기본 인프라는 페이지 및 자산과 같은 작성 환경의 컨텐츠에 적용되는 태그와 동일합니다.

* 태그 만들기 및 관리에 대한 자세한 내용은 [태그 관리](../../help/sites-administering/tags.md) 및 [사용자 생성 컨텐트 태그 지정](tag-ugc.md)(UGC)을 참조하십시오.

* [사용자 지정 응용 프로그램](../../help/sites-developing/building.md)에서 태그를 포함 및 확장하는 방법과 [태깅 프레임워크](../../help/sites-developing/framework.md)에 대한 자세한 내용은 [개발자용 태그 지정](../../help/sites-developing/tags.md)을 참조하십시오.

* 게시 환경에서 UGC에 적용된 태그를 강조 표시하기 위해 페이지에 `social tag cloud` 구성 요소를 추가하는 방법에 대한 작성자의 자세한 내용은 [소셜 태그 클라우드 사용](tagcloud.md)을 참조하십시오.

* 카탈로그의 리소스 태그 지정에 대한 자세한 내용은 [태깅 지원 리소스](tag-resources.md)를 참조하십시오.

[커뮤니티 사이트](sites-console.md#tagging) 또는 다음 기능 중 하나를 구성할 때 UGC 태깅을 활성화할 수 있습니다.

* [블로그](blog-feature.md)
* [달력](calendar.md)
* [파일 라이브러리](file-library.md)
* [포럼](forum.md)
* [QnA](working-with-qna.md)

## Essentials for Client-Side {#essentials-for-client-side}

### 소셜 태그 클라우드 {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>includable</strong></a></td>
   <td>아니오</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.tagcloud</td>
  </tr>
  <tr>
   <td> <strong>템플릿</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/tagcloud.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/clientlibs/tagcloud.css</td>
  </tr>
  <tr>
   <td><strong>속성</strong></td>
   <td><a href="tagcloud.md">소셜 태그 클라우드 사용</a> 참조</td>
  </tr>
 </tbody>
</table>

* [클라이언트측 사용자 지정](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [소셜 태그 클라우드 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [소셜 태그 관리자](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [서버측 사용자 정의](server-customize.md)

## 태그 검색 {#tag-searching}

[기능 팩 1](deploy-communities.md#latestfeaturepack)(FP1)부터 [태그 제목](../../help/sites-developing/framework.md#tag-characteristics)을 사용하여 태그 검색이 수행됩니다.

FP1 이전에는 [태그 id](../../help/sites-developing/framework.md#tagid)를 사용하여 검색이 수행되었습니다.
