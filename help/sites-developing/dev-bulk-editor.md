---
title: 벌크 편집기 개발
description: 태깅을 통해 컨텐츠를 분류하고 구성할 수 있습니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 8753aaab-959f-459b-bdb6-057cbe05d480
source-git-commit: 26c0411d6cc16f4361cfa9e6b563eba0bfafab1e
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 2%

---

# 벌크 편집기 개발{#developing-the-bulk-editor}

이 섹션에서는 벌크 편집기 도구를 개발하는 방법과 벌크 편집기를 기반으로 하는 제품 목록 구성 요소를 확장하는 방법을 설명합니다.

## 벌크 편집기 쿼리 매개 변수 {#bulk-editor-query-parameters}

벌크 편집기로 작업할 때 URL에 추가하여 특정 구성으로 벌크 편집기를 호출할 수 있는 여러 쿼리 매개 변수가 있습니다. 예를 들어 제품 목록 구성 요소에서와 같이 벌크 편집기를 항상 특정 구성과 함께 사용하려면 다음을 편집해야 합니다 `bulkeditor.jsp` ( /libs/wcm/core/components/bulkeditor에서) 또는 특정 구성으로 구성 요소를 만듭니다. 쿼리 매개 변수를 사용하여 변경한 내용은 영구적이지 않습니다.

예를 들어 브라우저의 URL에 다음을 입력하는 경우:

`https://<servername><port_number>/etc/importers/bulkeditor.html?rootPath=/content/geometrixx/en&queryParams=geometrixx&initialSearch=true&hrp=true`

벌크 편집기 가 **루트 경로** hrp=true인 필드는 필드를 숨깁니다. hrp=false 매개 변수를 사용하면 필드가 표시됩니다(기본값).

다음은 벌크 편집기 쿼리 매개 변수 목록입니다.

>[!NOTE]
>
>각 매개 변수의 이름은 길고 짧을 수 있습니다. 예를 들어 검색 루트 경로의 긴 이름은 입니다. `rootPath`: 짧은 것은 입니다. `rp`. 긴 이름이 정의되지 않으면 짧은 이름을 요청에서 읽습니다.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p> 매개변수</p> <p>(긴 이름/짧은 이름)<br /> </p> </td>
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
   <td> true인 경우 콘텐츠 모드가 활성화됩니다.<br /> </td>
  </tr>
  <tr>
   <td> colsValue / cv<br /> </td>
   <td> 문자열[]</td>
   <td> 검색된 속성(colsSelection에서 선택된 값이 확인란으로 표시됨)</td>
  </tr>
  <tr>
   <td> extraCols / ec<br /> </td>
   <td> 문자열[]</td>
   <td> 추가 검색 속성(쉼표로 구분된 텍스트 필드에 표시됨)</td>
  </tr>
  <tr>
   <td> initialSearch/<br /> </td>
   <td> 부울</td>
   <td> true인 경우 페이지 로드 시 쿼리가 수행됩니다<br /> </td>
  </tr>
  <tr>
   <td> colsSelection / cs<br /> </td>
   <td> 문자열[]</td>
   <td> 검색된 속성 선택(확인란으로 표시됨)</td>
  </tr>
  <tr>
   <td> showGridOnly / sgo<br /> </td>
   <td> 부울</td>
   <td> true인 경우 검색 패널은 표시하지 않고 그리드만 표시합니다. <br /> </td>
  </tr>
  <tr>
   <td> searchPanelCollapsed / spc</td>
   <td> 부울</td>
   <td> true인 경우 로드 시 검색 패널이 축소됩니다.</td>
  </tr>
  <tr>
   <td> hideRootPath / hrp</td>
   <td> 부울</td>
   <td> true이면 루트 경로 필드를 숨깁니다.</td>
  </tr>
  <tr>
   <td> hideQueryParams / hqp</td>
   <td> 부울</td>
   <td> true이면 쿼리 필드를 숨깁니다.</td>
  </tr>
  <tr>
   <td> hideContentMode / hcm</td>
   <td> 부울</td>
   <td> true이면 콘텐츠 모드 필드를 숨깁니다.</td>
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
   <td> true이면 검색 단추를 숨깁니다.</td>
  </tr>
  <tr>
   <td> hideSaveButton / hsavep</td>
   <td> 부울</td>
   <td> true이면 저장 단추를 숨깁니다.</td>
  </tr>
  <tr>
   <td> hideExportButton / hexpb</td>
   <td> 부울</td>
   <td> true인 경우 내보내기 단추를 숨깁니다.</td>
  </tr>
  <tr>
   <td> hideImportButton / hib</td>
   <td> 부울</td>
   <td> true이면 가져오기 단추를 숨깁니다.</td>
  </tr>
  <tr>
   <td> hideResultNumber / hrn</td>
   <td> 부울</td>
   <td> true이면 그리드 검색 결과 번호 텍스트를 숨깁니다.</td>
  </tr>
  <tr>
   <td> hideInsertButton / hinsertb</td>
   <td> 부울</td>
   <td> true이면 격자 삽입 단추를 숨깁니다.</td>
  </tr>
  <tr>
   <td> hideDeleteButton / hdelb</td>
   <td> 부울</td>
   <td> true인 경우 그리드 삭제 단추를 숨깁니다.</td>
  </tr>
  <tr>
   <td> hidePathCol / hpc</td>
   <td> 부울</td>
   <td> true인 경우, 격자 "경로" 열을 숨깁니다.</td>
  </tr>
 </tbody>
