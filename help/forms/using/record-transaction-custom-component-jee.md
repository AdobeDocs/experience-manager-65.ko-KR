---
title: JEE의 AEM Forms에 대한 사용자 지정 구성 요소 API에 대한 트랜잭션을 기록합니다.
description: TransactionRecorder API를 사용하여 사용자 지정 구성 요소의 트랜잭션을 기록하는 방법에 대해 알아봅니다.
feature: Transaction Reports
exl-id: 33e1868a-2a7f-4785-8571-95651e661e21
role: Admin, User, Developer
solution: "Experience Manager, Experience Manager Forms"
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# JEE의 AEM Forms에 대한 사용자 지정 구성 요소 API에 대한 트랜잭션을 기록합니다 {#record-a-transaction-for-custom-components}

사용자 지정 구성 요소에서 청구 가능한 API를 사용하는 경우 구성 요소에 대해 거래 보고를 활성화할 수 있습니다. 트랜잭션 보고를 사용하려면 구성 요소의 `component.xml` 파일을 수정하고 트랜잭션 보고를 사용하도록 설정해야 하는 작업에 아래 지정된 태그를 추가하십시오.

**태그**: `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| 이전 작업 태그 | 새 작업 태그 |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

입력 카운트 수에 따라 거래 카운트가 달라지는 배치 API와 같이 API에 대해 두 개 이상의 거래를 캡처해야 하는 경우 API 레벨에서 거래 카운트를 처리합니다.

**다양한 트랜잭션 수를 기록하려면:**

1. 코드에서 클래스 `"com.adobe.idp.dsc.InvocationContextStack"`을(를) 가져옵니다. 클래스는 `adobe-livecycle-client.jar` sdk 파일의 일부입니다. sdk 파일은 `<AEM_Forms_JEE_Install>\sdk\client-libs\common`에서 사용할 수 있습니다.

   >[!NOTE]
   > 이미 번들로 제공되면 클라이언트 프로젝트에서 공유한 클라이언트 파일을 새 파일로 업데이트합니다.

1. 다양한 트랜잭션을 기록해야 하는 API에서 다음을 수행합니다.
   1. 트랜잭션 수를 `transaction_count`과(와) 같은 일부 정수 변수에 저장할 수 있도록 논리를 추가합니다.
   1. 작업이 완료되면 `InvocationContextStack.recordTransactionCount(transaction_count)`을(를) 추가하십시오.

<!--For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.-->

## 관련 문서

* [JEE에서 AEM Forms에 대한 거래 보고서 활성화 및 보기](/help/forms/using/transaction-report-overview-jee.md)
* [JEE의 AEM Forms에 대한 청구 가능 API 목록](/help/forms/using/transaction-reports-billable-apis-jee.md)
