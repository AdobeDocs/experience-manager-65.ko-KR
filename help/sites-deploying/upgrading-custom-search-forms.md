---
title: 사용자 정의 검색 Forms 업그레이드
description: 이 문서에서는 사용자 정의 검색 양식이 작동하기 위해 업그레이드 후 필요한 조정 사항에 대해 자세히 설명합니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: 797bbdf9-917a-4537-a5f9-bf2682db968b
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1797'
ht-degree: 2%

---

# 사용자 정의 검색 Forms 업그레이드{#upgrading-custom-search-forms}

AEM 6.2에서 저장소에 저장된 사용자 지정 검색 Forms의 위치가 변경되었습니다. 업그레이드 시 6.1의 다음 위치에서 이동됩니다.

* /apps/cq/gui/content/facet

아래의 새 위치로:

* /conf/global/settings/cq/search/facet

따라서 양식이 계속 작동하려면 업그레이드 후 수동으로 조정해야 합니다.

이는 맞춤화된 새 검색 Forms 및 기본 Forms에 적용됩니다.

자세한 내용은 [검색 패싯](/help/assets/search-facets.md)에 대한 설명서를 참조하세요.

## resourceType 속성 변경 {#changing-the-resourcetype-property}

달리 명시되지 않은 경우 업그레이드 후 수행해야 하는 대부분의 조정에서는 구성된 사용자 지정 검색 Forms에 대한 `sling:resourceType` 속성을 변경해야 합니다. 속성이 렌더링 스크립트의 올바른 위치를 가리키도록 해야 합니다.

다음을 수행하여 속성을 변경할 수 있습니다.

1. `https://server:port/crx/de/index.jsp`(으)로 이동하여 CRXDE Lite 열기
1. 아래 [사용자 지정 검색 Forms](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms) 목록에 지정된 대로 조정할 노드의 위치를 찾습니다.
1. 노드를 클릭합니다. 오른쪽 속성 창에서 **sling:resourceType** 속성을 클릭하여 수정합니다.
1. 마지막으로 **모두 저장** 단추를 눌러 변경 사항을 저장합니다.

## 사용자 지정 검색 Forms 목록 {#list-of-custom-search-forms}

아래에는 모든 사용자 정의 검색 Forms 목록과 업그레이드 후 필요한 수정 사항이 나와 있습니다. `/conf/global/settings/cq/search/facets/sites/items`의 이름을 참조합니다.

### 노드 이름이 &quot;fulltext&quot;인 전체 텍스트 조건자 {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>6.1의 기본 검색 양식에 있는 노드</td>
   <td>전체 텍스트</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td>해당 사항 없음</td>
  </tr>
 </tbody>
</table>

AEM 6.1에서 표준 전체 텍스트 조건자는 검색 양식의 일부였습니다. 6.2에서 전체 텍스트 필드가 OmniSearch로 대체되었습니다. 이 조건자는 프로그래밍 방식으로 건너뛰며 제거할 수 있습니다.

**작업:** 노드를 완전히 제거하십시오.

