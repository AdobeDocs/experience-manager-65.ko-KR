---
title: 자산 업로드 제한 사항 구성
description: 사용자가 업로드할 수 있는 에셋(파일) 유형 제한
contentOwner: AG
role: Developer, Admin
feature: Asset Management,Upload
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: cda65036-5305-4f01-89da-9b3506ae8c50
    internal-label: Administration
subfeature_v2:
  - id: f1dc0c96-022d-4003-afbe-47bd40173c4a
    internal-label: Upload assets
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 9%
---
# 자산 업로드 제한 사항 구성 {#configuring-asset-upload-restrictions}

사용자가 업로드할 수 있는 에셋 유형을 제한하도록 [!DNL Adobe Experience Manager Assets]을(를) 구성할 수 있습니다. 원하지 않는 형식 및 악성 파일이 실수로 업로드되는 것을 방지하는 데 도움이 됩니다. `Day CQ DAM Asset Upload Restriction` 서비스를 사용하면 사용자가 업로드할 수 있는 파일 형식을 제어할 수 있습니다. 기본적으로 [!DNL Assets]에서는 사용자가 모든 MIME 유형의 자산을 업로드할 수 있습니다. 그러나 사용자가 특정 MIME 유형의 파일만 업로드하도록 제한하도록 서비스를 구성할 수 있습니다.

1. Configuration Manager 웹 콘솔을 엽니다. `https://[aem_server]:[port]/system/console/configMgr`에 액세스합니다.
1. 편집 모드에서 **[!UICONTROL 일 CQ DAM 자산 업로드 제한]** 서비스를 엽니다. 기본적으로 사용자가 모든 MIME 유형의 파일을 업로드할 수 있는 **모든 MIME 허용** 옵션이 선택되어 있습니다.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. 사용자가 특정 MIME 유형의 파일만 업로드하도록 제한하려면 **[!UICONTROL 모든 MIME 허용]** 옵션의 선택을 취소하고 정규식을 사용하여 **[!UICONTROL 허용된 자산 MIME(정규 표현식)]** 필드에 허용된 MIME 유형을 지정하십시오.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. **[!UICONTROL 저장]**&#x200B;을 클릭하여 변경 내용을 저장합니다. 허용된 MIME 유형에 MIME 문자열을 지정하는 경우 이러한 필드에 구성된 MIME 문자열과 일치하지 않는 MIME 유형의 자산에 대해 업로드 작업이 실패합니다.
