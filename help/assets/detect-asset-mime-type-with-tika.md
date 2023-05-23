---
title: Apache Tika를 사용하여 MIME 유형의 자산 탐지
description: Apache Tika를 활성화하여 도움 받기 [!DNL Experience Manager Assets] 업로드 작업 중에 파일 확장명 대신 콘텐츠 스트림에서 MIME 유형의 자산을 감지합니다.
contentOwner: AG
role: Admin, Architect
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 5%

---

# 다음을 사용하여 MIME 유형의 자산 감지 [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

일반적으로, [!DNL Adobe Experience Manager Assets] 는 파일 확장에서 업로드하는 자산의 MIME 유형을 감지합니다.

를 사용하는 경우 [!DNL Apache Tika] 에셋을 업로드하려면 [!DNL Assets] 는 업로드 작업 중에 파일 확장명 대신 콘텐츠 스트림에서 MIME 유형을 감지합니다.

이 기능은 기본적으로 비활성화되어 있습니다. 이 기능을 활성화하려면 다음을 구성합니다. **[!UICONTROL 일 CQ DAM Mime 유형]** 서비스 출처: [!UICONTROL 구성 관리자].

>[!NOTE]
>
>다음을 사용하여 MIME 유형 검색 [!DNL Apache Tika] 라이브러리는 리소스를 많이 사용하는 작업입니다.

1. Configuration Manager 웹 콘솔을 열려면 `https://[aem_server]:[port]/system/console/configMgr`.

1. 서비스 목록에서 **[!UICONTROL 일별 CQ DAM Mime 유형 서비스]** 및 클릭 **[!UICONTROL 편집]**.

1. 다음 항목 선택 **[!UICONTROL 컨텐츠에서 MIME 감지]** 파일 확장자를 무시하면서 MIME 유형을 결정하기 위해 업로드된 에셋의 구문 분석을 활성화하는 옵션입니다. 기본적으로 이 옵션은 선택되지 않습니다.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 클릭 **[!UICONTROL 저장]** 변경 내용을 저장합니다.