### 기타 전체 텍스트 술어 {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1에서 기본 검색의 노드</td>
   <td>해당 사항 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 경로 브라우저 조건자 {#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식에 있는 노드 </td>
   <td>경로</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 태그 술어 {#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식에 있는 노드 </td>
   <td>태그</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** **resourceType** 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 페이지 상태 설명 {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식에 있는 노드 </td>
   <td>pagestatuspredicate</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/pagestatuspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td>해당 사항 없음</td>
  </tr>
 </tbody>
</table>

페이지 상태가 게시와 LiveCopy 상태, 이렇게 두 개의 옵션 속성 술어로 대체되었습니다.

**작업:**

* `pagestatuspredicate` 노드 제거
* 노드 복사

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * `/conf/global/settings/cq/search/facets/sites/jcr:content/items`에

* 노드 복사

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * `/conf/global/settings/cq/search/facets/sites/jcr:content/items`에

* `analyticspredicate` 노드의 `listOrder` 속성을 &quot;**8**&quot;(으)로 설정해야 합니다. 이것은 충돌을 피하기 위해 필요합니다.

### 날짜 범위 술어 {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식에 있는 노드 </td>
   <td>daterangepredicate</td>
  </tr>
  <tr>
   <td>6.1의 리소스 유형</td>
   <td>cq/gui/components/common/admin/customsearch/searchpredicates/daterangepredicate</td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/daterangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 숨겨진 필터 {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식에 있는 노드 </td>
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

**작업:** 조정할 항목이 없습니다.

### 분석 조건자 {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식에 있는 노드 </td>
   <td>분석 예측</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/analyticpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/analyticpredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 범위 조건자 {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식에 있는 노드 </td>
   <td>해당 사항 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/rangepredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/rangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

>[!NOTE]
>
>참고: 6.1과 반대로 범위 조건자는 더 이상 검색 막대에서 태그를 렌더링하지 않습니다.

### 옵션 속성 조건자 {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식에 있는 노드 </td>
   <td>해당 사항 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/optionpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/optionpredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 슬라이더 범위 조건자 {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식에 있는 노드 </td>
   <td>해당 사항 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 구성 요소 조건자 {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식에 있는 노드 </td>
   <td>해당 사항 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/componentpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/componentpredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 작성자 조건자 {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식에 있는 노드 </td>
   <td>해당 사항 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 템플릿 조건자 {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식에 있는 노드 </td>
   <td>해당 사항 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/templatepredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/templatepredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

## 자산 관리자 검색 레일 {#assets-admin-search-rail}

아래 노드는 `/conf/global/settings/dam/search/facets/assets/items`의 이름을 참조합니다.

### 노드 이름이 &quot;fulltext&quot;인 전체 텍스트 조건자 {#fulltext-predicate-with-node-name-fulltext-1}

| 6.1의 기본 검색 양식에 있는 노드 | 전체 텍스트 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/fulltextpredicate |
| 6.2의 리소스 유형 | 해당 사항 없음 |

6.1에서 표준 전체 텍스트 조건자는 검색 양식의 일부였습니다. 6.2에서 전체 텍스트 필드가 OmniSearch로 대체되었습니다. 이 조건자는 프로그래밍 방식으로 건너뛰며 제거할 수 있습니다.

**작업:** 위에서 언급한 노드를 제거하십시오.

### 경로 브라우저 조건자 {#path-browser-predicates-1}

| 6.1의 기본 검색 양식에 있는 노드 | pathbrowser |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/pathbrowserpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/pathbrowserpredicate |

**작업:** `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### Mime 유형 조건자 {#mime-type-predicates}

| 6.1의 기본 검색 양식에 있는 노드 | mimetype |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/optionpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionpredicate |

**작업:** `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 파일 크기 조건자 {#file-size-predicates}

| 6.1의 기본 검색 양식에 있는 노드 | 파일 크기 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/filesizepredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**작업:** 위의 6.2 위치에 표시된 대로 `resourceType`을(를) 조정합니다.

### 마지막으로 수정된 자산 술어 {#asset-last-modified-predicates}

| 6.1의 기본 검색 양식에 있는 노드 | assetlastmodifiedpredicate |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |

작업: resourceType 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;/coral&quot; 추가).

### Publish 설명 {#publish-predicate}

| 6.1의 기본 검색 양식에 있는 노드 | 게시 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/publishpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/publishpredicate |

**작업:**

* `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

* 값이 `/libs/dam/options/predicates/publish`인 `optionPaths`(문자열 유형) 속성을 추가하십시오.

* 부울 값이 `true`인 `singleSelect` 속성을 추가하십시오.

### 상태 조건자 {#status-predicates}

| 6.1의 기본 검색 양식에 있는 노드 | 상태 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/optionpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionpredicate |

**작업:** `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 만료 상태 조건자 {#expiry-status-predicates}

| 6.1의 기본 검색 양식에 있는 노드 | 만료 상태 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/expiredassetpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/expiredassetpredicate |

**작업:** `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 메타데이터 유효성 술어 {#metadata-validity-predicates}

| 6.1의 기본 검색 양식에 있는 노드 | 메타데이터 유효성 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/optionpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionpredicate |

**작업:** `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 등급 조건자 {#rating-predicates}

| 6.1의 기본 검색 양식에 있는 노드 | 등급 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/ratingpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**작업:** `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 방향 조건자 {#orientation-predicate}

| 6.1의 기본 검색 양식에 있는 노드 | orientation |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| 6.2의 리소스 유형 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**작업:**

* `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

* 같은 노드의 `text` 속성과 값이 같은 `fieldLabel` 속성을 추가하십시오.

* 같은 노드의 `text` 속성과 같은 값을 가진 `emptyText` 속성을 추가하십시오.

* 같은 노드의 `optionPaths` 속성과 값이 같은 `rootPath` 속성을 추가하십시오.

### 스타일 조건자 {#style-predicate}

| 6.1의 기본 검색 양식에 있는 노드 | 스타일 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| 6.2의 리소스 유형 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**작업:**

* `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

* 같은 노드의 `text` 속성과 값이 같은 `fieldLabel` 속성을 추가하십시오.

* 같은 노드의 `text` 속성과 같은 값을 가진 `emptyText` 속성을 추가하십시오.

* 같은 노드의 `optionPaths` 속성과 값이 같은 `rootPath` 속성을 추가하십시오.

### 비디오 형식 조건자 {#video-format-predicates}

| 6.1의 기본 검색 양식에 있는 노드 | videoFormat |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/optionpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionpredicate |

**작업:** `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### Mainasset 조건자 {#mainasset-predicate}

| 6.1의 기본 검색 양식에 있는 노드 | 주요 자산 |
|---|---|
| 6.1의 리소스 유형 | granite/ui/components/foundation/form/hidden |
| 6.2의 리소스 유형 | granite/ui/components/coral/foundation/form/hidden |

**작업:** `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).
