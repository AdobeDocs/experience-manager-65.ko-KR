---
title: 정책으로 문서 보호
description: Document Security 서비스를 사용하여 Adobe PDF 문서에 기밀 유지 설정을 동적으로 적용하고 문서에 대한 제어 권한을 유지할 수 있습니다. 또한 Document Security 서비스를 통해 사용자는 수신자가 정책으로 보호된 PDF 문서를 사용하는 방법을 제어할 수 있습니다.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: ff42579e-6aaf-433d-8b5d-9e9dd0957250
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '15394'
ht-degree: 0%

---

# 정책으로 문서 보호 {#protecting-documents-with-policies}

**이 문서의 샘플과 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

**문서 보안 서비스 정보**

Document Security 서비스를 통해 사용자는 Adobe PDF 문서에 기밀 유지 설정을 동적으로 적용하고 문서가 광범위하게 배포된 경우에도 문서에 대한 제어 권한을 유지할 수 있습니다.

Document Security 서비스는 사용자가 수신자가 정책으로 보호된 PDF 문서를 사용하는 방법을 제어할 수 있도록 하여 정보가 사용자의 범위를 넘어 확산되는 것을 방지합니다. 사용자는 문서를 열 수 있는 사용자를 지정하고, 문서를 사용할 수 있는 방법을 제한하고, 문서가 배포된 후 문서를 모니터링할 수 있습니다. 사용자는 정책으로 보호된 문서에 대한 액세스를 동적으로 제어할 수 있으며 문서에 대한 액세스를 동적으로 취소할 수도 있습니다.

Document Security 서비스는 Microsoft Word 파일(DOC 파일)과 같은 다른 파일 유형도 보호합니다. Document Security 클라이언트 API를 사용하여 이러한 파일 유형으로 작업할 수 있습니다. 지원되는 버전은 다음과 같습니다.

* Microsoft Office 2003 파일(DOC, XLS, PPT 파일)
* Microsoft Office 2007 파일(DOCX, XLSX, PPTX 파일)
* PTC Pro/E 파일

명확성을 위해 다음 두 절에서는 Word 문서에서 작업하는 방법에 대해 설명합니다.

