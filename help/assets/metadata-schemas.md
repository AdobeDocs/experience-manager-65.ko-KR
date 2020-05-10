---
title: '메타데이터 속성 페이지의 레이아웃을 정의하는 메타데이터 스키마 [!DNL Adobe Experience Manager Assets]. '
description: 메타데이터 스키마는 속성 페이지의 레이아웃과 자산에 대해 표시되는 메타데이터 속성을 정의합니다. 사용자 정의 메타데이터 스키마를 만들고 메타데이터 스키마를 편집하며 자산에 메타데이터 스키마를 적용하는 방법을 알아봅니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 6151c1afe3006e8d4b93648fc9eb779c73df4181
workflow-type: tm+mt
source-wordcount: '2741'
ht-degree: 2%

---


# 메타데이터 스키마 {#metadata-schemas}

조직은 에셋 검색, 사용, 상호 운용성 등을 향상시키는 메타데이터 모델을 제공합니다. 메타데이터 기반의 워크플로우와 프로세스를 유지하기 위해 매우 안전한 메타데이터 애플리케이션을 구축할 수 있습니다. 조직 전체의 메타데이터 전략 및 표준을 준수하려면 DAM 사용자가 정렬하는 데 도움이 되는 메타데이터 스키마를 사용할 수 있습니다. Adobe Experience Manager를 사용하면 간편하고 유연한 방식으로 메타데이터 스키마를 생성, 유지 관리 및 적용할 수 있습니다.

in [!DNL Adobe Experience Manager Assets], 스키마에는 채울 특정 정보에 대한 특정 필드가 포함됩니다. 또한 사용자에게 친숙한 방식으로 메타데이터 필드를 표시하는 레이아웃 정보도 포함되어 있습니다. 메타데이터 속성에는 제목, 설명, MIME 유형, 태그 등이 포함됩니다. 메타데이터 스키마 [!UICONTROL 양식] 편집기를 사용하여 기존 스키마를 수정하거나 사용자 정의 메타데이터 스키마를 추가할 수 있습니다.

자산에 대한 속성 페이지를 보려면 다음 단계를 수행합니다.

1. 카드 보기의 자산 타일에 있는 **[!UICONTROL 빠른 작업]** 에서 속성 보기 아이콘을 클릭하거나 탭합니다.

   ![자산 타일에 대한 빠른 작업](assets/chlimage_1-170.png)

1. 다양한 탭에서 다양한 메타데이터 속성을 편집할 수 있습니다. 하지만 속성 페이지에서 자산 유형을 수정할 수는 [!UICONTROL 없습니다] .

   ![자산 속성의 기본 탭. 여기서 자산 유형은 변경할 수 없습니다.](assets/asset-properties-basic-tab.png)

1. 사용 가능한 탭에서 다양한 메타데이터 속성을 편집할 수 있습니다. 하지만 속성 페이지의 [!UICONTROL 기본] 탭에서 자산 유형 [!UICONTROL 을] 수정할 수는 없습니다.

   ![자산 속성의 기본 탭. 여기서 자산 유형은 변경할 수 없습니다.](assets/asset-properties-basic-tab.png)

*그림: 자산 속성의 기본 탭.*

