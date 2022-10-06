---
title: 에셋 업로드 제한 사항 구성
description: 사용자가 업로드할 수 있는 자산 유형 제한
contentOwner: AG
role: Developer, Admin, Architect
feature: Asset Management,Upload
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 20%

---

# 에셋 업로드 제한 사항 구성 {#configuring-asset-upload-restrictions}

다음을 구성할 수 있습니다 [!DNL Adobe Experience Manager Assets] 를 추가하여 사용자가 업로드할 수 있는 자산 유형을 제한합니다. 원치 않는 포맷과 악성 파일이 우발적으로 업로드되는 것을 방지할 수 있습니다. 다음 `Day CQ DAM Asset Upload Restriction` 서비스를 사용하면 사용자가 업로드할 수 있는 파일 유형을 제어할 수 있습니다. 기본적으로 [!DNL Assets] 모든 MIME 유형의 자산을 업로드할 수 있습니다. 그러나 특정 MIME 유형의 파일만 업로드하도록 사용자를 제한하도록 서비스를 구성할 수 있습니다.

1. 구성 관리자 웹 콘솔을 엽니다. 액세스 `https://[aem_server]:[port]/system/console/configMgr`.
1. 를 엽니다. **[!UICONTROL 일 CQ DAM 자산 업로드 제한]** 서비스를 편집 모드로 전환합니다. 기본적으로 **모든 MIME 허용** 옵션을 선택하면 사용자가 모든 MIME 유형의 파일을 업로드할 수 있습니다.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. 사용자가 특정 MIME 유형의 파일만 업로드하도록 제한하려면 **[!UICONTROL 모든 MIME 허용]** 옵션을 선택하고 허용되는 MIME 유형을 **[!UICONTROL 허용되는 자산 MIME(regex)]** 정규 표현식을 사용하는 필드.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. 클릭 **[!UICONTROL 저장]** 변경 사항을 저장하려면 을 클릭합니다. If you specify MIME-strings for allowed MIME types, the upload operation fails for any asset with MIME type that doesn’t match the configured MIME strings in these fields.
