---
title: 메타데이터 스키마는 메타데이터 속성 페이지의 레이아웃을 정의합니다.
description: 메타데이터 스키마는 에셋에 대해 표시되는 메타데이터 속성 페이지 및 속성 페이지의 레이아웃을 정의합니다. 사용자 지정 메타데이터 스키마를 만들고, 메타데이터 스키마를 편집하고, 메타데이터 스키마를 에셋에 적용하는 방법을 알아봅니다.
contentOwner: AG
mini-toc-levels: 1
role: User,Admin
feature: Metadata
exl-id: 0dd322cd-ce97-4335-825d-71f72a5e438c
hide: true
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '3616'
ht-degree: 10%

---

# 메타데이터 스키마 {#metadata-schemas}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-schemas.html?lang=en) |
| AEM 6.5 | 이 문서 |

조직은 자산 검색, 사용, 상호 운용성 등을 향상시키는 메타데이터 모델을 고안합니다. 올바른 메타데이터 애플리케이션은 메타데이터 기반 워크플로우 및 프로세스를 유지 관리하는 데 불가항력적입니다. 조직 전체의 메타데이터 전략 및 표준을 준수하기 위해 DAM 사용자가 조정할 수 있도록 도와주는 메타데이터 스키마를 사용할 수 있습니다. [!DNL Adobe Experience Manager] 쉽고 유연한 방법으로 메타데이터 스키마를 만들고, 유지하고, 적용할 수 있습니다.

위치 [!DNL Adobe Experience Manager Assets]스키마에는 채울 특정 정보에 대한 특정 필드가 포함되어 있습니다. 또한 사용자에게 친숙한 방식으로 메타데이터 필드를 표시하기 위한 레이아웃 정보가 포함되어 있습니다. 메타데이터 속성에는 제목, 설명, MIME 유형, 태그 등이 포함됩니다. 다음을 사용할 수 있습니다. [!UICONTROL 메타데이터 스키마 Forms] 기존 스키마를 수정하거나 사용자 지정 메타데이터 스키마를 추가하는 편집기.

에셋의 속성 페이지를 보고 편집하려면 다음 단계를 따르십시오.

1. 다음을 클릭합니다. **[!UICONTROL 속성 보기]** 카드 보기의 자산 타일에 대한 빠른 작업 옵션입니다. 또는 에셋을 선택한 다음 를 클릭합니다 **[!UICONTROL 속성]** ![속성 보기](assets/do-not-localize/info-circle-icon.png) 을 클릭합니다.

1. 사용 가능한 탭에서 편집 가능한 다양한 메타데이터 속성을 편집할 수 있습니다. 그러나 에셋은 수정할 수 없습니다 [!UICONTROL 유형] 다음에서 [!UICONTROL 기본] 속성 페이지의 탭입니다.

   ![자산 유형을 변경할 수 없는 자산 속성의 기본 탭](assets/asset-properties-basic-tab.png)

   *그림: 에셋의 기본 탭 [!UICONTROL 속성].*

   메타데이터 스키마를 만들거나 편집하는 동안 하나의 속성만 필드에 매핑되는지 확인합니다.

   에셋의 MIME 유형을 수정하려면 사용자 지정 메타데이터 스키마 양식을 사용하거나 기존 양식을 수정합니다. 다음을 참조하십시오 [메타데이터 스키마 편집 Forms](#edit-metadata-schema-forms) 추가 정보. MIME 유형의 메타데이터 스키마를 수정하면 에셋 및 모든 하위 유형에 대한 속성 페이지 레이아웃이 수정됩니다. 예: 아래에서 jpeg 스키마 수정 `default/image` mime 유형의 자산에 대한 메타데이터 레이아웃(자산 속성)만 수정합니다 `image/jpeg`. 그러나 기본 스키마를 편집하면 변경 사항이 모든 유형의 에셋에 대한 메타데이터 레이아웃을 수정합니다.

## 메타데이터 스키마 양식 {#default-metadata-schema-forms}

양식 또는 템플릿 목록을 보려면 [!DNL Experience Manager] 인터페이스 탐색 위치 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL 메타데이터 스키마]**.

[!DNL Experience Manager] 는 다음 메타데이터 스키마 양식 템플릿을 제공합니다.

