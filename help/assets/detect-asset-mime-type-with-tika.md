---
title: Apache Tika를 사용하여 MIME 유형의 자산 탐지
description: Apache Tika를 활성화하여 [!DNL Experience Manager Assets] 파일 확장명 대신 업로드 작업 중에 콘텐츠 스트림에서 MIME 유형의 자산을 감지합니다.
contentOwner: AG
role: Admin, Developer
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 9%

---

# [!DNL Apache Tika]을(를) 사용하여 자산의 MIME 유형 검색 {#detecting-mime-type-of-assets-using-apache-tika}

일반적으로 [!DNL Adobe Experience Manager Assets]은(는) 파일 확장명에서 업로드하는 자산의 MIME 형식을 검색합니다.

[!DNL Apache Tika]을(를) 사용하여 자산을 업로드하는 경우 [!DNL Assets]이(가) 파일 확장명 대신 업로드 작업 중에 콘텐츠 스트림에서 해당 MIME 형식을 감지합니다.

이 기능은 기본적으로 비활성화되어 있습니다. 이 기능을 사용하려면 **[!UICONTROL 구성 관리자]**&#x200B;에서 [!UICONTROL 일 CQ DAM Mime 유형] 서비스를 구성하십시오.

>[!NOTE]
>
>[!DNL Apache Tika] 라이브러리를 사용하는 MIME 유형 검색은 리소스를 많이 사용하는 작업입니다.

1. Configuration Manager 웹 콘솔을 열려면 `https://[aem_server]:[port]/system/console/configMgr`에 액세스합니다.

1. 서비스 목록에서 **[!UICONTROL 일 CQ DAM Mime 유형 서비스]**&#x200B;를 찾은 다음 **[!UICONTROL 편집]**&#x200B;을 클릭합니다.

1. **[!UICONTROL 콘텐츠에서 MIME 검색]** 옵션을 선택하여 업로드한 에셋의 구문 분석을 활성화하여 파일 확장자를 무시하면서 해당 MIME 유형을 결정합니다. 기본적으로 이 옵션은 선택되지 않습니다.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. **[!UICONTROL 저장]**&#x200B;을 클릭하여 변경 내용을 저장합니다.
