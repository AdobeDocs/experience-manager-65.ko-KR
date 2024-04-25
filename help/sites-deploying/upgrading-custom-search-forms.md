---
title: 사용자 지정 Search Forms 업그레이드
description: 이 문서에서는 사용자 지정 검색 양식이 작동하기 위해 업그레이드 후 필요한 조정에 대해 자세히 설명합니다.
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

# 사용자 지정 Search Forms 업그레이드{#upgrading-custom-search-forms}

AEM 6.2에서는 저장소에서 사용자 지정 Search Forms이 저장되는 위치가 변경되었습니다. 업그레이드 시 6.1의 위치에서 다음 위치로 이동됩니다.

* /apps/cq/gui/컨텐츠/facets

다음 아래의 새 위치로 드래그합니다.

* /conf/global/settings/cq/검색/facets

따라서 업그레이드 후 양식이 계속 작동하려면 수동으로 조정해야 합니다.

이는 사용자 정의된 새 Search Forms 및 기본 Forms에 적용됩니다.

자세한 내용은 Search 패싯](/help/assets/search-facets.md) 문서를 [참조하십시오.

## resourceType 속성 변경 {#changing-the-resourcetype-property}

별도로 명시되지 않는 한, 업그레이드 이후 수행해야 하는 대부분의 조정은 `sling:resourceType` 구성된 사용자 지정 검색 Forms에 대한 속성입니다. 속성이 렌더링 스크립트의 올바른 위치를 가리키도록 해야 합니다.

다음을 수행하여 속성을 변경할 수 있습니다.

1. 다음으로 이동하여 CRXDE Lite를 엽니다. `https://server:port/crx/de/index.jsp`
1. 아래의 사용자 지정 Search Forms 목록에 [지정된 대로 조정해야 하는 노드의 위치로 검색](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms) .
1. 노드 클릭 오른쪽 속성 창에서 을(를) 클릭하고 **sling:resourceType** 속성.
1. 마지막으로 **모두 저장** 단추를 클릭합니다.

## 사용자 지정 검색 Forms 목록 {#list-of-custom-search-forms}

아래에는 모든 사용자 정의 검색 Forms 목록과 업그레이드 후 필요한 수정 사항이 나와 있습니다. 이 이름은 의 이름을 참조합니다 `/conf/global/settings/cq/search/facets/sites/items`.

### 노드 이름이 &quot;fulltext&quot;인 전체 텍스트 설명 {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>6.1에서 기본 Search 양식의 노드</td>
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

AEM 6.1에서는 표준 전체 텍스트 설명이 검색 양식의 일부였습니다. 6.2에서는 전체 텍스트 필드가 OmniSearch로 대체되었습니다. 이 조건자는 프로그래밍 방식으로 건너뛰고 제거할 수 있습니다.

**작업:** 노드를 완전히 제거.

### 기타 전체 텍스트 설명 {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1에서 기본 Search From의 노드</td>
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

**작업:** 속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 좋아요 추가).

### 경로 브라우저 설명 {#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1<br />에서 기본 Search 양식의 노드 <br /> </td>
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

**작업:** 조정 `resourceType` 속성(추가 &quot;**/coral**&#x200B;위에 표시된 6.2 위치에서와 같이).

### 태그 술어 {#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1의 기본 검색 양식에 있는 노드<br /> <br /> </td>
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

**작업:** resourceType **속성 조정**(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 좋아요 추가).

### 페이지 상태 설명 {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br />에서 기본 Search 양식의 노드 <br /> </td>
   <td>pageStatusPredicate</td>
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

이 페이지 상태는 두 개의 옵션 속성 조건자로 대체되었는데, 하나는 게시이고 다른 하나는 LiveCopy 상태입니다.

**작업:**

* `pagestatuspredicate` 노드 제거
* 복사 노드

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * 받는 사람 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 복사 노드

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * 받는 사람 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 노드 속성 `analyticspredicate` 을 &quot;**8**&quot;로 설정해야 `listOrder` 합니다. 이는 충돌을 방지하는 데 필요합니다.

### 날짜 범위 술어 {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1의 기본 검색 양식에 있는 노드<br /> <br /> </td>
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

**작업:** 조정 `resourceType` 속성(추가 &quot;**/coral**&#x200B;위에 표시된 6.2 위치에서와 같이).

### 숨겨진 필터 {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>6.1의 기본 검색 양식에 있는 노드<br /> <br /> </td>
   <td>유형</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>granite/ui/components/foundation/form/숨김</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>granite/ui/components/foundation/form/숨김</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 조정할 것이 없습니다.

### 분석 조건자 {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br />에서 기본 Search 양식의 노드 <br /> </td>
   <td>AnalyticsPredicate</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 좋아요 추가).

### 범위 조건자 {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br />에서 기본 Search 양식의 노드 <br /> </td>
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

**작업:** 속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 좋아요 추가).

>[!NOTE]
>
>참고: 6.1과 달리 범위 조건자는 더 이상 검색 막대에서 태그를 렌더링하지 않습니다.

### 옵션 속성 조건자 {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br />에서 기본 Search 양식의 노드 <br /> </td>
   <td>해당 사항 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 좋아요 추가).

### 슬라이더 범위 조건자 {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br />에서 기본 Search 양식의 노드 <br /> </td>
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

**작업:** 속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 좋아요 추가).

### 구성 요소 조건자 {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br />에서 기본 Search 양식의 노드 <br /> </td>
   <td>해당 사항 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 좋아요 추가).

### 작성자 조건자 {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br />에서 기본 Search 양식의 노드 <br /> </td>
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

**작업:** 속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 좋아요 추가).