| 템플릿 | | 설명 |
|---|---|---|
| [!UICONTROL 기본값] | | 에셋의 기본 메타데이터 스키마 양식. |
| | 다음 자식 폼은 [!UICONTROL 기본값] 양식: | |
| | <ul><li>[!UICONTROL dm_video]</li></ul> | Dynamic Media 비디오용 스키마 양식. |
| | <ul><li>[!UICONTROL 이미지]</li></ul> | 다음과 같은 MIME 유형의 이미지에 대한 스키마 양식 `image/jpeg` 및 `image/png`. <br> 다음 [!UICONTROL 이미지] 양식에는 다음과 같은 하위 양식 템플릿이 있습니다. <ul><li> [!UICONTROL jpeg]: 하위 유형이 있는 에셋의 스키마 양식 [!UICONTROL jpeg].</li> <li>[!UICONTROL tiff]: 하위 유형 TIFF이 있는 에셋의 스키마 양식.</li></ul> |
| | <ul><li>[!UICONTROL 애플리케이션]</li></ul> | MIME 유형의 자산에 대한 스키마 양식: `application/pdf` 및 `application/zip`. <br>[!UICONTROL pdf]: 하위 유형 PDF이 있는 에셋의 스키마 양식. |
| | <ul><li>[!UICONTROL 비디오]</li></ul> | MIME 유형의 비디오 자산에 대한 스키마 양식: `video/avi` 및 `video/mp4`. |
| [!UICONTROL 컬렉션] | | 컬렉션에 대한 스키마 양식입니다. |
| [!UICONTROL contentfragment] | | [콘텐츠 조각용 스키마 양식](/help/sites-developing/customizing-content-fragments.md). |
| [!UICONTROL 양식] | | 이 스키마 양식과 관련된 항목 [Adobe Experience Manager Forms](/help/forms/home.md). |
| [!UICONTROL ugc_contentfragment] | | 소셜 미디어에서 Experience Manager에 통합된 사용자 생성 콘텐츠 부분 및 에셋에 대한 스키마 양식입니다. |

>[!NOTE]
>
>스키마 양식의 하위 양식을 보려면 스키마 양식 이름을 누릅니다.

## 메타데이터 스키마 양식 추가 {#add-a-metadata-schema-form}

메타데이터 스키마 양식을 추가하려면 다음 단계를 수행합니다.

1. 사용자 지정 템플릿을 목록에 추가하려면 **[!UICONTROL 만들기]** 을 클릭합니다.

   >[!NOTE]
   >
   >편집되지 않은 템플릿과 함께 잠금 기호가 표시됩니다. 템플릿을 사용자 지정하는 경우 잠기지 않습니다 ![잠금 닫힘](assets/do-not-localize/lock_closed_icon.svg).

1. 대화 상자에서 스키마 양식의 제목을 입력하고 를 클릭합니다 **[!UICONTROL 만들기]** 을 클릭하여 양식 만들기 프로세스를 완료합니다.

## 메타데이터 스키마 양식 편집 {#edit-metadata-schema-forms}

새로 추가된 메타데이터 스키마 양식 또는 기존 메타데이터 스키마 양식을 편집할 수 있습니다. 메타데이터 스키마 양식에는 탭과 탭 내의 양식 항목이 포함됩니다. 이러한 양식 항목을 CRX 저장소의 메타데이터 노드 내에 있는 필드에 매핑/구성할 수 있습니다. 메타데이터 스키마 양식에 탭이나 양식 항목을 추가할 수 있습니다. 상위 항목에서 파생된 탭과 양식 항목이 잠긴 상태입니다. 하위 수준에서는 변경할 수 없습니다.

1. 다음에서 [!UICONTROL 메타데이터 스키마 Forms] 페이지에서 양식을 선택하고 **[!UICONTROL 편집]** 을 클릭합니다.

1. 다음에서 **[!UICONTROL 메타데이터 스키마 양식 편집기]** 페이지에서 메타데이터 양식을 사용자 지정합니다. 필요한 구성 요소를 **[!UICONTROL 양식 작성]** 탭 을 클릭하여 탭 중 하나를 선택합니다.

1. 구성 요소를 구성하려면 구성 요소를 선택하고 **[!UICONTROL 설정]** 탭.

### 구성 요소 [!UICONTROL 양식 작성] 탭 {#components-within-the-build-form-tab}

다음 **[!UICONTROL 양식 작성]** 탭에는 스키마 양식에서 사용하는 양식 항목이 나열됩니다. 다음 **[!UICONTROL 설정]** 탭에서 선택하는 각 항목의 속성을 제공합니다. **[!UICONTROL 양식 작성]** 탭. 다음 표에서 사용할 수 있는 양식 항목을 나열합니다. **[!UICONTROL 양식 작성]** 탭:

