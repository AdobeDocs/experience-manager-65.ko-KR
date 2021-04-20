---
title: 사용자 정의 검색 Forms 업그레이드
seo-title: 사용자 정의 검색 Forms 업그레이드
description: 이 문서에서는 사용자 정의 검색 양식이 작동하도록 업그레이드 후 필요한 조정 사항에 대해 자세히 설명합니다.
seo-description: 이 문서에서는 사용자 정의 검색 양식이 작동하도록 업그레이드 후 필요한 조정 사항에 대해 자세히 설명합니다.
uuid: 35b8fbb9-5951-4e1c-bf04-4471a55b9cb0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: a08cee9c-e981-4483-8bdc-e6353977f854
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 3%

---


# 사용자 지정 검색 Forms 업그레이드{#upgrading-custom-search-forms}

AEM 6.2에서는 사용자 지정 검색 Forms이 저장소에 저장되는 위치가 변경되었습니다. 업그레이드 시 6.1의 위치에서 다음 위치로 이동됩니다.

* /apps/cq/gui/content/facet

를 새 위치에 추가합니다.

* /conf/global/settings/cq/search/facet

따라서 양식이 계속 작동하도록 하려면 업그레이드 후 수동으로 조정해야 합니다.

이는 새로운 검색 Forms뿐만 아니라 사용자 지정된 기본 Forms에도 적용됩니다.

자세한 내용은 [검색 패싯](/help/assets/search-facets.md)에 대한 설명서를 참조하십시오.

## resourceType 속성 {#changing-the-resourcetype-property} 변경

별도로 명시되어 있지 않는 한, 업그레이드 후에 수행해야 하는 대부분의 조정 사항은 구성된 사용자 지정 검색 Forms에 대해 `sling:resourceType` 속성을 변경해야 합니다. 속성이 렌더링 스크립트의 올바른 위치를 가리키도록 해야 합니다.

다음을 수행하여 속성을 변경할 수 있습니다.

1. `https://server:port/crx/de/index.jsp`으로 이동하여 CRXDE Lite 열기
1. 아래 [사용자 지정 검색 Forms](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms) 목록에 지정된 대로 조정해야 하는 노드의 위치를 찾습니다.
1. 노드를 클릭합니다. 오른쪽 속성 창에서 **sling:resourceType** 속성을 클릭하고 수정합니다.
1. 마지막으로 **모두 저장** 단추를 눌러 변경 사항을 저장합니다.

## 사용자 지정 검색 Forms 목록 {#list-of-custom-search-forms}

아래에 모든 사용자 정의 검색 Forms의 목록과 업그레이드 후 필요한 수정 사항이 표시됩니다. `/conf/global/settings/cq/search/facets/sites/items`의 이름을 참조합니다.

### 노드 이름이 &quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext}인 전체 텍스트 설명

<table>
 <tbody>
  <tr>
   <td>6.1의 기본 검색 양식의 노드/s</td>
   <td>전체 텍스트</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchitects/fulltext술어</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td>해당 없음</td>
  </tr>
 </tbody>
</table>

AEM 6.1에서는 표준 전체 텍스트 조건자가 검색 양식의 일부였습니다. 6.2에서는 전체 텍스트 필드가 OmniSearch로 대체되었습니다. 이 조건자는 프로그래밍 방식으로 생략되며 제거할 수 있습니다.

**작업:** 노드를 완전히 제거합니다.

### 기타 전체 텍스트 예측: {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1에서 기본 검색의 노드/s</td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchitects/fulltext술어</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchitects/fulltextpredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성을  `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot;을 추가합니다).

### 경로 브라우저는 {#path-browser-predicates}을(를) 예측합니다.

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식의 노드/s </td>
   <td>경로</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchitects/pathpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchitects/pathpredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성을  `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot;을 추가합니다).

### 태그는 {#tags-predicates}을(를) 예측합니다.

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식의 노드/s </td>
   <td>태그</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchitects/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchitects/tagspredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** resourceTypeproperty를  **** 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot;을 추가).

### 페이지 상태 설명 {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식의 노드/s </td>
   <td>pagestatusectiple</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/searchpredicates/pagestus술어</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td>해당 없음</td>
  </tr>
 </tbody>
</table>

페이지 상태는 2개의 옵션 속성 예측자로 대체되었습니다. 하나는 게시용이고 다른 하나는 LiveCopy 상태입니다.

**작업:**

* `pagestatuspredicate` 노드 제거
* 노드 복사

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * 끝 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 노드 복사

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * 끝 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* `analyticspredicate` 노드의 `listOrder` 속성을 &quot;**8**&quot;으로 설정해야 합니다. 이것은 충돌을 피하기 위해 필요합니다.

### 날짜 범위는 {#date-range-predicates}을(를) 예측합니다.

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식의 노드/s </td>
   <td>daterangepredict</td>
  </tr>
  <tr>
   <td>6.1의 리소스 유형</td>
   <td>cq/gui/components/common/admin/customsearch/searchpredicates/daterangepredicate</td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchiteschematements/daterangedepredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성을  `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot;을 추가합니다).

### 숨겨진 필터 {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식의 노드/s </td>
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

**동작:** 조정할 사항이 없습니다.

### 분석 조건자 {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식의 노드/s </td>
   <td>analytics사전</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/search예측자/analytics사전 설정</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search예측자/analytics사전 설정</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성을  `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot;을 추가합니다).

### 범위 조건자 {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식의 노드/s </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/search예측자/범위 설명</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search예측/범위 설명</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성을  `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot;을 추가합니다).

>[!NOTE]
>
>참고:6.1과 반대로 범위 술어는 더 이상 검색 막대에서 태그를 렌더링하지 않습니다.

### 옵션 속성 조건자 {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식의 노드/s </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search예측자/optionspredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성을  `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot;을 추가합니다).

