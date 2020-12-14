---
title: 거래 보고서 개요
seo-title: 거래 보고서 개요
description: 제출된 모든 양식, 인터랙티브한 커뮤니케이션을 렌더링한 문서, 한 포맷으로 변환된 문서 등
seo-description: 제출된 모든 양식, 인터랙티브한 커뮤니케이션을 렌더링한 문서, 한 포맷으로 변환된 문서 등
uuid: 2c3dc1f3-5bbf-4aab-aa84-7aef5aabadf6
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b2c09e6b-a1d8-4b30-af2c-988442a3a986
docset: aem65
translation-type: tm+mt
source-git-commit: 8f90dc4865126d52e04effc9197ef7145b1a167e
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---


# 거래 보고서 개요{#transaction-reports-overview}

## 소개 {#introduction}

AEM Forms의 트랜잭션 보고서를 사용하면 AEM Forms 배포의 지정된 날짜 이후 발생한 모든 트랜잭션 수를 유지할 수 있습니다. 목표는 제품 사용에 대한 정보를 제공하고 비즈니스 이해 관계자가 자신의 디지털 처리 용량을 이해할 수 있도록 돕는 것입니다. 트랜잭션의 예는 다음과 같습니다.

* 적응형 양식, HTML5 양식 또는 양식 세트 제출
* 인터랙티브 커뮤니케이션의 인쇄 또는 웹 버전 변환
* 한 파일 형식에서 다른 파일 형식으로 문서 변환

거래로 간주되는 사항에 대한 자세한 내용은 [청구 가능한 API](../../forms/using/transaction-reports-billable-apis.md)를 참조하십시오.

기본적으로 트랜잭션 기록이 비활성화됩니다. AEM 웹 콘솔에서 [거래 기록](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports)을 활성화할 수 있습니다. 작성, 처리 또는 게시 인스턴스에 대한 거래 보고서를 볼 수 있습니다. 모든 트랜잭션의 합계값에 대한 작성자 또는 처리 인스턴스에 대한 거래 보고서를 봅니다. 보고서가 실행되는 게시 인스턴스에서만 발생하는 모든 트랜잭션 수에 대한 게시 인스턴스의 트랜잭션 보고서를 봅니다.

동일한 AEM 인스턴스에서 내용을 작성(적응형 양식, 인터랙티브 커뮤니케이션, 테마 및 기타 제작 활동 작성)하고 문서를 처리(워크플로우, 문서 서비스 및 기타 처리 활동 사용)하지 마십시오. 컨텐츠를 작성하는 데 사용되는 AEM Forms 서버에 대해 트랜잭션 기록을 사용하지 않도록 설정합니다. 문서를 처리하는 데 사용되는 AEM Forms 서버에 대해 트랜잭션 기록을 사용하도록 유지합니다.

![sample-transaction-report-author-1](assets/sample-transaction-report-author-1.png)

트랜잭션은 지정된 기간 동안 버퍼에 남아 있습니다(플러시 버퍼 시간 + 역방향 복제 시간). 기본적으로 트랜잭션 수가 트랜잭션 보고서에 반영되는 데 약 90초가 소요됩니다.

PDF 양식 제출, 에이전트 UI를 사용하여 대화형 통신을 미리 보거나, 비표준 양식 제출 방법 사용과 같은 작업은 거래로 간주되지 않습니다. AEM Forms은 이러한 트랜잭션을 기록할 API를 제공합니다. 사용자 지정 구현에서 API를 호출하여 트랜잭션을 기록합니다.

## 지원되는 토폴로지 {#supported-topology}

거래 보고서는 OSGi 환경의 AEM Forms에서만 사용할 수 있습니다. 이 플러그인은 작성자 게시, 작성자 처리 게시 및 처리 토폴로지만 지원합니다. 예를 들어 토폴로지를 보려면 [AEM Forms](../../forms/using/transaction-reports-overview.md)용 아키텍처 및 배포 토폴로지를 참조하십시오.

트랜잭션 수는 게시 인스턴스에서 작성자 또는 처리 인스턴스로 역복제됩니다. 아래 표시된 작성자 게시 토폴로지가 표시됩니다.

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms 트랜잭션 보고서는 게시 인스턴스만 포함하는 토폴로지를 지원하지 않습니다.

### 거래 보고서 사용 지침 {#guidelines-for-using-transaction-reports}

* 작성 활동 동안 등록된 트랜잭션이 작성자 인스턴스의 보고서에 포함되므로 모든 작성 인스턴스에서 거래 보고서를 비활성화합니다.
* 모든 게시 인스턴스의 누적 트랜잭션을 보려면 작성자 인스턴스에서 **게시 전용** 트랜잭션의 표시 옵션을 활성화합니다. 특정 게시 인스턴스에서만 실제 거래에 대한 각 게시 인스턴스의 거래 보고서를 볼 수도 있습니다.
* 작성 인스턴스를 사용하여 워크플로우를 실행하고 문서를 처리하지 마십시오.
* 트랜잭션 보고를 사용하기 전에 게시 서버가 있는 토폴로지가 있으면 모든 게시 인스턴스에 대해 역 복제가 활성화되어 있는지 확인하십시오.
* 트랜잭션 데이터는 게시 인스턴스에서 해당 작성자 또는 처리 인스턴스로만 역복제됩니다. 작성자 또는 처리 인스턴스는 데이터를 다른 인스턴스에 더 복제할 수 없습니다. 예를 들어 작성자 처리 게시 토폴로지가 있는 경우 집계된 트랜잭션 데이터는 처리 인스턴스에만 복제됩니다.

## 관련 문서 {#related-articles}

* [거래 보고서 보기 및 이해](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [거래 보고서 청구 가능한 API](../../forms/using/transaction-reports-billable-apis.md)
* [사용자 지정 구현에 대한 거래 기록](/help/forms/using/record-transaction-custom-implementation.md)

