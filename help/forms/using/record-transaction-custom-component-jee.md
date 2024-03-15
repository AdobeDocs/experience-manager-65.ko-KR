---
title: JEE의 AEM Forms에 대한 사용자 지정 구성 요소 API에 대한 트랜잭션을 기록합니다.
description: TransactionRecorder API를 사용하여 사용자 지정 구성 요소에 대한 트랜잭션을 기록합니다.
feature: Transaction Reports
source-git-commit: d0db00de6b767a12a9492bbbcec49a8c5d25ff27
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# JEE의 AEM Forms에 대한 사용자 지정 구성 요소 API에 대한 트랜잭션을 기록합니다 {#record-a-transaction-for-custom-components}

사용자 지정 구성 요소에서 청구 가능한 API를 사용하는 경우 구성 요소에 대한 트랜잭션 보고를 활성화할 수 있습니다. 트랜잭션 보고를 사용하려면 `component.xml` 구성 요소의 파일을 추가하고, 트랜잭션 보고를 활성화해야 하는 작업 아래에 지정된 태그를 추가합니다.

**태그**: `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| 이전 작업 태그 | 새 작업 태그 |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

거래 수가 입력 수 수에 따라 달라질 수 있는 배치 API의 경우 등 API에 대해 두 개 이상의 거래를 캡처해야 하는 요구 사항이 있는 경우 API 수준에서 거래 수를 처리해야 합니다. 다음은 가변 트랜잭션 수를 기록하는 단계입니다.

1. 클래스 가져오기 `"com.adobe.idp.dsc.InvocationContextStack"` 코드에서. 클래스는 `adobe-livecycle-client.jar` sdk 파일. sdk 파일은에서 사용할 수 있습니다. `<AEM_Forms_JEE_Install>\sdk\client-libs\common`

   >[!NOTE]
   > 이미 번들로 제공되면 클라이언트 프로젝트에서 위에서 공유한 클라이언트 파일을 새 파일로 업데이트합니다.

1. 다양한 트랜잭션을 기록해야 하는 API에서 다음을 수행합니다.
   1. 다음과 같은 일부 정수 변수에 트랜잭션 수를 저장하는 논리를 추가합니다. `transaction_count`.
   1. 작업이 성공하면 을(를) 추가합니다 `InvocationContextStack.recordTransactionCount(transaction_count)`.

<!--For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.-->

## 관련 문서

* [JEE의 AEM Forms에 대한 트랜잭션 보고서 활성화 및 보기](/help/forms/using/transaction-report-overview-jee.md)
* [JEE의 AEM Forms에 대한 청구 가능 API 목록](/help/forms/using/transaction-reports-billable-apis-jee.md)


