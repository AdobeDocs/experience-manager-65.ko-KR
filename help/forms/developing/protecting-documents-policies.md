---
title: 정책으로 문서 보호
seo-title: Protecting Documents with Policies
description: Document Security 서비스를 사용하여 Adobe PDF 문서에 기밀 설정을 동적으로 적용하고 문서에 대한 제어를 유지 관리합니다. 또한 Document Security 서비스를 통해 사용자는 수신자가 정책으로 보호된 PDF 문서를 사용하는 방법을 제어할 수 있습니다.
seo-description: Use the Document Security service to dynamically apply confidentiality settings to Adobe PDF documents and to maintain control over the documents. The Document Security service also enables the users to maintain control over how recipients use the policy-protected PDF document.
uuid: 6feb69ef-7b61-4d0b-8c87-d65d98bae9b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9b1d2bf3-f28c-41b2-9026-1f3311556422
role: Developer
exl-id: ff42579e-6aaf-433d-8b5d-9e9dd0957250
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '15514'
ht-degree: 0%

---

# 정책으로 문서 보호 {#protecting-documents-with-policies}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms용입니다.**

**문서 보안 서비스 정보**

Document Security 서비스를 사용하면 사용자가 Adobe PDF 문서에 기밀성 설정을 동적으로 적용하고 문서의 배포 범위에 관계없이 해당 문서를 제어할 수 있습니다.

문서 보안 서비스는 사용자가 정책에 따라 보호된 PDF 문서를 받는 사람이 사용하는 방법을 제어할 수 있도록 하여 사용자의 범위를 넘어 정보가 퍼지지 않도록 합니다. 사용자는 문서를 열 수 있는 사용자를 지정하고, 문서를 사용할 수 있는 방법을 제한하며, 문서가 배포되면 문서를 모니터링할 수 있습니다. 또한 사용자가 정책에 따라 보호된 문서에 대한 액세스를 동적으로 제어할 수 있으며 문서에 대한 액세스를 동적으로 취소할 수도 있습니다.

Document Security 서비스는 Microsoft Word 파일(DOC 파일)과 같은 다른 파일 유형도 보호합니다. Document Security Client API를 사용하여 이러한 파일 유형을 사용할 수 있습니다. 지원되는 버전은 다음과 같습니다.

* Microsoft Office 2003 파일(DOC, XLS, PPT 파일)
* Microsoft Office 2007 파일(DOCX, XLSX, PPTX 파일)
* PTC Pro/E 파일

명확하게 설명하려면 다음 두 섹션에서 Word 문서를 사용하는 방법을 설명합니다.

