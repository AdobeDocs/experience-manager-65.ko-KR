---
title: 자산 업로드 제한 사항 구성
description: 사용자가 업로드할 수 있는 에셋(파일) 유형 제한
contentOwner: AG
role: Developer, Admin, Architect
feature: Asset Management,Upload
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 20%

---

# 자산 업로드 제한 사항 구성 {#configuring-asset-upload-restrictions}

다음을 구성할 수 있습니다. [!DNL Adobe Experience Manager Assets] 사용자가 업로드할 수 있는 에셋 유형을 제한합니다. 원하지 않는 형식 및 악성 파일이 실수로 업로드되는 것을 방지하는 데 도움이 됩니다. 다음 `Day CQ DAM Asset Upload Restriction` 서비스를 사용하면 사용자가 업로드할 수 있는 파일 유형을 제어할 수 있습니다. 기본적으로, [!DNL Assets] 사용자가 모든 MIME 유형의 자산을 업로드할 수 있습니다. 그러나 사용자가 특정 MIME 유형의 파일만 업로드하도록 제한하도록 서비스를 구성할 수 있습니다.

1. Configuration Manager 웹 콘솔을 엽니다. 액세스 `https://[aem_server]:[port]/system/console/configMgr`.
1. 를 엽니다. **[!UICONTROL 일별 CQ DAM 자산 업로드 제한]** 서비스가 편집 모드에 있습니다. 기본적으로 **모든 MIME 허용** 사용자가 모든 MIME 유형의 파일을 업로드할 수 있는 옵션이 선택되어 있습니다.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. 사용자가 특정 MIME 유형의 파일만 업로드하도록 제한하려면 **[!UICONTROL 모든 MIME 허용]** 옵션이에 허용된 MIME 유형을 지정하고 **[!UICONTROL 허용된 자산 MIME(정규 표현식)]** 정규 표현식을 사용하는 필드입니다.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. 클릭 **[!UICONTROL 저장]** 변경 내용을 저장합니다. If you specify MIME-strings for allowed MIME types, the upload operation fails for any asset with MIME type that doesn’t match the configured MIME strings in these fields.