| 구성 요소 이름 | 설명 |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| [!UICONTROL 섹션 머리글] | 공통 구성 요소 목록의 섹션 머리글을 추가합니다. |
| [!UICONTROL 한 줄 텍스트] | 한 줄 텍스트 속성을 추가합니다. 문자열로 저장됩니다. |
| [!UICONTROL 다중 값 텍스트] | 다중 값 텍스트 속성을 추가합니다. 문자열 배열로 저장됩니다. |
| [!UICONTROL 숫자] | 숫자 구성 요소를 추가합니다. |
| [!UICONTROL 날짜] | 날짜 구성 요소를 추가합니다. |
| [!UICONTROL 드롭다운] | 드롭다운 목록을 추가합니다. |
| [!UICONTROL 표준 태그] | 태그 추가. |
| [!UICONTROL 스마트 태그] | 메타데이터 태그를 자동으로 추가하여 검색 기능을 보강합니다. |
| [!UICONTROL 숨김 필드] | 숨겨진 필드를 추가합니다. 에셋이 저장될 때 POST 매개 변수로 전송됩니다. |
| [!UICONTROL 자산 참조자] | 자산이 참조하는 자산 목록을 보려면 이 구성 요소를 추가하십시오. |
| [!UICONTROL 자산 참조] | 를 추가하여 에셋을 참조하는 에셋 목록을 표시합니다. |
| [!UICONTROL 제품 참조] | 를 추가하여 자산과 연결된 제품 목록을 표시합니다. |
| [!UICONTROL 자산 등급] | 를 추가하여 자산 등급 지정 옵션을 표시합니다. |
| [!UICONTROL 상황에 맞는 메타데이터] | 를 추가하여 자산의 속성 페이지에서 다른 메타데이터 탭의 표시를 제어합니다. |

#### 메타데이터 구성 요소 편집 {#edit-the-metadata-component}

양식에 대한 메타데이터 구성 요소의 속성을 편집하려면 구성 요소를 클릭하여 **[!UICONTROL 설정]** 탭. 메타데이터 스키마의 특정 속성에 필드를 매핑하는 것이 좋습니다. 그렇지 않으면 속성에 매핑된 최신 추가 필드가 시스템에 의해 선택됩니다.

**필드 레이블**: 에셋의 속성 페이지에 표시되는 메타데이터 속성의 이름입니다.

**속성에 매핑**: 이 속성은 CRX 저장소에 저장된 에셋 노드의 상대 경로 또는 이름을 지정합니다. 다음으로 시작: `./` 경로가 자산의 노드 아래에 있음을 나타냅니다.

다음은 속성에 유효한 값의 예입니다.

* `./jcr:content/metadata/dc:title`: Stores the value at the asset&#39;s metadata node as the property `dc:title`.

* `./jcr:created`: 에셋의 생성 날짜 및 시간을 저장합니다. 보호 속성입니다. 이러한 속성을 구성하는 경우, Adobe은 해당 속성을 편집 비활성화로 표시할 것을 권장합니다. Otherwise, the error &quot;Asset(s) failed to modify&quot; occurs when you save the asset&#39;s properties.

구성 요소가 메타데이터 스키마 양식에 제대로 표시되도록 하려면 속성 경로에 공백을 포함해서는 안 됩니다.

* **자리 표시자**: 이 속성을 사용하여 메타데이터 속성과 관련된 관련 자리 표시자 텍스트를 지정합니다.
* **필수**: 이 속성을 사용하여 메타데이터 속성을 속성 페이지에서 필수로 표시합니다.
* **편집 비활성화**: 속성 페이지에서 속성을 편집할 수 없도록 하려면 이 속성을 사용하십시오.
* **읽기 전용에 빈 필드 표시**: 값이 없는 경우에도 속성 페이지에 메타데이터 속성을 표시하려면 이 속성을 선택합니다. 기본적으로 메타데이터 속성에 값이 없으면 속성 페이지에 나열되지 않습니다.
* **정렬된 목록 표시**: 이 속성을 사용하여 순서가 지정된 선택 목록을 표시합니다.
* **선택 사항**: 이 속성을 사용하여 목록에서 선택 항목을 지정합니다.
* **설명** : 이 속성을 사용하여 메타데이터 구성 요소에 대한 간단한 설명을 추가합니다.
* **클래스**: 속성이 연결된 오브젝트 클래스.
* **삭제**: 클릭 [!UICONTROL 삭제] 스키마 양식에서 구성 요소를 삭제합니다.

