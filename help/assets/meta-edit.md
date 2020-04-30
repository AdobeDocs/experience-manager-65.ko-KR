---
title: 메타데이터를 편집하거나 추가하는 방법
description: '[!DNL Adobe Experience Manager Assets]의 자산 메타데이터에 대해 자산 메타데이터를 편집할 수 있는 다양한 방법을 알아봅니다.'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# 메타데이터를 편집하거나 추가하는 방법 {#how-to-edit-or-add-metadata}

메타데이터는 검색할 수 있는 자산에 대한 추가 정보입니다. 이미지를 업로드할 때 자동으로 압축이 해제됩니다. 기존 메타데이터를 편집하거나 새 메타데이터 속성을 기존 필드에 추가할 수 있습니다(예: 메타데이터 필드가 비어 있는 경우).

조직에는 제어되고 안정적인 메타데이터 어휘가 필요하므로 새로운 메타데이터 속성을 임시로 추가하는 것은 허용되지 [!DNL Experience Manager Assets] 않습니다. 작성자가 에셋에 대한 새 메타데이터 필드를 추가할 수는 없지만 개발자는 이를 수행할 수 있습니다. 자산에 [](meta-edit.md#editing-metadata-schema)대한 새 메타데이터 속성 만들기를 참조하십시오.

## 자산에 대한 메타데이터 편집 {#editing-metadata-for-an-asset}

메타데이터를 편집하려면:

1. 다음 중 하나를 수행하십시오.

   * 인터페이스에서 자산을 선택하고 도구 [!DNL Assets] 모음에서 속성 **** 보기를 클릭합니다.
   * 자산 축소판에서 속성 보기 **[!UICONTROL 빠른 작업을]** 선택합니다.
   * 자산 페이지의 도구 모음에서 **[!UICONTROL 속성]** 보기 ![변경_](assets/chlimage_1-168.png) 1-168을클릭합니다.
   자산 페이지에는 자산의 모든 메타데이터가 표시됩니다. 자산이 Experience Manager에 업로드(인제스트)되면 메타데이터가 추출됩니다.

   ![자산 속성을 선택하여 메타데이터 보기](assets/asset-metadata.png)

   *그림:자산 속성 페이지에서 메타데이터를 편집하거나 추가합니다.*

1. 필요에 따라 다양한 탭에서 메타데이터를 편집하고 완료되면 도구 모음에서 **[!UICONTROL 저장을]** 클릭하여 변경 내용을 저장합니다. 닫기를 **[!UICONTROL 클릭하여]** 자산 웹 인터페이스로 돌아갑니다.

   >[!NOTE]
   >
   >텍스트 필드가 비어 있으면 기존 메타데이터 세트가 없습니다. 필드에 값을 입력하고 저장하여 메타데이터 속성을 추가할 수 있습니다.

자산의 메타데이터에 대한 변경 사항은 XMP 데이터의 일부로 원본 바이너리에 다시 기록됩니다. 이 작업은 Experience Manager 메타데이터 다시 쓰기 워크플로우를 통해 수행됩니다. 기존 속성(예: `dc:title``cq:tags`)에 대한 변경 사항이 덮어쓰기되고 새로 생성된 속성(예: 사용자 정의 속성 포함)이 스키마와 함께 추가됩니다.

XMP 다시 쓰기는 [기술 요구 사항에 설명된 플랫폼 및 파일 포맷에 대해 지원되고 활성화됩니다.](/help/sites-deploying/technical-requirements.md)

## 메타데이터 스키마 편집 {#editing-metadata-schema}

메타데이터 스키마 편집 방법에 대한 자세한 내용은 메타데이터 스키마 [양식](metadata-schemas.md#edit-metadata-schema-forms)편집을 참조하십시오.

## Experience Manager 내에서 사용자 지정 네임스페이스 등록 {#registering-a-custom-namespace-within-aem}

Adobe Experience Manager 내에서 고유한 네임스페이스를 추가할 수 있습니다. cq, jcr 및 sling과 같은 사전 정의된 네임스페이스가 있는 것처럼 저장소 메타데이터 및 xml 처리를 위한 네임스페이스를 가질 수 있습니다.

1. 노드 유형 관리 페이지로 `https:[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`이동합니다.
1. 페이지 **[!UICONTROL 상단에서]** 네임스페이스를 클릭합니다. 네임스페이스 관리 페이지가 창에 표시됩니다.

1. 네임스페이스를 추가하려면 **[!UICONTROL 하단에서 [새로]** 만들기]를 클릭합니다.
1. XML 네임스페이스 규칙에서 사용자 정의 네임스페이스를 지정합니다(URI 형식으로 id를 지정하고 ID에 연결된 접두사를 지정합니다). 그런 다음 [저장]을 **[!UICONTROL 클릭합니다]**.
