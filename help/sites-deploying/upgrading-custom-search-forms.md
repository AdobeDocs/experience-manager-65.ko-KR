---
title: 사용자 지정 검색 Forms 업그레이드
seo-title: Upgrading Custom Search Forms
description: 이 문서에서는 사용자 지정 검색 양식이 작동하도록 업그레이드 후 필요한 조정에 대해 자세히 설명합니다.
seo-description: This article details the adjustments that are required after an upgrade in order for the custom search forms to function.
uuid: 35b8fbb9-5951-4e1c-bf04-4471a55b9cb0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: a08cee9c-e981-4483-8bdc-e6353977f854
feature: Upgrading
exl-id: 797bbdf9-917a-4537-a5f9-bf2682db968b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1685'
ht-degree: 3%

---

# 사용자 지정 검색 Forms 업그레이드{#upgrading-custom-search-forms}

AEM 6.2에서 사용자 지정된 검색 Forms이 저장소에 저장되는 위치가 변경되었습니다. 업그레이드 시 6.1의 위치에서 다음 위치로 이동됩니다.

* /apps/cq/gui/content/facets

아래와 같이 새 위치를 지정합니다.

* /conf/global/settings/cq/search/facets

이러한 이유로 양식이 계속 작동하려면 업그레이드 후 수동으로 조정해야 합니다.

이는 사용자 지정된 기본 Forms과 새 검색 Forms에 적용됩니다.

자세한 내용은 [검색 패싯](/help/assets/search-facets.md).

## resourceType 속성 변경 {#changing-the-resourcetype-property}

별도로 명시하지 않는 한 업그레이드 후 수행해야 하는 대부분의 조정 작업은 `sling:resourceType` 구성된 사용자 지정 검색 Forms에 대한 속성입니다. 속성이 렌더링 스크립트의 올바른 위치를 가리키도록 해야 합니다.

다음을 수행하여 속성을 변경할 수 있습니다.

1. 로 이동하여 CRXDE Lite 열기 `https://server:port/crx/de/index.jsp`
1. 목록에서 지정한 대로 조정해야 하는 노드의 위치를 찾습니다 [사용자 지정 검색 Forms](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms) 아래의 제품에서 사용할 수 있습니다.
1. 노드를 클릭합니다. 오른쪽 속성 창에서 을(를) 클릭하고 을(를) 수정합니다 **sling:resourceType** 속성을 사용합니다.
1. 마지막으로, **모두 저장** 버튼을 클릭합니다.

## 사용자 지정 검색 Forms 목록 {#list-of-custom-search-forms}

아래에서는 모든 사용자 지정 검색 Forms 목록과 업그레이드 후 필요한 수정 사항을 확인할 수 있습니다. 이 이름들은 `/conf/global/settings/cq/search/facets/sites/items`.

### 노드 이름이 &quot;fulltext&quot;인 전체 텍스트 설명 {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>6.1에서 기본 검색 양식의 노드/초</td>
   <td>전체 텍스트</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicate/fulltext 설명</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td>해당 없음</td>
  </tr>
 </tbody>
</table>

AEM 6.1에서는 표준 전체 텍스트 설명이 검색 양식의 일부였습니다. 6.2에서 전체 텍스트 필드가 OmniSearch로 대체되었습니다. 이 조건자는 프로그래밍 방식으로 생략되며 제거할 수 있습니다.

**작업:** 노드를 완전히 제거합니다.

### 기타 전체 텍스트 설명 {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1에서 기본 검색 노드/초</td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicate/fulltext 설명</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>공통/관리/사용자 지정/검색 설명/전체 텍스트 설명</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 조정 `resourceType` 속성(추가)**/coral**&quot; 위에 표시된 6.2 위치의 경우처럼)

### 경로 브라우저 설명 {#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1에서 기본 검색 양식의 노드/초<br /> <br /> </td>
   <td>경로</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicate/pathpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>공통/관리/사용자 지정 검색/검색 설명/경로 설명</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 조정 `resourceType` 속성(추가)**/coral**&quot; 위에 표시된 6.2 위치의 경우처럼)

### 태그 설명 {#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1에서 기본 검색 양식의 노드/초<br /> <br /> </td>
   <td>태그</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicate/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicate/tagspredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 조정 **resourceType** 속성(추가)**/coral**&quot; 위에 표시된 6.2 위치의 경우처럼)

### 페이지 상태 설명 {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1에서 기본 검색 양식의 노드/초<br /> <br /> </td>
   <td>pagestatusprediction</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/searchpredicate/pagestatestatestatestate조건자</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td>해당 없음</td>
  </tr>
 </tbody>
</table>

페이지 상태가 게시 및 LiveCopy 상태에 대한 옵션 속성 설명, 즉 두 개의 옵션 속성으로 대체되었습니다.

