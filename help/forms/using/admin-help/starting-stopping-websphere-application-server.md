---
title: WebSphere Application Server 시작 및 중지
description: 몇 가지 절차를 수행하려면 AEM Forms 제품을 배포하려는 WebSphere 인스턴스를 중지하거나 시작해야 합니다. 이 문서에서는 WebSphere Application Server를 시작 및 정지하는 방법에 대해 설명합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# WebSphere Application Server 시작 및 중지 {#starting-and-stopping-websphere-application-server}

몇 가지 절차를 수행하려면 AEM Forms 제품을 배포하려는 WebSphere 인스턴스를 중지하거나 시작해야 합니다. 응용 프로그램 서버가 시작되었는지 확실하지 않은 경우 먼저 WebSphere Application Server의 상태를 볼 수 있습니다.

## WebSphere Application Server 상태 보기 {#view-the-status-of-websphere-application-server}

1. 명령 프롬프트에서 `[appserver root]/bin` 디렉토리.
1. 다음 명령을 입력하여 을 바꿉니다. *server_name* WebSphere Application Server의 이름:

   * (Windows) `serverStatus.bat`*server_name*
   * (Linux, UNIX) 를 참조하십시오./ `serverStatus.sh`*server_name*

## WebSphere 애플리케이션 서버 시작 {#start-websphere-application-server}

1. 명령 프롬프트에서 `[appserver root]/bin` 디렉토리.
1. 다음 명령을 입력하여 을 바꿉니다. *server_name* WebSphere Application Server의 이름:

   * (Windows) `startServer.bat`*server_name*
   * (Linux, UNIX) 를 참조하십시오./ `startServer.sh`*server_name*

## WebSphere 애플리케이션 서버 중지 {#stop-websphere-application-server}

1. 명령 프롬프트에서 `[appserver root]/bin` 디렉토리.
1. 다음 명령을 입력하여 을 바꿉니다. *server_name* WebSphere Application Server의 이름:

   * (Windows) `stopServer.bat`*server_name*
   * (Linux, UNIX) 를 참조하십시오./ `stopServer.sh`*server_name*
