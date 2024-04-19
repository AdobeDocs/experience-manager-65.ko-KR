---
title: JEE의 AEM Forms에 대한 사용자 지정 구성 요소 API에 대한 트랜잭션을 기록합니다.
description: TransactionRecorder API를 사용하여 사용자 지정 구성 요소의 트랜잭션을 기록하는 방법에 대해 알아봅니다.
feature: Transaction Reports
exl-id: 33e1868a-2a7f-4785-8571-95651e661e21
source-git-commit: bf99ad3710638ec823d3b17967e1c750d0405c77
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# JEE의 AEM Forms에 대한 사용자 지정 구성 요소 API에 대한 트랜잭션을 기록합니다 {#record-a-transaction-for-custom-components}

사용자 지정 구성 요소에서 청구 가능한 API를 사용하는 경우 구성 요소에 대해 거래 보고를 활성화할 수 있습니다. 트랜잭션 보고를 사용하려면 `component.xml` 구성 요소의 파일을 추가하고, 트랜잭션 보고를 활성화해야 하는 작업 아래에 지정된 태그를 추가합니다.

**태그**: `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| 이전 작업 태그 | 새 작업 태그 |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

입력 카운트 수에 따라 거래 카운트가 달라지는 배치 API와 같이 API에 대해 두 개 이상의 거래를 캡처해야 하는 경우 API 레벨에서 거래 카운트를 처리합니다.

**가변 트랜잭션 수를 기록하려면**

1. 클래스 가져오기 `"com.adobe.idp.dsc.InvocationContextStack"` 코드에서. 클래스는 `adobe-livecycle-client.jar` sdk 파일. sdk 파일은에서 사용할 수 있습니다. `<AEM_Forms_JEE_Install>\sdk\client-libs\common`

   >[!NOTE]
   > 이미 번들로 제공되면 클라이언트 프로젝트에서 공유한 클라이언트 파일을 새 파일로 업데이트합니다.

1. 다양한 트랜잭션을 기록해야 하는 API에서 다음을 수행합니다.
   1. 다음과 같은 일부 정수 변수에 트랜잭션 수를 저장할 수 있도록 논리를 추가합니다. `transaction_count`.
   1. 작업이 성공하면 을(를) 추가합니다 `InvocationContextStack.recordTransactionCount(transaction_count)`.

<!--For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.-->

## 관련 문서

* [JEE에서 AEM Forms에 대한 거래 보고서 활성화 및 보기](/help/forms/using/transaction-report-overview-jee.md)
* [JEE의 AEM Forms에 대한 청구 가능 API 목록](/help/forms/using/transaction-reports-billable-apis-jee.md)
