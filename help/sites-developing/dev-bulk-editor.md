---
title: 벌크 편집기 개발
seo-title: Developing the Bulk Editor
description: 태깅을 사용하면 컨텐츠를 분류하고 구성할 수 있습니다
seo-description: Tagging allows content to be categorized and organized
uuid: 3cd04c52-5bdb-47f6-9fa3-d7a4937e8e20
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e9a1ff95-e88e-41f0-9731-9a59159b4653
exl-id: 8753aaab-959f-459b-bdb6-057cbe05d480
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1837'
ht-degree: 2%

---

# 벌크 편집기 개발{#developing-the-bulk-editor}

이 섹션에서는 벌크 편집기 도구를 개발하는 방법과 벌크 편집기를 기반으로 하는 제품 목록 구성 요소를 확장하는 방법을 설명합니다.

## 벌크 편집기 쿼리 매개 변수 {#bulk-editor-query-parameters}

벌크 편집기 작업 시 URL에 추가하여 특정 구성으로 벌크 편집기를 호출할 수 있는 몇 가지 쿼리 매개 변수가 있습니다. 제품 목록 구성 요소와 같이 벌크 편집기를 항상 특정 구성과 함께 사용하려면 bulkeditor.jsp(/libs/wcm/core/components/bulkeditor에 있음)를 수정하거나 특정 구성으로 구성 요소를 만들어야 합니다. 쿼리 매개 변수를 사용하여 변경한 내용은 영구적이지 않습니다.

예를 들어 브라우저의 URL에 다음을 입력하는 경우:

`https://<servername><port_number>/etc/importers/bulkeditor.html?rootPath=/content/geometrixx/en&queryParams=geometrixx&initialSearch=true&hrp=true`

벌크 편집기는 **루트 경로** href=true인 필드는 필드를 숨깁니다. 매개 변수 hrp=false를 사용하면 필드가 표시됩니다(기본값).

다음은 벌크 편집기 쿼리 매개 변수 목록입니다.

