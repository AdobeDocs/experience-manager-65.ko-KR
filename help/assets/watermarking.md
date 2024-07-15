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

[!DNL Adobe Experience Manager Assets]을(를) 사용하면 자산의 정품 여부 및 저작권 소유권을 확인하는 데 도움이 되는 디지털 워터마크를 자산에 추가할 수 있습니다. [!DNL Experience Manager Assets]은(는) PNG 및 JPEG 파일에서 워터마크로 사용할 텍스트를 지원합니다.

자산에 워터마크를 적용하려면 [!UICONTROL DAM 자산 업데이트] 워크플로우에서 워터마킹 단계를 추가하십시오.

1. [!DNL Experience Manager] 사용자 인터페이스에 액세스하여 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 모델]**(으)로 이동합니다.
1. **[!UICONTROL 워크플로 모델]** 페이지에서 **[!UICONTROL DAM 자산 업데이트]** 워크플로를 선택하고 **[!UICONTROL 편집]**&#x200B;을 클릭합니다.

1. 사이드 패널에서 **[!UICONTROL 워터마크 추가]** 단계를 [!UICONTROL DAM 자산 업데이트] 워크플로우로 드래그합니다.

   ![[!UICONTROL 워터마크 추가] 단계를 끌어서 [!UICONTROL DAM 자산 업데이트] 워크플로우에 추가](assets/add_watermark_step_aem_assets.png)

   *그림: [!UICONTROL 워터마크 추가] 단계를 끌어서 [!UICONTROL DAM 자산 업데이트] 워크플로우에 추가합니다.*

   >[!NOTE]
   >
   >[!UICONTROL 워터마크 추가] 단계를 [!UICONTROL 프로세스 썸네일] 단계 앞에 배치하십시오.

1. 속성을 표시하려면 **[!UICONTROL 워터마크 추가]** 단계를 여십시오.
1. **[!UICONTROL 인수]** 탭에서 텍스트, 글꼴 유형, 크기, 색상, 위치, 방향 등 다양한 필드에 유효한 값을 지정합니다. 변경 내용을 확인하려면 **[!UICONTROL 완료]**&#x200B;를 클릭하세요.

   ![[!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)의 워터마크 추가 단계에서 인수를 제공합니다.

   *그림: [!DNL Assets]의 워터마크 추가 단계에서 인수를 입력하십시오.*

1. 워터마크 단계로 **[!UICONTROL DAM 자산 업데이트]** 워크플로우를 저장합니다.
1. [!DNL Assets] 사용자 인터페이스에서 샘플 자산을 업로드합니다. 위 단계에서 구성한 위치에 글꼴 크기, 색상 등이 워터마크가 표시됩니다.

PDF 문서에 프로그래밍 방식으로 또는 동적 정보를 사용하여 워터마크를 지정하려면 [Experience Manager 문서 서비스](/help/forms/using/overview-aem-document-services.md) 서비스를 사용하는 것이 좋습니다.

## 팁 및 제한 사항 {#tips-limitations}

* 텍스트 기반 워터마크만 지원됩니다. [!UICONTROL 워터마크 추가 프로세스]를 만들 때 이미지를 업로드할 수 있어도 이미지가 워터마크로 사용되지 않습니다.
* PNG 및 JPEG 파일만 워터마크 지정이 지원됩니다. 다른 에셋 형식은 워터마크가 적용되지 않습니다.
