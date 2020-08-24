---
title: 메타데이터를 편집하거나 추가하는 방법
description: 자산 메타데이터를 편집할 수 있는 다양한 방법 [!DNL Adobe Experience Manager Assets] 으로 자산 메타데이터에 대해 알아봅니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: fc14ccc834c9a41b67eb8cf17dd8b34f5dff2406
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 2%

---


# 메타데이터를 편집하거나 추가하는 방법 {#how-to-edit-or-add-metadata}

메타데이터는 검색할 수 있는 자산에 대한 추가 정보입니다. 이미지를 업로드할 때 자동으로 압축이 해제됩니다. 메타데이터 필드가 비어 있는 경우와 같이 기존 메타데이터를 편집하거나 기존 필드에 새 메타데이터 속성을 추가할 수 있습니다.

조직에는 제어 및 안정적인 메타데이터 어휘가 필요합니다. 따라서 새로운 메타데이터 속성을 On-Demand로 추가할 수 [!DNL Experience Manager Assets] 없습니다. 작성자가 아닌 개발자는 에셋에 대한 새 메타데이터 필드를 추가할 수 있습니다. 자산에 대한 메타데이터 [속성 만들기를 참조하십시오](meta-edit.md#editing-metadata-schema).

## 자산에 대한 메타데이터 편집 {#editing-metadata-for-an-asset}

메타데이터를 편집하려면 다음 단계를 따르십시오.

1. 다음 중 하나를 수행하십시오.

   * 인터페이스에서 자산을 선택하고 도구 모음에서 [!DNL Assets] 속성 **** 보기 를 클릭합니다.
   * 자산 축소판에서 속성 **[!UICONTROL 보기 빠른 작업을]** 선택합니다.
   * 자산 페이지의 도구 모음에서 **[!UICONTROL 속성]** 정보 ![보기 아이콘](assets/do-not-localize/info-circle-icon.png) 을 클릭합니다.

   자산 페이지에는 모든 자산의 메타데이터가 표시됩니다. 에셋이 업로드될 때 메타데이터가 추출됩니다(인제스트됨) [!DNL Experience Manager].

   ![자산의 속성을 선택하여 해당 메타데이터를 봅니다.](assets/asset-metadata.png)

   *그림:자산 속성 페이지에서 메타데이터를 편집하거나[!UICONTROL 추가합니다].*

1. 필요에 따라 다양한 탭에서 메타데이터를 편집하고 완료되면 도구 모음에서 **[!UICONTROL 저장]** 을 클릭하여 변경 사항을 저장합니다. 닫기 **[!UICONTROL 를]** 클릭하여 [!DNL Assets] 웹 인터페이스로 돌아갑니다.

   >[!NOTE]
   >
   >텍스트 필드가 비어 있으면 기존 메타데이터 세트가 없습니다. 필드에 값을 입력하고 저장하여 해당 메타데이터 속성을 추가할 수 있습니다.

자산의 메타데이터에 대한 모든 변경 사항은 XMP 데이터의 일부로서 원본 바이너리에 다시 기록됩니다. 메타데이터 다시 쓰기 워크플로우는 원본 바이너리에 메타데이터를 추가합니다. 기존 속성(예:)에 대한 변경 사항 `dc:title`이 덮어쓰기되고 새 속성(예: 사용자 정의 속성 포함)이 스키마에 `cq:tags`추가됩니다.

XMP의 쓰기 되돌리는 [기술 요구 사항에 설명된 플랫폼 및 파일 포맷에 대해 지원되고 활성화됩니다.](/help/sites-deploying/technical-requirements.md)

## 메타데이터 스키마 편집 {#editing-metadata-schema}

자세한 내용은 메타데이터 스키마 양식 [편집을 참조하십시오](metadata-schemas.md#edit-metadata-schema-forms).

## 사용자 정의 네임스페이스 등록 [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

고유한 네임스페이스를 안에 추가할 수 있습니다 [!DNL Experience Manager]. 저장소 메타데이터 및 XML 처리와 같은 사전 정의된 네임스페이스 `cq``jcr`와 `sling`마찬가지로 저장소 메타데이터 및 XML 처리를 위한 네임스페이스를 가질 수 있습니다.

1. 노드 유형 관리 페이지에 액세스합니다 `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. 네임스페이스 관리 페이지에 액세스하려면 페이지 **[!UICONTROL 상단의 네임스페이스]** 를 클릭합니다.
1. 네임스페이스를 추가하려면 페이지 **[!UICONTROL 아래쪽에서]** [새로 만들기]를 클릭합니다.
1. XML 네임스페이스 규칙에서 사용자 지정 네임스페이스를 지정합니다. URI 형식으로 ID를 지정하고 ID에 연결된 접두사를 지정합니다. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

## 팁 및 제한 사항 {#best-practices-limitations}

* Touch-UI를 통한 메타데이터 업데이트는 네임스페이스의 메타데이터 속성을 `dc` 변경합니다. HTTP API를 통해 수행된 모든 업데이트는 네임스페이스의 메타데이터 속성을 `jcr` 변경합니다. HTTP API를 사용하여 메타데이터를 업데이트하는 [방법을 참조하십시오](/help/assets/mac-api-assets.md#update-asset-metadata).

>[!MORELIKETHIS]
>
>* [자산에서의 메타데이터 및 그 필요 정보](metadata.md)
>* [XMP 메타데이터](xmp.md)
>* [메타데이터 스키마 참조](meta-ref.md)

