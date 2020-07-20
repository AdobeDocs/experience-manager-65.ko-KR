---
title: 디지털 자산에 워터마크 추가
description: 워터마크 기능을 사용하여 디지털 워터마크를 자산에 추가하는 방법을 알아봅니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5035d3457187f4d5fe5c2af255a1a886df7291b4
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# 디지털 에셋에 워터마크 표시 {#watermarking}

[!DNL Adobe Experience Manager Assets] 디지털 워터마크를 자산에 추가할 수 있습니다. 이를 통해 사용자는 자산의 인증 및 저작권 소유권을 확인할 수 있습니다. [!DNL Experience Manager Assets] 에서는 PNG 및 JPEG 파일에서 워터마크로 사용할 텍스트를 지원합니다.

자산에 워터마크를 적용하려면 [!UICONTROL DAM 자산 업데이트 워크플로우에서 워터마크 단계를] 추가하십시오.

1. 사용자 [!DNL Experience Manager] 인터페이스에 액세스하고 도구 **[!UICONTROL > 워크플로우]** **[!UICONTROL > 모델]** 으로 **[!UICONTROL 이동합니다]**.
1. 워크플로우 **[!UICONTROL 모델]** 페이지에서 **[!UICONTROL DAM 자산]** 업데이트 워크플로우를 선택하고 **[!UICONTROL 편집을 클릭합니다]**.

1. 사이드 패널에서 워터마크 **[!UICONTROL 추가]** 단계를 [!UICONTROL DAM 자산 업데이트 워크플로우로] 드래그합니다.

   ![워터마크 [!UICONTROL 추가] 단계를 드래그하여 [!UICONTROL DAM 자산 업데이트 워크플로우에] 추가](assets/add_watermark_step_aem_assets.png)2
   *그림: 워터마크[!UICONTROL 추가]단계를 드래그하여[!UICONTROL DAM 자산 업데이트 워크플로우에]추가합니다.*

   >[!NOTE]
   >
   >[ [!UICONTROL 프로세스 축소판] ] 단계 앞 어디에나 [워터마크 [!UICONTROL 추가] ] 단계를배치할 수 있습니다.

1. 워터마크 **[!UICONTROL 추가]** 단계를 열어 속성을 표시합니다.
1. [ **[!UICONTROL 인수]** ] 탭에서 텍스트, 글꼴 유형, 크기, 색상, 위치, 방향 등 다양한 필드에 유효한 값을 지정합니다. 변경 사항을 확인하려면 완료를 **[!UICONTROL 클릭합니다]**.

   ![자산의 워터마크 추가 단계에서 인수 제공](assets/arguments_add_watermark_aem_assets.png)

   *그림: 의 워터마크 추가 단계에서 인수를 제공합니다[!DNL Assets].*

1. 워터마크 단계를 통해 **[!UICONTROL DAM 자산]** 업데이트 워크플로우를 저장합니다.
1. 사용자 인터페이스에서 샘플 자산을 업로드합니다. [!DNL Assets] 워터마크는 위 단계에서 구성한 위치에 글꼴 크기, 색상 등과 함께 나타납니다.

프로그래밍 방식으로 또는 동적 정보로 PDF 문서에 워터마크를 지정하려면 [AEM Document Services](/help/forms/using/overview-aem-document-services.md) 제공을 사용하는 것이 좋습니다.