>[!NOTE]
>
>다음 [!UICONTROL 숨겨진 필드] 구성 요소에는 이러한 속성이 포함되지 않습니다. 대신 속성 이름, 값, 필드 레이블 및 설명과 같은 속성이 포함됩니다. 숨김 필드 구성 요소에 대한 값은 에셋이 저장될 때마다 POST 매개 변수로 전송됩니다. 에셋의 메타데이터로 저장되지 않습니다.

If you select the **[!UICONTROL Required]** option, you can search for assets missing mandatory metadata. From the **[!UICONTROL Filters]** panel, expand the **[!UICONTROL Metadata Validation]** predicate and select the **[!UICONTROL Invalid]** option. The search results display assets missing mandatory metadata that you configured through the schema form.

![필터 패널의 메타데이터 유효성 검사 조건부에서 선택한 옵션](assets/invalid-metadata-predicate.png)

컨텍스트 메타데이터 구성 요소를 스키마 양식의 탭에 추가하면 구성 요소가 특정 스키마가 적용되는 에셋의 속성 페이지에 목록으로 표시됩니다. 이 목록에는 컨텍스트 메타데이터 구성 요소를 적용한 탭을 제외한 다른 모든 탭이 포함되어 있습니다. 현재, 이 기능은 컨텍스트를 기반으로 메타데이터 표시를 제어하는 기본 기능을 제공합니다.

![에셋 속성의 탭 나열 컨텍스트 메타데이터 구성 요소](assets/metadata-contextual-component-list.png)

컨텍스트 메타데이터 구성 요소가 적용되는 탭 외에 속성 페이지에 탭을 표시하려면 목록에서 탭을 선택합니다. 탭이 속성 페이지에 추가됩니다.

![상황별 메타데이터 목록에서 선택한 탭이 에셋 속성 페이지에 표시됩니다](assets/contextual-metadata-asset-properties.png)

*그림: 자산 속성 페이지의 컨텍스트 기반 메타데이터*

### JSON 파일의 속성 지정 {#specify-properties-in-json-file}

Instead of specifying properties for the options in the **[!UICONTROL Settings]** tab, you can define the options in a JSON file by specifying corresponding key-value pairs. Specify the path of the JSON file in the **[!UICONTROL JSON Path]** field.

#### 스키마 양식에서 탭 추가 또는 삭제 {#adding-deleting-a-tab-in-the-schema-form}

The schema editor lets you add or delete a tab. The default schema form includes the **[!UICONTROL Basic]**, **[!UICONTROL Advanced]** , **[!UICONTROL IPTC]**, and **[!UICONTROL IPTC Extension]** tabs.

클릭 `+` 를 클릭하여 스키마 양식에 탭을 추가합니다. 기본적으로 새 탭의 이름은 입니다 `Unnamed-1`. 다음에서 이름을 수정할 수 있습니다. **[!UICONTROL 설정]** 탭. 클릭 `X` 탭을 삭제하려면 다음 작업을 수행하십시오.

![메타데이터 스키마 편집기를 사용하여 탭 추가 또는 삭제](assets/metadata-schema-form-new-tab.png)

## 연속 메타데이터 {#cascading-metadata}

에셋의 메타데이터 정보를 캡처할 때, 사용자는 다양한 이용 가능한 필드들의 정보를 제공한다. 특정 메타데이터 필드나 다른 필드에서 선택한 옵션에 따라 달라지는 필드 값을 표시할 수 있습니다. 이러한 메타데이터의 조건부 표시를 계단식 메타데이터라고 합니다. 즉, 특정 메타데이터 필드/값과 하나 이상의 필드 및/또는 해당 값 사이에 종속성을 만들 수 있습니다.

메타데이터 스키마를 사용하여 계단식 메타데이터를 표시하는 규칙을 정의합니다. 예를 들어 메타데이터 스키마에 에셋 유형 필드가 포함된 경우 사용자가 선택하는 에셋 유형에 따라 표시할 관련 필드 세트를 정의할 수 있습니다.

>[!CAUTION]
>
>계단식 메타데이터는 콘텐츠 조각에 대해 지원되지 않습니다.

다음은 계단식 메타데이터를 정의할 수 있는 몇 가지 사용 사례입니다.