>[!NOTE]
>
>각 매개 변수에는 긴 이름과 짧은 이름이 있을 수 있습니다. 예를 들어 검색 루트 경로의 긴 이름은 입니다 `rootPath`짧은 것은 `rp`. 긴 이름이 정의되지 않으면 요청에서 짧은 이름을 읽습니다.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p> 매개변수</p> <p>(긴 이름 / 짧은 이름)<br /> </p> </td>
   <td> 유형 <br /> </td>
   <td> 설명 <br /> </td>
  </tr>
  <tr>
   <td> rootPath / rp<br /> </td>
   <td> 문자열 </td>
   <td> 루트 경로 검색</td>
  </tr>
  <tr>
   <td> queryParams / qp<br /> </td>
   <td> 문자열</td>
   <td> 검색 쿼리</td>
  </tr>
  <tr>
   <td> contentMode / cm<br /> </td>
   <td> 부울</td>
   <td> true면 콘텐츠 모드가 활성화됩니다<br /> </td>
  </tr>
  <tr>
   <td> colsValue / cv<br /> </td>
   <td> 문자열[]</td>
   <td> 검색된 속성(colsSelection에서 확인된 값이 확인란으로 표시됨)</td>
  </tr>
  <tr>
   <td> extraCols / ec<br /> </td>
   <td> 문자열[]</td>
   <td> 검색된 추가 속성(쉼표로 구분된 텍스트 필드에 표시됨)</td>
  </tr>
  <tr>
   <td> initialSearch / is<br /> </td>
   <td> 부울</td>
   <td> true일 경우 페이지 로드 시 쿼리가 수행됩니다<br /> </td>
  </tr>
  <tr>
   <td> colsSelection / cs<br /> </td>
   <td> 문자열[]</td>
   <td> 검색된 속성 선택 사항(확인란으로 표시됨)</td>
  </tr>
  <tr>
   <td> showGridOnly / sgo<br /> </td>
   <td> 부울</td>
   <td> true일 경우 검색 패널은 표시하지 않고 그리드만 표시합니다 <br /> </td>
  </tr>
  <tr>
   <td> searchPanelCollected / spc</td>
   <td> 부울</td>
   <td> true일 경우 로드 시 검색 패널이 축소됩니다</td>
  </tr>
  <tr>
   <td> hideRootPath / hrp</td>
   <td> 부울</td>
   <td> true이면 루트 경로 필드를 숨깁니다.</td>
  </tr>
  <tr>
   <td> hideQueryParams / hqp</td>
   <td> 부울</td>
   <td> true이면 는 쿼리 필드를 숨깁니다</td>
  </tr>
  <tr>
   <td> hideContentMode / hcm</td>
   <td> 부울</td>
   <td> true이면 는 컨텐츠 모드 필드를 숨깁니다</td>
  </tr>
  <tr>
   <td> hideColsSelection / hcs</td>
   <td> 부울</td>
   <td> true이면 열 선택 필드를 숨깁니다.</td>
  </tr>
  <tr>
   <td> hideExtraCols / hec</td>
   <td> 부울</td>
   <td> true이면 추가 열 필드를 숨깁니다.</td>
  </tr>
  <tr>
   <td> hideSearchButton</td>
   <td> 부울</td>
   <td> true이면 는 검색 단추를 숨깁니다</td>
  </tr>
  <tr>
   <td> hideSaveButton / 저장</td>
   <td> 부울</td>
   <td> true이면 저장 단추를 숨깁니다.</td>
  </tr>
  <tr>
   <td> hideExportButton / hexpb</td>
   <td> 부울</td>
   <td> true이면 내보내기 단추를 숨깁니다</td>
  </tr>
  <tr>
   <td> hideImportButton / hib</td>
   <td> 부울</td>
   <td> true이면 는 가져오기 단추를 숨깁니다</td>
  </tr>
  <tr>
   <td> hideResultNumber / hrn</td>
   <td> 부울</td>
   <td> true이면 격자 검색 결과 번호 텍스트를 숨깁니다.</td>
  </tr>
  <tr>
   <td> hideInsertButton / hinsertb</td>
   <td> 부울</td>
   <td> true이면 격자 삽입 단추를 숨깁니다.</td>
  </tr>
  <tr>
   <td> hideDeleteButton / hdelb</td>
   <td> 부울</td>
   <td> true이면 격자 삭제 단추를 숨깁니다.</td>
  </tr>
  <tr>
   <td> hidePathCol / hpc</td>
   <td> 부울</td>
   <td> true이면 격자 "경로" 열을 숨깁니다.</td>
  </tr>
 </tbody>
</table>

### 벌크 편집기 기반 구성 요소 개발: 제품 목록 구성 요소 {#developing-a-bulk-editor-based-component-the-product-list-component}

이 섹션에서는 벌크 편집기를 사용하는 방법에 대한 개요를 제공하고 벌크 편집기를 기반으로 기존 Geometrixx 구성 요소에 대한 설명을 제공합니다. 제품 목록 구성 요소입니다.

제품 목록 구성 요소를 사용하면 사용자가 데이터 테이블을 표시하고 편집할 수 있습니다. 예를 들어 제품 목록 구성 요소를 사용하여 카탈로그의 제품을 나타낼 수 있습니다. 정보는 표준 HTML 표에 표시되며, 모든 편집은 **편집** 대화 상자에 BulkEditor 위젯이 들어 있습니다. (이 벌크 편집기는 /etc/importers/bulkeditor.html 또는 도구 메뉴를 통해 액세스할 수 있는 편집기와 동일합니다.) 제품 목록 구성 요소가 특정 제한된 벌크 편집기 기능용으로 구성되었습니다. 벌크 편집기의 모든 부분(또는 벌크 편집기에서 파생된 구성 요소)을 구성할 수 있습니다.

벌크 편집기를 사용하여 행을 추가, 수정, 삭제, 필터링 및 내보내고, 수정 사항을 저장하고, 행 세트를 가져올 수 있습니다. 모든 행은 제품 목록 구성 요소 인스턴스 자체 아래에 노드로 저장됩니다. 모든 셀은 각 노드의 속성입니다. 이 옵션은 디자인 선택이며, 쉽게 변경할 수 있습니다. 예를 들어 리포지토리의 다른 위치에 노드를 저장할 수 있습니다. 쿼리 서블릿의 역할은 표시할 노드 목록을 반환하는 것입니다. 검색 경로는 제품 목록 인스턴스로 정의됩니다.

