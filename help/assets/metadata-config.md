---
title: 메타데이터 기능 구성 및 관리.
description: 구성 및 관리 [!DNL Experience Manager Assets] 메타데이터 추가 및 관리와 관련된 기능입니다.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 56c92b7f-e687-4ab5-a376-afa58bdb6ee0
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1978'
ht-degree: 3%

---

# 에서 메타데이터 기능 구성 및 관리 [!DNL Assets] {#config-metadata}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-profiles.html?lang=en) |
| AEM 6.5 | 이 문서 |

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, and so on, operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] 는 모든 에셋에 대한 메타데이터를 유지합니다. 에셋을 보다 쉽게 분류하고 구성할 수 있으며 특정 에셋을 찾는 사람들에게 도움이 됩니다. 에셋으로 메타데이터를 보관하고 관리할 수 있으므로 에셋의 메타데이터를 기반으로 에셋을 자동으로 구성하고 처리할 수 있습니다. [!DNL Adobe Experience Manager Assets] 관리자가 메타데이터 기능을 구성하고 사용자 정의하여 기본 Adobe 오퍼링을 수정할 수 있습니다.

## 메타데이터 스키마 편집 {#metadata-schema}

자세한 내용은 [메타데이터 스키마 양식 편집](metadata-schemas.md#edit-metadata-schema-forms).

## 내에서 사용자 지정 네임스페이스 등록 [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

내에서 나만의 네임스페이스를 추가할 수 있습니다. [!DNL Experience Manager]. 다음과 같이 사전 정의된 네임스페이스가 있는 것처럼 `cq`, `jcr`, 및 `sling`저장소 메타데이터 및 XML 처리를 위한 네임스페이스를 가질 수 있습니다.

1. 노드 유형 관리 페이지에 액세스 `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. 네임스페이스 관리 페이지에 액세스하려면 다음을 클릭합니다. **[!UICONTROL 네임스페이스]** 을 클릭합니다.
1. 네임스페이스를 추가하려면 **[!UICONTROL 신규]** 페이지 하단에 있습니다.
1. XML 네임스페이스 규칙에서 사용자 지정 네임스페이스를 지정합니다. URI 형식으로 ID를 지정하고 ID에 연결된 접두사를 지정합니다. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

## 벌크 메타데이터 업데이트에 대한 제한 구성 {#bulk-metadata-update-limit}

서비스 거부(DOS)와 같은 상황을 방지하기 위해 [!DNL Enterprise Manager] sling 요청에서 지원되는 매개 변수의 수를 제한합니다. 한 번에 많은 에셋의 메타데이터를 업데이트할 때 한도에 도달할 수 있으며 더 많은 에셋에 대한 메타데이터는 업데이트되지 않습니다. Enterprise Manager는 로그에 다음 경고를 생성합니다.

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

한도를 변경하려면 액세스 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]** 및 값 변경 **[!UICONTROL 최대 POST 매개변수]** 위치: **[!UICONTROL Apache Sling 요청 매개 변수 처리]** OSGi 구성.

## 메타데이터 프로필 {#metadata-profiles}

메타데이터 프로필을 사용하면 폴더 내의 에셋에 기본 메타데이터를 적용할 수 있습니다. 메타데이터 프로필을 만들어 폴더에 적용합니다. 나중에 폴더에 업로드하는 모든 에셋은 메타데이터 프로필에서 구성한 기본 메타데이터를 상속합니다.

### 메타데이터 프로필 추가 {#adding-a-metadata-profile}

1. 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL 메타데이터 프로필]** 및 클릭 **[!UICONTROL 만들기]**.
1. 프로필의 제목 입력(예: ) `Sample Metadata`, 및 클릭 **[!UICONTROL 만들기]**. 다음 [!UICONTROL 양식 편집] 메타데이터 프로필이 표시됩니다.

   ![메타데이터 양식 편집](assets/metadata-edit-form.png)

1. 구성 요소를 클릭하고 **[!UICONTROL 설정]** 탭. 예를 들어 **[!UICONTROL 설명]** 구성 요소를 확인하고 속성을 편집합니다.

   ![메타데이터 프로필의 구성 요소 설정](assets/metadata-profile-component-setting.png)

   다음에 대한 속성을 편집합니다. **[!UICONTROL 설명]** 구성 요소:

   * **[!UICONTROL 필드 레이블]**: 메타데이터 속성의 표시 이름입니다. 사용자 참조용으로만 사용됩니다.

   * **[!UICONTROL 속성에 매핑]**: 이 속성의 값은 저장소에 저장된 에셋 노드에 대한 상대 경로 또는 이름을 제공합니다. 값은 항상 다음으로 시작해야 합니다. `./` 경로가 자산의 노드 아래에 있음을 나타내기 때문입니다.

   ![메타데이터 프로필의 속성 설정에 매핑](assets/metadata-profile-setting-map-property.png)

   에 지정하는 값 **[!UICONTROL 속성에 매핑]** 는 에셋의 메타데이터 노드 아래에 속성으로 저장됩니다. 예를 들어, `./jcr:content/metadata/dc:desc` 을(를) 의 이름으로 **[!UICONTROL 속성에 매핑]**, [!DNL Assets] 값 저장 `dc:desc` (자산의 메타데이터 노드) Adobe은 메타데이터 스키마의 특정 속성에 필드를 한 개만 매핑할 것을 권장합니다. 그렇지 않으면 속성에 매핑된 최신 추가 필드가 시스템에 의해 선택됩니다.

   * **[!UICONTROL 기본값]**: 이 속성을 사용하여 메타데이터 구성 요소에 대한 기본값을 추가합니다. 예를 들어 &quot;내 설명&quot;을 지정하면 이 값이 속성에 지정됩니다 `dc:desc` (자산의 메타데이터 노드)

   ![메타데이터 프로필에 기본 설명 설정](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >새 메타데이터 속성(에 존재하지 않음)에 기본값 추가 `/jcr:content/metadata` node)가 자산의 속성 및 값을 표시하지 않습니다. [!UICONTROL 속성] 기본적으로 페이지입니다. 에셋의 새 속성을 보려면 [!UICONTROL 속성] 페이지에서 해당 스키마 양식을 수정합니다.

1. (선택 사항) **[!UICONTROL 양식 작성]** 탭, 더 많은 구성 요소 추가 [!UICONTROL 양식 편집], 및에서 해당 속성 구성 **[!UICONTROL 설정]** 탭. 에서 다음 속성을 사용할 수 있습니다. **[!UICONTROL 양식 작성]** 탭:

| 구성 요소 | 속성 |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL 섹션 머리글] | 필드 레이블, <br> 설명 |
| [!UICONTROL 한 줄 텍스트] | 필드 레이블, <br> 속성에 매핑, <br> 기본값 |
| [!UICONTROL 다중 값 텍스트] | 필드 레이블, <br> 속성에 매핑, <br> 기본값 |
| [!UICONTROL 숫자] | 필드 레이블, <br> 속성에 매핑, <br> 기본값 |
| [!UICONTROL 날짜] | 필드 레이블, <br> 속성에 매핑, <br> 기본값 |
| [!UICONTROL 표준 태그] | 필드 레이블, <br> 속성에 매핑, <br> 기본값, <br> 설명 |

1. 클릭 **[!UICONTROL 완료]**. 메타데이터 프로필이 의 프로필 목록에 추가됩니다 **[!UICONTROL 메타데이터 프로필]** 페이지를 가리키도록 업데이트하는 중입니다.<br>

   ![메타데이터 프로필 페이지에 추가된 메타데이터 프로필](assets/MetadataProfiles-page.png)

### 메타데이터 프로필 복사 {#copying-a-metadata-profile}

1. 다음에서 **[!UICONTROL 메타데이터 프로필]** 페이지에서 메타데이터 프로필을 선택하여 복사본을 만듭니다.

   ![메타데이터 프로필 복사](assets/metadata-profile-edit-copy-option.png)

1. 클릭 **[!UICONTROL 복사]** 을 클릭합니다.
1. 다음에서 **[!UICONTROL 메타데이터 프로필 복사]** 대화 상자에서 메타데이터 프로필의 새 사본에 대한 제목을 입력합니다.
1. 클릭 **[!UICONTROL 복사]**. The copy of the Metadata Profile appears in the list of profiles in the **[!UICONTROL Metadata Profiles]** page.

   ![메타데이터 프로필 페이지에 추가된 메타데이터 프로필 사본](assets/copy-metadata-profile.png)

### 메타데이터 프로필 삭제 {#deleting-a-metadata-profile}

1. 다음에서 **[!UICONTROL 메타데이터 프로필]** 페이지에서 삭제할 프로필을 선택합니다.

1. 클릭 **[!UICONTROL 메타데이터 프로필 삭제]** 을 클릭합니다.
1. 대화 상자에서 **[!UICONTROL 삭제]** 삭제 작업을 확인합니다. 메타데이터 프로필이 목록에서 삭제됩니다.

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

## 폴더에 대한 메타데이터 스키마 {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] 폴더 속성 페이지에 표시되는 레이아웃 및 메타데이터를 정의하는 자산 폴더에 대한 메타데이터 스키마를 생성할 수 있습니다.

### 폴더 메타데이터 스키마 양식 추가 {#add-a-folder-metadata-schema-form}

폴더 메타데이터 스키마 Forms 편집기를 사용하여 폴더에 대한 메타데이터 스키마를 만들고 편집합니다.

1. 위치 [!DNL Experience Manager] 인터페이스, 이동 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL 폴더 메타데이터 스키마]**.
1. 다음에서 [!UICONTROL 폴더 메타데이터 스키마 Forms] 페이지, 클릭 **[!UICONTROL 만들기]**.
1. 양식 이름을 지정하고 **[!UICONTROL 만들기]**. 새 스키마 양식이에 나열되어 있습니다 [!UICONTROL 스키마 Forms] 페이지를 가리키도록 업데이트하는 중입니다.

### 폴더 메타데이터 스키마 양식 편집 {#edit-folder-metadata-schema-forms}

다음을 포함하는 새로 추가되거나 기존 메타데이터 스키마 양식을 편집할 수 있습니다.

* 탭
* 탭 내의 양식 항목입니다.

이러한 양식 항목을 CRX 저장소의 메타데이터 노드 내에 있는 필드에 매핑/구성할 수 있습니다. 메타데이터 스키마 양식에 새 탭이나 양식 항목을 추가할 수 있습니다.

1. 스키마 Forms 페이지에서 만든 양식을 선택한 다음 **[!UICONTROL 편집]** 도구 모음의 옵션입니다.
1. 폴더 메타데이터 스키마 편집기 페이지에서 `+` 을 눌러 양식에 탭을 추가합니다. 탭의 이름을 바꾸려면 기본 이름을 클릭하고 아래에 새 이름을 지정합니다. **[!UICONTROL 설정]**.

   ![custom_tab](assets/custom_tab.png)

   탭을 더 추가하려면 `+`. 삭제하려면 `X` 탭으로 이동합니다.

1. 활성 탭에서 **[!UICONTROL 양식 작성]** 탭.

   ![add_components](assets/adding_components.png)

   여러 탭을 만드는 경우 특정 탭을 클릭하여 구성 요소를 추가합니다.

1. 구성 요소를 구성하려면 구성 요소를 선택하고 **[!UICONTROL 설정]** 탭.

   필요한 경우 **[!UICONTROL 설정]** 탭.

   ![configure_properties](assets/configure_properties.png)

1. 변경 사항을 저장하려면 을 선택합니다. **[!UICONTROL 저장]** 을 클릭합니다.

#### 양식을 작성할 구성 요소 {#components-to-build-forms}

다음 **[!UICONTROL 양식 작성]** 탭에는 폴더 메타데이터 스키마 양식에서 사용하는 양식 항목이 나열됩니다. 다음 **[!UICONTROL 설정]** 탭에서 선택한 각 항목에 대한 속성이 표시됩니다. **[!UICONTROL 양식 작성]** 탭. 다음은에서 사용할 수 있는 양식 항목 목록입니다. **[!UICONTROL 양식 작성]** 탭:

| 구성 요소 이름 | 설명 |
|---|---|
| [!UICONTROL 섹션 머리글] | 공통 구성 요소 목록의 섹션 머리글을 추가합니다. |
| [!UICONTROL 한 줄 텍스트] | 한 줄 텍스트 속성을 추가합니다. 문자열로 저장됩니다. |
| [!UICONTROL 다중 값 텍스트] | 다중 값 텍스트 속성을 추가합니다. 문자열 배열로 저장됩니다. |
| [!UICONTROL 숫자] | 숫자 구성 요소를 추가합니다. |
| [!UICONTROL 날짜] | 날짜 구성 요소를 추가합니다. |
| [!UICONTROL 드롭다운] | 드롭다운 목록을 추가합니다. |
| [!UICONTROL 표준 태그] | 태그를 추가합니다. |
| [!UICONTROL 숨겨진 필드] | 숨겨진 필드를 추가합니다. 에셋이 저장될 때 POST 매개 변수로 전송됩니다. |

#### 양식 항목 편집 {#editing-form-items}

양식 항목의 속성을 편집하려면 구성 요소를 클릭하고 **[!UICONTROL 설정]** 탭.

**[!UICONTROL 필드 레이블]**: 폴더의 속성 페이지에 표시되는 메타데이터 속성의 이름입니다.

**[!UICONTROL 속성에 매핑]**: 이 속성은 저장되는 CRX 저장소에 있는 폴더 노드의 상대 경로를 지정합니다. 다음으로 시작: &quot;**./**&quot;: 경로가 폴더의 노드 아래에 있음을 나타냅니다.

다음은 이 속성에 유효한 값입니다.

* `./jcr:content/metadata/dc:title`: 폴더의 메타데이터 노드에 있는 값을 속성으로 저장합니다 `dc:title`.

* `./jcr:created`: 폴더의 노드에 JCR 속성을 표시합니다. CRXDE에서 이러한 속성을 구성하는 경우, 보호되므로 Adobe은 해당 속성을 편집 비활성화로 표시하는 것을 권장합니다. 그렇지 않으면 오류 &#39; `Asset(s) failed to modify`에셋의 속성을 저장하면 &#39;이 발생합니다.

구성 요소가 메타데이터 스키마 양식에 제대로 표시되도록 하려면 속성 경로에 공백을 포함하지 마십시오.

**[!UICONTROL JSON 경로]**: 옵션의 키-값 쌍을 지정하는 JSON 파일의 경로를 지정하는 데 사용합니다.

**[!UICONTROL 자리 표시자]**: 이 속성을 사용하여 메타데이터 속성과 관련된 관련 자리 표시자 텍스트를 지정합니다.

**[!UICONTROL 선택 사항]**: 이 속성을 사용하여 목록에서 선택 항목을 지정합니다.

**[!UICONTROL 설명]**: 이 속성을 사용하여 메타데이터 구성 요소에 대한 간단한 설명을 추가합니다.

**[!UICONTROL 클래스]**: 속성이 연결된 오브젝트 클래스.

### 폴더 메타데이터 스키마 양식 삭제 {#delete-folder-metadata-schema-forms}

폴더 메타데이터 스키마 Forms 페이지에서 폴더 메타데이터 스키마 양식을 삭제할 수 있습니다. 양식을 삭제하려면 양식을 선택하고 도구 모음에서 삭제 옵션을 클릭합니다.

![delete_form](assets/delete_form.png)

### 폴더 메타데이터 스키마 할당 {#assign-a-folder-metadata-schema}

폴더 메타데이터 스키마 Forms 페이지에서 또는 폴더를 만들 때 폴더에 폴더 메타데이터 스키마를 할당할 수 있습니다.

폴더에 대한 메타데이터 스키마를 구성하는 경우 스키마 양식에 대한 경로가 `folderMetadataSchema` 아래의 폴더 노드 속성 `./jcr:content`.

#### 폴더 메타데이터 스키마 페이지에서 스키마에 할당 {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. 위치 [!DNL Experience Manager] 인터페이스, 이동 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL 폴더 메타데이터 스키마]**.
1. 폴더 메타데이터 스키마 Forms 페이지에서 폴더에 적용할 스키마 양식을 선택합니다.
1. 도구 모음에서 를 클릭합니다 **[!UICONTROL 폴더에 적용]**.

1. 스키마를 적용할 폴더를 선택한 다음 **[!UICONTROL 적용]**. 폴더에 메타데이터 스키마가 이미 적용된 경우 기존 메타데이터 스키마를 덮어쓰려고 한다는 경고 메시지가 표시됩니다. 클릭 **[!UICONTROL 덮어쓰기]**.
1. 메타데이터 스키마를 적용한 폴더의 메타데이터 속성을 엽니다.

   ![folder_properties](assets/folder_properties.png)

   폴더 메타데이터 필드를 보려면 **[!UICONTROL 폴더 메타데이터]** 탭.

   ![folder_meta_properties](assets/folder_metadata_properties.png)

#### 폴더를 만들 때 스키마 할당 {#assign-a-schema-when-creating-a-folder}

폴더를 만들 때 폴더 메타데이터 스키마를 할당할 수 있습니다. 시스템에 하나 이상의 폴더 메타데이터 스키마가 있는 경우 추가 목록이 **[!UICONTROL 폴더 만들기]** 대화 상자. 원하는 스키마를 선택할 수 있습니다. 기본적으로 스키마는 선택되지 않습니다.

1. 다음에서 [!DNL Experience Manager Assets] 사용자 인터페이스, 클릭 **[!UICONTROL 만들기]** 을 클릭합니다.
1. 폴더의 제목과 이름을 지정합니다.
1. 폴더 메타데이터 스키마 목록에서 원하는 스키마를 선택합니다. 그런 다음 을 클릭합니다. **[!UICONTROL 만들기]**.

   ![select_schema](assets/select_schema.png)

1. 메타데이터 스키마를 적용한 폴더의 메타데이터 속성을 엽니다.
1. 폴더 메타데이터 필드를 보려면 **[!UICONTROL 폴더 메타데이터]** 탭.

### 폴더 메타데이터 스키마 사용 {#use-the-folder-metadata-schema}

Open the properties for a folder configured with a folder metadata schema. A **[!UICONTROL 폴더 메타데이터]** 폴더에 탭이 표시됩니다. [!UICONTROL 속성] 페이지를 가리키도록 업데이트하는 중입니다. To view the folder metadata schema form, select this tab.

다양한 필드에 메타데이터 값을 입력하고 **[!UICONTROL 저장]** 값을 저장합니다. 지정하는 값은 CRX 저장소의 폴더 노드에 저장됩니다.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## 팁 및 제한 사항 {#best-practices-limitations}

* 사용자 지정 네임스페이스에 대한 메타데이터를 가져오려면 먼저 네임스페이스를 등록합니다.
* 속성 선택기는 스키마 편집기 및 검색 양식에 사용되는 속성을 표시합니다. 속성 선택기가 에셋에서 메타데이터 속성을 선택하지 않습니다.
* 로 업그레이드하기 전에 이미 존재하는 메타데이터 프로필이 있을 수 있습니다. [!DNL Experience Manager] 6.5. 업그레이드 후 폴더에 이러한 프로필을 적용하는 경우 [!UICONTROL 속성] 위치: [!UICONTROL 메타데이터 프로필] 탭에서 메타데이터 양식 필드가 표시되지 않습니다. 그러나 새로 만든 메타데이터 프로필을 적용하는 경우 양식 필드가 표시되지만 예상대로 사용할 수 없습니다. 기능은 손실되지 않지만 (사용할 수 없는) 양식 필드를 보려면 기존 메타데이터 프로필을 편집하고 저장합니다.

>[!MORELIKETHIS]
>
>* [메타데이터 개념 및 이해](metadata-concepts.md).
>* [여러 컬렉션의 메타데이터 속성 편집](manage-collections.md#editing-collection-metadata-in-bulk).
>* [Experience Manager Assets에서 메타데이터 가져오기 및 내보내기](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-export.html).
>* [메타데이터, 이미지 및 비디오 처리 프로필](processing-profiles.md).
>* [처리 프로필을 사용하도록 디지털 에셋을 구성하는 우수 사례](/help/assets/organize-assets.md).
>* [XMP 원본에 쓰기](/help/assets/xmp-writeback.md).
