---
title: 태그 기본 사항
seo-title: Tag Essentials
description: 태그 개요
seo-description: Tag overview
uuid: a5d52319-f821-4608-b0ab-abc8a1374343
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d355a3ee-c8a8-4a07-8d28-d1a99bda315c
exl-id: 6e8af8cf-1239-46f9-b2fe-4aa80abc86ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 3%

---

# 태그 기본 사항 {#tag-essentials}

AEM Communities 구성 요소가 태그 지정이 활성화된 상태로 구성되면 커뮤니티 구성원은 게시 환경에서 게시하는 콘텐츠에 태그를 지정할 수 있습니다.

게시 환경에 적용된 태그의 기본 인프라는 작성 환경의 콘텐츠에 적용된 태그(예: 페이지 및 에셋)와 동일합니다.

* 다음을 참조하십시오 [태그 관리](../../help/sites-administering/tags.md) 및 [사용자 생성 컨텐츠 태깅](tag-ugc.md) (UGC) 를 참조하십시오.

* 다음을 참조하십시오 [개발자를 위한 태깅](../../help/sites-developing/tags.md) 에 대한 자세한 내용은 [태깅 프레임워크](../../help/sites-developing/framework.md) 에서 태그를 포함 및 확장할 수 있습니다. [사용자 정의 애플리케이션](../../help/sites-developing/building.md).

* 다음을 참조하십시오 [소셜 태그 클라우드 사용](tagcloud.md) 추가 방법에 대한 작성자 정보 `social tag cloud` 구성 요소를 페이지에 추가하여 게시 환경에서 UGC에 적용된 태그를 강조 표시할 수 있습니다.

* 다음을 참조하십시오 [태그 지정 지원 리소스](tag-resources.md) 카탈로그의 리소스에 태깅하는 방법에 대한 정보입니다.

다음을 구성할 때 UGC의 태깅을 활성화할 수 있습니다. [커뮤니티 사이트](sites-console.md#tagging) 또는 다음 기능 중 하나를 사용할 수 있습니다.

* [블로그](blog-feature.md)
* [달력](calendar.md)
* [파일 라이브러리](file-library.md)
* [포럼](forum.md)
* [QnA](working-with-qna.md)

## 클라이언트측 핵심 사항 {#essentials-for-client-side}

### 소셜 태그 클라우드 {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>포함하기 쉬워</strong></a></td>
   <td>아니요</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
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
   <td>다음을 참조하십시오 <a href="tagcloud.md">소셜 태그 클라우드 사용</a></td>
  </tr>
 </tbody>
</table>

* [클라이언트측 사용자 지정](client-customize.md)

## 서버측 Essentials {#essentials-for-server-side}

* [소셜 태그 클라우드 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [소셜 태그 관리자](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [서버측 사용자 지정](server-customize.md)

## 태그 검색 {#tag-searching}

기준: [기능 팩 1](deploy-communities.md#latestfeaturepack) (FP1), 태그 검색은 [태그 제목](../../help/sites-developing/framework.md#tag-characteristics).

FP1 이전에는 다음을 사용하여 검색을 수행했습니다. [태그 id](../../help/sites-developing/framework.md#tagid).
