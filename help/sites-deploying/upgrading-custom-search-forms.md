---
title: 사용자 지정 검색 Forms 업그레이드
seo-title: 사용자 지정 검색 Forms 업그레이드
description: 이 문서에서는 사용자 정의 검색 양식이 작동하도록 업그레이드 후 필요한 조정에 대해 자세히 설명합니다.
seo-description: 이 문서에서는 사용자 정의 검색 양식이 작동하도록 업그레이드 후 필요한 조정에 대해 자세히 설명합니다.
uuid: 35b8fbb9-5951-4e1c-bf04-4471a55b9cb0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: a08cee9c-e981-4483-8bdc-e6353977f854
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1709'
ht-degree: 3%

---


# 사용자 지정 검색 Forms 업그레이드{#upgrading-custom-search-forms}

AEM 6.2에서는 Customized Search Forms이 저장소에 저장되는 위치가 변경되었습니다. 업그레이드 시 6.1의 위치에서 다음 위치로 이동됩니다.

* /apps/cq/gui/content/facets

to new location under:

* /conf/global/settings/cq/search/facets

따라서 양식이 계속 작동하도록 하려면 업그레이드 후 수동으로 조정해야 합니다.

이는 사용자 지정된 기본 Forms뿐만 아니라 새 검색 Forms에도 적용됩니다.

자세한 내용은 [검색 패싯](/help/assets/search-facets.md)의 설명서를 참조하십시오.

## resourceType 속성 {#changing-the-resourcetype-property} 변경

별도로 명시되어 있지 않는 한, 업그레이드 후에 수행해야 하는 조정 작업의 대부분은 구성된 사용자 지정 검색 Forms에 대해 `sling:resourceType` 속성을 변경해야 합니다. 속성이 렌더링 스크립트의 올바른 위치를 가리키도록 필요합니다.

다음을 수행하여 속성을 변경할 수 있습니다.

1. `https://server:port/crx/de/index.jsp`으로 이동하여 CRXDE Lite 열기
1. 아래 [사용자 지정 검색 Forms](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms) 목록에 지정된 대로 조정해야 하는 노드의 위치를 찾습니다.
1. 노드를 클릭합니다. 오른쪽 속성 창에서 **sling:resourceType** 속성을 클릭하고 수정합니다.
1. 마지막으로 **모두 저장** 단추를 눌러 변경 사항을 저장합니다.

## 사용자 지정 검색 Forms 목록 {#list-of-custom-search-forms}

아래에는 모든 사용자 정의 검색 Forms의 목록과 업그레이드 후 필요한 수정 사항이 나와 있습니다. `/conf/global/settings/cq/search/facets/sites/items`의 이름을 참조합니다.

### 노드 이름이 &quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext}인 전체 텍스트 설명

<table>
 <tbody>
  <tr>
   <td>6.1의 기본 검색 양식의 노드/s</td>
   <td>전체 텍스트</td>
  </tr>
  <tr>
   <td><p>리소스 유형(6.1)</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchitects/fulltext 술어</p> </td>
  </tr>
  <tr>
   <td>리소스 유형(6.2)</td>
   <td>해당 없음</td>
  </tr>
 </tbody>
</table>

AEM 6.1에서는 표준 전체 텍스트 술어가 검색 양식의 일부였습니다. 6.2에서는 전체 텍스트 필드가 OmniSearch로 대체되었습니다. 이 술어는 프로그래밍 방식으로 생략되며 제거할 수 있습니다.

**작업:** 노드를 완전히 제거합니다.

### 기타 전체 텍스트 예측 {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1에서 기본 검색 노드/s</td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>리소스 유형(6.1)</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchitects/fulltext 술어</p> </td>
  </tr>
  <tr>
   <td>리소스 유형(6.2)</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchitects/fulltext술어</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 추가).

### 경로 브라우저가 {#path-browser-predicates} 예측

