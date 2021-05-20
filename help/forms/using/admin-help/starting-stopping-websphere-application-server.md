---
title: WebSphere Application Server 시작 및 중지
seo-title: WebSphere Application Server 시작 및 중지
description: AEM Forms 제품을 배포하려는 WebSphere 인스턴스를 중지하거나 시작해야 하는 몇 가지 절차가 있습니다. 이 문서에서는 WebSphere Application Server를 시작하고 정지하는 방법을 설명합니다.
seo-description: AEM Forms 제품을 배포하려는 WebSphere 인스턴스를 중지하거나 시작해야 하는 몇 가지 절차가 있습니다. 이 문서에서는 WebSphere Application Server를 시작하고 정지하는 방법을 설명합니다.
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# WebSphere 응용 프로그램 서버 {#starting-and-stopping-websphere-application-server} 시작 및 중지

AEM Forms 제품을 배포하려는 WebSphere 인스턴스를 중지하거나 시작해야 하는 몇 가지 절차가 있습니다. 응용 프로그램 서버가 시작되었는지 확실하지 않은 경우 먼저 WebSphere 응용 프로그램 서버의 상태를 볼 수 있습니다.

## WebSphere 응용 프로그램 서버 {#view-the-status-of-websphere-application-server} 상태 보기

1. 명령 프롬프트에서 `[appserver root]/bin` 디렉토리로 이동합니다.
1. 다음 명령을 입력하여 *server_name*&#x200B;을 WebSphere 응용 프로그램 서버의 이름으로 바꿉니다.

   * (Windows) `serverStatus.bat`*server_name*
   * (Linux, UNIX) 를 참조하십시오./ `serverStatus.sh`*server_name*

## WebSphere 응용 프로그램 서버 {#start-websphere-application-server} 시작

1. 명령 프롬프트에서 `[appserver root]/bin` 디렉토리로 이동합니다.
1. 다음 명령을 입력하여 *server_name*&#x200B;을 WebSphere 응용 프로그램 서버의 이름으로 바꿉니다.

   * (Windows) `startServer.bat`*server_name*
   * (Linux, UNIX) 를 참조하십시오./ `startServer.sh`*server_name*

## WebSphere 응용 프로그램 서버 중지 {#stop-websphere-application-server}

1. 명령 프롬프트에서 `[appserver root]/bin` 디렉토리로 이동합니다.
1. 다음 명령을 입력하여 *server_name*&#x200B;을 WebSphere 응용 프로그램 서버의 이름으로 바꿉니다.

   * (Windows) `stopServer.bat`*server_name*
   * (Linux, UNIX) 를 참조하십시오./ `stopServer.sh`*server_name*
