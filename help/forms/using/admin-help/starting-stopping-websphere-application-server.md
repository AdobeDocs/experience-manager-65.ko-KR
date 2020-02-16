---
title: WebSphere 응용 프로그램 서버 시작 및 중지
seo-title: WebSphere 응용 프로그램 서버 시작 및 중지
description: 여러 절차에 따라 AEM 양식 제품을 배포할 WebSphere 인스턴스를 중지하거나 시작해야 합니다. 이 문서에서는 WebSphere 응용 프로그램 서버를 시작 및 중지하는 방법에 대해 설명합니다.
seo-description: 여러 절차에 따라 AEM 양식 제품을 배포할 WebSphere 인스턴스를 중지하거나 시작해야 합니다. 이 문서에서는 WebSphere 응용 프로그램 서버를 시작 및 중지하는 방법에 대해 설명합니다.
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# WebSphere 응용 프로그램 서버 시작 및 중지 {#starting-and-stopping-websphere-application-server}

여러 절차에 따라 AEM 양식 제품을 배포할 WebSphere 인스턴스를 중지하거나 시작해야 합니다. 응용 프로그램 서버가 시작되었는지 확실하지 않은 경우 먼저 WebSphere 응용 프로그램 서버의 상태를 볼 수 있습니다.

## WebSphere 응용 프로그램 서버의 상태 보기 {#view-the-status-of-websphere-application-server}

1. 명령 프롬프트에서 appserver root *[]*/bin 디렉토리로 이동합니다.
1. 다음 명령을 입력하여 *server_name* 을 WebSphere 응용 프로그램 서버의 이름으로 바꿉니다.

   * (Windows) `serverStatus.bat`*server_name *
   * (Linux, UNIX)./ `serverStatus.sh`*server_name *

## WebSphere 응용 프로그램 서버 시작 {#start-websphere-application-server}

1. 명령 프롬프트에서 appserver root *[]*/bin 디렉토리로 이동합니다.
1. 다음 명령을 입력하여 *server_name* 을 WebSphere 응용 프로그램 서버의 이름으로 바꿉니다.

   * (Windows) `startServer.bat`*server_name *
   * (Linux, UNIX)./ `startServer.sh`*server_name *

## WebSphere 응용 프로그램 서버 중지 {#stop-websphere-application-server}

1. 명령 프롬프트에서 appserver root *[]*/bin 디렉토리로 이동합니다.
1. 다음 명령을 입력하여 *server_name* 을 WebSphere 응용 프로그램 서버의 이름으로 바꿉니다.

   * (Windows) `stopServer.bat`*server_name *
   * (Linux, UNIX)./ `stopServer.sh`*server_name *