**액션:**

* 제거 `pagestatuspredicate` 노드
* 노드 복사

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * 끝 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 노드 복사

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * 끝 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 설정 `listOrder` 에 대한 속성 `analyticspredicate` 노드 -**8**&quot;. 충돌을 피하려면 이것은 필요하다.

### 날짜 범위 설명 {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1에서 기본 검색 양식의 노드/초<br /> <br /> </td>
   <td>daterangepredicate</td>
  </tr>
  <tr>
   <td>6.1의 리소스 유형</td>
   <td>cq/gui/components/common/admin/customsearch/searchpredicate/daterangepredicate</td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>일반/관리/사용자 지정 검색/검색 설명/daterangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 조정 `resourceType` 속성(추가)**/coral**&quot; 위에 표시된 6.2 위치의 경우처럼)

### 숨겨진 필터 {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>6.1에서 기본 검색 양식의 노드/초<br /> <br /> </td>
   <td>유형</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 조정할 게 없어요

### 분석 조건자 {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1에서 기본 검색 양식의 노드/초<br /> <br /> </td>
   <td>analyticspredictive</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/searchpredicate/analyticspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicate/analyticspredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 조정 `resourceType` 속성(추가)**/coral**&quot; 위에 표시된 6.2 위치의 경우처럼)

### 범위 조건자 {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1에서 기본 검색 양식의 노드/초<br /> <br /> </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/searchpredicate/rangepredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicate/rangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 조정 `resourceType` 속성(추가)**/coral**&quot; 위에 표시된 6.2 위치의 경우처럼)

>[!NOTE]
>
>참고: 6.1과 달리 범위 조건부는 더 이상 검색 막대에서 태그를 렌더링하지 않습니다.

### 옵션 속성 조건자 {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1에서 기본 검색 양식의 노드/초<br /> <br /> </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/searchpredicate/optionspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicate/optionspredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 조정 `resourceType` 속성(추가)**/coral**&quot; 위에 표시된 6.2 위치의 경우처럼)

### 슬라이더 범위 조건자 {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1에서 기본 검색 양식의 노드/초<br /> <br /> </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/searchpredicate/sliderrangepredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicate/sliderrangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 조정 `resourceType` 속성(추가)**/coral**&quot; 위에 표시된 6.2 위치의 경우처럼)

### 구성 요소 조건자 {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1에서 기본 검색 양식의 노드/초<br /> <br /> </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/searchpredicate/componentspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicate/componentspredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 조정 `resourceType` 속성(추가)**/coral**&quot; 위에 표시된 6.2 위치의 경우처럼)

### 작성자 조건자 {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1에서 기본 검색 양식의 노드/초<br /> <br /> </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/searchpredicate/userpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicate/userpredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 조정 `resourceType` 속성(추가)**/coral**&quot; 위에 표시된 6.2 위치의 경우처럼)

### 템플릿 조건자 {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1에서 기본 검색 양식의 노드/초<br /> <br /> </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/searchpredicate/templatest술어</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicate/templatestpredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 조정 `resourceType` 속성(추가)**/coral**&quot; 위에 표시된 6.2 위치의 경우처럼)

## 자산 관리자 검색 레일 {#assets-admin-search-rail}

아래 노드는 의 이름을 참조합니다. `/conf/global/settings/dam/search/facets/assets/items`

### 노드 이름이 &quot;fulltext&quot;인 전체 텍스트 설명 {#fulltext-predicate-with-node-name-fulltext-1}

| 6.1에서 기본 검색 양식의 노드/초 | 전체 텍스트 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicate/fulltext 설명 |
| 6.2의 리소스 유형 | 해당 없음 |

6.1에서는 표준 전체 텍스트 설명이 검색 양식의 일부였습니다. 6.2에서 전체 텍스트 필드가 OmniSearch로 대체되었습니다. 이 조건자는 프로그래밍 방식으로 생략되며 제거할 수 있습니다.

**작업:** 위에 언급된 노드를 제거합니다.

### 경로 브라우저 설명 {#path-browser-predicates-1}

| 6.1에서 기본 검색 양식의 노드/초 | 경로 브라우저 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicate/pathbrowserpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicate/pathbrowserpredicate |

**작업:** 조정 `resourceType` 속성(추가)**/coral**&quot; 위에 표시된 6.2 위치의 경우처럼)

### MIME 유형 설명 {#mime-type-predicates}

| 6.1에서 기본 검색 양식의 노드/초 | mime 유형 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicate/optionsDisdicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicate/options사전지정 |

**작업:** 조정 `resourceType` 속성(추가)**/coral**&quot; 위에 표시된 6.2 위치의 경우처럼)

### 파일 크기 설명 {#file-size-predicates}