</table>

### 벌크 편집기 기반 구성 요소 개발: 제품 목록 구성 요소 {#developing-a-bulk-editor-based-component-the-product-list-component}

이 섹션에서는 벌크 편집기 사용 방법에 대한 개요를 제공하고 벌크 편집기를 기반으로 하는 기존 Geometrixx 구성 요소인 제품 목록 구성 요소에 대해 설명합니다.

제품 목록 구성 요소를 사용하여 데이터 테이블을 표시하고 편집할 수 있습니다. 예를 들어 제품 목록 구성 요소를 사용하여 카탈로그에 제품을 표시할 수 있습니다. 이 정보는 표준 HTML 테이블에 표시되며 모든 편집은 **편집** 대화 상자에 BulkEditor 위젯이 포함되어 있습니다. (이 벌크 편집기는 /etc/importers/bulkeditor.html 또는 도구 메뉴를 통해 액세스할 수 있는 편집기와 동일합니다.) 제품 목록 구성 요소는 제한된 특정 벌크 편집기 기능을 위해 구성되었습니다. 벌크 편집기의 모든 부분(또는 벌크 편집기에서 파생된 구성 요소)을 구성할 수 있습니다.

벌크 편집기를 사용하여 행을 추가, 수정, 삭제, 필터링 및 내보내고, 수정 사항을 저장하고 행 집합을 가져올 수 있습니다. 모든 행은 제품 목록 구성 요소 인스턴스 아래의 노드로 저장됩니다. 모든 셀은 각 노드의 속성입니다. 이는 디자인적인 선택이며 쉽게 변경할 수 있습니다. 예를 들어 노드를 저장소의 다른 위치에 저장할 수 있습니다. 쿼리 서블릿의 역할은 표시할 노드 목록을 반환하는 것입니다. 검색 경로는 제품 목록 인스턴스로 정의됩니다.

제품 목록 구성 요소의 소스 코드는 /apps/geometrixx/components/productlist의 저장소에서 사용할 수 있으며 모든 Adobe Experience Manager(AEM) 구성 요소와 같은 여러 부분으로 구성됩니다.