### 템플릿 조건자 {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1의 기본 검색 양식에 있는 노드<br /> <br /> </td>
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

**작업:** 속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 좋아요 추가).

## 자산 관리자 검색 레일 {#assets-admin-search-rail}

아래 노드는 `/conf/global/settings/dam/search/facets/assets/items`

### 노드 이름이 &quot;fulltext&quot;인 전체 텍스트 설명 {#fulltext-predicate-with-node-name-fulltext-1}

| 6.1에서 기본 Search 양식의 노드 | 전체 텍스트 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/fulltextpredicate |
| 6.2의 리소스 유형 | 해당 사항 없음 |

6.1에서 표준 전체 텍스트 조건자는 검색 양식의 일부였습니다. 6.2에서 전체 텍스트 필드가 OmniSearch로 대체되었습니다. 이 조건자는 프로그래밍 방식으로 건너뛰며 제거할 수 있습니다.

**작업:** 위에서 언급한 노드를 제거합니다.

### 경로 브라우저 조건자 {#path-browser-predicates-1}

| 6.1의 기본 검색 양식에 있는 노드 | pathbrowser |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/pathbrowserpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/pathbrowserpredicate |

**작업:** 속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 좋아요 추가).

### MIME 유형 설명 {#mime-type-predicates}

| 6.1에서 기본 Search 양식의 노드 | Mimetype |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**작업:** 속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 좋아요 추가).

### 파일 크기 설명 {#file-size-predicates}

| 6.1에서 기본 Search 양식의 노드 | Filesize |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/filesizepredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**작업:** 위의 6.2 위치에 표시된 대로 조정합니다 `resourceType` .

### 마지막으로 수정된 자산 설명 {#asset-last-modified-predicates}

| 6.1에서 기본 Search 양식의 노드 | assetlastmodifiedpredicate |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |

작업: resourceType 속성 조정(위에 표시된 6.2 위치에 &quot;/coral&quot; 좋아요 추가).

### Publish 조건자 {#publish-predicate}

| 6.1에서 기본 Search 양식의 노드 | 게시 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/publishpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/publishpredicate |

**작업:**

* 속성 조정 `resourceType` (위에 표시된 6.2 위치에 &quot;**/coral**&quot; 좋아요 추가)

* `optionPaths` 다음 값을 갖는 (String 유형) 속성 추가:`/libs/dam/options/predicates/publish`

* 추가 `singleSelect` 부울 값이 있는 속성 `true`.

### 상태 조건자 {#status-predicates}

| 6.1에서 기본 Search 양식의 노드 | 상태 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**작업:** 속성 조정 `resourceType` (위에 표시된 6.2 위치에 &quot;**/coral**&quot; 좋아요 추가)

### 만료 상태 설명 {#expiry-status-predicates}

| 6.1에서 기본 Search 양식의 노드 | 만료 상태 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/expiredassetpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/expiredassetpredicate |

**작업:** 조정 `resourceType` 속성(추가 &quot;**/coral**&quot; 위에 표시된 6.2 위치와 유사)

### 메타데이터 유효성 술어 {#metadata-validity-predicates}

| 6.1의 기본 검색 양식에 있는 노드 | 메타데이터 유효성 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/optionpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**작업:** 속성 조정 `resourceType` (위에 표시된 6.2 위치에 &quot;**/coral**&quot; 좋아요 추가)

### 등급 설명 {#rating-predicates}

| 6.1에서 기본 Search 양식의 노드 | 등급 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/ratingpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**작업:** 속성 조정 `resourceType` (위에 표시된 6.2 위치에 &quot;**/coral**&quot; 좋아요 추가)

### 방향 설명 {#orientation-predicate}

| 6.1에서 기본 Search 양식의 노드 | 방향 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| 6.2의 리소스 유형 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**작업:**

* 속성 조정 `resourceType` (위에 표시된 6.2 위치에 &quot;**/coral**&quot; 좋아요 추가)

* 동일한 노드의 `fieldLabel` 속성와 동일한 값을 `text` 갖는 속성 추가합니다.

* 동일한 노드의 `emptyText` 속성와 동일한 `text` 값을 갖는 속성 추가합니다.

* `rootPath` 동일한 노드의 속성와 동일한 `optionPaths` 값을 갖는 속성 추가합니다.

### 스타일 설명 {#style-predicate}

| 6.1에서 기본 Search 양식의 노드 | 스타일 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| 6.2의 리소스 유형 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**작업:**

* 속성 조정 `resourceType` (위에 표시된 6.2 위치에 &quot;**/coral**&quot; 좋아요 추가)

* 동일한 노드의 `fieldLabel` 속성와 동일한 값을 `text` 갖는 속성 추가합니다.

* 동일한 노드의 `emptyText` 속성와 동일한 `text` 값을 갖는 속성 추가합니다.

* `rootPath` 동일한 노드의 속성와 동일한 `optionPaths` 값을 갖는 속성 추가합니다.

### 비디오 형식 설명 {#video-format-predicates}

| 6.1에서 기본 Search 양식의 노드 | 비디오 포맷 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**작업:** 속성 조정 `resourceType` (위에 표시된 6.2 위치에 &quot;**/coral**&quot; 좋아요 추가)

### 주 자산 설명 {#mainasset-predicate}

| 6.1에서 기본 Search 양식의 노드 | 주자산 |
|---|---|
| 6.1의 리소스 유형 | granite/ui/components/foundation/form/숨김 |
| 6.2의 리소스 유형 | 화강암/UI/구성 요소/산호/기초/양식/숨김 |

**작업:** 조정 `resourceType` 속성(추가 &quot;**/coral**&quot; 위에 표시된 6.2 위치와 유사)
