---
title: 카탈로그 기본 사항
seo-title: Catalog Essentials
description: 카탈로그 개요
seo-description: Catalog overview
uuid: 788512bb-fa38-48fb-a769-1eaae6bb95a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 542467ef-3793-4347-8424-c365c5a166f6
exl-id: 4ca76b50-d56d-4f4d-be92-bf8929c5d754
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 2%

---

# 카탈로그 기본 사항 {#catalog-essentials}

이 페이지에서는 지원 커뮤니티 사이트의 카탈로그 기능을 사용하는 데 필요한 기본 정보를 제공합니다.

카탈로그 기능을 커뮤니티 사이트에 포함하면 커뮤니티 구성원이 카탈로그에 나열된 지원 리소스를 찾아보고 선택할 수 있습니다.

다음 [ `enablement catalog` 구성 요소](catalog.md) 커뮤니티 구성원이 카탈로그에 액세스할 수 있도록 허용 [지원 리소스](resources.md). AEM 태그 사용은 카탈로그에 있는 지원 리소스의 모양을 관리하는 중요한 부분입니다.

다음을 참조하십시오 [태그 지정 지원 리소스](tag-resources.md).

## 클라이언트측 핵심 사항 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/enablement/components/hbs/catalog</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>포함하기 쉬워</strong></a></td>
   <td>아니요</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.catalog<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
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
   <td>다음을 참조하십시오 <a href="catalog.md">카탈로그 기능</a></td>
  </tr>
 </tbody>
</table>

## 서버측 Essentials {#essentials-for-server-side}

### 카탈로그 기능 {#catalog-function}

다음을 포함하는 커뮤니티 사이트 구조 [카탈로그 기능](functions.md#catalog-function), 구성된 포함 `enablement catalog` 구성 요소.

### 사전 필터 {#pre-filters}

커뮤니티 사이트에 카탈로그 기능이 추가된 경우 사전 필터를 지정하여 카탈로그에 표시되는 활성화 리소스 및 학습 경로를 제한할 수 있습니다. 이 작업은 사이트에 대한 카탈로그 리소스의 인스턴스에 속성을 설정하여 수행됩니다.

의 예 사용 [지원 튜토리얼](getting-started-enablement.md):

* 작성자
* 사용 [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * 과 같은 [https://&lt;server>:&lt;port>/crx/de](http://localhost:4502/crx/de)

* 카탈로그 페이지의 카탈로그 리소스로 이동합니다.

   * 예, `/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* 하위 필터 노드 추가

   * 다음 항목 선택 `catalog`노드
   * 선택 **[!UICONTROL 노드 만들기]**

      * 이름: `filters`
      * 유형: `nt:unstructured`
      * 선택 **[!UICONTROL 모두 저장]**

* 추가 `se_resource-tags` 에 대한 속성 `filters` 노드

   * 다음 항목 선택 `filters` 노드
   * 다중 속성 추가

      * 이름: `se_resource-tags`
      * 유형: 문자열
      * 값: *&lt;enter a=&quot;&quot; span=&quot;&quot; id=&quot;1&quot; translate=&quot;no&quot; />태그 ID](#pre-filter-tagids)>*[
         * 선택 **[!UICONTROL 다중]**
         * 선택 **[!UICONTROL 추가]**

            * 팝업 대화 상자에서 다음을 선택합니다 `+` 사전 필터 TagID를 추가하려면

* 커뮤니티 사이트 다시 게시

![catalog 구성](assets/configure-catalog.png)

#### TagID 사전 필터링 {#pre-filter-tagids}

사전 필터 [태그 ID](../../help/sites-developing/framework.md#tagid) 은(는) 지원 리소스에 적용된 태그와 정확히 일치해야 합니다. 다음 화면에 표시됩니다. `resources` 속성 값으로 사이트에 대한 폴더 `se_resource-tags`.

![필터 구성](assets/configure-catalog1.png)

### 참조 API {#reference-apis}

* [지원 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [보고 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [Reporting Analytics API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/model/api/package-summary.html)
