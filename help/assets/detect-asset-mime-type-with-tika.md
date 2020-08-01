---
title: Apache Tika를 사용하여 MIME 유형의 자산 탐지
description: Apache Tika를 활성화하여 파일 확장자 대신 업로드 작업 중에 콘텐츠 스트림에서 MIME 유형의 자산을 [!DNL Experience Manager Assets] 검색할 수 있습니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 5%

---


# MIME 유형의 자산 감지 [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

일반적으로 파일 확장자에서 업로드하는 자산의 MIME 유형을 [!DNL Adobe Experience Manager Assets] 감지합니다.

자산 [!DNL Apache Tika] 을 업로드하는 데 사용하는 경우 파일 확장자 대신 업로드 작업 중에 콘텐츠 스트림에서 해당 MIME 형식을 [!DNL Assets] 감지합니다.

이 기능은 기본적으로 비활성화됩니다. 이 기능을 활성화하려면 **[!UICONTROL Configuration Manager에서]** 일 CQ DAM MIME 유형 [!UICONTROL 서비스를]구성합니다.

>[!NOTE]
>
>라이브러리를 사용하는 MIME 유형 [!DNL Apache Tika] 감지는 리소스를 많이 사용하는 작업입니다.

1. Configuration Manager 웹 콘솔을 열려면 액세스합니다 `https://[aem_server]:[port]/system/console/configMgr`.

1. 서비스 목록에서 **[!UICONTROL Day CQ DAM MIME 유형 서비스]** 를 찾아 **[!UICONTROL 편집을 클릭합니다]**.

1. 파일 **[!UICONTROL 확장자를 무시하고 업로드한 자산의 구문 분석을 활성화하여 MIME 형식을 결정하려면 [콘텐츠에서]** MIME 감지] 옵션을 선택합니다. 기본적으로 이 옵션은 선택되지 않습니다.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Click **[!UICONTROL Save]** to save the changes.