자산에 대한 MIME 형식을 수정하려면 사용자 지정 메타데이터 스키마 양식을 사용하거나 기존 양식을 수정하십시오. 자세한 [내용은 메타데이터 스키마 양식](/help/assets/metadata-schemas.md#edit-metadata-schema-forms) 편집을 참조하십시오. 특정 MIME 유형의 메타데이터 스키마를 수정하는 경우 현재 MIME 형식과 모든 자산 하위 형식의 자산에 대한 속성 페이지 레이아웃이 수정됩니다. 예를 들어 jpeg 스키마를 `default/image` 수정하면 MIME 형식의 자산에 대한 메타데이터 레이아웃(자산 속성)만 수정됩니다 `image/jpeg`. 그러나 기본 스키마를 편집하는 경우 변경 사항은 모든 유형의 자산에 대한 메타데이터 레이아웃을 수정합니다.

1. 양식/템플릿 목록을 보려면 [!DNL Experience Manager] 인터페이스에서 **[!UICONTROL 도구]** > 자산 **[!UICONTROL > 메타데이터 스키마]** 로 **[!UICONTROL 이동합니다]**.

## 메타데이터 스키마 양식을 기본적으로 사용할 수 있습니다. {#available-metadata-schema-templates}

[!DNL Experience Manager] provides the following templates:

### 기본값 {#default-template}

기본값은 [!UICONTROL 자산의 기본 메타데이터 스키마 양식입니다] . 다음 하위 양식은 기본 양식의 속성을 상속합니다.

**image** is the schema form for assets with the MIME type &quot;image&quot;. 예: `image/jpeg`, `image/png`등. &quot;이미지&quot; 양식에는 다음과 같은 하위 양식 템플릿이 있습니다.
* **jpeg** is the schema form for assets with sub type `jpeg`.

* **tiff** 는 하위 유형의 자산에 대한 스키마 양식입니다 `tiff`.

**application** is the schema form for assets with MIME type `application`. 예: `application/pdf`, `application/zip`등. **pdf** is the schema form for assets with sub type `pdf`.

**video** is the schema form for assets with `video`MIME type, such `video/avi`, `video/mp4`so on.

### 컬렉션 {#collection-template}

컬렉션 [!UICONTROL 은] 컬렉션에 대한 스키마 양식입니다.

### contentfragment {#contentfragment-template}

컨텐츠 [!UICONTROL 조각은] 컨텐츠 조각에 대한 스키마 양식입니다.

### forms {#forms-template}

양식 [!UICONTROL 스키마] 양식은 [Adobe Experience Manager Forms와 관련이 있습니다](/help/forms/home.md).

>[!NOTE]
>
>스키마 양식의 하위 양식을 보려면 스키마 양식 이름을 클릭합니다.

## 메타데이터 스키마 양식 추가 {#add-a-metadata-schema-form}

1. 사용자 지정 템플릿을 목록에 추가하려면 도구 모음에서 **[!UICONTROL 만들기를]** 클릭합니다.

   >[!NOTE]
   >
   >편집되지 않은 템플릿에는 잠금 아이콘이 있습니다. 템플릿을 사용자 지정하면 템플릿 앞에서 잠금 아이콘이 사라집니다.

1. 대화 상자에서 스키마 양식의 제목을 입력하고 **[!UICONTROL 만들기를]** 클릭하여 양식 작성 프로세스를 완료합니다.

## 메타데이터 스키마 양식 편집 {#edit-metadata-schema-forms}

새로 추가되거나 기존 메타데이터 스키마 양식을 편집할 수 있습니다. 메타데이터 스키마 양식에는 탭 내의 탭 및 양식 항목이 포함됩니다. 이러한 양식 항목을 CRX 저장소의 메타데이터 노드 내의 필드에 매핑/구성할 수 있습니다. 메타데이터 스키마 양식에 새 탭 또는 양식 항목을 추가할 수 있습니다. 상위에서 파생된 탭 및 양식 항목은 잠긴 상태입니다. 하위 수준에서 변경할 수 없습니다.

1. 스키마 양식 페이지에서 양식 앞에 있는 확인란을 선택한 다음 도구 모음에서 **[!UICONTROL 편집을]** 클릭합니다.

1. [ **[!UICONTROL 메타데이터 스키마 편집기]** ] 페이지에서 [양식 **[!UICONTROL 작성] 탭의 구성 요소 유형 목록에서 하나 이상의 구성 요소를]** 기본 **[!UICONTROL 탭으로 드래그하여 자산의 속성 페이지를 사용자]** 정의합니다.

   ![자산 속성 사용자 지정을 위한 메타데이터 스키마 편집기](assets/metadata-schema-editor.png)

   *그림:[!UICONTROL 메타데이터 스키마]편집기의 기본[!UICONTROL 탭].*

1. 구성 요소를 구성하려면 구성 요소를 선택하고 설정 **[!UICONTROL 탭에서 해당 속성을]** 수정합니다.

### 양식 작성 탭 내의 구성 요소 {#components-within-the-build-form-tab}

양식 **[!UICONTROL 작성]** 탭에는 스키마 양식에서 사용하는 양식 항목이 나열됩니다. [ **[!UICONTROL 설정]** ] 탭에서는 [양식 **[!UICONTROL 작성] 탭에서 선택하는 각 항목의 속성을]** 제공합니다. 다음 표에는 양식 작성 탭에서 사용할 수 있는 양식 **[!UICONTROL 항목이]** 나열됩니다.

| 구성 요소 이름 | 설명 |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| [!UICONTROL 섹션 머리글] | 공통 구성 요소 목록에 대한 섹션 머리글을 추가합니다. |
| [!UICONTROL 한 줄 텍스트] | 단일 행 텍스트 속성을 추가합니다. 문자열로 저장됩니다. |
| [!UICONTROL 다중 값 텍스트] | 다중 값 텍스트 속성을 추가합니다. 문자열 배열로 저장됩니다. |
| [!UICONTROL 번호] | 숫자 구성 요소를 추가합니다. |
| [!UICONTROL 날짜] | 날짜 구성 요소를 추가합니다. |
| [!UICONTROL 드롭다운] | 드롭다운 목록을 추가합니다. |
| [!UICONTROL 표준 태그] | 태그 추가. |
| [!UICONTROL 스마트 태그] | 메타데이터 태그를 자동으로 추가하여 검색 기능을 강화합니다. |
| [!UICONTROL 숨김 필드] | 숨김 필드를 추가합니다. 자산이 저장되면 POST 매개 변수로 전송됩니다. |
| [!UICONTROL 자산 참조자] | 이 구성 요소를 추가하여 자산에서 참조하는 자산 목록을 봅니다. |
| [!UICONTROL 자산 참조] | 자산을 참조하는 자산 목록을 표시하려면 추가합니다. |
| [!UICONTROL 제품 참조] | 자산에 연결된 제품 목록을 표시하려면 추가합니다. |
| [!UICONTROL 자산 등급] | 자산 등급을 위한 표시 옵션에 추가합니다. |
| [!UICONTROL 상황에 맞는 메타데이터] | 자산의 속성 페이지에서 다른 메타데이터 탭의 표시를 제어하는 데 추가합니다. |

<!-- TBD: Check against 6.5.4.0 if the list of components is complete.
-->

#### 메타데이터 구성 요소 편집 {#edit-the-metadata-component}

양식에서 메타데이터 구성 요소의 속성을 편집하려면 구성 요소를 클릭하고 설정 **[!UICONTROL 탭에서 다음 속성의 전체 또는 하위 집합을]** 편집합니다.

**필드 레이블**: 자산의 속성 페이지에 표시되는 메타데이터 속성의 이름입니다.

**속성에 매핑**: 이 속성은 CRX 저장소에 저장된 자산 노드의 상대 경로/이름을 지정합니다. 경로가 자산의 노드 아래에 있음을 `./` 나타내므로 시작합니다.

다음은 이 속성에 유효한 값입니다.

* `./jcr:content/metadata/dc:title`: 자산의 메타데이터 노드에 값을 속성으로 저장합니다 `dc:title`.

* `./jcr:created`: 자산의 노드에 JCR 속성을 표시합니다. 보기 속성에 이러한 속성을 구성하는 경우 해당 속성이 보호되므로 편집 비활성화 상태로 표시하는 것이 좋습니다. 그렇지 않으면 에셋의 [!UICONTROL 속성을 저장할 때 오류] 에셋이 결과를 수정하지 못했습니다.

구성 요소가 메타데이터 스키마 양식에서 제대로 표시되도록 하려면 속성 경로에 공백이 없어야 합니다.

* **자리 표시자**: 이 속성을 사용하여 메타데이터 속성과 관련된 관련 자리 표시자 텍스트를 지정합니다.
* **필수**: 속성 페이지에서 메타데이터 속성을 필수로 표시하려면 이 속성을 사용합니다.
* **편집 비활성화**: 속성 페이지에서 메타데이터 속성을 편집할 수 없도록 하려면 이 속성을 사용합니다.
* **빈 필드를 읽기 전용으로 표시**: 값이 없더라도 속성 페이지에 메타데이터 속성을 표시하려면 이 속성을 표시합니다. 기본적으로 메타데이터 속성에 값이 없으면 속성 페이지에 나열되지 않습니다.
* **목록 순서 표시**: 이 속성을 사용하여 순차 선택 항목 목록을 표시합니다.
* **선택 사항**: 이 속성을 사용하여 목록의 선택 사항 지정
* **설명** : 이 속성을 사용하여 메타데이터 구성 요소에 대한 짧은 설명을 추가합니다.
* **클래스**: 속성이 연결된 객체 클래스입니다.
* **삭제**: 스키마 [!UICONTROL 양식에서] 구성 요소를 삭제하려면 삭제를 클릭합니다.

>[!NOTE]
>
>숨김 [!UICONTROL 필드] 구성 요소에는 이러한 속성이 포함되어 있지 않습니다. 대신 속성 이름, 값, 필드 레이블 및 설명과 같은 속성을 포함합니다. 숨김 필드 구성 요소의 값은 자산을 저장할 때마다 POST 매개 변수로 전송됩니다. 자산에 대한 메타데이터로 저장되지 않습니다.

필수 **[!UICONTROL 옵션을]** 선택하면 필수 메타데이터가 없는 자산을 검색할 수 있습니다. 필터 **** 패널에서 **[!UICONTROL 메타데이터 유효성 검사]** 설명 **[!UICONTROL 을 확장하고]** 잘못된옵션을선택합니다. 검색 결과에는 스키마 양식을 통해 구성한 필수 메타데이터가 누락된 에셋이 표시됩니다.

![필터 패널의 메타데이터 유효성 검사 조건자에서 잘못된 옵션을 선택했습니다. ](assets/chlimage_1-178.png)

컨텍스트 메타데이터 구성 요소를 스키마 양식의 임의 탭에 추가하는 경우 구성 요소는 특정 스키마가 적용되는 자산의 속성 페이지에 목록으로 나타납니다. 목록에는 컨텍스트 메타데이터 구성 요소를 적용한 탭을 제외한 다른 모든 탭이 포함되어 있습니다. 현재 이 기능은 컨텍스트에 따라 메타데이터 표시를 제어하는 기본 기능을 제공합니다.

![자산 속성의 컨텍스트 메타데이터 구성 요소 목록 탭](assets/chlimage_1-179.png)

컨텍스트 메타데이터 구성 요소가 적용된 탭 외에 속성 페이지에 탭을 표시하려면 목록에서 탭을 선택합니다. 탭이 속성 페이지에 추가됩니다.

![컨텍스트 메타데이터 목록에서 선택한 탭이 자산 속성 페이지에 표시됩니다.](assets/contextual-metadata-asset-properties.png)

*그림: 자산 속성 페이지의 컨텍스트 메타데이터*

### JSON 파일에서 속성 지정 {#specify-properties-in-json-file}

[ **[!UICONTROL 설정]** ] 탭에서 옵션에 대한 속성을 지정하는 대신 해당 키-값 쌍을 지정하여 JSON 파일에서 옵션을 정의할 수 있습니다. JSON 경로 **[!UICONTROL 필드에 JSON 파일 경로를]** 지정합니다.

#### 스키마 양식에서 탭 추가 또는 삭제 {#adding-deleting-a-tab-in-the-schema-form}

스키마 편집기를 사용하면 탭을 추가하거나 삭제할 수 있습니다. 기본 스키마 양식에는 **[!UICONTROL 기본]**, **[!UICONTROL 고급]** , **[!UICONTROL IPTC]****[!UICONTROL 및]** IPTC 확장탭이포함됩니다.

![메타데이터 스키마 양식의 기본 탭](assets/chlimage_1-181.png)

스키마 양식 `+` 에 새 탭을 추가하려면 클릭합니다. 기본적으로 새 탭에 이름이 지정됩니다 `Unnamed-1`. 설정 탭에서 이름을 수정할 수 **[!UICONTROL 있습니다]** .

탭 `X` 을 삭제하려면 클릭합니다.

![메타데이터 스키마 편집기를 사용하여 탭 추가 또는 삭제](assets/chlimage_1-182.png)

## 메타데이터 스키마 양식 삭제 {#delete-metadata-schema-forms}

[!DNL Experience Manager] 사용자 정의 스키마 양식만 삭제할 수 있습니다. 기본 스키마 양식/템플릿을 삭제할 수 없습니다. 그러나 이러한 양식에서 사용자 정의 변경 사항을 삭제할 수 있습니다.

양식을 삭제하려면 양식을 선택하고 삭제를 클릭합니다.

>[!NOTE]
>
>* 기본 양식에 대한 사용자 지정 변경 사항을 삭제하면 이 잠금 아이콘이 메타데이터 스키마 인터페이스에서 해당 양식이 기본 상태로 돌아갔다는 것을 나타내기 위해 앞에 다시 나타납니다.
>* Assets에서 메타데이터 스키마 양식을 삭제할 수 없습니다.


## MIME 형식의 스키마 양식 {#schema-forms-for-mime-types}

자산은 즉시 사용 가능한 다양한 MIME 유형에 대한 기본 양식을 제공합니다. 그러나 다양한 MIME 형식의 자산에 대해 사용자 지정 양식을 추가할 수 있습니다.

### MIME 유형에 새 양식 추가 {#add-new-forms-for-mime-types}

적절한 양식 유형 아래에서 새 양식을 만듭니다. 예를 들어 하위 유형에 대한 새 템플릿을 추가하려면 &quot;이미지&quot; 양식 아래에 양식을 `image/png` 만듭니다. 스키마 양식의 제목은 하위 유형 이름입니다. 이 경우 제목은 입니다 `png`.

#### 다양한 MIME 유형에 기존 스키마 템플릿 사용 {#use-an-existing-schema-template-for-various-mime-types}

기존 템플릿을 다른 MIME 유형에 사용할 수 있습니다. 예를 들어 MIME 형식의 자산에 `image/jpeg` 양식을 사용하십시오 `image/png`.

이 경우 CRX 저장소의 새 노드 `/etc/dam/metadataeditor/mimetypemappings` 를 만듭니다. 노드의 이름을 지정하고 다음 속성을 정의합니다.

| 이름 | 설명 | 유형 | 값 |
|------|-------------|------|-------|
| `exposedmimetype` | 매핑할 기존 양식의 이름 | `String` | `image/jpeg` |
| `mimetypes` | 특성에 정의된 양식을 사용하는 MIME 형식 `exposedmimetype` 목록 | `String` | `image/png` |

자산은 다음 MIME 형식과 스키마 양식을 매핑합니다.

| 스키마 양식 | MIME 형식 |
| --------------------------- | --------------------------------------------------- |
| image/jpeg | image/pjpeg |
| image/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related; type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related; type=application/x-SpinSet |
| application/x-mixedMediaSet | Multipart/Related; type=application/x-MixedMediaSet |
| video/quicktime | video/x-quicktime |
| video/mpeg4 | video/mp4 |
| 비디오/avi | video/avi, video/msvideo, video/x-msvideo |
| video/wmv | video/x-ms-wmv |
| 비디오/flv | video/x-flv |

## 메타데이터 스키마에 대한 액세스 권한 부여 {#grant-access-to-metadata-schemas}

메타데이터 스키마 기능은 관리자만 사용할 수 있습니다. 하지만 관리자는 일부 권한을 수정하여 비관리자에게 액세스할 수 있습니다. 관리자가 아닌 사용자에게는 `/conf` 폴더에 대한 권한이 생성, 수정 및 삭제되어야 합니다.

## 폴더별 메타데이터 적용 {#apply-folder-specific-metadata}

에셋을 사용하면 메타데이터 스키마의 변형을 정의하고 특정 폴더에 적용할 수 있습니다.

예를 들어 기본 메타데이터 스키마의 변형을 정의하고 폴더에 적용할 수 있습니다. 수정된 스키마를 적용하면 폴더 내의 자산에 적용되는 원본 기본 메타데이터 스키마를 무시합니다.

이 스키마가 적용되는 폴더에 업로드된 자산만 변형 메타데이터 스키마에 정의된 수정된 메타데이터에 따릅니다. 원본 스키마가 적용된 다른 폴더의 에셋은 원본 스키마에 정의된 메타데이터를 계속 준수하므로

자산별 메타데이터 상속은 계층의 첫 번째 수준 폴더에 적용되는 스키마를 기반으로 합니다. 즉, 폴더에 하위 폴더가 없으면 폴더 내의 에셋은 폴더에 적용된 스키마의 메타데이터를 상속합니다.

폴더에 하위 폴더가 있는 경우 하위 폴더 내의 에셋은 하위 폴더 수준에서 다른 스키마를 적용하는 경우 하위 폴더 수준에서 적용된 스키마의 메타데이터를 상속합니다. 하지만 하위 폴더 수준에서 스키마나 동일한 스키마가 적용되지 않으면 하위 폴더 에셋은 상위 폴더 수준에서 적용된 스키마의 메타데이터를 상속합니다.

1. 인터페이스에서 [!DNL Experience Manager] 도구 **[!UICONTROL > 자산]** **[!UICONTROL >]** 메타데이터 스키마 **[!UICONTROL 로 이동합니다]**. 메타데이터 **[!UICONTROL 스키마 양식]** 페이지가 표시됩니다.
1. 양식 앞에 있는 확인란(예: 기본 메타데이터 양식)을 선택하고 **[!UICONTROL 복사를]** 클릭하고 사용자 지정 양식으로 저장합니다. 예를 들어 양식의 사용자 지정 이름을 지정합니다 `my_default`. 또는 사용자 지정 양식을 만들 수 있습니다.

1. [ **[!UICONTROL 메타데이터 스키마 양식]** ] 페이지에서 `my_default` 양식을 선택한 다음 편집을 **[!UICONTROL 클릭합니다]**.

1. [ **[!UICONTROL 메타데이터 스키마 편집기]** ] 페이지에서 스키마 양식에 텍스트 필드를 추가합니다. 예를 들어 레이블이 카테고리로 필드를 **[!UICONTROL 추가합니다]**.

   ![메타데이터 스키마 양식 편집기에 추가된 텍스트 필드](assets/text-field-metadata-schema-editor.png)

   *그림: 메타데이터 스키마 양식 편집기에 텍스트 필드가 추가되었습니다.*

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다. 수정된 양식이 [ **[!UICONTROL 메타데이터 스키마 양식] 페이지에]** 나열됩니다.
1. 도구 모음 **[!UICONTROL 에서]** 폴더에 적용을 클릭하여 사용자 지정 메타데이터를 폴더에 적용합니다.

1. 수정된 스키마를 적용할 폴더를 선택한 다음 적용을 **[!UICONTROL 클릭합니다]**.

   ![메타데이터 스키마를 적용할 폴더 선택](assets/chlimage_1-188.png)

1. 폴더에 다른 메타데이터 스키마가 적용된 경우 기존 메타데이터 스키마를 덮어쓸지 묻는 메시지가 나타납니다. 덮어쓰기를 **클릭합니다**.
1. 확인 **을** 클릭하여 성공 메시지를 닫습니다.
1. 수정된 메타데이터 스키마를 적용한 폴더로 이동합니다.

## 필수 메타데이터 정의 {#define-mandatory-metadata}

폴더에 업로드된 자산에 대해 적용되는 폴더 수준에서 필수 필드를 정의할 수 있습니다. 앞에서 정의된 필수 필드에 대해 메타데이터가 없는 자산을 업로드하면 카드 보기의 자산에 누락된 메타데이터에 대한 시각적 표시가 나타납니다.

>[!NOTE]
>
>메타데이터 필드는 다른 필드의 값을 기준으로 필수로 정의할 수 있습니다. 카드 보기에서는 이러한 필수 메타데이터 필드에 대한 누락된 메타데이터에 대한 경고 메시지를 표시하지 [!DNL Experience Manager] 않습니다.

1. 인터페이스에서 [!DNL Experience Manager] 도구 **[!UICONTROL > 자산]** **[!UICONTROL >]** 메타데이터 스키마 **[!UICONTROL 로 이동합니다]**. 메타데이터 **[!UICONTROL 스키마 양식]** 페이지가 표시됩니다.
1. 기본 메타데이터 양식을 사용자 지정 양식으로 저장합니다. 예를 들어 다른 이름으로 저장합니다 `my_default`.

1. 사용자 지정 양식을 편집합니다. 필수 필드를 추가합니다. 예를 들어 카테고리 **** 필드를 추가하고 필드를 필수 필드로 만듭니다.

   ![메타데이터 스키마 양식 편집기의 규칙 탭에서 필수를 선택하여 메타데이터 양식에 필수 필드 추가](assets/mandatory-field-metadata-schema-editor.png)

   *그림: 메타데이터 스키마 양식 편집기의 필수 필드입니다.*

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다. 수정된 양식이 [ **[!UICONTROL 메타데이터 스키마 양식] 페이지에]** 나열됩니다. 양식을 선택한 다음 도구 모음 **[!UICONTROL 에서 폴더에]** 적용을 클릭하여 사용자 지정 메타데이터를 폴더에 적용합니다.

1. 사용자 지정 양식에 추가한 필수 필드에 대한 메타데이터가 없는 일부 자산을 폴더로 이동하고 업로드합니다. 필수 필드에 대한 누락된 메타데이터에 대한 메시지가 자산의 카드 보기에 표시됩니다.

   ![폴더에 자산 업로드 시 자산 카드 보기에서 필수 메타데이터가 누락되는 메시지](assets/chlimage_1-192.png)

1. (선택 사항) 액세스 `https://[aem_server]:[port]/system/console/components/`. 기본적으로 비활성화된 구성 `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` 요소를 구성하고 활성화합니다. 자산에 대한 메타데이터의 유효성을 [!DNL Experience Manager] 확인하는 빈도를 설정합니다. 이 구성은 자산의 속성 `hasValidMetadata` 을 `jcr:content` 추가합니다. 이 속성을 사용하면 검색에서 필터 결과가 잘못될 [!DNL Experience Manager] 수 있습니다. 확인 후 자산을 추가하는 경우, 자산은 다음 예약된 확인 `hasValidMetadata` 이 될 때까지 로 플래그되지 않습니다. 따라서 다음 예약된 확인 후 까지 유효하지 않은 메타데이터의 검색 필터에는 자산이 표시되지 않습니다.

   >[!CAUTION]
   >
   >메타데이터 유효성 검사는 리소스를 많이 사용하므로 시스템 성능에 영향을 줄 수 있습니다. 그에 따라 검사를 예약합니다. 서버에서 부하를 처리할 수 없는 경우 이 작업을 비활성화하십시오.

<!-- TBD: Add this method to find invalid metadata in the metadata article later.
-->
