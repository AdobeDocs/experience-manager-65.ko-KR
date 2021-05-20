---
title: 편지 인스턴스에 액세스할 수 있는 API
seo-title: 편지 인스턴스에 액세스할 수 있는 API
description: API를 사용하여 편지 인스턴스에 액세스하는 방법을 배웁니다.
seo-description: API를 사용하여 편지 인스턴스에 액세스하는 방법을 배웁니다.
uuid: e7fb7798-f49d-458f-87f5-22df5f3e7d10
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9c27f976-972a-4250-b56d-b84a7d72f8c8
feature: 서신 관리
exl-id: 9d43d9d4-5487-416c-b641-e807227ac056
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 1%

---

# 문자 인스턴스 {#apis-to-access-letter-instances}에 액세스하기 위한 API

## 개요 {#overview}

서신 관리의 서신 UI 만들기를 사용하여 진행 중인 서신 인스턴스의 초안을 저장할 수 있으며 제출된 편지 인스턴스가 있습니다.

Correspondence Management는 제출된 편지 인스턴스 또는 초안에서 작업할 수 있도록 목록 인터페이스를 구축할 수 있는 를 사용하는 API를 제공합니다. API 목록 및 열린 에이전트의 제출 및 초안 편지 인스턴스로 인해 에이전트가 초안 또는 제출된 편지 인스턴스에서 계속 작업할 수 있습니다.

## 문자 인스턴스 {#fetching-letter-instances} 가져오기

서신 관리는 LetterInstanceService 서비스를 통해 편지 인스턴스를 가져오도록 API를 표시합니다.

| 메서드 | 설명 |
|--- |--- |
| getAllLetterInstances | 입력 쿼리 매개 변수를 기반으로 문자 인스턴스를 가져옵니다. 모든 편지 인스턴스를 가져오려면 쿼리 매개 변수를 null로 전달합니다. |
| getLetterInstance | 편지 인스턴스 ID를 기반으로 지정된 편지 인스턴스를 가져옵니다. |
| letterInstanceExists | LetterInstance가 지정된 이름으로 존재하는지 확인합니다. |

>[!NOTE]
>
>LetterInstanceService는 OSGI 서비스이며 Java@Reference 사용하여 인스턴스를 검색할 수 있습니다
>클래스 또는 sling.getService(LetterInstanceService)입니다. Class )를 JSP에 있는 Windows Media Optimizer에서 참조할 수 있습니다.

### getAllLetterInstances {#using-nbsp-getallletterinstances} 사용

다음 API는 쿼리 개체(제출됨 및 초안 모두)를 기반으로 편지 인스턴스를 찾습니다. 쿼리 개체가 null이면 모든 편지 인스턴스를 반환합니다. 이 API는 문자 인스턴스의 추가 정보를 추출하는 데 사용할 수 있는 [LetterInstanceVO](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html) 개체 목록을 반환합니다

**구문**:  `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>매개 변수</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>쿼리</td>
   <td>쿼리 매개 변수는 편지 인스턴스를 찾거나 필터링하는 데 사용됩니다. 이 쿼리는 객체의 최상위 속성/속성만 지원합니다. Query는 문으로 구성되며 Statement 개체에 사용되는 "attributeName"은 Letter 인스턴스 개체에 있는 속성의 이름이어야 합니다.<br /> </td>
  </tr>
 </tbody>
</table>

#### 예제 1:SUBMITTED {#example-fetch-all-the-letter-instances-of-type-submitted} 유형의 모든 편지 인스턴스 가져오기

다음 코드는 제출된 편지 인스턴스 목록을 반환합니다. 초안만 가져오려면 `LetterInstanceType.COMPLETE.name()`을 `LetterInstanceType.DRAFT.name().`(으)로 변경하십시오

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

#### 예제 2: 사용자가 제출한 모든 편지 인스턴스를 가져오며 편지 인스턴스 유형은 DRAFT {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}입니다.

다음 코드에는 사용자가 제출한 편지 인스턴스(Attribute submittedby)와 같은 다른 기준에 따라 필터링된 결과를 얻기 위해 동일한 쿼리에 여러 개의 문이 있으며 letterInstanceType의 형식은 DRAFT입니다.

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

지정된 편지 인스턴스 ID로 식별된 편지 인스턴스를 가져옵니다. 인스턴스 ID가 일치하지 않으면 &quot;null&quot;을 반환합니다.

**구문:** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### LetterInstance가 {#verifying-if-letterinstance-exist} 있는지 확인

Letter 인스턴스가 지정된 이름으로 존재하는지 확인합니다.

**구문**:  `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

| **매개 변수** | **설명** |
|---|---|
| letterInstanceName | 편지 인스턴스가 있는지 확인할 편지 인스턴스의 이름입니다. |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## 편지 인스턴스 열기 {#opening-letter-instances}

편지 인스턴스는 제출됨 또는 초안 유형일 수 있습니다. 두 문자 인스턴스 유형을 모두 열면 다른 동작이 표시됩니다.

* 제출된 편지 인스턴스의 경우 편지 인스턴스를 나타내는 PDF가 열립니다. 서버에 지속된 Submitted Letter 인스턴스에는 PDF/A 만들기와 같은 사례를 완수하고 추가로 사용자 지정하는 데 사용할 수 있는 dataXML 및 처리된 XDP도 포함되어 있습니다.
* 초안 편지 인스턴스의 경우, 작성 서신 UI는 초안이 작성된 시간 동안의 정확한 이전 상태로 다시 로드됩니다

### 초안 편지 인스턴스 열기  {#opening-draft-letter-instance-nbsp}

CCR UI는 문자를 다시 로드하는 데 사용할 수 있는 cmLetterInstanceId 매개 변수를 지원합니다.

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>제출된 데이터에 이미 다시 로드되는 서신에 대한 모든 세부 사항이 포함되므로, 서신 다시 로드할 때 cmLetterId 또는 cmLetterName/State/Version을 지정할 필요가 없습니다. RandomNo는 브라우저 캐시 문제를 방지하기 위해 사용됩니다. 타임스탬프를 임의의 숫자로 사용할 수 있습니다.

### 제출된 편지 인스턴스 {#opening-submitted-letter-instance} 열기

제출된 PDF를 편지 인스턴스 ID를 사용하여 직접 열 수 있습니다.

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