<table>
 <tbody>
  <tr>
   <td>Node/s in default Search Form in 6.1<br /> <br /> </td>
   <td>경로</td>
  </tr>
  <tr>
   <td><p>리소스 유형(6.1)</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchitects/path술어</p> </td>
  </tr>
  <tr>
   <td>리소스 유형(6.2)</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchitects/path술어</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 추가).

### 태그는 {#tags-predicates}을(를) 예측합니다.

<table>
 <tbody>
  <tr>
   <td>Node/s in default Search Form in 6.1<br /> <br /> </td>
   <td>태그</td>
  </tr>
  <tr>
   <td><p>리소스 유형(6.1)</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchitects/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>리소스 유형(6.2)</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchitects/tagspredicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** resourceTypeproperty를  **** 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 추가).

### 페이지 상태 설명 {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>Node/s in default Search Form in 6.1<br /> <br /> </td>
   <td>pagestadus술자</td>
  </tr>
  <tr>
   <td><p>리소스 유형(6.1)</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchitects/pagestateus술어</p> </td>
  </tr>
  <tr>
   <td>리소스 유형(6.2)</td>
   <td>해당 없음</td>
  </tr>
 </tbody>
</table>

페이지 상태가 게시 및 LiveCopy 상태에 대해 각각 하나씩, 두 개의 옵션 속성 예측자로 대체되었습니다.

**작업:**

* `pagestatuspredicate` 노드 제거
* 노드 복사

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * 끝 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 노드 복사

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * 끝 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* `analyticspredicate` 노드의 `listOrder` 속성을 &quot;**8**&quot;으로 설정해야 합니다. 이것은 충돌을 피하기 위해 필요합니다.

### 날짜 범위 예측자 {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>Node/s in default Search Form in 6.1<br /> <br /> </td>
   <td>daterangeperc</td>
  </tr>
  <tr>
   <td>리소스 유형(6.1)</td>
   <td>cq/gui/components/common/admin/customsearch/searchiteschematts/daterangedeparts</td>
  </tr>
  <tr>
   <td>리소스 유형(6.2)</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchiteschemates/daterangedeparts</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 추가).

### 숨겨진 필터 {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>Node/s in default Search Form in 6.1<br /> <br /> </td>
   <td>유형</td>
  </tr>
  <tr>
   <td><p>리소스 유형(6.1)</p> </td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
  <tr>
   <td>리소스 유형(6.2)</td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 조정할 사항이 없습니다.

### 분석 설명 {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>Node/s in default Search Form in 6.1<br /> <br /> </td>
   <td>분석 자료</td>
  </tr>
  <tr>
   <td><p>리소스 유형(6.1)</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchitects/analytics분석</p> </td>
  </tr>
  <tr>
   <td>리소스 유형(6.2)</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchitecusts/analyticsDiscopate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 추가).

### 범위 설명 {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>Node/s in default Search Form in 6.1<br /> <br /> </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>리소스 유형(6.1)</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/search예측자/범위 설명</p> </td>
  </tr>
  <tr>
   <td>리소스 유형(6.2)</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search예측/범위</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 추가).

>[!NOTE]
>
>참고:6.1과 반대로 범위 술어가 더 이상 검색 막대에서 태그를 렌더링하지 않습니다.

### 옵션 속성 설명 {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>Node/s in default Search Form in 6.1<br /> <br /> </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>리소스 유형(6.1)</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchitects/optionspecific</p> </td>
  </tr>
  <tr>
   <td>리소스 유형(6.2)</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchiteschemates/optiondisdicate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 추가).

### 슬라이더 범위 설명 {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>Node/s in default Search Form in 6.1<br /> <br /> </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>리소스 유형(6.1)</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchiteschematts/sliderrangescheme</p> </td>
  </tr>
  <tr>
   <td>리소스 유형(6.2)</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchiteschemates/sliderrangedeparts</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 추가).

### 구성 요소 설명 {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>Node/s in default Search Form in 6.1<br /> <br /> </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>리소스 유형(6.1)</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchitects/componentspredicate</p> </td>
  </tr>
  <tr>
   <td>리소스 유형(6.2)</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchitects/components구성 요소</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 추가).

