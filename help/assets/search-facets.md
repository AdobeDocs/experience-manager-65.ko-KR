---
title: 검색 결과를 필터링할 검색 패싯
description: 에서 검색 패싯을 만들고, 수정하고, 사용하는 방법 [!DNL Adobe Experience Manager].
contentOwner: AG
role: Admin, Developer
feature: Search
exl-id: acaf46e6-ff70-4825-8922-ce8f82905a92
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '2429'
ht-degree: 17%

---

# 검색 패싯 {#search-facets}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/search-facets.html?lang=en) |
| AEM 6.5 | 이 문서 |
| AEM 6.4 | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/search-facets.html?lang=en) |

의 엔터프라이즈급 배포 [!DNL Adobe Experience Manager Assets] 는 많은 에셋을 저장할 수 있습니다. 의 일반 검색 기능만 사용하는 경우 적합한 자산을 찾는 데 많은 시간이 소요될 수 있습니다. [!DNL Experience Manager].

필터 패널의 검색 패싯을 사용하여 검색 경험에 세부 기간을 추가하고 검색 기능을 보다 효율적이고 다양하게 만들 수 있습니다. 검색 패싯에는 보다 복잡한 검색을 수행할 수 있도록 하는 여러 차원(술어)이 추가됩니다. 필터 패널에는 몇 가지 표준 패싯이 포함되어 있습니다. 사용자 정의 검색 패싯을 추가할 수도 있습니다.

요약하면, 검색 패싯을 사용하면 미리 결정된 단일 분류 순서가 아니라 여러 방법으로 자산을 검색할 수 있습니다. 원하는 세부 수준으로 쉽게 드릴다운하여 보다 집중적인 검색을 수행할 수 있습니다.

예를 들어 이미지를 찾는 경우 비트맵 이미지를 원하는지 벡터 이미지를 원하는지 선택할 수 있습니다. 이미지에 대한 MIME 유형을 지정하여 검색 범위를 추가로 줄일 수 있습니다. 마찬가지로 문서를 검색할 때 형식을 지정할 수 있습니다(예: PDF 또는 MS Word).

## 술어 추가 {#adding-a-predicate}

필터 패널에 나타나는 검색 패싯은 술어를 사용하여 기본 검색 양식에서 정의됩니다. 더 많은 패싯이나 다른 패싯을 표시하려면 기본 양식에 술어를 추가하거나 선택한 패싯을 포함하는 사용자 정의 양식을 사용합니다.

전체 텍스트 검색의 경우 **[!UICONTROL 전체 텍스트]** 양식에 대한 조건자입니다. 속성 조건자를 사용하여 지정한 단일 속성과 일치하는 에셋을 검색합니다. 옵션 술어를 사용하여 특정 속성에 대해 하나 이상의 값과 일치하는 에셋을 검색합니다. 지정된 날짜 범위 내에서 생성된 에셋을 검색하려면 날짜 범위 술어를 추가하십시오.

1. 다음을 클릭합니다. [!DNL Experience Manager] 로고, 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL Forms 검색]**.
1. 다음에서 [!UICONTROL Forms 검색] 페이지, 선택 **[!UICONTROL 에셋 관리자 검색 레일]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 편집]** ![편집 아이콘](assets/do-not-localize/aemassets_edit.png).

   >[!NOTE]
   >
   >사전 구성된 폴더에서 폴더 검색 기능을 사용하려면 [!DNL Assets] 이전 버전의 관리자 검색 레일에서 다음 단계를 수행합니다.
   >
   >1. 다음으로 이동 `/conf/global/settings/dam/search/facets/assets/jcr:content/items` CRXDE.
   >1. 삭제 `type` 노드.
   >1. 경로에서 `/libs/settings/dam/search/facets/assets/jcr:content/items`, 노드 복사 `asset`, `directory`, `typeor`, `excludepaths`, 및 `searchtype` 1단계에서 언급된 경로로 이동합니다.
   >1. 변경 사항을 저장합니다.