* [Word 문서에 정책 적용](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Word 문서에서 정책 제거](protecting-documents-policies.md#removing-policies-from-word-documents)

Document Security 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* 정책을 만듭니다. 자세한 내용은 [정책 만들기](protecting-documents-policies.md#creating-policies)를 참조하십시오.
* 정책을 수정합니다. 자세한 내용은 [정책 수정](protecting-documents-policies.md#modifying-policies)을 참조하십시오.
* 정책을 삭제합니다. 자세한 내용은 [정책 삭제](protecting-documents-policies.md#deleting-policies)를 참조하십시오.
* PDF 문서에 정책을 적용합니다. 자세한 내용은 [PDF 문서에 정책 적용](protecting-documents-policies.md#applying-policies-to-pdf-documents)을 참조하십시오.
* PDF 문서에서 정책을 제거합니다. 자세한 내용은 [PDF 문서에서 정책 제거](protecting-documents-policies.md#removing-policies-from-pdf-documents)를 참조하십시오.
* Inspect 정책으로 보호된 문서. 자세한 내용은 [정책으로 보호된 PDF 문서 검사](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents)를 참조하십시오.
* PDF 문서에 대한 액세스 권한을 취소합니다. 자세한 내용은 [문서에 대한 액세스 취소](protecting-documents-policies.md#revoking-access-to-documents)를 참조하십시오.
* 해지된 문서에 대한 액세스 권한을 복원합니다. 자세한 내용은 [해지된 문서에 대한 액세스 복원](protecting-documents-policies.md#reinstating-access-to-revoked-documents)을 참조하십시오.
* 워터마크 만들기 자세한 내용은 [워터마크 만들기](protecting-documents-policies.md#creating-watermarks)를 참조하십시오.
* 이벤트를 검색합니다. 자세한 내용은 [이벤트 검색](protecting-documents-policies.md#searching-for-events)을 참조하세요.

>[!NOTE]
>
>Document Security 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## 정책 만들기 {#creating-policies}

Document Security Java API 또는 웹 서비스 API를 사용하여 프로그래밍 방식으로 정책을 만들 수 있습니다. *정책*&#x200B;은(는) 문서 보안 설정, 승인된 사용자 및 사용 권한이 포함된 정보 모음입니다. 다양한 상황과 사용자에 적합한 보안 설정을 사용하여 원하는 수의 정책을 만들고 저장할 수 있습니다.

정책을 사용하면 다음 작업을 수행할 수 있습니다.

* 문서를 열 수 있는 개인을 지정합니다. 수신자는 조직에 속하거나 조직의 외부에 있을 수 있습니다.
* 수신자가 문서를 사용할 수 있는 방법을 지정합니다. 다양한 Acrobat 및 Adobe Reader 기능에 대한 액세스를 제한할 수 있습니다. 이러한 기능에는 텍스트 인쇄 및 복사 기능, 서명 추가 기능, 문서에 주석 추가 기능 등이 있습니다.
* 정책으로 보호된 문서를 배포한 후에도 언제든지 액세스 및 보안 설정을 변경할 수 있습니다.
* 문서를 배포한 후 사용 상태를 모니터링합니다. 문서가 어떻게 사용되고 있는지, 누가 사용하고 있는지 확인할 수 있습니다. 예를 들어, 문서를 연 날짜를 확인할 수 있습니다.

### 웹 서비스를 사용하여 정책 만들기 {#creating-a-policy-using-web-services}

웹 서비스 API를 사용하여 정책을 만들 때 정책을 설명하는 기존 PDRL(Portable Document Rights Language) XML 파일을 참조하십시오. 정책 권한 및 주도자는 PDL 문서에 정의되어 있습니다. 다음 XML 문서는 PDRL 문서의 예입니다.

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
>Document Security 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary-of-steps}

정책을 만들려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Document Security 클라이언트 API 개체를 만듭니다.
1. 정책의 속성을 설정합니다.
1. 정책 항목을 만듭니다.
1. 정책을 등록합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-rightsmanagement-client.jar
* namespace.jar(AEM Forms이 JBoss에 배포된 경우)
* jaxb-api.jar (AEM Forms이 JBoss에 배포된 경우)
* jaxb-impl.jar(AEM Forms이 JBoss에 배포된 경우)
* jaxb-libs.jar (AEM Forms이 JBoss에 배포된 경우)
* jaxb-xjc.jar(AEM Forms이 JBoss에 배포된 경우)
* relaxngDatatype.jar(AEM Forms이 JBoss에 배포된 경우)
* xsdlib.jar(AEM Forms이 JBoss에 배포된 경우)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar(AEM Forms이 JBoss에 배포되지 않은 경우 다른 JAR 파일 사용)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**Document Security 클라이언트 API 개체 만들기**

Document Security 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만듭니다.

**정책의 특성을 설정합니다**

정책을 만들려면 정책 특성을 설정합니다. 필수 속성은 정책 이름입니다. 정책 이름은 각 정책 집합에 대해 고유해야 합니다. 정책 집합은 단순히 정책의 집합입니다. 정책이 별도의 정책 집합에 속하는 경우 동일한 이름의 정책이 두 개 있을 수 있습니다. 그러나 단일 정책 집합 내의 두 정책은 동일한 정책 이름을 가질 수 없습니다.

또 다른 유용한 속성은 유효 기간입니다. 유효 기간은 승인된 수신자가 정책으로 보호된 문서에 액세스할 수 있는 기간입니다. 이 속성을 설정하지 않으면 정책이 항상 유효합니다.

유효 기간은 다음 옵션 중 하나로 설정할 수 있습니다.

* 문서가 게시된 시간부터 문서에 액세스할 수 있는 설정된 일 수입니다
* 문서에 액세스할 수 없는 종료 날짜
* 문서에 액세스할 수 있는 특정 날짜 범위
* 항상 유효

시작 날짜만 지정할 수 있으며, 이렇게 하면 시작 날짜 이후에 정책이 유효합니다. 종료 날짜만 지정하는 경우 종료 날짜까지 정책이 유효합니다. 그러나 시작 날짜와 종료 날짜가 모두 정의되어 있지 않으면 예외가 throw됩니다.

정책에 속하는 속성을 설정할 때 암호화 설정도 설정할 수 있습니다. 이러한 암호화 설정은 정책이 문서에 적용될 때 적용됩니다. 다음 암호화 값을 지정할 수 있습니다.

* **AES256**: 256비트 키가 있는 AES 암호화 알고리즘을 나타냅니다.
* **AES128**: 128비트 키가 있는 AES 암호화 알고리즘을 나타냅니다.
* **NoEncryption:**&#x200B;은(는) 암호화 없음을 나타냅니다.

`NoEncryption` 옵션을 지정할 때 `PlaintextMetadata` 옵션을 `false`(으)로 설정할 수 없습니다. 그렇게 하려고 하면 예외가 발생합니다.

>[!NOTE]
>
>설정할 수 있는 다른 특성에 대한 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)에서 `Policy` 인터페이스 설명을 참조하십시오.

**정책 항목 만들기**

정책 항목은 그룹 및 사용자인 주도자와 권한을 정책에 연결합니다. 정책에는 하나 이상의 정책 항목이 있어야 합니다. 예를 들어 다음 작업을 수행한다고 가정해 보겠습니다.

* 그룹이 온라인 상태에서만 문서를 볼 수 있고 수신자는 문서를 복사할 수 없도록 하는 정책 항목을 만들고 등록합니다.
* 정책에 정책 항목을 첨부합니다.
* Acrobat을 사용하여 정책으로 문서를 보호합니다.

이러한 작업을 수행하면 수신자는 온라인에서만 문서를 볼 수 있고 문서를 복사할 수 없습니다. 이 문서는 보안이 제거될 때까지 보안 상태로 유지됩니다.

**정책 등록**

새 정책을 사용하려면 먼저 등록해야 합니다. 정책을 등록한 후 이를 사용하여 문서를 보호할 수 있습니다.

### Java API를 사용하여 정책 만들기 {#create-a-policy-using-the-java-api}

Java(Document Security API)를 사용하여 정책을 만듭니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security 클라이언트 API 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `DocumentSecurityClient` 개체를 만듭니다.

1. 정책의 속성을 설정합니다.

   * `InfomodelObjectFactory` 개체의 정적 `createPolicy` 메서드를 호출하여 `Policy` 개체를 만듭니다. 이 메서드는 `Policy` 개체를 반환합니다.
   * `Policy` 개체의 `setName` 메서드를 호출하고 정책 이름을 지정하는 문자열 값을 전달하여 정책의 이름 특성을 설정합니다.
   * `Policy` 개체의 `setDescription` 메서드를 호출하고 정책 설명을 지정하는 문자열 값을 전달하여 정책 설명을 설정합니다.
   * `Policy` 개체의 `setPolicySetName` 메서드를 호출하고 정책 집합 이름을 지정하는 문자열 값을 전달하여 새 정책이 속하는 정책 집합을 지정하십시오. (이 매개 변수 값에 대해 `null`을(를) 지정하면 정책이 *내 정책* 정책 집합에 추가됩니다.)
   * `InfomodelObjectFactory` 개체의 정적 `createValidityPeriod` 메서드를 호출하여 정책의 유효 기간을 만드십시오. 이 메서드는 `ValidityPeriod` 개체를 반환합니다.
   * `ValidityPeriod` 개체의 `setRelativeExpirationDays` 메서드를 호출하고 일 수를 지정하는 정수 값을 전달하여 정책으로 보호된 문서에 액세스할 수 있는 일 수를 설정하십시오.
   * `Policy` 개체의 `setValidityPeriod` 메서드를 호출하고 `ValidityPeriod` 개체를 전달하여 정책의 유효 기간을 설정하십시오.

1. 정책 항목을 만듭니다.

   * `InfomodelObjectFactory` 개체의 정적 `createPolicyEntry` 메서드를 호출하여 정책 항목을 만듭니다. 이 메서드는 `PolicyEntry` 개체를 반환합니다.
   * `InfomodelObjectFactory` 개체의 정적 `createPermission` 메서드를 호출하여 정책의 권한을 지정하십시오. 권한을 나타내는 `Permission` 인터페이스에 속하는 정적 데이터 멤버를 전달합니다. 이 메서드는 `Permission` 개체를 반환합니다. 예를 들어 사용자가 정책으로 보호된 PDF 문서에서 데이터를 복사할 수 있는 권한을 추가하려면 `Permission.COPY`을(를) 전달합니다. (추가할 각 권한에 대해 이 단계를 반복합니다.)
   * `PolicyEntry` 개체의 `addPermission` 메서드를 호출하고 `Permission` 개체를 전달하여 정책 항목에 권한을 추가하십시오. (만든 각 `Permission` 개체에 대해 이 단계를 반복합니다.)
   * `InfomodelObjectFactory` 개체의 정적 `createSpecialPrincipal` 메서드를 호출하여 정책 주체를 만듭니다. 주체를 나타내는 `InfomodelObjectFactory` 개체에 속하는 데이터 멤버를 전달합니다. 이 메서드는 `Principal` 개체를 반환합니다. 예를들어, 문서의 게시자를 주체로 추가하려면 `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`을(를) 전달합니다.
   * `PolicyEntry` 개체의 `setPrincipal` 메서드를 호출하고 `Principal` 개체를 전달하여 정책 항목에 주체를 추가합니다.
   * `Policy` 개체의 `addPolicyEntry` 메서드를 호출하고 `PolicyEntry` 개체를 전달하여 정책에 정책 항목을 추가하십시오.

1. 정책을 등록합니다.

   * `DocumentSecurityClient` 개체의 `getPolicyManager` 메서드를 호출하여 `PolicyManager` 개체를 만듭니다.
   * `PolicyManager` 개체의 `registerPolicy` 메서드를 호출하고 다음 값을 전달하여 정책을 등록합니다.

      * 등록할 정책을 나타내는 `Policy` 개체입니다.

   * 정책이 속한 정책 집합을 나타내는 문자열 값입니다.

   연결 설정 내에서 AEM Forms 관리자 계정을 사용하여 `DocumentSecurityClient` 개체를 만드는 경우 `registerPolicy` 메서드를 호출할 때 정책 집합 이름을 지정하십시오. 정책 집합에 대한 `null` 값을 전달하면 관리자 *내 정책* 정책 집합에 정책이 만들어집니다.

   연결 설정 내에서 Document Security 사용자를 사용하는 경우 정책만 허용하는 오버로드된 `registerPolicy` 메서드를 호출할 수 있습니다. 즉, 정책 세트 이름을 지정할 필요가 없습니다. 그러나 정책이 *내 정책* 정책 집합에 추가됩니다. 이 정책 집합에 새 정책을 추가하지 않으려면 `registerPolicy` 메서드를 호출할 때 정책 집합 이름을 지정하십시오.

   >[!NOTE]
   >
   >정책을 생성할 때 기존 정책 세트를 참조하십시오. 존재하지 않는 정책 집합을 지정하면 예외가 throw됩니다.

Document Security 서비스를 사용하는 코드 예에 대해서는 다음을 참조하십시오.

* &quot;빠른 시작(SOAP 모드): Java API를 사용하여 정책 만들기&quot;

### 웹 서비스 API를 사용하여 정책 만들기 {#create-a-policy-using-the-web-service-api}

Document Security API(웹 서비스)를 사용하여 정책을 만듭니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. Document Security 클라이언트 API 개체를 만듭니다.

   * 기본 생성자를 사용하여 `DocumentSecurityServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `DocumentSecurityServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `RightsManagementServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `RightsManagementServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `RightsManagementServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.

   * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 정책의 속성을 설정합니다.

   * 해당 생성자를 사용하여 `PolicySpec` 개체를 만듭니다.
   * `PolicySpec` 개체의 `name` 데이터 멤버에 문자열 값을 할당하여 정책 이름을 설정합니다.
   * `PolicySpec` 개체의 `description` 데이터 멤버에 문자열 값을 할당하여 정책의 설명을 설정하십시오.
   * `PolicySpec` 개체의 `policySetName` 데이터 멤버에 문자열 값을 할당하여 정책이 속하는 정책 집합을 지정하십시오. 기존 정책 집합 이름을 지정하십시오. (이 매개 변수 값에 `null`을(를) 지정하면 정책이 *내 정책*&#x200B;에 추가됩니다.)
   * 정수 값을 `PolicySpec` 개체의 `offlineLeasePeriod` 데이터 멤버에 할당하여 정책의 오프라인 임대 기간을 설정하십시오.
   * `PolicySpec` 개체의 `policyXml` 데이터 멤버를 PDL XML 데이터를 나타내는 문자열 값으로 설정합니다. 이 작업을 수행하려면 생성자를 사용하여 .NET `StreamReader` 개체를 만드십시오. 정책을 나타내는 PDRL XML 파일의 위치를 `StreamReader` 생성자에 전달합니다. 그런 다음 `StreamReader` 개체의 `ReadLine` 메서드를 호출하고 반환 값을 문자열 변수에 할당합니다. `ReadLine` 메서드가 null을 반환할 때까지 `StreamReader` 개체를 반복합니다. `PolicySpec` 개체의 `policyXml` 데이터 멤버에 문자열 변수를 할당합니다.

1. 정책 항목을 만듭니다.

   Document Security 웹 서비스 API를 사용하여 정책을 만들 때는 정책 항목을 만들 필요가 없습니다. 정책 항목은 PDRL 문서에 정의됩니다.

1. 정책을 등록합니다.

   `DocumentSecurityServiceClient` 개체의 `registerPolicy` 메서드를 호출하고 다음 값을 전달하여 정책을 등록합니다.

   * 등록할 정책을 나타내는 `PolicySpec` 개체입니다.
   * 정책이 속한 정책 집합을 나타내는 문자열 값입니다. *MyPolicies* 정책 집합에 정책이 추가되는 `null` 값을 지정할 수 있습니다.

   연결 설정 내에서 AEM Forms 관리자 계정을 사용하여 `DocumentSecurityClient` 개체를 만드는 경우 `registerPolicy` 메서드를 호출할 때 정책 집합 이름을 지정하십시오.

   연결 설정 내에서 Document SecurityDocument Security 사용자를 사용하는 경우 정책만 허용하는 오버로드된 `registerPolicy` 메서드를 호출할 수 있습니다. 즉, 정책 세트 이름을 지정할 필요가 없습니다. 그러나 정책이 *내 정책* 정책 집합에 추가됩니다. 이 정책 집합에 새 정책을 추가하지 않으려면 `registerPolicy` 메서드를 호출할 때 정책 집합 이름을 지정하십시오.

   >[!NOTE]
   >
   >정책을 만들 때 정책 집합을 지정할 때는 기존 정책 집합을 지정해야 합니다. 존재하지 않는 정책 집합을 지정하면 예외가 throw됩니다.

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 정책 만들기&quot;
* &quot;빠른 시작(SwaRef): 웹 서비스 API를 사용하여 정책 만들기&quot;

## 정책 수정 {#modifying-policies}

Document Security Java API 또는 웹 서비스 API를 사용하여 기존 정책을 수정할 수 있습니다. 기존 정책을 변경하려면 정책을 검색하고 수정한 다음 서버에서 정책을 업데이트합니다. 예를 들어 기존 정책을 검색하고 유효 기간을 연장한다고 가정해 보겠습니다. 변경 사항이 적용되기 전에 정책을 업데이트해야 합니다.

비즈니스 요구 사항이 변경되고 정책이 이러한 요구 사항을 더 이상 반영하지 않을 때 정책을 수정할 수 있습니다. 정책을 만드는 대신 기존 정책을 업데이트할 수 있습니다.

웹 서비스를 사용하여 정책 속성을 수정하려면(예: JAX-WS로 만든 Java 프록시 클래스 사용) 정책이 Document Security 서비스에 등록되어 있는지 확인해야 합니다. 그런 다음 `PolicySpec.getPolicyXml` 메서드를 사용하여 기존 정책을 참조하고 해당 메서드를 사용하여 정책 특성을 수정할 수 있습니다. 예를 들어 `PolicySpec.setOfflineLeasePeriod` 메서드를 호출하여 오프라인 임대 기간을 수정할 수 있습니다.

>[!NOTE]
>
>Document Security 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-1}

기존 정책을 수정하려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. Document Security 클라이언트 API 개체를 만듭니다.
1. 기존 정책을 검색합니다.
1. 정책 속성을 변경합니다.
1. 정책을 업데이트합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security 클라이언트 API 개체 만들기**

Document Security 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `RightsManagementClient` 개체를 만듭니다. Document Security 웹 서비스 API를 사용하는 경우 `RightsManagementServiceService` 개체를 만듭니다.

**기존 정책 검색**

기존 정책을 검색하여 수정합니다. 정책을 검색하려면 정책 이름과 정책이 속한 정책 집합을 지정합니다. 정책 집합 이름에 `null` 값을 지정하면 *내 정책* 정책 집합에서 정책을 검색합니다.

**정책의 특성을 설정합니다**

정책을 수정하려면 정책 속성의 값을 수정합니다. 변경할 수 없는 유일한 정책 속성은 이름 속성입니다. 예를 들어 정책의 오프라인 임대 기간을 변경하려면 정책의 오프라인 임대 기간 속성 값을 수정할 수 있습니다.

웹 서비스를 사용하여 정책의 오프라인 임대 기간을 수정할 때 `PolicySpec` 인터페이스의 `offlineLeasePeriod` 필드가 무시됩니다. 오프라인 임대 기간을 업데이트하려면 PDRL XML 문서에서 `OfflineLeasePeriod` 요소를 수정하십시오. 그런 다음 `PolicySpec` 인터페이스의 `policyXML` 데이터 멤버를 사용하여 업데이트된 PDRL XML 문서를 참조합니다.

>[!NOTE]
>
>설정할 수 있는 다른 특성에 대한 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)에서 `Policy` 인터페이스 설명을 참조하십시오.

**정책 업데이트**

정책에 대한 변경 사항이 적용되기 전에 Document Security 서비스로 정책을 업데이트해야 합니다. 다음 번에 정책으로 보호된 문서가 Document Security 서비스와 동기화되면 문서를 보호하는 정책에 대한 변경 사항이 업데이트됩니다.

### Java API를 사용하여 기존 정책 수정 {#modify-existing-policies-using-the-java-api}

Document Security API(Java)를 사용하여 기존 정책을 수정합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security 클라이언트 API 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `RightsManagementClient` 개체를 만듭니다.

1. 기존 정책을 검색합니다.

   * `RightsManagementClient` 개체의 `getPolicyManager` 메서드를 호출하여 `PolicyManager` 개체를 만듭니다.
   * `PolicyManager` 개체의 `getPolicy` 메서드를 호출하고 다음 값을 전달하여 업데이트할 정책을 나타내는 `Policy` 개체를 만듭니다.&quot;

      * 정책이 속한 정책 집합 이름을 나타내는 문자열 값입니다. `MyPolicies` 정책 집합이 사용되는 `null`을(를) 지정할 수 있습니다.
      * 정책 이름을 나타내는 문자열 값입니다.

1. 정책의 속성을 설정합니다.

   비즈니스 요구 사항을 충족하도록 정책의 속성을 변경합니다. 예를 들어 정책의 오프라인 임대 기간을 변경하려면 `Policy` 개체의 `setOfflineLeasePeriod` 메서드를 호출하십시오.

1. 정책을 업데이트합니다.

   `PolicyManager` 개체의 `updatePolicy` 메서드를 호출하여 정책을 업데이트합니다. 업데이트할 정책을 나타내는 `Policy` 개체를 전달합니다.

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 빠른 시작(SOAP 모드): Java API를 사용하여 정책 수정 섹션을 참조하십시오.

### 웹 서비스 API를 사용하여 기존 정책 수정 {#modify-existing-policies-using-the-web-service-api}

Document Security API(웹 서비스)를 사용하여 기존 정책을 수정합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. Document Security 클라이언트 API 개체를 만듭니다.

   * 기본 생성자를 사용하여 `RightsManagementServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `RightsManagementServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `RightsManagementServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `RightsManagementServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `RightsManagementServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.

   * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 기존 정책을 검색합니다.

   `RightsManagementServiceClient` 개체의 `getPolicy` 메서드를 호출하고 다음 값을 전달하여 수정할 정책을 나타내는 `PolicySpec` 개체를 만듭니다.

   * 정책이 속한 정책 집합 이름을 지정하는 문자열 값입니다. `MyPolicies` 정책 집합이 사용되는 `null`을(를) 지정할 수 있습니다.
   * 정책의 이름을 지정하는 문자열 값입니다.

1. 정책의 속성을 설정합니다.

   비즈니스 요구 사항을 충족하도록 정책의 속성을 변경합니다.

1. 정책을 업데이트합니다.

   `RightsManagementServiceClient` 개체의 `updatePolicyFromSDK` 메서드를 호출하고 업데이트할 정책을 나타내는 `PolicySpec` 개체를 전달하여 정책을 업데이트합니다.

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 정책 수정&quot;
* &quot;빠른 시작(SwaRef): 웹 서비스 API를 사용하여 정책 수정&quot;

## 정책 삭제 {#deleting-policies}

Document Security Java API 또는 웹 서비스 API를 사용하여 기존 정책을 삭제할 수 있습니다. 정책이 삭제되면 더 이상 문서 보호에 사용할 수 없습니다. 그러나 정책을 사용하는 정책으로 보호된 기존 문서는 여전히 보호됩니다. 새 정책을 사용할 수 있게 되면 정책을 삭제할 수 있습니다.

>[!NOTE]
>
>Document Security 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-2}

기존 정책을 삭제하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. Document Security 클라이언트 API 개체를 만듭니다.
1. 정책을 삭제합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security 클라이언트 API 개체 만들기**

Document Security 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `RightsManagementClient` 개체를 만듭니다. Document Security 웹 서비스 API를 사용하는 경우 `RightsManagementServiceService` 개체를 만듭니다.

**정책 삭제**

정책을 삭제하려면 삭제할 정책과 정책이 속한 정책 집합을 지정합니다. AEM Forms을 호출하는 데 설정을 사용하는 사용자는 정책을 삭제할 권한이 있어야 합니다. 그렇지 않으면 예외가 발생합니다. 마찬가지로 존재하지 않는 정책을 삭제하려고 하면 예외가 발생합니다.

### Java API를 사용하여 정책 삭제 {#delete-policies-using-the-java-api}

Document Security API(Java)를 사용하여 정책을 삭제합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security 클라이언트 API 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `RightsManagementClient` 개체를 만듭니다.

1. 정책을 삭제합니다.

   * `RightsManagementClient` 개체의 `getPolicyManager` 메서드를 호출하여 `PolicyManager` 개체를 만듭니다.
   * `PolicyManager` 개체의 `deletePolicy` 메서드를 호출하고 다음 값을 전달하여 정책을 삭제합니다.

      * 정책이 속한 정책 집합 이름을 지정하는 문자열 값입니다. `MyPolicies` 정책 집합이 사용되는 `null`을(를) 지정할 수 있습니다.
      * 삭제할 정책의 이름을 지정하는 문자열 값입니다.

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(SOAP 모드): Java API를 사용하여 정책 삭제&quot;

### 웹 서비스 API를 사용하여 정책 삭제 {#delete-policies-using-the-web-service-api}

Document Security API(웹 서비스)를 사용하여 정책을 삭제합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. Document Security 클라이언트 API 개체를 만듭니다.

   * 기본 생성자를 사용하여 `RightsManagementServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `RightsManagementServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `RightsManagementServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `RightsManagementServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `RightsManagementServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.

   * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 정책을 삭제합니다.

   `RightsManagementServiceClient` 개체의 `deletePolicy` 메서드를 호출하고 다음 값을 전달하여 정책을 삭제합니다.

   * 정책이 속한 정책 집합 이름을 지정하는 문자열 값입니다. `MyPolicies` 정책 집합이 사용되는 `null`을(를) 지정할 수 있습니다.
   * 삭제할 정책의 이름을 지정하는 문자열 값입니다.

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 정책 삭제&quot;
* &quot;빠른 시작(SwaRef): 웹 서비스 API를 사용하여 정책 삭제&quot;

## PDF 문서에 정책 적용 {#applying-policies-to-pdf-documents}

PDF 문서에 정책을 적용하여 문서를 보호할 수 있습니다. PDF 문서에 정책을 적용하여 문서에 대한 액세스를 제한합니다. 정책으로 문서가 이미 보호되어 있는 경우에는 문서에 정책을 적용할 수 없습니다.

문서가 열려 있는 동안 텍스트 인쇄 및 복사, 변경, 문서에 서명 및 주석 추가 등 Acrobat 및 Adobe Reader 기능에 대한 액세스를 제한할 수도 있습니다. 또한 사용자가 문서에 더 이상 액세스하지 못하도록 하려는 경우 정책으로 보호된 PDF 문서를 취소할 수 있습니다.

배포한 후 정책으로 보호된 문서의 사용을 모니터링할 수 있습니다. 즉, 문서가 어떻게 사용되고 있으며 누가 사용하고 있는지 확인할 수 있습니다. 예를 들어, 누군가가 문서를 언제 열었는지 확인할 수 있습니다.

>[!NOTE]
>
>Document Security 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-3}

PDF 문서에 정책을 적용하려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. Document Security 클라이언트 API 개체를 만듭니다.
1. 정책이 적용되는 PDF 문서를 검색합니다.
1. PDF 문서에 기존 정책을 적용합니다.
1. 정책으로 보호된 PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security Client APIobject 만들기**

Document Security 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만듭니다. Java API를 사용하는 경우 `DocumentSecurityClient` 개체를 만듭니다. Document Security 웹 서비스 API를 사용하는 경우 `DocumentSecurityServiceService` 개체를 만듭니다.

**PDF 문서 검색**

PDF 문서를 검색하여 정책을 적용할 수 있습니다. PDF 문서에 정책을 적용하면 문서 사용 시 사용자가 제한됩니다. 예를 들어 오프라인일 때 정책에서 문서를 열 수 있도록 설정하지 않은 경우 사용자가 문서를 열려면 온라인 상태여야 합니다.

**PDF 문서에 기존 정책 적용**

PDF 문서에 정책을 적용하려면 기존 정책을 참조하고 정책이 속한 정책 세트를 지정합니다. 연결 속성을 설정하는 사용자는 지정된 정책에 액세스할 수 있어야 합니다. 그렇지 않은 경우 예외가 발생합니다.

**PDF 문서 저장**

Document Security 서비스가 PDF 문서에 정책을 적용한 후 정책으로 보호된 PDF 문서를 PDF 파일로 저장할 수 있습니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[문서에 대한 액세스 취소](protecting-documents-policies.md#revoking-access-to-documents)

### Java API를 사용하여 PDF 문서에 정책 적용 {#apply-a-policy-to-a-pdf-document-using-the-java-api}

Document Security API(Java)를 사용하여 PDF 문서에 정책 적용:

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security 클라이언트 API 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `RightsManagementClient` 개체를 만듭니다.

1. PDF 문서를 검색합니다.

   * 생성자를 사용하여 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다. PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하고 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. PDF 문서에 기존 정책을 적용합니다.

   * `RightsManagementClient` 개체의 `getDocumentManager` 메서드를 호출하여 `DocumentManager` 개체를 만듭니다.
   * `DocumentManager` 개체의 `protectDocument` 메서드를 호출하고 다음 값을 전달하여 PDF 문서에 정책을 적용합니다.

      * 정책이 적용되는 PDF 문서가 포함된 `com.adobe.idp.Document` 개체입니다.
      * 문서의 이름을 지정하는 문자열 값입니다.
      * 정책이 속한 정책 집합의 이름을 지정하는 문자열 값입니다. `MyPolicies` 정책 집합이 사용되는 `null` 값을 지정할 수 있습니다.
      * 정책 이름을 지정하는 문자열 값입니다.
      * 문서의 게시자인 사용자의 사용자 관리자 도메인 이름을 나타내는 문자열 값입니다. 이 매개변수 값은 선택 사항이며 null일 수 있습니다(이 매개변수가 null이면 다음 매개변수 값은 null이어야 함).
      * 문서의 게시자인 사용자 관리자 사용자의 정식 이름을 나타내는 문자열 값입니다. 이 매개 변수 값은 선택 사항이며 `null`일 수 있습니다(이 매개 변수가 null이면 이전 매개 변수 값은 `null`이어야 함).
      * MS Office 템플릿을 선택하는 데 사용되는 로케일을 나타내는 `com.adobe.livecycle.rightsmanagement.Locale`입니다. 이 매개 변수 값은 선택 사항이며 PDF 문서에 사용되지 않습니다. PDF 문서의 보안을 유지하려면 `null`을(를) 지정하십시오.

     `protectDocument` 메서드가 정책으로 보호된 PDF 문서를 포함하는 `RMSecureDocumentResult` 개체를 반환합니다.

1. PDF 문서를 저장합니다.

   * `RMSecureDocumentResult` 개체의 `getProtectedDoc` 메서드를 호출하여 정책으로 보호된 PDF 문서를 가져옵니다. 이 메서드는 `com.adobe.idp.Document` 개체를 반환합니다.
   * `java.io.File` 개체를 만들고 파일 확장명이 PDF 상태인지 확인하십시오.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 `Document` 개체의 내용을 파일에 복사합니다(`getProtectedDoc` 메서드에서 반환된 `Document` 개체를 사용하는지 확인).

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(EJB 모드): Java API를 사용하여 PDF 문서에 정책 적용&quot;
* &quot;빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서에 정책 적용&quot;

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 PDF 문서에 정책 적용 {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

Document Security API(웹 서비스)를 사용하여 PDF 문서에 정책 적용:

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. Document Security 클라이언트 API 개체를 만듭니다.

   * 기본 생성자를 사용하여 `RightsManagementServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `RightsManagementServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `RightsManagementServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `RightsManagementServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `RightsManagementServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.

   * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. PDF 문서를 검색합니다.

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 정책이 적용되는 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열 크기를 결정합니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 해당 `MTOM` 필드를 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.

1. PDF 문서에 기존 정책을 적용합니다.

   `RightsManagementServiceClient` 개체의 `protectDocument` 메서드를 호출하고 다음 값을 전달하여 PDF 문서에 정책을 적용합니다.

   * 정책이 적용되는 PDF 문서가 포함된 `BLOB` 개체입니다.
   * 문서의 이름을 지정하는 문자열 값입니다.
   * 정책이 속한 정책 집합의 이름을 지정하는 문자열 값입니다. `MyPolicies` 정책 집합이 사용되는 `null` 값을 지정할 수 있습니다.
   * 정책 이름을 지정하는 문자열 값입니다.
   * 문서의 게시자인 사용자의 사용자 관리자 도메인 이름을 나타내는 문자열 값입니다. 이 매개 변수 값은 선택 사항이며 null일 수 있습니다(이 매개 변수가 null이면 다음 매개 변수 값은 `null`이어야 함).
   * 문서의 게시자인 사용자 관리자 사용자의 정식 이름을 나타내는 문자열 값입니다. 이 매개 변수 값은 선택 사항이며 null일 수 있습니다(이 매개 변수가 null이면 이전 매개 변수 값은 `null`이어야 함).
   * 로케일 값을 지정하는 `RMLocale` 값(예: `RMLocale.en`)입니다.
   * 정책 식별자 값을 저장하는 데 사용되는 문자열 출력 매개 변수입니다.
   * 정책으로 보호된 식별자 값을 저장하는 데 사용되는 문자열 출력 매개 변수입니다.
   * MIME 형식을 저장하는 데 사용되는 문자열 출력 매개 변수(예: `application/pdf`)입니다.

   `protectDocument` 메서드가 정책으로 보호된 PDF 문서를 포함하는 `BLOB` 개체를 반환합니다.

1. PDF 문서를 저장합니다.

   * 해당 생성자를 호출하고 정책으로 보호된 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `protectDocument` 메서드에서 반환된 `BLOB` 개체의 데이터 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 씁니다.

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 PDF 문서에 정책 적용&quot;
* &quot;빠른 시작(SwaRef): 웹 서비스 API를 사용하여 PDF 문서에 정책 적용&quot;

## PDF 문서에서 정책 제거 {#removing-policies-from-pdf-documents}

정책으로 보호된 문서에서 정책을 제거하여 문서에서 보안을 제거할 수 있습니다. 즉, 더 이상 정책으로 문서를 보호하지 않으려는 경우. 정책으로 보호된 문서를 최신 정책으로 업데이트하려면 정책을 제거하고 업데이트된 정책을 추가하는 대신 정책을 전환하는 것이 더 효율적입니다.

>[!NOTE]
>
>Document Security 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-4}

정책으로 보호된 PDF 문서에서 정책을 제거하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. Document Security 클라이언트 API 개체를 만듭니다.
1. 정책으로 보호된 PDF 문서를 검색합니다.
1. PDF 문서에서 정책을 제거합니다.
1. 보안되지 않은 PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security 클라이언트 API 개체 만들기**

Document Security 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만듭니다.

**정책으로 보호된 PDF 문서 검색**

정책으로 보호된 PDF 문서를 검색하여 정책을 제거할 수 있습니다. 정책으로 보호되지 않는 PDF 문서에서 정책을 제거하려고 하면 예외가 발생합니다.

**PDF 문서에서 정책 제거**

연결 설정에 관리자가 지정되어 있는 경우 정책으로 보호된 PDF 문서에서 정책을 제거할 수 있습니다. 그렇지 않으면 문서 보안에 사용되는 정책에 PDF 문서에서 정책을 제거하려면 `SWITCH_POLICY` 권한이 있어야 합니다. 또한 AEM Forms 연결 설정에 지정된 사용자에게도 해당 권한이 있어야 합니다. 그렇지 않으면 예외가 throw됩니다.

**보안되지 않은 PDF 문서 저장**

Document Security 서비스가 PDF 문서에서 정책을 제거한 후 보안되지 않은 PDF 문서를 PDF 파일로 저장할 수 있습니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 문서에 정책 적용](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Java API를 사용하여 PDF 문서에서 정책 제거 {#remove-a-policy-from-a-pdf-document-using-the-java-api}

Document Security API(Java)를 사용하여 정책으로 보호된 PDF 문서에서 정책을 제거합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security 클라이언트 API 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `DocumentSecurityClient` 개체를 만듭니다.

1. 정책으로 보호된 PDF 문서를 검색합니다.

   * 생성자를 사용하고 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 정책으로 보호된 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. PDF 문서에서 정책을 제거합니다.

   * `DocumentSecurityClient` 개체의 `getDocumentManager` 메서드를 호출하여 `DocumentManager` 개체를 만듭니다.
   * `DocumentManager` 개체의 `removeSecurity` 메서드를 호출하고 정책으로 보호된 PDF 문서가 포함된 `com.adobe.idp.Document` 개체를 전달하여 PDF 문서에서 정책을 제거합니다. 이 메서드는 보안되지 않은 PDF 문서가 포함된 `com.adobe.idp.Document` 개체를 반환합니다.

1. 보안되지 않은 PDF 문서를 저장합니다.

   * `java.io.File` 개체를 만들고 파일 확장명이 PDF 상태인지 확인하십시오.
   * `Document` 개체의 `copyToFile` 메서드를 호출하여 `Document` 개체의 내용을 파일에 복사합니다(`removeSecurity` 메서드에서 반환된 `Document` 개체를 사용하는지 확인).

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서에서 정책 제거&quot;

### 웹 서비스 API를 사용하여 정책 제거 {#remove-a-policy-using-the-web-service-api}

Document Security API(웹 서비스)를 사용하여 정책으로 보호된 PDF 문서에서 정책 제거:

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. Document Security 클라이언트 API 개체를 만듭니다.

   * 기본 생성자를 사용하여 `DocumentSecurityServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `DocumentSecurityServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `DocumentSecurityServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.

   * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 정책으로 보호된 PDF 문서를 검색합니다.

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 정책이 제거된 정책으로 보호된 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 해당 `MTOM` 필드를 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.

1. PDF 문서에서 정책을 제거합니다.

   `DocumentSecurityServiceClient` 개체의 `removePolicySecurity` 메서드를 호출하고 정책으로 보호된 PDF 문서가 포함된 `BLOB` 개체를 전달하여 PDF 문서에서 정책을 제거합니다. 이 메서드는 보안되지 않은 PDF 문서가 포함된 `BLOB` 개체를 반환합니다.

1. 보안되지 않은 PDF 문서를 저장합니다.

   * 해당 생성자를 호출하고 보안되지 않은 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `removePolicySecurity` 메서드에서 반환된 `BLOB` 개체의 데이터 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 필드 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 PDF 문서에서 정책 제거&quot;
* &quot;빠른 시작(SwaRef): 웹 서비스 API를 사용하여 PDF 문서에서 정책 제거&quot;

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 문서에 대한 액세스 취소 {#revoking-access-to-documents}

정책으로 보호된 PDF 문서에 대한 액세스를 취소하면 사용자가 문서의 모든 사본에 액세스할 수 없게 됩니다. 사용자가 취소된 PDF 문서를 열려고 하면 수정된 문서를 볼 수 있는 지정된 URL로 리디렉션됩니다. 사용자가 리디렉션되는 의 URL은 프로그래밍 방식으로 지정해야 합니다. 문서에 대한 액세스를 취소하면 다음에 사용자가 정책으로 보호된 문서를 온라인으로 열어 Document Security 서비스와 동기화할 때 변경 사항이 적용됩니다.

문서에 대한 액세스를 취소하는 기능은 추가 보안을 제공합니다. 예를 들어, 새 버전의 문서를 사용할 수 있고 더 이상 오래된 버전을 볼 필요가 없다고 가정해 보겠습니다. 이 경우 이전 문서에 대한 액세스가 취소될 수 있으며, 액세스 권한이 복구되지 않으면 문서를 볼 수 없습니다.

>[!NOTE]
>
>Document Security 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-5}

정책으로 보호된 문서를 취소하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Document Security 클라이언트 API 개체를 만듭니다.
1. 정책으로 보호된 PDF 문서를 검색합니다.
1. 정책으로 보호된 문서를 취소합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security 클라이언트 API 개체 만들기**

Document Security 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만들어야 합니다.

**정책으로 보호된 PDF 문서 검색**

정책으로 보호된 PDF 문서를 검색하여 취소합니다. 이미 해지되었거나 정책으로 보호된 문서가 아닌 문서는 해지할 수 없습니다.

정책으로 보호된 문서의 라이선스 식별자 값을 알고 있는 경우 정책으로 보호된 PDF 문서를 검색할 필요는 없습니다. 그러나 대부분의 경우 라이센스 식별자 값을 얻으려면 PDF 문서를 검색해야 합니다.

**정책으로 보호된 문서 해지**

정책으로 보호된 문서를 취소하려면 정책으로 보호된 문서의 라이선스 식별자를 지정합니다. 또한 사용자가 취소된 문서를 열려고 할 때 볼 수 있는 문서의 URL을 지정할 수 있습니다. 즉, 오래된 문서가 취소되었다고 가정합니다. 사용자가 해지된 문서를 열려고 하면 해지된 문서 대신 업데이트된 문서가 표시됩니다.

>[!NOTE]
>
>이미 취소된 문서를 취소하려고 하면 예외가 발생합니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 문서에 정책 적용](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[해지된 문서에 대한 액세스 복원](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### Java API를 사용하여 문서에 대한 액세스 취소 {#revoke-access-to-documents-using-the-java-api}

Document Security API(Java)를 사용하여 정책으로 보호된 PDF 문서에 대한 액세스 취소:

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security 클라이언트 API 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `DocumentSecurityClient` 개체를 만듭니다.

1. 정책으로 보호된 PDF 문서 검색

   * 생성자를 사용하고 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 정책으로 보호된 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. 정책으로 보호된 문서 취소

   * `DocumentSecurityClient` 개체의 `getDocumentManager` 메서드를 호출하여 `DocumentManager` 개체를 만듭니다.
   * `DocumentManager` 개체의 `getLicenseId` 메서드를 호출하여 정책으로 보호된 문서의 라이선스 식별자 값을 검색합니다. 정책으로 보호된 문서를 나타내는 `com.adobe.idp.Document` 개체를 전달합니다. 이 메서드는 라이선스 식별자 값을 나타내는 문자열 값을 반환합니다.
   * `DocumentSecurityClient` 개체의 `getLicenseManager` 메서드를 호출하여 `LicenseManager` 개체를 만듭니다.
   * `LicenseManager` 개체의 `revokeLicense` 메서드를 호출하고 다음 값을 전달하여 정책으로 보호된 문서를 취소합니다.

      * 정책으로 보호된 문서의 라이선스 식별자 값을 지정하는 문자열 값입니다(`DocumentManager` 개체의 `getLicenseId` 메서드에 대한 반환 값 지정).
      * 문서를 취소하는 이유를 지정하는 `License` 인터페이스의 정적 데이터 멤버입니다. 예를 들어 `License.DOCUMENT_REVISED`을(를) 지정할 수 있습니다.
      * 수정된 문서가 있는 위치를 지정하는 `java.net.URL` 값입니다. 사용자를 다른 URL로 리디렉션하지 않으려면 `null`을(를) 전달할 수 있습니다.

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(SOAP 모드): Java API를 사용하여 문서 취소&quot;

### 웹 서비스 API를 사용하여 문서에 대한 액세스 취소 {#revoke-access-to-documents-using-the-web-service-api}

Document Security API(웹 서비스)를 사용하여 정책으로 보호된 PDF 문서에 대한 액세스 취소:

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. Document Security 클라이언트 API 개체 만들기

   * 기본 생성자를 사용하여 `DocumentSecurityServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `DocumentSecurityServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `DocumentSecurityServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.

   * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 정책으로 보호된 PDF 문서 검색

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 해지된 정책으로 보호된 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 취소할 정책으로 보호된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 해당 `MTOM` 필드를 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.

1. 정책으로 보호된 문서 취소

   * `DocumentSecurityServiceClient` 개체의 `getLicenseID` 메서드를 호출하고 정책으로 보호된 문서를 나타내는 `BLOB` 개체를 전달하여 정책으로 보호된 문서의 라이선스 식별자 값을 검색합니다. 이 메서드는 라이선스 식별자를 나타내는 문자열 값을 반환합니다.
   * `DocumentSecurityServiceClient` 개체의 `revokeLicense` 메서드를 호출하고 다음 값을 전달하여 정책으로 보호된 문서를 취소합니다.

      * 정책으로 보호된 문서의 라이선스 식별자 값을 지정하는 문자열 값입니다(`DocumentSecurityServiceService` 개체의 `getLicenseId` 메서드에 대한 반환 값 지정).
      * 문서를 취소하는 이유를 지정하는 `Reason` 열거형의 정적 데이터 멤버입니다. 예를 들어 `Reason.DOCUMENT_REVISED`을(를) 지정할 수 있습니다.
      * 수정된 문서가 있는 URL 위치를 지정하는 `string` 값입니다. 사용자를 다른 URL로 리디렉션하지 않으려면 `null`을(를) 전달할 수 있습니다.

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 문서 취소&quot;
* &quot;빠른 시작(SwaRef): 웹 서비스 API를 사용하여 문서 취소&quot;

**추가 참조**

[Word 문서에서 정책 제거](protecting-documents-policies.md#removing-policies-from-word-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 해지된 문서에 대한 액세스 복원 {#reinstating-access-to-revoked-documents}

해지된 PDF 문서에 대한 액세스 권한을 복원할 수 있으므로 해지된 문서의 모든 사본에 사용자가 액세스할 수 있습니다. 취소된 복원 문서를 열면 문서를 볼 수 있습니다.

>[!NOTE]
>
>Document Security 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-6}

해지된 PDF 문서에 대한 액세스를 복원하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Document Security 클라이언트 API 개체를 만듭니다.
1. 해지된 PDF 문서의 라이선스 식별자를 검색합니다.
1. 해지된 PDF 문서에 대한 액세스 권한을 복원합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security 클라이언트 API 개체 만들기**

Document Security 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `DocumentSecurityClient` 개체를 만듭니다. Document Security 웹 서비스 API를 사용하는 경우 `DocumentSecurityServiceService` 개체를 만듭니다.

**해지된 PDF 문서의 라이선스 식별자를 검색합니다**

취소된 PDF 문서의 라이선스 식별자를 검색하여 취소된 PDF 문서를 복원합니다. 라이센스 식별자 값을 얻은 후 해지된 문서를 복원할 수 있습니다. 취소되지 않은 문서를 복원하려고 하면 예외가 발생합니다.

**해지된 PDF 문서에 대한 액세스 권한을 복원합니다**

해지된 PDF 문서에 대한 액세스를 복원하려면 해지된 문서의 라이선스 식별자를 지정해야 합니다. 취소되지 않은 PDF 문서에 대한 액세스를 복원하려고 하면 예외가 발생합니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 문서에 정책 적용](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[문서에 대한 액세스 취소](protecting-documents-policies.md#revoking-access-to-documents)

### Java API를 사용하여 해지된 문서에 대한 액세스 복원 {#reinstate-access-to-revoked-documents-using-the-java-api}

Document Security API(Java)를 사용하여 취소된 문서에 대한 액세스 복원:

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security 클라이언트 API 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `DocumentSecurityClient` 개체를 만듭니다.

1. 해지된 PDF 문서의 라이선스 식별자를 검색합니다.

   * 생성자를 사용하고 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 해지된 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.
   * `DocumentSecurityClient` 개체의 `getDocumentManager` 메서드를 호출하여 `DocumentManager` 개체를 만듭니다.
   * `DocumentManager` 개체의 `getLicenseId` 메서드를 호출하고 해지된 문서를 나타내는 `com.adobe.idp.Document` 개체를 전달하여 해지된 문서의 라이선스 식별자 값을 검색합니다. 이 메서드는 라이선스 식별자를 나타내는 문자열 값을 반환합니다.

1. 해지된 PDF 문서에 대한 액세스 권한을 복원합니다.

   * `DocumentSecurityClient` 개체의 `getLicenseManager` 메서드를 호출하여 `LicenseManager` 개체를 만듭니다.
   * `LicenseManager` 개체의 `unrevokeLicense` 메서드를 호출하고 해지된 문서의 라이선스 식별자 값을 전달하여 해지된 PDF 문서에 대한 액세스를 복원하십시오.

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(SOAP 모드): 웹 서비스 API를 사용하여 해지된 문서에 대한 액세스 복원&quot;

### 웹 서비스 API를 사용하여 해지된 문서에 대한 액세스 복원 {#reinstate-access-to-revoked-documents-using-the-web-service-api}

Document Security API(웹 서비스)를 사용하여 취소된 문서에 대한 액세스 복원:

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. Document Security 클라이언트 API 개체를 만듭니다.

   * 기본 생성자를 사용하여 `DocumentSecurityServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `DocumentSecurityServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `DocumentSecurityServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.

   * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 해지된 PDF 문서의 라이선스 식별자를 검색합니다.

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 액세스가 복원되는 해지된 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 해지된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 해당 `MTOM` 필드를 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.

1. 해지된 PDF 문서에 대한 액세스 권한을 복원합니다.

   * `DocumentSecurityServiceClient` 개체의 `getLicenseID` 메서드를 호출하고 해지된 문서를 나타내는 `BLOB` 개체를 전달하여 해지된 문서의 라이선스 식별자 값을 검색합니다. 이 메서드는 라이선스 식별자를 나타내는 문자열 값을 반환합니다.
   * `DocumentSecurityServiceClient` 개체의 `unrevokeLicense` 메서드를 호출하고 해지된 PDF 문서의 라이선스 식별자 값을 지정하는 문자열 값을 전달하여 해지된 PDF 문서에 대한 액세스를 복원합니다(`DocumentSecurityServiceClient` 개체의 `getLicenseId` 메서드의 반환 값 전달).

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 해지된 문서에 대한 액세스 복원&quot;
* &quot;빠른 시작(SwaRef): 웹 서비스 API를 사용하여 해지된 문서에 대한 액세스 복원&quot;

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 정책으로 보호된 PDF 문서 검사 {#inspecting-policy-protected-pdf-documents}

Document Security Service API(Java 및 웹 서비스)를 사용하여 정책으로 보호된 PDF 문서를 검사할 수 있습니다. 정책으로 보호된 PDF 문서를 검사하면 정책으로 보호된 PDF 문서에 대한 정보가 반환됩니다. 예를 들어 문서를 보호하는 데 사용된 정책과 문서가 보안된 날짜를 결정할 수 있습니다.

LiveCycle 버전이 8.x 또는 이전 버전인 경우 이 작업을 수행할 수 없습니다. 정책으로 보호된 문서 검사를 위한 지원이 AEM Forms에 추가되었습니다. LiveCycle 8.x(또는 이전 버전)를 사용하여 정책으로 보호된 문서를 검사하려고 하면 예외가 발생합니다.

>[!NOTE]
>
>Document Security 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-7}

정책으로 보호된 PDF 문서를 검사하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Document Security 클라이언트 API 개체를 만듭니다.
1. 검사할 정책으로 보호된 문서를 검색합니다.
1. 정책으로 보호된 문서에 대한 정보를 얻습니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security 클라이언트 API 개체 만들기**

Document Security 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만듭니다. Java API를 사용하는 경우 `RightsManagementClient` 개체를 만듭니다. Document Security 웹 서비스 API를 사용하는 경우 `RightsManagementServiceService` 개체를 만듭니다.

**검사할 정책으로 보호된 문서 검색**

정책으로 보호된 문서를 검사하려면 해당 문서를 검색합니다. 정책으로 보호되지 않거나 취소된 문서를 검사하려고 하면 예외가 발생합니다.

**문서 Inspect**

정책으로 보호된 문서를 검색한 후 검사할 수 있습니다.

**정책으로 보호된 문서에 대한 정보 가져오기**

정책으로 보호된 PDF 문서를 검사하면 해당 문서에 대한 정보를 얻을 수 있습니다. 예를 들어 문서 보안에 사용되는 정책을 결정할 수 있습니다.

내 정책에 속하는 정책으로 문서를 보호한 다음 `RMInspectResult.getPolicysetName` 또는 `RMInspectResult.getPolicysetId`을(를) 호출하면 null이 반환됩니다.

내 정책 이외의 정책 집합에 포함된 정책을 사용하여 문서를 보호하면 `RMInspectResult.getPolicysetName` 및 `RMInspectResult.getPolicysetId`이(가) 올바른 문자열을 반환합니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 Inspect 정책으로 보호된 PDF 문서 {#inspect-policy-protected-pdf-documents-using-the-java-api}

Inspect은 Document Security Service API(Java)를 사용하여 정책으로 보호된 PDF 문서입니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar과 같은 클라이언트 JAR 파일을 포함합니다. 이러한 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

1. Document Security 클라이언트 API 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다. ([연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하세요.)
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `RightsManagementClient` 개체를 만듭니다.

1. 검사할 정책으로 보호된 문서를 검색합니다.

   * 생성자를 사용하여 정책으로 보호된 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다. PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하고 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. 문서를 Inspect 합니다.

   * `RightsManagementClient` 개체의 `getDocumentManager` 메서드를 호출하여 `DocumentManager` 개체를 만듭니다.
   * `LicenseManager` 개체의 `inspectDocument` 메서드를 호출하여 정책으로 보호된 문서를 Inspect합니다. 정책으로 보호된 PDF 문서가 포함된 `com.adobe.idp.Document` 개체를 전달합니다. 이 메서드는 정책으로 보호된 문서에 대한 정보가 포함된 `RMInspectResult` 개체를 반환합니다.

1. 정책으로 보호된 문서에 대한 정보를 얻습니다.

   정책으로 보호된 문서에 대한 정보를 얻으려면 `RMInspectResult` 개체에 속하는 적절한 메서드를 호출하십시오. 예를 들어 정책 이름을 검색하려면 `RMInspectResult` 개체의 `getPolicyName` 메서드를 호출하십시오.

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(SOAP 모드): Java API를 사용하여 정책으로 보호된 PDF 문서 검사&quot;

### 웹 서비스 API를 사용하여 Inspect 정책으로 보호된 PDF 문서 {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Inspect은 Document Security Service API(웹 서비스)를 사용하여 정책으로 보호된 PDF 문서입니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. Document Security 클라이언트 API 개체를 만듭니다.

   * 기본 생성자를 사용하여 `RightsManagementServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `RightsManagementServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `RightsManagementServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `RightsManagementServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `RightsManagementServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.

   * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 검사할 정책으로 보호된 문서를 검색합니다.

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 검사할 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 해당 `MTOM` 필드를 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.

1. 문서를 Inspect 합니다.

   `RightsManagementServiceClient` 개체의 `inspectDocument` 메서드를 호출하여 정책으로 보호된 문서를 Inspect합니다. 정책으로 보호된 PDF 문서가 포함된 `BLOB` 개체를 전달합니다. 이 메서드는 정책으로 보호된 문서에 대한 정보가 포함된 `RMInspectResult` 개체를 반환합니다.

1. 정책으로 보호된 문서에 대한 정보를 얻습니다.

   정책으로 보호된 문서에 대한 정보를 얻으려면 `RMInspectResult` 개체에 속하는 적절한 필드의 값을 가져옵니다. 예를 들어 정책 이름을 검색하려면 `RMInspectResult` 개체의 `policyName` 필드 값을 가져옵니다.

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 정책으로 보호된 PDF 문서 검사&quot;
* &quot;빠른 시작(SwaRef): 웹 서비스 API를 사용하여 정책으로 보호된 PDF 문서 검사&quot;

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 워터마크 만들기 {#creating-watermarks}

워터마크는 문서를 고유하게 식별하고 저작권 침해를 제어함으로써 문서의 보안을 보장하는 데 도움이 됩니다. 예를 들어 문서의 모든 페이지에 기밀을 나타내는 워터마크를 만들어 배치할 수 있습니다. 워터마크가 생성되면 정책의 일부로 워터마크를 포함할 수 있습니다. 즉, 새로 생성된 워터마크로 정책의 워터마크 속성을 설정할 수 있습니다. 워터마크가 포함된 정책이 문서에 적용되면 워터마크가 정책으로 보호된 문서에 표시됩니다.

>[!NOTE]
>
>Document Security 관리 권한이 있는 사용자만 워터마크를 만들 수 있습니다. 즉, Document Security 서비스 클라이언트 개체를 만드는 데 필요한 연결 설정을 정의할 때 이러한 사용자를 지정해야 합니다.

>[!NOTE]
>
>Document Security 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-8}

워터마크를 만들려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Document Security 클라이언트 API 개체를 만듭니다.
1. 워터마크 속성을 설정합니다.
1. Document Security 서비스에 워터마크를 등록합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security 클라이언트 API 개체 만들기**

Document Security 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `RightsManagementClient` 개체를 만듭니다. Document Security 웹 서비스 API를 사용하는 경우 `RightsManagementServiceService` 개체를 만듭니다.

**워터마크 특성을 설정합니다**

워터마크를 만들려면 워터마크 속성을 설정해야 합니다. name 특성을 항상 정의해야 합니다. name 속성 외에 다음 속성 중 하나 이상을 설정해야 합니다.

* 사용자 지정 텍스트
* 포함된 날짜
* 사용자 ID 포함됨
* 사용자 이름 포함됨

다음 표에는 웹 서비스를 사용하여 워터마크를 만들 때 필요한 키 및 값 쌍이 나와 있습니다.

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
   <td><p>문서를 여는 사용자의 ID가 워터마크의 일부인지 지정합니다.</p></td>
   <td><p>True 또는 False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>현재 날짜가 워터마크의 일부인지 여부를 지정합니다.</p></td>
   <td><p>True 또는 False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>이 값이 true이면 <code>WaterBackCmd:SRCTEXT</code>을(를) 사용하여 사용자 지정 텍스트의 값을 지정해야 합니다.</p></td>
   <td><p>True 또는 False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>워터마크의 불투명도를 지정합니다. 지정하지 않은 경우 기본값은 0.5입니다.</p></td>
   <td><p>0.0과 1.0 사이의 값입니다.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>워터마크의 회전을 지정합니다. 기본값은 0도입니다.</p></td>
   <td><p>0~359 사이의 값입니다.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>이 값을 지정하면 <code>WaterBackCmd:IS_SIZE_ENABLED</code>이(가) 있어야 하며 값이 true여야 합니다. 이 속성을 지정하지 않으면 기본 동작이 페이지에 맞춰집니다.</p></td>
   <td><p>0.0보다 크고 1.0보다 작거나 같은 값입니다.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>워터마크의 수평 정렬을 지정합니다. 기본값은 가운데(center)입니다.</p></td>
   <td><p>left, center 또는 right</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>워터마크의 세로 정렬을 지정합니다. 기본값은 가운데(center)입니다.</p></td>
   <td><p>위쪽, 가운데 또는 아래쪽</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>워터마크가 배경인지 여부를 지정합니다. 기본값은 false입니다.</p></td>
   <td><p>True 또는 False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>사용자 지정 배율이 지정된 경우 True입니다. 이 값이 true이면 SCALE도 지정해야 합니다. 이 값이 false이면 기본값이 페이지에 맞춰집니다.</p></td>
   <td><p>True 또는 False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>워터마크에 대한 사용자 지정 텍스트를 지정합니다. 이 값이 있으면 <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code>도 있어야 하며 true로 설정해야 합니다.</p></td>
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

새 워터마크를 사용하려면 먼저 Document Security 서비스에 등록해야 합니다. 워터마크를 등록한 후 정책 내에서 사용할 수 있습니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 문서에 정책 적용](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Java API를 사용하여 워터마크 만들기 {#create-watermarks-using-the-java-api}

Java(Document Security API)를 사용하여 워터마크를 만듭니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 `adobe-rightsmanagement-client.jar`과(와) 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security 클라이언트 API 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `RightsManagementClient` 개체를 만듭니다.

1. 워터마크 속성 설정

   * `InfomodelObjectFactory` 개체의 정적 `createWatermark` 메서드를 호출하여 `Watermark` 개체를 만듭니다. 이 메서드는 `Watermark` 개체를 반환합니다.
   * `Watermark` 개체의 `setName` 메서드를 호출하고 정책 이름을 지정하는 문자열 값을 전달하여 워터마크의 이름 특성을 설정합니다.
   * `Watermark` 개체의 `setBackground` 메서드를 호출하고 `true`을(를) 전달하여 워터마크의 백그라운드 특성을 설정합니다. 이 속성을 설정하면 문서 배경에 워터마크가 표시됩니다.
   * `Watermark` 개체의 `setCustomText` 메서드를 호출하고 워터마크의 텍스트를 나타내는 문자열 값을 전달하여 워터마크의 사용자 지정 텍스트 특성을 설정합니다.
   * `Watermark` 개체의 `setOpacity` 메서드를 호출하고 불투명도 수준을 지정하는 정수 값을 전달하여 워터마크의 불투명도 특성을 설정합니다. 값이 100이면 워터마크가 완전히 불투명함을 나타내고 값이 0이면 워터마크가 완전히 투명함을 나타냅니다.

1. 워터마크를 등록합니다.

   * `RightsManagementClient` 개체의 `getWatermarkManager` 메서드를 호출하여 `WatermarkManager` 개체를 만듭니다. 이 메서드는 `WatermarkManager` 개체를 반환합니다.
   * `WatermarkManager` 개체의 `registerWatermark` 메서드를 호출하고 워터마크를 나타내는 `Watermark` 개체를 등록하도록 전달하여 워터마크를 등록합니다. 이 메서드는 워터마크의 식별 값을 나타내는 문자열 값을 반환합니다.

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(SOAP 모드): Java API를 사용하여 워터마크 만들기&quot;

### 웹 서비스 API를 사용하여 워터마크 만들기 {#create-watermarks-using-the-web-service-api}

Document Security API(웹 서비스)를 사용하여 워터마크를 만듭니다.

1. Document Security 클라이언트 API 개체를 만듭니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. Document Security 클라이언트 API 개체를 만듭니다.

   * 기본 생성자를 사용하여 `RightsManagementServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `RightsManagementServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `RightsManagementServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `RightsManagementServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `RightsManagementServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.

   * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 워터마크 속성을 설정합니다.

   * `WatermarkSpec` 생성자를 호출하여 `WatermarkSpec` 개체를 만듭니다.
   * `WatermarkSpec` 개체의 `name` 데이터 멤버에 문자열 값을 할당하여 워터마크의 이름을 설정합니다.
   * 문자열 값을 `WatermarkSpec` 개체의 `id` 데이터 멤버에 할당하여 워터마크의 `id` 특성을 설정합니다.
   * 설정할 각 워터마크 속성에 대해 별도의 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 만듭니다.
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `key` 데이터 멤버(예: `WaterBackCmd:OPACITY)`)에 값을 할당하여 키 값을 설정하십시오.
   * 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `value` 데이터 멤버(예: `.25`)에 할당하여 값을 설정하십시오.
   * `MyArrayOf_xsd_anyType` 개체를 만듭니다. 각 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체에 대해 `MyArrayOf_xsd_anyType` 개체의 `Add` 메서드를 호출합니다. `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 전달합니다.
   * `MyArrayOf_xsd_anyType` 개체를 `WatermarkSpec` 개체의 `values` 데이터 멤버에 할당합니다.

1. 워터마크를 등록합니다.

   `RightsManagementServiceClient` 개체의 `registerWatermark` 메서드를 호출하고 워터마크를 나타내는 `WatermarkSpec` 개체를 등록하도록 전달하여 워터마크를 등록합니다.

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 워터마크 만들기&quot;
* &quot;빠른 시작(SwaRef): 웹 서비스 API를 사용하여 워터마크 만들기&quot;

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 워터마크 수정 {#modifying-watermarks}

Document Security Java API 또는 웹 서비스 API를 사용하여 기존 워터마크를 수정할 수 있습니다. 기존 워터마크를 변경하려면 워터마크를 검색하고 속성을 수정한 다음 서버에서 업데이트합니다. 예를 들어 워터마크를 검색하고 불투명도 속성을 수정한다고 가정해 보겠습니다. 변경 사항이 적용되기 전에 워터마크를 업데이트해야 합니다.

워터마크를 수정하면 워터마크가 적용된 이후 문서에 변경 사항이 적용됩니다. 즉, 워터마크가 포함된 기존 PDF 문서는 영향을 받지 않습니다.

>[!NOTE]
>
>Document Security 관리 권한이 있는 사용자만 워터마크를 수정할 수 있습니다. 즉, Document Security 서비스 클라이언트 개체를 만드는 데 필요한 연결 설정을 정의할 때 이러한 사용자를 지정해야 합니다.

>[!NOTE]
>
>Document Security 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-9}

워터마크를 수정하려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. Document Security 클라이언트 API 개체를 만듭니다.
1. 수정할 워터마크를 검색합니다.
1. 워터마크 속성을 설정합니다.
1. 워터마크를 업데이트합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security 클라이언트 API 개체 만들기**

Document Security 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `DocumentSecurityClient` 개체를 만듭니다. Document Security 웹 서비스 API를 사용하는 경우 `DocumentSecurityServiceService` 개체를 만듭니다.

**수정할 워터마크를 검색합니다**

워터마크를 수정하려면 기존 워터마크를 검색해야 합니다. 워터마크의 이름을 지정하거나 해당 식별자 값을 지정하여 워터마크를 검색할 수 있습니다.

**워터마크 특성을 설정합니다**

기존 워터마크를 수정하려면 하나 이상의 워터마크 속성 값을 변경합니다. 웹 서비스를 사용하여 프로그래밍 방식으로 워터마크를 업데이트할 때에는 값이 변경되지 않더라도 원래 설정된 모든 속성을 설정해야 합니다. 예를 들어 워터마크 특성 `WaterBackCmd:IS_USERID_ENABLED`, `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`, `WaterBackCmd:OPACITY` 및 `WaterBackCmd:SRCTEXT`이(가) 설정되어 있다고 가정합니다. 수정할 특성은 `WaterBackCmd:OPACITY`뿐이지만 다른 값도 올바르게 설정해야 합니다.

>[!NOTE]
>
>Java API를 사용하여 워터마크를 수정하는 경우, 모든 속성을 지정할 필요가 없습니다. 수정할 워터마크 속성을 설정합니다.

>[!NOTE]
>
>워터마크 특성 이름에 대한 자세한 내용은 [워터마크 만들기](protecting-documents-policies.md#creating-watermarks)를 참조하십시오.

**워터마크 업데이트**

워터마크의 속성을 수정한 후에는 워터마크를 업데이트해야 합니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[워터마크 만들기](protecting-documents-policies.md#creating-watermarks)

### Java API를 사용하여 워터마크 수정 {#modify-watermarks-using-the-java-api}

Java(Document Security API)를 사용하여 워터마크를 수정합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security 클라이언트 API 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `DocumentSecurityClient` 개체를 만듭니다.

1. 수정할 워터마크를 검색합니다.

   `DocumentSecurityClient` 개체의 `getWatermarkManager` 메서드를 호출하여 `WatermarkManager` 개체를 만들고 워터마크 이름을 지정하는 문자열 값을 전달하십시오. 이 메서드는 수정할 워터마크를 나타내는 `Watermark` 개체를 반환합니다.

1. 워터마크 속성을 설정합니다.

   `Watermark` 개체의 `setOpacity` 메서드를 호출하고 불투명도 수준을 지정하는 정수 값을 전달하여 워터마크의 불투명도 특성을 설정합니다. 값이 100이면 워터마크가 완전히 불투명함을 나타내고 값이 0이면 워터마크가 완전히 투명함을 나타냅니다.

   >[!NOTE]
   >
   >이 예제에서는 opacity 속성만 수정합니다.

1. 워터마크를 업데이트합니다.

   * `WatermarkManager` 개체의 `updateWatermark` 메서드를 호출하여 워터마크를 업데이트하고 특성이 수정된 `Watermark` 개체를 전달합니다.

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 빠른 시작(SOAP 모드): Java API를 사용하여 워터마크 수정 섹션을 참조하십시오.

### 웹 서비스 API를 사용하여 워터마크 수정 {#modify-watermarks-using-the-web-service-api}

Document Security API(웹 서비스)를 사용하여 워터마크를 수정합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. Document Security 클라이언트 API 개체를 만듭니다.

   * 기본 생성자를 사용하여 `DocumentSecurityServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `RightsManagementServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `DocumentSecurityServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.

   * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 수정할 워터마크를 검색합니다.

   `DocumentSecurityServiceClient` 개체의 `getWatermarkByName` 메서드를 호출하여 수정할 워터마크를 검색합니다. 워터마크 이름을 지정하는 문자열 값을 전달합니다. 이 메서드는 수정할 워터마크를 나타내는 `WatermarkSpec` 개체를 반환합니다.

1. 워터마크 속성을 설정합니다.

   * 업데이트할 각 워터마크 속성에 대해 별도의 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 만드십시오.
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `key` 데이터 멤버(예: `WaterBackCmd:OPACITY)`)에 값을 할당하여 키 값을 설정하십시오.
   * 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `value` 데이터 멤버(예: `.50`)에 할당하여 값을 설정하십시오.
   * `MyArrayOf_xsd_anyType` 개체를 만듭니다. 각 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체에 대해 `MyArrayOf_xsd_anyType` 개체의 `Add` 메서드를 호출합니다. `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 전달합니다.
   * `MyArrayOf_xsd_anyType` 개체를 `WatermarkSpec` 개체의 `values` 데이터 멤버에 할당합니다.

1. 워터마크를 업데이트합니다.

   `DocumentSecurityServiceClient` 개체의 `updateWatermark` 메서드를 호출하고 수정할 워터마크를 나타내는 `WatermarkSpec` 개체를 전달하여 워터마크를 업데이트합니다.

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 워터마크 수정&quot;

## 이벤트 검색 {#searching-for-events}

Rights Management 서비스는 문서에 정책 적용, 정책으로 보호된 문서 열기, 문서에 대한 액세스 취소 등 특정 작업이 발생하면 추적합니다. Rights Management 서비스에 대해 이벤트 감사를 사용하도록 설정해야 합니다. 그렇지 않으면 이벤트가 추적되지 않습니다.

이벤트는 다음 카테고리 중 하나에 속합니다.

* 관리자 이벤트는 관리자 계정 생성과 같이 관리자 관련 작업입니다.
* 문서 이벤트는 정책으로 보호된 문서를 닫는 것과 같이 문서와 관련된 작업입니다.
* 정책 이벤트는 정책 생성과 같이 정책과 관련된 작업입니다.
* 서비스 이벤트는 사용자 디렉터리와의 동기화와 같이 Rights Management 서비스와 관련된 작업입니다.

Rights Management Java API 또는 웹 서비스 API를 사용하여 특정 이벤트를 검색할 수 있습니다. 이벤트를 검색하여 특정 이벤트의 로그 파일 생성과 같은 작업을 수행할 수 있습니다.

>[!NOTE]
>
>Rights Management 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-10}

Rights Management 이벤트를 검색하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Rights Management 클라이언트 API 개체를 만듭니다.
1. 검색할 이벤트를 지정합니다.
1. 이벤트를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Rights Management 클라이언트 API 개체 만들기**

Rights Management 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Rights Management 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `DocumentSecurityClient` 개체를 만듭니다. Rights Management 웹 서비스 API를 사용하는 경우 `DocumentSecurityServiceService` 개체를 만듭니다.

**검색할 이벤트 지정**

검색할 이벤트를 지정합니다. 예를 들어 새 정책이 만들어질 때 발생하는 정책 만들기 이벤트를 검색할 수 있습니다.

**이벤트 검색**

검색할 이벤트를 지정한 후에는 Rights Management Java API 또는 Rights Management 웹 서비스 API를 사용하여 이벤트를 검색할 수 있습니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 이벤트 검색 {#search-for-events-using-the-java-api}

Rights Management API(Java)를 사용하여 이벤트를 검색합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. Rights Management 클라이언트 API 개체 만들기

   해당 생성자를 사용하고 연결 속성이 포함된 `ServiceClientFactory` 개체를 전달하여 `DocumentSecurityClient` 개체를 만듭니다.

1. 검색할 이벤트 지정

   * `DocumentSecurityClient` 개체의 `getEventManager` 메서드를 호출하여 `EventManager` 개체를 만듭니다. 이 메서드는 `EventManager` 개체를 반환합니다.
   * 해당 생성자를 호출하여 `EventSearchFilter` 개체를 만듭니다.
   * `EventSearchFilter` 개체의 `setEventCode` 메서드를 호출하고 검색할 이벤트를 나타내는 `EventManager` 클래스에 속하는 정적 데이터 멤버를 전달하여 검색할 이벤트를 지정합니다. 예를 들어 정책 만들기 이벤트를 검색하려면 `EventManager.POLICY_CREATE_EVENT`을(를) 전달합니다.

   >[!NOTE]
   >
   >`EventSearchFilter` 개체 메서드를 호출하여 추가 검색 조건을 정의할 수 있습니다. 예를 들어 `setUserName` 메서드를 호출하여 이벤트와 연결된 사용자를 지정합니다.

1. 이벤트 검색

   `EventManager` 개체의 `searchForEvents` 메서드를 호출하고 이벤트 검색 조건을 정의하는 `EventSearchFilter` 개체를 전달하여 이벤트를 검색합니다. 이 메서드는 `Event` 개체의 배열을 반환합니다.

**코드 예제**

Rights Management 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(SOAP): Java API를 사용하여 이벤트 검색&quot;

### 웹 서비스 API를 사용하여 이벤트 검색 {#search-for-events-using-the-web-service-api}

Rights Management API(웹 서비스)를 사용하여 이벤트를 검색합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. Rights Management 클라이언트 API 개체 만들기

   * 기본 생성자를 사용하여 `DocumentSecurityServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `DocumentSecurityServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `DocumentSecurityServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.

   * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 검색할 이벤트 지정

   * 해당 생성자를 사용하여 `EventSpec` 개체를 만듭니다.
   * 이벤트가 발생한 날짜 범위의 시작을 나타내는 `DataTime` 인스턴스로 `EventSpec` 개체의 `firstTime.date` 데이터 멤버를 설정하여 이벤트가 발생한 기간의 시작을 지정하십시오.
   * `EventSpec` 개체의 `firstTime.dateSpecified` 데이터 멤버에 값 `true`을(를) 할당합니다.
   * 이벤트가 발생한 날짜 범위의 끝을 나타내는 `DataTime` 인스턴스로 `EventSpec` 개체의 `lastTime.date` 데이터 멤버를 설정하여 이벤트가 발생한 기간의 끝을 지정하십시오.
   * `EventSpec` 개체의 `lastTime.dateSpecified` 데이터 멤버에 값 `true`을(를) 할당합니다.
   * `EventSpec` 개체의 `eventCode` 데이터 멤버에 문자열 값을 할당하여 검색할 이벤트를 설정하십시오. 다음 표에는 이 속성에 지정할 수 있는 숫자 값이 나열되어 있습니다.

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
    <td><p>999</p></td>
    </tr>
    <tr>
    <td><p><code>USER_CHANGE_PASSWORD_EVENT</code></p></td>
    <td><p>1000년</p></td>
    </tr>
    <tr>
    <td><p><code>USER_REGISTER_EVENT</code></p></td>
    <td><p>1001</p></td>
    </tr>
    <tr>
    <td><p><code>USER_PREREGISTER_EVENT</code></p></td>
    <td><p>1002</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACTIVATE_EVENT</code></p></td>
    <td><p>1003</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DEACTIVATE_EVENT</code></p></td>
    <td><p>1004</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_EVENT</code></p></td>
    <td><p>1005</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_DENY_EVENT </code></p></td>
    <td><p>1006</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACCOUNT_LOCK_EVENT</code></p></td>
    <td><p>1007</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DELETE_EVENT </code></p></td>
    <td><p>1008</p></td>
    </tr>
    <tr>
    <td><p><code>USER_UPDATE_PROFILE_EVENT </code></p></td>
    <td><p>1009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_VIEW_EVENT </code></p></td>
    <td><p>2000</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_LOW_EVENT </code></p></td>
    <td><p>2001</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_HIGH_EVENT </code></p></td>
    <td><p>2002</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SIGN_EVENT </code></p></td>
    <td><p>2003</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_ADD_ANNOTATION_EVENT </code></p></td>
    <td><p>2004</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_FORM_FILL_EVENT </code></p></td>
    <td><p>2005</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CLOSE_EVENT </code></p></td>
    <td><p>2006</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_MODIFY_EVENT </code></p></td>
    <td><p>2007</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_SECURITY_HANDLER_EVENT </code></p></td>
    <td><p>2008</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SWITCH_POLICY_EVENT </code></p></td>
    <td><p>2009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_REVOKE_EVENT </code></p></td>
    <td><p>2010</p></td>
    </tr>
    <tr>
    <td><p><code>$1</code></p></td>
    <td><p>2011</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SECURE_EVENT </code></p></td>
    <td><p>2012</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_UNKNOWN_CLIENT_EVENT </code></p></td>
    <td><p>2013</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_REVOKE_URL_EVENT </code></p></td>
    <td><p>2014</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_EVENT </code></p></td>
    <td><p>3000</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_ENABLE_EVENT </code></p></td>
    <td><p>3001</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DISABLE_EVENT </code></p></td>
    <td><p>3002</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CREATE_EVENT </code></p></td>
    <td><p>3003</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DELETE_EVENT </code></p></td>
    <td><p>3004</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_OWNER_EVENT </code></p></td>
    <td><p>3005</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CLIENT_SYNC_EVENT </code></p></td>
    <td><p>4000</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_INFO_EVENT </code></p></td>
    <td><p>4001</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_COMPLETE_EVENT </code></p></td>
    <td><p>4002</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_VERSION_MISMATCH_EVENT </code></p></td>
    <td><p>4003</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CONFIG_CHANGE_EVENT </code></p></td>
    <td><p>4004</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_ENABLE_OFFLINE_ACCESS_EVENT </code></p></td>
    <td><p>4005</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ADD_EVENT </code></p></td>
    <td><p>5000</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DELETE_EVENT </code></p></td>
    <td><p>5001</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_EDIT_EVENT </code></p></td>
    <td><p>5002</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ACTIVATE_EVENT </code></p></td>
    <td><p>5003</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DEACTIVATE_EVENT </code></p></td>
    <td><p>5004</p></td>
    </tr>
    <tr>
    <td><p><code>ERROR_DIRECTORY_SERVICE_EVENT </code></p></td>
    <td><p>6000</p></td>
    </tr>
    <tr>
    <td><p><code>CREATED_POLICYSET_EVENT</code></p></td>
    <td><p>7000</p></td>
    </tr>
    <tr>
    <td><p><code>DELETED_POLICYSET_EVENT</code></p></td>
    <td><p>7001</p></td>
    </tr>
    <tr>
    <td><p><code>MODIFIED_POLICYSET_EVENT</code></p></td>
    <td><p>7002</p></td>
    </tr>
    </tbody>
    </table>

1. 이벤트 검색

   `DocumentSecurityServiceClient` 개체의 `searchForEvents` 메서드를 호출하고 검색할 이벤트와 최대 결과 수를 나타내는 `EventSpec` 개체를 전달하여 이벤트를 검색합니다. 이 메서드는 각 요소가 `AuditSpec` 인스턴스인 `MyArrayOf_xsd_anyType` 컬렉션을 반환합니다. `AuditSpec` 인스턴스를 사용하면 이벤트가 발생한 시간과 같은 이벤트에 대한 정보를 얻을 수 있습니다. `AuditSpec` 인스턴스에 이 정보를 지정하는 `timestamp` 데이터 멤버가 있습니다.

**코드 예제**

Rights Management 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 이벤트 검색&quot;
* &quot;빠른 시작(SwaRef): 웹 서비스 API를 사용하여 이벤트 검색&quot;

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Word 문서에 정책 적용 {#applying-policies-to-word-documents}

Rights Management 서비스는 PDF 문서 외에도 Microsoft Word 문서(DOC 파일) 및 기타 Microsoft Office 파일 형식과 같은 추가 문서 형식을 지원합니다. 예를 들어 Word 문서에 정책을 적용하여 보안을 설정할 수 있습니다. Word 문서에 정책을 적용하면 문서에 대한 액세스를 제한할 수 있습니다. 정책으로 문서가 이미 보호되어 있는 경우에는 문서에 정책을 적용할 수 없습니다.

배포한 후 정책으로 보호된 Word 문서의 사용을 모니터링할 수 있습니다. 즉, 문서가 어떻게 사용되고 있으며 누가 사용하고 있는지 확인할 수 있습니다. 예를 들어, 누군가가 문서를 언제 열었는지 확인할 수 있습니다.

>[!NOTE]
>
>Document Security 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-11}

Word 문서에 정책을 적용하려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. Document Security 클라이언트 API 개체를 만듭니다.
1. 정책이 적용되는 Word 문서를 검색합니다.
1. Word 문서에 기존 정책을 적용합니다.
1. 정책으로 보호된 Word 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security Client APIobject 만들기**

Document Security 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만들어야 합니다.

**Word 문서 검색**

정책을 적용할 Word 문서를 검색합니다. Word 문서에 정책을 적용하면 문서를 사용할 때 사용자가 제한됩니다. 예를 들어 오프라인일 때 정책에서 문서를 열 수 있도록 설정하지 않은 경우 사용자가 문서를 열려면 온라인 상태여야 합니다.

**Word 문서에 기존 정책 적용**

Word 문서에 정책을 적용하려면 기존 정책을 참조하고 해당 정책이 속한 정책 집합을 지정해야 합니다. 연결 속성을 설정하는 사용자는 지정된 정책에 액세스할 수 있어야 합니다. 그렇지 않은 경우 예외가 발생합니다.

**Word 문서 저장**

Document Security 서비스가 Word 문서에 정책을 적용한 후 정책으로 보호된 Word 문서를 DOC 파일로 저장할 수 있습니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[문서에 대한 액세스 취소](protecting-documents-policies.md#revoking-access-to-documents)

### Java API를 사용하여 Word 문서에 정책 적용 {#apply-a-policy-to-a-word-document-using-the-java-api}

Document Security API(Java)를 사용하여 Word 문서에 정책 적용:

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security 클라이언트 API 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `DocumentSecurityClient` 개체를 만듭니다.

1. Word 문서를 검색합니다.

   * 생성자를 사용하고 Word 문서의 위치를 지정하는 문자열 값을 전달하여 Word 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. Word 문서에 기존 정책을 적용합니다.

   * `DocumentSecurityClient` 개체의 `getDocumentManager` 메서드를 호출하여 `DocumentManager` 개체를 만듭니다.
   * `DocumentManager` 개체의 `protectDocument` 메서드를 호출하고 다음 값을 전달하여 Word 문서에 정책을 적용합니다.

      * 정책이 적용되는 Word 문서가 포함된 `com.adobe.idp.Document` 개체입니다.
      * 문서의 이름을 지정하는 문자열 값입니다.
      * 정책이 속한 정책 집합의 이름을 지정하는 문자열 값입니다. `MyPolicies` 정책 집합이 사용되는 `null` 값을 지정할 수 있습니다.
      * 정책 이름을 지정하는 문자열 값입니다.
      * 문서의 게시자인 사용자의 사용자 관리자 도메인 이름을 나타내는 문자열 값입니다. 이 매개변수 값은 선택 사항이며 null일 수 있습니다(이 매개변수가 null이면 다음 매개변수 값은 null이어야 함).
      * 문서의 게시자인 사용자 관리자 사용자의 정식 이름을 나타내는 문자열 값입니다. 이 매개 변수 값은 선택 사항이며 `null`일 수 있습니다(이 매개 변수가 `null`이면 이전 매개 변수 값은 `null`이어야 함).
      * MS Office 템플릿을 선택하는 데 사용되는 로케일을 나타내는 `com.adobe.livecycle.rightsmanagement.Locale`입니다. 이 매개 변수 값은 선택 사항이며 `null`을(를) 지정할 수 있습니다.

     `protectDocument` 메서드가 정책으로 보호된 Word 문서를 포함하는 `RMSecureDocumentResult` 개체를 반환합니다.

1. Word 문서를 저장합니다.

   * `RMSecureDocumentResult` 개체의 `getProtectedDoc` 메서드를 호출하여 정책으로 보호된 Word 문서를 가져옵니다. 이 메서드는 `com.adobe.idp.Document` 개체를 반환합니다.
   * `java.io.File` 개체를 만들고 파일 확장명이 DOC인지 확인합니다.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 `Document` 개체의 내용을 파일에 복사합니다(`getProtectedDoc` 메서드에서 반환된 `Document` 개체를 사용하는지 확인).

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(SOAP 모드): Java API를 사용하여 Word 문서에 정책 적용&quot;

### 웹 서비스 API를 사용하여 Word 문서에 정책 적용 {#apply-a-policy-to-a-word-document-using-the-web-service-api}

Document Security API(웹 서비스)를 사용하여 Word 문서에 정책 적용:

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. Document Security 클라이언트 API 개체를 만듭니다.

   * 기본 생성자를 사용하여 `DocumentSecurityServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `DocumentSecurityServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `DocumentSecurityServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.

   * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. Word 문서를 검색합니다.

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 정책이 적용되는 Word 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 Word 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열 크기를 결정합니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 해당 `MTOM` 필드를 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.

1. Word 문서에 기존 정책을 적용합니다.

   `DocumentSecurityServiceClient` 개체의 `protectDocument` 메서드를 호출하고 다음 값을 전달하여 Word 문서에 정책을 적용합니다.

   * 정책이 적용되는 Word 문서가 포함된 `BLOB` 개체입니다.
   * 문서의 이름을 지정하는 문자열 값입니다.
   * 정책이 속한 정책 집합의 이름을 지정하는 문자열 값입니다. `MyPolicies` 정책 집합이 사용되는 `null` 값을 지정할 수 있습니다.
   * 정책 이름을 지정하는 문자열 값입니다.
   * 문서의 게시자인 사용자의 사용자 관리자 도메인 이름을 나타내는 문자열 값입니다. 이 매개 변수 값은 선택 사항이며 null일 수 있습니다(이 매개 변수가 null이면 다음 매개 변수 값은 `null`이어야 함).
   * 문서의 게시자인 사용자 관리자 사용자의 정식 이름을 나타내는 문자열 값입니다. 이 매개 변수 값은 선택 사항이며 null일 수 있습니다(이 매개 변수가 null이면 이전 매개 변수 값은 `null`이어야 함).
   * 로케일 값을 지정하는 `RMLocale` 값(예: `RMLocale.en`)입니다.
   * 정책 식별자 값을 저장하는 데 사용되는 문자열 출력 매개 변수입니다.
   * 정책으로 보호된 식별자 값을 저장하는 데 사용되는 문자열 출력 매개 변수입니다.
   * MIME 형식을 저장하는 데 사용되는 문자열 출력 매개 변수(예: `application/doc`)입니다.

   `protectDocument` 메서드가 정책으로 보호된 Word 문서를 포함하는 `BLOB` 개체를 반환합니다.

1. Word 문서를 저장합니다.

   * 해당 생성자를 호출하고 정책으로 보호된 Word 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `protectDocument` 메서드에서 반환된 `BLOB` 개체의 데이터 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 Word 파일에 씁니다.

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 Word 문서에 정책 적용 &quot;

## Word 문서에서 정책 제거 {#removing-policies-from-word-documents}

정책으로 보호된 Word 문서에서 정책을 제거하여 문서에서 보안을 제거할 수 있습니다. 즉, 더 이상 정책으로 문서를 보호하지 않으려는 경우. 정책으로 보호된 Word 문서를 최신 정책으로 업데이트하려면 정책을 제거하고 업데이트된 정책을 추가하는 대신 정책을 전환하는 것이 더 효율적입니다.

>[!NOTE]
>
>Document Security 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-12}

정책으로 보호된 Word 문서에서 정책을 제거하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. Document Security 클라이언트 API 개체를 만듭니다.
1. 정책으로 보호된 Word 문서를 검색합니다.
1. Word 문서에서 정책을 제거합니다.
1. 보안되지 않은 Word 문서 저장

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Document Security 클라이언트 API 개체 만들기**

Document Security 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Document Security 서비스 클라이언트 개체를 만듭니다.

**정책으로 보호된 Word 문서 검색**

정책으로 보호된 Word 문서를 검색하여 정책을 제거합니다. 정책으로 보호되지 않는 Word 문서에서 정책을 제거하려고 하면 예외가 발생합니다.

**Word 문서에서 정책 제거**

연결 설정에 관리자가 지정되어 있으면 정책으로 보호된 Word 문서에서 정책을 제거할 수 있습니다. 그렇지 않으면 문서 보안에 사용되는 정책에 Word 문서에서 정책을 제거하려면 `SWITCH_POLICY` 권한이 있어야 합니다. 또한 AEM Forms 연결 설정에 지정된 사용자에게도 해당 권한이 있어야 합니다. 그렇지 않으면 예외가 throw됩니다.

**보안되지 않은 Word 문서 저장**

Document Security 서비스가 Word 문서에서 정책을 제거한 후 보안되지 않은 Word 문서를 DOC 파일로 저장할 수 있습니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Word 문서에 정책 적용](protecting-documents-policies.md#applying-policies-to-word-documents)

### Java API를 사용하여 Word 문서에서 정책 제거 {#remove-a-policy-from-a-word-document-using-the-java-api}

Document Security API(Java)를 사용하여 정책으로 보호된 Word 문서에서 정책을 제거합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-rightsmanagement-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. Document Security 클라이언트 API 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `RightsManagementClient` 개체를 만듭니다.

1. 정책으로 보호된 Word 문서 검색

   * 생성자를 사용하고 Word 문서의 위치를 지정하는 문자열 값을 전달하여 정책으로 보호된 Word 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. Word 문서에서 정책 제거

   * `RightsManagementClient` 개체의 `getDocumentManager` 메서드를 호출하여 `DocumentManager` 개체를 만듭니다.
   * `DocumentManager` 개체의 `removeSecurity` 메서드를 호출하고 정책으로 보호된 Word 문서가 포함된 `com.adobe.idp.Document` 개체를 전달하여 Word 문서에서 정책을 제거합니다. 이 메서드는 보안되지 않은 Word 문서가 포함된 `com.adobe.idp.Document` 개체를 반환합니다.

1. 보안되지 않은 Word 문서 저장

   * `java.io.File` 개체를 만들고 파일 확장명이 DOC인지 확인합니다.
   * `Document` 개체의 `copyToFile` 메서드를 호출하여 `Document` 개체의 내용을 파일에 복사합니다(`removeSecurity` 메서드에서 반환된 `Document` 개체를 사용하는지 확인).

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(SOAP 모드): Java API를 사용하여 Word 문서에서 정책 제거&quot;

### 웹 서비스 API를 사용하여 Word 문서에서 정책 제거 {#remove-a-policy-from-a-word-document-using-the-web-service-api}

Document Security API(웹 서비스)를 사용하여 정책으로 보호된 Word 문서에서 정책을 제거합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. Document Security 클라이언트 API 개체 만들기

   * 기본 생성자를 사용하여 `RightsManagementServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `RightsManagementServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/RightsManagementService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `RightsManagementServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `RightsManagementServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `RightsManagementServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.

   * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 정책으로 보호된 Word 문서 검색

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 정책이 제거된 정책으로 보호된 Word 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 Word 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 해당 `MTOM` 필드를 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.

1. Word 문서에서 정책 제거

   `RightsManagementServiceClient` 개체의 `removePolicySecurity` 메서드를 호출하고 정책으로 보호된 Word 문서가 포함된 `BLOB` 개체를 전달하여 Word 문서에서 정책을 제거합니다. 이 메서드는 보안되지 않은 Word 문서가 포함된 `BLOB` 개체를 반환합니다.

1. 보안되지 않은 Word 문서 저장

   * 해당 생성자를 호출하고 보안되지 않은 Word 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `removePolicySecurity` 메서드에서 반환된 `BLOB` 개체의 데이터 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 필드 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.

**코드 예제**

Document Security 서비스를 사용하는 코드 예에 대해서는 다음 빠른 시작을 참조하십시오.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 Word 문서에서 정책 제거&quot;

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
