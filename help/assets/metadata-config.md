---
title: 메타데이터 기능 구성 및 관리.
description: 메타데이터 추가 및 관리와 관련된  [!DNL Experience Manager Assets] 기능의 구성 및 관리.
contentOwner: AG
role: Business Practitioner, Administrator
feature: 메타데이터
exl-id: 56c92b7f-e687-4ab5-a376-afa58bdb6ee0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 3%

---

# [!DNL Assets] {#config-metadata}에서 메타데이터 기능 구성 및 관리

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] 모든 자산에 대한 메타데이터를 유지합니다. 자산을 보다 쉽게 분류하고 구성할 수 있으며 특정 자산을 찾는 사람에게 도움이 됩니다. 자산으로 메타데이터를 유지 및 관리하는 기능을 사용하면 메타데이터를 기반으로 자산을 자동으로 구성하고 처리할 수 있습니다. [!DNL Adobe Experience Manager Assets] 관리자는 기본 Adobe 오퍼링을 수정할 메타데이터 기능을 구성하고 사용자 지정할 수 있습니다.

## 메타데이터 스키마 편집 {#metadata-schema}

자세한 내용은 [메타데이터 스키마 양식 편집](metadata-schemas.md#edit-metadata-schema-forms)을 참조하십시오.

## [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem} 내에 사용자 지정 네임스페이스를 등록합니다

[!DNL Experience Manager] 내에 고유한 네임스페이스를 추가할 수 있습니다. `cq`, `jcr`, `sling` 등과 같이 사전 정의된 네임스페이스가 있는 것처럼 저장소 메타데이터 및 XML 처리를 위한 네임스페이스를 가질 수 있습니다.

1. 노드 유형 관리 페이지 `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`에 액세스합니다.
1. 네임스페이스 관리 페이지에 액세스하려면 페이지 맨 위에서 **[!UICONTROL 네임스페이스]**&#x200B;를 클릭하십시오.
1. 네임스페이스를 추가하려면 페이지 하단에서 **[!UICONTROL 새로 만들기]**&#x200B;를 클릭합니다.
1. XML 네임스페이스 규칙에서 사용자 지정 네임스페이스를 지정합니다. ID를 URI 형태로 지정하고 ID에 연결된 접두사를 지정합니다. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

## 벌크 메타데이터 업데이트 {#bulk-metadata-update-limit}에 대한 제한 구성

DOS(서비스 거부) 등의 상황을 방지하기 위해 [!DNL Enterprise Manager] 은 Sling 요청에서 지원되는 매개 변수 수를 제한합니다. 한 번에 많은 자산의 메타데이터를 업데이트할 때 제한에 도달할 수 있으며 더 많은 자산에 대해 메타데이터가 업데이트되지 않습니다. Enterprise Manager는 로그에 다음 경고를 생성합니다.

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

제한을 변경하려면 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**&#x200B;에 액세스하여 **[!UICONTROL Apache Sling 요청 매개 변수 처리]** OSGi 구성에서 **[!UICONTROL 최대 POST 매개 변수]**&#x200B;의 값을 변경합니다.

## 메타데이터 프로필 {#metadata-profiles}

메타데이터 프로필을 사용하면 폴더 내의 자산에 기본 메타데이터를 적용할 수 있습니다. 메타데이터 프로필을 만들어 폴더에 적용합니다. 이후에 폴더에 업로드하는 모든 자산은 메타데이터 프로필에서 구성한 기본 메타데이터를 상속합니다.

### 메타데이터 프로필 {#adding-a-metadata-profile} 추가

1. **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 메타데이터 프로필]**&#x200B;로 이동하고 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.
1. 프로필의 제목(예: `Sample Metadata`)을 입력하고 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 메타데이터 프로필에 대한 [!UICONTROL 양식 편집]이 표시됩니다.

   ![메타데이터 양식 편집](assets/metadata-edit-form.png)