1. 다음에서 [!UICONTROL 검색 Forms 편집] 페이지에서 술어를 끌어서 놓습니다. **[!UICONTROL 조건자 선택]** 탭으로 이동하여 기본 창을 표시합니다. 예: 드래그 **[!UICONTROL 속성 조건자]**.

   ![검색 필터를 사용자 지정할 술어를 선택하고 이동합니다.](assets/drag_predicate.png)

   *그림: 검색 필터를 사용자 지정할 술어를 선택하고 이동합니다.*

1. 다음에서 [!UICONTROL 설정] 탭에서 조건자에 대한 필드 레이블, 자리 표시자 텍스트 및 설명을 입력합니다. 술어와 연결할 메타데이터 속성에 유효한 이름을 지정하십시오. 의 헤더 레이블 [!UICONTROL 설정] 탭은 선택한 술어의 유형을 식별합니다.

1. In the [!UICONTROL Property Name] field, specify a valid name for the metadata property you want to associate with the predicate. It is the name based on which the search is performed. For example, enter `jcr:content/metadata/dc:description` or `./jcr:content/metadata/dc:description`.

   선택 대화 상자에서 기존 노드를 선택할 수도 있습니다.

   ![속성 이름 필드의 술어와 메타데이터 속성 연결](assets/property_settings.png)

   속성 이름 필드의 술어와 메타데이터 속성 연결

1. 다음을 클릭합니다. **[!UICONTROL 미리 보기]** ![미리보기](assets/do-not-localize/preview_icon.png) 술어를 추가한 후 나타나는 필터 패널의 미리 보기를 생성하려면 다음을 수행합니다.
1. 미리보기 모드에서 술어 레이아웃을 검토합니다.

   ![변경 사항을 제출하기 전에 검색 양식 미리 보기](assets/preview-1.png)

   변경 사항을 제출하기 전에 검색 양식 미리 보기

1. 미리보기를 닫으려면 **[!UICONTROL 닫기]** ![닫기](assets/do-not-localize/close.png) 미리 보기의 오른쪽 상단 모서리에서
1. 클릭 **[!UICONTROL 완료]** 설정을 저장합니다.
1. 에서 검색 패널로 이동합니다. [!DNL Assets] 사용자 인터페이스. 속성 조건자가 패널에 추가됩니다.
1. 텍스트 상자에 검색할 에셋에 대한 설명을 입력합니다. 예를 들어 다음을 입력합니다. `Adobe`. 검색을 수행할 때 설명이 일치하는 에셋 `Adobe` 검색 결과에 나열됩니다.

## 옵션 설명 추가 {#adding-an-options-predicate}

옵션 설명 을 사용하면 필터 패널에서 여러 검색 옵션을 추가할 수 있습니다. 필터 패널에서 이러한 옵션 중 하나 이상을 선택하여 에셋을 검색할 수 있습니다. 예를 들어 파일 유형에 따라 에셋을 검색하려면 검색 양식에서 이미지, 멀티미디어, 문서 및 아카이브와 같은 옵션을 구성합니다. 이러한 옵션을 구성한 후 [필터] 패널에서 [이미지] 옵션을 선택하면 GIF, JPEG, PNG 등의 유형 에셋에 대해 검색이 수행됩니다.

옵션을 각 속성에 매핑하려면 옵션에 대한 노드 구조를 만들고 옵션 술어의 속성 이름 속성에 상위 노드의 경로를 제공합니다. 상위 노드는 유형이어야 합니다. `sling`: `OrderedFolder`. 옵션은 유형이어야 합니다. `nt:unstructured`. 옵션 노드에는 속성이 있어야 합니다. `jcr:title` 및 `value` 구성되었습니다.

다음 `jcr:title` 속성은 [필터] 패널에 표시되는 옵션의 사용자에게 친숙한 이름입니다. 다음 `value` 필드는 지정된 속성과 일치하도록 쿼리에 사용됩니다.

