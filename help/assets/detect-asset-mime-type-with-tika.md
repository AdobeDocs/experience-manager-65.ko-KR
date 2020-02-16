---
title: Apache Tika를 사용하여 MIME 유형의 자산 감지
description: Apache Tika를 활성화하면 AEM 자산이 파일 확장자 대신 업로드 작업 중에 콘텐츠 스트림에서 자산의 MIME 유형을 검색할 수 있습니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Detect MIME type of assets using Apache Tika {#detecting-mime-type-of-assets-using-apache-tika}

일반적으로 Adobe Experience Manager(AEM) 자산은 파일 확장자에서 업로드하는 자산의 MIME 유형을 감지합니다.

Apache Tika를 사용하여 자산을 업로드하는 경우 AEM Assets는 업로드 작업 동안 파일 확장명 대신 콘텐츠 스트림에서 MIME 유형을 감지합니다.

이 기능은 기본적으로 비활성화됩니다. 이 기능을 활성화하려면 Configuration Manager에서 **[!UICONTROL Day CQ DAM Mime]** 유형 서비스를 [!UICONTROL 구성합니다].

>[!NOTE]
>
>Apache Tika 라이브러리를 사용하는 MIME 유형 감지는 리소스를 많이 사용하는 작업입니다.

1. Configuration Manager 웹 콘솔을 열려면 에 `https://[aem_server]:[port]/system/console/configMgr`액세스하십시오.
1. 서비스 목록에서 Day CQ DAM Mime **[!UICONTROL Type Service를]** 찾아 옆에 **[!UICONTROL 있는 편집을]** 탭하여 편집 모드로 엽니다.

1. 파일 **[!UICONTROL 확장자를 무시하면서 업로드된 자산의]** 구문 분석을 활성화하여 MIME 유형을 결정하려면 [내용에서 MIME 감지] 옵션을 선택합니다. 기본적으로 이 옵션은 선택되지 않습니다.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 저장을 클릭/탭하여 **** 변경 내용을 저장합니다.
