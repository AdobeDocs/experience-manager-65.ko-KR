---
title: 디지털 자산의 메타데이터를 관리할 수 있습니다 [!DNL Adobe Experience Manager].
description: 메타데이터의 유형과 메타데이터를 기반으로 에셋을 자동으로 구성하고 [!DNL Adobe Experience Manager Assets] helps manage metadata for assets to allow easier categorization and organization of assets. [!DNL Experience Manager] 처리하는 방법을 살펴볼 수 있습니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: d070f5dca569dfb90d3034b74c2940fd68d8ceab
workflow-type: tm+mt
source-wordcount: '2421'
ht-degree: 2%

---


# 디지털 자산의 메타데이터 관리 {#managing-metadata-for-digital-assets}

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] 모든 에셋에 대한 메타데이터를 유지합니다. 또한 보다 쉽게 에셋을 분류하고 구성할 수 있으며 특정 에셋을 찾는 사용자에게 도움이 됩니다. 메타데이터 관리는 업로드된 파일에서 메타데이터를 추출하는 기능 [!DNL Experience Manager Assets]을 통해 크리에이티브 워크플로우와 통합됩니다. 자산을 사용하여 메타데이터를 유지 및 관리할 수 있으므로 메타데이터를 기반으로 자산을 자동으로 구성하고 처리할 수 있습니다.

## 메타데이터 및 원본 {#how-to-edit-or-add-metadata}

메타데이터는 검색할 수 있는 자산에 대한 추가 정보입니다. 자산에 추가되고 자산을 업로드할 때 [!DNL Experience Manager] 가 처리됩니다. 기존 메타데이터를 편집하고 기존 필드에 새 메타데이터 속성을 추가할 수 있습니다. 조직에는 제어 및 안정적인 메타데이터 어휘가 필요합니다. 따라서 새로운 메타데이터 속성을 On-Demand로 추가할 수 [!DNL Experience Manager Assets] 없습니다. 관리자와 개발자만 메타데이터를 포함하는 새 속성이나 필드를 추가할 수 있습니다. 사용자는 메타데이터로 기존 필드를 채울 수 있습니다.

다음 방법을 사용하여 디지털 자산에 메타데이터를 추가할 수 있습니다.