옵션을 선택하면 다음에 준하여 검색이 수행됩니다. `value` 옵션 노드 및 해당 하위 노드의 속성(있는 경우). 옵션 노드 아래의 전체 트리가 트래버스되고 `value` 각 자식 노드의 속성은 OR 연산을 사용하여 결합되어 검색 쿼리를 만듭니다.

For example, if you select &quot;Images&quot; for file types, the search query for the assets is built by combining the `value` property using an OR operation. For example, the search query for images is built by combining the results matched for *image/jpeg*, *image/gif*, *image/png*, *image/pjpeg*, and *image/tiff* for the property `jcr:content/metadata/dc:format` using an OR operation.

![CRXDE에 표시된 파일 형식의 값 속성은 검색 쿼리가 작동하는 데 사용됩니다.](assets/filetype-value-property.png)

CRXDE에 표시된 파일 형식의 값 속성은 검색 쿼리가 작동하는 데 사용됩니다.

CRXDE 저장소의 옵션에 대한 노드 구조를 수동으로 만드는 대신 해당 키-값 쌍을 지정하여 JSON 파일에 옵션을 정의할 수 있습니다. Specify the path of the JSON file in the **[!UICONTROL Property Name]** field. For example, you can define the key-value pairs, `image/bmp`, `image/gif`, `image/jpeg`, and `image/png` and specify their values as shown in the following sample JSON file. 다음에서 **[!UICONTROL 속성 이름]** 필드에서는 이 파일의 CRXDE 경로를 지정할 수 있습니다.

```json
{
    "options" :
 [
          {"value" : "image/bmp","text" : "BMP"},
          {"value" : "image/gif","text" : "GIF"},
          {"value" : "image/jpeg","text" : "JPEG"},
          {"value" : "image/png","text" : "PNG"}
 ]
}
```

기존 노드를 사용하려면 선택 대화 상자를 사용하여 지정합니다.

>[!NOTE]
>
>옵션 조건자는 설명된 동작을 보여 주기 위해 속성 조건자를 포함하는 사용자 지정 래퍼입니다. 현재 기능을 기본적으로 지원하는 데 사용할 수 있는 REST 끝점이 없습니다.

1. 다음을 클릭합니다. [!DNL Experience Manager] 로고, 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL Forms 검색]**.
1. 다음에서 **[!UICONTROL Forms 검색]** 페이지, 선택 **[!UICONTROL 에셋 관리자 검색 레일]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 편집]**.
1. In the **[!UICONTROL Edit Search Form]** page, drag **[!UICONTROL Options Predicate]** from the **[!UICONTROL Select Predicate]** tab to the main pane.
1. In the **[!UICONTROL Settings]** tab, enter a label and a name for the property. For example, to search assets based on their format, specify a user-friendly name for the label, for example **[!UICONTROL File Type]**. Specify the property based on which the search is to be performed in the property field, for example `jcr:content/metadata/dc:format.`
1. 다음 중 하나를 수행하십시오.

   * 다음에서 **[!UICONTROL 속성 이름]** 필드에서는 옵션에 대한 노드를 정의하고 해당 키-값 쌍을 지정하는 JSON 파일의 경로를 언급합니다.
   * 다음을 클릭합니다. `+` [옵션] 필드 옆의 기호로 이동하여 [필터] 패널에서 제공할 옵션의 표시 텍스트와 값을 지정합니다. 다른 옵션을 추가하려면 `+` 기호를 지정한 다음 단계를 반복합니다.

1. Ensure that **[!UICONTROL Single Select]** is cleared to let the user select multiple options for file types at a time (for example, Images, Documents, Multimedia, and Archives). If you select **[!UICONTROL Single Select]**, the user can select only one option for file types at a time.

   ![옵션 조건자의 사용 가능한 필드](assets/options_predicate.png)

   옵션 조건자의 사용 가능한 필드