* [Word 문서에 정책 적용](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Word 문서에서 정책 제거](protecting-documents-policies.md#removing-policies-from-word-documents)

문서 보안 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* 정책을 만듭니다. 자세한 내용은 [정책 만들기](protecting-documents-policies.md#creating-policies).
* 정책을 수정합니다. 자세한 내용은 [정책 수정](protecting-documents-policies.md#modifying-policies).
* 정책을 삭제합니다. 자세한 내용은 [정책 삭제](protecting-documents-policies.md#deleting-policies).
* PDF 문서에 정책을 적용합니다. 자세한 내용은 [PDF 문서에 정책 적용](protecting-documents-policies.md#applying-policies-to-pdf-documents).
* PDF 문서에서 정책을 제거합니다. 자세한 내용은 [PDF 문서에서 정책 제거](protecting-documents-policies.md#removing-policies-from-pdf-documents).
* Inspect 정책으로 보호된 문서 자세한 내용은 [정책 보호 PDF 문서 검사](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents).
* PDF 문서에 대한 액세스를 취소합니다. 자세한 내용은 [문서에 대한 액세스 취소](protecting-documents-policies.md#revoking-access-to-documents).
* 해지된 문서에 대한 액세스를 복원합니다. 자세한 내용은 [해지된 문서에 대한 액세스 복원](protecting-documents-policies.md#reinstating-access-to-revoked-documents).
* 워터마크를 만듭니다. 자세한 내용은 [워터마크 만들기](protecting-documents-policies.md#creating-watermarks).
* 이벤트를 검색합니다. 자세한 내용은 [이벤트 검색](protecting-documents-policies.md#searching-for-events).

>[!NOTE]
>
>문서 보안 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

## 정책 만들기 {#creating-policies}

Document Security Java API 또는 웹 서비스 API를 사용하여 프로그래밍 방식으로 정책을 만들 수 있습니다. A *정책* 는 문서 보안 설정, 인증된 사용자 및 사용 권한을 포함하는 정보 모음입니다. 상황에 맞는 보안 설정을 사용하여 원하는 수만큼 정책을 만들고 저장할 수 있습니다.

정책을 사용하면 다음 작업을 수행할 수 있습니다.

* 문서를 열 수 있는 개인을 지정합니다. 수신자는 조직에 속하거나 조직에 외부에 있을 수 있습니다.
* 수신자가 문서를 사용할 수 있는 방법을 지정합니다. 다양한 Acrobat 및 Adobe Reader 기능에 대한 액세스를 제한할 수 있습니다. 이러한 기능에는 텍스트를 인쇄 및 복사하고 서명을 추가하고 문서에 주석을 추가하는 기능이 포함됩니다.
* 정책으로 보호된 문서를 배포한 후에도 언제든지 액세스 및 보안 설정을 변경합니다.
* 문서를 배포한 후 문서 사용을 모니터링합니다. 문서의 사용 방법과 사용 중인 사용자를 확인할 수 있습니다. 예를 들어 사용자가 문서를 연 시점을 확인할 수 있습니다.

### 웹 서비스를 사용하여 정책 만들기 {#creating-a-policy-using-web-services}

웹 서비스 API를 사용하여 정책을 만들 때 정책을 설명하는 기존 PDRL(Portable Document Rights Language) XML 파일을 참조하십시오. 정책 권한 및 주도자는 PDRL 문서에 정의됩니다. 다음 XML 문서는 PDRL 문서의 예입니다.

```xml
 <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
 <Policy PolicyInstanceVersion="1" PolicyID="5DA3F847-DE76-F9CC-63EA-49A8D59154DE" PolicyCreationTime="2004-08-30T00:02:28.294+00:00" PolicyType="1" PolicySchemaVersion="1.0" PolicyName="SDK Test Policy -4344050357301573237" PolicyDescription="An SDK Test policy" xmlns="https://www.adobe.com/schema/1.0/pdrl">
       <PolicyEntry>
          <ns1:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns1="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns2:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns2="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns3:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns3="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns4:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns4="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>all_internal_users</PrincipalName>
          </Principal>
       </PolicyEntry>
       <PolicyEntry>
          <ns5:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns5="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns6:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns6="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns7:Permission PermissionName="com.adobe.aps.pdf.copy" Access="ALLOW" xmlns:ns7="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns8:Permission PermissionName="com.adobe.aps.pdf.printLow" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns8="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns9:Permission PermissionName="com.adobe.aps.policySwitch" Access="ALLOW" xmlns:ns9="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns10:Permission PermissionName="com.adobe.aps.revoke" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns10="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns11:Permission PermissionName="com.adobe.aps.pdf.edit" Access="ALLOW" xmlns:ns11="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns12:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns12="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns13:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns13="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns14:Permission PermissionName="com.adobe.aps.pdf.printHigh" Access="ALLOW" xmlns:ns14="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>publisher</PrincipalName>
          </Principal>
       </PolicyEntry>
 
       <OfflineLeasePeriod>
          <Duration>P31D</Duration>
       </OfflineLeasePeriod>
 
       <AuditSettings isTracked="true" />
 
       <PolicyValidityPeriod isAbsoluteTime="false">
          <ValidityPeriodRelative>
             <NotBeforeRelative>PT0S</NotBeforeRelative>
 
             <NotAfterRelative>P20D</NotAfterRelative>
          </ValidityPeriodRelative>
       </PolicyValidityPeriod>
 </Policy>
 
```

>[!NOTE]
>
>문서 보안 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary-of-steps}

정책을 만들려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Document Security Client API 개체를 만듭니다.
1. 정책의 속성을 설정합니다.
1. 정책 항목을 만듭니다.
1. 정책을 등록합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-rightsmanagement-client.jar
* namespace.jar(AEM Forms이 JBoss에 배포된 경우)
* jaxb-api.jar(AEM Forms이 JBoss에 배포된 경우)
* jaxb-impl.jar(AEM Forms이 JBoss에 배포된 경우)
* jaxb-libs.jar(AEM Forms이 JBoss에 배포된 경우)
* jaxb-xjc.jar(AEM Forms이 JBoss에 배포된 경우)
* rellaxingDatatype.jar(AEM Forms이 JBoss에 배포된 경우)
* xsdlib.jar(AEM Forms이 JBoss에 배포된 경우)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar(AEM Forms이 JBoss에 배포되지 않은 경우 다른 JAR 파일 사용)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Document Security Client API 개체 만들기**

문서 보안 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만듭니다.

**정책의 속성 설정**

정책을 만들려면 정책 속성을 설정합니다. 필수 속성은 정책 이름입니다. 정책 이름은 각 정책 세트에 대해 고유해야 합니다. 정책 집합은 단순히 정책의 집합입니다. 정책이 별도의 정책 세트에 속하는 경우 이름이 같은 두 개의 정책이 있을 수 있습니다. 그러나 단일 정책 집합 내의 두 정책은 동일한 정책 이름을 가질 수 없습니다.

설정할 다른 유용한 속성은 유효 기간입니다. 유효 기간은 인증된 수신자가 정책에 따라 보호된 문서에 액세스할 수 있는 기간입니다. 이 속성을 설정하지 않으면 정책이 항상 유효합니다.

유효 기간은 다음 옵션 중 하나로 설정할 수 있습니다.

* 문서를 게시한 시점부터 문서에 액세스할 수 있는 기간(일)입니다
* 문서에 액세스할 수 없는 종료 날짜입니다
* 문서에 액세스할 수 있는 특정 날짜 범위입니다
* 항상 유효

시작 날짜만 지정할 수 있으므로 시작 날짜 이후에 정책이 유효합니다. 종료 날짜만 지정하면 종료 날짜까지 정책이 유효합니다. 그러나 시작 날짜와 종료 날짜가 모두 정의되어 있지 않으면 예외가 발생합니다.

정책에 속하는 속성을 설정할 때 암호화 설정을 설정할 수도 있습니다. 이러한 암호화 설정은 정책이 문서에 적용될 때 영향을 받습니다. 다음 암호화 값을 지정할 수 있습니다.

* **AES256**: 256비트 키를 사용하여 AES 암호화 알고리즘을 나타냅니다.
* **AES128**: 128비트 키를 사용하여 AES 암호화 알고리즘을 나타냅니다.
* **암호화 없음:** 암호화가 없음을 나타냅니다.

을 지정할 때 `NoEncryption` 옵션을 설정할 수 없습니다 `PlaintextMetadata` 옵션 `false`. 그럴 경우 예외가 발생합니다.

>[!NOTE]
>
>설정할 수 있는 기타 속성에 대한 자세한 내용은 `Policy` 인터페이스 설명 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**정책 항목 만들기**

정책 항목에서는 그룹 및 사용자인 주도자와 권한을 정책에 첨부합니다. 정책에 하나 이상의 정책 항목이 있어야 합니다. 예를 들어 다음 작업을 수행한다고 가정합니다.

* 그룹이 온라인 상태에서만 문서를 볼 수 있고 수신자가 문서를 복사하지 못하도록 하는 정책 항목을 만들고 등록합니다.
* 정책에 정책 항목을 첨부합니다.
* Acrobat을 사용하여 정책을 사용하여 문서를 보호합니다.

이러한 작업을 수행하면 수신자가 문서를 온라인으로 볼 수만 있고 복사할 수 없습니다. 이 문서는 보안이 제거될 때까지 안전하게 유지됩니다.

**정책 등록**

새 정책을 사용하려면 먼저 등록해야 합니다. 정책을 등록한 후 이 정책을 사용하여 문서를 보호할 수 있습니다.

### Java API를 사용하여 정책 만들기 {#create-a-policy-using-the-java-api}

문서 보안 API(Java)를 사용하여 정책을 만듭니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security Client API 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `DocumentSecurityClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. 정책의 속성을 설정합니다.

   * 만들기 `Policy` 객체를 호출하여 `InfomodelObjectFactory` 개체의 정적 `createPolicy` 메서드를 사용합니다. 이 메서드는 `Policy` 개체.
   * 를 호출하여 정책의 이름 속성을 설정합니다 `Policy` 개체 `setName` 메서드와 정책 이름을 지정하는 문자열 값 전달
   * 를 호출하여 정책의 설명을 설정합니다 `Policy` 개체 `setDescription` 정책의 설명을 지정하는 문자열 값 전달 및 메서드입니다.
   * 새 정책이 속한 정책 집합을 `Policy` 개체 `setPolicySetName` 정책 세트 이름을 지정하는 문자열 값 전달 및 메서드. (다음을 지정할 수 있습니다 `null` 이 매개변수 값에 대해 정책이 *내 정책* 정책 집합입니다.)
   * 를 호출하여 정책의 유효 기간을 만듭니다 `InfomodelObjectFactory` 개체의 정적 `createValidityPeriod` 메서드를 사용합니다. 이 메서드는 `ValidityPeriod` 개체.
   * 를 호출하여 정책으로 보호된 문서에 액세스할 수 있는 일 수를 설정합니다 `ValidityPeriod` 개체 `setRelativeExpirationDays` 메서드 및 일 수를 지정하는 정수 값 전달
   * 를 호출하여 정책의 유효 기간을 설정합니다 `Policy` 개체 `setValidityPeriod` 메서드 및 전달 `ValidityPeriod` 개체.

1. 정책 항목을 만듭니다.

   * 를 호출하여 정책 항목을 만듭니다 `InfomodelObjectFactory` 개체의 정적 `createPolicyEntry` 메서드를 사용합니다. 이 메서드는 `PolicyEntry` 개체.
   * 를 호출하여 정책의 권한을 지정합니다 `InfomodelObjectFactory` 개체의 정적 `createPermission` 메서드를 사용합니다. 에 속하는 정적 데이터 멤버를 전달합니다. `Permission` 권한을 나타내는 인터페이스입니다. 이 메서드는 `Permission` 개체. 예를 들어, 사용자가 정책으로 보호된 PDF 문서에서 데이터를 복사할 수 있는 권한을 추가하려면 다음을 수행합니다 `Permission.COPY`. (추가할 각 권한에 대해 이 단계를 반복합니다.)
   * 를 호출하여 정책 항목에 권한을 추가합니다 `PolicyEntry` 개체 `addPermission` 메서드 및 전달 `Permission` 개체. (각각에 대해 이 단계를 반복합니다 `Permission` 만든 개체).
   * 를 호출하여 정책 주도자를 만듭니다 `InfomodelObjectFactory` 개체의 정적 `createSpecialPrincipal` 메서드를 사용합니다. 에 속하는 데이터 멤버를 전달합니다 `InfomodelObjectFactory` 주도자를 나타내는 개체입니다. 이 메서드는 `Principal` 개체. 예를 들어 문서의 게시자를 주체로 추가하려면 `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`.
   * 을 호출하여 정책 항목에 주도자를 추가합니다 `PolicyEntry` 개체 `setPrincipal`메서드 및 전달 `Principal` 개체.
   * 를 호출하여 정책에 정책 항목을 추가합니다 `Policy` 개체 `addPolicyEntry` 메서드 및 전달 `PolicyEntry` 개체.

1. 정책을 등록합니다.

   * 만들기 `PolicyManager` 객체를 호출하여 `DocumentSecurityClient` 개체 `getPolicyManager` 메서드를 사용합니다.
   * 를 호출하여 정책을 등록합니다 `PolicyManager` 개체 `registerPolicy` 메서드 및 다음 값 전달:

      * 다음 `Policy` 등록할 정책을 나타내는 개체입니다.
   * 정책이 속한 정책 집합을 나타내는 문자열 값입니다.

   연결 설정 내에서 AEM Forms 관리자 계정을 사용하여 `DocumentSecurityClient` 개체를 호출한 다음 `registerPolicy` 메서드를 사용합니다. 만약 `null` 정책 세트의 값이면 관리자가 정책을 만듭니다 *내 정책* 정책 집합입니다.

   연결 설정 내에서 문서 보안 사용자를 사용하는 경우 오버로드된 `registerPolicy` 정책만 허용하는 메서드입니다. 즉, 정책 세트 이름을 지정할 필요가 없습니다. 하지만 정책이 이름이 지정된 정책 세트에 추가됩니다 *내 정책*. 이 정책 세트에 새 정책을 추가하지 않으려면 `registerPolicy` 메서드를 사용합니다.

   >[!NOTE]
   >
   >정책을 만들 때 기존 정책 세트를 참조합니다. 존재하지 않는 정책 세트를 지정하면 예외가 발생합니다.

문서 보안 서비스를 사용하는 코드 예에 대해서는 다음을 참조하십시오.

* &quot;빠른 시작(SOAP 모드): Java API를 사용하여 정책 만들기&quot;

### 웹 서비스 API를 사용하여 정책 만들기 {#create-a-policy-using-the-web-service-api}

문서 보안 API(웹 서비스)를 사용하여 정책을 만듭니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. Document Security Client API 개체를 만듭니다.

   * 만들기 `DocumentSecurityServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `DocumentSecurityServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`) 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 생성할 때 사용됩니다.)
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `RightsManagementServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.


1. 정책의 속성을 설정합니다.

   * 만들기 `PolicySpec` 생성자를 사용하여 개체를 작성합니다.
   * 문자열 값을 `PolicySpec` 개체 `name` 데이터 멤버.
   * 문자열 값을 `PolicySpec` 개체 `description` 데이터 멤버.
   * 문자열 값을 `PolicySpec` 개체 `policySetName` 데이터 멤버. 기존 정책 세트 이름을 지정해야 합니다. (다음을 지정할 수 있습니다 `null` 이 매개 변수 값에 대해 정책이 *내 정책*)
   * 정수 값을 `PolicySpec` 개체 `offlineLeasePeriod` 데이터 멤버.
   * 설정 `PolicySpec` 개체 `policyXml` PDRL XML 데이터를 나타내는 문자열 값이 있는 데이터 멤버. 이 작업을 수행하려면 .NET을 만드십시오 `StreamReader` 생성자를 사용하여 개체를 작성합니다. 정책을 나타내는 PDRL XML 파일의 위치를 `StreamReader` 생성자입니다. 그런 다음 `StreamReader` 개체 `ReadLine` 메서드를 사용하여 반환 값을 문자열 변수에 지정합니다. 를 통해 반복 `StreamReader` 개체 `ReadLine` 메서드는 null을 반환합니다. 에 문자열 변수를 지정합니다. `PolicySpec` 개체 `policyXml` 데이터 멤버.

1. 정책 항목을 만듭니다.

   Document Security 웹 서비스 API를 사용하여 정책을 만들 때 정책 항목을 만들 필요가 없습니다. 정책 항목은 PDRL 문서에 정의되어 있습니다.

1. 정책을 등록합니다.

   를 호출하여 정책을 등록합니다 `DocumentSecurityServiceClient` 개체 `registerPolicy` 메서드 및 다음 값 전달:

   * 다음 `PolicySpec` 등록할 정책을 나타내는 개체입니다.
   * 정책이 속한 정책 집합을 나타내는 문자열 값입니다. 을(를) 지정할 수 있습니다 `null` 정책에 추가되는 값입니다. *내 정책* 정책 집합입니다.

   연결 설정 내에서 AEM Forms 관리자 계정을 사용하여 `DocumentSecurityClient` 개체를 호출하려면 `registerPolicy` 메서드를 사용합니다.

   연결 설정 내에서 Document SecurityDocument Security 사용자를 사용하는 경우 오버로드된 파일을 호출할 수 있습니다 `registerPolicy` 정책만 허용하는 메서드입니다. 즉, 정책 세트 이름을 지정할 필요가 없습니다. 하지만 정책이 이름이 지정된 정책 세트에 추가됩니다 *내 정책*. 이 정책 세트에 새 정책을 추가하지 않으려면 `registerPolicy` 메서드를 사용합니다.

   >[!NOTE]
   >
   >정책을 만들고 정책 세트를 지정할 때는 기존 정책 세트를 지정해야 합니다. 존재하지 않는 정책 세트를 지정하면 예외가 발생합니다.

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 정책 만들기&quot;
* &quot;빠른 시작(SwaRef): 웹 서비스 API를 사용하여 정책 만들기&quot;

## 정책 수정 {#modifying-policies}

Document Security Java API 또는 웹 서비스 API를 사용하여 기존 정책을 수정할 수 있습니다. 기존 정책을 변경하려면 정책을 검색하고 수정한 다음 서버에서 정책을 업데이트합니다. 예를 들어 기존 정책을 검색하고 유효 기간을 연장한다고 가정합니다. 변경 사항을 적용하려면 먼저 정책을 업데이트해야 합니다.

비즈니스 요구 사항이 변경되고 정책이 이러한 요구 사항을 더 이상 반영하지 않는 경우 정책을 수정할 수 있습니다. 새 정책을 만드는 대신 기존 정책을 업데이트할 수 있습니다.

웹 서비스를 사용하여 정책 속성을 수정하려면(예: JAX-WS로 작성된 Java 프록시 클래스 사용) 해당 정책이 문서 보안 서비스에 등록되어 있는지 확인해야 합니다. 그런 다음 `PolicySpec.getPolicyXml` 해당 메서드를 사용하여 정책 속성을 수정하고 방법을 사용합니다. 예를 들어 를 호출하여 오프라인 임대 기간을 수정할 수 있습니다 `PolicySpec.setOfflineLeasePeriod` 메서드를 사용합니다.

>[!NOTE]
>
>문서 보안 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-1}

기존 정책을 수정하려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. Document Security Client API 개체를 만듭니다.
1. 기존 정책을 검색합니다.
1. 정책 속성을 변경합니다.
1. 정책을 업데이트합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security Client API 개체 만들기**

문서 보안 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `RightsManagementClient` 개체. Document Security 웹 서비스 API를 사용하는 경우 `RightsManagementServiceService` 개체.

**기존 정책 검색**

기존 정책을 수정하려면 읽어들여야 합니다. 정책을 검색하려면 정책 이름과 정책이 속한 정책 집합을 지정합니다. 를 지정하는 경우 `null` 정책 집합 이름의 값에서 정책이 검색됩니다 *내 정책* 정책 집합입니다.

**정책의 속성 설정**

정책을 수정하려면 정책 속성의 값을 수정합니다. 변경할 수 없는 유일한 정책 속성은 이름 속성입니다. 예를 들어 정책의 오프라인 임대 기간을 변경하려면 정책의 오프라인 임대 기간 속성 값을 수정할 수 있습니다.

웹 서비스를 사용하여 정책의 오프라인 임대 기간을 수정할 때 `offlineLeasePeriod` 필드의 필드 `PolicySpec` 인터페이스가 무시됩니다. 오프라인 임대 기간을 갱신하려면 `OfflineLeasePeriod` PDRL XML 문서의 요소 그런 다음 `PolicySpec` 인터페이스 `policyXML` 데이터 멤버.

>[!NOTE]
>
>설정할 수 있는 기타 속성에 대한 자세한 내용은 `Policy` 인터페이스 설명 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**정책 업데이트**

정책에 대한 변경 내용이 적용되기 전에 Document Security 서비스로 정책을 업데이트해야 합니다. 문서를 보호하는 정책의 변경 사항은 다음에 Document Security 서비스와 정책에 보호된 문서를 동기화할 때 업데이트됩니다.

### Java API를 사용하여 기존 정책 수정 {#modify-existing-policies-using-the-java-api}

문서 보안 API(Java)를 사용하여 기존 정책을 수정합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security Client API 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `RightsManagementClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. 기존 정책을 검색합니다.

   * 만들기 `PolicyManager` 객체를 호출하여 `RightsManagementClient` 개체 `getPolicyManager` 메서드를 사용합니다.
   * 만들기 `Policy` 업데이트할 정책을 나타내는 개체입니다 `PolicyManager` 개체 `getPolicy` 메서드 및 다음 값 전달

      * 정책이 속한 정책 집합 이름을 나타내는 문자열 값입니다. 다음을 지정할 수 있습니다 `null` 결과 `MyPolicies` 사용 중인 정책 집합입니다.
      * 정책 이름을 나타내는 문자열 값입니다.

1. 정책의 속성을 설정합니다.

   비즈니스 요구 사항을 충족하도록 정책의 속성을 변경합니다. 예를 들어 정책의 오프라인 임대 기간을 변경하려면 `Policy` 개체 `setOfflineLeasePeriod` 메서드를 사용합니다.

1. 정책을 업데이트합니다.

   를 호출하여 정책 업데이트 `PolicyManager` 개체 `updatePolicy` 메서드를 사용합니다. 전달 `Policy` 업데이트할 정책을 나타내는 개체입니다.

**코드 예**

문서 보안 서비스를 사용하는 코드 예에 대해서는 빠른 시작(SOAP 모드)을 참조하십시오. Java API 섹션을 사용하여 정책 수정.

### 웹 서비스 API를 사용하여 기존 정책 수정 {#modify-existing-policies-using-the-web-service-api}

문서 보안 API(웹 서비스)를 사용하여 기존 정책을 수정합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. Document Security Client API 개체를 만듭니다.

   * 만들기 `RightsManagementServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `RightsManagementServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`) 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 생성할 때 사용됩니다.)
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `RightsManagementServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.


1. 기존 정책을 검색합니다.

   만들기 `PolicySpec` 수정할 정책을 나타내는 객체입니다. `RightsManagementServiceClient` 개체 `getPolicy` 메서드 및 다음 값 전달:

   * 정책이 속한 정책 집합 이름을 지정하는 문자열 값입니다. 다음을 지정할 수 있습니다 `null` 결과 `MyPolicies` 사용 중인 정책 집합입니다.
   * 정책의 이름을 지정하는 문자열 값입니다.

1. 정책의 속성을 설정합니다.

   비즈니스 요구 사항을 충족하도록 정책의 속성을 변경합니다.

1. 정책을 업데이트합니다.

   를 호출하여 정책을 업데이트합니다 `RightsManagementServiceClient` 개체 `updatePolicyFromSDK` 메서드 및 전달 `PolicySpec` 업데이트할 정책을 나타내는 개체입니다.

**코드 예**

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 정책 수정&quot;
* &quot;빠른 시작(SwaRef): 웹 서비스 API를 사용하여 정책 수정&quot;

## 정책 삭제 {#deleting-policies}

Document Security Java API 또는 웹 서비스 API를 사용하여 기존 정책을 삭제할 수 있습니다. 정책을 삭제한 후에는 더 이상 문서를 보호하는 데 사용할 수 없습니다. 그러나 정책을 사용하는 기존 정책 보호 문서는 계속 보호됩니다. 새 정책을 사용할 수 있게 되면 정책을 삭제할 수 있습니다.

>[!NOTE]
>
>문서 보안 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-2}

기존 정책을 삭제하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. Document Security Client API 개체를 만듭니다.
1. 정책을 삭제합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security Client API 개체 만들기**

문서 보안 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `RightsManagementClient` 개체. Document Security 웹 서비스 API를 사용하는 경우 `RightsManagementServiceService` 개체.

**정책 삭제**

정책을 삭제하려면 삭제할 정책과 정책이 속한 정책 세트를 지정합니다. AEM Forms을 호출하는 데 설정을 사용하는 사용자에게는 정책을 삭제할 수 있는 권한이 있어야 합니다. 그렇지 않으면 예외가 발생합니다. 마찬가지로 존재하지 않는 정책을 삭제하려고 하면 예외가 발생합니다.

### Java API를 사용하여 정책 삭제 {#delete-policies-using-the-java-api}

문서 보안 API(Java)를 사용하여 정책을 삭제합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security Client API 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `RightsManagementClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. 정책을 삭제합니다.

   * 만들기 `PolicyManager` 객체를 호출하여 `RightsManagementClient` 개체 `getPolicyManager` 메서드를 사용합니다.
   * 를 호출하여 정책을 삭제합니다. `PolicyManager` 개체 `deletePolicy` 메서드 및 다음 값 전달:

      * 정책이 속한 정책 집합 이름을 지정하는 문자열 값입니다. 다음을 지정할 수 있습니다 `null` 결과 `MyPolicies` 사용 중인 정책 집합입니다.
      * 삭제할 정책의 이름을 지정하는 문자열 값입니다.

**코드 예**

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(SOAP 모드): Java API를 사용하여 정책 삭제&quot;

### 웹 서비스 API를 사용하여 정책 삭제 {#delete-policies-using-the-web-service-api}

문서 보안 API(웹 서비스)를 사용하여 정책을 삭제합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. Document Security Client API 개체를 만듭니다.

   * 만들기 `RightsManagementServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `RightsManagementServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`) 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 생성할 때 사용됩니다.)
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `RightsManagementServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.


1. 정책을 삭제합니다.

   를 호출하여 정책을 삭제합니다. `RightsManagementServiceClient` 개체 `deletePolicy` 메서드 및 다음 값 전달:

   * 정책이 속한 정책 집합 이름을 지정하는 문자열 값입니다. 다음을 지정할 수 있습니다 `null` 결과 `MyPolicies` 사용 중인 정책 집합입니다.
   * 삭제할 정책의 이름을 지정하는 문자열 값입니다.

**코드 예**

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 정책 삭제&quot;
* &quot;빠른 시작(SwaRef): 웹 서비스 API를 사용하여 정책 삭제&quot;

## PDF 문서에 정책 적용 {#applying-policies-to-pdf-documents}

문서를 보호하기 위해 PDF 문서에 정책을 적용할 수 있습니다. PDF 문서에 정책을 적용하면 문서에 대한 액세스를 제한합니다. 문서에 정책이 이미 설정되어 있으면 문서에 정책을 적용할 수 없습니다.

문서가 열려 있는 동안 텍스트 인쇄 및 복사, 변경, 문서에 서명 및 주석 추가 등 Acrobat 및 Adobe Reader 기능에 대한 액세스를 제한할 수도 있습니다. 또한 사용자가 문서에 더 이상 액세스하지 못하게 할 때 정책에 따라 보호된 PDF 문서를 취소할 수 있습니다.

정책을 지정한 문서를 배포한 후 해당 문서의 사용을 모니터링할 수 있습니다. 즉, 문서의 사용 방법과 사용 중인 사용자를 확인할 수 있습니다. 예를 들어, 사용자가 문서를 연 시점을 확인할 수 있습니다.

>[!NOTE]
>
>문서 보안 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-3}

PDF 문서에 정책을 적용하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Document Security Client API 개체를 만듭니다.
1. 정책이 적용되는 PDF 문서를 검색합니다.
1. PDF 문서에 기존 정책을 적용합니다.
1. 정책으로 보호된 PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security Client API 개체 만들기**

문서 보안 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만듭니다. Java API를 사용하는 경우 `DocumentSecurityClient` 개체. Document Security 웹 서비스 API를 사용하는 경우 `DocumentSecurityServiceService` 개체.

**PDF 문서 검색**

정책을 적용하려면 PDF 문서를 검색할 수 있습니다. PDF 문서에 정책을 적용하면 문서를 사용할 때 사용자가 제한됩니다. 예를 들어 정책을 통해 오프라인 상태에서 문서를 열 수 없는 경우, 사용자는 온라인 상태여야 문서를 열 수 있습니다.

**PDF 문서에 기존 정책 적용**

PDF 문서에 정책을 적용하려면 기존 정책을 참조하고 정책이 속한 정책을 지정합니다. 연결 속성을 설정하는 사용자는 지정된 정책에 액세스할 수 있어야 합니다. 그렇지 않으면 예외가 발생합니다.

**PDF 문서를 저장합니다**

Document Security 서비스가 PDF 문서에 정책을 적용한 후 정책으로 보호된 PDF 문서를 PDF 파일로 저장할 수 있습니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[문서에 대한 액세스 취소](protecting-documents-policies.md#revoking-access-to-documents)

### Java API를 사용하여 PDF 문서에 정책 적용 {#apply-a-policy-to-a-pdf-document-using-the-java-api}

문서 보안 API(Java)를 사용하여 PDF 문서에 정책을 적용합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security Client API 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `RightsManagementClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. PDF 문서를 검색합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하여 PDF 문서를 나타내는 객체입니다. PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * 만들기 `com.adobe.idp.Document` 생성자를 사용하여 객체를 전달하고 `java.io.FileInputStream` 개체.

1. PDF 문서에 기존 정책을 적용합니다.

   * 만들기 `DocumentManager` 객체를 호출하여 `RightsManagementClient` 개체 `getDocumentManager` 메서드를 사용합니다.
   * 를 호출하여 PDF 문서에 정책을 적용합니다 `DocumentManager` 개체 `protectDocument` 메서드 및 다음 값 전달:

      * 다음 `com.adobe.idp.Document` 정책이 적용되는 PDF 문서를 포함하는 객체입니다.
      * 문서의 이름을 지정하는 문자열 값입니다.
      * 정책이 속한 정책 집합의 이름을 지정하는 문자열 값입니다. 을(를) 지정할 수 있습니다 `null` 결과를 가져오는 값 `MyPolicies` 사용 중인 정책 집합입니다.
      * 정책 이름을 지정하는 문자열 값입니다.
      * 문서 게시자인 사용자의 사용자 관리자 도메인의 이름을 나타내는 문자열 값입니다. 이 매개 변수 값은 선택 사항이며 null일 수 있습니다(이 매개 변수가 null이면 다음 매개 변수 값은 null이어야 함).
      * 문서 게시자인 사용자 관리자 사용자의 정식 이름을 나타내는 문자열 값입니다. 이 매개 변수 값은 선택 사항이며 다음 작업을 수행할 수 있습니다. `null` (이 매개 변수가 null이면 이전 매개 변수 값은 `null`).
      * A `com.adobe.livecycle.rightsmanagement.Locale` MS Office 템플릿을 선택하는 데 사용되는 로케일을 나타냅니다. 이 매개 변수 값은 선택 사항이며 PDF 문서에 사용되지 않습니다. PDF 문서를 보호하려면 `null`.

      다음 `protectDocument` 메서드 반환 `RMSecureDocumentResult` 정책으로 보호된 PDF 문서를 포함하는 객체입니다.


1. PDF 문서를 저장합니다.

   * 를 호출합니다 `RMSecureDocumentResult` 개체 `getProtectedDoc` 정책으로 보호된 PDF 문서를 가져오는 방법입니다. 이 메서드는 `com.adobe.idp.Document` 개체.
   * 만들기 `java.io.File` 개체 및 파일 확장자가 PDF인지 확인합니다.
   * 를 호출합니다 `com.adobe.idp.Document` 개체 `copyToFile` 컨텐츠의 내용 복사 방법 `Document` 개체를 파일에 추가합니다. `Document` 반환되는 개체 `getProtectedDoc` 메서드).

**코드 예**

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(EJB 모드): Java API를 사용하여 PDF 문서에 정책 적용&quot;
* &quot;빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서에 정책 적용&quot;

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 PDF 문서에 정책 적용 {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

문서 보안 API(웹 서비스)를 사용하여 PDF 문서에 정책을 적용합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. Document Security Client API 개체를 만듭니다.

   * 만들기 `RightsManagementServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `RightsManagementServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`) 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 생성할 때 사용됩니다.)
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `RightsManagementServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.


1. PDF 문서를 검색합니다.

   * 만들기 `BLOB` 생성자를 사용하여 개체를 작성합니다. 다음 `BLOB` 정책은 적용된 PDF 문서를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 객체를 사용하여 해당 생성자를 호출하고 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열 크기를 결정합니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 메서드를 사용합니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 필드입니다.

1. PDF 문서에 기존 정책을 적용합니다.

   를 호출하여 PDF 문서에 정책을 적용합니다 `RightsManagementServiceClient` 개체 `protectDocument` 메서드 및 다음 값 전달:

   * 다음 `BLOB` 정책이 적용되는 PDF 문서를 포함하는 객체입니다.
   * 문서의 이름을 지정하는 문자열 값입니다.
   * 정책이 속한 정책 집합의 이름을 지정하는 문자열 값입니다. 을(를) 지정할 수 있습니다 `null` 결과를 가져오는 값 `MyPolicies` 사용 중인 정책 집합입니다.
   * 정책 이름을 지정하는 문자열 값입니다.
   * 문서 게시자인 사용자의 사용자 관리자 도메인의 이름을 나타내는 문자열 값입니다. 이 매개 변수 값은 선택 사항이며 null일 수 있습니다(이 매개 변수가 null이면 다음 매개 변수 값이 되어야 함). `null`).
   * 문서 게시자인 사용자 관리자 사용자의 정식 이름을 나타내는 문자열 값입니다. 이 매개 변수 값은 선택 사항이며 null일 수 있습니다(이 매개 변수가 null이면 이전 매개 변수 값은 다음과 같아야 함) `null`).
   * A `RMLocale` 로케일 값을 지정하는 값(예: `RMLocale.en`).
   * 정책 식별자 값을 저장하는 데 사용되는 문자열 출력 매개 변수입니다.
   * 정책으로 보호된 식별자 값을 저장하는 데 사용되는 문자열 출력 매개 변수입니다.
   * MIME 유형을 저장하는 데 사용되는 문자열 출력 매개 변수입니다(예: `application/pdf`).

   다음 `protectDocument` 메서드 반환 `BLOB` 정책으로 보호된 PDF 문서를 포함하는 객체입니다.

1. PDF 문서를 저장합니다.

   * 만들기 `System.IO.FileStream` 객체를 생성자를 호출하고 정책 보호 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달하여 객체를 생성합니다.
   * 의 데이터 내용을 저장하는 바이트 배열을 만듭니다 `BLOB` 반환되는 개체 `protectDocument` 메서드를 사용합니다. 의 값을 가져와서 바이트 배열을 채웁니다 `BLOB` 개체 `MTOM` 데이터 멤버.
   * 만들기 `System.IO.BinaryWriter` 생성자를 호출하고 전달하여 개체를 `System.IO.FileStream` 개체.
   * 를 호출하여 PDF 파일에 바이트 배열의 내용을 씁니다. `System.IO.BinaryWriter` 개체 `Write` 메서드를 사용하여 바이트 배열을 전달합니다.

**코드 예**

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 PDF 문서에 정책 적용&quot;
* &quot;빠른 시작(SwaRef): 웹 서비스 API를 사용하여 PDF 문서에 정책 적용 &quot;

## PDF 문서에서 정책 제거 {#removing-policies-from-pdf-documents}

문서에서 보안을 제거하려면 정책으로 보호된 문서에서 정책을 제거할 수 있습니다. 즉, 더 이상 정책에 의해 문서를 보호하지 않으려는 경우 정책을 제거하고 업데이트된 정책을 추가하는 대신 정책으로 보호된 문서를 최신 정책으로 업데이트하려면 정책을 변경하는 것이 더 효율적입니다.

>[!NOTE]
>
>문서 보안 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-4}

정책으로 보호된 PDF 문서에서 정책을 제거하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. Document Security Client API 개체를 만듭니다.
1. 정책으로 보호된 PDF 문서를 검색합니다.
1. PDF 문서에서 정책을 제거합니다.
1. 비보안 PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security Client API 개체 만들기**

문서 보안 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만듭니다.

**정책으로 보호된 PDF 문서 검색**

정책을 제거하기 위해 정책으로 보호된 PDF 문서를 검색할 수 있습니다. 정책에 의해 보호되지 않는 PDF 문서에서 정책을 제거하려고 하면 예외가 발생합니다.

**PDF 문서에서 정책을 제거합니다**

관리자가 연결 설정에 지정된 경우 정책으로 보호된 PDF 문서에서 정책을 제거할 수 있습니다. 그렇지 않은 경우 문서 보안에 사용되는 정책에 `SWITCH_POLICY` PDF 문서에서 정책을 제거하려면 권한이 필요합니다. 또한 AEM Forms 연결 설정에 지정된 사용자에게도 해당 권한이 있어야 합니다. 그렇지 않으면 예외가 발생합니다.

**비보안 PDF 문서를 저장합니다**

문서 보안 서비스가 PDF 문서에서 정책을 제거한 후 비보안 PDF 문서를 PDF 파일로 저장할 수 있습니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 문서에 정책 적용](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Java API를 사용하여 PDF 문서에서 정책을 제거합니다 {#remove-a-policy-from-a-pdf-document-using-the-java-api}

Document Security API(Java)를 사용하여 정책으로 보호된 PDF 문서에서 정책을 제거합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security Client API 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `DocumentSecurityClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. 정책으로 보호된 PDF 문서를 검색합니다.

   * 만들기 `java.io.FileInputStream` 해당 생성자를 사용하고 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 정책으로 보호된 PDF 문서를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 생성자를 사용하여 객체를 전달하고 `java.io.FileInputStream` 개체.

1. PDF 문서에서 정책을 제거합니다.

   * 만들기 `DocumentManager` 객체를 호출하여 `DocumentSecurityClient` 개체 `getDocumentManager` 메서드를 사용합니다.
   * 를 호출하여 PDF 문서에서 정책을 제거합니다 `DocumentManager` 개체 `removeSecurity` 메서드 및 전달 `com.adobe.idp.Document` 정책으로 보호된 PDF 문서를 포함하는 객체입니다. 이 메서드는 `com.adobe.idp.Document` 비보안 PDF 문서를 포함하는 객체입니다.

1. 비보안 PDF 문서를 저장합니다.

   * 만들기 `java.io.File` 개체 및 파일 확장자가 PDF인지 확인합니다.
   * 를 호출합니다 `Document` 개체 `copyToFile` 컨텐츠의 내용 복사 방법 `Document` 개체를 파일에 추가합니다. `Document` 반환되는 개체 `removeSecurity` 메서드).

**코드 예**

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서에서 정책 제거&quot;

### 웹 서비스 API를 사용하여 정책 제거 {#remove-a-policy-using-the-web-service-api}

Document Security API(웹 서비스)를 사용하여 정책으로 보호된 PDF 문서에서 정책을 제거합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. Document Security Client API 개체를 만듭니다.

   * 만들기 `DocumentSecurityServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `DocumentSecurityServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`) 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 생성할 때 사용됩니다.)
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `DocumentSecurityServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.


1. 정책으로 보호된 PDF 문서를 검색합니다.

   * 만들기 `BLOB` 생성자를 사용하여 개체를 작성합니다. 다음 `BLOB` 정책은 제거된 정책으로 보호된 PDF 문서를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 객체를 사용하여 해당 생성자를 호출하고 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 메서드와 전달
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 필드입니다.

1. PDF 문서에서 정책을 제거합니다.

   를 호출하여 PDF 문서에서 정책을 제거합니다 `DocumentSecurityServiceClient` 개체 `removePolicySecurity` 메서드 및 전달 `BLOB` 정책으로 보호된 PDF 문서를 포함하는 객체입니다. 이 메서드는 `BLOB` 비보안 PDF 문서를 포함하는 객체입니다.

1. 비보안 PDF 문서를 저장합니다.

   * 만들기 `System.IO.FileStream` 객체를 사용하여 해당 생성자를 호출하고 비보안 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달합니다.
   * 의 데이터 내용을 저장하는 바이트 배열을 만듭니다 `BLOB` 반환되는 개체 `removePolicySecurity` 메서드를 사용합니다. 의 값을 가져와서 바이트 배열을 채웁니다 `BLOB` 개체 `MTOM` 필드.
   * 만들기 `System.IO.BinaryWriter` 생성자를 호출하고 전달하여 개체를 `System.IO.FileStream` 개체.

**코드 예**

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 PDF 문서에서 정책 제거 &quot;
* &quot;빠른 시작(SwaRef): 웹 서비스 API를 사용하여 PDF 문서에서 정책 제거&quot;

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 문서에 대한 액세스 취소 {#revoking-access-to-documents}

정책으로 보호된 PDF 문서에 대한 액세스를 취소하여 사용자가 문서의 모든 복사본을 액세스할 수 없게 만들 수 있습니다. 사용자가 해지된 PDF 문서를 열려고 하면 개정된 문서를 볼 수 있는 지정된 URL로 리디렉션됩니다. 사용자를 리디렉션하는 URL은 프로그래밍 방식으로 지정해야 합니다. 문서에 대한 액세스를 취소할 경우 사용자가 정책에 의해 보호된 문서를 온라인으로 열어 다음에 문서 보안 서비스와 동기화할 때 변경 내용이 적용됩니다.

문서에 대한 액세스를 취소할 수 있으므로 추가 보안이 제공됩니다. 예를 들어, 최신 버전의 문서를 사용할 수 있으며 더 이상 이전 버전을 볼 수 없도록 할 수 있다고 가정합니다. 이 경우 이전 문서에 대한 액세스가 취소될 수 있으며 액세스가 복원되지 않는 한 문서를 볼 수 없습니다.

>[!NOTE]
>
>문서 보안 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-5}

정책으로 보호된 문서를 취소하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Document Security Client API 개체를 만듭니다.
1. 정책으로 보호된 PDF 문서를 검색합니다.
1. 정책으로 보호된 문서를 취소합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security Client API 개체 만들기**

문서 보안 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만들어야 합니다.

**정책으로 보호된 PDF 문서 검색**

정책 보호 PDF 문서를 검색하려면 해당 문서를 검색해야 합니다. 이미 해지되었거나 정책이 보호된 문서가 아닌 문서는 취소할 수 없습니다.

정책으로 보호된 문서의 라이센스 식별자 값을 알고 있는 경우 정책으로 보호된 PDF 문서를 검색할 필요가 없습니다. 그러나 대부분의 경우 라이센스 식별자 값을 얻으려면 PDF 문서를 검색해야 합니다.

**정책으로 보호된 문서 취소**

정책에 따라 보호된 문서를 취소하려면 정책에 따라 보호된 문서의 라이선스 식별자를 지정합니다. 또한 사용자가 해지된 문서를 열려고 할 때 볼 수 있는 문서의 URL을 지정할 수 있습니다. 즉, 오래된 문서가 해지되었다고 가정합니다. 사용자가 해지된 문서를 열려고 하면 해지된 문서 대신 업데이트된 문서가 표시됩니다.

>[!NOTE]
>
>이미 취소된 문서를 취소하려고 하면 예외가 발생합니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 문서에 정책 적용](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[해지된 문서에 대한 액세스 복원](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### Java API를 사용하여 문서에 대한 액세스 취소 {#revoke-access-to-documents-using-the-java-api}

Document Security API(Java)를 사용하여 정책으로 보호된 PDF 문서에 대한 액세스를 취소합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security Client API 개체 만들기

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `DocumentSecurityClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. 정책으로 보호된 PDF 문서 검색

   * 만들기 `java.io.FileInputStream` 생성자를 사용하여 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 정책으로 보호된 PDF 문서를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 생성자를 사용하여 객체를 전달하고 `java.io.FileInputStream` 개체.

