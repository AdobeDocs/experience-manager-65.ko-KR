---
title: Apache Tika를 사용하여 MIME 유형의 자산 탐지
description: 'Apache Tika를 활성화하여 파일 확장자 대신 업로드 작업 중에 컨텐츠 스트림에서 MIME 유형의 자산을 탐지할 수 있습니다. [!DNL Experience Manager Assets] '
contentOwner: AG
role: Administrator, Architect
feature: 메타데이터,개발자 도구,자산 관리
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 5%

---

# [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}을 사용하여 MIME 유형의 자산 탐지

일반적으로 [!DNL Adobe Experience Manager Assets] 은 파일 확장자에서 업로드하는 MIME 유형의 자산을 감지합니다.

[!DNL Apache Tika]을 사용하여 자산을 업로드하는 경우, [!DNL Assets]은 파일 확장자 대신 업로드 작업 중에 컨텐츠 스트림에서 해당 MIME 유형을 감지합니다.

이 기능은 기본적으로 비활성화됩니다. 이 기능을 사용하려면 [!UICONTROL 구성 관리자]에서 **[!UICONTROL 일 CQ DAM Mime 유형]** 서비스를 구성하십시오.

>[!NOTE]
>
>[!DNL Apache Tika] 라이브러리를 사용하는 MIME 유형 감지는 리소스를 많이 사용하는 작업입니다.

1. 구성 관리자 웹 콘솔을 열려면 `https://[aem_server]:[port]/system/console/configMgr`에 액세스합니다.

1. 서비스 목록에서 **[!UICONTROL 일 CQ DAM MIME 유형 서비스]**&#x200B;를 찾아 **[!UICONTROL 편집]**&#x200B;을 클릭합니다.

1. 파일 확장자를 무시하면서 업로드된 자산의 구문 분석을 사용하여 MIME 유형을 확인할 수 있도록 하려면 **[!UICONTROL 컨텐츠에서 MIME 감지 옵션을 선택하십시오.]** 기본적으로 이 옵션은 선택되어 있지 않습니다.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. **[!UICONTROL 저장]**&#x200B;을 클릭하여 변경 내용을 저장합니다.