1. 구성 요소를 클릭하고 **[!UICONTROL 설정]** 탭에서 해당 속성을 구성합니다. 예를 들어 **[!UICONTROL 설명]** 구성 요소를 클릭하고 해당 속성을 편집합니다.

   ![메타데이터 프로필에서 구성 요소 설정](assets/metadata-profile-component-setting.png)

   **[!UICONTROL 설명]** 구성 요소에 대해 다음 속성을 편집합니다.

   * **[!UICONTROL 필드 레이블]**:메타데이터 속성의 표시 이름입니다. 사용자 참조용입니다.

   * **[!UICONTROL 속성에 매핑]**:이 속성의 값은 저장소에 저장되는 자산 노드에 대한 상대 경로 또는 이름을 제공합니다. 이 값은 경로가 자산의 노드 아래에 있음을 나타내므로 항상 `./` 로 시작해야 합니다.

   ![메타데이터 프로필의 속성 설정에 매핑](assets/metadata-profile-setting-map-property.png)

   **[!UICONTROL 속성에 매핑]**&#x200B;에 대해 지정하는 값은 자산의 메타데이터 노드 아래에 속성으로 저장됩니다. 예를 들어 **[!UICONTROL 속성에 매핑]**&#x200B;의 이름으로 `./jcr:content/metadata/dc:desc`을 지정하는 경우 [!DNL Assets]은 자산의 메타데이터 노드에 값 `dc:desc`을 저장합니다.

   * **[!UICONTROL 기본값]**:이 속성을 사용하여 메타데이터 구성 요소에 대한 기본값을 추가합니다. 예를 들어 &quot;My description&quot;을 지정하면 이 값이 자산의 메타데이터 노드에서 속성 `dc:desc`에 할당됩니다.

   ![메타데이터 프로필에서 기본 설명 설정](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >에 이미 존재하지 않는 새 메타데이터 속성에 기본값을 추가합니다. `/jcr:content/metadata` node)가 기본적으로 자산의 속성 페이지에 속성 및 해당 값을 표시하지 않습니다. 자산의 [!UICONTROL 속성] 페이지에서 새 속성을 보려면 해당 스키마 양식을 수정합니다.

1. (선택 사항) **[!UICONTROL 양식 작성]** 탭에서 양식 편집에 구성 요소를 더 추가하고 **[!UICONTROL 설정]** 탭에서 해당 속성을 구성합니다. 다음 속성은 **[!UICONTROL 빌드 양식]** 탭에서 사용할 수 있습니다.

| 구성 요소 | 속성 |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL 섹션 머리글] | 필드 레이블, <br> 설명 |
| [!UICONTROL 한 줄 텍스트] | 필드 레이블, <br> 속성에 매핑, <br> 기본값 |
| [!UICONTROL 다중 값 텍스트] | 필드 레이블, <br> 속성에 매핑, <br> 기본값 |
| [!UICONTROL 번호] | 필드 레이블, <br> 속성에 매핑, <br> 기본값 |
| [!UICONTROL 날짜] | 필드 레이블, <br> 속성에 매핑, <br> 기본값 |
| [!UICONTROL 표준 태그] | 필드 레이블, <br> 속성에 매핑, <br> 기본값, <br> 설명 |

1. **[!UICONTROL 완료]**&#x200B;를 클릭합니다. 메타데이터 프로필이 **[!UICONTROL 메타데이터 프로필]** 페이지의 프로필 목록에 추가됩니다.<br>

   ![메타데이터 프로필 페이지에 추가된 메타데이터 프로필](assets/MetadataProfiles-page.png)

### 메타데이터 프로필 {#copying-a-metadata-profile} 복사

1. **[!UICONTROL 메타데이터 프로필]** 페이지에서 메타데이터 프로필을 선택하여 복사본을 만듭니다.

   ![메타데이터 프로필 복사](assets/metadata-profile-edit-copy-option.png)

1. 도구 모음에서 **[!UICONTROL 복사]**&#x200B;를 클릭합니다.
1. **[!UICONTROL 메타데이터 프로필 복사]** 대화 상자에서 메타데이터 프로필의 새 사본에 대한 제목을 입력합니다.
1. **[!UICONTROL 복사]**&#x200B;를 클릭합니다. 메타데이터 프로필 사본이 **[!UICONTROL 메타데이터 프로필]** 페이지의 프로필 목록에 나타납니다.

   ![메타데이터 프로필 페이지에 추가된 메타데이터 프로필 사본](assets/copy-metadata-profile.png)

### 메타데이터 프로필 {#deleting-a-metadata-profile} 삭제

1. **[!UICONTROL 메타데이터 프로필]** 페이지에서 삭제할 프로필을 선택합니다.

