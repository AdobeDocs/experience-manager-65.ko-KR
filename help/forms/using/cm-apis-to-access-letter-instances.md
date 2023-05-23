---
title: 편지 인스턴스에 액세스하기 위한 API
seo-title: APIs to access letter instances
description: API를 사용하여 편지 인스턴스에 액세스하는 방법을 알아봅니다.
seo-description: Learn how to use APIs to access letter instances.
uuid: e7fb7798-f49d-458f-87f5-22df5f3e7d10
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9c27f976-972a-4250-b56d-b84a7d72f8c8
feature: Correspondence Management
exl-id: 9d43d9d4-5487-416c-b641-e807227ac056
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 1%

---

# 편지 인스턴스에 액세스하기 위한 API {#apis-to-access-letter-instances}

## 개요 {#overview}

서신 관리의 서신 작성 UI를 사용하여 진행 중인 편지 인스턴스의 초안을 저장할 수 있으며 제출된 편지 인스턴스가 있습니다.

서신 관리는 제출된 편지 인스턴스 또는 초안으로 작동하는 목록 인터페이스를 작성할 수 있는 API를 제공합니다. API는 에이전트의 제출 및 초안 편지 인스턴스를 나열하고 열어 에이전트가 초안 또는 제출된 편지 인스턴스에서 작업을 계속할 수 있도록 합니다.

## 편지 인스턴스를 가져오는 중 {#fetching-letter-instances}

서신 관리는 LetterInstanceService 서비스를 통해 편지 인스턴스를 가져오는 API를 표시합니다.

| 메서드 | 설명 |
|--- |--- |
| getAllLetterInstances | 입력 쿼리 매개 변수를 기반으로 문자 인스턴스를 가져옵니다. 모든 문자 인스턴스를 가져오려면 쿼리 매개 변수를 null로 전달합니다. |
| getLetterInstance | 편지 인스턴스 ID를 기반으로 지정된 편지 인스턴스를 가져옵니다. |
| letter인스턴스 있음 | 지정된 이름으로 LetterInstance가 있는지 확인합니다. |

>[!NOTE]
>
>LetterInstanceService는 OSGI 서비스이며 Java로 Java를 사용하여 인스턴스를 @Reference 수 있습니다
>클래스 또는 sling.getService(LetterInstanceService) JSP의 클래스 )

### getAllLetterInstances 사용 {#using-nbsp-getallletterinstances}

다음 API는 쿼리 개체(제출됨 및 초안 모두)를 기반으로 편지 인스턴스를 검색합니다. 쿼리 개체가 null이면 모든 문자 인스턴스를 반환합니다. 이 API는 다음 목록을 반환합니다. [편지 인스턴스 VO](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html) 객체 : 편지 인스턴스의 추가 정보를 추출하는 데 사용할 수 있습니다.

**구문**: `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>매개변수</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>쿼리</td>
   <td>쿼리 매개 변수는 Letter 인스턴스를 찾거나 필터링하는 데 사용됩니다. 여기서 쿼리는 객체의 최상위 속성/속성만 지원합니다. 쿼리는 문으로 구성되며 Statement 개체에 사용된 "attributeName"은 Letter 인스턴스 개체에 있는 속성의 이름이어야 합니다.<br /> </td>
  </tr>
 </tbody>
</table>

#### 예제 1: SUBMITTED 유형의 모든 편지 인스턴스 가져오기 {#example-fetch-all-the-letter-instances-of-type-submitted}

다음 코드는 제출된 편지 인스턴스 목록을 반환합니다. 초안만 가져오려면 `LetterInstanceType.COMPLETE.name()` 끝 `LetterInstanceType.DRAFT.name().`

```java
@Reference
LetterInstanceService letterInstanceService;
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

#### 예제 2: 사용자가 제출한 모든 편지 인스턴스 가져오기 및 편지 인스턴스 유형은 DRAFT입니다. {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

다음 코드에는 사용자가 제출한 문자 인스턴스(특성 제출자)와 같은 다른 기준을 기반으로 필터링된 결과를 얻기 위한 동일한 쿼리에 여러 개의 문이 있으며, letterInstanceType의 형식은 DRAFT입니다.

```java
@Reference
LetterInstanceService letterInstanceService;

String submittedBy = "tglodman";
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);

Statement statementForSubmittedBy = new Statement();
statementForSubmittedBy .setAttributeName("submittedby");
statementForSubmittedBy .setOperator(Operator.EQUALS);
statementForSubmittedBy .setAttributeValue(submittedBy);
query.addStatement(statementForSubmittedBy );
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

### getLetterInstance 사용 {#using-nbsp-getletterinstance}

특정 편지 인스턴스 ID로 식별되는 편지 인스턴스를 가져옵니다. 인스턴스 ID가 일치하지 않으면 &quot;null&quot;을 반환합니다.

**구문:** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### LetterInstance가 있는지 확인하는 중 {#verifying-if-letterinstance-exist}

지정된 이름으로 편지 인스턴스가 있는지 확인

**구문**: `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

| **매개변수** | **설명** |
|---|---|
| 편지 인스턴스 이름 | 존재하는지 확인할 편지 인스턴스의 이름입니다. |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## 편지 인스턴스 열기 {#opening-letter-instances}

편지 인스턴스는 제출됨 또는 초안 유형일 수 있습니다. 두 문자 인스턴스 유형을 모두 열면 서로 다른 동작이 표시됩니다.

* 제출된 편지 인스턴스의 경우 편지 인스턴스를 나타내는 PDF이 열립니다. 서버에서 지속되는 제출된 편지 인스턴스에는 dataXML 및 처리된 XDP도 포함되어 있습니다. 이 인스턴스는 PDF/A 작성과 같은 맞춤형 사용 사례를 완수하고 추가로 사용하는 데 사용할 수 있습니다.
* 초안 편지 인스턴스의 경우, 서신 만들기 UI가 초안을 만든 시간의 정확한 이전 상태로 다시 로드됩니다

### 초안 편지 인스턴스 열기  {#opening-draft-letter-instance-nbsp}

CCR UI는 문자를 다시 로드하는 데 사용할 수 있는 cmLetterInstanceId 매개 변수를 지원합니다.

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>제출된 데이터에는 다시 로드되는 서신에 대한 모든 세부 사항이 이미 포함되어 있으므로 서신을 다시 로드할 때 cmLetterId 또는 cmLetterName/State/Version을 지정하지 않아도 됩니다. RandomNo는 브라우저 캐시 문제를 방지하기 위해 사용되며 타임스탬프를 임의의 숫자로 사용할 수 있습니다.

### 제출된 편지 인스턴스 열기 {#opening-submitted-letter-instance}

제출된 PDF은 편지 인스턴스 ID를 사용하여 직접 열 수 있습니다.

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
