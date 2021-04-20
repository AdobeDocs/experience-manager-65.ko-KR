---
title: Apache Tika를 사용하여 MIME 유형의 자산 탐지
description: 'Apache Tika를 활성화하여 파일 확장명 대신 업로드 작업 중에 콘텐츠 스트림에서 MIME 유형의 자산을 검색합니다. [!DNL Experience Manager Assets] '
contentOwner: AG
role: Administrator, Architect
feature: Metadata,Developer Tools,Asset Management
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 5%

---


# [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}을(를) 사용하여 자산의 MIME 유형 감지

일반적으로 [!DNL Adobe Experience Manager Assets]은 파일 확장자에서 업로드하는 자산의 MIME 유형을 감지합니다.

[!DNL Apache Tika]을 사용하여 자산을 업로드하는 경우, [!DNL Assets]은 파일 확장자 대신 업로드 작업 중에 콘텐츠 스트림에서 MIME 형식을 감지합니다.

이 기능은 기본적으로 비활성화됩니다. 이 기능을 활성화하려면 [!UICONTROL 구성 관리자]에서 **[!UICONTROL 일 CQ DAM MIME 유형]** 서비스를 구성합니다.

>[!NOTE]
>
>[!DNL Apache Tika] 라이브러리를 사용하는 MIME 유형 감지는 리소스를 많이 사용하는 작업입니다.

1. 구성 관리자 웹 콘솔을 열려면 `https://[aem_server]:[port]/system/console/configMgr`에 액세스하십시오.

1. 서비스 목록에서 **[!UICONTROL Day CQ DAM MIME 유형 서비스]**&#x200B;를 찾아 **[!UICONTROL 편집]**&#x200B;을 클릭합니다.

1. **[!UICONTROL 콘텐트]**&#x200B;에서 MIME 감지 옵션을 선택하여 업로드된 에셋의 구문 분석을 활성화하여 파일 확장자를 무시하고 MIME 유형을 결정합니다. 기본적으로 이 옵션은 선택되어 있지 않습니다.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. **[!UICONTROL 저장]**&#x200B;을 클릭하여 변경 내용을 저장합니다.