### 작성자 설명 {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>Node/s in default Search Form in 6.1<br /> <br /> </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>리소스 유형(6.1)</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/search예측자/사용자 술어</p> </td>
  </tr>
  <tr>
   <td>리소스 유형(6.2)</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchitects/userdeparate</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 추가).

### 템플릿 설명 {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>Node/s in default Search Form in 6.1<br /> <br /> </td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td><p>리소스 유형(6.1)</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/search예측자/템플릿</p> </td>
  </tr>
  <tr>
   <td>리소스 유형(6.2)</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchiteschematts/templatescheme</p> </td>
  </tr>
 </tbody>
</table>

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 추가).

## 자산 관리자 검색 레일 {#assets-admin-search-rail}

아래 노드는 `/conf/global/settings/dam/search/facets/assets/items`의 이름을 나타냅니다.

### 노드 이름이 &quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext-1}인 전체 텍스트 설명

| 6.1의 기본 검색 양식의 노드/s | 전체 텍스트 |
|---|---|
| 리소스 유형(6.1) | dam/gui/components/admin/customsearch/searchitets/fulltext술어 |
| 리소스 유형(6.2) | 해당 없음 |

6.1에서는 표준 전체 텍스트 술어가 검색 양식의 일부였습니다. 6.2에서는 전체 텍스트 필드가 OmniSearch로 대체되었습니다. 이 술어는 프로그래밍 방식으로 생략되며 제거할 수 있습니다.

**작업:** 위에 언급된 노드를 제거합니다.

### 경로 브라우저가 {#path-browser-predicates-1} 예측

| 6.1의 기본 검색 양식의 노드/s | 경로 브라우저 |
|---|---|
| 리소스 유형(6.1) | dam/gui/components/admin/customsearch/searchitets/pathbrowser |
| 리소스 유형(6.2) | dam/gui/coral/components/admin/customsearch/searchitets/pathbrowser |

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 추가).

### MIME 유형 예측 {#mime-type-predicates}

| 6.1의 기본 검색 양식의 노드/s | mimetype |
|---|---|
| 리소스 유형(6.1) | dam/gui/components/admin/customsearch/searchitects/optionspredicate |
| 리소스 유형(6.2) | dam/gui/coral/components/admin/customsearch/searchitects/optionspredicate |

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 추가).

### 파일 크기 예측 {#file-size-predicates}

| 6.1의 기본 검색 양식의 노드/s | 파일 크기 |
|---|---|
| 리소스 유형(6.1) | dam/gui/components/admin/customsearch/search예측자/filesizede술어 |
| 리소스 유형(6.2) | dam/gui/coral/components/admin/customsearch/searchiteschematts/sliderange술어 |

**작업:** 위의 6.2 위치 `resourceType` 에 표시된 대로 조정합니다.

### 마지막으로 수정한 자산 예측자 {#asset-last-modified-predicates}

| 6.1의 기본 검색 양식의 노드/s | asetlastmodified조건자 |
|---|---|
| 리소스 유형(6.1) | dam/gui/components/admin/customsearch/search예측자/assetmodifiedpret |
| 리소스 유형(6.2) | dam/gui/coral/components/admin/customsearch/search예측자/assetmodifiedpret |

작업:resourceType 속성을 조정합니다(위에 표시된 6.2 위치와 같이 &quot;/coral&quot; 추가).

### 게시 설명 {#publish-predicate}

| 6.1의 기본 검색 양식의 노드/s | 페이지를 |
|---|---|
| 리소스 유형(6.1) | dam/gui/components/admin/customsearch/searchitets/publishpredicts |
| 리소스 유형(6.2) | dam/gui/coral/components/admin/customsearch/searchitets/publish술어 |

**작업:**

* `resourceType` 속성(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가) 조정

* 값을 사용하여 `optionPaths`(문자열 유형) 속성을 추가합니다.`/libs/dam/options/predicates/publish`

* 부울 값이 `true`인 `singleSelect` 속성을 추가합니다.

### 상태 설명 {#status-predicates}