1. 다음에서 **[!UICONTROL 설명]** 필드에 선택적 설명을 입력한 다음 **[!UICONTROL 완료]**.
1. 검색 패널로 이동합니다. 옵션 조건자가 **검색** 패널. 옵션 **[!UICONTROL 파일 유형]** 확인란으로 표시됩니다.

## 다중 값 속성 설명 추가 {#adding-a-multi-value-property-predicate}

다중 값 속성 조건자를 사용하면 에셋에서 여러 값을 검색할 수 있습니다. 에 여러 제품 이미지가 있는 시나리오를 고려하십시오. [!DNL Assets] 각 이미지에 대한 메타데이터에는 제품과 연관된 SKU 번호가 포함됩니다. 이 술어를 사용하여 여러 SKU 번호를 기반으로 제품 이미지를 검색할 수 있습니다.

1. 다음을 클릭합니다. [!DNL Experience Manager] 로고, 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL Forms 검색]**.
1. Forms 검색 페이지에서 다음을 선택합니다. **[!UICONTROL 에셋 관리자 검색 레일]**, 클릭 **[!UICONTROL 편집]** ![편집 아이콘](assets/do-not-localize/aemassets_edit.png).
1. In the Edit Search Form page, drag a **[!UICONTROL Multi Value Property Predicate]** from the **[!UICONTROL Select Predicate]** tab to the main pane.
1. 다음에서 **[!UICONTROL 설정]** 탭에서 술어에 대한 레이블 및 자리 표시자 텍스트를 입력합니다. 속성 필드에서 검색을 수행할 기준 속성 이름을 지정합니다(예: ). `jcr:content/metadata/dc:value`. 선택 대화 상자 를 사용하여 노드를 선택할 수도 있습니다.
1. Ensure that **[!UICONTROL Delimiter Support]** is selected. In the **[!UICONTROL Input Delimiters]** field, specify delimiters to separate individual values. By default, comma is specified as the delimiter. You can specify a different delimiter.
1. 다음에서 **설명** 필드에 선택적 설명을 입력한 다음 **[!UICONTROL 완료]**.
1. 에서 필터 패널로 이동합니다. [!DNL Assets] 사용자 인터페이스. The **[!UICONTROL Multi Value Property]** predicate is added to the panel.
1. 다중 값 필드에 구분 기호로 구분된 여러 값을 지정하고 검색을 수행합니다. 술어는 사용자가 지정하는 값에 대해 정확히 일치하는 텍스트를 가져옵니다.

## 태그 조건자 추가 {#adding-a-tags-predicate}

태그 술어를 사용하면 에셋에 대한 태그 기반 검색을 수행할 수 있습니다. 기본적으로, [!DNL Assets] 지정한 태그를 기반으로 하나 이상의 태그 일치 항목을 에셋에서 검색합니다. 즉, 검색 쿼리는 지정된 태그를 사용하여 OR 작업을 수행합니다. 그러나 모든 태그 일치 옵션을 사용하여 지정한 모든 태그가 포함된 에셋을 검색할 수 있습니다.

1. 다음을 클릭합니다. [!DNL Experience Manager] 로고, 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL Forms 검색]**.
1. Forms 검색 페이지에서 을 선택합니다. **[!UICONTROL 에셋 관리자 검색 레일]** 그런 다음 을 클릭합니다. **[!UICONTROL 편집]** ![편집 아이콘](assets/do-not-localize/aemassets_edit.png).
1. 검색 양식 편집 페이지에서 을 드래그합니다. **[!UICONTROL 태그 조건자]** 설명 선택 탭에서 기본 창으로 이동합니다.
1. 설정 탭에서 술어에 대한 자리 표시자 텍스트를 입력합니다. 속성 필드에서 검색을 수행할 기준 속성 이름을 지정합니다(예: ). *jcr:content/metadata/cq:tags*. 또는 선택 대화 상자에서 CRXDE의 노드를 선택할 수 있습니다.
1. 태그 목록의 다양한 태그를 채우도록 이 술어의 루트 태그 경로 속성을 구성합니다.
1. Select **[!UICONTROL Show match all tags option]** to search for assets that include all tags that you specify.