* 사용자 위치가 필요한 경우 사용자의 국가 및 주 선택에 따라 관련 도시 이름을 표시합니다.
* 사용자가 선택한 제품 범주에 따라 목록에 관련 브랜드 이름을 로드합니다.
* 다른 필드에 지정된 값을 기준으로 특정 필드의 가시성을 전환합니다. 예를 들어 사용자가 다른 주소로 배송을 배송하려는 경우 별도의 배송 주소 필드를 표시합니다.
* 다른 필드에 지정된 값을 기준으로 필드를 필수 항목으로 지정합니다.
* 다른 필드에 지정된 값을 기준으로 특정 필드에 표시되는 옵션을 변경합니다.
* 다른 필드에 지정된 값을 기반으로 특정 필드의 기본 메타데이터 값을 설정합니다.

### 에서 계단식 메타데이터 구성 [!DNL Experience Manager] {#configure-cascading-metadata-in-aem}

선택한 에셋 유형에 따라 계단식 메타데이터를 표시할 시나리오를 생각해 보십시오. 몇 가지 예

* 비디오의 경우 형식, 코덱, 지속 시간 등과 같은 적용 가능한 필드를 표시합니다.
* Word 또는 PDF 문서의 경우 페이지 수, 작성자 등과 같은 필드를 표시합니다.

선택한 에셋 유형에 관계없이 저작권 정보를 필수 필드로 표시합니다.

1. 위치 [!DNL Experience Manager] 인터페이스, 이동 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL 메타데이터 스키마]**.
1. 다음에서 **[!UICONTROL 스키마 Forms]** 페이지에서 스키마 양식을 선택한 다음 **[!UICONTROL 편집]** 을 클릭하여 스키마를 편집합니다.

   ![select_form](assets/select_form.png)

1. (선택 사항) 메타데이터 스키마 편집기에서 조건화할 필드를 만듭니다. 에서 이름 및 속성 경로 지정 **[!UICONTROL 설정]** 탭.

   탭을 만들려면 `+` 탭을 추가한 다음 메타데이터 필드를 추가합니다.

   ![add_tab](assets/add_tab.png)

1. 에셋 유형에 대한 드롭다운 필드를 추가합니다. 에서 이름 및 속성 경로 지정 **[!UICONTROL 설정]** 탭. 선택적 설명을 추가합니다.

   ![asset_type_field](assets/asset_type_field.png)

1. 키-값 쌍은 양식 사용자에게 제공되는 옵션입니다. 키-값 쌍을 수동으로 또는 JSON 파일에서 제공할 수 있습니다.

   * 값을 수동으로 지정하려면 다음을 선택합니다 **[!UICONTROL 수동으로 추가]**, 및 클릭 **[!UICONTROL 선택 항목 추가]** 옵션 텍스트와 값을 지정합니다. 예를 들어 비디오, PDF, Word 및 Image 에셋 유형을 지정합니다.

   * JSON 파일에서 값을 동적으로 가져오려면 다음을 선택합니다. **[!UICONTROL JSON 경로를 통해 추가]** JSON 파일의 경로를 제공합니다. [!DNL Experience Manager] 양식이 사용자에게 표시될 때 실시간으로 키-값 쌍을 가져옵니다.

   두 옵션은 함께 사용할 수 없습니다. JSON 파일에서 옵션을 가져와 수동으로 편집할 수 없습니다.

   ![add_choice](assets/add_choice.png)

   >[!NOTE]
   >
   >JSON 파일을 추가하면 키-값 쌍이 메타데이터 스키마 편집기에 표시되지 않지만 게시된 양식에서 사용할 수 있습니다.

   >[!NOTE]
   >
   >선택 항목을 추가할 때 드롭다운 필드를 클릭하면 인터페이스가 왜곡되고 선택 항목에 대한 삭제 옵션이 작동하지 않습니다. 변경 사항을 저장할 때까지 드롭다운을 클릭하지 마십시오. 이 문제가 발생하면 스키마를 저장하고 다시 열어 편집을 계속합니다.

1. (선택 사항) 다른 필수 필드를 추가합니다. 예: 에셋 유형 비디오의 형식, 코덱 및 기간.

   마찬가지로 다른 에셋 유형에 종속 필드를 추가합니다. 예를 들어 PDF 및 Word 파일과 같은 문서 에셋에 대한 필드 페이지 수 및 작성자를 추가합니다.

   ![video_dependent_fields](assets/video_dependent_fields.png)