| 6.1의 기본 검색 양식의 노드/s | 상태 |
|---|---|
| 리소스 유형(6.1) | dam/gui/components/admin/customsearch/searchitects/optionspredicate |
| 리소스 유형(6.2) | dam/gui/coral/components/admin/customsearch/searchitects/optionspredicate |

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 추가).

### 만료 상태 {#expiry-status-predicates} 예측

| 6.1의 기본 검색 양식의 노드/s | 만료 상태 |
|---|---|
| 리소스 유형(6.1) | dam/gui/components/admin/customsearch/search예측자/전문적 |
| 리소스 유형(6.2) | dam/gui/coral/components/admin/customsearch/search예측자/전문적 |

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 추가).

### 메타데이터 유효성에 {#metadata-validity-predicates} 예측

| 6.1의 기본 검색 양식의 노드/s | 메타산 |
|---|---|
| 리소스 유형(6.1) | dam/gui/components/admin/customsearch/searchitects/optionspredicate |
| 리소스 유형(6.2) | dam/gui/coral/components/admin/customsearch/searchitects/optionspredicate |

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 추가).

### 등급 예측{#rating-predicates}

| 6.1의 기본 검색 양식의 노드/s | 등급 |
|---|---|
| 리소스 유형(6.1) | dam/gui/components/admin/customsearch/searchitets/rating술어 |
| 리소스 유형(6.2) | dam/gui/coral/components/admin/customsearch/searchiteschematts/sliderange술어 |

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 추가).

### 방향 설명 {#orientation-predicate}

| 6.1의 기본 검색 양식의 노드/s | 방향 |
|---|---|
| 리소스 유형(6.1) | dam/gui/components/admin/customsearch/searchitects/tagsfilterdec |
| 리소스 유형(6.2) | cq/gui/components/coral/common/admin/customsearch/searchitects/tagspredicate |

**작업:**

* `resourceType` 속성(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가) 조정

* 동일한 노드에서 `text` 속성과 동일한 값을 갖는 `fieldLabel` 속성을 추가합니다.

* 동일한 노드의 `text` 속성과 동일한 값을 갖는 `emptyText` 속성을 추가합니다.

* 동일한 노드의 `optionPaths` 속성과 동일한 값을 갖는 `rootPath` 속성을 추가합니다.

### 스타일 설명 {#style-predicate}

| 6.1의 기본 검색 양식의 노드/s | 화면 위치가 |
|---|---|
| 리소스 유형(6.1) | dam/gui/components/admin/customsearch/searchitects/tagsfilterdec |
| 리소스 유형(6.2) | cq/gui/components/coral/common/admin/customsearch/searchitects/tagspredicate |

**작업:**

* `resourceType` 속성(위에 표시된 6.2 위치와 같이 &quot;**/coral**&quot; 추가) 조정

* 동일한 노드에서 `text` 속성과 동일한 값을 갖는 `fieldLabel` 속성을 추가합니다.

* 동일한 노드의 `text` 속성과 동일한 값을 갖는 `emptyText` 속성을 추가합니다.

* 동일한 노드의 `optionPaths` 속성과 동일한 값을 갖는 `rootPath` 속성을 추가합니다.

### 비디오 형식 예측 {#video-format-predicates}

| 6.1의 기본 검색 양식의 노드/s | videoFormat |
|---|---|
| 리소스 유형(6.1) | dam/gui/components/admin/customsearch/searchitects/optionspredicate |
| 리소스 유형(6.2) | dam/gui/coral/components/admin/customsearch/searchitects/optionspredicate |

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 추가).

### 유지 자산 설명 {#mainasset-predicate}

| 6.1의 기본 검색 양식의 노드/s | 유지 자산 |
|---|---|
| 리소스 유형(6.1) | granite/ui/components/foundation/form/hidden |
| 리소스 유형(6.2) | granite/ui/components/coral/foundation/form/hidden |

**작업:** 속성 `resourceType` 을 조정합니다(위에 표시된 6.2 위치에 &quot;**/coral**&quot; 추가).
