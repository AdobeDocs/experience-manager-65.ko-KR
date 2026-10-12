---
title: WebSphere Application Server 시작 및 중지
description: 여러 절차를 수행하는 과정에서 AEM Forms 제품을 배포할 WebSphere 인스턴스를 중지하거나 시작해야 합니다. 이 문서에서는 WebSphere Application Server를 시작하고 중지하는 방법을 설명합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
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
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 95%
---
# WebSphere Application Server 시작 및 중지 {#starting-and-stopping-websphere-application-server}

여러 절차를 수행하는 과정에서 AEM Forms 제품을 배포할 WebSphere 인스턴스를 중지하거나 시작해야 합니다. 애플리케이션 서버가 시작되었는지 확실하지 않은 경우에는 먼저 WebSphere Application Server의 상태를 확인할 수 있습니다.

## WebSphere Application Server의 상태 확인 {#view-the-status-of-websphere-application-server}

1. 명령 프롬프트에서 `[appserver root]/bin` 디렉터리로 이동합니다.
1. 다음 명령을 입력하고 *server_name*&#x200B;을 WebSphere Application Server의 이름으로 바꿉니다.

   * (Windows) `serverStatus.bat`*server_name*
   * (Linux, UNIX) ./ `serverStatus.sh`*server_name*

## WebSphere Application Server 시작 {#start-websphere-application-server}

1. 명령 프롬프트에서 `[appserver root]/bin` 디렉터리로 이동합니다.
1. 다음 명령을 입력하고 *server_name*&#x200B;을 WebSphere Application Server의 이름으로 바꿉니다.

   * (Windows) `startServer.bat`*server_name*
   * (Linux, UNIX) ./ `startServer.sh`*server_name*

## WebSphere Application Server 중지 {#stop-websphere-application-server}

1. 명령 프롬프트에서 `[appserver root]/bin` 디렉터리로 이동합니다.
1. 다음 명령을 입력하고 *server_name*&#x200B;을 WebSphere Application Server의 이름으로 바꿉니다.

   * (Windows) `stopServer.bat`*server_name*
   * (Linux, UNIX) ./ `stopServer.sh`*server_name*
