---
title: 사용자 관리
seo-title: Managing Users
description: 사용자 관리 API를 사용하여 역할, 권한 및 주체(사용자 또는 그룹일 수 있음)를 관리하고 사용자를 인증할 수 있는 클라이언트 응용 프로그램을 만듭니다.
seo-description: Use the User Management API to create client applications that can manage roles, permissions, and principals (which can be users or groups), as well as authenticate users.
uuid: 68d8a0bc-6e3d-4286-ba5c-534dcf58cb84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 95804bff-9e6f-4807-aae4-790bd9e7cb57
role: Developer
exl-id: d7c5bb84-a988-4b2e-a587-f4e5b50fea58
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '6228'
ht-degree: 0%

---

# 사용자 관리 {#managing-users}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms용입니다.**

**사용자 관리 정보**

사용자 관리 API를 사용하여 역할, 권한 및 주체(사용자 또는 그룹일 수 있음)를 관리하고 사용자를 인증할 수 있는 클라이언트 애플리케이션을 만들 수 있습니다. 사용자 관리 API는 다음 AEM Forms API로 구성됩니다.

* 디렉터리 관리자 서비스 API
* 인증 관리자 서비스 API
* 인증 관리자 서비스 API

사용자 관리를 사용하면 역할 및 권한을 지정, 제거 및 결정할 수 있습니다. 도메인, 사용자 및 그룹을 할당, 제거 및 쿼리할 수도 있습니다. 마지막으로 사용자 관리를 사용하여 사용자를 인증할 수 있습니다.