1. 다음에서 **[!UICONTROL 설명]** 필드에 선택적 설명을 입력한 다음 **[!UICONTROL 완료]**.
1. 검색 패널로 이동합니다. 다음 **[!UICONTROL 태그]** 조건자가 검색 패널에 추가됩니다.
1. 에셋을 검색할 태그를 지정하거나 제안 목록에서 선택합니다.

1. 선택 **[!UICONTROL 모두 일치]** 를 클릭하여 지정한 모든 태그가 포함된 일치 항목을 검색합니다.

## 다른 술어 추가 {#adding-other-predicates}

속성 술어 또는 옵션 술어를 추가하는 방법과 유사하게 검색 패널에 다음과 같은 술어를 추가할 수 있습니다.

| 술어 이름 | 설명 | 속성 |
|---|---|---|
| [!UICONTROL 전체 텍스트] | 전체 에셋 노드에서 전체 텍스트 검색을 수행하는 검색 조건자입니다. jcr:contains 연산자로 매핑됩니다. 에셋 노드의 특정 부분에서 전체 텍스트 검색을 수행하려는 경우 상대 경로를 지정할 수 있습니다. | <ul><li>레이블</li><li>자리 표시자</li><li>속성 이름</li><li>설명</li></ul> |
| [!UICONTROL 경로 브라우저] | 사전 구성된 루트 경로에서 폴더 및 하위 폴더의 에셋을 검색하는 검색 조건자 | <ul><li>자리 표시자</li><li>루트 경로</li><li>설명</li></ul> |
| [!UICONTROL 경로] | 위치에서 결과를 필터링하는 데 사용합니다. 다른 경로를 옵션으로 지정할 수 있습니다. | <ul><li>레이블</li><li>경로</li><li>설명</li></ul> |
| [!UICONTROL 게시 상태] | 게시 상태를 기반으로 에셋을 검색하는 검색 조건자 | <ul><li>레이블</li><li>속성 이름</li><li>설명</li></ul> |
| [!UICONTROL 상대적 날짜] | 만든 상대적 날짜를 기준으로 자산을 검색하는 검색 조건자입니다. 예를 들어 2개월 전, 3주 전 등과 같은 옵션을 구성할 수 있습니다. | <ul><li>레이블</li><li>속성 이름</li><li>상대적 날짜</li></ul> |
| [!UICONTROL 범위] | 지정된 범위 내에 있는 에셋을 검색하는 검색 조건자입니다. [검색] 패널에서 범위의 최소값과 최대값을 지정할 수 있습니다. | <ul><li>레이블</li><li>속성 이름</li><li>설명</li></ul> |
| [!UICONTROL 날짜 범위] | 날짜 속성에 대해 지정된 범위 내에 생성된 에셋을 검색하는 검색 조건자입니다. 검색 패널에서 날짜 선택기를 사용하여 시작 및 종료 날짜를 지정할 수 있습니다. | <ul><li>레이블</li><li>자리 표시자</li><li>속성 이름</li><li>범위 텍스트(시작)</li><li>범위 텍스트(종료)</li><li>설명</li></ul> |
| [!UICONTROL 날짜] | 날짜 속성을 기반으로 하는 에셋의 슬라이더 기반 검색에 대한 검색 조건자입니다. | <ul><li>레이블</li><li>속성 이름</li><li>설명</li></ul> |
| [!UICONTROL 파일 크기] | 크기 기준으로 에셋을 검색하는 검색 조건자입니다. 구성 가능한 노드에서 슬라이더 옵션을 선택하는 Silder 기반 술어입니다. 기본 옵션은 CRXDE 저장소의 /libs/dam/options/predicates/filesize에 정의되어 있습니다. 파일 크기는 바이트 단위로 제공됩니다. | <ul><li>레이블</li><li>속성 이름</li><li>경로</li><li>설명</li></ul> |
| [!UICONTROL 마지막으로 수정된 자산] | 최근에 수정된 자산을 검색하는 검색 조건자 | <ul><li>속성 이름</li><li>속성 값</li><li>설명</li></ul> |
| [!UICONTROL 게시 상태] | 게시 상태를 기반으로 에셋을 검색하는 검색 조건자 | <ul><li>레이블</li><li>속성 이름</li><li>설명</li></ul> |
| [!UICONTROL 등급] | 평균 등급을 기반으로 에셋을 검색하는 검색 조건자 | <ul><li>레이블</li><li>속성 이름</li><li>옵션 경로</li><li>설명</li></ul> |
| [!UICONTROL 만료 상태] | 만료 상태를 기반으로 에셋을 검색하는 검색 조건자 | <ul><li>레이블</li><li>속성 이름</li><li>설명</li></ul> |
| [!UICONTROL 숨김] | 에셋을 검색할 숨겨진 필드 속성을 정의하는 검색 조건자 | <ul><li>속성 이름</li><li>속성 값</li><li>설명</li></ul> |