1. 도구 모음에서 **[!UICONTROL 메타데이터 프로필 삭제]**&#x200B;를 클릭합니다.
1. 대화 상자에서 **[!UICONTROL 삭제]**&#x200B;를 클릭하여 삭제 작업을 확인합니다. 메타데이터 프로필이 목록에서 삭제됩니다.

<!-- TBD: Revisit to find out the correct config. and update these steps. When fixed, also o
These steps have been carried forward from old AEM versions. See https://helpx.adobe.com/experience-manager/6-2/assets/using/metadata-profiles.html#ApplyingaMetadataProfiletoFolders

### Configuration to apply a metadata profile globally {#apply-a-metadata-profile-globally}

In addition to applying a profile to a folder, you can also apply one globally so that any content uploaded into [!DNL Experience Manager] assets in any folder has the selected profile applied.

You can reprocess assets in a folder that already has an existing metadata profile that you later changed. See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets).

To apply a metadata profile globally, follow these steps:

* Navigate to `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` and apply the appropriate profile and click **[!UICONTROL Save]**.

  ![Apply metadata profile to a folder globally](assets/metadata-profile-folder-setting.png)

* In CRXDE Lite, navigate to the following node: `/content/dam/jcr:content`. Add the property `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` and click **[!UICONTROL Save All]**.

  ![See applied metadata profile to a folder in the JCR in CRXDE](assets/metadata-profile-folder-setting2.png)
-->

## 폴더 {#folder-metadata-schema}에 대한 메타데이터 스키마

[!DNL Adobe Experience Manager Assets]을 사용하면 폴더 속성 페이지에 표시되는 레이아웃 및 메타데이터를 정의하는 자산 폴더에 대한 메타데이터 스키마를 생성할 수 있습니다. 

### {#add-a-folder-metadata-schema-form} 폴더 메타데이터 스키마 추가

폴더 메타데이터 스키마 Forms 편집기를 사용하여 폴더에 대한 메타데이터 스키마를 만들고 편집합니다.

1. [!DNL Experience Manager] 인터페이스에서 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 폴더 메타데이터 스키마]**&#x200B;로 이동합니다.
1. [!UICONTROL 폴더 메타데이터 스키마 Forms] 페이지에서 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.
1. 양식의 이름을 지정하고 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 새 스키마 양식은 [!UICONTROL 스키마 Forms] 페이지에 나열됩니다.

### 폴더 메타데이터 스키마 양식 편집 {#edit-folder-metadata-schema-forms}

다음을 포함하는 새로 추가되거나 기존 메타데이터 스키마 양식을 편집할 수 있습니다.

* 탭
* 탭 내의 양식 항목.

이러한 양식 항목을 CRX 저장소의 메타데이터 노드 내의 필드에 매핑/구성할 수 있습니다. 새 탭 또는 양식 항목을 메타데이터 스키마 양식에 추가할 수 있습니다.

1. 스키마 Forms 페이지에서 생성한 양식을 선택한 다음 도구 모음에서 **[!UICONTROL 편집]** 옵션을 선택합니다.
1. 폴더 메타데이터 스키마 편집기 페이지에서 `+` 을 클릭하여 양식에 탭을 추가합니다. 탭의 이름을 변경하려면 기본 이름을 클릭하고 **[!UICONTROL 설정]** 아래에 새 이름을 지정합니다.

   ![custom_tab](assets/custom_tab.png)

   탭을 더 추가하려면 `+` 을 클릭합니다. 탭에서 `X` 을 클릭하여 삭제합니다.

1. 활성 탭에서 **[!UICONTROL 빌드 양식]** 탭에서 구성 요소를 한 개 이상 추가합니다.

   ![adding_components](assets/adding_components.png)

   여러 탭을 만드는 경우 특정 탭을 클릭하여 구성 요소를 추가합니다.

1. 구성 요소를 구성하려면 구성 요소를 선택하고 **[!UICONTROL 설정]** 탭에서 해당 속성을 수정합니다.

   필요한 경우 **[!UICONTROL 설정]** 탭에서 구성 요소를 삭제합니다.

   ![configure_properties](assets/configure_properties.png)

1. 도구 모음에서 **[!UICONTROL 저장]** 을 클릭하여 변경 사항을 저장합니다.

#### 양식을 작성할 구성 요소 {#components-to-build-forms}

