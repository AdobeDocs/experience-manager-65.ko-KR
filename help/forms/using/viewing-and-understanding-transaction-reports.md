---
title: 거래 보고서 보기 및 이해
description: 트랜잭션 보고서를 사용하여 제품 사용과 하드웨어 및 소프트웨어에 대한 투자 재조정에 대해 정보에 입각한 결정을 내릴 수 있습니다.
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 3c7cbe1f-ac81-4df9-96b2-662cbc5f2075
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# 거래 보고서 보기 및 이해{#viewing-and-understanding-transaction-reports}

트랜잭션 보고서를 사용하여 제출된 양식, 처리된 문서 및 렌더링된 문서의 수를 캡처하고 추적할 수 있습니다. 이러한 거래를 추적하는 목적은 제품 사용과 하드웨어 및 소프트웨어에 대한 투자 재조정에 대한 정보에 입각한 결정을 내리는 것입니다. 자세한 내용은 [AEM Forms 거래 보고서 개요](../../forms/using/transaction-reports-overview.md).

## 거래 보고서 설정  {#setting-up-transaction-reports}

트랜잭션 보고서 기능은 AEM Forms 추가 기능 패키지의 일부로 사용할 수 있습니다. 모든 작성자 및 게시 인스턴스에 추가 기능 패키지를 설치하는 방법에 대한 자세한 내용은 [AEM Forms 설치 및 구성](/help/forms/using/installing-configuring-aem-forms-osgi.md). AEM Forms 추가 기능 패키지가 설치되면 다음을 수행합니다.

