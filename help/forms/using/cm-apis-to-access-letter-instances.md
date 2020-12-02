---
title: API를 사용하여 문자 인스턴스 액세스
seo-title: API를 사용하여 문자 인스턴스 액세스
description: API를 사용하여 문자 인스턴스에 액세스하는 방법을 알아봅니다.
seo-description: API를 사용하여 문자 인스턴스에 액세스하는 방법을 알아봅니다.
uuid: e7fb7798-f49d-458f-87f5-22df5f3e7d10
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9c27f976-972a-4250-b56d-b84a7d72f8c8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---


# 문자 인스턴스 {#apis-to-access-letter-instances}에 액세스하기 위한 API

## 개요 {#overview}

서신 관리의 서신 UI를 사용하여 진행 중인 서신 인스턴스 초안을 저장할 수 있으며 제출된 서신 인스턴스가 있습니다.

Correspondence Management는 제출된 서신 인스턴스 또는 초안과 함께 작동하는 목록 인터페이스를 작성할 수 있는 API를 제공합니다. 에이전트가 초안 또는 제출된 서신 인스턴스 작업을 계속 수행할 수 있도록 API 목록 및 열린 제출자 및 초안 편지 인스턴스.

## 문자 인스턴스 {#fetching-letter-instances}을(를) 가져오는 중

통신 관리에서는 LetterInstanceService 서비스를 통해 문자 인스턴스를 가져오기 위해 API를 표시합니다.

| 메서드 | 설명 |
|--- |--- |
| getAllLetterInstances | 입력 쿼리 매개 변수를 기반으로 문자 인스턴스를 가져옵니다. 모든 문자 인스턴스를 가져오려면 쿼리 매개 변수를 null로 전달합니다. |
| getLetterInstance | 문자 인스턴스 ID를 기반으로 지정된 문자 인스턴스를 가져옵니다. |
| letterInstanceExists | LetterInstance가 지정된 이름으로 존재하는지 확인합니다. |

>[!NOTE]
>
>LetterInstanceService는 OSGI 서비스이며 Java에서 @Reference를 사용하여 해당 인스턴스를 검색할 수 있습니다
>클래스 또는 sling.getService(LetterInstanceService)입니다. 클래스 )를 JSP에 추가했습니다.

### getAllLetterInstances {#using-nbsp-getallletterinstances} 사용

다음 API는 쿼리 개체(제출됨 및 초안 모두)를 기반으로 문자 인스턴스를 찾습니다. 쿼리 개체가 null이면 모든 문자 인스턴스를 반환합니다. 이 API는 문자 인스턴스의 추가 정보를 추출하는 데 사용할 수 있는 [LetterInstanceVO](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html) 개체의 목록을 반환합니다

**구문**:  `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>매개 변수</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>쿼리</td>
   <td>쿼리 매개 변수는 문자 인스턴스를 찾거나 필터링하는 데 사용됩니다. 이 쿼리는 객체의 최상위 속성/속성만 지원합니다. 쿼리는 문으로 구성되며 문 개체에 사용되는 "attributeName"은 Letter 인스턴스 개체의 속성 이름이어야 합니다.<br /> </td>
  </tr>
 </tbody>
</table>

#### 예 1:SUBMITTED {#example-fetch-all-the-letter-instances-of-type-submitted} 유형의 모든 문자 인스턴스 가져오기

다음 코드는 제출된 문자 인스턴스 목록을 반환합니다. 초안만 가져오려면 `LetterInstanceType.COMPLETE.name()`을 `LetterInstanceType.DRAFT.name().`(으)로 변경하십시오.

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

#### 예 2: 사용자가 제출한 모든 문자 인스턴스 가져오기 및 문자 인스턴스 유형은 DRAFT {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}입니다.

다음 코드에는 같은 쿼리에 여러 개의 문이 있으므로 사용자가 제출한 문자 인스턴스(전송된 특성) 등의 다른 기준을 기반으로 필터링된 결과를 가져올 수 있고 letterInstanceType의 유형은 DRAFT입니다.

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

### getLetterInstance {#using-nbsp-getletterinstance} 사용

지정된 문자 인스턴스 ID로 식별된 문자 인스턴스를 가져옵니다. 인스턴스 ID가 일치하지 않으면 &quot;null을 반환합니다.

**구문:** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### LetterInstance가 {#verifying-if-letterinstance-exist}인지 확인

문자 인스턴스가 주어진 이름으로 존재하는지 확인

**구문**:  `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

| **매개 변수** | **설명** |
|---|---|
| letterInstanceName | 확인하려는 문자 인스턴스의 이름입니다. |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## 문자 인스턴스 {#opening-letter-instances} 열기

편지 인스턴스는 제출됨 또는 초안 유형일 수 있습니다. 두 문자 인스턴스 유형을 모두 열면 서로 다른 동작이 표시됩니다.

* 전송 문자 인스턴스의 경우 문자 인스턴스를 나타내는 PDF가 열립니다. 서버에 지속되는 제출된 서신 인스턴스에는 PDF/A 만들기와 같은 사용자 정의 사용 사례를 수행하고 수행하는 데 사용할 수 있는 dataXML 및 처리된 XDP도 포함되어 있습니다.
* 초안 문자 인스턴스의 경우 작성 통신 UI가 초안 작성 시의 정확한 이전 상태로 다시 로드됩니다

### 초안 문자 인스턴스 열기  {#opening-draft-letter-instance-nbsp}

CCR UI는 문자를 다시 로드하는 데 사용할 수 있는 cmLetterInstanceId 매개 변수를 지원합니다.

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>메시지를 다시 로드할 때 cmLetterId 또는 cmLetterName/State/Version을 지정할 필요가 없습니다. 전송된 데이터에는 이미 다시 로드되는 통신에 대한 모든 세부 사항이 포함되어 있습니다. RandomNo는 브라우저 캐시 문제를 방지하는 데 사용됩니다. 타임스탬프를 임의의 숫자로 사용할 수 있습니다.

### 제출된 문자 인스턴스 {#opening-submitted-letter-instance}을(를) 여는 중

제출된 PDF는 문자 인스턴스 ID를 사용하여 직접 열 수 있습니다.

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
