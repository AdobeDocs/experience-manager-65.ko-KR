---
title: 사용자 지정 구현에 대한 거래 기록
seo-title: 사용자 지정 구현에 대한 거래 기록
description: TransactionRecorder API를 사용하여 트랜잭션에서 자동으로 계산되지 않는 작업을 기록합니다.
seo-description: TransactionRecorder API를 사용하여 트랜잭션에서 자동으로 계산되지 않는 작업을 기록합니다.
uuid: a22b1a0b-7553-4a17-8fb4-a3bee97b4a98
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 0d961630-573b-4c8e-902f-996f1d1265b6
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# 사용자 지정 구현에 대한 거래 기록 {#record-a-transaction-for-custom-implementations}

TransactionRecorder API를 사용하여 트랜잭션에서 자동으로 계산되지 않는 작업을 기록합니다.

사용자 정의 코드를 사용하여 PDF 양식을 제출하거나, 최종 사용자에게 에이전트 UI 미리 보기 URL을 전송하여 대화형 통신을 미리 보거나, AEM Forms에서 제공하는 제출 방법을 사용하는 대신 사용자 정의 방법을 사용하여 양식을 제출할 수 있습니다. 이전에 언급한 모든 작업 및 AEM Forms API의 사용자 지정 구현은 거래로 간주되지 않습니다. AEM Forms은 트랜잭션과 같은 작업을 기록하기 위해 [TransactionRecorder](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aem/transaction/core/ITransactionRecorder.html) API를 제공합니다.

트랜잭션을 기록하려면 [표준 sling servlet](https://helpx.adobe.com/experience-manager/using/custom-sling-servlets.html)을 작성하고 클라이언트에서 서블릿을 호출하여 트랜잭션을 기록합니다. AJAX 또는 다른 표준 방법을 사용하여 서블릿을 호출할 수 있습니다.

## 샘플 서버측 코드 {#sample-server-sided-code}

아래 샘플 코드를 사용하여 사용자 지정 OSGi 번들을 사용하여 JAVA 클래스에서 TransactionRecorder API를 실행할 수 있습니다.

```java
import com.adobe.aem.transaction.core.ITransactionRecorder;
import com.adobe.aem.transaction.core.model.TransactionRecord;
import com.adobe.aem.transaction.core.exception.TransactionException;
import com.adobe.aem.transaction.core.FormsTransactionConstants;

@Reference
private ITransactionRecorder transactionRecorder;

doPost (SlingHttpServletRequest request, SlingHttpServletResponse response) {
    transactionRecorder.startContext();
    TransactionRecord txRecord = extractTxRecordFromRequest(request); //extract transaction relevant data from request
    try {
        bool success = doBillableWork();
        if (success) {
            transactionRecorder.recordTransaction(txRecord);
        }
    } catch (Exception e) {
        //exception handling
    } finally {
        transactionRecorder.endContext();
    }
}

//Here, it is assumed that txInfo is passed in Stringified json form in the ajax call (in data parameter). You can pass txInfo from client in any way that you find suitable.
private TransactionRecord extractTxRecordFromRequest(SlingHttpServletRequest request) {
    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(request.getInputStream()));
    Map<String, Object> txDataMap = new HashMap<String, Object>();
    String txData = bufferedReader.readLine();
    JSONObject txInfo= new JSONObject(txData );
    try {
        String resourceType= txInfo.getString("resourceType");
        String transactionType = txInfo.getString("transactionType");
        Integer transactionCount = (Integer)txInfo.get("transactionCount");
        //Extract all the relevant tx record attributes similarly and pass them in Transaction Record constructor as per the java doc}
        return new TransactionRecord(transactionCount, transactionType, resourceType, ..);
    } catch (JSONException e) {
        //exception handling
    } finally {
        bufferedReader.close();
    }
}
```

## 샘플 클라이언트측 코드 {#sample-client-side-code}

아래 샘플 코드를 사용하여 `TransactionRecorder`API가 있는 서블릿을 호출할 수 있습니다.

```javascript
$.ajax({
   type: 'POST',
   url: url, //servlet url
   contentType: 'application/json; UTF-8',
   data: JSON.stringify({transactionCount : 1,
                        transactionType: "SUBMIT",
                        resourceType: "FORM",
                        resourceSubType: "ADAPTIVE-FORM"}),
   success: successHandler,
   error: faultHandler
})
```

## 관련 문서 {#related-articles}

* [거래 보고서 개요](/help/forms/using/transaction-reports-overview.md)
* [거래 보고서 보기 및 이해](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [거래 보고서 청구 가능한 API](/help/forms/using/transaction-reports-billable-apis.md)

