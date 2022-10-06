---
title: 트랜잭션 보고서 개요
seo-title: Transaction Reports Overview
description: 제출된 모든 양식, 대화형 커뮤니케이션이 렌더링되고 문서가 다른 형식으로 변환되는 등의 개수를 유지합니다
seo-description: Keep a count of all the forms submitted, interactive communication rendered, Documents converted to one format to another, and more
uuid: 2c3dc1f3-5bbf-4aab-aa84-7aef5aabadf6
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b2c09e6b-a1d8-4b30-af2c-988442a3a986
docset: aem65
exl-id: bb812614-f4d8-4f57-bea2-8f7d31457039
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# 트랜잭션 보고서 개요{#transaction-reports-overview}

## 소개 {#introduction}

AEM Forms의 트랜잭션 보고서를 사용하면 AEM Forms 배포에 지정된 날짜 이후 발생한 모든 트랜잭션 수를 유지할 수 있습니다. 목표는 제품 사용에 대한 정보를 제공하고 비즈니스 이해 관계자가 디지털 처리 볼륨을 이해하도록 돕는 것입니다. 거래의 예는 다음과 같습니다.

* 적응형 양식, HTML5 양식 또는 양식 세트 제출
* 대화형 커뮤니케이션의 인쇄 또는 웹 버전 변환
* 한 파일 형식에서 다른 파일 형식으로 문서 변환

거래로 간주되는 사항에 대한 자세한 내용은 [청구 가능한 API](../../forms/using/transaction-reports-billable-apis.md).

트랜잭션 기록은 기본적으로 비활성화되어 있습니다. 다음을 수행할 수 있습니다 [트랜잭션 기록 활성화](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) AEM 웹 콘솔에서 게시할 수 있습니다. 작성자, 처리 또는 게시 인스턴스에 대해 트랜잭션 보고서를 볼 수 있습니다. 모든 트랜잭션에 대한 합계로서 작성 또는 처리 인스턴스에 대한 트랜잭션 보고서 보기. 보고서가 실행되는 해당 게시 인스턴스에서만 발생하는 모든 트랜잭션 수에 대한 게시 인스턴스의 트랜잭션 보고서를 봅니다.

동일한 AEM 인스턴스에서 컨텐츠 작성(적응형 양식, 대화형 커뮤니케이션, 테마 및 기타 작성 활동 만들기)과 문서 처리(워크플로우, 문서 서비스 및 기타 처리 활동 사용)를 수행하지 마십시오. 컨텐츠를 작성하는 데 사용되는 AEM Forms 서버에 대해 트랜잭션 기록을 비활성화하지 않도록 유지합니다. 문서를 처리하는 데 사용되는 AEM Forms 서버에 대해 트랜잭션 기록을 사용하도록 유지합니다.

![sample-transaction-report-author-1](assets/sample-transaction-report-author-1.png)

트랜잭션이 지정된 기간(플러시 버퍼 시간 + 역방향 복제 시간) 동안 버퍼에 남아 있습니다. 기본적으로 트랜잭션 수가 트랜잭션 보고서에 반영되려면 약 90초가 걸립니다.

PDF 양식 제출, 에이전트 UI를 사용하여 대화형 커뮤니케이션을 미리 보거나 비표준 양식 제출 방법 사용과 같은 작업은 트랜잭션으로 간주되지 않습니다. AEM Forms은 이러한 트랜잭션을 기록할 API를 제공합니다. 사용자 지정 구현에서 API를 호출하여 트랜잭션을 기록합니다.

## 지원되는 토폴로지 {#supported-topology}

거래 보고서는 OSGi 환경의 AEM Forms에서만 사용할 수 있습니다. 이 보고서는 작성자 게시, 작성자 처리-게시 및 처리 토폴로지만 지원합니다. 예를 들어 토폴로지는 [AEM Forms을 위한 아키텍처 및 배포 토폴로지](../../forms/using/transaction-reports-overview.md).

트랜잭션 수가 게시 인스턴스에서 작성자 또는 처리 인스턴스로 다시 복제됩니다. 아래에는 암시적인 작성자 게시 토폴로지가 표시됩니다.

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms 트랜잭션 보고서는 게시 인스턴스만 포함하는 토폴로지를 지원하지 않습니다.

### 트랜잭션 보고서 사용 지침 {#guidelines-for-using-transaction-reports}

* 작성 활동의 보고서에 작성 활동 중에 등록된 트랜잭션이 포함되므로 모든 작성 인스턴스에서 트랜잭션 보고서를 비활성화합니다.
* 를 활성화합니다 **게시 상태의 트랜잭션만 표시** 모든 게시 인스턴스에서 누적 트랜잭션을 볼 수 있는 작성자 인스턴스의 옵션입니다. 각 게시 인스턴스에서 해당 특정 게시 인스턴스에서만 실제 트랜잭션에 대한 트랜잭션 보고서를 볼 수도 있습니다.
* 워크플로우 실행 및 문서 처리에 작성자 인스턴스를 사용하지 마십시오.
* 트랜잭션 보고를 사용하기 전에 게시 서버가 있는 토폴로지가 있으면 모든 게시 인스턴스에 대해 역방향 복제가 활성화되어 있는지 확인하십시오.
* 트랜잭션 데이터가 게시 인스턴스에서 해당 작성자 또는 처리 인스턴스로만 역복제됩니다. 작성자 또는 처리 인스턴스는 다른 인스턴스에 데이터를 더 이상 복제할 수 없습니다. 예를 들어 작성자 처리-게시 토폴로지가 있는 경우 집계된 트랜잭션 데이터는 처리 인스턴스에만 복제됩니다.

## 관련 문서 {#related-articles}

* [트랜잭션 보고서 보기 및 이해](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [거래 보고서 청구 가능한 API](../../forms/using/transaction-reports-billable-apis.md)
* [사용자 지정 구현에 대한 거래 기록](/help/forms/using/record-transaction-custom-implementation.md)