1. 에셋 유형 필드와 다른 필드 사이에 종속성을 만들려면 종속 필드를 선택하고 **[!UICONTROL 규칙]** 탭.

   ![select_dependentfield](assets/select_dependentfield.png)

1. 아래 **[!UICONTROL 요구 사항]**, 을(를) 선택합니다. **[!UICONTROL 필수, 새 규칙 기반]** 옵션을 선택합니다.
1. 클릭 **[!UICONTROL 규칙 추가]** 및 선택 **[!UICONTROL 에셋 유형]** 종속성을 만드는 필드입니다. Also choose the field value upon which to create the dependency. In this case, choose **[!UICONTROL Video]**. **[!UICONTROL 완료]**&#x200B;를 클릭하여 변경 내용을 저장합니다.

   ![define_rule](assets/define_rule.png)

   >[!NOTE]
   >
   >수동으로 사전 정의된 값이 있는 드롭다운을 규칙과 함께 사용할 수 있습니다. 사전 정의된 값을 사용하여 조건을 적용하는 규칙에는 JSON 경로가 구성된 드롭다운 메뉴를 사용할 수 없습니다. 런타임 시 JSON에서 값이 로드되는 경우 사전 정의된 규칙을 적용할 수 없습니다.

1. Under **[!UICONTROL Visibility]**, choose the **[!UICONTROL Visible, based on new rule]** option.

1. 클릭 **[!UICONTROL 규칙 추가]** 및 선택 **[!UICONTROL 에셋 유형]** 종속성을 만드는 필드입니다. Also choose the field value upon which to create the dependency. In this case, choose **[!UICONTROL Video]**. **[!UICONTROL 완료]**&#x200B;를 클릭하여 변경 내용을 저장합니다.

   ![define_visibilityrule](assets/define_visibilityrule.png)

   >[!NOTE]
   >
   >공백(또는 값 이외의 위치)을 클릭하면 값이 재설정됩니다. 그런 경우 값을 다시 선택합니다.

   >[!NOTE]
   >
   >You can apply **[!UICONTROL Requirement]** condition and **[!UICONTROL Visibility]** condition independent of each other.

1. 마찬가지로 에셋 유형 필드의 값 Video와 코덱 및 지속 시간과 같은 다른 필드 간에 종속성을 만듭니다.
1. 에서 문서 에셋(PDF 및 Word) 간에 종속성을 만들려면 단계를 반복합니다. [!UICONTROL 에셋 유형] 필드 및 필드 [!UICONTROL 페이지 수] 및 [!UICONTROL 작성자].
1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다. 폴더에 메타데이터 스키마를 적용합니다.

1. 메타데이터 스키마를 적용한 폴더로 이동하고 자산의 속성 페이지를 엽니다. 에셋 유형 필드에서 선택한 사항에 따라 관련 계단식 메타데이터 필드가 표시됩니다.

   ![비디오 자산에 대한 계단식 메타데이터](assets/video_asset.png)

   *그림: 비디오에 대한 계단식 메타데이터*

   ![문서 에셋에 대한 계단식 메타데이터](assets/doc_type_fields.png)

   *그림: 문서에 대한 계단식 메타데이터*

## 메타데이터 스키마 양식 삭제 {#delete-metadata-schema-forms}

[!DNL Experience Manager] 사용자 정의 스키마 양식만 삭제할 수 있습니다. 기본 스키마 양식/템플릿을 삭제할 수는 없습니다. 그러나 이러한 양식에서 사용자 정의 변경 사항을 삭제할 수 있습니다.

양식을 삭제하려면 양식을 선택하고 삭제를 누릅니다.

>[!NOTE]
>
>* 기본 양식에 대한 사용자 지정 변경 내용을 삭제하면 ![잠금 닫힘](assets/do-not-localize/lock_closed_icon.svg) 양식 앞에 다시 나타납니다. 양식이 기본 상태로 되돌려짐을 나타냅니다.
>* 에서 기본 메타데이터 스키마 양식을 삭제할 수 없습니다. [!DNL Assets].

## MIME 유형에 대한 스키마 양식 {#schema-forms-for-mime-types}

[!DNL Experience Manager] 에서는 다양한 MIME 유형에 대한 기본 양식을 즉시 제공합니다. 하지만 다양한 MIME 유형의 자산에 대한 사용자 정의 양식을 추가할 수 있습니다.

