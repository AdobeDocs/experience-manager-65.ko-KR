---
title: 거래 보고서 개요
seo-title: Transaction Reports Overview
description: 제출된 모든 양식, 렌더링된 대화형 통신, 한 형식으로 변환된 문서 등의 수를 유지합니다.
seo-description: Keep a count of all the forms submitted, interactive communication rendered, Documents converted to one format to another, and more
uuid: 2c3dc1f3-5bbf-4aab-aa84-7aef5aabadf6
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b2c09e6b-a1d8-4b30-af2c-988442a3a986
docset: aem65
exl-id: bb812614-f4d8-4f57-bea2-8f7d31457039
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# 거래 보고서 개요{#transaction-reports-overview}

## 소개 {#introduction}

AEM Forms의 트랜잭션 보고서를 사용하면 AEM Forms 배포에서 지정된 날짜 이후 발생한 모든 트랜잭션의 수를 유지할 수 있습니다. 제품 사용에 대한 정보를 제공하고 비즈니스 이해 당사자가 디지털 처리 볼륨을 이해할 수 있도록 지원하는 것이 목표입니다. 거래의 예는 다음과 같습니다.

* 적응형 양식, HTML5 양식 또는 양식 세트 제출
* 대화형 통신의 인쇄 또는 웹 버전 렌디션
* 한 파일 형식에서 다른 파일 형식으로 문서 변환

거래로 간주되는 항목에 대한 자세한 내용은 [청구 가능 API](../../forms/using/transaction-reports-billable-apis.md).

거래 기록은 기본적으로 비활성화되어 있습니다. 다음을 수행할 수 있습니다. [트랜잭션 기록 활성화](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) AEM 웹 콘솔에서 가져왔습니다. 작성자, 처리 또는 게시 인스턴스에 대한 거래 보고서를 볼 수 있습니다. 작성자 또는 처리 인스턴스에 대한 모든 트랜잭션의 집계된 합계에 대한 트랜잭션 보고서를 봅니다. 보고서가 실행되는 게시 인스턴스에서만 수행되는 모든 트랜잭션의 수에 대한 게시 인스턴스의 트랜잭션 보고서를 봅니다.

동일한 AEM 인스턴스에서 콘텐츠를 작성(적응형 양식, 대화형 통신, 테마 및 기타 작성 활동 만들기)하고 문서를 처리(워크플로, 문서 서비스 및 기타 처리 활동 사용)하지 마십시오. 콘텐츠를 작성하는 데 사용되는 AEM Forms 서버에 대해 트랜잭션 기록을 비활성화합니다. 문서 처리에 사용되는 AEM Forms 서버에 대해 트랜잭션 기록을 활성화 상태로 유지합니다.

![sample-transaction-report-author-1](assets/sample-transaction-report-author-1.png)

트랜잭션은 지정된 기간(버퍼 초기화 시간 + 역방향 복제 시간) 동안 버퍼에 남아 있습니다. 기본적으로 거래 수가 거래 보고서에 반영되는 데 약 90초가 소요됩니다.

PDF 양식 제출, 에이전트 UI를 사용하여 대화형 통신 미리 보기 또는 비표준 양식 제출 방법과 같은 작업은 트랜잭션으로 간주되지 않습니다. AEM Forms은 이러한 트랜잭션을 기록하는 API를 제공합니다. 사용자 지정 구현에서 API를 호출하여 트랜잭션을 기록합니다.

## 지원되는 토폴로지 {#supported-topology}

거래 보고서는 OSGi 환경의 AEM Forms에서만 사용할 수 있습니다. 작성자-게시, 작성자-처리-게시 및 처리 토폴로지만 지원합니다. 예를 들어 토폴로지는 [AEM Forms의 아키텍처 및 배포 토폴로지](../../forms/using/transaction-reports-overview.md).

트랜잭션 수는 게시 인스턴스에서 작성자 또는 처리 인스턴스로 역복제됩니다. 표시된 작성자-게시 토폴로지는 아래에 표시됩니다.

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms 트랜잭션 보고서는 게시 인스턴스만 포함하는 토폴로지를 지원하지 않습니다.

### 거래 보고서 사용 지침 {#guidelines-for-using-transaction-reports}

* 작성자 인스턴스에 대한 보고서에는 작성 활동 중에 등록된 트랜잭션이 포함되므로 모든 작성자 인스턴스에서 트랜잭션 보고서를 비활성화합니다.
* 활성화 **게시의 트랜잭션만 표시** 모든 게시 인스턴스의 누적 트랜잭션을 볼 수 있는 작성자 인스턴스의 옵션입니다. 각 게시 인스턴스의 트랜잭션 보고서를 해당 특정 게시 인스턴스의 실제 트랜잭션에 대해서만 볼 수도 있습니다.
* 작성자 인스턴스를 사용하여 워크플로우를 실행하고 문서를 처리하지 마십시오.
* 트랜잭션 보고를 사용하기 전에 게시 서버에 대한 토폴로지가 있는 경우 모든 게시 인스턴스에 대해 역방향 복제가 활성화되어 있는지 확인하십시오.
* 트랜잭션 데이터는 게시 인스턴스에서 해당 작성자 또는 처리 인스턴스로만 역복제됩니다. 작성자 또는 처리 인스턴스는 데이터를 다른 인스턴스로 더 이상 복제할 수 없습니다. 예를 들어 작성자-처리-게시 토폴로지가 있는 경우 집계된 트랜잭션 데이터는 처리 인스턴스에만 복제됩니다.

## 관련 문서 {#related-articles}

* [거래 보고서 보기 및 이해](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [거래 보고서 청구 가능 API](../../forms/using/transaction-reports-billable-apis.md)
* [사용자 지정 구현에 대한 트랜잭션 기록](/help/forms/using/record-transaction-custom-implementation.md)
