---
title: AEM 6의 감사 로그 유지 관리
seo-title: AEM 6의 감사 로그 유지 관리
description: AEM의 감사 로그 유지 관리에 대해 알아봅니다.
seo-description: AEM의 감사 로그 유지 관리에 대해 알아봅니다.
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
exl-id: 1e05faf5-619a-4ea3-acbf-2fd37c71e6d2
feature: 작업
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---

# AEM 6의 감사 로그 유지 관리{#audit-log-maintenance-in-aem}

감사 로깅의 자격을 갖춘 AEM 이벤트에서 아카이브된 데이터가 많이 생성됩니다. 복제, 자산 업로드 및 기타 시스템 작업으로 인해 시간이 지남에 따라 이 데이터가 빠르게 증가할 수 있습니다.

감사 로그 유지 관리에는 특정 정책에 따라 감사 로그 유지 관리를 자동화할 수 있는 몇 가지 기능이 포함되어 있습니다.

구성 가능한 주별 유지 관리 작업으로 구현되며 Operations Dashboard 모니터링 콘솔을 통해 액세스할 수 있습니다.

자세한 내용은 [작업 대시보드 설명서](/help/sites-administering/operations-dashboard.md)를 참조하십시오.

감사 로그 삭제 옵션에는 3가지 유형이 있습니다.

1. [페이지 감사 로그 삭제](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [DAM 감사 로그 제거](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [복제 감사 로그 사용 중](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

각 구성 요소는 AEM 웹 콘솔에서 규칙을 만들어 구성할 수 있습니다. 구성한 후에는 **도구 - 작업 - 유지 관리 - 주별 유지 관리 창**&#x200B;으로 이동하여 **감사 로그 유지 관리 작업**&#x200B;을 실행하여 트리거할 수 있습니다.

## 페이지 감사 로그 삭제 구성 {#configure-page-audit-log-purging}

감사 로그 제거를 구성하려면 다음 단계를 수행합니다.

1. 브라우저를 `http://localhost:4502/system/console/configMgr/`으로 가리켜 웹 콘솔 관리자로 이동합니다.

1. **페이지 감사 로그 삭제 규칙**&#x200B;이라는 항목을 검색하고 클릭합니다.

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. 그런 다음 요구 사항에 따라 비우기 스케줄러를 구성합니다. 사용 가능한 옵션은 다음과 같습니다.

   * **규칙 이름:** 감사 정책 규칙의 이름;
   * **컨텐츠 경로:** 규칙이 적용될 컨텐츠의 경로;
   * **최소 연령:** 감사 로그를 보관해야 하는 일 수.
   * **감사 로그 유형:** 삭제할 감사 로그 유형입니다.

   >[!NOTE]
   >
   >컨텐츠 경로는 저장소의 `/var/audit/com.day.cq.wcm.core.page` 노드의 1차 하위 구성요소에만 적용됩니다.

1. 규칙을 저장합니다.
1. 방금 만든 규칙을 실행하려면 작업 대시보드에 표시해야 합니다. 이렇게 하려면 AEM 시작 화면에서 **도구 - 작업 - 유지 관리**&#x200B;로 이동합니다.

1. **주별 유지 관리 창** 카드를 누릅니다.

1. **AuditLog 유지 관리 작업** 카드에 유지 관리 작업이 이미 있습니다.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 다음 실행 날짜를 검사하거나, 구성하거나, 재생 단추를 눌러 수동으로 실행할 수 있습니다.

AEM 6.3에서는 감사 로그 삭제 작업이 완료되기 전에 예약된 유지 관리 창이 닫히면 작업이 자동으로 중지됩니다. 다음 유지 관리 창이 열리면 다시 시작됩니다.

**AEM 6.5에서는** 중지 아이콘을 클릭하여 실행 중인 감사 로그 삭제 작업을 수동으로 중지할 수  **** 있습니다. 다음 실행 시 작업이 안전하게 다시 시작됩니다.

>[!NOTE]
>
>유지 관리 작업을 중지하려면 이미 진행 중인 작업의 추적을 손실하지 않고 실행을 일시 중단하는 것입니다.

## DAM 감사 로그 삭제 구성 {#configure-dam-audit-log-purging}

1. *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*&#x200B;의 시스템 콘솔로 이동합니다.
1. **DAM 감사 로그 삭제** 규칙을 검색하고 결과를 클릭합니다.
1. 다음 창에서 이에 따라 규칙을 구성합니다. 옵션은 다음과 같습니다.

   * **규칙 이름:** 감사 정책 규칙의 이름;
   * **컨텐츠 경로:** 규칙이 적용될 컨텐츠의 경로
   * **최소 연령:** 감사 로그를 보관해야 하는 일 수
   * **감사 로그 Dam 이벤트 유형:** 제거해야 하는 DAM 감사 이벤트 유형.

1. **저장**&#x200B;을 클릭하여 구성을 저장합니다.

## 복제 감사 로그 제거 구성 {#configure-replication-audit-log-purging}

1. *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*&#x200B;의 시스템 콘솔로 이동합니다.
1. **복제 감사 로그 삭제 스케줄러**&#x200B;를 검색하고 결과를 클릭합니다.
1. 다음 창에서 이에 따라 규칙을 구성합니다. 옵션은 다음과 같습니다.

   * **규칙 이름:** 감사 정책 규칙의 이름
   * **컨텐츠 경로:** 규칙이 적용될 컨텐츠의 경로
   * **최소 연령:** 감사 로그를 보관해야 하는 일 수
   * **감사 로그 복제 이벤트 유형:** 삭제할 복제 감사 이벤트 유형

1. **저장**&#x200B;을 클릭하여 구성을 저장합니다.
