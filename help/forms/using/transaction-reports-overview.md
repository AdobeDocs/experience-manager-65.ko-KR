---
title: 거래 보고서 개요
description: 제출된 모든 양식, 렌더링된 대화형 통신, 한 형식으로 변환된 문서 등의 수를 유지합니다.
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Transaction Reports
exl-id: bb812614-f4d8-4f57-bea2-8f7d31457039
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# OSGi의 AEM Forms에 대한 거래 보고서 {#transaction-reports-overview}

<!--## Introduction {#introduction}

Transaction reports in AEM Forms let you keep a count of all transactions taken place since a specified date on your AEM Forms deployment. The objective is to provide information about product usage and help business stakeholders understand their digital processing volumes. Examples of a transaction include:

* Submission of an adaptive form, an HTML5 Form, or a form set
* Rendition of a print or a web version of an interactive communication
* Conversion of a document from one file format to another

For more information on what is considered a transaction, see [Billable APIs](../../forms/using/transaction-reports-billable-apis.md).-->

거래 기록은 기본적으로 비활성화되어 있습니다. AEM 웹 콘솔에서 [트랜잭션 기록을 활성화](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports)할 수 있습니다. 작성자, 처리 또는 게시 인스턴스에 대한 거래 보고서를 볼 수 있습니다. 작성자 또는 처리 인스턴스에 대한 모든 트랜잭션의 집계된 합계에 대한 트랜잭션 보고서를 봅니다. 보고서가 실행되는 게시 인스턴스에서만 수행되는 모든 트랜잭션의 수에 대한 게시 인스턴스의 트랜잭션 보고서를 봅니다.

동일한 AEM 인스턴스에서 콘텐츠를 작성(적응형 양식, 대화형 통신, 테마 및 기타 작성 활동 만들기)하고 문서를 처리(워크플로, 문서 서비스 및 기타 처리 활동 사용)하지 마십시오. 콘텐츠를 작성하는 데 사용되는 AEM Forms 서버에 대해 트랜잭션 기록을 비활성화합니다. 문서 처리에 사용되는 AEM Forms 서버에 대해 트랜잭션 기록을 활성화 상태로 유지합니다.

![sample-transaction-report-author-1](assets/sample-transaction-report-author-1.png)

트랜잭션은 지정된 기간(버퍼 초기화 시간 + 역방향 복제 시간) 동안 버퍼에 남아 있습니다. 기본적으로 거래 수가 거래 보고서에 반영되는 데 약 90초가 소요됩니다.

PDF 양식 제출, 에이전트 UI를 사용하여 대화형 통신 미리 보기 또는 비표준 양식 제출 방법과 같은 작업은 트랜잭션으로 간주되지 않습니다. AEM Forms은 이러한 트랜잭션을 기록하는 API를 제공합니다. 사용자 지정 구현에서 API를 호출하여 트랜잭션을 기록합니다.

## 지원되는 토폴로지 {#supported-topology}

거래 보고서는 OSGi 환경의 AEM Forms에서만 사용할 수 있습니다. 작성자-게시, 작성자-처리-게시 및 처리 토폴로지만 지원합니다. 예를 들어 토폴로지는 [AEM Forms의 아키텍처 및 배포 토폴로지](../../forms/using/transaction-reports-overview.md)를 참조하십시오.

트랜잭션 수는 게시 인스턴스에서 작성자 또는 처리 인스턴스로 역복제됩니다. 표시된 작성자-게시 토폴로지는 아래에 표시됩니다.

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms 트랜잭션 보고서는 게시 인스턴스만 포함하는 토폴로지를 지원하지 않습니다.

### 거래 보고서 사용 지침 {#guidelines-for-using-transaction-reports}

* 작성자 인스턴스에 대한 보고서에는 작성 활동 중에 등록된 트랜잭션이 포함되므로 모든 작성자 인스턴스에서 트랜잭션 보고서를 비활성화합니다.
* 작성자 인스턴스에서 **게시만 트랜잭션 표시** 옵션을 활성화하여 모든 게시 인스턴스의 누적 트랜잭션을 봅니다. 각 게시 인스턴스의 트랜잭션 보고서를 해당 특정 게시 인스턴스의 실제 트랜잭션에 대해서만 볼 수도 있습니다.
* 작성자 인스턴스를 사용하여 워크플로우를 실행하고 문서를 처리하지 마십시오.
* 트랜잭션 보고를 사용하기 전에 게시 서버에 대한 토폴로지가 있는 경우 모든 게시 인스턴스에 대해 역방향 복제가 활성화되어 있는지 확인하십시오.
* 트랜잭션 데이터는 게시 인스턴스에서 해당 작성자 또는 처리 인스턴스로만 역복제됩니다. 작성자 또는 처리 인스턴스는 데이터를 다른 인스턴스로 더 이상 복제할 수 없습니다. 예를 들어 작성자-처리-게시 토폴로지가 있는 경우 집계된 트랜잭션 데이터는 처리 인스턴스에만 복제됩니다.

## 관련 문서 {#related-articles}

* [OSGi에서 AEM Forms에 대한 거래 보고서 보기 및 이해](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [OSGi의 AEM Forms에 대한 거래 보고서 청구 가능 API](../../forms/using/transaction-reports-billable-apis.md)
* [OSGi에서 AEM Forms에 대한 사용자 지정 구현에 대한 트랜잭션을 기록합니다](/help/forms/using/record-transaction-custom-implementation.md)
