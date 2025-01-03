---
title: 서비스 시작 및 중지
description: AEM Forms 모듈, 애플리케이션 서버 및 데이터베이스와 연결된 서비스를 시작 및 중지하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 55bf5196-22c6-4286-8c92-ff44d81dde49
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# 서비스 시작 및 중지 {#starting-and-stopping-services}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인합니다.

AEM Forms의 일부인 서비스에는 두 가지 유형이 있습니다.

* AEM Forms 응용 프로그램 서버 및 데이터베이스를 제어하는 서비스입니다.
* AEM Forms 모듈을 제어하는 서비스

## AEM Forms 모듈과 연결된 서비스 시작 또는 중지 {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM forms 모듈(예: Forms, Rights Management, 출력)은 서비스로 작동합니다. 이러한 AEM Forms 모듈에 대한 서비스를 중지하거나 시작해야 하는 경우가 있습니다. 예를 들어 서비스에 대한 설정을 변경한 후 AEM Forms 서비스를 중지했다가 다시 시작해야 합니다.

>[!NOTE]
>
> SDK을 다시 시작하려면 &#39;Ctrl + C&#39; 명령을 사용하는 것이 좋습니다. Java 프로세스를 중지하는 등의 대체 방법을 사용하여 AEM SDK을 다시 시작하면 AEM 개발 환경이 일치하지 않을 수 있습니다.

1. 관리 콘솔에서 **서비스** > **응용 프로그램 및 서비스** > **서비스 관리**&#x200B;를 클릭합니다.
1. 서비스 관리 페이지에서 중지하거나 시작할 서비스 옆의 확인란을 선택하고 중지 또는 시작을 누릅니다.

## 응용 프로그램 서버 및 데이터베이스에 대한 서비스 시작 또는 중지 {#start-or-stop-services-for-the-application-server-and-database}

AEM Forms의 전체 구현에는 애플리케이션 서버 및 데이터베이스 서비스가 포함됩니다.

* AEM 양식용 *`[application server]`*
* AEM 양식용 *`[database]`*

Windows에서는 **관리 도구** > **서비스 패널**&#x200B;을 통해 이러한 서비스에 액세스할 수 있습니다. 예를 들어, turnkey 메서드를 사용하여 JBoss에 AEM Forms를 설치한 경우 시스템에서 다음 서비스를 사용할 수 있습니다.

* Adobe Experience Manager forms용 JBoss
* Adobe Experience Manager forms용 MySQL

[서비스] 패널의 목록에서 이러한 서비스를 선택한 다음 패널에서 해당 작업 버튼을 클릭하여 시작하거나 중지합니다.

UNIX® 또는 Linux의 경우 명령줄에서 다음 텍스트를 입력하십시오. 여기서 *`[service name]`*&#x200B;은(는) 확인 중인 서비스 이름입니다.

```java
     ps -A | grep [service name]
```
