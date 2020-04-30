---
title: 디지털 자산에 워터마크를 추가합니다.
description: 워터마크 기능을 사용하여 디지털 워터마크를 자산에 추가하는 방법을 알아봅니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# 디지털 자산에 워터마크 표시 {#watermarking}

[!DNL Adobe Experience Manager Assets] 디지털 워터마크를 자산에 추가할 수 있으므로 사용자는 에셋의 신뢰성 및 저작권 소유권을 확인할 수 있습니다. [!DNL Experience Manager Assets] 는 PNG 및 JPEG 파일에서 워터마크로 사용할 텍스트를 지원합니다.

자산에 워터마크를 적용하려면 DAM 자산 업데이트 [!UICONTROL 워크플로우에서 워터마크 단계를] 추가하십시오.

1. 사용자 인터페이스에 액세스하고 도구 > 워크플로우 [!DNL Experience Manager] > **[!UICONTROL 모델로]** **[!UICONTROL 이동합니다]** ****.
1. 워크플로우 **[!UICONTROL 모델]** 페이지에서 DAM 자산 **[!UICONTROL 업데이트 워크플로우를 선택하고]** 편집을 **[!UICONTROL 클릭합니다]**.

1. 사이드 패널에서 워터마크 **[!UICONTROL 추가]** 단계를 DAM 자산 [!UICONTROL 업데이트 워크플로우로] 드래그합니다.

   ![워터마크 [!UICONTROL 추가] 단계를 드래그하여 DAM 자산 [!UICONTROL 업데이트 워크플로우에] 추가](assets/add_watermark_step_aem_assets.png)작업2
   *그림:워터마크[!UICONTROL 추가]단계를 드래그하여 DAM 자산[!UICONTROL 업데이트 워크플로우에]추가합니다.*

   >[!NOTE]
   >
   >[ [!UICONTROL 프로세스 축소판] ] 단계 전에 아무 곳에나 [워터마크 추가] [!UICONTROL 단계를] 배치할 수 있습니다.

1. 워터마크 **[!UICONTROL 추가]** 단계를 열어 속성을 표시합니다.
1. 인수 **[!UICONTROL 탭에서]** 텍스트, 글꼴 유형, 크기, 색상, 위치, 방향 등 다양한 필드에 유효한 값을 지정합니다. 변경 내용을 확인하려면 완료를 **[!UICONTROL 클릭합니다]**.

   ![자산의 워터마크 추가 단계에서 인수 제공](assets/arguments_add_watermark_aem_assets.png)

   *그림:의 워터마크 추가 단계에서 인수를[!DNL Assets]제공합니다.*

1. 워터마크 **[!UICONTROL 단계를 사용하여 DAM 자산]** 업데이트 워크플로우를 저장합니다.
1. 사용자 인터페이스에서 샘플 자산을 업로드합니다. [!DNL Assets] 위 단계에서 구성한 위치에 워터마크가 글꼴 크기, 색상 등과 함께 나타납니다.