in [사용자 추가](users.md#adding-users) 프로그래밍 방식으로 사용자를 추가하는 방법을 이해할 수 있습니다. 이 섹션에서는 디렉토리 관리자 서비스 API를 사용합니다.

in [사용자 삭제](users.md#deleting-users) 프로그래밍 방식으로 사용자를 삭제하는 방법을 이해합니다. 이 섹션에서는 디렉토리 관리자 서비스 API를 사용합니다.

in [사용자 및 그룹 관리](users.md#managing-users-and-groups) 로컬 사용자와 디렉토리 사용자의 차이점을 파악하고 Java 및 웹 서비스 API를 사용하여 사용자와 그룹을 프로그래밍 방식으로 관리하는 방법의 예를 볼 수 있습니다. 이 섹션에서는 디렉토리 관리자 서비스 API를 사용합니다.

in [역할 및 권한 관리](users.md#managing-roles-and-permissions) 시스템 역할 및 권한과 이를 증가시키기 위해 프로그래밍 방식으로 수행할 수 있는 작업에 대해 학습하고, Java 및 웹 서비스 API를 사용하여 역할 및 권한을 프로그래밍 방식으로 관리하는 방법의 예를 참조하십시오. 이 섹션에서는 Directory Manager 서비스 API 및 Authorization Manager 서비스 API를 모두 사용합니다.

in [사용자 인증](users.md#authenticating-users) Java 및 웹 서비스 API를 사용하여 사용자를 프로그래밍 방식으로 인증하는 방법의 예를 볼 수 있습니다. 이 섹션에서는 인증 관리자 서비스 API를 사용합니다.

**인증 프로세스 이해**

사용자 관리에서는 기본 제공 인증 기능을 제공하며, 자체 인증 공급자와 연결할 수 있는 기능도 제공합니다. 사용자 관리에서 인증 요청을 받으면(예: 사용자가 로그인하려고 함) 사용자 정보를 인증 공급자에게 전달하여 인증합니다. 사용자 관리는 사용자를 인증한 후 인증 공급자로부터 결과를 수신합니다.

다음 다이어그램은 로그인하려는 최종 사용자, 사용자 관리 및 인증 공급자 간의 상호 작용을 보여줍니다.

![mu_mu_umauth_process](assets/mu_mu_umauth_process.png)

다음 표에서는 인증 프로세스의 각 단계에 대해 설명합니다.

<table>
 <thead>
  <tr>
   <th><p>단계</p></th>
   <th><p>설명</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>사용자가 사용자 관리를 호출하는 서비스에 로그인하려고 합니다. 사용자가 사용자 이름과 암호를 지정합니다. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>사용자 관리에서는 사용자 이름 및 암호와 구성 정보를 인증 공급자에게 보냅니다.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>인증 공급자는 사용자 저장소에 연결하고 사용자를 인증합니다.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>인증 공급자가 결과를 사용자 관리에 반환합니다.</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>사용자 관리에서 사용자가 로그인하거나 제품 액세스를 거부할 수 있습니다.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>서버 시간대가 클라이언트 시간대와 다른 경우 WebSphere Application Server 클러스터에서 .NET 클라이언트를 사용하여 기본 SOAP 스택에서 AEM Forms Generate PDF 서비스용 WSDL을 사용하는 경우 다음 사용자 관리 인증 오류가 발생할 수 있습니다.

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**디렉토리 관리 이해**

사용자 관리는 LDAP 디렉터리에 대한 연결을 지원하는 디렉터리 서비스 공급자(DirectoryManagerService)와 함께 패키지되어 있습니다. 조직에서 비LDAP 리포지토리를 사용하여 사용자 레코드를 저장하는 경우, 리포지토리와 함께 작동하는 고유한 디렉토리 서비스 공급자를 생성할 수 있습니다.

디렉터리 서비스 공급자는 사용자 관리의 요청에 따라 사용자 저장소에서 레코드를 검색합니다. 사용자 관리는 데이터베이스의 사용자 및 그룹 레코드를 정기적으로 캐시하여 성능을 향상시킵니다.

디렉터리 서비스 공급자를 사용하여 사용자 관리 데이터베이스를 사용자 저장소와 동기화할 수 있습니다. 이 단계에서는 모든 사용자 디렉토리 정보와 모든 사용자 및 그룹 레코드가 최신 상태가 되도록 합니다.

또한 DirectoryManagerService는 도메인을 만들고 관리할 수 있는 기능을 제공합니다. 도메인은 서로 다른 사용자 기반을 정의합니다. 도메인의 경계는 일반적으로 조직의 구성 방식 또는 사용자 저장소의 설정 방법에 따라 정의됩니다. 사용자 관리 도메인은 인증 공급자 및 디렉토리 서비스 공급자가 사용하는 구성 설정을 제공합니다.

사용자 관리가 내보내는 구성 XML에서 속성 값이 인 루트 노드입니다 `Domains` 사용자 관리를 위해 정의된 각 도메인에 대한 XML 요소를 포함합니다. 이러한 각 요소에는 특정 서비스 공급자와 연관된 도메인의 측면을 정의하는 다른 요소가 포함되어 있습니다.

**objectSID 값 이해**

Active Directory를 사용할 때는 `objectSID` 값은 여러 도메인에서 고유한 속성이 아닙니다. 이 값은 개체의 보안 식별자를 저장합니다. 여러 도메인 환경(예: 도메인 트리)에서는 `objectSID` 값은 다를 수 있습니다.

An `objectSID` 개체가 한 Active Directory 도메인에서 다른 도메인으로 이동되면 값이 변경됩니다. 일부 개체는 동일합니다 `objectSID` 값은 도메인에 있는 모든 위치에 있습니다. 예를 들어, BUILTIN\Administrators, BUILTIN\Power Users 등과 같은 그룹에는 동일한 항목이 있습니다 `objectSID` 값과 상관 없이 상관 없습니다. 다음 `objectSID` 값은 잘 알려져 있습니다.

## 사용자 추가 {#adding-users}

Directory Manager Service API(Java 및 웹 서비스)를 사용하여 사용자를 프로그래밍 방식으로 AEM Forms에 추가할 수 있습니다. 사용자를 추가한 후 사용자가 필요한 서비스 작업을 수행할 때 해당 사용자를 사용할 수 있습니다. 예를 들어 새 사용자에게 작업을 할당할 수 있습니다.

### 단계 요약 {#summary-of-steps}

사용자를 추가하려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. DirectoryManagerService 클라이언트를 만듭니다.
1. 사용자 정보를 정의합니다.
1. 사용자를 AEM Forms에 추가합니다.
1. 사용자가 추가되었는지 확인합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

**DirectoryManagerService 클라이언트 만들기**

Directory Manager 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Directory Manager Service API 클라이언트를 만듭니다.

**사용자 정보 정의**

디렉토리 관리자 서비스 API를 사용하여 새 사용자를 추가할 때 해당 사용자에 대한 정보를 정의합니다. 일반적으로 새 사용자를 추가할 때 다음 값을 정의합니다.

* **도메인 이름**: 사용자가 속한 도메인(예: `DefaultDom`).
* **사용자 식별자 값**: 사용자의 식별자 값(예: `wblue`).
* **주체 유형**: 사용자 유형(예: `USER)`.
* **지정된 이름**: 사용자에 대해 지정된 이름(예: `Wendy`).
* **가족 이름**: 사용자의 가족 이름(예: `Blue)`.
* **로케일**: 사용자의 로케일 정보입니다.

**AEM Forms에 사용자 추가**

사용자 정보를 정의한 후 사용자를 AEM Forms에 추가할 수 있습니다. 사용자를 추가하려면 `DirectoryManagerServiceClient` 개체 `createLocalUser` 메서드를 사용합니다.

**사용자가 추가되었는지 확인합니다**

사용자가 추가되어 문제가 발생하지 않았는지 확인할 수 있습니다. 사용자 식별자 값을 사용하여 새 사용자를 찾습니다.

**추가 참조**

[Java API를 사용하여 사용자 추가](users.md#add-users-using-the-java-api)

[웹 서비스 API를 사용하여 사용자 추가](users.md#add-users-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[사용자 삭제](users.md#deleting-users)

### Java API를 사용하여 사용자 추가 {#add-users-using-the-java-api}

Directory Manager 서비스 API(Java)를 사용하여 사용자를 추가합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-usermanager-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. DirectoryManagerServices 클라이언트를 만듭니다.

   만들기 `DirectoryManagerServiceClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.

1. 사용자 정보를 정의합니다.

   * 만들기 `UserImpl` 생성자를 사용하여 개체를 작성합니다.
   * 를 호출하여 도메인 이름을 설정합니다 `UserImpl` 개체 `setDomainName` 메서드를 사용합니다. 도메인 이름을 지정하는 문자열 값을 전달합니다.
   * 다음 코드를 호출하여 주체 유형을 설정합니다 `UserImpl` 개체 `setPrincipalType` 메서드를 사용합니다. 사용자 유형을 지정하는 문자열 값을 전달합니다. 예를 들어 `USER`.
   * 사용자 ID 값을 `UserImpl` 개체 `setUserid` 메서드를 사용합니다. 사용자 식별자 값을 지정하는 문자열 값을 전달합니다. 예를 들어 `wblue`.
   * 를 호출하여 정식 이름을 설정합니다 `UserImpl` 개체 `setCanonicalName` 메서드를 사용합니다. 사용자의 정식 이름을 지정하는 문자열 값을 전달합니다. 예를 들어 `wblue`.
   * 를 호출하여 지정된 이름을 설정합니다 `UserImpl` 개체 `setGivenName` 메서드를 사용합니다. 사용자의 지정된 이름을 지정하는 문자열 값을 전달합니다. 예를 들어 `Wendy`.
   * 를 호출하여 패밀리 이름을 설정합니다 `UserImpl` 개체 `setFamilyName` 메서드를 사용합니다. 사용자의 가족 이름을 지정하는 문자열 값을 전달합니다. 예를 들어 `Blue`.

   >[!NOTE]
   >
   >에 속하는 메서드 호출 `UserImpl` 다른 값을 설정할 개체 예를 들어 `UserImpl` 개체 `setLocale` 메서드를 사용합니다.

1. 사용자를 AEM Forms에 추가합니다.

   를 호출합니다 `DirectoryManagerServiceClient` 개체 `createLocalUser` 메서드를 사용하여 다음 값을 전달합니다.

   * 다음 `UserImpl` 새 사용자를 나타내는 개체
   * 사용자의 암호를 나타내는 문자열 값입니다

   다음 `createLocalUser` 메서드는 로컬 사용자 식별자 값을 지정하는 문자열 값을 반환합니다.

1. 사용자가 추가되었는지 확인합니다.

   * 만들기 `PrincipalSearchFilter` 생성자를 사용하여 개체를 작성합니다.
   * 사용자 ID 값을 `PrincipalSearchFilter` 개체 `setUserId` 메서드를 사용합니다. 사용자 식별자 값을 나타내는 문자열 값을 전달합니다.
   * 를 호출합니다 `DirectoryManagerServiceClient` 개체 `findPrincipals` 메서드 및 전달 `PrincipalSearchFilter` 개체. 이 메서드는 `java.util.List` 인스턴스: 각 요소가 `User` 개체. 를 통해 반복 `java.util.List` 인스턴스를 사용하여 사용자를 찾습니다.

**추가 참조**

[단계 요약](users.md#summary-of-steps)

[빠른 시작(SOAP 모드): Java API를 사용하여 사용자 추가](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 사용자 추가 {#add-users-using-the-web-service-api}

디렉터리 관리자 서비스 API(웹 서비스)를 사용하여 사용자를 추가합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 서비스 참조에 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. DirectoryManagerService 클라이언트를 만듭니다.

   * 만들기 `DirectoryManagerServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `DirectoryManagerServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 다음을 지정했는지 확인합니다 `?blob=mtom`.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `DirectoryManagerServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. 사용자 정보를 정의합니다.

   * 만들기 `UserImpl` 생성자를 사용하여 개체를 작성합니다.
   * 에 문자열 값을 할당하여 도메인 이름을 설정합니다. `UserImpl` 개체 `domainName` 필드.
   * 문자열 값을 `UserImpl` 개체 `principalType` 필드. 예를 들어 `USER`.
   * 문자열 값을 `UserImpl` 개체 `userid` 필드.
   * 문자열 값을 `UserImpl` 개체 `canonicalName` 필드.
   * 문자열 값을 `UserImpl` 개체 `givenName` 필드.
   * 문자열 값을 `UserImpl` 개체 `familyName` 필드.

1. 사용자를 AEM Forms에 추가합니다.

   를 호출합니다 `DirectoryManagerServiceClient` 개체 `createLocalUser` 메서드를 사용하여 다음 값을 전달합니다.

   * 다음 `UserImpl` 새 사용자를 나타내는 개체
   * 사용자의 암호를 나타내는 문자열 값입니다

   다음 `createLocalUser` 메서드는 로컬 사용자 식별자 값을 지정하는 문자열 값을 반환합니다.

1. 사용자가 추가되었는지 확인합니다.

   * 만들기 `PrincipalSearchFilter` 생성자를 사용하여 개체를 작성합니다.
   * 사용자 식별자 값을 나타내는 문자열 값을 로 할당하여 사용자의 사용자 식별자 값을 설정합니다. `PrincipalSearchFilter` 개체 `userId` 필드.
   * 를 호출합니다 `DirectoryManagerServiceClient` 개체 `findPrincipals` 메서드 및 전달 `PrincipalSearchFilter` 개체. 이 메서드는 `MyArrayOfUser` 컬렉션 개체(각 요소가 `User` 개체. 를 통해 반복 `MyArrayOfUser` 컬렉션을 클릭하여 사용자를 찾습니다.

**추가 참조**

[단계 요약](users.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 사용자 삭제 {#deleting-users}

Directory Manager Service API(Java 및 웹 서비스)를 사용하여 AEM Forms에서 사용자를 프로그래밍 방식으로 삭제할 수 있습니다. 사용자를 삭제한 후에는 사용자가 필요한 서비스 작업을 수행하는 데 더 이상 사용할 수 없습니다. 예를 들어, 삭제된 사용자에게 작업을 할당할 수 없습니다.

### 단계 요약 {#summary_of_steps-1}

사용자를 삭제하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. DirectoryManagerService 클라이언트를 만듭니다.
1. 삭제할 사용자를 지정합니다.
1. AEM Forms에서 사용자를 삭제합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

**DirectoryManagerService 클라이언트 만들기**

Directory Manager 서비스 API 작업을 프로그래밍 방식으로 수행하려면 먼저 Directory Manager 서비스 클라이언트를 만듭니다.

**삭제할 사용자를 지정합니다**

사용자의 식별자 값을 사용하여 삭제할 사용자를 지정할 수 있습니다.

**AEM Forms에서 사용자 삭제**

사용자를 삭제하려면 `DirectoryManagerServiceClient` 개체 `deleteLocalUser` 메서드를 사용합니다.

**추가 참조**

[Java API를 사용하여 사용자 삭제](users.md#delete-users-using-the-java-api)

[웹 서비스 API를 사용하여 사용자 삭제](users.md#delete-users-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[사용자 추가](users.md#adding-users)

### Java API를 사용하여 사용자 삭제 {#delete-users-using-the-java-api}

Directory Manager 서비스 API(Java)를 사용하여 사용자를 삭제합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-usermanager-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. DirectoryManagerService 클라이언트를 만듭니다.

   만들기 `DirectoryManagerServiceClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.

1. 삭제할 사용자를 지정합니다.

   * 만들기 `PrincipalSearchFilter` 생성자를 사용하여 개체를 작성합니다.
   * 사용자 ID 값을 `PrincipalSearchFilter` 개체 `setUserId` 메서드를 사용합니다. 사용자 식별자 값을 나타내는 문자열 값을 전달합니다.
   * 를 호출합니다 `DirectoryManagerServiceClient` 개체 `findPrincipals` 메서드 및 전달 `PrincipalSearchFilter` 개체. 이 메서드는 `java.util.List` 인스턴스: 각 요소가 `User` 개체. 를 통해 반복 `java.util.List` 삭제할 사용자를 찾을 인스턴스입니다.

1. AEM Forms에서 사용자를 삭제합니다.

   를 호출합니다 `DirectoryManagerServiceClient` 개체 `deleteLocalUser` 메서드 및 `User` 개체 `oid` 필드. 를 호출합니다 `User` 개체 `getOid` 메서드를 사용합니다. 를 사용하십시오 `User` 개체에서 검색된 개체 `java.util.List` 인스턴스.

**추가 참조**

[단계 요약](users.md#summary-of-steps)

[빠른 시작(EJB 모드): Java API를 사용하여 사용자 삭제](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 사용자 삭제](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 사용자 삭제 {#delete-users-using-the-web-service-api}

디렉터리 관리자 서비스 API(웹 서비스)를 사용하여 사용자를 삭제합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-usermanager-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. DirectoryManagerService 클라이언트를 만듭니다.

   * 만들기 `DirectoryManagerServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `DirectoryManagerServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 다음을 지정했는지 확인합니다 `blob=mtom.`
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `DirectoryManagerServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. 삭제할 사용자를 지정합니다.

   * 만들기 `PrincipalSearchFilter` 생성자를 사용하여 개체를 작성합니다.
   * 문자열 값을 `PrincipalSearchFilter` 개체 `userId` 필드.
   * 를 호출합니다 `DirectoryManagerServiceClient` 개체 `findPrincipals` 메서드 및 전달 `PrincipalSearchFilter` 개체. 이 메서드는 `MyArrayOfUser` 컬렉션 개체(각 요소가 `User` 개체. 를 통해 반복 `MyArrayOfUser` 컬렉션을 클릭하여 사용자를 찾습니다. 다음 `User` 개체에서 검색된 개체 `MyArrayOfUser` 컬렉션 개체는 사용자를 삭제하는 데 사용됩니다.

1. AEM Forms에서 사용자를 삭제합니다.

   을 전달하여 사용자를 삭제합니다. `User` 개체 `oid` 필드 값 `DirectoryManagerServiceClient` 개체 `deleteLocalUser` 메서드를 사용합니다.

**추가 참조**

[단계 요약](users.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 그룹 만들기 {#creating-groups}

Directory Manager Service API(Java 및 웹 서비스)를 사용하여 프로그래밍 방식으로 AEM Forms 그룹을 만들 수 있습니다. 그룹을 생성한 후에는 해당 그룹을 사용하여 그룹이 필요한 서비스 작업을 수행할 수 있습니다. 예를 들어 사용자를 새 그룹에 할당할 수 있습니다. (자세한 내용은 [사용자 및 그룹 관리](users.md#managing-users-and-groups))

### 단계 요약 {#summary_of_steps-2}

그룹을 만들려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. DirectoryManagerService 클라이언트를 만듭니다.
1. 그룹이 존재하지 않는지 확인합니다.
1. 그룹을 만듭니다.
1. 그룹을 사용하여 작업을 수행합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포되는 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**DirectoryManagerService 클라이언트 만들기**

Directory Manager 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Directory Manager Service API 클라이언트를 만듭니다.

**그룹이 있는지 확인**

그룹을 만들 때 해당 그룹이 동일한 도메인에 없는지 확인합니다. 즉, 동일한 도메인 내에 두 그룹의 이름이 같을 수 없습니다. 이 작업을 수행하려면 검색을 수행하고 두 값을 기준으로 검색 결과를 필터링하십시오. 주체 유형을 로 설정합니다. `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` 그룹만 반환되는지 확인합니다. 또한 도메인 이름을 지정해야 합니다.

**그룹 만들기**

해당 그룹이 도메인에 존재하지 않는다고 결정하면 그룹을 만들고 다음 속성을 지정합니다.

* **CommonName**: 그룹의 이름입니다.
* **도메인**: 그룹이 추가되는 도메인입니다.
* **설명**: 그룹에 대한 설명입니다.

**그룹을 사용하여 작업 수행**

그룹을 만든 후 그룹을 사용하여 작업을 수행할 수 있습니다. 예를 들어 사용자를 그룹에 추가할 수 있습니다. 사용자를 그룹에 추가하려면 사용자와 그룹 모두의 고유 식별자 값을 검색합니다. 다음 값을에 전달 `addPrincipalToLocalGroup` 메서드를 사용합니다.

**추가 참조**

[Java API를 사용하여 그룹 만들기](users.md#create-groups-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[사용자 추가](users.md#adding-users)

[사용자 삭제](users.md#deleting-users)

### Java API를 사용하여 그룹 만들기 {#create-groups-using-the-java-api}

Directory Manager 서비스 API(Java)를 사용하여 그룹을 만듭니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-usermanager-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. DirectoryManagerService 클라이언트를 만듭니다.

   만들기 `DirectoryManagerServiceClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.

1. 그룹이 있는지 여부를 결정합니다.

   * 만들기 `PrincipalSearchFilter` 생성자를 사용하여 개체를 작성합니다.
   * 다음 코드를 호출하여 주체 유형을 설정합니다 `PrincipalSearchFilter` 개체 `setPrincipalType` 개체. 값 전달 `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`.
   * 을 호출하여 도메인을 설정합니다 `PrincipalSearchFilter` 개체 `setSpecificDomainName` 개체. 도메인 이름을 지정하는 문자열 값을 전달합니다.
   * 그룹을 찾으려면 `DirectoryManagerServiceClient` 개체 `findPrincipals` 메서드(주도자는 그룹일 수 있음). 전달 `PrincipalSearchFilter` 주체 유형 및 도메인 이름을 지정하는 개체입니다. 이 메서드는 `java.util.List` 각 요소가 인 인스턴스 `Group` 인스턴스. 각 그룹 인스턴스는 `PrincipalSearchFilter` 개체.
   * 를 통해 반복 `java.util.List` 인스턴스. 각 요소에 대해 그룹 이름을 검색합니다. 그룹 이름이 새 그룹 이름과 같지 않은지 확인하십시오.

1. 그룹을 만듭니다.

   * 그룹이 없으면 `Group` 개체 `setCommonName` 메서드를 사용하여 그룹 이름을 지정하는 문자열 값을 전달합니다.
   * 를 호출합니다 `Group` 개체 `setDescription` 메서드를 사용하여 그룹 설명을 지정하는 문자열 값을 전달합니다.
   * 를 호출합니다 `Group` 개체 `setDomainName` 메서드를 사용하여 도메인 이름을 지정하는 문자열 값을 전달합니다.
   * 를 호출합니다 `DirectoryManagerServiceClient` 개체 `createLocalGroup` 메서드 및 전달 `Group` 인스턴스.

   다음 `createLocalUser` 메서드는 로컬 사용자 식별자 값을 지정하는 문자열 값을 반환합니다.

1. 그룹을 사용하여 작업을 수행합니다.

   * 만들기 `PrincipalSearchFilter` 생성자를 사용하여 개체를 작성합니다.
   * 사용자 ID 값을 `PrincipalSearchFilter` 개체 `setUserId` 메서드를 사용합니다. 사용자 식별자 값을 나타내는 문자열 값을 전달합니다.
   * 를 호출합니다 `DirectoryManagerServiceClient` 개체 `findPrincipals` 메서드 및 전달 `PrincipalSearchFilter` 개체. 이 메서드는 `java.util.List` 인스턴스: 각 요소가 `User` 개체. 를 통해 반복 `java.util.List` 인스턴스를 사용하여 사용자를 찾습니다.
   * 를 호출하여 그룹에 사용자 추가 `DirectoryManagerServiceClient` 개체 `addPrincipalToLocalGroup` 메서드를 사용합니다. 의 반환 값 전달 `User` 개체 `getOid` 메서드를 사용합니다. 의 반환 값 전달 `Group` 개체 `getOid` 메서드(를 사용하여 `Group` 새 그룹을 나타내는 인스턴스)입니다.

**추가 참조**

[단계 요약](users.md#summary-of-steps)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 사용자 및 그룹 관리 {#managing-users-and-groups}

이 항목에서는 (Java)를 사용하여 프로그래밍 방식으로 도메인, 사용자 및 그룹을 지정, 제거 및 쿼리하는 방법을 설명합니다.

>[!NOTE]
>
>도메인을 구성할 때는 그룹 및 사용자에 대한 고유 식별자를 설정해야 합니다. 선택한 속성은 LDAP 환경 내에서 고유해야 할 뿐만 아니라 변경할 수 없으며 디렉토리 내에서 변경되지 않아야 합니다. 또한 이 특성은 단순 문자열 데이터 유형이어야 합니다(현재 Active Directory2000/2003에 허용되는 유일한 예외는 `"objectsid"`: 이진 값)입니다. Novell eDirectory 속성 `"GUID"`예를 들어 는 단순 문자열 데이터 유형이 아니므로 작동하지 않습니다.

* Active Directory의 경우 `"objectsid"`.
* SunOne의 경우 `"nsuniqueid"`.

>[!NOTE]
>
>LDAP 디렉터리 동기화가 진행 중인 동안 여러 로컬 사용자 및 그룹을 만들 수 없습니다. 이 프로세스를 시도하면 오류가 발생할 수 있습니다.

### 단계 요약 {#summary_of_steps-3}

사용자 및 그룹을 관리하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. DirectoryManagerService 클라이언트를 만듭니다.
1. 해당 사용자 또는 그룹 작업을 호출합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**DirectoryManagerService 클라이언트 만들기**

Directory Manager 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Directory Manager 서비스 클라이언트를 만들어야 합니다. Java API를 사용하면 `DirectoryManagerServiceClient` 개체. 웹 서비스 API를 사용하면 `DirectoryManagerServiceService` 개체.

**적절한 사용자 또는 그룹 작업 호출**

서비스 클라이언트를 만들었으면 사용자 또는 그룹 관리 작업을 호출할 수 있습니다. 서비스 클라이언트를 사용하면 도메인, 사용자 및 그룹을 할당, 제거 및 쿼리할 수 있습니다. 디렉터리 주체 또는 로컬 주도자를 로컬 그룹에 추가할 수 있지만 로컬 주도자를 디렉터리 그룹에 추가할 수는 없습니다.

**추가 참조**

[Java API를 사용하여 사용자 및 그룹 관리](users.md#managing-users-and-groups-using-the-java-api)

[웹 서비스 API를 사용하여 사용자 및 그룹 관리](users.md#managing-users-and-groups-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[사용자 관리자 API 빠른 시작](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Java API를 사용하여 사용자 및 그룹 관리 {#managing-users-and-groups-using-the-java-api}

(Java)를 사용하여 사용자, 그룹 및 도메인을 프로그래밍 방식으로 관리하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-usermanager-client.jar와 같은 클라이언트 JAR 파일을 포함합니다. 이러한 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. DirectoryManagerService 클라이언트를 만듭니다.

   만들기 `DirectoryManagerServiceClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다. 자세한 내용은 [연결 속성 설정&#x200B;](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*.*

1. 해당 사용자 또는 그룹 작업을 호출합니다.

   사용자 또는 그룹을 찾으려면 다음 중 하나를 호출합니다 `DirectoryManagerServiceClient` 주도자를 찾기 위한 개체의 메서드입니다. 주도자는 사용자 또는 그룹일 수 있으므로 아래 예에서는 `findPrincipals` 메서드는 검색 필터( )를 사용하여 호출됩니다 `PrincipalSearchFilter` 개체)를 참조하십시오.

   이 경우 반환 값이 `java.util.List` 포함 `Principal` 개체, 결과 반복 및 캐스트 `Principal` 개체 `User` 또는 `Group` 개체.

   결과 사용 `User` 또는 `Group` 객체(둘 다 `Principal` 인터페이스)를 사용하여 워크플로우에서 필요한 정보를 검색합니다. 예를 들어 도메인 이름 및 정식 이름 값이 조합되어 주도자를 고유하게 식별합니다. 이러한 함수는 `Principal` 개체 `getDomainName` 및 `getCanonicalName` 메서드를 사용합니다.

   로컬 사용자를 삭제하려면 `DirectoryManagerServiceClient` 개체 `deleteLocalUser` 메서드를 사용하여 사용자 식별자를 전달합니다.

   로컬 그룹을 삭제하려면 `DirectoryManagerServiceClient` 개체 `deleteLocalGroup` 메서드를 사용하여 그룹의 식별자를 전달합니다.

**추가 참조**

[단계 요약](users.md#summary-of-steps)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 사용자 및 그룹 관리 {#managing-users-and-groups-using-the-web-service-api}

Directory Manager 서비스 API(웹 서비스)를 사용하여 사용자, 그룹 및 도메인을 프로그래밍 방식으로 관리하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.

   * Directory Manager WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다. (자세한 내용은 [Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding))
   * Microsoft .NET 클라이언트 어셈블리를 참조합니다. (자세한 내용은 [Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding))

1. DirectoryManagerService 클라이언트를 만듭니다.

   만들기 `DirectoryManagerServiceService` 프록시 클래스의 생성자를 사용하여 개체를 작성합니다.

1. 해당 사용자 또는 그룹 작업을 호출합니다.

   사용자 또는 그룹을 찾으려면 다음 중 하나를 호출합니다 `DirectoryManagerServiceService` 주도자를 찾기 위한 개체의 메서드입니다. 주도자는 사용자 또는 그룹일 수 있으므로 아래 예에서는 `findPrincipalsWithFilter` 메서드는 검색 필터( )를 사용하여 호출됩니다 `PrincipalSearchFilter` 개체)를 참조하십시오. 사용 시 `PrincipalSearchFilter` 객체, 로컬 주도자는 `isLocal` 속성이 `true`. 이 동작은 Java API에서 발생하는 것과 다릅니다.

   >[!NOTE]
   >
   >검색 필터에 최대 결과 수가 지정되지 않은 경우 `PrincipalSearchFilter.resultsMax` 필드)이면 최대 1000개의 결과가 반환됩니다. 이는 Java API를 사용하여 발생하는 것과 다른 동작으로, 10개의 결과가 기본 최대입니다. 또한 다음과 같은 검색 방법을 사용합니다. `findGroupMembers` 검색 필터에 최대 결과 수를 지정하지 않는 한(예를 들어 `GroupMembershipSearchFilter.resultsMax` 필드)만 로드하는 것입니다. 이는 `GenericSearchFilter` 클래스 이름을 지정합니다. 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   이 경우 반환 값이 `object[]` 포함 `Principal` 개체, 결과 반복 및 캐스트 `Principal` 개체 `User` 또는 `Group` 개체.

   결과 사용 `User` 또는 `Group` 객체(둘 다 `Principal` 인터페이스)를 사용하여 워크플로우에서 필요한 정보를 검색합니다. 예를 들어 도메인 이름 및 정식 이름 값이 조합되어 주도자를 고유하게 식별합니다. 이러한 함수는 `Principal` 개체 `domainName` 및 `canonicalName` 필드(각각)를 반환합니다.

   로컬 사용자를 삭제하려면 `DirectoryManagerServiceService` 개체 `deleteLocalUser` 메서드를 사용하여 사용자 식별자를 전달합니다.

   로컬 그룹을 삭제하려면 `DirectoryManagerServiceService` 개체 `deleteLocalGroup` 메서드를 사용하여 그룹의 식별자를 전달합니다.

**추가 참조**

[단계 요약](users.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 역할 및 권한 관리 {#managing-roles-and-permissions}

이 항목에서는 Authorization Manager Service API(Java)를 사용하여 역할 및 권한을 프로그래밍 방식으로 지정, 제거 및 결정하는 방법에 대해 설명합니다.

AEM Forms에서 *역할* 하나 이상의 시스템 수준 리소스에 액세스하기 위한 권한 그룹입니다. 이러한 권한은 사용자 관리를 통해 만들어지며 서비스 구성 요소에 적용됩니다. 예를 들어, 관리자는 사용자 그룹에 &quot;정책 세트 작성자&quot; 역할을 할당할 수 있습니다. 그런 다음 Rights Management은 해당 역할을 가진 해당 그룹의 사용자가 관리 콘솔을 통해 정책 세트를 작성할 수 있도록 허용합니다.

두 가지 유형의 역할이 있습니다. *기본 역할* 및 *사용자 지정 역할*. 기본 역할 (*시스템 역할)* 은(는) 이미 AEM Forms에 있습니다. 관리자가 기본 역할을 삭제하거나 수정할 수 없으므로 변경할 수 없다고 가정합니다. 관리자가 만든 사용자 지정 역할은 나중에 수정하거나 삭제할 수 있으므로 변경할 수 있습니다.

역할을 사용하면 권한을 쉽게 관리할 수 있습니다. 주도자에게 역할을 할당하면 권한 세트가 자동으로 해당 주도자에게 할당되고 주도자에 대한 모든 특정 액세스 관련 결정은 할당된 전체 권한 집합을 기반으로 합니다.

### 단계 요약 {#summary_of_steps-4}

역할 및 권한을 관리하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. AuthorizationManagerService 클라이언트를 만듭니다.
1. 적절한 역할 또는 권한 작업을 호출합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**AuthorizationManagerService 클라이언트 만들기**

사용자 관리 AuthorizationManagerService 작업을 프로그래밍 방식으로 수행하려면 먼저 AuthorizationManagerService 클라이언트를 만들어야 합니다. Java API를 사용하면 `AuthorizationManagerServiceClient` 개체.

**적절한 역할 또는 권한 작업 호출**

서비스 클라이언트를 만들었으면 역할이나 권한 작업을 호출할 수 있습니다. 서비스 클라이언트를 사용하면 역할 및 권한을 지정, 제거 및 결정할 수 있습니다.

**추가 참조**

[Java API를 사용하여 역할 및 권한 관리](users.md#managing-roles-and-permissions-using-the-java-api)

[웹 서비스 API를 사용하여 역할 및 권한 관리](users.md#managing-roles-and-permissions-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[사용자 관리자 API 빠른 시작](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Java API를 사용하여 역할 및 권한 관리 {#managing-roles-and-permissions-using-the-java-api}

Authorization Manager Service API(Java)를 사용하여 역할 및 권한을 관리하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-usermanager-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. AuthorizationManagerService 클라이언트를 만듭니다.

   만들기 `AuthorizationManagerServiceClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.

1. 적절한 역할 또는 권한 작업을 호출합니다.

   주도자에게 역할을 할당하려면 `AuthorizationManagerServiceClient` 개체 `assignRole` 메서드를 사용하여 다음 값을 전달합니다.

   * A `java.lang.String` 역할 식별자를 포함하는 객체
   * 일련의 `java.lang.String` 주체 식별자를 포함하는 개체

   주도자에서 역할을 제거하려면 `AuthorizationManagerServiceClient` 개체 `unassignRole` 메서드를 사용하여 다음 값을 전달합니다.

   * A `java.lang.String` 역할 식별자를 포함하는 객체입니다.
   * 일련의 `java.lang.String` 주체 식별자를 포함하는 개체


**추가 참조**

[단계 요약](users.md#summary-of-steps)

[빠른 시작(SOAP 모드): Java API를 사용하여 역할 및 권한 관리](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 역할 및 권한 관리 {#managing-roles-and-permissions-using-the-web-service-api}

Authorization Manager Service API(웹 서비스)를 사용하여 역할 및 권한을 관리합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. AuthorizationManagerService 클라이언트를 만듭니다.

   * 만들기 `AuthorizationManagerServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `AuthorizationManagerServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`) 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `AuthorizationManagerServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. 적절한 역할 또는 권한 작업을 호출합니다.

   주도자에게 역할을 할당하려면 `AuthorizationManagerServiceClient` 개체 `assignRole` 메서드를 사용하여 다음 값을 전달합니다.

   * A `string` 역할 식별자를 포함하는 객체
   * A `MyArrayOf_xsd_string` 주체 식별자를 포함하는 객체입니다.

   주도자에서 역할을 제거하려면 `AuthorizationManagerServiceService` 개체 `unassignRole` 메서드를 사용하여 다음 값을 전달합니다.

   * A `string` 역할 식별자를 포함하는 객체입니다.
   * 일련의 `string` 주체 식별자를 포함하는 개체


**추가 참조**

[단계 요약](users.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 사용자 인증 {#authenticating-users}

이 항목에서는 Authentication Manager Service API(Java)를 사용하여 클라이언트 응용 프로그램에서 사용자를 프로그래밍 방식으로 인증하는 방법을 설명합니다.

보안 데이터를 저장하는 엔터프라이즈 데이터베이스 또는 다른 엔터프라이즈 리포지토리와 상호 작용하려면 사용자 인증이 필요할 수 있습니다.

예를 들어, 사용자가 웹 페이지에 사용자 이름과 암호를 입력하고 값을 Forms을 호스팅하는 J2EE 애플리케이션 서버로 전송하는 시나리오를 생각해 보십시오. Forms 사용자 지정 애플리케이션은 인증 관리자 서비스로 사용자를 인증할 수 있습니다.

인증이 성공하면 응용 프로그램은 보안 엔터프라이즈 데이터베이스에 액세스합니다. 그렇지 않으면 사용자가 인증된 사용자가 아니라는 메시지가 사용자에게 전송됩니다.

다음 다이어그램은 응용 프로그램의 논리 플로우를 보여 줍니다.

![au_au_umauth_process](assets/au_au_umauth_process.png)

다음 표에서는 이 다이어그램의 단계에 대해 설명합니다

<table>
 <thead>
  <tr>
   <th><p>단계</p></th>
   <th><p>설명</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>사용자는 웹 사이트에 액세스하여 사용자 이름과 암호를 지정합니다. 이 정보는 AEM Forms을 호스팅하는 J2EE 애플리케이션 서버에 제출됩니다.</p></td>
  </tr>
  <tr>
   <td><p>2개</p></td>
   <td><p>사용자 자격 증명은 인증 관리자 서비스로 인증됩니다. 사용자 자격 증명이 유효하면 워크플로우가 3단계로 진행합니다. 그렇지 않으면 사용자가 인증된 사용자가 아니라는 메시지가 사용자에게 전송됩니다.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>보안 엔터프라이즈 데이터베이스에서 사용자 정보 및 양식 디자인을 검색합니다. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>사용자 정보는 양식 디자인과 병합되고 양식이 사용자에게 렌더링됩니다. </p></td>
  </tr>
 </tbody>
</table>

### 단계 요약 {#summary_of_steps-5}

사용자를 프로그래밍 방식으로 인증하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. AuthenticationManagerService 클라이언트를 만듭니다.
1. 인증 작업을 호출합니다.
1. 필요한 경우 클라이언트 애플리케이션이 인증을 위해 다른 AEM Forms 서비스로 전달할 수 있도록 컨텍스트를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**AuthenticationManagerService 클라이언트 만들기**

사용자를 프로그래밍 방식으로 인증하려면 먼저 AuthenticationManagerService 클라이언트를 만들어야 합니다. Java API를 사용할 때 `AuthenticationManagerServiceClient` 개체.

**인증 작업 호출**

서비스 클라이언트를 만들었으면 인증 작업을 호출할 수 있습니다. 이 작업은 사용자의 이름 및 암호와 같은 사용자에 대한 정보가 필요합니다. 사용자가 인증하지 않으면 예외가 발생합니다.

**인증 컨텍스트 검색**

사용자를 인증하면 인증된 사용자를 기반으로 컨텍스트를 만들 수 있습니다. 그런 다음 컨텐츠를 사용하여 다른 AEM Forms 서비스를 호출할 수 있습니다. 예를 들어 컨텍스트를 사용하여 `EncryptionServiceClient` 또한 암호로 PDF 문서를 암호화합니다. 인증된 사용자에게 라는 역할이 있는지 확인합니다 `Services User` AEM Forms 서비스를 호출하는 데 필요합니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[사용자 관리자 API 빠른 시작](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[암호로 PDF 문서 암호화](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API를 사용하여 사용자 인증 {#authenticate-a-user-using-the-java-api}

Authentication Manager Service API(Java)를 사용하여 사용자 인증:

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-usermanager-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. AuthenticationManagerServices 클라이언트를 만듭니다.

   만들기 `AuthenticationManagerServiceClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.

1. 인증 작업을 호출합니다.

   를 호출합니다 `AuthenticationManagerServiceClient` 개체 `authenticate` 메서드를 사용하여 다음 값을 전달합니다.

   * A `java.lang.String` 사용자 이름이 포함된 객체입니다.
   * 바이트 배열(a `byte[]` 개체)를 포함합니다. 을 가져올 수 있습니다. `byte[]` 객체를 호출하여 `java.lang.String` 개체 `getBytes` 메서드를 사용합니다.

   인증 메서드는 `AuthResult` 인증된 사용자에 대한 정보가 포함된 개체입니다.

1. 인증 컨텍스트를 검색합니다.

   를 호출합니다 `ServiceClientFactory` 개체 `getContext` 메서드를 반환하는 메서드입니다. `Context` 개체.

   그런 다음 `Context` 개체 `initPrincipal` 메서드 및 전달 `AuthResult`.

### 웹 서비스 API를 사용하여 사용자 인증 {#authenticate-a-user-using-the-web-service-api}

인증 관리자 서비스 API(웹 서비스)를 사용하여 사용자 인증:

1. 프로젝트 파일을 포함합니다.

   * Authentication Manager WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다. (자세한 내용은 [Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding))
   * Microsoft .NET 클라이언트 어셈블리를 참조합니다. 자세한 내용은 [Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding))

1. AuthenticationManagerService 클라이언트를 만듭니다.

   만들기 `AuthenticationManagerServiceService` 프록시 클래스의 생성자를 사용하여 개체를 작성합니다.

1. 인증 작업을 호출합니다.

   를 호출합니다 `AuthenticationManagerServiceClient` 개체 `authenticate` 메서드를 사용하여 다음 값을 전달합니다.

   * A `string` 사용자 이름이 포함된 객체
   * 바이트 배열(a `byte[]` 개체)를 포함합니다. 을 가져올 수 있습니다. `byte[]` 개체 변환 `string` 에 대한 암호가 포함된 개체 `byte[]` 아래 예에 표시된 논리를 사용하여 배열합니다.
   * 반환된 값은 `AuthResult` 사용자 정보를 검색하는 데 사용할 수 있는 객체입니다. 아래 예에서는 사용자의 정보를 먼저 가져와서 검색합니다. `AuthResult` 개체 `authenticatedUser` 필드 및 그 후에 결과 가져오기 `User` 개체 `canonicalName` 및 `domainName` 필드.

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 프로그래밍 방식으로 사용자 동기화 {#programmatically-synchronizing-users}

사용자 관리 API를 사용하여 사용자를 프로그래밍 방식으로 동기화할 수 있습니다. 사용자를 동기화하면 사용자 리포지토리에 있는 사용자 데이터로 AEM Forms이 업데이트됩니다. 예를 들어 사용자 저장소에 새 사용자를 추가한다고 가정합니다. 동기화 작업을 수행하면 새 사용자가 AEM Forms 사용자가 됩니다. 또한 더 이상 사용자 지표에 없는 사용자는 AEM Forms에서 제거됩니다.

다음 다이어그램은 AEM Forms이 사용자 담당자와 동기화하는 것을 보여줍니다.

![ps_ps_umauth_sync](assets/ps_ps_umauth_sync.png)

다음 표에서는 이 다이어그램의 단계에 대해 설명합니다

<table>
 <thead>
  <tr>
   <th><p>단계</p></th>
   <th><p>설명</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>클라이언트 애플리케이션은 AEM Forms에서 동기화 작업을 수행하도록 요청합니다.</p></td>
  </tr>
  <tr>
   <td><p>2개</p></td>
   <td><p>AEM Forms에서 동기화 작업을 수행합니다.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>사용자 정보가 업데이트됩니다.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>사용자는 업데이트된 사용자 정보를 볼 수 있습니다. </p></td>
  </tr>
 </tbody>
</table>

### 단계 요약 {#summary_of_steps-6}

사용자를 프로그래밍 방식으로 동기화하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. UserManagerUtilServiceClient 클라이언트를 만듭니다.
1. 엔터프라이즈 도메인을 지정합니다.
1. 인증 작업을 호출합니다.
1. 동기화 작업이 완료되었는지 확인

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**UserManagerUtilServiceClientclient 만들기**

사용자를 프로그래밍 방식으로 동기화하려면 먼저 `UserManagerUtilServiceClient` 개체.

**엔터프라이즈 도메인 지정**

사용자 관리 API를 사용하여 동기화 작업을 수행하기 전에 사용자가 속한 엔터프라이즈 도메인을 지정합니다. 하나 이상의 엔터프라이즈 도메인을 지정할 수 있습니다. 동기화 작업을 프로그래밍 방식으로 수행하려면 먼저 관리 콘솔을 사용하여 엔터프라이즈 도메인을 설정해야 합니다. (자세한 내용은 [관리 도움말](https://www.adobe.com/go/learn_aemforms_admin_63))

**동기화 작업 호출**

하나 이상의 엔터프라이즈 도메인을 지정한 후 동기화 작업을 수행할 수 있습니다. 이 작업을 수행하는 데 걸리는 시간은 사용자 저장소에 있는 사용자 레코드 수에 따라 다릅니다.

**동기화 작업이 완료되었는지 확인**

동기화 작업을 프로그래밍 방식으로 수행한 후 작업이 완료되었는지 확인할 수 있습니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[사용자 관리자 API 빠른 시작](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[암호로 PDF 문서 암호화](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API를 사용하여 사용자를 프로그래밍 방식으로 동기화 {#programmatically-synchronizing-users-using-the-java-api}

사용자 관리 API(Java)를 사용하여 사용자를 동기화합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-usermanager-client.jar 및 adobe-usermanager-util-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. UserManagerUtilServiceClient 클라이언트를 만듭니다.

   만들기 `UserManagerUtilServiceClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.

1. 엔터프라이즈 도메인을 지정합니다.

   * 를 호출합니다 `UserManagerUtilServiceClient` 개체 `scheduleSynchronization` 사용자 동기화 작업을 시작하는 방법
   * 만들기 `java.util.Set` 인스턴스를 사용하여 `HashSet` 생성자입니다. 다음을 지정했는지 확인합니다 `String` 를 입력합니다. 이 `Java.util.Set` 인스턴스는 동기화 작업이 적용되는 도메인 이름을 저장합니다.
   * 추가할 각 도메인 이름에 대해 `java.util.Set` 개체의 add 메서드를 사용하여 도메인 이름을 전달합니다.

1. 동기화 작업을 호출합니다.

   를 호출합니다 `ServiceClientFactory` 개체 `getContext` 메서드를 반환하는 메서드입니다. `Context` 개체.

   그런 다음 `Context` 개체 `initPrincipal` 메서드 및 전달 `AuthResult`.

**추가 참조**

[프로그래밍 방식으로 사용자 동기화](users.md#programmatically-synchronizing-users)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