제품 목록 구성 요소의 소스 코드는 /apps/geometrixx/components/productlist의 저장소에서 사용할 수 있으며, 모든 AEM 구성 요소와 같은 여러 부분으로 구성됩니다.

* HTML 렌더링: 렌더링은 JSP 파일(/apps/geometrixx/components/productlist/productlist.jsp)에서 수행됩니다. JSP는 현재 제품 목록 구성 요소의 하위 노드를 읽고 각 노드를 HTML 테이블의 행으로 표시합니다.
* 편집 대화 상자 - 벌크 편집기 구성을 정의합니다. 구성 요소의 요구 사항에 맞게 대화 상자를 구성합니다. 그리드 또는 검색에서 수행되는 사용 가능한 열 및 가능한 작업. 자세한 내용은 [대량 편집기 구성 속성](#bulk-editor-configuration-properties) 를 참조하십시오.

다음은 대화 상자 하위 노드의 XML 표현입니다.

```xml
        <editor
            jcr:primaryType="cq:Widget"
            colsSelection="[ProductId,ProductName,Color,CatalogCode,SellingSku]"
            colsValue="[ProductId,ProductName,Color,CatalogCode,SellingSku]"
            contentMode="false"
            exportURL="/etc/importers/bulkeditor/export.tsv"
            extraCols="Selection"
            hideColsSelection="false"
            hideContentMode="true"
            hideDeleteButton="false"
            hideExportButton="false"
            hideExtraCols="true"
            hideImportButton="false"
            hideInsertButton="false"
            hideMoveButtons="false"
            hidePathCol="true"
            hideRootPath="true"
            hideSaveButton="false"
            hideSearchButton="false"
            importURL="/etc/importers/bulkeditor/import"
            initialSearch="true"
            insertedResourceType="geometrixx/components/productlist/sku"
            queryParams=""
            queryURL="/etc/importers/bulkeditor/query.json"
            saveURL="/etc/importers/bulkeditor/save"
            xtype="bulkeditor">
            <saveButton
                jcr:primaryType="nt:unstructured"
                text="Save modifications"/>
            <searchButton
                jcr:primaryType="nt:unstructured"
                text="Apply filter"/>
            <queryParamsInput
                jcr:primaryType="nt:unstructured"
                fieldDescription="Enter here your filters"
                fieldLabel="Filters"/>
            <searchPanel
                jcr:primaryType="nt:unstructured"
                height="200">
                <defaults
                    jcr:primaryType="nt:unstructured"
                    labelWidth="150"/>
            </searchPanel>
            <grid
                jcr:primaryType="nt:unstructured"
                height="275"/>
            <store jcr:primaryType="nt:unstructured">
                <sortInfo
                    jcr:primaryType="nt:unstructured"
                    direction="ASC"
                    field="CatalogCode"/>
            </store>
            <colModel
                jcr:primaryType="nt:unstructured"
                width="150"/>
            <colsMetadata jcr:primaryType="nt:unstructured">
                <Selection
                    jcr:primaryType="nt:unstructured"
                    checkbox="true"
                    forcedPosition="0"
                    headerText=""/>
                <ProductId
                    jcr:primaryType="nt:unstructured"
                    cellCls="productlist-cell-productid"
                    headerText="Product Id"/>
                <ProductName
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #FFCC99;"
                    headerText="Product Name"/>
                <CatalogCode
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #EDEDED;"
                    headerText="Catalog Code"/>
                <Color jcr:primaryType="nt:unstructured">
                    <editor
                        jcr:primaryType="nt:unstructured"
                        store="[Blue,Red,Yellow]"
                        triggerAction="all"
                        typeAhead="true"
                        xtype="combo"/>
                </Color>
                <SellingSku
                    jcr:primaryType="nt:unstructured"
                    headerText="Sku Id"/>
            </colsMetadata>
        </editor>
```

### 벌크 편집기 구성 속성 {#bulk-editor-configuration-properties}

벌크 편집기의 모든 부분을 구성할 수 있습니다. 다음 표에는 벌크 편집기의 모든 구성 속성이 나와 있습니다.

<table>
 <tbody>
  <tr>
   <td>속성 이름</td>
   <td>정의</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>검색 루트 경로</td>
  </tr>
  <tr>
   <td>queryParams</td>
   <td>검색 쿼리</td>
  </tr>
  <tr>
   <td>contentMode</td>
   <td>컨텐츠 모드를 활성화하려면 True입니다. 속성은 검색 결과 노드가 아니라 jcr:content 노드에서 읽습니다.</td>
  </tr>
  <tr>
   <td>colsValue</td>
   <td>검색된 속성(colsSelection에서 선택한 값이 확인란으로 표시됨)</td>
  </tr>
  <tr>
   <td>extraCols</td>
   <td>검색된 추가 속성(텍스트 필드에 쉼표로 표시됨)</td>
  </tr>
  <tr>
   <td>initialSearch</td>
   <td>페이지 로드 시 쿼리를 수행하려면 True입니다</td>
  </tr>
  <tr>
   <td>colsSelection</td>
   <td>속성 선택 사항(확인란으로 표시됨)을 검색했습니다.</td>
  </tr>
  <tr>
   <td>showGridOnly</td>
   <td>True로 설정하면 검색 패널이 아니라 그리드만 표시되고 initialSearch를 true로 설정하는 것을 잊지 않습니다.</td>
  </tr>
  <tr>
   <td>searchPanelCollected</td>
   <td>기본적으로 검색 패널을 축소하려면 True입니다</td>
  </tr>
  <tr>
   <td>hideRootPath</td>
   <td>루트 경로 필드 숨기기</td>
  </tr>
  <tr>
   <td>hideQueryParams</td>
   <td>쿼리 필드 숨기기</td>
  </tr>
  <tr>
   <td>hideContentMode</td>
   <td>컨텐츠 모드 필드 숨기기</td>
  </tr>
  <tr>
   <td>hideColsSelection</td>
   <td>열 선택 필드 숨기기</td>
  </tr>
  <tr>
   <td>hideExtraCols</td>
   <td>추가 열 필드 숨기기</td>
  </tr>
  <tr>
   <td>hideSearchButton</td>
   <td>검색 단추 숨기기</td>
  </tr>
  <tr>
   <td>hideSaveButton</td>
   <td>저장 단추 숨기기</td>
  </tr>
  <tr>
   <td>hideExportButton</td>
   <td>내보내기 숨기기 단추</td>
  </tr>
  <tr>
   <td>hideImportButton</td>
   <td>가져오기 단추 숨기기</td>
  </tr>
  <tr>
   <td>hideResultNumber</td>
   <td>그리드 검색 결과 번호 텍스트 숨기기</td>
  </tr>
  <tr>
   <td>hideInsertButton</td>
   <td>격자 삽입 단추 숨기기</td>
  </tr>
  <tr>
   <td>hideDeleteButton</td>
   <td>그리드 삭제 단추 숨기기</td>
  </tr>
  <tr>
   <td>hidePathCol</td>
   <td>격자 "경로" 열 숨기기</td>
  </tr>
  <tr>
   <td>queryURL</td>
   <td>쿼리 서블릿에 대한 경로</td>
  </tr>
  <tr>
   <td>exportURL</td>
   <td>서블릿을 내보내는 경로</td>
  </tr>
  <tr>
   <td>importURL</td>
   <td>서블릿을 가져올 경로</td>
  </tr>
  <tr>
   <td>insertedResourceType</td>
   <td>행이 삽입될 때 노드에 추가된 리소스 유형</td>
  </tr>
  <tr>
   <td>saveButton</td>
   <td>저장 단추 위젯 구성</td>
  </tr>
  <tr>
   <td>searchButton</td>
   <td>검색 단추 위젯 구성</td>
  </tr>
  <tr>
   <td>exportButton</td>
   <td>내보내기 단추 위젯 구성</td>
  </tr>
  <tr>
   <td>importButton</td>
   <td>가져오기 단추 위젯 구성</td>
  </tr>
  <tr>
   <td>searchPanel</td>
   <td>검색 패널 위젯 구성</td>
  </tr>
  <tr>
   <td>그리드</td>
   <td>그리드 위젯 구성</td>
  </tr>
  <tr>
   <td>스토어</td>
   <td>저장 구성</td>
  </tr>
  <tr>
   <td>colModel</td>
   <td>그리드 열 모델 구성</td>
  </tr>
  <tr>
   <td>rootPathInput</td>
   <td>rootPath 위젯 구성</td>
  </tr>
  <tr>
   <td>queryParamsInput</td>
   <td>queryParams 위젯 구성</td>
  </tr>
  <tr>
   <td>contentModeInput</td>
   <td>contentMode 위젯 구성</td>
  </tr>
  <tr>
   <td>colsSelectionInput</td>
   <td>colsSelection 위젯 구성</td>
  </tr>
  <tr>
   <td>extraColsInput</td>
   <td>extraCols 위젯 구성</td>
  </tr>
  <tr>
   <td>colsMetadata</td>
   <td>열 메타데이터 구성. 가능한 속성은 열의 모든 셀에 적용되어 있습니다. <br />
    <ul>
     <li>cellStyle: html 스타일 </li>
     <li>cellCls: css 클래스 </li>
     <li>readOnly: 값을 변경할 수 없는 경우 true </li>
     <li>확인란: true 로 설정하면 열의 모든 셀을 확인란으로 정의할 수 있습니다(true/false 값) </li>
     <li>forcedPosition: 그리드에 열을 배치해야 하는 위치를 지정하는 정수 값(0과 열 수 사이-1)<p><br /> </p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 열 메타데이터 구성 {#columns-metadata-configuration}

각 열에 대해 구성할 수 있습니다.

* 표시 속성: html 스타일, CSS 클래스 및 읽기 전용

* 확인란
* 강제 지위

CSS 및 읽기 전용 열

벌크 편집기에는 세 개의 열 구성이 있습니다.

* 셀 CSS 클래스 이름(cellCls): 구성된 열의 각 셀에 추가되는 CSS 클래스 이름입니다.
* 셀 스타일(cellStyle): 구성된 열의 각 셀에 추가되는 HTML 스타일입니다.
* 읽기 전용(readOnly): 구성된 열의 각 셀에 대해 읽기 전용이 설정됩니다.

구성은 다음 구성으로 정의해야 합니다.

```
"colsMetadata": {
"Column name": {
     "cellStyle": "html style",
     "cellCls": "CSS class",
     "readOnly": true/false
}
}
```

다음 예는 productlist 구성 요소(/apps/geometrixx/components/productlist/dialog/items/editor/colsMetadata)에서 찾을 수 있습니다.

```xml
            <colsMetadata jcr:primaryType="nt:unstructured">
                <Selection
                    jcr:primaryType="nt:unstructured"
                    checkbox="true"
                    forcedPosition="0"
                    headerText=""/>
                <ProductId
                    jcr:primaryType="nt:unstructured"
                    cellCls="productlist-cell-productid"
                    headerText="Product Id"/>
                <ProductName
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #FFCC99;"
                    headerText="Product Name"/>
                <CatalogCode
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #EDEDED;"
                    headerText="Catalog Code"/>
                <Color jcr:primaryType="nt:unstructured">
                    <editor
                        jcr:primaryType="nt:unstructured"
                        store="[Blue,Red,Yellow]"
                        triggerAction="all"
                        typeAhead="true"
                        xtype="combo"/>
                </Color>
                <SellingSku
                    jcr:primaryType="nt:unstructured"
                    headerText="Sku Id"/>
            </colsMetadata>
```

**확인란**

확인란 구성 속성을 true로 설정하면 열의 모든 셀이 확인란으로 렌더링됩니다. 확인란을 선택하면 **true** 서버 저장 서블릿에 대해, **false** 그렇지 않은 경우 헤더 메뉴에서 다음을 수행할 수도 있습니다 **모두 선택** 또는 **없음 선택**. 이 옵션은 선택한 헤더가 확인란 열의 헤더인 경우 활성화됩니다.

이전 예에서 선택 열에는 확인란=&quot;true&quot;인 확인란만 포함됩니다.

**강제 위치**

강제 위치 메타데이터 forcedPosition을 사용하면 그리드 내에 열이 배치되는 위치를 지정할 수 있습니다. 0이 첫 번째이고 &lt;number of=&quot;&quot; columns=&quot;&quot;>-1이 마지막 위치입니다. 다른 모든 값은 무시됩니다.

이전 예에서 선택 열은 forcedPosition=&quot;0&quot;이라는 첫 번째 열입니다.

### 쿼리 서블릿 {#query-servlet}

기본적으로 Query 서블릿은 `/libs/wcm/core/components/bulkeditor/json.java`. 데이터를 검색하도록 다른 경로를 구성할 수 있습니다.

쿼리 서블릿은 다음과 같이 작동합니다. GQL 쿼리 및 반환할 열을 수신하여 결과를 계산한 다음 결과를 벌크 편집기로 JSON 스트림으로 다시 전송합니다.

제품 목록 구성 요소 사례에서 쿼리 서블릿으로 전송되는 두 매개 변수는 다음과 같습니다.

* 쿼리: &quot;path:/content/geometrixx/en/customers/jcr:content/par/productlist Cube&quot;
* cols: &quot;Selection,ProductId,ProductName,Color,CatalogCode,SellingSku&quot;

그리고 반환된 JSON 스트림은 다음과 같습니다.

```
{
  "hits": [{
      "jcr:path": "/content/geometrixx/en/products/jcr:content/par/productlist/1258674828905",
      "ProductId": "21",
      "ProductName": "Cube",
      "Color": "Blue",
      "CatalogCode": "43244",
      "SellingSku": "32131"
    }
  ],
  "results": 1
}
```

각 히트는 하나의 노드 및 해당 속성에 해당하며 그리드에 행으로 표시됩니다.

쿼리 서블릿을 확장하여 복잡한 상속 모델 또는 특정 논리 위치에 저장된 반환 노드를 반환할 수 있습니다. 쿼리 서블릿을 사용하여 복잡한 계산을 수행할 수 있습니다. 그리드는 저장소에 있는 여러 노드의 집합인 행을 표시할 수 있습니다. 이 경우 이러한 행의 수정 및 저장을 저장 서블릿으로 관리해야 합니다.

### 서블릿 저장 {#save-servlet}

벌크 편집기의 기본 구성에서 각 행은 노드이고 이 노드의 경로는 행 레코드에 저장됩니다. 벌크 편집기는 jcr 경로를 통해 행과 노드 사이의 링크를 유지합니다. 사용자가 그리드를 편집하면 모든 수정 사항 목록이 빌드됩니다. 사용자가 클릭하면 **저장**&#x200B;를 입력하면 업데이트된 속성 값이 있는 각 경로로 POST 쿼리가 전송됩니다. 이는 Sling 개념의 기반이며 각 셀이 노드의 속성인 경우 잘 작동합니다. 하지만 상속 계산을 수행하기 위해 쿼리 서블릿이 구현된 경우 이 모델은 쿼리 서블릿이 반환한 속성으로 다른 노드에서 상속될 수 없습니다.

저장 서블릿 개념은 수정 사항이 각 노드에 직접 게시되지 않고 저장 작업을 수행하는 하나의 서블릿에 게시된다는 것입니다. 이렇게 하면 이 서블릿이 수정 사항을 분석하고 올바른 노드에 속성을 저장할 수 있습니다.

업데이트된 각 속성은 다음 형식의 서블릿으로 전송됩니다.

* 매개 변수 이름: &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>

   예: /content/geometrixx/en/products/jcr:content/par/productlist/1258674859000/SellingSku

* 값: &lt;value>

   예: 12123

서블릿은 catalogCode 속성이 저장되는 위치를 알고 있어야 합니다.

기본 저장 서블릿 구현은 /libs/wcm/bulkeditor/save/POST.jsp에서 사용할 수 있으며 제품 목록 구성 요소에서 사용됩니다. 요청에서 모든 매개 변수를 가져옵니다(다음을 포함). &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;> JCR API를 사용하여 노드에 속성을 형식 및 씁니다. 또한 노드가 없는 경우(그리드가 삽입된 행) 노드가 만들어집니다.

기본 코드는 서버가 기본적으로 수행하는 작업(POST의 경우)을 다시 구현하므로 사용하지 않아야 합니다 &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>)과 는 속성 상속 모델을 관리할 Save 서블릿을 빌드하기 위한 좋은 시작점일 뿐입니다.
