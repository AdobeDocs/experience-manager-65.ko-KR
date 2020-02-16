---
title: 사용자 정의 검색 양식 업그레이드
seo-title: 사용자 정의 검색 양식 업그레이드
description: 이 문서에서는 사용자 정의 검색 양식이 작동하도록 업그레이드 후 필요한 조정 내용을 자세히 설명합니다.
seo-description: 이 문서에서는 사용자 정의 검색 양식이 작동하도록 업그레이드 후 필요한 조정 내용을 자세히 설명합니다.
uuid: 35b8fbb9-5951-4e1c-bf04-4471a55b9cb0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: a08cee9c-e981-4483-8bdc-e6353977f854
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 사용자 정의 검색 양식 업그레이드{#upgrading-custom-search-forms}

AEM 6.2에서 사용자 지정 검색 양식이 저장소에 저장되는 위치가 변경되었습니다. 업그레이드 시 6.1의 위치에서 이동됩니다.

* /apps/cq/gui/content/facets

를 새 위치에 추가합니다.

* /conf/global/settings/cq/search/facets

따라서 양식을 계속 사용하려면 업그레이드 후 수동으로 조정해야 합니다.

이는 새 검색 양식과 사용자 정의된 기본 양식에 적용됩니다.

자세한 내용은 검색 패싯 문서를 [참조하십시오](/help/assets/search-facets.md).

## resourceType 속성 변경 {#changing-the-resourcetype-property}

별도로 명시되어 있지 않는 한, 업그레이드 후에 수행해야 하는 대부분의 조정 작업은 구성된 사용자 지정 검색 양식의 `sling:resourceType` 속성을 변경해야 합니다. 속성이 렌더링 스크립트의 올바른 위치를 가리키도록 필요합니다.

다음을 수행하여 속성을 변경할 수 있습니다.

1. 다음으로 이동하여 CRXDE Lite 열기 `https://server:port/crx/de/index.jsp`
1. 아래 사용자 지정 검색 양식 목록에 지정된 대로 조정해야 하는 노드의 위치를 [찾습니다](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms) .
1. 노드를 클릭합니다. 오른쪽 속성 창에서 sling:resourceType **속성을 클릭하고 수정합니다** .
1. 마지막으로 모든 저장 **단추를 눌러 변경 사항을 저장합니다** .

## 사용자 지정 검색 양식 목록 {#list-of-custom-search-forms}

아래에 모든 사용자 정의 검색 양식 및 업그레이드 후 필요한 수정 사항 목록이 표시됩니다. 그들은 의 이름을 `/conf/global/settings/cq/search/facets/sites/items`말한다.

### 노드 이름이 &quot;fulltext&quot;인 전체 텍스트 설명 {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>6.1의 기본 검색 양식의 노드/s</td>
   <td>전체 텍스트</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchitects/fulltextdecher</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td>해당 없음</td>
  </tr>
 </tbody>
</table>

AEM 6.1에서 표준 전체 텍스트 설명은 검색 양식의 일부였습니다. 6.2에서는 전체 텍스트 필드가 OmniSearch로 대체되었습니다. 이 조건자는 프로그래밍 방식으로 생략되며 제거할 수 있습니다.

**** 작업:노드를 완전히 제거합니다.

### 기타 전체 텍스트 설명 {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>Node/s in default Search From in 6.1</td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchitects/fulltextdecher</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchitects/fulltextpredicate</p> </td>
  </tr>
 </tbody>
</table>

**** 작업:속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 경로 브라우저 설명 {#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1의 기본 검색 양식의 노드/s<br /><br /> </td>
   <td>경로</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchitects/pathector</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/pathector</p> </td>
  </tr>
 </tbody>
</table>

**** 작업:속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 태그 설명 {#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1의 기본 검색 양식의 노드/s<br /><br /> </td>
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

**** 작업:resourceType **속성을** 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 페이지 상태 설명 {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1의 기본 검색 양식의 노드/s<br /><br /> </td>
   <td>pagestatus술어</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/pagestateusdec</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td>해당 없음</td>
  </tr>
 </tbody>
</table>

페이지 상태는 두 개의 옵션 속성 예측자로 대체되었습니다. 하나는 게시용이고 다른 하나는 LiveCopy 상태용입니다.

**작업:**

* 노드 `pagestatuspredicate` 제거
* 노드 복사

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * 끝 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 노드 복사

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * 끝 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 노드의 `listOrder` 속성을 &quot; `analyticspredicate` 8 ****&quot;으로 설정해야 합니다. 이것은 충돌을 피하기 위해 필요합니다.

### 날짜 범위 설명 {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1의 기본 검색 양식의 노드/s<br /><br /> </td>
   <td>daterangeperc</td>
  </tr>
  <tr>
   <td>6.1의 리소스 유형</td>
   <td>cq/gui/components/common/admin/customsearch/searchiteschematements/daterangedec</td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchiteschematements/daterangede조건자</p> </td>
  </tr>
 </tbody>
</table>

**** 작업:속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 숨겨진 필터 {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>6.1의 기본 검색 양식의 노드/s<br /><br /> </td>
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

**** 작업:조정할 필요가 없습니다.

### 분석 설명 {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1의 기본 검색 양식의 노드/s<br /><br /> </td>
   <td>분석 자료</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/analyticsDisdicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/analyticsDisdicate</p> </td>
  </tr>
 </tbody>
</table>

**** 작업:속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 범위 설명 {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1의 기본 검색 양식의 노드/s<br /><br /> </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/rangedec</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/range조건자</p> </td>
  </tr>
 </tbody>
</table>

**** 작업:속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

>[!NOTE]
>
>참고:6.1과 반대로 범위 술어가 더 이상 검색 막대에서 태그를 렌더링하지 않습니다.

### 옵션 속성 설명 {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1의 기본 검색 양식의 노드/s<br /><br /> </td>
   <td>해당 없음</td>
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

**** 작업:속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 슬라이더 범위 설명 {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1의 기본 검색 양식의 노드/s<br /><br /> </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/sliderrangedec</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/sliderrangedecher</p> </td>
  </tr>
 </tbody>
</table>

**** 작업:속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 구성 요소 설명 {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1의 기본 검색 양식의 노드/s<br /><br /> </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/componentsDisdicate</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/componentsDisdicate</p> </td>
  </tr>
 </tbody>
</table>

**** 작업:속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 작성자 설명 {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1의 기본 검색 양식의 노드/s<br /><br /> </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/userpredictive</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
 </tbody>
</table>

**** 작업:속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 템플릿 설명 {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1의 기본 검색 양식의 노드/s<br /><br /> </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>6.1의 리소스 유형</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/templatester</p> </td>
  </tr>
  <tr>
   <td>6.2의 리소스 유형</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/templateschemer</p> </td>
  </tr>
 </tbody>
</table>

**** 작업:속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

## 자산 관리자 검색 레일 {#assets-admin-search-rail}

아래 노드는 `/conf/global/settings/dam/search/facets/assets/items`

### 노드 이름이 &quot;fulltext&quot;인 전체 텍스트 설명 {#fulltext-predicate-with-node-name-fulltext-1}

| 6.1의 기본 검색 양식의 노드/s | 전체 텍스트 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchitects/fulltextpredicate |
| 6.2의 리소스 유형 | 해당 없음 |

6.1에서는 표준 전체 텍스트 조건자가 검색 양식의 일부였습니다. 6.2에서는 전체 텍스트 필드가 OmniSearch로 대체되었습니다. 이 조건자는 프로그래밍 방식으로 생략되며 제거할 수 있습니다.

**** 작업:위에 언급된 노드를 제거합니다.

### 경로 브라우저 설명 {#path-browser-predicates-1}

| 6.1의 기본 검색 양식의 노드/s | 경로 브라우저 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/pathbrowserdec |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/pathbrowser |

**** 작업:속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### MIME 유형 설명 {#mime-type-predicates}

| 6.1의 기본 검색 양식의 노드/s | mimetype |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**** 작업:속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 파일 크기 예측 {#file-size-predicates}

| 6.1의 기본 검색 양식의 노드/s | 파일 크기 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/filesizedicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchiteschematements/sliderangedespeech |

**** 작업:위의 6.2 위치에 표시된 대로 `resourceType` 조정합니다.

### 마지막으로 수정한 자산 예측 {#asset-last-modified-predicates}

| 6.1의 기본 검색 양식의 노드/s | assetlastmodified |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/assetmodifiedpred |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/assetlatemodifiedpred |

작업:resourceType 속성을 조정합니다(위에 표시된 6.2 위치에 &quot;/coral&quot; 추가).

### 설명 게시 {#publish-predicate}

| 6.1의 기본 검색 양식의 노드/s | 게시 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/publishpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchategies/publishpredicate |

**작업:**

* 속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

* 값을 사용하여 `optionPaths` (문자열 유형) 속성을 추가합니다. `/libs/dam/options/predicates/publish`

* 부울 값을 사용하여 `singleSelect` 속성을 추가합니다 `true`.

### 상태 설명 {#status-predicates}

| 6.1의 기본 검색 양식의 노드/s | 상태 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**** 작업:속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 만료 상태 예측 {#expiry-status-predicates}

| 6.1의 기본 검색 양식의 노드/s | 만료 상태 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/expiredassetdetechm |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/expiredassetdicate |

**** 작업:속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 메타데이터 유효성 예측 {#metadata-validity-predicates}

| 6.1의 기본 검색 양식의 노드/s | 메타데이터의 가능성 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**** 작업:속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 등급 예측 {#rating-predicates}

| 6.1의 기본 검색 양식의 노드/s | 등급 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/ratingpredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchiteschematements/sliderangedespeech |

**** 작업:속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 방향 설명 {#orientation-predicate}

| 6.1의 기본 검색 양식의 노드/s | 방향 |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/tags |
| 6.2의 리소스 유형 | cq/gui/components/coral/common/admin/customsearch/searchitects/tagspredicate |

**작업:**

* 속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

* 동일한 노드의 속성과 동일한 `fieldLabel` `text` 값을 갖는 속성을 추가합니다.

* 동일한 노드의 속성과 동일한 `emptyText` `text` 값을 갖는 속성을 추가합니다.

* 동일한 노드의 속성과 동일한 `rootPath` `optionPaths` 값을 갖는 속성을 추가합니다.

### 스타일 설명 {#style-predicate}

| 6.1의 기본 검색 양식의 노드/s | style |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/tags |
| 6.2의 리소스 유형 | cq/gui/components/coral/common/admin/customsearch/searchitects/tagspredicate |

**작업:**

* 속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

* 동일한 노드의 속성과 동일한 `fieldLabel` `text` 값을 갖는 속성을 추가합니다.

* 동일한 노드의 속성과 동일한 `emptyText` `text` 값을 갖는 속성을 추가합니다.

* 동일한 노드의 속성과 동일한 `rootPath` `optionPaths` 값을 갖는 속성을 추가합니다.

### 비디오 형식 예측 {#video-format-predicates}

| 6.1의 기본 검색 양식의 노드/s | videoFormat |
|---|---|
| 6.1의 리소스 유형 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| 6.2의 리소스 유형 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**** 작업:속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).

### 기본 자산 설명 {#mainasset-predicate}

| 6.1의 기본 검색 양식의 노드/s | 유지 자산 |
|---|---|
| 6.1의 리소스 유형 | granite/ui/components/foundation/form/hidden |
| 6.2의 리소스 유형 | granite/ui/components/coral/foundation/form/hidden |

**** 작업:속성을 `resourceType` 조정합니다(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가).