* 모든 게시 인스턴스에서 역방향 복제 활성화
* 거래 보고서 활성화
* 거래 보고서를 볼 수 있는 권한 제공
* (선택 사항) 트랜잭션 플러시 기간 및 보낼 편지함 구성 [](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* AEM Forms 트랜잭션 보고서는 게시 인스턴스만 포함하는 토폴로지를 지원하지 않습니다.
>* 트랜잭션 보고를 사용하기 전에 모든 게시 인스턴스에 대해 역방향 복제가 활성화되어 있는지 확인하십시오.
>* 트랜잭션 데이터는 게시 인스턴스에서 해당 작성자 또는 처리 인스턴스로만 역복제됩니다. 작성자 또는 처리 인스턴스는 데이터를 다른 인스턴스로 더 이상 복제할 수 없습니다.
>

### 모든 게시 인스턴스에서 역방향 복제 활성화 {#enable-reverse-replication-on-all-the-publish-instances}

트랜잭션 보고서는 역방향 복제를 사용하여 게시 인스턴스의 트랜잭션 수를 작성자 인스턴스로 통합합니다. 모든 게시 인스턴스에 대해 역방향 복제를 설정합니다. 역방향 복제를 설정하는 자세한 지침은 [복제](/help/sites-deploying/replication.md).

### 거래 보고서 활성화 {#enable-transaction-reports}

거래 보고서는 기본적으로 비활성화되어 있습니다. AEM 웹 콘솔에서 보고서를 활성화할 수 있습니다. AEM Forms 환경에서 트랜잭션 보고서를 활성화하려면 모든 작성자 및 게시 인스턴스에서 다음 단계를 수행합니다.

1. 관리자로 AEM 인스턴스에 로그인합니다. 다음으로 이동 **도구** > **작업** > **웹 콘솔**.
1. 을(를) 찾아 엽니다. **Forms 거래 보고** 서비스.
1. 트랜잭션 기록 체크박스를 선택합니다. **저장**&#x200B;을 클릭합니다.

   모든 작성 및 게시 인스턴스에서 1~3단계를 반복합니다.

### 거래 보고서를 볼 수 있는 권한 제공 {#provide-rights-to-view-a-transaction-report}

fd-administrator 그룹의 멤버만 트랜잭션 보고서를 볼 수 있습니다. 사용자가 거래 보고서를 볼 수 있도록 하려면 사용자를 fd-administrator 그룹의 구성원으로 설정합니다. 사용자를 AEM 그룹의 구성원으로 만드는 방법에 대한 지침은 [사용자, 그룹 및 액세스 권한 관리](/help/sites-administering/user-group-ac-admin.md).

### (선택 사항) 트랜잭션 플러시 기간 및 보낼 편지함 구성 {#optional-configure-transaction-flush-period-and-outboxes}

트랜잭션은 저장소에 저장되기 전에 메모리에 캐시됩니다. 저장소에 자주 쓰지 않도록 하기 위해 프로세스가 수행됩니다. 기본적으로 캐싱 기간(트랜잭션 플러시 기간)은 60초로 설정됩니다. 사용자 환경에 맞게 기본 기간을 변경할 수 있습니다. 기본 캐싱 기간을 변경하려면 다음 단계를 수행하십시오.

1. 작성자 인스턴스에 관리자로 로그인합니다. 다음으로 이동 **도구** > **작업** > **웹 콘솔**.
1. 을(를) 찾아 엽니다. **Forms 트랜잭션 저장소 저장소 저장소 공급자** 서비스.
1. 에서 초 수를 지정합니다. **트랜잭션 플러시 기간** 필드. **저장**&#x200B;을 클릭합니다.

역방향 복제는 트랜잭션 데이터를 작성자 인스턴스의 기본 보낼 편지함으로 복사합니다. 사용자 지정 보낼 편지함에 트랜잭션 데이터를 넣을 수 있습니다. 사용자 지정 보낼 편지함을 지정하려면 다음 단계를 수행하십시오.

1. 작성자 인스턴스에 관리자로 로그인합니다. 다음으로 이동 **도구** > **작업** > **웹 콘솔**.
1. 을(를) 찾아 엽니다. **Forms 트랜잭션 저장소 저장소 저장소 공급자** 서비스.
1. 사용자 지정 보낼 편지함의 이름 지정 **보낼 편지함** 필드. 클릭 **저장**. 지정된 이름의 보낼 편지함이 모든 작성자 인스턴스에 만들어집니다.

## 트랜잭션 보고서 보기 {#viewing-the-transaction-report}

작성자 또는 게시 인스턴스에서 거래 보고서를 볼 수 있습니다. 작성자 인스턴스의 트랜잭션 보고서는 구성된 작성자 및 게시 인스턴스에서 발생하는 모든 트랜잭션의 집계된 합계를 제공합니다. 게시 인스턴스의 트랜잭션 보고서는 기본 게시 인스턴스에서만 발생하는 트랜잭션 수를 제공합니다. 보고서를 보려면 다음 단계를 수행하십시오.

1. 다음 위치에서 AEM Forms 서버에 로그인 `https://[hostname]:'port'`.
1. 다음으로 이동 **도구** > **Forms**>**거래 보고서 보기**.

## 보고서 이해 {#understanding-the-report}

AEM Forms은 아래 요약 보고서에 표시된 대로 구성된 날짜 이후의 트랜잭션 보고서를 표시합니다.

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* 사용 **날짜를 오늘로 재설정** 트랜잭션 레코드를 재설정하는 옵션입니다. 날짜를 오늘로 재설정하면 모든 이전 거래 기록이 소실됩니다. 작성자 인스턴스에서 날짜를 재설정할 때 변경 사항이 게시 인스턴스의 트랜잭션 보고서에 영향을 주지 않으며 이와 반대로 영향을 주지 않습니다.
* 사용 **게시 인스턴스의 트랜잭션만 표시** 구성된 게시 인스턴스 또는 게시 팜에서만 발생한 모든 트랜잭션을 봅니다.
* 범주를 사용합니다. **문서 처리됨**, **렌더링된 문서**, 및 **Forms 제출됨** 를 클릭하여 해당 트랜잭션을 봅니다. 이러한 범주에 계상된 거래 유형에 대해서는 다음을 참조하십시오 [청구 가능 거래 보고서 API](../../forms/using/transaction-reports-billable-apis.md).

## 트랜잭션 보고 로그 보기 {#view-transaction-reporting-logs}

트랜잭션 보고는 보고서에 표시된 모든 정보와 일부 추가 정보를 로그에 표시합니다. 로그에 제공된 정보는 고급 사용자에게 유용합니다. 예를 들어 로그는 보고서에 표시된 세 개의 통합 범주와 비교하여 트랜잭션을 여러 개의 세분화된 범주로 나눕니다. 로그는 다음에서 사용할 수 있습니다. `error.log` 파일 위치: `/crx-repository/logs/` 디렉토리. AEM 웹 콘솔에서 트랜잭션 보고서를 활성화하지 않은 경우에도 로그를 사용할 수 있습니다.

## 관련 문서 {#related-articles}

* [거래 보고서 개요](../../forms/using/transaction-reports-overview.md)
* [거래 보고서 청구 가능 API](../../forms/using/transaction-reports-billable-apis.md)
* [사용자 지정 구현에 대한 트랜잭션 기록](/help/forms/using/record-transaction-custom-implementation.md)
