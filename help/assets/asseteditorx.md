---
title: 자산 편집기 확장
description: 사용자 지정 구성 요소를 사용하여 자산 편집기의 기능을 확장하는 방법을 알아봅니다.
contentOwner: AG
role: User, Admin
feature: Developer Tools
exl-id: de1c63c1-a0e5-470b-8d83-b594513a5dbd
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 14%

---

# 자산 편집기 확장 {#extending-asset-editor}

에셋 편집기 는 에셋 공유를 통해 찾은 에셋을 클릭하면 열리는 페이지로, 사용자가 에셋의 메타데이터, 썸네일, 제목 및 태그 같은 측면을 편집할 수 있도록 해 줍니다.

미리 정의된 편집 구성 요소를 사용한 편집기 구성은에서 다룹니다 [자산 편집기 페이지 만들기 및 구성](assets-finder-editor.md#creating-and-configuring-an-asset-editor-page).

기존 편집기 구성 요소를 사용하는 것 외에도 [!DNL Adobe Experience Manager] 개발자는 자체 구성 요소를 만들 수도 있습니다.

## 자산 편집기 템플릿 만들기 {#creating-an-asset-editor-template}

다음 샘플 페이지가 Geometrixx에 포함되어 있습니다.

* Geometrixx 샘플 페이지: `/content/geometrixx/en/press/asseteditor.html`
* 샘플 템플릿: `/apps/geometrixx/templates/asseteditor`
* 샘플 페이지 구성 요소: `/apps/geometrixx/components/asseteditor`

### Clientlib 구성 {#configuring-clientlib}

[!DNL Assets] 구성 요소는 WCM edit clientlib의 확장을 사용합니다. clientlib은에서 일반적으로 로드됩니다. `init.jsp`.

기본 clientlib 로드와 비교(코어 `init.jsp`), [!DNL Assets] 템플릿에는 다음 항목이 있어야 합니다.

* 템플릿에는 `cq.dam.edit` clientlib(대신) `cq.wcm.edit`).

* The clientlib must also be included in disabled WCM mode (for example, loaded on **publish**) to be able to render the predicates, actions, and lenses.

대부분의 경우 기존 샘플을 복사합니다. `init.jsp` (`/apps/geometrixx/components/asseteditor/init.jsp`)은(는) 이러한 요구 사항을 충족해야 합니다.

### JS 작업 구성 {#configuring-js-actions}

일부 [!DNL Assets] 구성 요소는에 정의된 JS 함수가 필요합니다. `component.js`. 이 파일을 구성 요소 디렉토리에 복사한 다음 연결합니다.

```javascript
<script type="text/javascript" src="<%= component.getPath() %>/component.js"></script>
```

샘플은에서 이 JavaScript 소스를 로드합니다. `head.jsp`(`/apps/geometrixx/components/asseteditor/head.jsp`).

### 추가 스타일 시트 {#additional-style-sheets}

일부 [!DNL Assets] 구성 요소는 위젯 라이브러리를 사용합니다. 콘텐츠 컨텍스트에서 제대로 렌더링하려면 추가 스타일 시트를 로드해야 합니다. 태그 작업 구성 요소에는 한 개 더 필요합니다.

```css
<link href="/etc/designs/geometrixx/ui.widgets.css" rel="stylesheet" type="text/css">
```

### Geometrixx 스타일시트 {#geometrixx-style-sheet}

샘플 페이지 구성 요소에서는 모든 선택기가 다음으로 시작해야 합니다. `.asseteditor` / `static.css` (`/etc/designs/geometrixx/static.css`). 모범 사례: 모두 복사 `.asseteditor` 선택기를 사용하여 스타일 시트를 만들고 원하는 대로 규칙을 조정합니다.

### FormChooser: 최종 로드된 리소스 조정 {#formchooser-adjustments-for-eventually-loaded-resources}

에셋 편집기는 양식 선택기를 사용하며, 양식 선택기와 양식의 경로를 에셋의 URL에 추가하기만 하면 동일한 양식 페이지에서 리소스(이 경우 에셋)를 편집할 수 있습니다.

예:

* 일반 양식 페이지: [http://localhost:4502/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/geometrixx/en/press/asseteditor.html)
* 양식 페이지로 로드된 자산: [http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html)

샘플은에서 처리합니다. `head.jsp` (`/apps/geometrixx/components/asseteditor/head.jsp`) 다음을 수행합니다.

* 에셋이 로드되었는지 또는 일반 양식을 표시해야 하는지를 감지합니다.
* 에셋이 로드되면 parsys는 일반 양식 페이지에서만 편집할 수 있으므로 WCM 모드를 비활성화합니다.
* 에셋이 로드되면 양식 페이지의 에셋 대신 에셋의 제목을 사용합니다.

```javascript
 List<Resource> resources = FormsHelper.getFormEditResources(slingRequest);
    if (resources != null) {
        if (resources.size() == 1) {
            // single resource
            FormsHelper.setFormLoadResource(slingRequest, resources.get(0));
        } else if (resources.size() > 1) {
            // multiple resources
            // not supported by CQ 5.3
        }
    }
    Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
    String title;
    if (loadResource != null) {
        // an asset is loaded: disable WCM
        WCMMode.DISABLED.toRequest(request);

        String path = loadResource.getPath();
        Asset asset = loadResource.adaptTo(Asset.class);
        try {
            // it might happen that the adobe xmp lib creates an array
            Object titleObj = asset.getMetadata("dc:title");
            if (titleObj instanceof Object[]) {
                Object[] titleArray = (Object[]) titleObj;
                title = (titleArray.length > 0) ? titleArray[0].toString() : "";
            } else {
                title = titleObj.toString();
            }
        }
        catch (NullPointerException e) {
            title = path.substring(path.lastIndexOf("/") + 1);
        }
    }
    else {
        title = currentPage.getTitle() == null ? currentPage.getName() : currentPage.getTitle();
    }
```

HTML 부분에서 앞의 제목 세트(에셋 또는 페이지 제목)를 사용합니다.

```html
<title><%= title %></title>
```

## 간단한 양식 필드 구성 요소 만들기 {#creating-a-simple-form-field-component}

이 예에서는 로드된 에셋의 메타데이터를 표시하고 표시하는 구성 요소를 빌드하는 방법을 설명합니다.

1. 프로젝트 디렉터리에 구성 요소 폴더 만들기(예: ) `/apps/geometrixx/components/samplemeta`.
1. 추가 `content.xml` (다음 코드 조각 포함)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Dimension"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Asset Editor"/>
   ```

1. 추가 `samplemeta.jsp` (다음 코드 조각 포함)

   ```javascript
   <%--
   
     Sample metadata field component
   
   --%><%@ page import="com.day.cq.dam.api.Asset,
                    java.security.AccessControlException" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       String value = "";
       String name = "dam:sampleMetadata";
       boolean readOnly = false;
   
       // If the form page is requested for an asset loadResource will be the asset.
       Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
   
       if (loadResource != null) {
   
           // Determine if the loaded asset is read only.
           Session session = slingRequest.getResourceResolver().adaptTo(Session.class);
           try {
               session.checkPermission(loadResource.getPath(), "set_property");
               readOnly = false;
           }
           catch (AccessControlException ace) {
               // checkPermission throws exception if asset is read only
               readOnly = true;
           }
           catch (RepositoryException re) {}
   
           // Get the value of the metadata.
           Asset asset = loadResource.adaptTo(Asset.class);
           try {
               value = asset.getMetadata(name).toString();
           }
           catch (NullPointerException npe) {
               // no metadata dc:description available
           }
       }
   %>
   <div class="form_row">
       <div class="form_leftcol">
           <div class="form_leftcollabel">Sample Metadata</div>
       </div>
       <div class="form_rightcol">
           <%
           if (readOnly) {
               %><c:out value="<%= value %>"/><%
           }
           else {
               %><input class="text" type="text" name="./jcr:content/metadata/<%= name %>" value="<c:out value="<%= value %>" />"><%
           }%>
       </div>
   </div>
   ```

1. To make the component available, you need to be able to edit it. 구성 요소를 편집할 수 있도록 하려면 CRXDE Lite에서 노드를 추가합니다 `cq:editConfig` 일차제품의 것 `cq:EditConfig`. So that you can remove paragraphs, add a multi-value property `cq:actions` with a single value of `DELETE`.

1. 브라우저로 이동한 다음 샘플 페이지에서 찾습니다(예: `asseteditor.html`) 디자인 모드로 전환하고 단락 시스템의 새 구성 요소를 활성화합니다.

1. In **Edit** mode, the new component (for example, **Sample Metadata**) is now available in the sidekick (found in the **Asset Editor** group). Insert the component. To be able to store the metadata, it must be added to the metadata form.

## 메타데이터 옵션 수정 {#modifying-metadata-options}

에서 사용할 수 있는 네임스페이스를 수정할 수 있습니다. [메타데이터 양식](assets-finder-editor.md#metadata-form-and-text-field-configuring-the-view-metadata-component).

현재 사용 가능한 메타데이터는에 정의되어 있습니다. `/libs/dam/options/metadata`:

* 이 디렉터리 내부의 첫 번째 수준에는 네임스페이스가 포함됩니다.
* 각 네임스페이스 내의 항목은 결과와 같은 메타데이터를 나타냅니다.
* 메타데이터 콘텐츠에는 유형 및 다중 값 옵션에 대한 정보가 포함됩니다.

옵션은에서 덮어쓸 수 있습니다. `/apps/dam/options/metadata`:

1. 에서 디렉터리 복사 `/libs` 끝 `/apps`.

1. 항목을 제거, 수정 또는 추가합니다.

>[!NOTE]
>
>새 네임스페이스를 추가하는 경우 저장소/CRX에 등록해야 합니다. 그렇지 않으면 메타데이터 양식을 제출하면 오류가 발생합니다.