### MIME 유형에 대한 새 양식 추가 {#add-new-forms-for-mime-types}

Create a form under the appropriate form type. For example, to add a template for the `image/png` subtype, create the form under the &quot;image&quot; forms. The title for the schema form is the subtype name. In this case, the title is `png`.

#### 다양한 MIME 유형에 기존 스키마 템플릿 사용 {#use-an-existing-schema-template-for-various-mime-types}

다른 MIME 유형에 기존 템플릿을 사용할 수 있습니다. 예를 들어 `image/jpeg` MIME 유형의 자산용 양식 `image/png`.

이 경우 다음 위치에 노드를 만듭니다. `/etc/dam/metadataeditor/mimetypemappings` CRX 저장소에서 노드 이름을 지정하고 다음 속성을 정의합니다.

| 이름 | 설명 | 유형 | 값 |
|------|-------------|------|-------|
| `exposedmimetype` | 매핑할 기존 양식의 이름 | `String` | `image/jpeg` |
| `mimetypes` | 에 정의된 양식을 사용하는 MIME 유형 목록 `exposedmimetype` 속성 | `String` | `image/png` |

[!DNL Assets] 다음 MIME 유형 및 스키마 양식을 매핑합니다.

| 스키마 양식 | MIME 유형 |
|---|---|
| image/jpeg | image/pjpeg |
| image/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related; type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related; type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related; type=application/x-MixedMediaSet |
| video/quicktime | video/x-quicktime |
| video/mpeg4 | video/mp4 |
| video/avi | video/avi, video/msvideo, video/x-msvideo |
| video/wmv | video/x-ms-wmv |
| video/flv | video/x-flv |

## 메타데이터 스키마에 대한 액세스 권한 부여 {#grant-access-to-metadata-schemas}

메타데이터 스키마 기능은 관리자만 사용할 수 있습니다. 그러나 관리자는 일부 권한을 수정하여 관리자가 아닌 사용자에게 액세스 권한을 제공할 수 있습니다. 관리자가 아닌 사용자에게 `/conf` 폴더를 삭제합니다.

## 폴더별 메타데이터 적용 {#apply-folder-specific-metadata}

[!DNL Assets] 메타데이터 스키마의 변형을 정의하고 특정 폴더에 적용할 수 있습니다.

예를 들어, 기본 메타데이터 스키마의 변형을 정의하여 폴더에 적용할 수 있습니다. 수정된 스키마를 적용하면 폴더 내의 에셋에 적용된 원래 기본 메타데이터 스키마를 재정의합니다.

이 스키마가 적용되는 폴더에 업로드된 자산만 변형 메타데이터 스키마에 정의된 수정된 메타데이터를 따릅니다. [!DNL Assets] 원본 스키마가 적용되는 다른 폴더에서는 원본 스키마에 정의된 메타데이터를 계속 준수합니다.

에셋의 메타데이터 상속은 계층의 최상위 폴더에 적용되는 스키마를 기반으로 합니다. 동일한 스키마가 하위 폴더에 적용되거나 하위 폴더에 상속됩니다. 하위 폴더 수준에서 다른 스키마가 적용되면 상속이 중지됩니다.

1. 위치 [!DNL Experience Manager] 인터페이스, 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL 메타데이터 스키마]**. The **[!UICONTROL Metadata Schema Forms]** page is displayed.
1. 기본 메타데이터 양식과 같은 양식 앞에 있는 확인란을 선택하고 **[!UICONTROL 복사]** 사용자 정의 양식으로 저장합니다. 양식에 대한 사용자 정의 이름 지정(예: ) `my_default`. 또는 사용자 정의 양식을 만들 수 있습니다.

1. 다음에서 **[!UICONTROL 메타데이터 스키마 Forms]** 페이지에서 `my_default` 폼을 클릭한 다음 **[!UICONTROL 편집]**.

1. 다음에서 **[!UICONTROL 메타데이터 스키마 편집기]** 페이지에서 스키마 양식에 텍스트 필드를 추가합니다. 예를 들어 레이블이 있는 필드를 추가합니다 **[!UICONTROL 범주]**.

   ![메타데이터 스키마 양식 편집기에 텍스트 필드가 추가됨](assets/text-field-metadata-schema-editor.png)

   *그림: 메타데이터 스키마 양식 편집기에 추가된 텍스트 필드*

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다. 수정된 양식이에 나열되어 있습니다. **[!UICONTROL 메타데이터 스키마 Forms]** 페이지를 가리키도록 업데이트하는 중입니다.
1. 클릭 **[!UICONTROL 폴더에 적용]** 을 클릭하여 폴더에 사용자 지정 메타데이터를 적용합니다.