1. 정책으로 보호된 문서 취소

   * 만들기 `DocumentManager` 객체를 호출하여 `DocumentSecurityClient` 개체 `getDocumentManager` 메서드를 사용합니다.
   * 를 호출하여 정책 보호 문서의 라이선스 식별자 값을 검색합니다 `DocumentManager` 개체 `getLicenseId` 메서드를 사용합니다. 전달 `com.adobe.idp.Document` 정책으로 보호된 문서를 나타내는 개체입니다. 이 메서드는 라이선스 식별자 값을 나타내는 문자열 값을 반환합니다.
   * 만들기 `LicenseManager` 객체를 호출하여 `DocumentSecurityClient` 개체 `getLicenseManager` 메서드를 사용합니다.
   * 를 호출하여 정책 보호 문서를 취소합니다 `LicenseManager` 개체 `revokeLicense` 메서드 및 다음 값 전달:

      * 정책 보호 문서의 라이선스 식별자 값을 지정하는 문자열 값(다음 항목의 반환 값 지정) `DocumentManager` 개체 `getLicenseId` 메서드).
      * 의 정적 데이터 멤버 `License` 문서를 취소하는 이유를 지정하는 인터페이스 예를 들어 `License.DOCUMENT_REVISED`.
      * A `java.net.URL` 수정된 문서가 있는 위치를 지정하는 값입니다. 사용자를 다른 URL로 리디렉션하지 않으려면 를 전달할 수 있습니다 `null`.