* HTML 렌더링: 렌더링은 JSP 파일(/apps/geometrixx/components/productlist/productlist.jsp)에서 수행됩니다. JSP는 현재 제품 목록 구성 요소의 하위 노드를 읽고 각각을 HTML 테이블의 행으로 표시합니다.
* 편집 대화 상자 - 여기서 벌크 편집기 구성을 정의합니다. 구성 요소의 요구 사항과 일치하도록 대화 상자를 구성합니다. 열 사용 가능 및 그리드 또는 검색에서 수행되는 가능한 작업입니다. 다음을 참조하십시오 [벌크 편집기 구성 속성](#bulk-editor-configuration-properties) 모든 구성 속성에 대해 설명합니다.

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

벌크 편집기의 모든 부분을 구성할 수 있습니다. 다음 표에는 벌크 편집기의 모든 구성 속성이 나열되어 있습니다.

<table>
 <tbody>
  <tr>
   <td>속성 이름</td>
   <td>정의</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>루트 경로 검색</td>
  </tr>
  <tr>
   <td>queryParams</td>
   <td>검색 쿼리</td>
  </tr>
  <tr>
   <td>contentMode</td>
   <td>컨텐츠 모드를 활성화하려면 True로 설정합니다. 속성은 검색 결과 노드가 아닌 jcr:content 노드에서 읽힙니다.</td>
  </tr>
  <tr>
   <td>colsValue</td>
   <td>검색된 속성(colsSelection에서 선택된 값이 확인란으로 표시됨)</td>
  </tr>
  <tr>
   <td>extraCols</td>
   <td>추가 검색 속성(쉼표로 구분된 텍스트 필드에 표시됨)</td>
  </tr>
  <tr>
   <td>initialSearch</td>
   <td>페이지 로드 시 쿼리를 수행하려면 True입니다</td>
  </tr>
  <tr>
   <td>열 선택</td>
   <td>검색된 속성 선택(확인란으로 표시됨)</td>
  </tr>
  <tr>
   <td>showGridOnly</td>
   <td>True로 설정하면 검색 패널은 표시되지 않고 격자선만 표시됩니다(initialSearch를 true로 설정하는 것을 잊지 마십시오).</td>
  </tr>
  <tr>
   <td>searchPanelCollapsed</td>
   <td>기본적으로 검색 패널을 축소하려면 True입니다.</td>
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
   <td>콘텐츠 모드 필드 숨기기</td>
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
   <td>내보내기 단추 숨기기</td>
  </tr>
  <tr>
   <td>hideImportButton</td>
   <td>가져오기 단추 숨기기</td>
  </tr>
  <tr>
   <td>hideResultNumber</td>
   <td>격자 검색 결과 번호 텍스트 숨기기</td>
  </tr>
  <tr>
   <td>hideInsertButton</td>
   <td>격자 삽입 단추 숨기기</td>
  </tr>
  <tr>
   <td>hideDeleteButton</td>
   <td>격자 삭제 단추 숨기기</td>
  </tr>
  <tr>
   <td>hidePathCol</td>
   <td>격자 "경로" 열 숨기기</td>
  </tr>
  <tr>
   <td>queryURL</td>
   <td>쿼리 서블릿 경로</td>
  </tr>
  <tr>
   <td>exportURL</td>
   <td>내보내기 서블릿 경로</td>
  </tr>
  <tr>
   <td>importURL</td>
   <td>가져오기 서블릿 경로</td>
  </tr>
  <tr>
   <td>insertedResourceType</td>
   <td>행이 삽입될 때 노드에 추가된 리소스 유형</td>
  </tr>
  <tr>
   <td>saveButton</td>
   <td>단추 위젯 구성 저장</td>
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
   <td>격자</td>
   <td>그리드 위젯 구성</td>
  </tr>
  <tr>
   <td>스토어</td>
   <td>저장소 구성</td>
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
   <td>열 메타데이터 구성 가능한 속성은 열의 모든 셀에 적용됩니다. <br />
    <ul>
     <li>cellStyle: html 스타일 </li>
     <li>cellCls: css 클래스 </li>
     <li>readOnly: 값을 변경할 수 없는 true </li>
     <li>확인란: true 를 클릭하여 열의 모든 셀을 확인란(true/false 값)으로 정의합니다. </li>
     <li>forcedPosition: 열이 그리드에 배치될 위치를 지정하는 정수 값(0에서 열 개수 - 1 사이)<p><br /> </p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 열 메타데이터 구성 {#columns-metadata-configuration}

각 열에 대해 를 구성할 수 있습니다.

* 디스플레이 속성: html 스타일, CSS 클래스 및 읽기 전용

* 확인란
* 강압적인 입장

CSS 및 읽기 전용 열

벌크 편집기에는 세 개의 열 구성이 있습니다.

* 셀 CSS 클래스 이름(cellCls): 구성된 열의 각 셀에 추가되는 CSS 클래스 이름입니다.
* 셀 스타일(cellStyle): 구성된 열의 각 셀에 추가되는 HTML 스타일입니다.
* 읽기 전용(읽기 전용): 구성된 열의 각 셀에 대해 읽기 전용이 설정됩니다.

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

다음 예제는 productlist 구성 요소(/apps/geometrixx/components/productlist/dialog/items/editor/colsMetadata)에서 찾을 수 있습니다.

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

checkbox 구성 속성이 true로 설정되면 열의 모든 셀이 확인란으로 렌더링됩니다. 선택한 상자가 **true** 서버 저장 서블릿에 **false** 그렇지 않으면. 헤더 메뉴에서 다음을 수행할 수도 있습니다 **모두 선택** 또는 **선택 안 함**. 이러한 옵션은 선택한 헤더가 확인란 열의 헤더인 경우 활성화됩니다.

앞의 예에서 선택 열에는 checkbox=&quot;true&quot;인 확인란만 포함됩니다.

**강제 위치**

강제 위치 메타데이터 forcedPosition을 사용하면 그리드 내에서 열이 배치되는 위치를 지정할 수 있습니다. 0이 첫 번째 위치이고 &lt;number of=&quot;&quot; columns=&quot;&quot;>-1이 마지막 위치입니다. 다른 모든 값은 무시됩니다.

앞의 예에서 선택 열은 forcedPosition=&quot;0&quot;인 첫 번째 열입니다.

### 쿼리 서블릿 {#query-servlet}

기본적으로 쿼리 서블릿은에서 찾을 수 있습니다. `/libs/wcm/core/components/bulkeditor/json.java`. 데이터를 검색할 다른 경로를 구성할 수 있습니다.

쿼리 서블릿은 다음과 같이 작동합니다. GQL 쿼리와 반환할 열을 수신하고 결과를 계산한 다음 결과를 벌크 편집기에 JSON 스트림으로 다시 보냅니다.

제품 목록 구성 요소의 경우 쿼리 서블릿에 전송되는 두 매개 변수는 다음과 같습니다.

* 쿼리: &quot;path:/content/geometrixx/en/customers/jcr:content/par/productlist Cube&quot;
* cols: &quot;Selection,ProductId,ProductName,Color,CatalogCode,SellingSku&quot;

JSON 스트림은 다음과 같이 반환됩니다.

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

쿼리 서블릿을 확장하여 복잡한 상속 모델을 반환하거나 특정 논리 위치에 저장된 노드를 반환할 수 있습니다. 쿼리 서블릿을 사용하여 모든 종류의 복잡한 계산을 수행할 수 있습니다. 그리드는 저장소의 여러 노드를 집계한 행을 표시할 수 있습니다. 이 경우 이러한 행의 수정 및 저장은 저장 서블릿에서 관리해야 합니다.

### 서블릿 저장 {#save-servlet}

벌크 편집기의 기본 구성에서 각 행은 노드이며 이 노드의 경로는 행 레코드에 저장됩니다. 벌크 편집기는 jcr 경로를 통해 행과 노드 간의 링크를 유지합니다. 사용자가 그리드를 편집하면 모든 수정 사항 목록이 작성됩니다. 사용자가 클릭할 때 **저장**, POST 쿼리가 업데이트된 속성 값이 있는 각 경로로 전송됩니다. 이는 Sling 개념의 기초이며 각 셀이 노드의 속성인 경우 잘 작동한다. 그러나 쿼리 서블릿이 상속 계산을 수행하도록 구현된 경우 이 모델은 쿼리 서블릿이 반환하는 속성으로 다른 노드에서 상속될 수 없습니다.

Save servlet 개념은 수정 사항이 각 노드에 직접 게시되지 않고 저장 작업을 수행하는 하나의 서블릿에 게시되는 것입니다. 이렇게 하면 이 서블릿에서 수정 사항을 분석하고 오른쪽 노드의 속성을 저장할 수 있습니다.

업데이트된 각 속성은 다음 형식으로 서블릿에 전송됩니다.

* 매개 변수 이름: &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>

  예: /content/geometrixx/en/products/jcr:content/par/productlist/1258674859000/SellingSku

* 값: &lt;value>

  예: 12123

서블릿은 catalogCode 속성이 저장된 위치를 알아야 합니다.

기본 저장 서블릿 구현은 /libs/wcm/bulkeditor/save/POST.jsp에서 사용할 수 있으며 제품 목록 구성 요소에서 사용됩니다. 요청에서 모든 매개 변수를 가져옵니다( 사용). &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;> format)을 참조하고 JCR API를 사용하여 노드에 속성을 기록합니다. 노드가 없는 경우(그리드가 삽입된 행) 노드도 생성합니다.

기본 코드는 서버가 기본적으로 수행하는 작업(의 POST)을 재구현하기 때문에 그대로 사용해서는 안 됩니다. &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>) 따라서 속성 상속 모델을 관리할 수 있는 저장 서블릿을 빌드하는 좋은 시작점입니다.
