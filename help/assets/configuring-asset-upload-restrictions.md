---
title: 자산 업로드 제한 사항 구성
description: '사용자가 업로드할 수 있는 자산 유형 제한 '
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 1%

---


# 자산 업로드 제한 사항 구성 {#configuring-asset-upload-restrictions}

사용자가 업로드할 수 있는 자산 유형을 제한하도록 [!DNL Adobe Experience Manager Assets]을 구성할 수 있습니다. 원치 않는 형식 및 악성 파일을 실수로 업로드하는 것을 방지할 수 있습니다. `Day CQ DAM Asset Upload Restriction` 서비스를 사용하면 사용자가 업로드할 수 있는 파일 유형을 제어할 수 있습니다. 기본적으로 [!DNL Assets]에서는 사용자가 모든 MIME 유형의 자산을 업로드할 수 있습니다. 그러나 특정 MIME 유형의 파일만 업로드하도록 사용자가 제한하도록 서비스를 구성할 수 있습니다.

1. Configuration Manager 웹 콘솔을 엽니다. 액세스 `https://[aem_server]:[port]/system/console/configMgr`.
1. 편집 모드에서 **[!UICONTROL 일 CQ DAM 자산 업로드 제한]** 서비스를 엽니다. 기본적으로 **모든 MIME** 허용 옵션이 선택되어 있어 사용자가 모든 MIME 유형의 파일을 업로드할 수 있습니다.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. 사용자가 특정 MIME 유형의 파일만 업로드하도록 제한하려면 **[!UICONTROL 모든 MIME]** 허용 옵션을 선택 취소하고 정규 표현식을 사용하여 **[!UICONTROL 허용되는 자산 MIME(regex)]** 필드에서 허용되는 MIME 유형을 지정합니다.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. **[!UICONTROL 저장]**&#x200B;을 클릭하여 변경 내용을 저장합니다. 허용되는 MIME 유형에 대해 MIME 문자열을 지정하는 경우 MIME 유형의 자산에 대해 업로드 작업이 실패합니다. 이 필드는 구성된 MIME 문자열과 일치하지 않습니다.