**코드 예**

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(SOAP 모드): Java API를 사용하여 문서 취소&quot;

### 웹 서비스 API를 사용하여 문서에 대한 액세스 취소 {#revoke-access-to-documents-using-the-web-service-api}

Document Security API(웹 서비스)를 사용하여 정책으로 보호된 PDF 문서에 대한 액세스를 취소합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. Document Security Client API 개체 만들기

   * 만들기 `DocumentSecurityServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `DocumentSecurityServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`) 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 생성할 때 사용됩니다.)
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `DocumentSecurityServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.


1. 정책으로 보호된 PDF 문서 검색

   * 만들기 `BLOB` 생성자를 사용하여 개체를 작성합니다. 다음 `BLOB` 해지된 정책으로 보호된 PDF 문서를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 객체를 사용하여 해당 생성자를 호출하고 정책 보호 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 메서드와 전달
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 필드입니다.

1. 정책으로 보호된 문서 취소

   * 를 호출하여 정책 보호 문서의 라이선스 식별자 값을 검색합니다 `DocumentSecurityServiceClient` 개체 `getLicenseID` 메서드 및 전달 `BLOB` 정책으로 보호된 문서를 나타내는 개체입니다. 이 메서드는 라이선스 식별자를 나타내는 문자열 값을 반환합니다.
   * 를 호출하여 정책 보호 문서를 취소합니다 `DocumentSecurityServiceClient` 개체 `revokeLicense` 메서드 및 다음 값 전달:

      * 정책 보호 문서의 라이선스 식별자 값을 지정하는 문자열 값(다음 항목의 반환 값 지정) `DocumentSecurityServiceService` 개체 `getLicenseId` 메서드).
      * 의 정적 데이터 멤버 `Reason` 문서를 취소하는 이유를 지정하는 열거형입니다. 예를 들어 `Reason.DOCUMENT_REVISED`.
      * A `string` 수정된 문서가 있는 URL 위치를 지정하는 값입니다. 사용자를 다른 URL로 리디렉션하지 않으려면 를 전달할 수 있습니다 `null`.

