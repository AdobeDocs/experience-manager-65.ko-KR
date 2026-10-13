---
title: Apache Tika를 사용하여 MIME 유형의 자산 탐지
description: 파일 확장명 대신 업로드 작업 중에 [!DNL Experience Manager Assets]이(가) 콘텐츠 스트림에서 MIME 유형의 자산을 검색할 수 있도록 Apache Tika를 사용하도록 설정합니다.
contentOwner: AG
role: Admin, Developer
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: ed6971a3-2c12-4fd2-81f4-ff329c416250
    internal-label: Metadata
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 9%
---
# [!DNL Apache Tika]을(를) 사용하여 자산의 MIME 유형 검색 {#detecting-mime-type-of-assets-using-apache-tika}

일반적으로 [!DNL Adobe Experience Manager Assets]은(는) 파일 확장명에서 업로드하는 자산의 MIME 형식을 검색합니다.

[!DNL Apache Tika]을(를) 사용하여 자산을 업로드하는 경우 [!DNL Assets]이(가) 파일 확장명 대신 업로드 작업 중에 콘텐츠 스트림에서 해당 MIME 형식을 감지합니다.

이 기능은 기본적으로 비활성화되어 있습니다. 이 기능을 사용하려면 [!UICONTROL 구성 관리자]에서 **[!UICONTROL 일 CQ DAM Mime 유형]** 서비스를 구성하십시오.

>[!NOTE]
>
>[!DNL Apache Tika] 라이브러리를 사용하는 MIME 유형 검색은 리소스를 많이 사용하는 작업입니다.

1. Configuration Manager 웹 콘솔을 열려면 `https://[aem_server]:[port]/system/console/configMgr`에 액세스합니다.

1. 서비스 목록에서 **[!UICONTROL 일 CQ DAM Mime 유형 서비스]**&#x200B;를 찾은 다음 **[!UICONTROL 편집]**&#x200B;을 클릭합니다.

1. **[!UICONTROL 콘텐츠에서 MIME 검색]** 옵션을 선택하여 업로드한 에셋의 구문 분석을 활성화하여 파일 확장자를 무시하면서 해당 MIME 유형을 결정합니다. 기본적으로 이 옵션은 선택되지 않습니다.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. **[!UICONTROL 저장]**&#x200B;을 클릭하여 변경 내용을 저장합니다.
