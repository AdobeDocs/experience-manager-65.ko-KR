---
title: 디지털 자산에 워터마크 추가
description: 워터마크 기능을 사용하여 자산에 디지털 워터마크를 추가하는 방법을 알아봅니다.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 2%

---

# 디지털 자산에 워터마크 지정 {#watermarking}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=en) |
| AEM 6.5 | 이 문서 |

[!DNL Adobe Experience Manager Assets] 에서는 사용자가 자산의 정품 여부 및 저작권 소유권을 확인하는 데 도움이 되는 자산에 디지털 워터마크를 추가할 수 있습니다. [!DNL Experience Manager Assets] 에서는 PNG 및 JPEG 파일에서 워터마크로 사용할 텍스트를 지원합니다.

자산에 워터마크를 적용하려면 [!UICONTROL DAM 자산 업데이트] 워크플로우.

1. 액세스 권한 [!DNL Experience Manager] 사용자 인터페이스를 사용하여 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로우]** > **[!UICONTROL 모델]**.
1. 에서 **[!UICONTROL 워크플로우 모델]** 페이지에서 을 선택합니다 **[!UICONTROL DAM 자산 업데이트]** 워크플로우 및 **[!UICONTROL 편집]**.

1. 사이드 패널에서 **[!UICONTROL 워터마크 추가]** 다음으로 이동 [!UICONTROL DAM 자산 업데이트] 워크플로우.

   ![을(를) 드래그합니다. [!UICONTROL 워터마크 추가] 단계 및 추가 [!UICONTROL DAM 자산 업데이트] 워크플로우](assets/add_watermark_step_aem_assets.png)

   *그림: 을(를) 드래그합니다. [!UICONTROL 워터마크 추가] 단계 및 추가 [!UICONTROL DAM 자산 업데이트] 워크플로우.*

   >[!NOTE]
   >
   >배치 [!UICONTROL 워터마크 추가] 이전 단계 [!UICONTROL 프로세스 축소판] 단계.

1. 를 엽니다. **[!UICONTROL 워터마크 추가]** 속성을 표시하는 단계입니다.
1. 에서 **[!UICONTROL 인수]** 탭에서 텍스트, 글꼴 유형, 크기, 색상, 위치, 방향 등 다양한 필드에 유효한 값을 지정합니다. 변경 사항을 확인하려면 **[!UICONTROL 완료]**.

   ![의 워터마크 추가 단계에서 인수를 제공합니다. [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *그림: 의 워터마크 추가 단계에서 인수를 제공합니다. [!DNL Assets].*

1. 를 저장합니다 **[!UICONTROL DAM 자산 업데이트]** 워터마크 단계를 사용한 워크플로우입니다.
1. 에서 [!DNL Assets] 사용자 인터페이스에서 샘플 자산을 업로드합니다. 워터마크는 위의 단계에서 구성한 위치에 글꼴 크기, 색상 등으로 나타납니다.

프로그래밍 방식으로 또는 동적 정보로 PDF 문서를 워터마킹하려면 다음을 사용하는 것이 좋습니다 [Experience Manager 문서 서비스](/help/forms/using/overview-aem-document-services.md) 제공

## 팁 및 제한 사항 {#tips-limitations}

* 텍스트 기반 워터마크만 지원됩니다. 이미지를 만들 때 이미지를 업로드할 수 있어도 이미지가 워터마크로 사용되지 않습니다 [!UICONTROL 워터마크 프로세스 추가].
* 워터마크 지정 기능은 PNG 및 JPEG 파일만 지원합니다. 다른 자산 형식은 워터마크가 되지 않습니다.