**코드 예**

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 문서 취소&quot;
* &quot;빠른 시작(SwaRef): 웹 서비스 API를 사용하여 문서 취소&quot;

**추가 참조**

[Word 문서에서 정책 제거](protecting-documents-policies.md#removing-policies-from-word-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 해지된 문서에 대한 액세스 복원 {#reinstating-access-to-revoked-documents}

해지된 PDF 문서에 대한 액세스를 복원할 수 있으므로, 해지된 문서의 모든 사본은 사용자가 액세스할 수 있습니다. 사용자가 취소된 복원된 문서를 열면 문서를 볼 수 있습니다.

>[!NOTE]
>
>문서 보안 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-6}

해지된 PDF 문서에 대한 액세스를 복원하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Document Security Client API 개체를 만듭니다.
1. 해지된 PDF 문서의 라이선스 식별자를 검색합니다.
1. 해지된 PDF 문서에 대한 액세스를 복원합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security Client API 개체 만들기**

문서 보안 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `DocumentSecurityClient` 개체. Document Security 웹 서비스 API를 사용하는 경우 `DocumentSecurityServiceService` 개체.

**해지된 PDF 문서의 라이선스 식별자를 검색합니다**

해지된 PDF 문서를 복원하려면 해지된 PDF 문서의 라이선스 식별자를 검색해야 합니다. 라이센스 식별자 값을 얻은 후에는 해지된 문서를 복원할 수 있습니다. 취소되지 않은 문서를 복원하려고 하면 예외가 발생합니다.

**해지된 PDF 문서에 대한 액세스 복원**

해지된 PDF 문서에 대한 액세스를 복원하려면 해지된 문서의 라이선스 식별자를 지정해야 합니다. 취소되지 않은 PDF 문서에 대한 액세스를 복원하려고 하면 예외가 발생합니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 문서에 정책 적용](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[문서에 대한 액세스 취소](protecting-documents-policies.md#revoking-access-to-documents)

### Java API를 사용하여 해지된 문서에 대한 액세스 복원 {#reinstate-access-to-revoked-documents-using-the-java-api}

문서 보안 API(Java)를 사용하여 해지된 문서에 대한 액세스를 복원합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security Client API 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `DocumentSecurityClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. 해지된 PDF 문서의 라이선스 식별자를 검색합니다.

   * 만들기 `java.io.FileInputStream` 해당 생성자를 사용하고 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 해지된 PDF 문서를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 생성자를 사용하여 객체를 전달하고 `java.io.FileInputStream` 개체.
   * 만들기 `DocumentManager` 객체를 호출하여 `DocumentSecurityClient` 개체 `getDocumentManager` 메서드를 사용합니다.
   * 해지된 문서의 라이선스 식별자 값을 `DocumentManager` 개체 `getLicenseId` 메서드 및 전달 `com.adobe.idp.Document` 해지된 문서를 나타내는 개체입니다. 이 메서드는 라이선스 식별자를 나타내는 문자열 값을 반환합니다.

1. 해지된 PDF 문서에 대한 액세스를 복원합니다.

   * 만들기 `LicenseManager` 객체를 호출하여 `DocumentSecurityClient` 개체 `getLicenseManager` 메서드를 사용합니다.
   * 를 호출하여 해지된 PDF 문서에 대한 액세스를 복원합니다 `LicenseManager` 개체 `unrevokeLicense` 해지된 문서의 라이선스 식별자 값을 전달하는 방법 및 전달

**코드 예**

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(SOAP 모드): 웹 서비스 API를 사용하여 해지된 문서에 대한 액세스 복원&quot;

### 웹 서비스 API를 사용하여 해지된 문서에 대한 액세스 복원 {#reinstate-access-to-revoked-documents-using-the-web-service-api}

문서 보안 API(웹 서비스)를 사용하여 해지된 문서에 대한 액세스를 복원합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. Document Security Client API 개체를 만듭니다.

   * 만들기 `DocumentSecurityServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `DocumentSecurityServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`) 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 생성할 때 사용됩니다.)
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `DocumentSecurityServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.


1. 해지된 PDF 문서의 라이선스 식별자를 검색합니다.

   * 만들기 `BLOB` 생성자를 사용하여 개체를 작성합니다. 다음 `BLOB` 객체는 액세스가 복원된 해지된 PDF 문서를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 개체의 생성자를 호출하고 해지된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 개체를 엽니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 메서드와 전달
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 필드입니다.

1. 해지된 PDF 문서에 대한 액세스를 복원합니다.

   * 해지된 문서의 라이선스 식별자 값을 `DocumentSecurityServiceClient` 개체 `getLicenseID` 메서드 및 전달 `BLOB` 해지된 문서를 나타내는 개체입니다. 이 메서드는 라이선스 식별자를 나타내는 문자열 값을 반환합니다.
   * 를 호출하여 해지된 PDF 문서에 대한 액세스를 복원합니다 `DocumentSecurityServiceClient` 개체 `unrevokeLicense` 해지된 PDF 문서의 라이선스 식별자 값을 지정하는 문자열 값 전달 및 메서드 전달 `DocumentSecurityServiceClient` 개체 `getLicenseId` 메서드).

**코드 예**

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 해지된 문서에 대한 액세스 복원&quot;
* &quot;빠른 시작(SwaRef): 웹 서비스 API를 사용하여 해지된 문서에 대한 액세스 복원&quot;

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 정책 보호 PDF 문서 검사 {#inspecting-policy-protected-pdf-documents}

Document Security Service API(Java 및 웹 서비스)를 사용하여 정책으로 보호된 PDF 문서를 검사할 수 있습니다. 정책으로 보호된 PDF 문서를 검사하면 정책으로 보호된 PDF 문서에 대한 정보가 반환됩니다. 예를 들어 문서의 보안을 유지하는 데 사용된 정책과 문서를 보안한 날짜를 결정할 수 있습니다.

LiveCycle 버전이 8.x 또는 이전 버전인 경우 이 작업을 수행할 수 없습니다. AEM Forms에서 정책에 따라 보호된 문서 검사 지원이 추가되었습니다. LiveCycle 8.x(또는 이전 버전)를 사용하여 정책으로 보호된 문서를 검사하려고 하면 예외가 발생합니다.

>[!NOTE]
>
>문서 보안 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-7}

정책으로 보호된 PDF 문서를 검사하려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. Document Security Client API 개체를 만듭니다.
1. 검사할 정책으로 보호된 문서를 검색합니다.
1. 정책으로 보호된 문서에 대한 정보를 얻습니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security Client API 개체 만들기**

문서 보안 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만듭니다. Java API를 사용하는 경우 `RightsManagementClient` 개체. Document Security 웹 서비스 API를 사용하는 경우 `RightsManagementServiceService` 개체.

**검사할 정책으로 보호된 문서 검색**

정책으로 보호된 문서를 검사하려면 검색합니다. 정책이 보안되지 않거나 해지된 문서를 검사하려고 하면 예외가 발생합니다.

**Inspect 문서**

보호된 문서를 검색한 후 검사할 수 있습니다.

**정책으로 보호된 문서에 대한 정보 얻기**

정책으로 보호된 PDF 문서를 검사하면 이에 대한 정보를 얻을 수 있습니다. 예를 들어 문서의 보안을 유지하는 데 사용되는 정책을 결정할 수 있습니다.

내 정책에 속하는 정책을 사용하여 문서를 보호하는 경우 `RMInspectResult.getPolicysetName` 또는 `RMInspectResult.getPolicysetId`이면 null이 반환됩니다.

정책 세트(내 정책 제외)에 포함된 정책을 사용하여 문서를 보호하는 경우 `RMInspectResult.getPolicysetName` 및 `RMInspectResult.getPolicysetId` 올바른 문자열을 반환합니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하는 Inspect 정책 보호된 PDF 문서 {#inspect-policy-protected-pdf-documents-using-the-java-api}

Inspect은 Document Security Service API(Java)를 사용하여 정책으로 보호된 PDF 문서입니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar와 같은 클라이언트 JAR 파일을 포함합니다. 이러한 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Document Security Client API 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다. (자세한 내용은 [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties))
   * 만들기 `RightsManagementClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. 검사할 정책으로 보호된 문서를 검색합니다.

   * 만들기 `java.io.FileInputStream` 해당 생성자를 사용하여 정책으로 보호된 PDF 문서를 나타내는 개체입니다. PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * 만들기 `com.adobe.idp.Document` 생성자를 사용하여 객체를 전달하고 `java.io.FileInputStream` 개체.

1. Inspect에서 문서를 작성합니다.

   * 만들기 `DocumentManager` 객체를 호출하여 `RightsManagementClient` 개체 `getDocumentManager` 메서드를 사용합니다.
   * Inspect에서 `LicenseManager` 개체 `inspectDocument` 메서드를 사용합니다. 전달 `com.adobe.idp.Document` 정책으로 보호된 PDF 문서를 포함하는 객체입니다. 이 메서드는 `RMInspectResult` 정책으로 보호된 문서에 대한 정보를 포함하는 객체입니다.

1. 정책으로 보호된 문서에 대한 정보를 얻습니다.

   정책에 따라 보호된 문서에 대한 정보를 얻으려면 해당 내용이 속한 메서드를 호출합니다 `RMInspectResult` 개체. 예를 들어 정책 이름을 검색하려면 `RMInspectResult` 개체 `getPolicyName` 메서드를 사용합니다.

**코드 예**

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(SOAP 모드): Java API를 사용하여 정책으로 보호된 PDF 문서 검사&quot;

### 웹 서비스 API를 사용하는 Inspect 정책 보호 PDF 문서 {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Inspect은 Document Security Service API(웹 서비스)를 사용하여 정책으로 보호된 PDF 문서입니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. Document Security Client API 개체를 만듭니다.

   * 만들기 `RightsManagementServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `RightsManagementServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`) 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 생성할 때 사용됩니다.)
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `RightsManagementServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.


1. 검사할 정책으로 보호된 문서를 검색합니다.

   * 만들기 `BLOB` 생성자를 사용하여 개체를 작성합니다. 다음 `BLOB` 객체를 사용하여 검사할 PDF 문서를 저장합니다.
   * 만들기 `System.IO.FileStream` 개체를 생성자로 호출하여 개체를 가져옵니다. PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 메서드를 사용합니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 필드입니다.

1. Inspect에서 문서를 작성합니다.

   Inspect에서 `RightsManagementServiceClient` 개체 `inspectDocument` 메서드를 사용합니다. 전달 `BLOB` 정책으로 보호된 PDF 문서를 포함하는 객체입니다. 이 메서드는 `RMInspectResult` 정책으로 보호된 문서에 대한 정보를 포함하는 객체입니다.

1. 정책으로 보호된 문서에 대한 정보를 얻습니다.

   정책으로 보호된 문서에 대한 정보를 얻으려면 `RMInspectResult` 개체. 예를 들어 정책 이름을 검색하려면 `RMInspectResult` 개체 `policyName` 필드.

**코드 예**

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 정책으로 보호된 PDF 문서 검사&quot;
* &quot;빠른 시작(SwaRef): 웹 서비스 API를 사용하여 정책으로 보호된 PDF 문서 검사&quot;

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 워터마크 만들기 {#creating-watermarks}

워터마크는 문서를 고유하게 식별하고 저작권 침해를 제어하여 문서의 보안을 보장하는 데 도움이 됩니다. 예를 들어 문서의 모든 페이지에 Confidential이라는 워터마크를 만들어 배치할 수 있습니다. 워터마크를 만든 후 정책의 일부로 포함할 수 있습니다. 즉, 새로 생성된 워터마크로 정책의 워터마크 속성을 설정할 수 있습니다. 문서에 워터마크가 포함된 정책이 적용된 후 해당 워터마크가 정책에 의해 보호된 문서에 나타납니다.

>[!NOTE]
>
>문서 보안 관리 권한이 있는 사용자만 워터마크를 만들 수 있습니다. 즉, Document Security 서비스 클라이언트 개체를 만드는 데 필요한 연결 설정을 정의할 때 이러한 사용자를 지정해야 합니다.

>[!NOTE]
>
>문서 보안 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-8}

워터마크를 만들려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Document Security Client API 개체를 만듭니다.
1. 워터마크 특성을 설정합니다.
1. Document Security 서비스에 워터마크를 등록합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security Client API 개체 만들기**

문서 보안 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `RightsManagementClient` 개체. Document Security 웹 서비스 API를 사용하는 경우 `RightsManagementServiceService` 개체.

**워터마크 특성을 설정합니다**