**[!UICONTROL 빌드 양식]** 탭에는 폴더 메타데이터 스키마 양식에서 사용하는 양식 항목이 나열됩니다. **[!UICONTROL 설정]** 탭에는 **[!UICONTROL 빌드 양식]** 탭에서 선택한 각 항목에 대한 속성이 표시됩니다. 다음은 **[!UICONTROL 빌드 양식]** 탭에서 사용할 수 있는 양식 항목의 목록입니다.

| 구성 요소 이름 | 설명 |
|---|---|
| [!UICONTROL 섹션 머리글] | 공통 구성 요소 목록에 대한 섹션 머리글을 추가합니다. |
| [!UICONTROL 한 줄 텍스트] | 한 줄 텍스트 속성을 추가합니다. 문자열로 저장됩니다. |
| [!UICONTROL 다중 값 텍스트] | 다중 값 텍스트 속성을 추가합니다. 문자열 배열로 저장됩니다. |
| [!UICONTROL 번호] | 숫자 구성 요소를 추가합니다. |
| [!UICONTROL 날짜] | 날짜 구성 요소를 추가합니다. |
| [!UICONTROL 드롭다운] | 드롭다운 목록을 추가합니다. |
| [!UICONTROL 표준 태그] | 태그 추가. |
| [!UICONTROL 숨김 필드] | 숨김 필드를 추가합니다. 자산을 저장할 때 POST 매개 변수로 전송됩니다. |

#### 양식 항목 편집 {#editing-form-items}

양식 항목의 속성을 편집하려면 구성 요소를 클릭하고 **[!UICONTROL 설정]** 탭에서 다음 속성의 하위 집합을 모두 또는 편집하십시오.

**[!UICONTROL 필드 레이블]**:폴더의 속성 페이지에 표시되는 메타데이터 속성의 이름입니다.

