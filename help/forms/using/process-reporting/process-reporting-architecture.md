---
title: 프로세스 보고 작동 방식
seo-title: 프로세스 보고 작동 방식
description: JEE 프로세스 보고에서 AEM Forms을 구성하는 서비스에 대한 설명과 프로세스 보고 UI 소개
seo-description: JEE 프로세스 보고에서 AEM Forms을 구성하는 서비스에 대한 설명과 프로세스 보고 UI 소개
uuid: 37e31985-088a-4ef6-ba57-10a01597a873
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a6ff50df-273d-48f7-b0c6-0e69e900b97f
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# 프로세스 보고 작동 방식{#how-process-reporting-works}

프로세스 보고는 JEE의 AEM Forms 보고 모듈입니다.

프로세스 보고를 사용하면 AEM Forms 프로세스 및 작업에 대한 보고서를 실행할 수 있습니다.

프로세스 보고는 포함된 프로세스 보고 저장소를 사용하여 Forms 데이터를 게시합니다. 그런 다음 이 데이터를 사용하여 보고서를 실행합니다.

프로세스 보고는 다음 모듈로 구성됩니다.

* [ProcessDataPublisher 서비스](#processdatapublisher-service-br-p)
* [ProcessDataStorage 서비스](#processdatastorageprovider-service-br-p)
* [OSGi 서비스](#osgi-service-br-p)
* [쿼리 데이터 서블릿](#querydataservlet-service-br-p)
* [프로세스 보고 사용자 인터페이스](#process-reporting-user-interface-br-p)

## 프로세스 보고 아키텍처 {#process-reporting-architecture-br}

![처리 reportingarchitecture](assets/processreportingarchitecture.png)

## 프로세스 보고 모듈 {#process-reporting-modules}

### ProcessDataPublisher 서비스 {#processdatapublisher-service-br}

ProcessDataPublisher 서버는 AEM Forms 데이터베이스에서 주기적으로 실행되고 서비스의 마지막 실행 이후 변경된 데이터를 추출합니다. 그런 다음 데이터를 Process Data Storage 서비스에 게시합니다.

서비스 구성에 대한 자세한 내용은 [ProcessDataPublisher 서비스 구성](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p)을 참조하십시오.

### ProcessDataStorageProvider 서비스 {#processdatastorageprovider-service-br}

ProcessDataStorageProvider 서비스는 ProcessDataPublisher 서비스에서 프로세스 데이터를 수신하여 데이터를 프로세스 보고 저장소에 저장합니다.

서비스 구성에 대한 자세한 내용은 [ProcessDataStorageProvider 서비스 구성](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p)을 참조하십시오.

### OSGi 서비스 {#osgi-service-br}

QueryDataServlet은 이 서비스를 사용하여 프로세스 보고 저장소에서 보고 데이터를 가져옵니다.

### QueryDataServlet 서비스 {#querydataservlet-service-br}

QueryDataServlet 서비스는 프로세스 보고 사용자 인터페이스에서 쿼리를 받습니다.

그런 다음 OSGi 서비스를 사용하여 관련 보고 데이터를 얻고 데이터를 처리하며 데이터를 사용자 인터페이스에 반환합니다.

### 프로세스 보고 사용자 인터페이스 {#process-reporting-user-interface-br}

프로세스 보고 사용자 인터페이스는 웹 브라우저 기반 인터페이스입니다. 이 인터페이스를 사용하여 AEM Forms 데이터베이스에서 게시된 프로세스 및 작업 정보를 봅니다.

프로세스 보고 사용자 인터페이스에 대한 소개는 [프로세스 보고 사용자 인터페이스](/help/forms/using/process-reporting/introduction-process-reporting.md)를 참조하십시오.

### QueryDataServlet 서비스 {#querydataservlet-service-br-1}

QueryDataServlet 서비스는 프로세스 보고 사용자 인터페이스에서 쿼리를 받습니다.

그런 다음 OSGi 서비스를 사용하여 관련 보고 데이터를 얻고 데이터를 처리하며 데이터를 사용자 인터페이스에 반환합니다.

### 사용자 지정 보고서 {#custom-reports-br}

고유한 사용자 지정 보고서를 만들고 이 보고서를 프로세스 보고 사용자 인터페이스의 사용자 지정 보고서 탭에 표시할 수 있습니다.

사용자 지정 보고서를 만드는 단계는 문서 [프로세스 보고 내 사용자 지정 보고서](/help/forms/using/process-reporting/process-reporting-custom-reports.md)에서 사용자 지정 보고서 만들기를 참조하십시오.
