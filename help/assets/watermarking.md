---
title: 디지털 자산에 워터마크 추가
description: 워터마크 기능을 사용하여 자산에 디지털 워터마크를 추가하는 방법을 알아봅니다.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 4%

---

# 디지털 자산에 워터마크 지정 {#watermarking}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=en) |
| AEM 6.5 | 이 문서 |

[!DNL Adobe Experience Manager Assets] 에셋의 진위 여부와 저작권 소유권을 확인하는 데 도움이 되는 에셋에 디지털 워터마크를 추가할 수 있습니다. [!DNL Experience Manager Assets] 는 PNG 및 JPEG 파일에서 워터마크로 사용할 텍스트를 지원합니다.

에셋에 워터마크를 적용하려면 [!UICONTROL DAM 자산 업데이트] 워크플로입니다.

1. 액세스 [!DNL Experience Manager] 사용자 인터페이스를 사용하여 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 모델]**.
1. 다음에서 **[!UICONTROL 워크플로 모델]** 페이지에서 **[!UICONTROL DAM 자산 업데이트]** 워크플로우 및 클릭 **[!UICONTROL 편집]**.

1. 사이드 패널에서 를 드래그합니다. **[!UICONTROL 워터마크 추가]** 로 이동 [!UICONTROL DAM 자산 업데이트] 워크플로입니다.

   ![드래그 [!UICONTROL 워터마크 추가] 단계에 추가 [!UICONTROL DAM 자산 업데이트] 워크플로우](assets/add_watermark_step_aem_assets.png)

   *그림: 을(를) 드래그합니다. [!UICONTROL 워터마크 추가] 단계에 추가 [!UICONTROL DAM 자산 업데이트] 워크플로입니다.*

   >[!NOTE]
   >
   >배치 [!UICONTROL 워터마크 추가] 다음 이전 아무 곳이나 이동 [!UICONTROL 프로세스 썸네일] 단계.

1. 를 엽니다. **[!UICONTROL 워터마크 추가]** 속성을 표시하는 단계입니다.
1. 다음에서 **[!UICONTROL 인수]** 탭에서 텍스트, 글꼴 유형, 크기, 색상, 위치, 방향 등을 포함하여 다양한 필드에 유효한 값을 지정합니다. 변경 사항을 확인하려면 **[!UICONTROL 완료]**.

   ![의 워터마크 추가 단계에서 인수를 제공합니다. [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *그림: 의 워터마크 추가 단계에서 인수 제공 [!DNL Assets].*

1. 저장 **[!UICONTROL DAM 자산 업데이트]** 워터마크 단계가 있는 워크플로우입니다.
1. 다음에서 [!DNL Assets] 사용자 인터페이스에서 샘플 자산을 업로드합니다. 위 단계에서 구성한 위치에 글꼴 크기, 색상 등이 워터마크가 표시됩니다.

PDF 문서에 프로그래밍 방식으로 또는 동적 정보를 사용하여 워터마크를 지정하려면 [Experience Manager 문서 서비스](/help/forms/using/overview-aem-document-services.md) 제공.

## 팁 및 제한 사항 {#tips-limitations}

* 텍스트 기반 워터마크만 지원됩니다. 이미지를 만들 때 이미지를 업로드할 수 있더라도 이미지는 워터마크로 사용되지 않습니다. [!UICONTROL 워터마크 프로세스 추가].
* PNG 및 JPEG 파일만 워터마크 지정이 지원됩니다. 다른 에셋 형식은 워터마크가 적용되지 않습니다.
