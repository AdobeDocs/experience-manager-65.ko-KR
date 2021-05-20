---
title: 카탈로그 핵심 사항
seo-title: 카탈로그 핵심 사항
description: 카탈로그 개요
seo-description: 카탈로그 개요
uuid: 788512bb-fa38-48fb-a769-1eaae6bb95a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 542467ef-3793-4347-8424-c365c5a166f6
exl-id: 4ca76b50-d56d-4f4d-be92-bf8929c5d754
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 2%

---

# 카탈로그 필수 패키지 {#catalog-essentials}

이 페이지에서는 지원 커뮤니티 사이트의 카탈로그 기능 작업에 필요한 필수 정보를 제공합니다.

커뮤니티 사이트에 포함된 카탈로그 기능을 통해 커뮤니티 구성원은 카탈로그에 나열된 지원 리소스를 검색하고 선택할 수 있습니다.

[ `enablement catalog` 구성 요소](catalog.md)를 사용하면 커뮤니티 구성원이 [지원 리소스](resources.md)의 카탈로그에 액세스할 수 있습니다. AEM 태그를 사용하는 것은 카탈로그에서 지원 리소스의 모양을 관리하는 중요한 부분입니다.

[태깅 지원 리소스](tag-resources.md)를 참조하십시오.

## 클라이언트측 {#essentials-for-client-side}에 대한 필수 사항

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
   <td>cq.social.enablement.hbs.breadcrums<br /> cq.social.enablement.hbs.catalog<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learning path</td>
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
   <td><a href="catalog.md">카탈로그 기능</a>을 참조하십시오</td>
  </tr>
 </tbody>
</table>

## 서버측 {#essentials-for-server-side}에 대한 필수 사항

### 카탈로그 기능 {#catalog-function}

[카탈로그 함수](functions.md#catalog-function)를 포함하는 커뮤니티 사이트 구조는 구성된 `enablement catalog` 구성 요소를 포함합니다.

### 사전 필터 {#pre-filters}

커뮤니티 사이트에 카탈로그 기능이 추가되면 사전 필터를 지정하여 카탈로그에 표시되는 지원 리소스 및 학습 경로를 제한할 수 있습니다. 이 작업은 사이트에 대한 카탈로그 리소스의 인스턴스에 속성을 설정하여 수행됩니다.

[지원 자습서](getting-started-enablement.md)의 예제 사용:

* 작성자 시
* [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md) 사용

   * 예: [https://&lt;server>:&lt;port>/crx/de](http://localhost:4502/crx/de)

* 카탈로그 페이지의 카탈로그 리소스로 이동합니다

   * 예, `/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* 하위 필터 노드 추가

   * `catalog`노드를 선택합니다
   * **[!UICONTROL 노드 만들기]** 를 선택합니다.

      * 이름: `filters`
      * 유형: `nt:unstructured`
      * **[!UICONTROL 모두 저장]** 선택

* `filters` 노드에 `se_resource-tags` 속성 추가

   * `filters` 노드를 선택합니다
   * 다중 속성 추가

      * 이름: `se_resource-tags`
      * 유형:문자열
      * 값:*[TagID](#pre-filter-tagids)* 입력
         * **[!UICONTROL Multi]** 선택
         * **[!UICONTROL 추가]** 선택

            * 팝업 대화 상자에서 `+` 을 선택하여 추가 사전 필터 TagID를 추가합니다

* 커뮤니티 사이트 다시 게시

![configure-catalog](assets/configure-catalog.png)

#### TagID 사전 필터링 {#pre-filter-tagids}

사전 필터 [TagID](../../help/sites-developing/framework.md#tagid)는 지원 리소스에 적용된 태그와 정확히 일치해야 합니다. 이는 `se_resource-tags` 속성의 값으로 사이트의 `resources` 폴더에 표시됩니다.

![configure-filters](assets/configure-catalog1.png)

### 참조 API {#reference-apis}

* [지원 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/api/package-summary.html)

* [보고 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/api/package-summary.html)

* [Reporting Analytics API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/analytics/api/package-summary.html)
