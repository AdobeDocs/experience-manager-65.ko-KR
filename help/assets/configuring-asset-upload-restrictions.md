---
title: 자산 업로드 제한 구성
description: '사용자가 업로드할 수 있는 자산 유형 제한 '
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# 자산 업로드 제한 구성 {#configuring-asset-upload-restrictions}

AEM(Adobe Experience Manager) 자산을 구성하여 사용자가 업로드할 수 있는 자산 유형(파일)을 제한할 수 있습니다. 이 기능을 사용하면 사용자가 원하지 않는 형식으로 자산을 업로드하거나 악의적인 파일을 업로드할 가능성을 제거할 수 있습니다. 이 `Day CQ DAM Asset Upload Restriction` 서비스를 사용하면 사용자가 업로드할 수 있는 파일 유형을 제어할 수 있습니다. 기본적으로 AEM Assets에서는 사용자가 모든 MIME 유형의 자산을 업로드할 수 있습니다. 그러나 특정 MIME 유형의 파일만 업로드하도록 사용자가 제한하도록 서비스를 구성할 수 있습니다.

1. Configuration Manager 웹 콘솔을 엽니다. 액세스 `https://[aem_server]:[port]/system/console/configMgr`.
1. 편집 모드에서 **[!UICONTROL CQ DAM 자산 업로드 제한]** 서비스를 엽니다. 기본적으로 모든 MIME **형식 허용** 옵션이 선택되어 있으므로 사용자가 모든 MIME 유형의 파일을 업로드할 수 있습니다.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. 사용자가 특정 MIME 유형의 파일만 업로드하도록 제한하려면 [모든 MIME **[!UICONTROL 허용]** ] 옵션을 선택 취소하고 정규식을 사용하여 허용된 자산 MIME(regex) **** 필드에 허용되는 MIME 형식을 지정합니다.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. 저장을 클릭/탭하여 **** 변경 내용을 저장합니다. 허용되는 MIME 유형에 대해 MIME 문자열을 지정하는 경우 MIME 유형의 모든 자산에 대해 업로드 작업이 실패합니다. MIME 형식은 이러한 필드에 구성된 MIME 문자열과 일치하지 않습니다.
