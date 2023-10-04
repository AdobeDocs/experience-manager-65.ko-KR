---
title: 서비스 시작 및 중지
description: AEM Forms 모듈, 애플리케이션 서버 및 데이터베이스와 연결된 서비스를 시작 및 중지하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 55bf5196-22c6-4286-8c92-ff44d81dde49
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 서비스 시작 및 중지 {#starting-and-stopping-services}

AEM Forms의 일부인 서비스에는 두 가지 유형이 있습니다.

* AEM Forms 응용 프로그램 서버 및 데이터베이스를 제어하는 서비스입니다.
* AEM Forms 모듈을 제어하는 서비스

## AEM Forms 모듈과 연결된 서비스 시작 또는 중지 {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM forms 모듈(예: Forms, Rights Management, 출력)은 서비스로 작동합니다. 이러한 AEM Forms 모듈에 대한 서비스를 중지하거나 시작해야 하는 경우가 있습니다. 예를 들어 서비스에 대한 설정을 변경한 후 AEM Forms 서비스를 중지했다가 다시 시작해야 합니다.

1. 관리 콘솔에서 다음을 클릭합니다. **서비스** > **애플리케이션 및 서비스** > **서비스 관리**.
1. 서비스 관리 페이지에서 중지하거나 시작할 서비스 옆의 확인란을 선택하고 중지 또는 시작을 누릅니다.

## 응용 프로그램 서버 및 데이터베이스에 대한 서비스 시작 또는 중지 {#start-or-stop-services-for-the-application-server-and-database}

AEM Forms의 전체 구현에는 애플리케이션 서버 및 데이터베이스 서비스가 포함됩니다.

* *`[application server]`* AEM forms용
* *`[database]`* AEM forms용

Windows에서는 다음을 통해 이러한 서비스에 액세스할 수 있습니다 **관리 도구** > **서비스 패널**. 예를 들어, turnkey 메서드를 사용하여 JBoss에 AEM Forms를 설치한 경우 시스템에서 다음 서비스를 사용할 수 있습니다.

* Adobe Experience Manager forms용 JBoss
* Adobe Experience Manager forms용 MySQL

[서비스] 패널의 목록에서 이러한 서비스를 선택한 다음 패널에서 해당 작업 버튼을 클릭하여 시작하거나 중지합니다.

UNIX® 또는 Linux의 경우 명령줄에서 다음 텍스트를 입력합니다. 여기서 *`[service name]`* 은(는) 확인 중인 서비스의 이름입니다.

```java
     ps -A | grep [service name]
```