새 워터마크를 만들려면 워터마크 속성을 설정해야 합니다. 이름 특성은 항상 정의해야 합니다. 이름 속성 외에 다음 속성 중 하나 이상을 설정해야 합니다.

* 사용자 지정 텍스트
* 포함된 날짜
* UserIdIncluded
* UserNameIncluded

다음 표에는 웹 서비스를 사용하여 워터마크를 만들 때 필요한 키 및 값 쌍이 나열되어 있습니다.

<table>
 <thead>
  <tr>
   <th><p>키 이름</p></th>
   <th><p>설명</p></th>
   <th><p>값</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERNAME_ENABLED</code></p></td>
   <td><p>문서를 여는 사용자의 사용자 이름이 워터마크의 일부인지 여부를 지정합니다.</p></td>
   <td><p>True 또는 False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERID_ENABLED</code></p></td>
   <td><p>문서를 여는 사용자의 ID가 워터마크의 일부인지 여부를 지정합니다.</p></td>
   <td><p>True 또는 False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>현재 날짜가 워터마크의 일부인지 여부를 지정합니다.</p></td>
   <td><p>True 또는 False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>이 값이 true이면 <code>WaterBackCmd:SRCTEXT</code>.</p></td>
   <td><p>True 또는 False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>워터마크의 불투명도를 지정합니다. 기본값이 지정되지 않은 경우 기본값은 0.5입니다.</p></td>
   <td><p>0.0에서 1.0 사이의 값입니다.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>워터마크의 회전을 지정합니다. 기본값은 0도입니다.</p></td>
   <td><p>0에서 359 사이의 값입니다.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>이 값을 지정한 경우 <code>WaterBackCmd:IS_SIZE_ENABLED</code> 가 있어야 하며 값은 true여야 합니다. 이 속성을 지정하지 않으면 기본 동작이 페이지에 적용됩니다.</p></td>
   <td><p>0.0보다 크고 1.0보다 작거나 같은 값.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>워터마크의 가로 정렬을 지정합니다. 기본값은 center입니다.</p></td>
   <td><p>왼쪽, 가운데 또는 오른쪽</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>워터마크의 세로 정렬을 지정합니다. 기본값은 center입니다.</p></td>
   <td><p>위쪽, 가운데 또는 아래쪽</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>워터마크가 배경인지 여부를 지정합니다. 기본값은 false입니다.</p></td>
   <td><p>True 또는 False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>사용자 지정 배율이 지정된 경우 True입니다. 이 값이 true이면 SCALE도 지정해야 합니다. 이 값이 false이면 기본값은 페이지에 맞습니다.</p></td>
   <td><p>True 또는 False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>워터마크의 사용자 지정 텍스트를 지정합니다. 이 값이 있으면 <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> 또한 가 있어야 하며 true로 설정되어 있어야 합니다.</p></td>
   <td><p>True 또는 False</p></td>
  </tr>
 </tbody>
</table>

모든 워터마크에는 다음 속성 중 하나가 정의되어 있어야 합니다.

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

다른 모든 속성은 선택 사항입니다.

**워터마크 등록**

새 워터마크를 사용하려면 Document Security 서비스에 등록해야 합니다. 워터마크를 등록하면 정책 내에서 사용할 수 있습니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 문서에 정책 적용](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Java API를 사용하여 워터마크 만들기 {#create-watermarks-using-the-java-api}

Document Security API(Java)를 사용하여 워터마크를 만듭니다.

1. 프로젝트 파일을 포함합니다.

   과 같은 클라이언트 JAR 파일을 포함합니다. `adobe-rightsmanagement-client.jar`를 반환합니다.

1. Document Security Client API 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `RightsManagementClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. 워터마크 속성 설정

   * 만들기 `Watermark` 객체를 호출하여 `InfomodelObjectFactory` 개체의 정적 `createWatermark` 메서드를 사용합니다. 이 메서드는 `Watermark` 개체.
   * 를 호출하여 워터마크 이름 속성을 설정합니다 `Watermark` 개체 `setName` 메서드와 정책 이름을 지정하는 문자열 값 전달
   * 를 호출하여 워터마크의 배경 속성을 설정합니다 `Watermark` 개체 `setBackground` 방법 및 전달 `true`. 이 속성을 설정하면 문서의 배경에 워터마크가 나타납니다.
   * 를 호출하여 워터마크의 사용자 지정 텍스트 속성을 설정합니다 `Watermark` 개체 `setCustomText` 워터마크의 텍스트를 나타내는 문자열 값을 전달하는 메서드입니다.
   * 를 호출하여 워터마크의 불투명도 속성을 설정합니다 `Watermark` 개체 `setOpacity` 불투명도 수준을 지정하는 정수 값 전달 및 메서드. 값이 100이면 워터마크가 완전히 불투명하고 값이 0이면 워터마크가 완전히 투명함을 나타냅니다.

1. 워터마크를 등록합니다.

   * 만들기 `WatermarkManager` 객체를 호출하여 `RightsManagementClient` 개체 `getWatermarkManager` 메서드를 사용합니다. 이 메서드는 `WatermarkManager` 개체.
   * 를 호출하여 워터마크를 등록합니다 `WatermarkManager` 개체 `registerWatermark` 메서드 및 전달 `Watermark` 등록할 워터마크를 나타내는 개체입니다. 이 메서드는 워터마크의 식별 값을 나타내는 문자열 값을 반환합니다.

**코드 예**

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(SOAP 모드): Java API를 사용하여 워터마크 만들기&quot;

### 웹 서비스 API를 사용하여 워터마크 만들기 {#create-watermarks-using-the-web-service-api}

Document Security API(웹 서비스)를 사용하여 워터마크를 만듭니다.

1. Document Security Client API 개체를 만듭니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. Document Security Client API 개체를 만듭니다.

   * 만들기 `RightsManagementServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `RightsManagementServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`) 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 생성할 때 사용됩니다.)
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `RightsManagementServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.


1. 워터마크 속성을 설정합니다.

   * 만들기 `WatermarkSpec` 객체를 호출하여 `WatermarkSpec` 생성자입니다.
   * 에 문자열 값을 할당하여 워터마크 이름을 설정합니다. `WatermarkSpec` 개체 `name` 데이터 멤버.
   * 워터마크 설정 `id` 속성에는 문자열 값을 `WatermarkSpec` 개체 `id` 데이터 멤버.
   * 설정할 각 워터마크 속성에 대해 별도의 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체.
   * 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `key` 데이터 멤버(예: `WaterBackCmd:OPACITY)`.
   * 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `value` 데이터 멤버(예: `.25`).
   * 만들기 `MyArrayOf_xsd_anyType` 개체. 각 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체, 호출 `MyArrayOf_xsd_anyType` 개체 `Add` 메서드를 사용합니다. 전달 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체.
   * 을(를) 지정합니다. `MyArrayOf_xsd_anyType` 개체 `WatermarkSpec` 개체 `values` 데이터 멤버.

1. 워터마크를 등록합니다.

   를 호출하여 워터마크를 등록합니다 `RightsManagementServiceClient` 개체 `registerWatermark` 메서드 및 전달 `WatermarkSpec` 등록할 워터마크를 나타내는 개체입니다.

**코드 예**

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 워터마크 만들기&quot;
* &quot;빠른 시작(SwaRef): 웹 서비스 API를 사용하여 워터마크 만들기&quot;

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 워터마크 수정 {#modifying-watermarks}

Document Security Java API 또는 웹 서비스 API를 사용하여 기존 워터마크를 수정할 수 있습니다. 기존 워터마크를 변경하려면 해당 워터마크를 검색하고 특성을 수정한 다음 서버에서 업데이트합니다. 예를 들어 워터마크를 검색하고 불투명도 속성을 수정한다고 가정합니다. 변경 사항을 적용하려면 먼저 워터마크를 업데이트해야 합니다.

워터마크를 수정하면 변경 사항이 워터마크가 적용된 이후 문서에 영향을 줍니다. 즉, 워터마크가 포함된 기존 PDF 문서는 영향을 받지 않습니다.

>[!NOTE]
>
>문서 보안 관리 권한이 있는 사용자만 워터마크를 수정할 수 있습니다. 즉, Document Security 서비스 클라이언트 개체를 만드는 데 필요한 연결 설정을 정의할 때 이러한 사용자를 지정해야 합니다.

>[!NOTE]
>
>문서 보안 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-9}

워터마크를 수정하려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. Document Security Client API 개체를 만듭니다.
1. 수정할 워터마크를 검색합니다.
1. 워터마크 특성을 설정합니다.
1. 워터마크를 업데이트합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security Client API 개체 만들기**

문서 보안 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `DocumentSecurityClient` 개체. Document Security 웹 서비스 API를 사용하는 경우 `DocumentSecurityServiceService` 개체.

**수정할 워터마크를 검색합니다.**

워터마크를 수정하려면 기존 워터마크를 검색해야 합니다. 이름을 지정하거나 해당 식별자 값을 지정하여 워터마크를 검색할 수 있습니다.

**워터마크 특성을 설정합니다**

기존 워터마크를 수정하려면 하나 이상의 워터마크 속성 값을 변경합니다. 웹 서비스를 사용하여 워터마크를 프로그래밍 방식으로 업데이트할 때는 값이 변경되지 않더라도 원래 설정된 모든 속성을 설정해야 합니다. 예를 들어 다음과 같은 워터마크 속성이 설정되어 있다고 가정합니다. `WaterBackCmd:IS_USERID_ENABLED`, `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`, `WaterBackCmd:OPACITY`, 및 `WaterBackCmd:SRCTEXT`. 수정할 유일한 속성은 다음과 같습니다 `WaterBackCmd:OPACITY`를 설정하는 경우 다른 값이 좋습니다.

>[!NOTE]
>
>Java API를 사용하여 워터마크를 수정하는 경우 모든 속성을 지정할 필요가 없습니다. 수정할 워터마크 속성을 설정합니다.

>[!NOTE]
>
>워터마크 속성 이름에 대한 자세한 내용은 [워터마크 만들기](protecting-documents-policies.md#creating-watermarks).

**워터마크 업데이트**

워터마크 속성을 수정한 후 워터마크를 업데이트해야 합니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[워터마크 만들기](protecting-documents-policies.md#creating-watermarks)

### Java API를 사용하여 워터마크 수정 {#modify-watermarks-using-the-java-api}

Document Security API(Java)를 사용하여 워터마크를 수정합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security Client API 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `DocumentSecurityClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. 수정할 워터마크를 검색합니다.

   만들기 `WatermarkManager` 객체를 호출하여 `DocumentSecurityClient` 개체 `getWatermarkManager` 메서드를 사용하여 워터마크 이름을 지정하는 문자열 값을 전달합니다. 이 메서드는 `Watermark` 수정할 워터마크를 나타내는 개체입니다.

1. 워터마크 속성을 설정합니다.

   를 호출하여 워터마크의 불투명도 속성을 설정합니다 `Watermark` 개체 `setOpacity` 불투명도 수준을 지정하는 정수 값 전달 및 메서드. 값이 100이면 워터마크가 완전히 불투명하고 값이 0이면 워터마크가 완전히 투명함을 나타냅니다.

   >[!NOTE]
   >
   >이 예에서는 opacity 속성만 수정합니다.

1. 워터마크를 업데이트합니다.

   * 를 호출하여 워터마크 업데이트 `WatermarkManager` 개체 `updateWatermark` 메서드 및 전달 `Watermark` 속성이 수정된 개체입니다.

**코드 예**

문서 보안 서비스를 사용하는 코드 예에 대해서는 빠른 시작(SOAP 모드)을 참조하십시오. Java API 섹션을 사용하여 워터마크 수정.

### 웹 서비스 API를 사용하여 워터마크 수정 {#modify-watermarks-using-the-web-service-api}

문서 보안 API(웹 서비스)를 사용하여 워터마크를 수정합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. Document Security Client API 개체를 만듭니다.

   * 만들기 `DocumentSecurityServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `RightsManagementServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`) 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 생성할 때 사용됩니다.)
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `DocumentSecurityServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.


1. 수정할 워터마크를 검색합니다.

   를 호출하여 수정할 워터마크를 검색합니다. `DocumentSecurityServiceClient` 개체 `getWatermarkByName` 메서드를 사용합니다. 워터마크 이름을 지정하는 문자열 값을 전달합니다. 이 메서드는 `WatermarkSpec` 수정할 워터마크를 나타내는 개체입니다.