1. 수정된 스키마를 적용할 폴더를 선택한 다음 **[!UICONTROL 적용]**.

   ![메타데이터 스키마를 적용할 폴더 선택](assets/metadata-schema-select-folder.png)

1. 폴더에 다른 메타데이터 스키마가 적용된 경우 기존 메타데이터 스키마를 덮어쓰려고 한다는 경고 메시지가 나타납니다. 클릭 **덮어쓰기**.
1. 클릭 **확인** 성공 메시지를 닫으려면 다음을 수행하십시오.
1. 수정된 메타데이터 스키마를 적용한 폴더로 이동합니다.

## 필수 메타데이터 정의 {#define-mandatory-metadata}

폴더에 업로드된 에셋에 적용되는 폴더 수준에서 필수 필드를 정의할 수 있습니다. 앞에서 정의한 필수 필드에 대해 누락된 메타데이터가 있는 에셋을 업로드하면 누락된 메타데이터에 대한 시각적 표시가 카드 보기의 에셋에 나타납니다.

>[!NOTE]
>
>메타데이터 필드는 다른 필드의 값을 기반으로 필수로 정의할 수 있습니다. 카드 보기에서, [!DNL Experience Manager] 는 이러한 필수 메타데이터 필드에 대한 메타데이터 누락에 대한 경고 메시지를 표시하지 않습니다.

1. 위치 [!DNL Experience Manager] 인터페이스, 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL 메타데이터 스키마]**. The **[!UICONTROL Metadata Schema Forms]** page is displayed.
1. 기본 메타데이터 양식을 사용자 정의 양식으로 저장합니다. 예를 들어 다음과 같이 저장합니다. `my_default`.

1. 사용자 정의 양식을 편집합니다. 필수 필드를 추가합니다. 예를 들어 **[!UICONTROL 범주]** 필드를 지정하고 필수 필수로 만듭니다.

   ![메타데이터 스키마 양식 편집기의 규칙 탭에서 필수 를 선택하여 메타데이터 양식에 필수 필드를 추가합니다.](assets/mandatory-field-metadata-schema-editor.png)

   *그림: 메타데이터 스키마 양식 편집기의 필수 필드*

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다. 수정된 양식이에 나열되어 있습니다. **[!UICONTROL 메타데이터 스키마 Forms]** 페이지를 가리키도록 업데이트하는 중입니다. 양식을 선택하고 **[!UICONTROL 폴더에 적용]** 을 클릭하여 폴더에 사용자 지정 메타데이터를 적용합니다.

1. 폴더로 이동하고 사용자 정의 양식에 추가한 필수 필드에 대해 메타데이터가 누락된 일부 에셋을 업로드합니다. 필수 필드에 대한 누락된 메타데이터에 대한 메시지가 에셋의 카드 보기에 표시됩니다.

   ![폴더에 에셋을 업로드할 때 에셋 카드 보기에 필수 메타데이터가 누락되기 위한 메시지](assets/metadata-missing-info-card-view.png)

1. (선택 사항) 액세스 `https://[aem_server]:[port]/system/console/components/`. 구성 및 활성화 `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` 기본적으로 비활성화된 구성 요소입니다. 빈도를 설정합니다. [!DNL Experience Manager] 는 에셋에 대한 메타데이터의 유효성을 확인합니다. 이 구성은 속성을 추가합니다. `hasValidMetadata` 끝 `jcr:content` 에셋. [!DNL Experience Manager] 이 속성을 사용하여 검색 결과에서 잘못된 에셋을 필터링합니다. 확인 후 에셋을 추가하면 에셋에 플래그가 지정되지 않습니다. `hasValidMetadata` 다음 예약된 검사까지. 따라서 자산은 예약된 다음 검사 이후까지 잘못된 메타데이터에 대한 검색 필터에 표시되지 않습니다.

   >[!CAUTION]
   >
   >메타데이터 유효성 검사는 리소스를 많이 사용하며 시스템 성능에 영향을 줄 수 있습니다. 그에 따라 검사를 예약합니다. 서버가 부하를 처리할 수 없는 경우 이 작업을 비활성화하십시오.

<!-- TBD: Add this method to find invalid metadata in the metadata.md article later when it is published as a top-level metadata article.
-->
