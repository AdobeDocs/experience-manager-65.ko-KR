---
title: PaperCapture 서비스가 PDF에서 OCR(Optical Character Recognition) 작업을 수행하지 못할 때 발생하는 문제를 해결하기 위한 문제 해결 문서
description: PaperCapture 서비스가 PDF에서 OCR(Optical Character Recognition) 작업을 수행하지 못하는 문제를 해결하기 위한 단계에 대해 알아봅니다.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 18005ba060954151df126789496c81f7238e32f6
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 1%

---


# PaperAture 서비스에서 PDF에 대해 OCR을 수행하지 못했습니다.

## 문제

AEM Forms 서비스 팩 6.5.21.0으로 업그레이드한 후 `PaperCapture` 서비스가 PDF에서 OCR(광학 문자 인식) 작업을 수행하지 못했습니다. 이 서비스는 PDF 또는 로그 파일의 형태로 출력을 생성하지 않습니다.

## 솔루션

1. 다운로드 [핫픽스](https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Ca285aedf27094c9e8d9b08dc91e26aa7%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545648843177070%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=uWk0PsSSDjLRxqEMGMW%2BbD%2Fv4egR4vWL%2B0mfKpXdrKQ%3D&amp;reserved=0) 소프트웨어 배포 포털에서.
1. 다운로드한 폴더의 컨텐츠를 추출하고 복사합니다.
1. 해당 애플리케이션 서버의 아래 경로로 이동합니다.
   * **jboss**:
     `..\Adobe\Adobe_Experience_Manager_Forms\jboss\standalone\svcnative\PaperCaptureSvc`
   * **weblogic**:
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **websphere**:\
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **OSGi 설정**:\
     `..\quickstart\crx-quickstart\bedrock\svcnative\PaperCaptureSvc`
1. 의 기존 콘텐츠 바꾸기 `PaperCaptureSvc` 복사한 콘텐츠가 있는 폴더.
1. [AEM 인스턴스 다시 시작](/help/forms/using/restart-aem-sdk.md).