1. 워터마크 속성을 설정합니다.

   * 업데이트할 각 워터마크 속성에 대해 별도의 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체.
   * 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `key` 데이터 멤버(예: `WaterBackCmd:OPACITY)`.
   * 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `value` 데이터 멤버(예: `.50`).
   * 만들기 `MyArrayOf_xsd_anyType` 개체. 각 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체, 호출 `MyArrayOf_xsd_anyType` 개체 `Add` 메서드를 사용합니다. 전달 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체.
   * 을(를) 지정합니다. `MyArrayOf_xsd_anyType` 개체 `WatermarkSpec` 개체 `values` 데이터 멤버.

1. 워터마크를 업데이트합니다.

   를 호출하여 워터마크 업데이트 `DocumentSecurityServiceClient` 개체 `updateWatermark` 메서드 및 전달 `WatermarkSpec` 수정할 워터마크를 나타내는 개체입니다.

**코드 예**

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 워터마크 수정&quot;

## 이벤트 검색 {#searching-for-events}

Rights Management 서비스는 문서에 정책 적용, 정책 보호 문서 열기, 문서에 대한 액세스 취소 등과 같은 특정 작업을 추적합니다. Rights Management 서비스에 대해 이벤트 감사를 사용하도록 설정해야 합니다. 그렇지 않으면 이벤트가 추적되지 않습니다.

이벤트는 다음 카테고리 중 하나에 속합니다.

* 관리자 이벤트는 새 관리자 계정 만들기와 같은 관리자와 관련된 작업입니다.
* 문서 이벤트는 정책으로 보호된 문서를 닫는 것과 같은 문서와 관련된 작업입니다.
* 정책 이벤트는 새 정책 만들기와 같은 정책과 관련된 작업입니다.
* 서비스 이벤트는 사용자 디렉토리와의 동기화 등 Rights Management 서비스와 관련된 작업입니다.

Rights Management Java API 또는 웹 서비스 API를 사용하여 특정 이벤트를 검색할 수 있습니다. 이벤트를 검색하여 특정 이벤트의 로그 파일 만들기와 같은 작업을 수행할 수 있습니다.

>[!NOTE]
>
>Rights Management 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-10}

Rights Management 이벤트를 검색하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Rights Management 클라이언트 API 개체를 만듭니다.
1. 검색할 이벤트를 지정합니다.
1. 이벤트를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Rights Management 클라이언트 API 개체 만들기**

Rights Management 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Rights Management 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `DocumentSecurityClient` 개체. Rights Management 웹 서비스 API를 사용하는 경우 `DocumentSecurityServiceService` 개체.

**검색할 이벤트를 지정합니다**

검색할 이벤트를 지정해야 합니다. 예를 들어 새 정책을 만들 때 발생하는 정책 만들기 이벤트를 검색할 수 있습니다.

**이벤트 검색**

검색할 이벤트를 지정한 후 Java API Rights Management 또는 Rights Management 웹 서비스 API를 사용하여 이벤트를 검색할 수 있습니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 이벤트 검색 {#search-for-events-using-the-java-api}

Rights Management API(Java)를 사용하여 이벤트를 검색합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Rights Management 클라이언트 API 개체 만들기

   만들기 `DocumentSecurityClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.

1. 검색할 이벤트를 지정합니다

   * 만들기 `EventManager` 객체를 호출하여 `DocumentSecurityClient` 개체 `getEventManager` 메서드를 사용합니다. 이 메서드는 `EventManager` 개체.
   * 만들기 `EventSearchFilter` 개체를 생성자로 호출하여 개체를 가져옵니다.
   * 를 호출하여 검색할 이벤트를 지정합니다 `EventSearchFilter` 개체 `setEventCode` 에 속한 정적 데이터 멤버를 전달하는 방법 및 전달 `EventManager` 검색할 이벤트를 나타내는 클래스입니다. 예를 들어 정책 만들기 이벤트를 검색하려면 를 전달합니다 `EventManager.POLICY_CREATE_EVENT`.

   >[!NOTE]
   >
   >을 호출하여 추가 검색 기준을 정의할 수 있습니다 `EventSearchFilter` 개체 메서드. 예를 들어 `setUserName` 이벤트와 연결된 사용자를 지정하는 방법입니다.

1. 이벤트 검색

   를 호출하여 이벤트를 검색합니다. `EventManager` 개체 `searchForEvents` 메서드 및 전달 `EventSearchFilter` 이벤트 검색 기준을 정의하는 개체입니다. 이 메서드는 `Event` 개체.

**코드 예**

Rights Management 서비스를 사용한 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(SOAP): Java API를 사용하여 이벤트 검색&quot;

### 웹 서비스 API를 사용하여 이벤트 검색 {#search-for-events-using-the-web-service-api}

Rights Management API(웹 서비스)를 사용하여 이벤트를 검색합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. Rights Management 클라이언트 API 개체 만들기

   * 만들기 `DocumentSecurityServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `DocumentSecurityServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`) 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 생성할 때 사용됩니다.)
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `DocumentSecurityServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.


1. 검색할 이벤트를 지정합니다

   * 만들기 `EventSpec` 생성자를 사용하여 개체를 작성합니다.
   * 을(를) 설정하여 이벤트가 발생한 기간의 시작을 지정합니다. `EventSpec` 개체 `firstTime.date` 데이터 요소 `DataTime` 이벤트가 발생한 날짜 범위의 시작을 나타내는 인스턴스입니다.
   * 값 할당 `true` 변환 후 `EventSpec` 개체 `firstTime.dateSpecified` 데이터 멤버.
   * 이벤트를 발생시킨 기간의 끝을 `EventSpec` 개체 `lastTime.date` 데이터 요소 `DataTime` 이벤트가 발생한 날짜 범위의 끝을 나타내는 인스턴스입니다.
   * 값 할당 `true` 변환 후 `EventSpec` 개체 `lastTime.dateSpecified` 데이터 멤버.
   * 에 문자열 값을 할당하여 검색할 이벤트를 설정합니다. `EventSpec` 개체 `eventCode` 데이터 멤버. 다음 표에는 이 속성에 지정할 수 있는 숫자 값이 나열되어 있습니다.

   <table>
    <thead>
    <tr>
    <th><p>이벤트 유형</p></th>
    <th><p>값</p></th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td><p><code>ALL_EVENTS</code></p></td>
    <td><p>999년</p></td>
    </tr>
    <tr>
    <td><p><code>USER_CHANGE_PASSWORD_EVENT</code></p></td>
    <td><p>1000</p></td>
    </tr>
    <tr>
    <td><p><code>USER_REGISTER_EVENT</code></p></td>
    <td><p>1001년</p></td>
    </tr>
    <tr>
    <td><p><code>USER_PREREGISTER_EVENT</code></p></td>
    <td><p>1002년</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACTIVATE_EVENT</code></p></td>
    <td><p>1003년</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DEACTIVATE_EVENT</code></p></td>
    <td><p>1004년</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_EVENT</code></p></td>
    <td><p>1005년</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_DENY_EVENT </code></p></td>
    <td><p>1006년</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACCOUNT_LOCK_EVENT</code></p></td>
    <td><p>1007년</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DELETE_EVENT </code></p></td>
    <td><p>1008년</p></td>
    </tr>
    <tr>
    <td><p><code>USER_UPDATE_PROFILE_EVENT </code></p></td>
    <td><p>1009년</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_VIEW_EVENT </code></p></td>
    <td><p>2000년</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_LOW_EVENT </code></p></td>
    <td><p>2001년</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_HIGH_EVENT </code></p></td>
    <td><p>2002년</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SIGN_EVENT </code></p></td>
    <td><p>2003년</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_ADD_ANNOTATION_EVENT </code></p></td>
    <td><p>2004년</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_FORM_FILL_EVENT </code></p></td>
    <td><p>2005년</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CLOSE_EVENT </code></p></td>
    <td><p>2006년</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_MODIFY_EVENT </code></p></td>
    <td><p>2007년</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_SECURITY_HANDLER_EVENT </code></p></td>
    <td><p>2008년</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SWITCH_POLICY_EVENT </code></p></td>
    <td><p>2009년</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_REVOKE_EVENT </code></p></td>
    <td><p>2010년</p></td>
    </tr>
    <tr>
    <td><p><code>$1</code></p></td>
    <td><p>2011년</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SECURE_EVENT </code></p></td>
    <td><p>2012년</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_UNKNOWN_CLIENT_EVENT </code></p></td>
    <td><p>2013년</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_REVOKE_URL_EVENT </code></p></td>
    <td><p>2014년</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_EVENT </code></p></td>
    <td><p>3000년</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_ENABLE_EVENT </code></p></td>
    <td><p>3001년</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DISABLE_EVENT </code></p></td>
    <td><p>3002년</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CREATE_EVENT </code></p></td>
    <td><p>3003년</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DELETE_EVENT </code></p></td>
    <td><p>3004년</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_OWNER_EVENT </code></p></td>
    <td><p>3005년</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CLIENT_SYNC_EVENT </code></p></td>
    <td><p>4000년</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_INFO_EVENT </code></p></td>
    <td><p>4001년</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_COMPLETE_EVENT </code></p></td>
    <td><p>4002년</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_VERSION_MISMATCH_EVENT </code></p></td>
    <td><p>4003년</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CONFIG_CHANGE_EVENT </code></p></td>
    <td><p>4004년</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_ENABLE_OFFLINE_ACCESS_EVENT </code></p></td>
    <td><p>4005년</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ADD_EVENT </code></p></td>
    <td><p>5000</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DELETE_EVENT </code></p></td>
    <td><p>5001년</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_EDIT_EVENT </code></p></td>
    <td><p>5002년</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ACTIVATE_EVENT </code></p></td>
    <td><p>5003년</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DEACTIVATE_EVENT </code></p></td>
    <td><p>5004년</p></td>
    </tr>
    <tr>
    <td><p><code>ERROR_DIRECTORY_SERVICE_EVENT </code></p></td>
    <td><p>6000</p></td>
    </tr>
    <tr>
    <td><p><code>CREATED_POLICYSET_EVENT</code></p></td>
    <td><p>7000년</p></td>
    </tr>
    <tr>
    <td><p><code>DELETED_POLICYSET_EVENT</code></p></td>
    <td><p>7001년</p></td>
    </tr>
    <tr>
    <td><p><code>MODIFIED_POLICYSET_EVENT</code></p></td>
    <td><p>7002년</p></td>
    </tr>
    </tbody>
    </table>

1. 이벤트 검색

   를 호출하여 이벤트를 검색합니다. `DocumentSecurityServiceClient` 개체 `searchForEvents` 메서드 및 전달 `EventSpec` 검색할 이벤트와 최대 결과 수를 나타내는 개체입니다. 이 메서드는 `MyArrayOf_xsd_anyType` 각 요소가 인 컬렉션 `AuditSpec` 인스턴스. 사용 `AuditSpec` 예를 들어 발생한 시간과 같은 이벤트에 대한 정보를 얻을 수 있습니다. 다음 `AuditSpec` 인스턴스에 다음이 포함되어 있습니다. `timestamp` 이 정보를 지정하는 데이터 멤버입니다.

**코드 예**

Rights Management 서비스를 사용한 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 이벤트 검색&quot;
* &quot;빠른 시작(SwaRef): 웹 서비스 API를 사용하여 이벤트 검색&quot;

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Word 문서에 정책 적용 {#applying-policies-to-word-documents}

Rights Management 서비스는 PDF 문서 외에도 Microsoft Word 문서(DOC 파일) 및 기타 Microsoft Office 파일 형식과 같은 추가 문서 형식을 지원합니다. 예를 들어 Word 문서의 보안을 위해 정책을 적용할 수 있습니다. Word 문서에 정책을 적용하면 문서에 대한 액세스를 제한합니다. 문서에 정책이 이미 설정되어 있으면 문서에 정책을 적용할 수 없습니다.

정책 보호 Word 문서를 배포한 후 해당 문서의 사용을 모니터링할 수 있습니다. 즉, 문서의 사용 방법과 사용 중인 사용자를 확인할 수 있습니다. 예를 들어, 사용자가 문서를 연 시점을 확인할 수 있습니다.

>[!NOTE]
>
>문서 보안 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-11}

Word 문서에 정책을 적용하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Document Security Client API 개체를 만듭니다.
1. 정책이 적용되는 Word 문서를 검색합니다.
1. Word 문서에 기존 정책을 적용합니다.
1. 정책으로 보호된 Word 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security Client API 개체 만들기**

문서 보안 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만들어야 합니다.

**Word 문서 검색**

정책을 적용하려면 Word 문서를 검색해야 합니다. Word 문서에 정책을 적용하면 문서를 사용할 때 사용자가 제한됩니다. 예를 들어 정책을 통해 오프라인 상태에서 문서를 열 수 없는 경우, 사용자는 온라인 상태여야 문서를 열 수 있습니다.

**Word 문서에 기존 정책 적용**

Word 문서에 정책을 적용하려면 기존 정책을 참조하고 정책이 속한 정책을 지정해야 합니다. 연결 속성을 설정하는 사용자는 지정된 정책에 액세스할 수 있어야 합니다. 그렇지 않으면 예외가 발생합니다.

**Word 문서를 저장합니다**

Document Security 서비스가 Word 문서에 정책을 적용한 후 정책에 의해 보호된 Word 문서를 DOC 파일로 저장할 수 있습니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[문서에 대한 액세스 취소](protecting-documents-policies.md#revoking-access-to-documents)

### Java API를 사용하여 Word 문서에 정책 적용 {#apply-a-policy-to-a-word-document-using-the-java-api}

Document Security API(Java)를 사용하여 Word 문서에 정책을 적용합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security Client API 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `DocumentSecurityClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. Word 문서를 검색합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하여 Word 문서를 나타내고 Word 문서의 위치를 지정하는 문자열 값을 전달하는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 생성자를 사용하여 객체를 전달하고 `java.io.FileInputStream` 개체.

