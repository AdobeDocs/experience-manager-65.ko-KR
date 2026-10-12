---
title: Assets Insights용 데모 패키지 사용
description: 데모 패키지를 사용하여 Adobe Assets Insights에서 데이터를 캡처하고 웹 페이지에 대한 인사이트를 생성할 수 있습니다.
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 13947513-da76-43e1-ae01-abd24a59752a
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: a4e1c1f5-18fc-592e-bfc7-453ce6ae0030
    internal-label: Asset Insights
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: c29e3a96-cd2b-4e21-b382-a8279aa04553
    internal-label: Asset reports
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 2%
---
# Assets Insights용 데모 패키지 사용 {#using-demo-package-for-asset-insights}

데모 패키지를 사용하여 Adobe Assets Insights를 활성화하여 샘플 웹 페이지의 데이터를 캡처하고 통찰력을 생성할 수 있습니다.

## 샘플 웹 페이지가 있는 [!DNL Use Experience Manager Assets] 인사이트  {#using-aem-assets-insights-with-sample-web-page}

1. [Assets 인사이트 구성](configure-asset-insights.md)의 지침을 사용하여 Assets 인사이트를 구성합니다.
1. 아래에서 샘플 Assets 패키지를 다운로드하고 CRXDE 패키지 관리자에서 패키지를 설치합니다.

   [파일 가져오기](assets/insightsdemo.zip)

1. 아래에서 샘플 웹 페이지가 포함된 ZIP 파일을 다운로드하여 로컬 파일 시스템에서 추출하십시오.

   [파일 가져오기](assets/demosite.zip)

1. 웹 브라우저에서 열리는 웹 페이지를 클릭합니다.

   >[!CAUTION]
   >
   >웹 페이지가 localhost 서버에서 자산을 로드하도록 구성되어 있습니다. 서버가 다른 곳에서 실행 중인 경우 서버 주소를 localhost에서 웹 페이지의 HTML 컨텐츠에 있는 서버 주소로 변경합니다.

   >[!NOTE]
   >
   >외부 웹 페이지는 [!DNL Experience Manager] 자체에 있을 수 있습니다.