* 먼저 에셋을 만드는 기본 애플리케이션에서 메타데이터를 추가합니다. 예를 들어 [Acrobat은 PDF 파일에 일부 메타데이터를](https://helpx.adobe.com/acrobat/using/pdf-properties-metadata.html) 추가하거나 카메라에 기본 메타데이터를 추가합니다. 자산을 생성할 때 기본 애플리케이션 자체에 메타데이터를 추가할 수 있습니다. 예를 들어 Adobe Lightroom에 IPTC 메타데이터를 [추가할 수 있습니다](https://helpx.adobe.com/lightroom-classic/help/metadata-basics-actions.html).

* 자산을 업로드하기 전에 자산 [!DNL Experience Manager]을 만들거나 기타 메타데이터 편집 응용 프로그램을 사용하는 기본 응용 프로그램을 사용하여 메타데이터를 편집하고 수정할 수 있습니다. 자산을 Experience Manager에 업로드하면 메타데이터가 처리됩니다. 예를 들어, 에서 메타데이터 [를 사용하여 [!DNL Adobe Bridge]](https://helpx.adobe.com/bridge/user-guide.html/bridge/using/metadata-adobe-bridge.ug.html) 작업하는 방법을 [보고 [!DNL Bridge CC]](https://exchange.adobe.com/creativecloud.details.20009.aem-tags-panel-for-bridge-cc.html) 의 [!DNL Adobe Exchange]태그 패널을참조하십시오.

* 에서 [!DNL Experience Manager Assets]속성 [!UICONTROL 페이지] 에서 자산의 메타데이터를 수동으로 추가하거나 편집할 수 있습니다.

* 에셋을 DAM에 업로드할 때 [메타데이터 프로필](/help/assets/metadata-config.md#metadata-profiles) 기능을 활용하여 메타데이터를 자동으로 추가할 [!DNL Experience Manager Assets] 수 있습니다.

## 메타데이터 추가 또는 편집 [!DNL Experience Manager Assets] {#add-edit-metadata}

사용자 인터페이스에서 자산의 메타데이터를 편집하려면 다음 단계를 [!DNL Assets] 수행합니다.

1. 다음 중 하나를 수행하십시오.

   * 인터페이스에서 자산을 선택하고 도구 모음에서 [!DNL Assets] 속성 **** 보기 를 클릭합니다.
   * 자산 축소판에서 속성 **[!UICONTROL 보기 빠른 작업을]** 선택합니다.
   * 자산 페이지의 도구 모음에서 **[!UICONTROL 속성]** 정보 ![보기 아이콘](assets/do-not-localize/info-circle-icon.png) 을 클릭합니다.

   자산 페이지에는 모든 자산의 메타데이터가 표시됩니다. 에셋이 업로드될 때 메타데이터가 추출됩니다(인제스트됨) [!DNL Experience Manager].

   ![자산의 속성을 선택하여 해당 메타데이터를 봅니다.](assets/asset-metadata.png)

   *그림:자산 속성 페이지에서 메타데이터를 편집하거나 [!UICONTROL 추가합니다] .*

1. 필요에 따라 다양한 탭에서 메타데이터를 편집하고 완료되면 도구 모음에서 **[!UICONTROL 저장]** 을 클릭하여 변경 사항을 저장합니다. 닫기 **[!UICONTROL 를]** 클릭하여 [!DNL Assets] 웹 인터페이스로 돌아갑니다.

   >[!NOTE]
   >
   >텍스트 필드가 비어 있으면 기존 메타데이터 세트가 없습니다. 필드에 값을 입력하고 저장하여 해당 메타데이터 속성을 추가할 수 있습니다.

자산의 메타데이터에 대한 모든 변경 사항은 XMP 데이터의 일부로서 원본 바이너리에 다시 기록됩니다. 메타데이터 다시 쓰기 워크플로우는 원본 바이너리에 메타데이터를 추가합니다. 기존 속성(예:)에 대한 변경 사항 `dc:title`이 덮어쓰기되고 새 속성(예: 사용자 정의 속성 포함)이 스키마에 `cq:tags`추가됩니다.

XMP의 쓰기 되돌리는 [기술 요구 사항에 설명된 플랫폼 및 파일 포맷에 대해 지원되고 활성화됩니다.](/help/sites-deploying/technical-requirements.md)

## 여러 자산의 메타데이터 속성 편집 {#editing-metadata-properties-of-multiple-assets}

[!DNL Adobe Enterprise Manager Assets] 여러 자산의 메타데이터를 동시에 편집할 수 있으므로 일반적인 메타데이터 변경 사항을 자산에 일괄 전파할 수 있습니다. 여러 컬렉션의 메타데이터를 일괄 편집할 수도 있습니다. 속성 페이지를 사용하여 여러 자산 또는 컬렉션에 대한 메타데이터 변경을 수행합니다.

* 메타데이터 속성을 일반 값으로 변경
* 태그 추가 또는 수정

메타데이터 속성 추가, 수정, 삭제 등 메타데이터 속성 페이지를 사용자 정의하려면 [스키마 편집기를 사용합니다](metadata-config.md#folder-metadata-schema).

>[!NOTE]
>
>벌크 편집 방법은 폴더 또는 컬렉션에서 사용할 수 있는 자산에 대해 작동합니다. 여러 폴더에서 사용할 수 있거나 일반적인 기준과 일치하는 자산의 경우 검색 후 메타데이터를 [일괄 업데이트할 수 있습니다](search-assets.md#metadataupdates).

1. 사용자 인터페이스에서 편집할 자산의 위치로 이동합니다. [!DNL Assets]
1. 공통 속성을 편집할 자산을 선택합니다.
1. 도구 모음에서 **[!UICONTROL 속성]** 을 클릭하여 선택한 자산에 대한 속성 페이지를 엽니다.

   >[!NOTE]
   >
   >여러 자산을 선택하면 자산에 대해 가장 낮은 공통 상위 양식이 선택됩니다. 즉, 속성 페이지에는 모든 개별 자산의 속성 페이지에서 공통인 메타데이터 필드만 표시됩니다.

1. 다양한 탭에서 선택한 자산에 대한 메타데이터 속성을 수정합니다.
1. 특정 자산에 대한 메타데이터 편집기를 보려면 목록에서 나머지 자산을 선택 취소합니다. 메타데이터 편집기 필드는 특정 자산에 대한 메타데이터로 채워집니다.

   >[!NOTE]
   >
   >* 속성 페이지에서 자산을 선택 취소하여 자산 목록에서 제거할 수 있습니다. 자산 목록에는 기본적으로 모든 자산이 선택되어 있습니다. 목록에서 제거하는 자산에 대한 메타데이터는 업데이트되지 않습니다.
   >* 자산 목록 맨 위에서 **[!UICONTROL 제목]** 근처의 확인란을 선택하여 자산 선택과 목록 지우기 간을 전환합니다.


1. 자산에 대해 다른 메타데이터 스키마를 선택하려면 도구 모음 **[!UICONTROL 에서]** 설정을 클릭하고 원하는 스키마를 선택합니다.
1. 변경 사항을 저장합니다.
1. 여러 값이 들어 있는 필드에 기존 메타데이터와 함께 새 메타데이터를 추가하려면 추가 모드 **[!UICONTROL 를 선택합니다]**. 이 옵션을 선택하지 않으면 새 메타데이터가 필드에 있는 기존 메타데이터를 대체합니다. 제출을 **[!UICONTROL 클릭합니다]**.

   >[!CAUTION]
   >
   >단일 값 필드의 경우 추가 모드를 선택하더라도 새 메타데이터는 필드의 기존 값에 추가되지 **[!UICONTROL 않습니다]**.

## 메타데이터 가져오기 {#import-metadata}

[!DNL Assets] CSV 파일을 사용하여 자산 메타데이터를 일괄적으로 가져올 수 있습니다. CSV 파일을 가져와 최근에 업로드한 자산이나 기존 자산에 대해 일괄 업데이트를 수행할 수 있습니다. 타사 시스템에서 CSV 형식으로 에셋 메타데이터를 일괄적으로 인제스트할 수도 있습니다.

메타데이터 가져오기는 비동기 방식이므로 시스템 성능을 방해하지 않습니다. 워크플로우 플래그를 선택하는 경우 XMP writeback 작업 때문에 여러 자산에 대한 메타데이터를 동시에 업데이트할 경우 리소스가 많이 소모될 수 있습니다. 다른 사용자의 성능에 영향을 주지 않도록 서버 사용량 감소 시 이러한 가져오기를 계획합니다.

>[!NOTE]
>
>사용자 정의 네임스페이스에 대한 메타데이터를 가져오려면 먼저 네임스페이스를 등록합니다.

1. 사용자 [!DNL Assets] 인터페이스로 이동하고 도구 모음에서 **[!UICONTROL 만들기를]** 클릭합니다.
1. 메뉴에서 **[!UICONTROL 메타데이터를 선택합니다]**.
1. 메타데이터 **[!UICONTROL 가져오기]** 페이지에서 파일 **[!UICONTROL 선택을 클릭합니다]**. 메타데이터가 있는 CSV 파일을 선택합니다.
1. 다음 매개 변수를 지정합니다. 메타데이터 가져오기-sample-file.csv의 샘플 CSV 파일을 [참조하십시오](/help/assets/assets/metadata-import-sample-file.csv).

   | 메타데이터 가져오기 매개 변수 | 설명 |
   |:---|:---|
   | [!UICONTROL 배치 크기] | 메타데이터를 가져올 일괄 처리 내의 자산 수입니다. 기본값은 50입니다. 최대값은 100입니다. |
   | [!UICONTROL 필드 분리 기호] | 기본값은 `,` (쉼표)입니다. 다른 문자를 지정할 수 있습니다. |
   | [!UICONTROL 다중 값 구분 기호] | 메타데이터 값의 구분 기호. Default value is `|`. |
   | [!UICONTROL 워크플로우 실행] | 기본적으로 False입니다. 설정 `true` 및 기본 론처 설정이 [!UICONTROL DAM 메타데이터 쓰기] 돌아가기 작업 과정(이진 XMP 데이터에 메타데이터를 쓰는 작업 과정)에 적용됩니다. 실행 워크플로우를 활성화하면 시스템이 느려집니다. |
   | [!UICONTROL 자산 경로 열 이름] | 자산이 있는 CSV 파일의 열 이름을 정의합니다. |

1. Click **[!UICONTROL Import]** from the toolbar. 메타데이터를 가져오면 알림 받은 [!UICONTROL 편지함에 알림이] 표시됩니다.

1. 올바른 가져오기를 확인하려면 자산의 [!UICONTROL 속성] 페이지로 이동하고 필드의 값을 확인합니다.

메타데이터를 가져올 때 날짜 및 타임스탬프를 추가하려면 날짜 및 시간에 대한 `YYYY-MM-DDThh:mm:ss.fff-00:00` 형식을 사용하십시오. 날짜와 시간은 서로 구분되며, `T`24시간 형식 `hh` 의 시간, 나노초 `fff` `-00:00` , 표준 시간대 오프셋입니다. 예를 들어 2020년 3월 26일 `2020-03-26T11:26:00.000-07:00` 오전 11시 26분 00.000초 PST 시간입니다.

>[!CAUTION]
>
>날짜 형식이 일치하지 않으면 날짜 값 `YYYY-MM-DDThh:mm:ss.fff-00:00`이 설정되지 않습니다. 내보낸 메타데이터 CSV 파일의 날짜 형식이 형식입니다 `YYYY-MM-DDThh:mm:ss-00:00`. 이 값을 가져오려는 경우, 에서 나타내는 나노초 값을 추가하여 허용 가능한 형식으로 변환하십시오 `fff`.

## Export metadata {#export-metadata}

여러 자산에 대한 메타데이터를 CSV 형식으로 내보낼 수 있습니다. 메타데이터는 비동기적으로 내보내지며 시스템의 성능에 영향을 주지 않습니다. 메타데이터를 내보내려면 자산 노드 [!DNL Experience Manager] `jcr:content/metadata` 및 해당 하위 노드의 속성을 통과하여 메타데이터 속성을 CSV 파일로 내보냅니다.

메타데이터를 일괄적으로 내보내는 데 사용되는 몇 가지 사용 사례는 다음과 같습니다.

* 자산을 마이그레이션할 때 타사 시스템에서 메타데이터를 가져옵니다.
* 다양한 프로젝트 팀과 에셋 메타데이터를 공유할 수 있습니다.
* 규정 준수를 위해 메타데이터를 테스트하거나 감사할 수 있습니다.
* 메타데이터를 별도로 지역화할 수 있습니다.

1. 메타데이터를 내보낼 에셋이 포함된 에셋 폴더를 선택합니다. 도구 모음에서 메타데이터 **[!UICONTROL 내보내기를 선택합니다]**.

1. 메타데이터 [!UICONTROL 내보내기] 대화 상자에서 CSV 파일의 이름을 지정합니다. 하위 폴더의 에셋에 대한 메타데이터를 내보내려면 하위 폴더에 **[!UICONTROL 에셋 포함을 선택합니다]**.

   ![모든 에셋의 메타데이터를](assets/export_metadata_page.png "폴더에 내보내기 위한 인터페이스 및 옵션인터페이스 및 옵션을 사용하여 폴더에 있는 모든 에셋의 메타데이터를 내보낼 수 있습니다")

1. 원하는 옵션을 선택합니다. 파일 이름과 필요한 경우 날짜를 입력합니다.

1. 내보낼 **[!UICONTROL 속성]** 필드에서 모든 속성을 내보낼 것인지 특정 속성을 내보낼 것인지 지정합니다. 내보낼 선택적 속성을 선택하는 경우 원하는 속성을 추가합니다.

1. 도구 모음에서 내보내기를 **[!UICONTROL 클릭합니다]**. 메타데이터가 내보내졌음을 확인하는 메시지가 표시됩니다. 메시지를 닫습니다.

1. 내보내기 작업에 대한 받은 편지함 알림을 엽니다. 작업을 선택하고 도구 모음에서 **[!UICONTROL 열기]** 를 클릭합니다. 메타데이터가 포함된 CSV 파일을 다운로드하려면 도구 모음에서 **[!UICONTROL CSV 다운로드]** 를 클릭합니다. 닫기를 **[!UICONTROL 클릭합니다]**.

   ![일괄적으로 내보낸 메타데이터가 포함된 CSV 파일을 다운로드하는 대화 상자](assets/csv_download.png)

   *그림:일괄적으로 내보낸 메타데이터가 포함된 CSV 파일을 다운로드하는 대화 상자*

## 컬렉션의 메타데이터 편집 {#collections-metadata}

자세한 내용은 컬렉션 메타데이터 [보기 및 편집](/help/assets/manage-collections.md#view-edit-collection-metadata) 및 여러 컬렉션의 메타데이터 [를 일괄](/help/assets/manage-collections.md#editing-collection-metadata-in-bulk)편집을 참조하십시오.

## 폴더에 메타데이터 프로필 적용 {#applying-a-metadata-profile-to-folders}

<!-- TBD: Review this overview.
-->

메타데이터 프로필을 폴더에 할당하면 모든 하위 폴더는 해당 상위 폴더에서 프로필을 자동으로 상속받습니다. 즉, 하나의 메타데이터 프로필만 폴더에 할당할 수 있습니다. 따라서 에셋을 업로드, 저장, 사용 및 보관하는 폴더 구조를 주의 깊게 고려합니다.

폴더에 다른 메타데이터 프로필을 할당하면 새 프로필이 이전 프로필을 덮어씁니다. 이전의 기존 폴더 자산은 변경되지 않습니다. 새 프로필은 나중에 폴더에 추가되는 자산에 적용됩니다.

프로필이 할당된 폴더가 사용자 인터페이스에 카드 이름에 나타나는 프로필 이름으로 표시됩니다.

![카드 보기에는 폴더에 적용된 메타데이터 프로필이 표시됩니다.](assets/metadata-profile-card-view-display.png)

특정 폴더 또는 모든 자산에 전역으로 메타데이터 프로필을 적용할 수 있습니다.

나중에 변경한 기존 메타데이터 프로필이 이미 있는 폴더에서 자산을 재처리할 수 있습니다. [폴더의 자산에 대한 처리 프로필을 편집한 후 재처리](processing-profiles.md#reprocessing-assets)를 참조하십시오.

[ **[!UICONTROL 도구] 메뉴 내에서 또는 폴더에 있는 경우 [속성]에서]** 메타데이터 프로필을 폴더에 적용할 수 **[!UICONTROL 있습니다]**. 이 섹션에서는 두 가지 방법으로 폴더에 메타데이터 프로필을 적용하는 방법을 설명합니다.

프로필이 이미 할당된 폴더는 폴더 이름 바로 아래에 프로필 이름이 표시되어 표시됩니다.

나중에 변경한 기존 비디오 프로필이 이미 있는 폴더의 에셋을 다시 처리할 수 있습니다. [폴더의 자산에 대한 처리 프로필을 편집한 후 재처리](processing-profiles.md#reprocessing-assets)를 참조하십시오.

### 프로필 사용자 인터페이스의 폴더에 메타데이터 프로필  적용 {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

단계에 따라 메타데이터 프로필을 적용합니다.

1. 로고를 클릭하고 [!DNL Experience Manager] 도구 **[!UICONTROL > 자산]** > **[!UICONTROL 메타데이터 프로필]** 으로 이동합니다 ****.
1. 폴더 또는 여러 폴더에 적용할 메타데이터 프로필을 선택합니다.
1. 폴더에 메타데이터 **[!UICONTROL 프로필 적용을]** 클릭하고 새로 업로드한 자산을 받기 위해 사용할 폴더 또는 폴더를 선택한 다음 완료를 **[!UICONTROL 클릭합니다]**. 프로필이 이미 할당된 폴더는 폴더 이름 바로 아래에 프로필 이름이 표시되어 표시됩니다.

### 속성의 폴더에 메타데이터 프로필 [!UICONTROL 적용] {#applying-metadata-profiles-to-folders-from-properties}

1. 왼쪽 레일에서 **[!UICONTROL 자산을]** 클릭한 다음 메타데이터 프로필을 적용할 폴더를 탐색합니다.
1. 폴더에서 확인 표시를 클릭하여 선택한 다음 속성 **[!UICONTROL 을 클릭합니다]**.

1. 메타데이터 **[!UICONTROL 프로필]** 탭을 선택하고 팝업 메뉴에서 프로필을 선택한 다음 저장을 **[!UICONTROL 클릭합니다]**.

프로필이 이미 할당된 폴더는 폴더 이름 바로 아래에 프로필 이름이 표시되어 표시됩니다.

<!-- TBD: Commenting as the topic in metadata-config.md is incomplete.

### Apply metadata profile globally {#metadata-profile-global}

For details, see [configuration to apply metadata profile globally](/help/assets/metadata-config.md#apply-a-metadata-profile-globally). -->

### 폴더에서 메타데이터 프로필 제거 {#removing-a-metadata-profile-from-folders}

폴더에서 메타데이터 프로필을 제거하면 모든 하위 폴더는 해당 상위 폴더에서 프로필 제거를 자동으로 상속합니다. 그러나 폴더 내에서 발생한 파일 처리는 그대로 유지됩니다.

폴더 내의 **[!UICONTROL 도구]** 메뉴 또는 **[!UICONTROL 속성]** 폴더에서 메타데이터프로필을 제거할 수 있습니다.

#### 프로필 사용자 인터페이스를 통해 폴더에서 메타데이터 프로필 제거 {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. 로고를 클릭하고 [!DNL Experience Manager] 도구 **[!UICONTROL > 자산]** > **[!UICONTROL 메타데이터 프로필]** 으로 이동합니다 ****.
1. 폴더 또는 여러 폴더에서 제거할 메타데이터 프로필을 선택합니다.
1. 폴더에서 **[!UICONTROL 메타데이터 프로필 제거를]** 클릭하고 프로필을 제거할 폴더 또는 여러 폴더를 선택한 다음 완료를 **[!UICONTROL 클릭합니다]**.

   이름이 더 이상 폴더 이름 아래에 나타나지 않으므로 메타데이터 프로필이 더 이상 폴더에 적용되지 않도록 확인할 수 있습니다.

#### 속성을 통해 폴더에서 메타데이터 프로필 제거 {#removing-metadata-profiles-from-folders-via-properties}

1. 로고를 클릭하고 [!DNL Experience Manager] 자산 **** 으로 이동한 다음 메타데이터 프로필을 제거할 폴더로 이동합니다.
1. 폴더에서 확인 표시를 클릭하여 선택한 다음 속성 **[!UICONTROL 을 클릭합니다]**.
1. 메타데이터 **[!UICONTROL 프로필]** 탭을 선택하고 드롭다운 메뉴에서 **[!UICONTROL 없음]** 을 선택하고 **[!UICONTROL 저장을]**&#x200B;클릭합니다. 프로필이 이미 할당된 폴더는 폴더 이름 바로 아래에 프로필 이름이 표시되어 표시됩니다.

## 팁 및 제한 사항 {#best-practices-limitations}

* 사용자 인터페이스를 통한 메타데이터 업데이트는 네임스페이스의 메타데이터 속성을 `dc` 변경합니다. HTTP API를 통해 수행된 모든 업데이트는 네임스페이스의 메타데이터 속성을 `jcr` 변경합니다. HTTP API를 사용하여 메타데이터를 업데이트하는 [방법을 참조하십시오](/help/assets/mac-api-assets.md#update-asset-metadata).

* 에셋 메타데이터를 가져오기 위한 CSV 파일은 매우 구체적인 형식입니다. 노력과 시간을 절약하고 의도하지 않은 오류를 방지하려면 내보낸 CSV 파일의 형식을 사용하여 CSV를 만들기 시작할 수 있습니다.

* CSV 파일을 사용하여 메타데이터를 가져오는 경우 필요한 날짜 형식이 됩니다 `YYYY-MM-DDThh:mm:ss.fff-00:00`. 다른 형식을 사용하는 경우 날짜 값이 설정되지 않습니다. 내보낸 메타데이터 CSV 파일의 날짜 형식이 형식입니다 `YYYY-MM-DDThh:mm:ss-00:00`. 이 값을 가져오려는 경우, 에서 나타내는 나노초 값을 추가하여 허용 가능한 형식으로 변환하십시오 `fff`.

>[!MORELIKETHIS]
>
>* [메타데이터 개념 및 이해](metadata-concepts.md).
>* [여러 컬렉션의 메타데이터 속성 편집](manage-collections.md#editing-collection-metadata-in-bulk)
>* [Experience Manager 에셋에서 메타데이터 가져오기 및 내보내기](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)


<!-- TBD: Try filling the available information in these topics to the extent possible. As and when complete, publish the sections live.

## Where to find metadata of an asset or folder {#find-metadata}

What all methods to access asset Properties. More Details option in column view. Select asset and click Properties. Keyboard shortcut `p`. What else?

## Understand metadata handling in Experience Manager {#metadata-possibilities-with-aem}

Describe the journey of an assets' metadata. What all happens to metadata when an asset is added to Experience Manager.

## Add metadata to your digital assets {#add-metadata}

* To begin with, assets come with some metadata. The applications that create digital assets add some metadata to the assets created. Before uploading an asset to Experience Manager, you can edit and modify metadata using either the native application used to create an asset or using some other metadata editing application. When you upload an asset to Experience Manager, the metadata is processed.

* Link to PS, ID, AI, PDF, etc. metadata-related help articles.

* Link to XMP writeback.

* Manually add (or edit) metadata in AEM in Properties page.

* Metadata profiles

* Any workflows related to metadata?

* Advanced topic: Add, edit, modify, process and writeback metadata of subassets.

## Metadata of assets, folders, and collections {#metadata-of-assets-folders-collections}

Similarities and differences between metadata of asset and folder. 

Link to metadata handling of collections.

## Modify metadata of an asset, folder, or collection {#modify-metadata}

* While creating assets: Native application.

* Before ingesting assets: Metadata editors

* After ingesting assets: Properties of an asset, folder, collection, etc.

* Any supported programmatic method to bulk edit metadata directly in JCR?

## Modify metadata in bulk {#modify-metadata-in-bulk}

[!DNL Adobe Enterprise Manager Assets] lets you edit the metadata of multiple assets simultaneously so you can quickly propagate common metadata changes to assets in bulk. You can also edit the metadata for multiple collections in bulk.

Use the properties page to perform metadata changes on multiple assets or collections:

* Change metadata properties to a common value

* Add or modify tags

To customize the metadata properties page, including adding, modifying, deleting metadata properties, use the schema editor.

>[!NOTE]
>
>The bulk editing methods work for assets available in a folder or a collection. For the assets that are available across folders or match a common criteria, it is possible to [bulk update the metadata after searching](search-assets.md#metadataupdates).

1. In the [!DNL Assets] user interface, navigate to the location of the assets you want to edit.
1. Select the assets for which you want to edit common properties.
1. From the toolbar, click **[!UICONTROL Properties]** to open the properties page for the selected assets.

   >[!NOTE]
   >
   >When you select multiple assets, the lowest common parent form is selected for the assets. In other words, the properties page only displays metadata fields that are common across the properties pages of all the individual assets.

1. Modify the metadata properties for selected assets under the various tabs.
1. To view the metadata editor for a specific asset, deselect the remaining assets in the list. The metadata editor fields are populated with the metadata for the particular asset.

   >[!NOTE]
   >
   >* In the Properties page, you can remove assets from the asset list by deselecting them. The asset list has all the assets selected by default. The metadata for assets that you remove from the list is not updated.
   >
   >* At the top of assets list, select the check box near **[!UICONTROL Title]** to toggle between selecting the assets and clearing the list.

1. To select a different metadata schema for the assets, click **[!UICONTROL Settings]** from the toolbar, and select the desired schema.
1. Save the changes.
1. To append the new metadata with the existing metadata in fields that contain multiple values, select **[!UICONTROL Append mode]**. If you do not select this option, the new metadata replaces the existing metadata in the fields. click **[!UICONTROL Submit]**.

   >[!CAUTION]
   >
   >For single-value fields, the new metadata is not appended to the existing value in the field even if you select **[!UICONTROL Append mode]**.

-->