**[!UICONTROL 속성에 매핑]**:이 속성은 CRX 저장소가 저장된 폴더 노드의 상대 경로를 지정합니다. &quot;**로 시작합니다./**&quot; - 경로가 폴더의 노드 아래에 있음을 나타냅니다.

다음은 이 속성에 유효한 값입니다.

* `./jcr:content/metadata/dc:title`:폴더의 메타데이터 노드에 값을 속성으로 저장합니다 `dc:title`.

* `./jcr:created`:폴더의 노드에 JCR 속성을 표시합니다. CRXDE에서 이러한 속성을 구성하는 경우, Adobe은 이러한 속성이 보호되므로 편집 비활성화로 표시하는 것이 좋습니다. 그렇지 않으면 자산의 속성을 저장할 때 &#39; `Asset(s) failed to modify`&#39; 오류가 발생합니다.

구성 요소가 메타데이터 스키마 양식에 올바르게 표시되는지 확인하려면 속성 경로에 공백을 포함하지 마십시오.

**[!UICONTROL JSON 경로]**:옵션에 키-값 쌍을 지정하는 JSON 파일의 경로를 지정하는 데 사용합니다.

**[!UICONTROL 자리 표시자]**:이 속성을 사용하여 메타데이터 속성과 관련된 관련 자리 표시자 텍스트를 지정합니다.

**[!UICONTROL 선택]** 사항:이 속성을 사용하여 목록에서 선택 사항을 지정합니다.

**[!UICONTROL 설명]**:이 속성을 사용하여 메타데이터 구성 요소에 대한 간단한 설명을 추가합니다.

**[!UICONTROL 클래스]**:속성이 연결된 객체 클래스입니다.

### 폴더 메타데이터 스키마 양식 삭제 {#delete-folder-metadata-schema-forms}

폴더 메타데이터 스키마 Forms 페이지에서 폴더 메타데이터 스키마 양식을 삭제할 수 있습니다. 양식을 삭제하려면 양식을 선택하고 도구 모음에서 삭제 옵션을 클릭합니다.

![delete_form](assets/delete_form.png)

### 폴더 메타데이터 스키마 {#assign-a-folder-metadata-schema} 할당

폴더 메타데이터 스키마 Forms 페이지나 폴더를 만들 때 폴더에 폴더 메타데이터 스키마를 할당할 수 있습니다.

폴더에 대한 메타데이터 스키마를 구성하는 경우 스키마 양식의 경로는 `./jcr:content` 아래의 폴더 노드의 `folderMetadataSchema` 속성에 저장됩니다.

#### 폴더 메타데이터 스키마 페이지 {#assign-to-a-schema-from-the-folder-metadata-schema-page}에서 스키마에 할당

1. [!DNL Experience Manager] 인터페이스에서 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 폴더 메타데이터 스키마]**&#x200B;로 이동합니다.
1. 폴더 메타데이터 스키마 Forms 페이지에서 폴더에 적용할 스키마 양식을 선택합니다.
1. 도구 모음에서 **[!UICONTROL 폴더에 적용]**&#x200B;을 클릭합니다.

1. 스키마를 적용할 폴더를 선택한 다음 **[!UICONTROL 적용]**&#x200B;을 클릭합니다. 메타데이터 스키마가 폴더에 이미 적용된 경우 기존 메타데이터 스키마를 덮어쓸 것임을 알리는 경고 메시지가 표시됩니다. **[!UICONTROL 덮어쓰기]**&#x200B;를 클릭합니다.
1. 메타데이터 스키마를 적용한 폴더의 메타데이터 속성을 엽니다.

   ![folder_properties](assets/folder_properties.png)

   폴더 메타데이터 필드를 보려면 **[!UICONTROL 폴더 메타데이터]** 탭을 클릭합니다.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### {#assign-a-schema-when-creating-a-folder} 폴더를 만들 때 스키마 할당

폴더를 만들 때 폴더 메타데이터 스키마를 할당할 수 있습니다. 시스템에 폴더 메타데이터 스키마가 하나 이상 있으면 **[!UICONTROL 폴더 만들기]** 대화 상자에 추가 목록이 표시됩니다. 원하는 스키마를 선택할 수 있습니다. 기본적으로 선택된 스키마가 없습니다.

1. [!DNL Experience Manager Assets] 사용자 인터페이스에서 도구 모음에서 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.
1. 폴더의 제목과 이름을 지정합니다.
1. 폴더 메타데이터 스키마 목록에서 원하는 스키마를 선택합니다. 그런 다음 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

   ![select_schema](assets/select_schema.png)

1. 메타데이터 스키마를 적용한 폴더의 메타데이터 속성을 엽니다.
1. 폴더 메타데이터 필드를 보려면 **[!UICONTROL 폴더 메타데이터]** 탭을 클릭합니다.

### 폴더 메타데이터 스키마 {#use-the-folder-metadata-schema} 사용

폴더 메타데이터 스키마로 구성된 폴더의 속성을 엽니다. **[!UICONTROL 폴더 메타데이터]** 탭이 [!UICONTROL 속성] 페이지에 표시됩니다. 폴더 메타데이터 스키마 양식을 보려면 이 탭을 선택합니다.

다양한 필드에 메타데이터 값을 입력하고 **[!UICONTROL 저장]**&#x200B;을 클릭하여 값을 저장합니다. 지정하는 값은 CRX 저장소의 폴더 노드에 저장됩니다.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## 팁 및 제한 사항 {#best-practices-limitations}

* 사용자 지정 네임스페이스에 메타데이터를 가져오려면 먼저 네임스페이스를 등록합니다.
* 속성 선택기는 스키마 편집기 및 검색 양식에 사용되는 속성을 표시합니다. 속성 선택기에서 자산에서 메타데이터 속성을 선택하지 않습니다.
* [!DNL Experience Manager] 6.5로 업그레이드하기 전에 기존 메타데이터 프로필이 있을 수 있습니다. 업그레이드 후 [!UICONTROL 메타데이터 프로필] 탭의 [!UICONTROL 속성]에 이러한 프로필을 적용하면 메타데이터 양식 필드가 표시되지 않습니다. 그러나 새로 만든 메타데이터 프로필을 적용하면 양식 필드가 표시되지만 예상대로 사용할 수 없습니다. 기능은 손실되지 않지만 (사용할 수 없음) 양식 필드를 보려면 기존 메타데이터 프로필을 편집하고 저장합니다.

>[!MORELIKETHIS]
>
>* [메타데이터 개념 및 이해](metadata-concepts.md).
>* [여러 컬렉션의 메타데이터 속성을 편집합니다](manage-collections.md#editing-collection-metadata-in-bulk).
>* [Experience Manager 자산에서 메타데이터 가져오기 및 내보내기](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html).
>* [메타데이터, 이미지 및 비디오 처리 프로필](processing-profiles.md).
>* [처리 프로필을 사용하도록 디지털 자산을 구성하는 우수 사례](/help/assets/organize-assets.md).
>* [XMP 원본에 쓰기](/help/assets/xmp-writeback.md).