1. Word 문서에 기존 정책을 적용합니다.

   * 만들기 `DocumentManager` 객체를 호출하여 `DocumentSecurityClient` 개체 `getDocumentManager` 메서드를 사용합니다.
   * Word 문서에 정책을 적용하려면 `DocumentManager` 개체 `protectDocument` 메서드 및 다음 값 전달:

      * 다음 `com.adobe.idp.Document` 정책이 적용되는 Word 문서를 포함하는 객체입니다.
      * 문서의 이름을 지정하는 문자열 값입니다.
      * 정책이 속한 정책 집합의 이름을 지정하는 문자열 값입니다. 을(를) 지정할 수 있습니다 `null` 결과를 가져오는 값 `MyPolicies` 사용 중인 정책 집합입니다.
      * 정책 이름을 지정하는 문자열 값입니다.
      * 문서 게시자인 사용자의 사용자 관리자 도메인의 이름을 나타내는 문자열 값입니다. 이 매개 변수 값은 선택 사항이며 null일 수 있습니다(이 매개 변수가 null이면 다음 매개 변수 값은 null이어야 함).
      * 문서 게시자인 사용자 관리자 사용자의 정식 이름을 나타내는 문자열 값입니다. 이 매개 변수 값은 선택 사항이며 다음 작업을 수행할 수 있습니다. `null` (이 매개 변수가 `null`를 지정하면 이전 매개 변수 값이 `null`).
      * A `com.adobe.livecycle.rightsmanagement.Locale` MS Office 템플릿을 선택하는 데 사용되는 로케일을 나타냅니다. 이 매개 변수 값은 선택 사항이며 다음을 지정할 수 있습니다 `null`.

      다음 `protectDocument` 메서드 반환 `RMSecureDocumentResult` 정책으로 보호된 Word 문서를 포함하는 개체입니다.


1. Word 문서를 저장합니다.

   * 를 호출합니다 `RMSecureDocumentResult` 개체 `getProtectedDoc` 정책으로 보호된 Word 문서를 가져오는 방법입니다. 이 메서드는 `com.adobe.idp.Document` 개체.
   * 만들기 `java.io.File` 개체 및 파일 확장자가 DOC인지 확인합니다.
   * 를 호출합니다 `com.adobe.idp.Document` 개체 `copyToFile` 컨텐츠의 내용 복사 방법 `Document` 개체를 파일에 추가합니다. `Document` 반환되는 개체 `getProtectedDoc` 메서드).

**코드 예**

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(SOAP 모드): Java API를 사용하여 Word 문서에 정책 적용&quot;

### 웹 서비스 API를 사용하여 Word 문서에 정책 적용 {#apply-a-policy-to-a-word-document-using-the-web-service-api}

문서 보안 API(웹 서비스)를 사용하여 Word 문서에 정책을 적용합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. Document Security Client API 개체를 만듭니다.

   * 만들기 `DocumentSecurityServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `DocumentSecurityServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`) 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 생성할 때 사용됩니다.)
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `DocumentSecurityServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.


1. Word 문서를 검색합니다.

   * 만들기 `BLOB` 생성자를 사용하여 개체를 작성합니다. 다음 `BLOB` 정책을 적용할 Word 문서를 저장하는 데 사용되는 개체입니다.
   * 만들기 `System.IO.FileStream` 객체를 사용하여 해당 생성자를 호출하고 Word 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열 크기를 결정합니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 메서드를 사용합니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 필드입니다.

1. Word 문서에 기존 정책을 적용합니다.

   Word 문서에 정책을 적용하려면 `DocumentSecurityServiceClient` 개체 `protectDocument` 메서드 및 다음 값 전달:

   * 다음 `BLOB` 정책이 적용되는 Word 문서를 포함하는 객체입니다.
   * 문서의 이름을 지정하는 문자열 값입니다.
   * 정책이 속한 정책 집합의 이름을 지정하는 문자열 값입니다. 을(를) 지정할 수 있습니다 `null` 결과를 가져오는 값 `MyPolicies` 사용 중인 정책 집합입니다.
   * 정책 이름을 지정하는 문자열 값입니다.
   * 문서 게시자인 사용자의 사용자 관리자 도메인의 이름을 나타내는 문자열 값입니다. 이 매개 변수 값은 선택 사항이며 null일 수 있습니다(이 매개 변수가 null이면 다음 매개 변수 값이 되어야 함). `null`).
   * 문서 게시자인 사용자 관리자 사용자의 정식 이름을 나타내는 문자열 값입니다. 이 매개 변수 값은 선택 사항이며 null일 수 있습니다(이 매개 변수가 null이면 이전 매개 변수 값은 다음과 같아야 함) `null`).
   * A `RMLocale` 로케일 값을 지정하는 값(예: `RMLocale.en`).
   * 정책 식별자 값을 저장하는 데 사용되는 문자열 출력 매개 변수입니다.
   * 정책으로 보호된 식별자 값을 저장하는 데 사용되는 문자열 출력 매개 변수입니다.
   * MIME 유형을 저장하는 데 사용되는 문자열 출력 매개 변수입니다(예: `application/doc`).

   다음 `protectDocument` 메서드 반환 `BLOB` 정책으로 보호된 Word 문서를 포함하는 개체입니다.

1. Word 문서를 저장합니다.

   * 만들기 `System.IO.FileStream` 객체를 생성자를 호출하고 정책 보호 Word 문서의 파일 위치를 나타내는 문자열 값을 전달하여 객체를 지정합니다.
   * 의 데이터 내용을 저장하는 바이트 배열을 만듭니다 `BLOB` 반환되는 개체 `protectDocument` 메서드를 사용합니다. 의 값을 가져와서 바이트 배열을 채웁니다 `BLOB` 개체 `MTOM` 데이터 멤버.
   * 만들기 `System.IO.BinaryWriter` 생성자를 호출하고 전달하여 개체를 `System.IO.FileStream` 개체.
   * 를 호출하여 바이트 배열의 내용을 Word 파일에 씁니다 `System.IO.BinaryWriter` 개체 `Write` 메서드를 사용하여 바이트 배열을 전달합니다.

**코드 예**

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 Word 문서에 정책 적용 &quot;

## Word 문서에서 정책 제거 {#removing-policies-from-word-documents}

문서에서 보안을 제거하기 위해 정책으로 보호된 Word 문서에서 정책을 제거할 수 있습니다. 즉, 더 이상 정책에 의해 문서를 보호하지 않으려는 경우 정책에 따라 보호된 Word 문서를 최신 정책으로 업데이트하려면 정책을 제거하고 업데이트된 정책을 추가하는 대신 정책을 보다 효율적으로 전환할 수 있습니다.

>[!NOTE]
>
>문서 보안 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-12}

정책으로 보호된 Word 문서에서 정책을 제거하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. Document Security Client API 개체를 만듭니다.
1. 정책으로 보호된 Word 문서를 검색합니다.
1. Word 문서에서 정책을 제거합니다.
1. 비보안 Word document.s를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security Client API 개체 만들기**

문서 보안 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만듭니다.

**정책으로 보호된 Word 문서 검색**

정책을 제거하려면 정책으로 보호된 Word 문서를 검색해야 합니다. 정책에 의해 보호되지 않는 Word 문서에서 정책을 제거하려고 하면 예외가 발생합니다.

**Word 문서에서 정책을 제거합니다**

관리자가 연결 설정에 지정된 경우 정책이 보호된 Word 문서에서 정책을 제거할 수 있습니다. 그렇지 않은 경우 문서 보안에 사용되는 정책에 `SWITCH_POLICY` Word 문서에서 정책을 제거하려면 권한이 필요합니다. 또한 AEM Forms 연결 설정에 지정된 사용자에게도 해당 권한이 있어야 합니다. 그렇지 않으면 예외가 발생합니다.

**비보안 Word 문서를 저장합니다**

문서 보안 서비스가 Word 문서에서 정책을 제거한 후 비보안 Word 문서를 DOC 파일로 저장할 수 있습니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Word 문서에 정책 적용](protecting-documents-policies.md#applying-policies-to-word-documents)

### Java API를 사용하여 Word 문서에서 정책을 제거합니다 {#remove-a-policy-from-a-word-document-using-the-java-api}

Document Security API(Java)를 사용하여 정책을 보호하는 Word 문서에서 정책을 제거합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security Client API 개체 만들기

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `RightsManagementClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. 정책으로 보호된 Word 문서 검색

   * 만들기 `java.io.FileInputStream` 해당 생성자를 사용하여 Word 문서의 위치를 지정하는 문자열 값을 전달하여 정책에 의해 보호된 Word 문서를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 생성자를 사용하여 객체를 전달하고 `java.io.FileInputStream` 개체.

1. Word 문서에서 정책을 제거합니다

   * 만들기 `DocumentManager` 객체를 호출하여 `RightsManagementClient` 개체 `getDocumentManager` 메서드를 사용합니다.
   * 를 호출하여 Word 문서에서 정책을 제거합니다 `DocumentManager` 개체 `removeSecurity` 메서드 및 전달 `com.adobe.idp.Document` 정책으로 보호된 Word 문서를 포함하는 개체입니다. 이 메서드는 `com.adobe.idp.Document` 비보안 Word 문서를 포함하는 개체입니다.

1. 비보안 Word 문서를 저장합니다

   * 만들기 `java.io.File` 개체 및 파일 확장자가 DOC인지 확인합니다.
   * 를 호출합니다 `Document` 개체 `copyToFile` 컨텐츠의 내용 복사 방법 `Document` 개체를 파일에 추가합니다. `Document` 반환되는 개체 `removeSecurity` 메서드).

**코드 예**

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(SOAP 모드): Java API를 사용하여 Word 문서에서 정책 제거 &quot;

### 웹 서비스 API를 사용하여 Word 문서에서 정책을 제거합니다 {#remove-a-policy-from-a-word-document-using-the-web-service-api}

Document Security API(웹 서비스)를 사용하여 정책을 보호하는 Word 문서에서 정책을 제거합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. Document Security Client API 개체 만들기

   * 만들기 `RightsManagementServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `RightsManagementServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`) 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 생성할 때 사용됩니다.)
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `RightsManagementServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.


1. 정책으로 보호된 Word 문서 검색

   * 만들기 `BLOB` 생성자를 사용하여 개체를 작성합니다. 다음 `BLOB` 정책을 제거한 정책으로 보호된 Word 문서를 저장하는 데 사용되는 개체입니다.
   * 만들기 `System.IO.FileStream` 객체를 사용하여 해당 생성자를 호출하고 Word 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 메서드와 전달
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 필드입니다.

1. Word 문서에서 정책을 제거합니다

   를 호출하여 Word 문서에서 정책을 제거합니다 `RightsManagementServiceClient` 개체 `removePolicySecurity` 메서드 및 전달 `BLOB` 정책으로 보호된 Word 문서를 포함하는 개체입니다. 이 메서드는 `BLOB` 비보안 Word 문서를 포함하는 개체입니다.

1. 비보안 Word 문서를 저장합니다

   * 만들기 `System.IO.FileStream` 객체를 사용하여 해당 생성자를 호출하고 보안되지 않은 Word 문서의 파일 위치를 나타내는 문자열 값을 전달합니다.
   * 의 데이터 내용을 저장하는 바이트 배열을 만듭니다 `BLOB` 반환되는 개체 `removePolicySecurity` 메서드를 사용합니다. 의 값을 가져와서 바이트 배열을 채웁니다 `BLOB` 개체 `MTOM` 필드.
   * 만들기 `System.IO.BinaryWriter` 생성자를 호출하고 전달하여 개체를 `System.IO.FileStream` 개체.

**코드 예**

문서 보안 서비스를 사용하는 코드 예는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 Word 문서에서 정책 제거&quot;

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
