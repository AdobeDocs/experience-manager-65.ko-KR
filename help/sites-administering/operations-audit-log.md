---
title: AEM 6의 감사 로그 유지 관리
description: Adobe Experience Manager(AEM)의 감사 로그 유지 관리에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 1e05faf5-619a-4ea3-acbf-2fd37c71e6d2
feature: Operations
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 1%

---

# AEM 6의 감사 로그 유지 관리{#audit-log-maintenance-in-aem}

감사 로깅에 적합한 AEM 이벤트는 많은 보관된 데이터를 생성합니다. 이 데이터는 복제, 에셋 업로드 및 기타 시스템 활동으로 인해 시간이 지남에 따라 빠르게 증가할 수 있습니다.

감사 로그 유지 관리에는 특정 정책에 따라 감사 로그 유지 관리를 자동화할 수 있는 몇 가지 기능이 포함되어 있습니다.

구성 가능한 주별 유지 관리 작업으로 구현되며 Operations Dashboard 모니터링 콘솔을 통해 액세스할 수 있습니다.

자세한 내용은 [작업 대시보드 설명서](/help/sites-administering/operations-dashboard.md).

감사 로그 제거 옵션에는 세 가지 유형이 있습니다.

1. [페이지 감사 로그 삭제](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [DAM 감사 로그 삭제](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [복제 감사 로그 제거](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

AEM 웹 콘솔에서 규칙을 만들어 각 규칙을 구성할 수 있습니다. 구성이 완료되면 다음 위치로 이동하여 트리거할 수 있습니다. **도구 - 작업 - 유지 관리 - 주간 유지 관리 창** 및 실행 **AuditLog 관리 작업**.

## 페이지 감사 로그 삭제 구성 {#configure-page-audit-log-purging}

다음 단계에 따라 감사 로그 삭제를 구성합니다.

1. 브라우저를 가리켜서 웹 콘솔 관리자로 이동합니다. `http://localhost:4502/system/console/configMgr/`

1. 라는 항목 검색 **페이지 감사 로그 제거 규칙** 을(를) 클릭합니다.

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. 그런 다음 요구 사항에 따라 제거 스케줄러를 구성합니다. 사용 가능한 옵션은 다음과 같습니다.

   * **규칙 이름:** 감사 정책 규칙 이름;
   * **컨텐츠 경로:** 규칙이 적용될 콘텐츠의 경로;
   * **최소 연령:** 감사 로그를 보관해야 하는 시간(일)
   * **감사 로그 유형:** 제거해야 하는 감사 로그 유형입니다.

   >[!NOTE]
   >
   >콘텐츠 경로는 의 하위 항목에만 적용됩니다. `/var/audit/com.day.cq.wcm.core.page` 노드의 형식입니다.

1. 규칙을 저장합니다.
1. 규칙을 실행하려면 만든 규칙을 작업 대시보드에 표시해야 합니다. 이렇게 하려면 **도구 - 작업 - 유지 관리** AEM 시작 화면에서 다음을 수행합니다.

1. 누르기 **주간 유지 관리 창** 카드.

1. 다음 아래에 이미 있는 유지 관리 작업을 찾을 수 있습니다. **AuditLog 관리 작업** 카드.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 다음 실행 날짜를 검사하거나 구성하거나 재생 버튼을 눌러 수동으로 실행할 수 있습니다.

AEM 6.3에서 감사 로그 제거 작업이 완료되기 전에 예약된 유지 관리 창이 닫히면 작업이 자동으로 중지됩니다. 다음 유지 관리 창이 열리면 다시 시작됩니다.

**AEM 6.5 사용**&#x200B;를 클릭하고, 실행 중인 감사 로그 제거 작업을 수동으로 중지할 수 있습니다. **중지** 아이콘. 다음 실행 시 작업이 안전하게 재개됩니다.

>[!NOTE]
>
>유지 관리 작업을 중지하는 것은 이미 진행 중인 작업의 추적을 잃지 않고 실행을 중지하는 것을 의미합니다.

## DAM 감사 로그 삭제 구성 {#configure-dam-audit-log-purging}

1. 다음 위치에서 시스템 콘솔로 이동합니다. *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. 검색 대상 **DAM 감사 로그 삭제** 규칙을 지정하고 결과를 클릭합니다.
1. 다음 창에서 그에 따라 규칙을 구성합니다. 옵션은 다음과 같습니다.

   * **규칙 이름:** 감사 정책 규칙 이름;
   * **컨텐츠 경로:** 규칙이 적용될 콘텐츠의 경로
   * **최소 연령:** 감사 로그를 보관해야 하는 시간(일)
   * **감사 로그 Dam 이벤트 유형:** 제거해야 하는 DAM 감사 이벤트 유형.

1. 클릭 **저장** 구성을 저장하려면

## 복제 감사 로그 삭제 구성  {#configure-replication-audit-log-purging}

1. 다음 위치에서 시스템 콘솔로 이동합니다. *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. 검색 대상 **복제 감사 로그 제거 스케줄러** 결과를 클릭합니다.
1. 다음 창에서 그에 따라 규칙을 구성합니다. 옵션은 다음과 같습니다.

   * **규칙 이름:** 감사 정책 규칙 이름
   * **컨텐츠 경로:** 규칙이 적용될 콘텐츠의 경로
   * **최소 연령:** 감사 로그를 보관해야 하는 시간(일)
   * **감사 로그 복제 이벤트 유형:** 제거해야 하는 복제 감사 이벤트 유형

1. 클릭 **저장** 구성을 저장합니다.