| 6.1에서 기본 검색 양식의 노드/초 | 파일 크기 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicate/filesizepredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicate/sliderange술어 |

**작업:** 조정 `resourceType` 위의 6.2 위치에 표시된 대로,

### 마지막으로 수정된 자산 설명 {#asset-last-modified-predicates}

| 6.1에서 기본 검색 양식의 노드/초 | assetlastmodifiedpredicate |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicate/assetlastmodifiedpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicate/assetlastmodifedpredicate |

작업: resourceType 속성을 조정합니다(위에 표시된 6.2 위치에 &quot;/coral&quot;을 추가합니다.).

### 게시 설명 {#publish-predicate}

| 6.1에서 기본 검색 양식의 노드/초 | 페이지를 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicate/publishpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicate/publishpredicate |

**액션:**

* 조정 `resourceType` 속성(추가)**/coral**&quot;(위에 표시된 6.2 위치 참조)

* 추가 `optionPaths` (String 유형) 속성 값: `/libs/dam/options/predicates/publish`

* 추가 `singleSelect` 부울 값이 있는 속성 `true`.

### 상태 설명 {#status-predicates}

| 6.1에서 기본 검색 양식의 노드/초 | 상태 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicate/optionsDisdicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicate/options사전지정 |

**작업:** 조정 `resourceType` 속성(추가)**/coral**&quot;(위에 표시된 6.2 위치 참조)

### 만료 상태 설명 {#expiry-status-predicates}

| 6.1에서 기본 검색 양식의 노드/초 | 만료 상태 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicate/expiredassetpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicate/expiredassetpredicate |

**작업:** 조정 `resourceType` 속성(추가)**/coral**&quot;(위에 표시된 6.2 위치 참조)

### 메타데이터 유효성 설명 {#metadata-validity-predicates}

| 6.1에서 기본 검색 양식의 노드/초 | 메타데이터 가산 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicate/optionsDisdicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicate/options사전지정 |

**작업:** 조정 `resourceType` 속성(추가)**/coral**&quot;(위에 표시된 6.2 위치 참조)

### 등급 예측 {#rating-predicates}

| 6.1에서 기본 검색 양식의 노드/초 | 등급 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicate/ratingpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicate/sliderange술어 |

**작업:** 조정 `resourceType` 속성(추가)**/coral**&quot;(위에 표시된 6.2 위치 참조)

### 방향 설명 {#orientation-predicate}

| 6.1에서 기본 검색 양식의 노드/초 | 방향 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicate/tagsfilterpredicate |
| 6.2의 리소스 유형 | cq/gui/components/coral/common/admin/customsearch/searchpredicate/tagspredicate |

**액션:**

* 조정 `resourceType` 속성(추가)**/coral**&quot;(위에 표시된 6.2 위치 참조)

* 추가 `fieldLabel` 값과 동일한 값을 갖는 속성 `text` 동일한 노드의 속성입니다.

* 추가 `emptyText` 값과 동일한 값을 갖는 속성 `text` 동일한 노드의 속성입니다.

* 추가 `rootPath` 값과 동일한 값을 갖는 속성 `optionPaths` 동일한 노드의 속성입니다.

### 스타일 설명 {#style-predicate}

| 6.1에서 기본 검색 양식의 노드/초 | 화면 위치가 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicate/tagsfilterpredicate |
| 6.2의 리소스 유형 | cq/gui/components/coral/common/admin/customsearch/searchpredicate/tagspredicate |

**액션:**

* 조정 `resourceType` 속성(추가)**/coral**&quot;(위에 표시된 6.2 위치 참조)

* 추가 `fieldLabel` 값과 동일한 값을 갖는 속성 `text` 동일한 노드의 속성입니다.

* 추가 `emptyText` 값과 동일한 값을 갖는 속성 `text` 동일한 노드의 속성입니다.

* 추가 `rootPath` 값과 동일한 값을 갖는 속성 `optionPaths` 동일한 노드의 속성입니다.

### 비디오 형식 설명 {#video-format-predicates}

| 6.1에서 기본 검색 양식의 노드/초 | videoFormat |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicate/optionsDisdicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicate/options사전지정 |

**작업:** 조정 `resourceType` 속성(추가)**/coral**&quot;(위에 표시된 6.2 위치 참조)

### 기본 자산 설명 {#mainasset-predicate}

| 6.1에서 기본 검색 양식의 노드/초 | 유지 관리 |
|---|---|
| 6.1의 리소스 유형 | granite/ui/components/foundation/form/hidden |
| 6.2의 리소스 유형 | granite/ui/components/coral/foundation/form/hidden |

**작업:** 조정 `resourceType` 속성(추가)**/coral**&quot;(위에 표시된 6.2 위치 참조)