### 슬라이더 범위 조건자 {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식의 노드/s </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/searchpredicates/sliderrangedepredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search예측/sliderrangedepredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성을  `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot;을 추가합니다).

### 구성 요소 조건자 {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식의 노드/s </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/searchpredicates/components미리 보기</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search예측자/components사전 지정</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성을  `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot;을 추가합니다).

### 작성자 조건자 {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식의 노드/s </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search예측자/사용자 설명</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성을  `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot;을 추가합니다).

### 템플릿 조건자 {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />의 기본 검색 양식의 노드/s </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/search예측자/템플릿 설명</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search예측자/templattescheme</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성을  `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot;을 추가합니다).

## 자산 관리자 검색 레일 {#assets-admin-search-rail}

아래 노드는 `/conf/global/settings/dam/search/facets/assets/items`의 이름을 나타냅니다.

### 노드 이름이 &quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext-1}인 전체 텍스트 설명

| 6.1의 기본 검색 양식의 노드/s | 전체 텍스트 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/search예측자/fulltextpredicate |
| 6.2의 리소스 유형 | 해당 없음 |

6.1에서는 표준 전체 텍스트 조건자가 검색 양식의 일부였습니다. 6.2에서는 전체 텍스트 필드가 OmniSearch로 대체되었습니다. 이 조건자는 프로그래밍 방식으로 생략되며 제거할 수 있습니다.

**작업:** 위에 언급된 노드를 제거합니다.

### 경로 브라우저는 {#path-browser-predicates-1}을(를) 예측합니다.

| 6.1의 기본 검색 양식의 노드/s | 경로 브라우저 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/search예측자/경로 탐색 설명 |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/search예측자/경로 탐색 설명 |

**작업:** 속성을  `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot;을 추가합니다).

### MIME 형식은 {#mime-type-predicates} 예고합니다.

| 6.1의 기본 검색 양식의 노드/s | mimetype |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchitects/optionspredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchitects/optionspredicate |

**작업:** 속성을  `resourceType` 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot;을 추가합니다).

### 파일 크기는 {#file-size-predicates} 예측

| 6.1의 기본 검색 양식의 노드/s | 파일 크기 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/search예측자/filesizepredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/search예측자/sliderangepredicate |

**작업:** 위 6.2 위치 `resourceType` 에 표시된 대로 조정합니다.

### 마지막으로 수정한 자산 예측: {#asset-last-modified-predicates}

| 6.1의 기본 검색 양식의 노드/s | assetlastmodifiedpredicate |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/search예측자/astelastmodifedpret |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/search예측자/astelastmodifedpret |

작업:resourceType 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;/coral&quot; 추가).

### 게시 설명 {#publish-predicate}

| 6.1의 기본 검색 양식의 노드/s | 페이지를 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/search예측자/publishpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/search예측자/publishpredicate |

**작업:**

* `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치에서 &quot;**/coral**&quot; 추가).

* 값을 사용하여 `optionPaths`(문자열 유형) 속성을 추가합니다.`/libs/dam/options/predicates/publish`

* 부울 값 `true`을(를) 사용하여 `singleSelect` 속성을 추가합니다.

### 상태 설명 {#status-predicates}

| 6.1의 기본 검색 양식의 노드/s | 상태 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchitects/optionspredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchitects/optionspredicate |

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 만료 상태 {#expiry-status-predicates} 예측

| 6.1의 기본 검색 양식의 노드/s | 만료 상태 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/experadassetpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/expreadassetpredicate |

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 메타데이터 유효성에 {#metadata-validity-predicates} 예측

| 6.1의 기본 검색 양식의 노드/s | 메타질량 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchitects/optionspredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchitects/optionspredicate |

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 등급 예측: {#rating-predicates}

| 6.1의 기본 검색 양식의 노드/s | 등급 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/search예측자/ratingpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/search예측자/sliderangepredicate |

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 방향 설명 {#orientation-predicate}

| 6.1의 기본 검색 양식의 노드/s | 방향 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/search예측자/태그필터 설명 |
| 6.2의 리소스 유형 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**작업:**

* `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치에서 &quot;**/coral**&quot; 추가).

* 동일한 노드의 `text` 속성과 동일한 값을 가진 `fieldLabel` 속성을 추가합니다.

* 동일한 노드의 `text` 속성과 동일한 값을 갖는 `emptyText` 속성을 추가합니다.

* 동일한 노드의 `optionPaths` 속성과 동일한 값을 가진 `rootPath` 속성을 추가합니다.

### 스타일 설명 {#style-predicate}

| 6.1의 기본 검색 양식의 노드/s | 화면 위치가 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/search예측자/태그필터 설명 |
| 6.2의 리소스 유형 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**작업:**

* `resourceType` 속성을 조정합니다(위에 표시된 6.2 위치에서 &quot;**/coral**&quot; 추가).

* 동일한 노드의 `text` 속성과 동일한 값을 가진 `fieldLabel` 속성을 추가합니다.

* 동일한 노드의 `text` 속성과 동일한 값을 갖는 `emptyText` 속성을 추가합니다.

* 동일한 노드의 `optionPaths` 속성과 동일한 값을 가진 `rootPath` 속성을 추가합니다.

### 비디오 형식은 {#video-format-predicates} 예측

| 6.1의 기본 검색 양식의 노드/s | videoFormat |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchitects/optionspredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchitects/optionspredicate |

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 유지 자산 설명 {#mainasset-predicate}

| 6.1의 기본 검색 양식의 노드/s | mainasset |
|---|---|
| 6.1의 리소스 유형 | granite/ui/components/foundation/form/hidden |
| 6.2의 리소스 유형 | granite/ui/components/coral/foundation/form/hidden |

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).
