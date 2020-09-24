---
title: Catalog Essentials
seo-title: Catalog Essentials
description: 카탈로그 개요
seo-description: 카탈로그 개요
uuid: 788512bb-fa38-48fb-a769-1eaae6bb95a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 542467ef-3793-4347-8424-c365c5a166f6
translation-type: tm+mt
source-git-commit: 41de9fff615b5b2f77d835740dfb1d33aa81e59b
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 2%

---


# Catalog Essentials {#catalog-essentials}

이 페이지에서는 활성 커뮤니티 사이트의 카탈로그 기능을 사용하여 작업하는 데 필요한 정보를 제공합니다.

커뮤니티 사이트에 포함된 카탈로그 기능을 통해 커뮤니티 구성원은 카탈로그에 나열된 활성 리소스를 검색하고 선택할 수 있습니다.

이 구성 요소 [ 를 사용하면 커뮤니티 구성원이 `enablement catalog` 활성 리소스 카탈로그에 액세스할 수 있습니다](catalog.md) [](resources.md). AEM 태그의 사용은 카탈로그의 활성 리소스 모양을 관리하는 데 중요한 부분입니다.

활성 리소스 [태그 지정을 참조하십시오](tag-resources.md).

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/enablement/components/hbs/catalog</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>포함 가능</strong></a></td>
   <td>아니오</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.enablcement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.catalog<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.lear닝경로</td>
  </tr>
  <tr>
   <td> <strong>템플릿</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/catalog.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/clientlibs/catalog.css</td>
  </tr>
  <tr>
   <td><strong> 속성</strong></td>
   <td>카탈로그 <a href="catalog.md">기능 보기</a></td>
  </tr>
 </tbody>
</table>

## Essentials for Server-Side {#essentials-for-server-side}

### 카탈로그 기능 {#catalog-function}

[ [카탈로그] 기능을](functions.md#catalog-function)포함하는 커뮤니티 사이트 구조에는 구성된 구성 `enablement catalog` 요소가 포함됩니다.

### 사전 필터 {#pre-filters}

커뮤니티 사이트에 Catalog 함수가 추가되면 사전 필터를 지정하여 카탈로그에 표시되는 활성 리소스 및 학습 경로를 제한할 수 있습니다. 사이트에 대한 카탈로그 리소스 인스턴스의 속성을 설정하여 이 작업을 수행합니다.

활성 자습서의 [예](getting-started-enablement.md)사용:

* 작성자
* CRXDE [사용](../../help/sites-developing/developing-with-crxde-lite.md)

   * 예: [https://&lt;server>:&lt;port>/crx/de](http://localhost:4502/crx/de)

* 카탈로그 페이지에서 카탈로그 리소스로 이동합니다.

   * 예, `/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* 하위 필터 노드 추가

   * 노드 `catalog`선택
   * 노드 **[!UICONTROL 만들기 선택]**

      * 이름: `filters`
      * 유형: `nt:unstructured`
      * 모두 **[!UICONTROL 저장 선택]**

* 노드에 `se_resource-tags` 속성 `filters` 추가

   * 노드 `filters` 선택
   * 다중 속성 추가

      * 이름: `se_resource-tags`
      * 유형:문자열
      * 값: *&lt;[TagID 입력](#pre-filter-tagids)>*
         * 다중 **[!UICONTROL 선택]**
         * 추가 **[!UICONTROL 선택]**

            * 팝업 대화 상자에서 추가 사전 필터 TagID `+` 를 추가하려면 선택합니다.

* 커뮤니티 사이트 다시 게시

![configure-catalog](assets/configure-catalog.png)

#### 태그 ID 사전 필터링 {#pre-filter-tagids}

사전 필터 [TagID는](../../help/sites-developing/framework.md#tagid) 활성 리소스에 적용된 태그와 정확히 일치해야 합니다. 사이트의 `resources` 폴더에서 속성 값으로 볼 수 있습니다 `se_resource-tags`.

![configure-filters](assets/configure-catalog1.png)

### 참조 API {#reference-apis}

* [활성 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/api/package-summary.html)

* [보고 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/api/package-summary.html)

* [보고 분석 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/analytics/api/package-summary.html)

