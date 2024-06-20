---
title: 프로세스 보고 소개
description: JEE 프로세스 보고에 대한 AEM Forms 소개 및 주요 기능
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 674d28dc-7353-49de-9e12-b1998e1509c7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 프로세스 보고 소개{#introduction-to-process-reporting}

![프로세스 보고](assets/process-reporting.png)

프로세스 보고는 AEM Forms 프로세스 및 작업에 대한 보고서를 만들고 보는 데 사용하는 브라우저 기반 도구입니다.

프로세스 보고에서는 장기 실행 프로세스, 프로세스 기간 및 워크플로우 볼륨에 대한 정보를 필터링하고 볼 수 있는 기본 보고서 세트를 제공합니다.

또한 프로세스 보고에서는 임시 쿼리를 실행하고 사용자 지정 보고서 보기를 프로세스 보고 사용자 인터페이스에 통합하는 인터페이스를 제공합니다.

지원되는 브라우저 목록에 대해서는 다음을 참조하십시오. [AEM Forms 지원 플랫폼](/help/forms/using/aem-forms-jee-supported-platforms.md).

프로세스 보고는 다음과 같은 모듈을 기반으로 구축됩니다.

* AEM Forms 데이터베이스에서 프로세스 데이터 읽기
* Publish 프로세스 데이터를 포함된 Process Reporting 저장소로
* 보고서를 볼 수 있는 브라우저 기반 사용자 인터페이스를 제공합니다.

## 주요 기능 {#key-capabilities}

### Always-on 보고 {#always-on-reporting}

![사이트 관리](assets/site-management.png)

장기 실행 프로세스, 프로세스 기간 차트 목록을 보고 필터를 사용하여 사용자 정의 쿼리를 실행합니다.

프로세스 보고에서는 보고서 및 쿼리 데이터를 CSV 형식으로 내보내는 옵션도 제공합니다.

### 임시 보고서 {#adhoc-reports}

![인쇄 및 색상](assets/print-&-colour.png)

필터를 사용하여 특정 데이터 보기를 얻을 수 있습니다.

ID, 기간, 시작 및 종료 날짜, 프로세스 개시자 등을 기준으로 프로세스 또는 작업을 검색할 수 있습니다.

여러 필터를 결합하여 특정 보고서를 만들 수 있습니다.

그런 다음 나중에 실행할 날짜 또는 시간에 보고서 필터를 저장할 수 있습니다.

### 프로세스/작업 내역 {#process-task-history}

![파일 관리](assets/file-management.png)

AEM Forms 서버는 수많은 프로세스를 동시에 실행합니다. 이러한 프로세스는 한 상태에서 다른 상태로 계속 전환됩니다. Forms 데이터를 일정한 간격으로 Process Reporting 저장소에 게시하면 Process Reporting에서는 AEM Forms에서 실행 중인 프로세스에 대한 전환 정보가 유지됩니다.

### 액세스 제어 {#access-control-br}

![제목 없음](assets/untitled.png)

프로세스 보고에서는 사용자 인터페이스에 대한 권한 기반 액세스를 제공합니다.

즉, 보고 권한이 있는 사용자만 Process Reporting 사용자 인터페이스에 액세스할 수 있습니다.
