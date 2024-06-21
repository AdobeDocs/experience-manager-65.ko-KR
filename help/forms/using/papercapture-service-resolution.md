---
title: PaperCapture 서비스가 PDF에서 OCR(Optical Character Recognition) 작업을 수행하지 못할 때 발생하는 문제를 해결하기 위한 문제 해결 문서
description: PaperCapture 서비스가 PDF에서 OCR(Optical Character Recognition) 작업을 수행하지 못하는 문제를 해결하기 위한 단계에 대해 알아봅니다.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 64e120ee-5f16-4cd3-9ae9-95b165169e47
source-git-commit: e682381f08e143c1bf14d7dcee4f022e684ee1f2
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 1%

---


# PaperAture 서비스에서 PDF에 대한 OCR 작업을 수행하지 못했습니다.

## 문제

AEM Forms 서비스 팩 6.5.21.0으로 업그레이드한 후 `PaperCapture` 서비스가 PDF에서 OCR(광학 문자 인식) 작업을 수행하지 못했습니다. 이 서비스는 PDF 또는 로그 파일의 형태로 출력을 생성하지 않습니다.

## 솔루션

1. 다운로드 [핫픽스](https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0) 소프트웨어 배포 포털에서.
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
1. AEM 애플리케이션 서버를 중지합니다.
1. 의 기존 콘텐츠 바꾸기 `PaperCaptureSvc` 복사한 콘텐츠가 있는 폴더.
1. AEM 응용 프로그램 서버를 다시 시작합니다.

   >[!NOTE]
   >
   > SDK를 다시 시작하려면 &#39;Ctrl + C&#39; 명령을 사용하는 것이 좋습니다. Java 프로세스 중지와 같은 대체 방법을 사용하여 AEM SDK를 다시 시작하면 AEM 개발 환경이 일치하지 않을 수 있습니다.
