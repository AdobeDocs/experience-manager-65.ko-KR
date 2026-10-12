---
title: 출력, Forms 및 (기록 문서) DoR 서비스 관련 연결 문제
description: SP19 이후 AEM Forms 연결 오류를 해결하십시오. Microsoft Visual C++를 설치하고 서버를 다시 시작하여 원활한 솔루션을 제공합니다. 출력, Forms, DoR 서비스 문제를 해결합니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin
exl-id: bd58099c-08cd-4056-afb6-a5935454429a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 26%
---
# 출력 서비스, 양식 서비스, DoR(기록 문서) 서비스를 사용할 수 없음 {#unable-to-use-output-service-forms-service-or-document-of-record-service}

## 문제

AEM Forms 6.5 서비스 팩 19를 설치한 후 출력 서비스, Forms 서비스 또는 기록 문서(DoR) 서비스를 사용하려고 하면 `Connection to failed service` 오류가 발생할 수 있습니다.

## 솔루션

문제를 해결하려면 다음을 수행하십시오.

1. AEM 6.5 Forms 인스턴스를 중지합니다.
1. AEM 6.5 Forms이 설치된 컴퓨터에서 Visual Studio 2015, 2017, 2019 및 2022용 Microsoft Visual C++ 재배포 가능 패키지 [64비트 버전을 다운로드하여 설치하십시오](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022).
1. AEM Forms 서버를 다시 시작합니다.

   >[!NOTE]
   >
   > SDK를 다시 시작하려면 &#39;Ctrl+C&#39; 명령을 사용하는 것이 좋습니다. 예를 들어 Java 프로세스를 중지하는 것과 같은 대체 방법을 사용하여 AEM SDK를 다시 시작하면 AEM 개발 환경에서 불일치가 발생할 수 있습니다.


>[!NOTE]
>
>
> 이전 버전이 설치된 경우에도 재배포 가능 패키지를 설치해야 합니다.