## 기본 검색 패싯 복원 {#restoring-default-search-facets}

기본적으로 잠금 아이콘 ![닫힘 아이콘 잠금](assets/do-not-localize/lock_closed_icon.svg) 다음 앞에 표시 **[!UICONTROL 에셋 관리자 검색 레일]** 다음에서 **[!UICONTROL Forms 검색]** 페이지를 가리키도록 업데이트하는 중입니다. Forms 검색 페이지의 옵션에 대해 아이콘을 잠그면 기본 설정이 그대로 있고 사용자 지정되지 않았음을 알 수 있습니다. 아이콘 ![닫힘 아이콘 잠금](assets/do-not-localize/lock_closed_icon.svg) 기본 양식이 수정되었음을 나타내는 검색 패싯을 양식에 추가하면 가 사라집니다.

![잠금 아이콘](assets/locked_admin_rail.png)

기본 검색 패싯을 복원하려면 다음 단계를 수행합니다.

1. 선택 **[!UICONTROL 에셋 관리자 검색 레일]** 다음에서 **[!UICONTROL Forms 검색]** 페이지를 가리키도록 업데이트하는 중입니다.
1. 클릭 **[!UICONTROL 삭제]** ![deleteoutline](assets/do-not-localize/deleteoutline.png) 을 클릭합니다.
1. 확인 대화 상자에서 **[!UICONTROL 삭제]** 사용자 지정 변경 내용을 제거합니다.

   검색 패싯에 대한 사용자 지정 변경 사항을 삭제한 후 잠금 아이콘 ![닫힘 아이콘 잠금](assets/do-not-localize/lock_closed_icon.svg) 다음 앞에 다시 표시 **[!UICONTROL 에셋 관리자 검색 레일]** 다음에서 **[!UICONTROL Forms 검색]** 페이지를 가리키도록 업데이트하는 중입니다.

## 사용자 권한 {#user-permissions}

관리자 역할이 할당되지 않은 경우 검색 패싯과 관련된 편집, 삭제 및 미리 보기 작업을 수행하는 데 필요한 권한 목록이 여기에 있습니다.

| 작업 | 권한 |
| ------------------- | ---------------------------------------------------------------- |
| [!UICONTROL 편집] | 읽기 및 쓰기 권한 `/apps` crxde의 노드 |
| [!UICONTROL 삭제] | 읽기, 쓰기 및 삭제 권한 `/apps` crxde의 노드 |
| [!UICONTROL 미리보기] | 읽기, 쓰기 및 삭제 권한 `/var/dam/content` crxde의 노드 또한 읽기 및 쓰기 권한도 `/apps` 노드. |

>[!MORELIKETHIS]
>
>* [자산 검색 기능 확장](searchx.md)
>* [자산 검색](search-assets.md)

