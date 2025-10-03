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
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '180'
ht-degree: 100%

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
