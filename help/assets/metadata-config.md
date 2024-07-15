---
title: 메타데이터 기능 구성 및 관리.
description: 메타데이터 추가 및 관리와 관련된  [!DNL Experience Manager Assets] 기능의 구성 및 관리.
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

# [!DNL Assets]의 메타데이터 기능 구성 및 관리 {#config-metadata}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-profiles.html?lang=en) |
| AEM 6.5 | 이 문서 |

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, and so on, operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets]은(는) 모든 에셋에 대한 메타데이터를 유지합니다. 에셋을 보다 쉽게 분류하고 구성할 수 있으며 특정 에셋을 찾는 사람들에게 도움이 됩니다. 에셋으로 메타데이터를 보관하고 관리할 수 있으므로 에셋의 메타데이터를 기반으로 에셋을 자동으로 구성하고 처리할 수 있습니다. [!DNL Adobe Experience Manager Assets]을(를) 사용하면 관리자가 메타데이터 기능을 구성하고 사용자 지정하여 기본 Adobe 서비스를 수정할 수 있습니다.

## 메타데이터 스키마 편집 {#metadata-schema}

자세한 내용은 [메타데이터 스키마 양식 편집](metadata-schemas.md#edit-metadata-schema-forms)을 참조하십시오.

## [!DNL Experience Manager] 내에서 사용자 지정 네임스페이스 등록 {#registering-a-custom-namespace-within-aem}

[!DNL Experience Manager] 내에서 고유한 네임스페이스를 추가할 수 있습니다. `cq`, `jcr`, `sling` 등 미리 정의된 네임스페이스가 있는 것처럼 저장소 메타데이터 및 XML 처리를 위한 네임스페이스를 가질 수 있습니다.

1. 노드 유형 관리 페이지 `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`에 액세스합니다.
1. 네임스페이스 관리 페이지에 액세스하려면 페이지 맨 위에서 **[!UICONTROL 네임스페이스]**&#x200B;를 클릭하십시오.
1. 네임스페이스를 추가하려면 페이지 하단의 **[!UICONTROL 새로 만들기]**&#x200B;를 클릭하세요.
1. XML 네임스페이스 규칙에서 사용자 지정 네임스페이스를 지정합니다. URI 형식으로 ID를 지정하고 ID에 연결된 접두사를 지정합니다. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

## 벌크 메타데이터 업데이트에 대한 제한 구성 {#bulk-metadata-update-limit}

DOS(서비스 거부) 같은 상황을 방지하기 위해 [!DNL Enterprise Manager]은(는) Sling 요청에서 지원되는 매개 변수의 수를 제한합니다. 한 번에 많은 에셋의 메타데이터를 업데이트할 때 한도에 도달할 수 있으며 더 많은 에셋에 대한 메타데이터는 업데이트되지 않습니다. Enterprise Manager는 로그에 다음 경고를 생성합니다.

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

제한을 변경하려면 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**&#x200B;에 액세스하고 **[!UICONTROL Apache Sling POST 매개 변수 처리]** OSGi 구성에서 **[!UICONTROL 최대 요청 매개 변수]**&#x200B;의 값을 변경하십시오.

## 메타데이터 프로필 {#metadata-profiles}

메타데이터 프로필을 사용하면 폴더 내의 에셋에 기본 메타데이터를 적용할 수 있습니다. 메타데이터 프로필을 만들어 폴더에 적용합니다. 나중에 폴더에 업로드하는 모든 에셋은 메타데이터 프로필에서 구성한 기본 메타데이터를 상속합니다.

### 메타데이터 프로필 추가 {#adding-a-metadata-profile}

1. **[!UICONTROL 도구]** > **[!UICONTROL Assets]** > **[!UICONTROL 메타데이터 프로필]**(으)로 이동한 다음 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.
1. 프로필의 제목(예: `Sample Metadata`)을 입력하고 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 메타데이터 프로필의 [!UICONTROL 양식 편집]이(가) 표시됩니다.

   ![메타데이터 양식 편집](assets/metadata-edit-form.png)

1. 구성 요소를 클릭하고 **[!UICONTROL 설정]** 탭에서 해당 속성을 구성합니다. 예를 들어 **[!UICONTROL 설명]** 구성 요소를 클릭하고 속성을 편집합니다.

   ![메타데이터 프로필에서 구성 요소 설정](assets/metadata-profile-component-setting.png)

   **[!UICONTROL 설명]** 구성 요소에 대한 다음 속성을 편집합니다.

   * **[!UICONTROL 필드 레이블]**: 메타데이터 속성의 표시 이름입니다. 사용자 참조용으로만 사용됩니다.

   * **[!UICONTROL 속성에 매핑]**: 이 속성의 값은 저장소에 저장된 에셋 노드에 대한 상대 경로 또는 이름을 제공합니다. 경로는 자산의 노드 아래에 있으므로 값은 항상 `./`로 시작해야 합니다.

   ![메타데이터 프로필의 속성에 매핑](assets/metadata-profile-setting-map-property.png)

   **[!UICONTROL 속성에 매핑]**&#x200B;에 지정한 값이 자산의 메타데이터 노드 아래에 속성으로 저장됩니다. 예를 들어 `./jcr:content/metadata/dc:desc`을(를) **[!UICONTROL 속성에 매핑]**&#x200B;의 이름으로 지정하는 경우 [!DNL Assets]은(는) 자산의 메타데이터 노드에 값 `dc:desc`을(를) 저장합니다. Adobe은 메타데이터 스키마의 특정 속성에 필드를 한 개만 매핑할 것을 권장합니다. 그렇지 않으면 속성에 매핑된 최신 추가 필드가 시스템에 의해 선택됩니다.

   * **[!UICONTROL 기본값]**: 메타데이터 구성 요소의 기본값을 추가하려면 이 속성을 사용합니다. 예를 들어 &quot;My description&quot;을 지정하면 이 값은 자산의 메타데이터 노드에서 `dc:desc` 속성에 할당됩니다.

   ![메타데이터 프로필에 기본 설명 설정](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >`/jcr:content/metadata` 노드에 없는 새 메타데이터 속성에 기본값을 추가해도 자산의 [!UICONTROL 속성] 페이지에 기본적으로 속성과 해당 값이 표시되지 않습니다. 자산의 [!UICONTROL 속성] 페이지에서 새 속성을 보려면 해당 스키마 양식을 수정하십시오.

1. (선택 사항) **[!UICONTROL 양식 작성]** 탭에서 [!UICONTROL 양식 편집]에 구성 요소를 더 추가하고 **[!UICONTROL 설정]** 탭에서 해당 속성을 구성합니다. **[!UICONTROL 양식 작성]** 탭에서 다음 속성을 사용할 수 있습니다.

| 구성 요소 | 속성 |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL 섹션 머리글] | 필드 레이블, <br> 설명 |
| [!UICONTROL 한 줄 텍스트] | 필드 레이블, <br> 속성에 매핑, <br> 기본값 |
| [!UICONTROL 다중 값 텍스트] | 필드 레이블, <br> 속성에 매핑, <br> 기본값 |
| [!UICONTROL 숫자] | 필드 레이블, <br> 속성에 매핑, <br> 기본값 |
| [!UICONTROL 날짜] | 필드 레이블, <br> 속성에 매핑, <br> 기본값 |
| [!UICONTROL 표준 태그] | 필드 레이블, <br> 속성에 매핑, <br> 기본값, <br> 설명 |

1. **[!UICONTROL 완료]**&#x200B;를 클릭합니다. 메타데이터 프로필이 **[!UICONTROL 메타데이터 프로필]** 페이지의 프로필 목록에 추가됩니다.<br>

   ![메타데이터 프로필 페이지에 추가된 메타데이터 프로필](assets/MetadataProfiles-page.png)

### 메타데이터 프로필 복사 {#copying-a-metadata-profile}

1. **[!UICONTROL 메타데이터 프로필]** 페이지에서 복사본을 만들 메타데이터 프로필을 선택하십시오.

   ![메타데이터 프로필 복사](assets/metadata-profile-edit-copy-option.png)

1. 도구 모음에서 **[!UICONTROL 복사]**&#x200B;를 클릭합니다.
1. **[!UICONTROL 메타데이터 프로필 복사]** 대화 상자에서 메타데이터 프로필의 새 복사본 제목을 입력합니다.
1. **[!UICONTROL 복사]**&#x200B;를 클릭합니다. The copy of the Metadata Profile appears in the list of profiles in the **[!UICONTROL Metadata Profiles]** page.

   ![메타데이터 프로필 페이지에 메타데이터 프로필 복사본이 추가되었습니다](assets/copy-metadata-profile.png)

### 메타데이터 프로필 삭제 {#deleting-a-metadata-profile}

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

## 폴더에 대한 메타데이터 스키마 {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets]을(를) 사용하면 폴더 속성 페이지에 표시되는 레이아웃 및 메타데이터를 정의하는 자산 폴더에 대한 메타데이터 스키마를 만들 수 있습니다.

### 폴더 메타데이터 스키마 양식 추가 {#add-a-folder-metadata-schema-form}

폴더 메타데이터 스키마 Forms 편집기를 사용하여 폴더에 대한 메타데이터 스키마를 만들고 편집합니다.

1. [!DNL Experience Manager] 인터페이스에서 **[!UICONTROL 도구]** > **[!UICONTROL Assets]** > **[!UICONTROL 폴더 메타데이터 스키마]**(으)로 이동합니다.
1. [!UICONTROL 폴더 메타데이터 스키마 Forms] 페이지에서 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.
1. 양식 이름을 지정하고 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 새 스키마 양식이 [!UICONTROL 스키마 Forms] 페이지에 나열됩니다.

### 폴더 메타데이터 스키마 양식 편집 {#edit-folder-metadata-schema-forms}

다음을 포함하는 새로 추가되거나 기존 메타데이터 스키마 양식을 편집할 수 있습니다.

* 탭
* 탭 내의 양식 항목입니다.

이러한 양식 항목을 CRX 저장소의 메타데이터 노드 내에 있는 필드에 매핑/구성할 수 있습니다. 메타데이터 스키마 양식에 새 탭이나 양식 항목을 추가할 수 있습니다.

1. 스키마 Forms 페이지에서 만든 양식을 선택한 다음 도구 모음에서 **[!UICONTROL 편집]** 옵션을 선택합니다.
1. 폴더 메타데이터 스키마 편집기 페이지에서 `+`을(를) 클릭하여 양식에 탭을 추가합니다. 탭의 이름을 바꾸려면 기본 이름을 클릭하고 **[!UICONTROL 설정]**&#x200B;에서 새 이름을 지정하십시오.

   ![custom_tab](assets/custom_tab.png)

   탭을 더 추가하려면 `+`을(를) 클릭합니다. 삭제하려면 탭에서 `X`을(를) 클릭합니다.

1. 활성 탭에서 **[!UICONTROL 양식 작성]** 탭에서 구성 요소를 하나 이상 추가합니다.

   ![add_components](assets/adding_components.png)

   여러 탭을 만드는 경우 특정 탭을 클릭하여 구성 요소를 추가합니다.

1. 구성 요소를 구성하려면 구성 요소를 선택하고 **[!UICONTROL 설정]** 탭에서 속성을 수정하십시오.

   필요한 경우 **[!UICONTROL 설정]** 탭에서 구성 요소를 삭제하십시오.

   ![configure_properties](assets/configure_properties.png)

1. 변경 사항을 저장하려면 도구 모음에서 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

#### 양식을 작성할 구성 요소 {#components-to-build-forms}

**[!UICONTROL 양식 작성]** 탭에는 폴더 메타데이터 스키마 양식에 사용하는 양식 항목이 나열됩니다. **[!UICONTROL 설정]** 탭에는 **[!UICONTROL 양식 작성]** 탭에서 선택한 각 항목의 특성이 표시됩니다. 다음은 **[!UICONTROL 양식 작성]** 탭에서 사용할 수 있는 양식 항목 목록입니다.

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

양식 항목의 속성을 편집하려면 구성 요소를 클릭하고 **[!UICONTROL 설정]** 탭에서 다음 속성의 전체 또는 하위 집합을 편집합니다.

**[!UICONTROL 필드 레이블]**: 폴더의 속성 페이지에 표시되는 메타데이터 속성의 이름입니다.

**[!UICONTROL 속성에 매핑]**: 이 속성은 저장되는 CRX 저장소의 폴더 노드의 상대 경로를 지정합니다. &quot;**&quot;(으)로 시작합니다./**&quot;은(는) 경로가 폴더의 노드 아래에 있음을 나타냅니다.

다음은 이 속성에 유효한 값입니다.

* `./jcr:content/metadata/dc:title`: 폴더의 메타데이터 노드에 있는 값을 속성 `dc:title`(으)로 저장합니다.

* `./jcr:created`: 폴더의 노드에 JCR 속성을 표시합니다. CRXDE에서 이러한 속성을 구성하는 경우, 보호되므로 Adobe은 해당 속성을 편집 비활성화로 표시하는 것을 권장합니다. 그렇지 않으면 자산의 속성을 저장할 때 오류 &#39;`Asset(s) failed to modify`&#39;이(가) 발생합니다.

구성 요소가 메타데이터 스키마 양식에 제대로 표시되도록 하려면 속성 경로에 공백을 포함하지 마십시오.

**[!UICONTROL JSON 경로]**: 옵션에 키-값 쌍을 지정하는 JSON 파일의 경로를 지정하는 데 사용합니다.

**[!UICONTROL 자리 표시자]**: 이 속성을 사용하여 메타데이터 속성과 관련된 관련 자리 표시자 텍스트를 지정합니다.

**[!UICONTROL 선택 항목]**: 목록에서 선택 항목을 지정하려면 이 속성을 사용하십시오.

**[!UICONTROL 설명]**: 메타데이터 구성 요소에 대한 간단한 설명을 추가하려면 이 속성을 사용합니다.

**[!UICONTROL 클래스]**: 속성이 연결된 개체 클래스입니다.

### 폴더 메타데이터 스키마 양식 삭제 {#delete-folder-metadata-schema-forms}

폴더 메타데이터 스키마 Forms 페이지에서 폴더 메타데이터 스키마 양식을 삭제할 수 있습니다. 양식을 삭제하려면 양식을 선택하고 도구 모음에서 삭제 옵션을 클릭합니다.

![delete_form](assets/delete_form.png)

### 폴더 메타데이터 스키마 할당 {#assign-a-folder-metadata-schema}

폴더 메타데이터 스키마 Forms 페이지에서 또는 폴더를 만들 때 폴더에 폴더 메타데이터 스키마를 할당할 수 있습니다.

폴더에 대한 메타데이터 스키마를 구성하는 경우 스키마 양식의 경로가 `./jcr:content` 아래 폴더 노드의 `folderMetadataSchema` 속성에 저장됩니다.

#### 폴더 메타데이터 스키마 페이지에서 스키마에 할당 {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. [!DNL Experience Manager] 인터페이스에서 **[!UICONTROL 도구]** > **[!UICONTROL Assets]** > **[!UICONTROL 폴더 메타데이터 스키마]**(으)로 이동합니다.
1. 폴더 메타데이터 스키마 Forms 페이지에서 폴더에 적용할 스키마 양식을 선택합니다.
1. 도구 모음에서 **[!UICONTROL 폴더에 적용]**&#x200B;을 클릭합니다.

1. 스키마를 적용할 폴더를 선택한 다음 **[!UICONTROL 적용]**&#x200B;을 클릭합니다. 폴더에 메타데이터 스키마가 이미 적용된 경우 기존 메타데이터 스키마를 덮어쓰려고 한다는 경고 메시지가 표시됩니다. **[!UICONTROL 덮어쓰기]**&#x200B;를 클릭합니다.
1. 메타데이터 스키마를 적용한 폴더의 메타데이터 속성을 엽니다.

   ![folder_properties](assets/folder_properties.png)

   폴더 메타데이터 필드를 보려면 **[!UICONTROL 폴더 메타데이터]** 탭을 클릭하십시오.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### 폴더를 만들 때 스키마 할당 {#assign-a-schema-when-creating-a-folder}

폴더를 만들 때 폴더 메타데이터 스키마를 할당할 수 있습니다. 시스템에 하나 이상의 폴더 메타데이터 스키마가 있는 경우 **[!UICONTROL 폴더 만들기]** 대화 상자에 추가 목록이 표시됩니다. 원하는 스키마를 선택할 수 있습니다. 기본적으로 스키마는 선택되지 않습니다.

1. [!DNL Experience Manager Assets] 사용자 인터페이스의 도구 모음에서 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.
1. 폴더의 제목과 이름을 지정합니다.
1. 폴더 메타데이터 스키마 목록에서 원하는 스키마를 선택합니다. 그런 다음 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

   ![select_schema](assets/select_schema.png)

1. 메타데이터 스키마를 적용한 폴더의 메타데이터 속성을 엽니다.
1. 폴더 메타데이터 필드를 보려면 **[!UICONTROL 폴더 메타데이터]** 탭을 클릭하십시오.

### 폴더 메타데이터 스키마 사용 {#use-the-folder-metadata-schema}

Open the properties for a folder configured with a folder metadata schema. **[!UICONTROL 폴더 메타데이터]** 탭이 폴더 [!UICONTROL 속성] 페이지에 표시됩니다. To view the folder metadata schema form, select this tab.

다양한 필드에 메타데이터 값을 입력하고 **[!UICONTROL 저장]**&#x200B;을 클릭하여 값을 저장합니다. 지정하는 값은 CRX 저장소의 폴더 노드에 저장됩니다.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## 팁 및 제한 사항 {#best-practices-limitations}

* 사용자 지정 네임스페이스에 대한 메타데이터를 가져오려면 먼저 네임스페이스를 등록합니다.
* 속성 선택기는 스키마 편집기 및 검색 양식에 사용되는 속성을 표시합니다. 속성 선택기가 에셋에서 메타데이터 속성을 선택하지 않습니다.
* [!DNL Experience Manager] 6.5로 업그레이드하기 전에 이미 존재하는 메타데이터 프로필이 있을 수 있습니다. 업그레이드 후 [!UICONTROL 메타데이터 프로필] 탭의 [!UICONTROL 속성] 폴더에 이러한 프로필을 적용하면 메타데이터 양식 필드가 표시되지 않습니다. 그러나 새로 만든 메타데이터 프로필을 적용하는 경우 양식 필드가 표시되지만 예상대로 사용할 수 없습니다. 기능은 손실되지 않지만 (사용할 수 없는) 양식 필드를 보려면 기존 메타데이터 프로필을 편집하고 저장합니다.

>[!MORELIKETHIS]
>
>* [메타데이터 개념 및 이해](metadata-concepts.md).
>* [여러 컬렉션의 메타데이터 속성을 편집합니다](manage-collections.md#editing-collection-metadata-in-bulk).
>* [Experience Manager Assets에서 메타데이터 가져오기 및 내보내기](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-export.html).
>* [메타데이터, 이미지 및 비디오를 처리할 프로필](processing-profiles.md).
>* [처리 프로필을 사용하도록 디지털 자산을 구성하는 모범 사례](/help/assets/organize-assets.md).
>* [XMP 원본에 쓰기](/help/assets/xmp-writeback.md).
