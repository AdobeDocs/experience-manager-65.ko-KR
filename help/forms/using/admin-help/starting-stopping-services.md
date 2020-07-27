---
title: 서비스 시작 및 중지
seo-title: 서비스 시작 및 중지
description: AEM Forms 모듈, 응용 프로그램 서버 및 데이터베이스와 관련된 서비스를 시작 및 중지하는 방법을 알아봅니다.
seo-description: AEM Forms 모듈, 응용 프로그램 서버 및 데이터베이스와 관련된 서비스를 시작 및 중지하는 방법을 알아봅니다.
uuid: 8c831cb2-4165-4118-8a09-764cec4e5e05
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b93060bd-c6e1-40d2-8acd-ccafb8ed56da
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# 서비스 시작 및 중지 {#starting-and-stopping-services}

AEM 양식에 포함된 두 가지 유형의 서비스가 있습니다.

* AEM Forms 애플리케이션 서버 및 데이터베이스를 제어하는 서비스입니다.
* AEM 양식 모듈을 제어하는 서비스

## AEM 양식 모듈과 연결된 서비스 시작 또는 중지 {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM 양식 모듈(예: 양식, 권한 관리, 출력)은 서비스로 작동합니다. 이러한 AEM 양식 모듈에 대한 서비스를 중지하거나 시작해야 할 수도 있습니다. 예를 들어, 서비스에 대한 설정을 변경한 후 AEM Forms 서비스를 중지하고 다시 시작해야 합니다.

1. 관리 콘솔에서 **서비스** > **애플리케이션 및 서비스** > **서비스 관리**&#x200B;를 클릭합니다.
1. 서비스 관리 페이지에서 중지하거나 시작할 서비스 옆의 확인란을 선택하고 중지 또는 시작을 클릭합니다.

## 응용 프로그램 서버 및 데이터베이스에 대한 서비스 시작 또는 중지 {#start-or-stop-services-for-the-application-server-and-database}

AEM 양식의 전체 구현에는 응용 프로그램 서버 및 데이터베이스 서비스가 포함됩니다.

* *`[application server]`* for AEM forms
* *`[database]`* for AEM forms

Windows의 경우 이러한 서비스는 **관리 도구** > **서비스 패널을 통해 액세스할 수 있습니다**. 예를 들어 턴키 방법을 사용하여 JBoss에 AEM 양식을 설치한 경우 시스템에서 다음 서비스를 사용할 수 있습니다.

* Adobe Experience Manager 양식용 JBoss
* Adobe Experience Manager 양식용 MySQL

서비스 패널의 목록에서 서비스를 선택한 다음 패널에서 해당 작업 단추를 클릭하여 서비스를 시작하거나 중지합니다.

UNIX® 또는 Linux의 경우 명령줄에 다음 텍스트 *`[service name]`* 를 입력합니다. 여기서 는 검증하는 서비스의 이름입니다.

```java
     ps -A | grep [service name]
```

