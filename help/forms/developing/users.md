---
title: 사용자 관리
seo-title: 사용자 관리
description: 사용자 관리 API를 사용하여 역할, 권한 및 주체(사용자 또는 그룹이 될 수 있음)를 관리하고 사용자를 인증할 수 있는 클라이언트 애플리케이션을 만듭니다.
seo-description: 사용자 관리 API를 사용하여 역할, 권한 및 주체(사용자 또는 그룹이 될 수 있음)를 관리하고 사용자를 인증할 수 있는 클라이언트 애플리케이션을 만듭니다.
uuid: 68d8a0bc-6e3d-4286-ba5c-534dcf58cb84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 95804bff-9e6f-4807-aae4-790bd9e7cb57
role: 개발자
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '6258'
ht-degree: 0%

---


# 사용자 관리 {#managing-users}

**이 문서의 샘플과 예는 JEE 환경의 AEM Forms에만 해당됩니다.**

**사용자 관리 정보**

사용자 관리 API를 사용하여 역할, 권한 및 주체(사용자 또는 그룹이 될 수 있음)를 관리하고 사용자를 인증할 수 있는 클라이언트 애플리케이션을 만들 수 있습니다. 사용자 관리 API는 다음 AEM Forms API로 구성됩니다.

* 디렉토리 관리자 서비스 API
* 인증 관리자 서비스 API
* 인증 관리자 서비스 API

사용자 관리를 사용하여 역할 및 권한을 할당, 제거 및 결정할 수 있습니다. 도메인, 사용자 및 그룹을 할당, 제거 및 쿼리할 수도 있습니다. 마지막으로 사용자 관리를 사용하여 사용자를 인증할 수 있습니다.

[사용자 추가](users.md#adding-users)에서는 프로그래밍 방식으로 사용자를 추가하는 방법을 이해합니다. 이 섹션에서는 디렉토리 관리자 서비스 API를 사용합니다.

[사용자 삭제](users.md#deleting-users)에서는 사용자를 프로그래밍 방식으로 삭제하는 방법을 이해합니다. 이 섹션에서는 디렉토리 관리자 서비스 API를 사용합니다.

[사용자 및 그룹 관리](users.md#managing-users-and-groups)에서는 로컬 사용자와 디렉토리 사용자 간의 차이점을 파악하고 Java 및 웹 서비스 API를 사용하여 프로그래밍 방식으로 사용자 및 그룹을 관리하는 방법의 예를 확인할 수 있습니다. 이 섹션에서는 디렉토리 관리자 서비스 API를 사용합니다.

[역할 및 권한 관리](users.md#managing-roles-and-permissions)에서는 시스템 역할과 권한에 대해 알아보고, 역할을 늘리기 위해 프로그래밍 방식으로 수행할 수 있는 작업에 대해 알아보고, Java 및 웹 서비스 API를 사용하여 역할 및 권한을 프로그래밍 방식으로 관리하는 방법에 대한 예를 봅니다. 이 섹션에서는 Directory Manager 서비스 API와 Authorization Manager Service API를 모두 사용합니다.

[사용자 인증](users.md#authenticating-users)에서는 Java 및 웹 서비스 API를 사용하여 프로그래밍 방식으로 사용자를 인증하는 방법의 예를 볼 수 있습니다. 이 섹션에서는 인증 관리자 서비스 API를 사용합니다.

**인증 프로세스 이해**

사용자 관리는 내장된 인증 기능을 제공하며, 자체 인증 공급자와 연결할 수 있는 기능도 제공합니다. 사용자 관리에서 인증 요청을 받으면(예: 사용자가 로그인을 시도) 사용자 정보를 인증 공급자에 전달하여 인증합니다. 사용자 관리는 사용자를 인증한 후 인증 공급자의 결과를 받습니다.

다음 다이어그램은 로그인하려는 최종 사용자, 사용자 관리 및 인증 공급자 간의 상호 작용을 보여 줍니다.

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
   <td><p>사용자 관리는 사용자 이름 및 암호와 구성 정보를 인증 공급자에게 보냅니다.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>인증 공급자가 사용자 스토어에 연결하여 사용자를 인증합니다.</p></td>
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
>서버 시간대가 클라이언트 표준 시간대와 다른 경우 WebSphere Application Server 클러스터의 .NET 클라이언트를 사용하여 기본 SOAP 스택에서 AEM Forms Generate PDF 서비스를 사용하는 경우 다음 사용자 관리 인증 오류가 발생할 수 있습니다.

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**디렉토리 관리 이해**

사용자 관리는 LDAP 디렉토리 연결을 지원하는 디렉토리 서비스 공급자(DirectoryManagerService)와 함께 패키징됩니다. 조직에서 LDAP가 아닌 저장소를 사용하여 사용자 레코드를 저장하는 경우 리포지토리와 함께 작동하는 고유한 디렉토리 서비스 공급자를 생성할 수 있습니다.

디렉토리 서비스 공급자는 사용자 관리의 요청에 따라 사용자 저장소에서 레코드를 검색합니다. 사용자 관리는 정기적으로 데이터베이스의 사용자 및 그룹 레코드를 캐시하여 성능을 향상시킵니다.

디렉토리 서비스 공급자를 사용하여 사용자 관리 데이터베이스를 사용자 스토어와 동기화할 수 있습니다. 이 단계를 수행하면 모든 사용자 디렉토리 정보와 모든 사용자 및 그룹 레코드가 최신 상태가 됩니다.

또한 DirectoryManagerService는 도메인을 만들고 관리하는 기능을 제공합니다. 도메인은 서로 다른 사용자 기반을 정의합니다. 도메인의 경계는 일반적으로 조직의 구조 또는 사용자 스토어가 설정되는 방식에 따라 정의됩니다. 사용자 관리 도메인은 인증 공급자 및 디렉토리 서비스 공급자가 사용하는 구성 설정을 제공합니다.

사용자 관리가 내보내는 구성 XML에서 `Domains` 속성 값이 있는 루트 노드에는 사용자 관리를 위해 정의된 각 도메인에 대한 XML 요소가 포함되어 있습니다. 이러한 각 요소에는 특정 서비스 제공자와 관련된 도메인의 측면을 정의하는 다른 요소가 포함되어 있습니다.

**objectSID 값 이해**

Active Directory를 사용할 때는 `objectSID` 값이 여러 도메인의 고유한 특성이 아님을 이해하는 것이 중요합니다. 이 값은 개체의 보안 식별자를 저장합니다. 여러 도메인 환경(예: 도메인 트리)에서 `objectSID` 값은 다를 수 있습니다.

개체가 하나의 Active Directory 도메인에서 다른 도메인으로 이동되면 `objectSID` 값이 변경됩니다. 일부 개체는 도메인의 모든 위치에서 동일한 `objectSID` 값을 가집니다. 예를 들어 BUILTIN\Administrators, BUILTIN\Power Users 등과 같은 그룹은 도메인에 관계없이 동일한 `objectSID` 값을 가집니다. 이러한 `objectSID` 값은 잘 알려져 있습니다.

## 사용자 {#adding-users} 추가

Directory Manager Service API(Java 및 웹 서비스)를 사용하여 프로그래밍 방식으로 AEM Forms에 사용자를 추가할 수 있습니다. 사용자를 추가한 후 사용자를 필요로 하는 서비스 작업을 수행할 때 해당 사용자를 사용할 수 있습니다. 예를 들어 새 사용자에게 작업을 할당할 수 있습니다.

### {#summary-of-steps} 단계 요약

사용자를 추가하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. DirectoryManagerService 클라이언트를 만듭니다.
1. 사용자 정보를 정의합니다.
1. AEM Forms에 사용자를 추가합니다.
1. 사용자가 추가되었는지 확인합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

**DirectoryManagerService 클라이언트 만들기**

디렉터리 관리자 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 디렉터리 관리자 서비스 API 클라이언트를 만듭니다.

**사용자 정보 정의**

디렉토리 관리자 서비스 API를 사용하여 새 사용자를 추가하는 경우 해당 사용자에 대한 정보를 정의합니다. 일반적으로 새 사용자를 추가할 때 다음 값을 정의합니다.

* **도메인 이름**:사용자가 속한 도메인(예:  `DefaultDom`).
* **사용자 식별자 값**:사용자의 식별자 값(예:  `wblue`).
* **주체 유형**:사용자 유형(예: 지정할 수 있습니다 `USER)`.
* **지정된 이름**:사용자의 지정된 이름(예:  `Wendy`).
* **가족 이름**:사용자의 가족 이름(예:  `Blue)`.
* **로케일**:사용자의 로케일 정보.

**AEM Forms에 사용자 추가**

사용자 정보를 정의한 후 사용자를 AEM Forms에 추가할 수 있습니다. 사용자를 추가하려면 `DirectoryManagerServiceClient` 객체의 `createLocalUser` 메서드를 호출합니다.

**사용자가 추가되었는지 확인**

문제가 발생하지 않도록 사용자가 추가되었는지 확인할 수 있습니다. 사용자 식별자 값을 사용하여 새 사용자를 찾습니다.

**참고 항목**

[Java API를 사용하여 사용자 추가](users.md#add-users-using-the-java-api)

[웹 서비스 API를 사용하여 사용자 추가](users.md#add-users-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[사용자 삭제](users.md#deleting-users)

### Java API {#add-users-using-the-java-api}을 사용하여 사용자 추가

Directory Manager 서비스 API(Java)를 사용하여 사용자를 추가합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-usermanager-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. DirectoryManagerServices 클라이언트를 만듭니다.

   해당 생성자를 사용하고 연결 속성이 포함된 `ServiceClientFactory` 객체를 전달하여 `DirectoryManagerServiceClient` 객체를 만듭니다.

1. 사용자 정보를 정의합니다.

   * 생성자를 사용하여 `UserImpl` 객체를 만듭니다.
   * `UserImpl` 개체의 `setDomainName` 메서드를 호출하여 demain 이름을 설정합니다. 도메인 이름을 지정하는 문자열 값을 전달합니다.
   * `UserImpl` 객체의 `setPrincipalType` 메서드를 호출하여 주체 유형을 설정합니다. 사용자 유형을 지정하는 문자열 값을 전달합니다. 예를 들어 `USER`을(를) 지정할 수 있습니다.
   * `UserImpl` 개체의 `setUserid` 메서드를 호출하여 사용자 식별자 값을 설정합니다. 사용자 식별자 값을 지정하는 문자열 값을 전달합니다. 예를 들어 `wblue`을(를) 지정할 수 있습니다.
   * `UserImpl` 개체의 `setCanonicalName` 메서드를 호출하여 정식 이름을 설정합니다. 사용자의 정식 이름을 지정하는 문자열 값을 전달합니다. 예를 들어 `wblue`을(를) 지정할 수 있습니다.
   * `UserImpl` 객체의 `setGivenName` 메서드를 호출하여 지정된 이름을 설정합니다. 사용자의 지정된 이름을 지정하는 문자열 값을 전달합니다. 예를 들어 `Wendy`을(를) 지정할 수 있습니다.
   * `UserImpl` 객체의 `setFamilyName` 메서드를 호출하여 패밀리 이름을 설정합니다. 사용자의 가족 이름을 지정하는 문자열 값을 전달합니다. 예를 들어 `Blue`을(를) 지정할 수 있습니다.

   >[!NOTE]
   >
   >`UserImpl` 개체에 속하는 메서드를 호출하여 다른 값을 설정합니다. 예를 들어 `UserImpl` 객체의 `setLocale` 메서드를 호출하여 로케일 값을 설정할 수 있습니다.

1. AEM Forms에 사용자를 추가합니다.

   `DirectoryManagerServiceClient` 객체의 `createLocalUser` 메서드를 호출하고 다음 값을 전달합니다.

   * 새 사용자를 나타내는 `UserImpl` 개체
   * 사용자의 암호를 나타내는 문자열 값

   `createLocalUser` 메서드는 로컬 사용자 식별자 값을 지정하는 문자열 값을 반환합니다.

1. 사용자가 추가되었는지 확인합니다.

   * 생성자를 사용하여 `PrincipalSearchFilter` 객체를 만듭니다.
   * `PrincipalSearchFilter` 개체의 `setUserId` 메서드를 호출하여 사용자 식별자 값을 설정합니다. 사용자 식별자 값을 나타내는 문자열 값을 전달합니다.
   * `DirectoryManagerServiceClient` 객체의 `findPrincipals` 메서드를 호출하고 `PrincipalSearchFilter` 객체를 전달합니다. 이 메서드는 `java.util.List` 인스턴스를 반환합니다. 여기서 각 요소는 `User` 개체입니다. `java.util.List` 인스턴스를 반복하여 사용자를 찾습니다.

**참고 항목**

[단계 요약](users.md#summary-of-steps)

[빠른 시작(SOAP 모드):Java API를 사용하여 사용자 추가](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#add-users-using-the-web-service-api}를 사용하여 사용자 추가

Directory Manager Service API(웹 서비스)를 사용하여 사용자를 추가합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 서비스 참조에 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. DirectoryManagerService 클라이언트를 만듭니다.

   * 기본 생성자를 사용하여 `DirectoryManagerServiceClient` 객체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `DirectoryManagerServiceClient.Endpoint.Address` 객체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스(예: `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`)에 전달합니다. `lc_version` 특성을 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. `?blob=mtom`을(를) 지정해야 합니다.
   * `DirectoryManagerServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`으로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM 양식 사용자 이름을 `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `DirectoryManagerServiceClient.ClientCredentials.UserName.Password` 필드에 지정합니다.
      * `BasicHttpBindingSecurity.Transport.ClientCredentialType` 필드에 상수 값 `HttpClientCredentialType.Basic`을 할당합니다.
      * `BasicHttpBindingSecurity.Security.Mode` 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 할당합니다.

1. 사용자 정보를 정의합니다.

   * 생성자를 사용하여 `UserImpl` 객체를 만듭니다.
   * 문자열 값을 `UserImpl` 객체의 `domainName` 필드에 할당하여 demain 이름을 설정합니다.
   * `UserImpl` 개체의 `principalType` 필드에 문자열 값을 할당하여 주체 유형을 설정합니다. 예를 들어 `USER`을(를) 지정할 수 있습니다.
   * 문자열 값을 `UserImpl` 개체의 `userid` 필드에 할당하여 사용자 식별자 값을 설정합니다.
   * 문자열 값을 `UserImpl` 개체의 `canonicalName` 필드에 할당하여 표준 이름 값을 설정합니다.
   * 문자열 값을 `UserImpl` 객체의 `givenName` 필드에 할당하여 지정된 이름 값을 설정합니다.
   * 문자열 값을 `UserImpl` 객체의 `familyName` 필드에 할당하여 패밀리 이름 값을 설정합니다.

1. AEM Forms에 사용자를 추가합니다.

   `DirectoryManagerServiceClient` 객체의 `createLocalUser` 메서드를 호출하고 다음 값을 전달합니다.

   * 새 사용자를 나타내는 `UserImpl` 개체
   * 사용자의 암호를 나타내는 문자열 값

   `createLocalUser` 메서드는 로컬 사용자 식별자 값을 지정하는 문자열 값을 반환합니다.

1. 사용자가 추가되었는지 확인합니다.

   * 생성자를 사용하여 `PrincipalSearchFilter` 객체를 만듭니다.
   * 사용자 식별자 값을 나타내는 문자열 값을 `PrincipalSearchFilter` 개체의 `userId` 필드에 할당하여 사용자의 사용자 식별자 값을 설정합니다.
   * `DirectoryManagerServiceClient` 객체의 `findPrincipals` 메서드를 호출하고 `PrincipalSearchFilter` 객체를 전달합니다. 이 메서드는 `MyArrayOfUser` 컬렉션 개체를 반환합니다. 여기서 각 요소는 `User` 개체입니다. `MyArrayOfUser` 컬렉션을 반복하여 사용자를 찾습니다.

**참고 항목**

[단계 요약](users.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 사용자 {#deleting-users} 삭제

Directory Manager Service API(Java 및 웹 서비스)를 사용하여 프로그래밍 방식으로 AEM Forms에서 사용자를 삭제할 수 있습니다. 사용자를 삭제하면 사용자가 필요한 서비스 작업을 수행하는 데 더 이상 사용자를 사용할 수 없습니다. 예를 들어, 삭제된 사용자에게 작업을 할당할 수는 없습니다.

### {#summary_of_steps-1} 단계 요약

사용자를 삭제하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. DirectoryManagerService 클라이언트를 만듭니다.
1. 삭제할 사용자를 지정합니다.
1. AEM Forms에서 사용자를 삭제합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

**DirectoryManagerService 클라이언트 만들기**

디렉터리 관리자 서비스 API 작업을 프로그래밍 방식으로 수행하려면 먼저 디렉터리 관리자 서비스 클라이언트를 만듭니다.

**삭제할 사용자 지정**

사용자의 식별자 값을 사용하여 삭제할 사용자를 지정할 수 있습니다.

**AEM Forms에서 사용자 삭제**

사용자를 삭제하려면 `DirectoryManagerServiceClient` 객체의 `deleteLocalUser` 메서드를 호출합니다.

**참고 항목**

[Java API를 사용하여 사용자 삭제](users.md#delete-users-using-the-java-api)

[웹 서비스 API를 사용하여 사용자 삭제](users.md#delete-users-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[사용자 추가](users.md#adding-users)

### Java API {#delete-users-using-the-java-api}을 사용하여 사용자 삭제

Directory Manager 서비스 API(Java)를 사용하여 사용자를 삭제합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-usermanager-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. DirectoryManagerService 클라이언트를 만듭니다.

   해당 생성자를 사용하고 연결 속성이 포함된 `ServiceClientFactory` 객체를 전달하여 `DirectoryManagerServiceClient` 객체를 만듭니다.

1. 삭제할 사용자를 지정합니다.

   * 생성자를 사용하여 `PrincipalSearchFilter` 객체를 만듭니다.
   * `PrincipalSearchFilter` 개체의 `setUserId` 메서드를 호출하여 사용자 식별자 값을 설정합니다. 사용자 식별자 값을 나타내는 문자열 값을 전달합니다.
   * `DirectoryManagerServiceClient` 객체의 `findPrincipals` 메서드를 호출하고 `PrincipalSearchFilter` 객체를 전달합니다. 이 메서드는 `java.util.List` 인스턴스를 반환합니다. 여기서 각 요소는 `User` 개체입니다. `java.util.List` 인스턴스를 반복하여 삭제할 사용자를 찾습니다.

1. AEM Forms에서 사용자를 삭제합니다.

   `DirectoryManagerServiceClient` 객체의 `deleteLocalUser` 메서드를 호출하고 `User` 객체의 `oid` 필드의 값을 전달합니다. `User` 객체의 `getOid` 메서드를 호출합니다. `java.util.List` 인스턴스에서 검색된 `User` 개체를 사용합니다.

**참고 항목**

[단계 요약](users.md#summary-of-steps)

[빠른 시작(EJB 모드):Java API를 사용하여 사용자 삭제](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 사용자 삭제](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#delete-users-using-the-web-service-api}를 사용하여 사용자 삭제

Directory Manager Service API(웹 서비스)를 사용하여 사용자를 삭제합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-usermanager-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. DirectoryManagerService 클라이언트를 만듭니다.

   * 기본 생성자를 사용하여 `DirectoryManagerServiceClient` 객체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `DirectoryManagerServiceClient.Endpoint.Address` 객체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스(예: `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`)에 전달합니다. `lc_version` 특성을 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. `blob=mtom.`을(를) 지정해야 합니다.
   * `DirectoryManagerServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`으로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM 양식 사용자 이름을 `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `DirectoryManagerServiceClient.ClientCredentials.UserName.Password` 필드에 지정합니다.
      * `BasicHttpBindingSecurity.Transport.ClientCredentialType` 필드에 상수 값 `HttpClientCredentialType.Basic`을 할당합니다.
      * `BasicHttpBindingSecurity.Security.Mode` 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 할당합니다.

1. 삭제할 사용자를 지정합니다.

   * 생성자를 사용하여 `PrincipalSearchFilter` 객체를 만듭니다.
   * 문자열 값을 `PrincipalSearchFilter` 개체의 `userId` 필드에 할당하여 사용자 식별자 값을 설정합니다.
   * `DirectoryManagerServiceClient` 객체의 `findPrincipals` 메서드를 호출하고 `PrincipalSearchFilter` 객체를 전달합니다. 이 메서드는 `MyArrayOfUser` 컬렉션 개체를 반환합니다. 여기서 각 요소는 `User` 개체입니다. `MyArrayOfUser` 컬렉션을 반복하여 사용자를 찾습니다. `MyArrayOfUser` 컬렉션 개체에서 검색된 `User` 개체는 사용자를 삭제하는 데 사용됩니다.

1. AEM Forms에서 사용자를 삭제합니다.

   `User` 개체의 `oid` 필드 값을 `DirectoryManagerServiceClient` 개체의 `deleteLocalUser` 메서드에 전달하여 사용자를 삭제합니다.

**참고 항목**

[단계 요약](users.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 그룹 만들기 {#creating-groups}

Directory Manager Service API(Java 및 웹 서비스)를 사용하여 프로그래밍 방식으로 AEM Forms 그룹을 만들 수 있습니다. 그룹을 만든 후 해당 그룹을 사용하여 그룹이 필요한 서비스 작업을 수행할 수 있습니다. 예를 들어 새 그룹에 사용자를 할당할 수 있습니다. ([사용자 및 그룹 관리](users.md#managing-users-and-groups)를 참조하십시오.)

### {#summary_of_steps-2} 단계 요약

그룹을 만들려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. DirectoryManagerService 클라이언트를 만듭니다.
1. 그룹이 존재하지 않는지 확인합니다.
1. 그룹을 만듭니다.
1. 그룹으로 작업을 수행합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**DirectoryManagerService 클라이언트 만들기**

디렉터리 관리자 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 디렉터리 관리자 서비스 API 클라이언트를 만듭니다.

**그룹이 있는지 여부 확인**

그룹을 만들 때 그룹이 동일한 도메인에 존재하지 않는지 확인합니다. 즉, 동일한 도메인 내에 동일한 이름을 둘 수 없습니다. 이 작업을 수행하려면 검색을 수행하고 두 값을 기준으로 검색 결과를 필터링합니다. 그룹만 반환되도록 하려면 주체 유형을 `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`으로 설정합니다. 또한 도메인 이름을 지정해야 합니다.

**그룹 만들기**

그룹이 도메인에 존재하지 않는다고 결정하면 그룹을 만들고 다음 특성을 지정합니다.

* **일반 이름**:그룹 이름입니다.
* **도메인**:그룹이 추가되는 도메인입니다.
* **설명**:그룹에 대한 설명입니다.

**그룹으로 작업 수행**

그룹을 만든 후 그룹을 사용하여 작업을 수행할 수 있습니다. 예를 들어 그룹에 사용자를 추가할 수 있습니다. 사용자를 그룹에 추가하려면 사용자와 그룹 모두의 고유 식별자 값을 검색합니다. 이러한 값을 `addPrincipalToLocalGroup` 메서드에 전달합니다.

**참고 항목**

[Java API를 사용하여 그룹 만들기](users.md#create-groups-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[사용자 추가](users.md#adding-users)

[사용자 삭제](users.md#deleting-users)

### Java API {#create-groups-using-the-java-api}을 사용하여 그룹 만들기

Directory Manager 서비스 API(Java)를 사용하여 그룹을 만듭니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-usermanager-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. DirectoryManagerService 클라이언트를 만듭니다.

   해당 생성자를 사용하고 연결 속성이 포함된 `ServiceClientFactory` 객체를 전달하여 `DirectoryManagerServiceClient` 객체를 만듭니다.

1. 그룹이 있는지 확인합니다.

   * 생성자를 사용하여 `PrincipalSearchFilter` 객체를 만듭니다.
   * `PrincipalSearchFilter` 개체의 `setPrincipalType` 개체를 호출하여 주체 유형을 설정합니다. `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` 값을 전달합니다.
   * `PrincipalSearchFilter` 개체의 `setSpecificDomainName` 개체를 호출하여 도메인을 설정합니다. 도메인 이름을 지정하는 문자열 값을 전달합니다.
   * 그룹을 찾으려면 `DirectoryManagerServiceClient` 객체의 `findPrincipals` 메서드를 호출합니다. 주체 유형 및 도메인 이름을 지정하는 `PrincipalSearchFilter` 개체를 전달합니다. 이 메서드는 각 요소가 `Group` 인스턴스인 `java.util.List` 인스턴스를 반환합니다. 각 그룹 인스턴스는 `PrincipalSearchFilter` 개체를 사용하여 지정한 필터를 따릅니다.
   * `java.util.List` 인스턴스를 반복합니다. 각 요소에 대해 그룹 이름을 검색합니다. 그룹 이름이 새 그룹 이름과 같지 않은지 확인합니다.

1. 그룹을 만듭니다.

   * 그룹이 없으면 `Group` 객체의 `setCommonName` 메서드를 호출하고 그룹 이름을 지정하는 문자열 값을 전달합니다.
   * `Group` 객체의 `setDescription` 메서드를 호출하고 그룹 설명을 지정하는 문자열 값을 전달합니다.
   * `Group` 객체의 `setDomainName` 메서드를 호출하고 도메인 이름을 지정하는 문자열 값을 전달합니다.
   * `DirectoryManagerServiceClient` 객체의 `createLocalGroup` 메서드를 호출하고 `Group` 인스턴스를 전달합니다.

   `createLocalUser` 메서드는 로컬 사용자 식별자 값을 지정하는 문자열 값을 반환합니다.

1. 그룹으로 작업을 수행합니다.

   * 생성자를 사용하여 `PrincipalSearchFilter` 객체를 만듭니다.
   * `PrincipalSearchFilter` 개체의 `setUserId` 메서드를 호출하여 사용자 식별자 값을 설정합니다. 사용자 식별자 값을 나타내는 문자열 값을 전달합니다.
   * `DirectoryManagerServiceClient` 객체의 `findPrincipals` 메서드를 호출하고 `PrincipalSearchFilter` 객체를 전달합니다. 이 메서드는 `java.util.List` 인스턴스를 반환합니다. 여기서 각 요소는 `User` 개체입니다. `java.util.List` 인스턴스를 반복하여 사용자를 찾습니다.
   * `DirectoryManagerServiceClient` 개체의 `addPrincipalToLocalGroup` 메서드를 호출하여 사용자를 그룹에 추가합니다. `User` 개체의 `getOid` 메서드의 반환 값을 전달합니다. `Group` 개체의 `getOid` 메서드의 반환 값을 전달합니다(새 그룹을 나타내는 `Group` 인스턴스 사용).

**참고 항목**

[단계 요약](users.md#summary-of-steps)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 사용자 및 그룹 관리 {#managing-users-and-groups}

이 항목에서는 도메인, 사용자 및 그룹을 프로그래밍 방식으로 할당, 제거 및 쿼리하는 데 (Java)를 사용할 수 있는 방법에 대해 설명합니다.

>[!NOTE]
>
>도메인을 구성할 때 그룹과 사용자의 고유 식별자를 설정해야 합니다. 선택한 속성은 LDAP 환경 내에서 고유해야 할 뿐만 아니라 변경할 수 없으며 디렉토리 내에서 변경되지 않습니다. 이 속성은 단순 문자열 데이터 유형이어야 합니다. 현재 Active Directory 2000/2003에 대해 허용되는 유일한 예외는 이진 값인 `"objectsid"`입니다. 예를 들어 Novell eDirectory 속성 `"GUID"`은(는) 단순 문자열 데이터 유형이 아니므로 작동하지 않습니다.

* Active Directory의 경우 `"objectsid"`을(를) 사용합니다.
* SunOne의 경우 `"nsuniqueid"`을 사용합니다.

>[!NOTE]
>
>LDAP 디렉토리 동기화가 진행 중일 때 여러 로컬 사용자 및 그룹을 만들 수 없습니다. 이 프로세스를 시도하면 오류가 발생할 수 있습니다.

### {#summary_of_steps-3} 단계 요약

사용자 및 그룹을 관리하려면 다음 단계를 수행합니다.

1. 프로젝트 파일 포함
1. DirectoryManagerService 클라이언트를 만듭니다.
1. 해당 사용자 또는 그룹 작업을 호출합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**DirectoryManagerService 클라이언트 만들기**

디렉터리 관리자 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 디렉터리 관리자 서비스 클라이언트를 만들어야 합니다. Java API를 사용하면 `DirectoryManagerServiceClient` 개체를 만들어 이러한 작업을 수행할 수 있습니다. 웹 서비스 API를 사용하면 `DirectoryManagerServiceService` 개체를 만들어 이 작업을 수행할 수 있습니다.

**해당 사용자 또는 그룹 작업을 호출합니다.**

서비스 클라이언트를 만들었으면 사용자 또는 그룹 관리 작업을 호출할 수 있습니다. 서비스 클라이언트를 사용하여 도메인, 사용자 및 그룹을 할당, 제거 및 쿼리할 수 있습니다. 로컬 그룹에 디렉토리 주체와 로컬 주체를 추가할 수는 있지만 로컬 주체를 디렉토리 그룹에 추가할 수는 없습니다.

**참고 항목**

[Java API를 사용하여 사용자 및 그룹 관리](users.md#managing-users-and-groups-using-the-java-api)

[웹 서비스 API를 사용하여 사용자 및 그룹 관리](users.md#managing-users-and-groups-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[사용자 관리자 API 빠른 시작](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Java API {#managing-users-and-groups-using-the-java-api}을 사용하여 사용자 및 그룹 관리

(Java)를 사용하여 사용자, 그룹 및 도메인을 프로그래밍 방식으로 관리하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-usermanager-client.jar 등의 클라이언트 JAR 파일을 포함합니다. 이러한 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

1. DirectoryManagerService 클라이언트를 만듭니다.

   해당 생성자를 사용하고 연결 속성이 포함된 `ServiceClientFactory` 객체를 전달하여 `DirectoryManagerServiceClient` 객체를 만듭니다. 자세한 내용은 [연결 속성 설정&#x200B;](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*.*&#x200B;을 참조하십시오.

1. 해당 사용자 또는 그룹 작업을 호출합니다.

   사용자 또는 그룹을 찾으려면 `DirectoryManagerServiceClient` 개체의 주체 찾기 메서드 중 하나를 호출합니다. 아래 예에서 검색 필터(`PrincipalSearchFilter` 개체)를 사용하여 `findPrincipals` 메서드를 호출합니다.

   이 경우 반환 값이 `Principal` 개체를 포함하는 `java.util.List`이므로 결과를 반복하여 `Principal` 개체를 `User` 또는 `Group` 개체 중 하나로 캐스팅합니다.

   결과 `User` 또는 `Group` 개체(둘 다 `Principal` 인터페이스에서 상속)를 사용하여 워크플로우에서 필요한 정보를 검색합니다. 예를 들어 도메인 이름과 표준 이름 값을 조합하여 주체를 고유하게 식별합니다. 이러한 메서드는 각각 `Principal` 객체의 `getDomainName` 및 `getCanonicalName` 메서드를 호출하여 검색합니다.

   로컬 사용자를 삭제하려면 `DirectoryManagerServiceClient` 객체의 `deleteLocalUser` 메서드를 호출하고 사용자 식별자를 전달합니다.

   로컬 그룹을 삭제하려면 `DirectoryManagerServiceClient` 객체의 `deleteLocalGroup` 메서드를 호출하고 그룹의 식별자를 전달합니다.

**참고 항목**

[단계 요약](users.md#summary-of-steps)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#managing-users-and-groups-using-the-web-service-api}를 사용하여 사용자 및 그룹 관리

디렉토리 관리자 서비스 API(웹 서비스)를 사용하여 사용자, 그룹 및 도메인을 프로그래밍 방식으로 관리하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함

   * Directory Manager WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다. (Base64 인코딩](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)을 사용하여 AEM Forms 호출 참조)[
   * Microsoft .NET 클라이언트 어셈블리를 참조하십시오. (Base64 인코딩](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)을 사용하는 .NET 클라이언트 어셈블리 만들기를 참조하십시오.)[

1. DirectoryManagerService 클라이언트를 만듭니다.

   프록시 클래스의 생성자를 사용하여 `DirectoryManagerServiceService` 개체를 만듭니다.

1. 해당 사용자 또는 그룹 작업을 호출합니다.

   사용자 또는 그룹을 찾으려면 `DirectoryManagerServiceService` 개체의 주체 찾기 메서드 중 하나를 호출합니다. 아래 예에서 검색 필터(`PrincipalSearchFilter` 개체)를 사용하여 `findPrincipalsWithFilter` 메서드를 호출합니다. `PrincipalSearchFilter` 개체를 사용할 때 로컬 주체는 `isLocal` 속성이 `true`로 설정된 경우에만 반환됩니다. 이 동작은 Java API에서 발생하는 동작과 다릅니다.

   >[!NOTE]
   >
   >검색 필터(`PrincipalSearchFilter.resultsMax` 필드를 통해)에 최대 결과 수가 지정되지 않으면 최대 1000개의 결과가 반환됩니다. 이 동작은 10개의 결과가 기본 최대값인 Java API를 사용하여 발생하는 동작과 다릅니다. 또한 검색 필터에서 최대 결과 수를 지정하지 않으면 `findGroupMembers`과 같은 검색 메서드는 결과를 산출하지 않습니다(예: `GroupMembershipSearchFilter.resultsMax` 필드를 통해). 이것은 `GenericSearchFilter` 클래스에서 상속되는 모든 검색 필터에 적용됩니다. 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)를 참조하십시오.

   이 경우 반환 값이 `Principal` 개체를 포함하는 `object[]`이므로 결과를 반복하여 `Principal` 개체를 `User` 또는 `Group` 개체 중 하나로 캐스팅합니다.

   결과 `User` 또는 `Group` 개체(둘 다 `Principal` 인터페이스에서 상속)를 사용하여 워크플로우에서 필요한 정보를 검색합니다. 예를 들어 도메인 이름과 표준 이름 값을 조합하여 주체를 고유하게 식별합니다. 이러한 항목은 각각 `Principal` 객체의 `domainName` 및 `canonicalName` 필드를 호출하여 검색합니다.

   로컬 사용자를 삭제하려면 `DirectoryManagerServiceService` 객체의 `deleteLocalUser` 메서드를 호출하고 사용자 식별자를 전달합니다.

   로컬 그룹을 삭제하려면 `DirectoryManagerServiceService` 객체의 `deleteLocalGroup` 메서드를 호출하고 그룹의 식별자를 전달합니다.

**참고 항목**

[단계 요약](users.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 역할 및 권한 관리 {#managing-roles-and-permissions}

이 항목에서는 Authorization Manager Service API(Java)를 사용하여 역할 및 권한을 프로그래밍 방식으로 할당, 제거 및 결정하는 방법에 대해 설명합니다.

AEM Forms에서 *역할*&#x200B;은 하나 이상의 시스템 수준 리소스에 액세스하기 위한 권한 그룹입니다. 이러한 권한은 사용자 관리를 통해 만들어지며 서비스 구성 요소에 의해 적용됩니다. 예를 들어, 관리자는 사용자 그룹에 &quot;정책 집합 작성자&quot;의 역할을 할당할 수 있습니다. 그런 다음 Rights Management은 해당 역할의 해당 그룹의 사용자가 관리 콘솔을 통해 정책 세트를 만들 수 있도록 허용합니다.

두 가지 유형의 역할이 있습니다.*기본 역할* 및 *사용자 지정 역할*. 기본 역할(*시스템 역할)*&#x200B;이(가) AEM Forms에 이미 있습니다. 관리자가 기본 역할을 삭제하거나 수정할 수 없으므로 변경할 수 없다고 가정합니다. 이후에 수정하거나 삭제할 수 있는 관리자가 만든 사용자 지정 역할은 변경할 수 있습니다.

역할을 사용하면 권한을 손쉽게 관리할 수 있습니다. 역할에 주체가 할당되면 권한 집합이 자동으로 해당 주체에 할당되고 주체에 대한 모든 특정 액세스 관련 결정은 할당된 전체 권한 집합을 기반으로 합니다.

### {#summary_of_steps-4} 단계 요약

역할 및 권한을 관리하려면 다음 단계를 수행합니다.

1. 프로젝트 파일 포함
1. AuthorizationManagerService 클라이언트를 만듭니다.
1. 적절한 역할 또는 권한 작업을 호출합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**AuthorizationManagerService 클라이언트 만들기**

사용자 관리 AuthorizationManagerService 작업을 프로그래밍 방식으로 수행하려면 먼저 AuthorizationManagerService 클라이언트를 만들어야 합니다. Java API를 사용하면 `AuthorizationManagerServiceClient` 개체를 만들어 이러한 작업을 수행할 수 있습니다.

**적절한 역할 또는 권한 작업을 호출합니다.**

서비스 클라이언트를 만들었으면 역할이나 권한 작업을 호출할 수 있습니다. 서비스 클라이언트를 사용하여 역할 및 권한을 할당, 제거 및 결정할 수 있습니다.

**참고 항목**

[Java API를 사용하여 역할 및 권한 관리](users.md#managing-roles-and-permissions-using-the-java-api)

[웹 서비스 API를 사용하여 역할 및 권한 관리](users.md#managing-roles-and-permissions-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[사용자 관리자 API 빠른 시작](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Java API {#managing-roles-and-permissions-using-the-java-api}을(를) 사용하여 역할 및 권한 관리

Authorization Manager Service API(Java)를 사용하여 역할 및 권한을 관리하려면 다음 작업을 수행합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-usermanager-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. AuthorizationManagerService 클라이언트를 만듭니다.

   해당 생성자를 사용하고 연결 속성이 포함된 `ServiceClientFactory` 객체를 전달하여 `AuthorizationManagerServiceClient` 객체를 만듭니다.

1. 적절한 역할 또는 권한 작업을 호출합니다.

   주체에 역할을 할당하려면 `AuthorizationManagerServiceClient` 객체의 `assignRole` 메서드를 호출하고 다음 값을 전달합니다.

   * 역할 식별자를 포함하는 `java.lang.String` 개체
   * 주체 식별자를 포함하는 `java.lang.String` 개체의 배열입니다.

   주체에서 역할을 제거하려면 `AuthorizationManagerServiceClient` 객체의 `unassignRole` 메서드를 호출하고 다음 값을 전달합니다.

   * 역할 식별자를 포함하는 `java.lang.String` 개체
   * 주체 식별자를 포함하는 `java.lang.String` 개체의 배열입니다.


**참고 항목**

[단계 요약](users.md#summary-of-steps)

[빠른 시작(SOAP 모드):Java API를 사용하여 역할 및 권한 관리](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#managing-roles-and-permissions-using-the-web-service-api}을(를) 사용하여 역할 및 권한 관리

Authorization Manager Service API(웹 서비스)를 사용하여 역할 및 권한을 관리합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. AuthorizationManagerService 클라이언트를 만듭니다.

   * 기본 생성자를 사용하여 `AuthorizationManagerServiceClient` 객체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `AuthorizationManagerServiceClient.Endpoint.Address` 객체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`). `lc_version` 특성을 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.
   * `AuthorizationManagerServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`으로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM 양식 사용자 이름을 `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password` 필드에 지정합니다.
      * `BasicHttpBindingSecurity.Transport.ClientCredentialType` 필드에 상수 값 `HttpClientCredentialType.Basic`을 할당합니다.
      * `BasicHttpBindingSecurity.Security.Mode` 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 할당합니다.

1. 적절한 역할 또는 권한 작업을 호출합니다.

   주체에 역할을 할당하려면 `AuthorizationManagerServiceClient` 객체의 `assignRole` 메서드를 호출하고 다음 값을 전달합니다.

   * 역할 식별자를 포함하는 `string` 개체
   * 주체 식별자를 포함하는 `MyArrayOf_xsd_string` 객체입니다.

   주체에서 역할을 제거하려면 `AuthorizationManagerServiceService` 객체의 `unassignRole` 메서드를 호출하고 다음 값을 전달합니다.

   * 역할 식별자를 포함하는 `string` 개체
   * 주체 식별자를 포함하는 `string` 개체의 배열입니다.


**참고 항목**

[단계 요약](users.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 사용자 인증 {#authenticating-users}

이 항목에서는 클라이언트 응용 프로그램이 프로그래밍 방식으로 사용자를 인증할 수 있도록 Authentication Manager Service API(Java)를 사용하는 방법에 대해 설명합니다.

보안 데이터를 저장하는 엔터프라이즈 데이터베이스 또는 다른 엔터프라이즈 리포지토리와 상호 작용하려면 사용자 인증이 필요할 수 있습니다.

예를 들어 사용자가 웹 페이지에 사용자 이름과 암호를 입력하고 해당 값을 Forms을 호스팅하는 J2EE 응용 프로그램 서버에 제출하는 시나리오를 가정해 보십시오. Forms 사용자 정의 응용 프로그램은 인증 관리자 서비스로 사용자를 인증할 수 있습니다.

인증이 성공하면 응용 프로그램에서 보안 엔터프라이즈 데이터베이스에 액세스합니다. 그렇지 않으면 사용자가 권한이 있는 사용자가 아니라는 메시지가 사용자에게 전송됩니다.

다음 다이어그램은 응용 프로그램의 논리 흐름을 보여줍니다.

![au_au_umauth_process](assets/au_au_umauth_process.png)

다음 표에서는 이 다이어그램의 단계를 설명합니다.

<table>
 <thead>
  <tr>
   <th><p>단계</p></th>
   <th><p>설명</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>3</p></td>
   <td><p>사용자가 웹 사이트에 액세스하고 사용자 이름과 암호를 지정합니다. 이 정보는 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 제출됩니다.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>사용자 자격 증명이 인증 관리자 서비스로 인증됩니다. 사용자 자격 증명이 유효하면 워크플로우가 3단계로 진행됩니다. 그렇지 않으면 사용자가 권한이 있는 사용자가 아니라는 메시지가 사용자에게 전송됩니다.</p></td>
  </tr>
  <tr>
   <td><p>1</p></td>
   <td><p>사용자 정보와 양식 디자인이 보안 엔터프라이즈 데이터베이스에서 검색됩니다. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>사용자 정보는 양식 디자인과 병합되고 양식은 사용자에게 렌더링됩니다. </p></td>
  </tr>
 </tbody>
</table>

### {#summary_of_steps-5} 단계 요약

사용자를 프로그래밍 방식으로 인증하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. AuthenticationManagerService 클라이언트를 만듭니다.
1. 인증 작업을 호출합니다.
1. 필요한 경우 클라이언트 응용 프로그램이 인증을 위해 다른 AEM Forms 서비스로 전달하도록 컨텍스트를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**AuthenticationManagerService 클라이언트 만들기**

프로그래밍 방식으로 사용자를 인증할 수 있으려면 먼저 AuthenticationManagerService 클라이언트를 만들어야 합니다. Java API를 사용할 때 `AuthenticationManagerServiceClient` 개체를 만듭니다.

**인증 작업 호출**

서비스 클라이언트를 만들었으면 인증 작업을 호출할 수 있습니다. 이 작업에는 사용자의 이름 및 암호와 같은 사용자에 대한 정보가 필요합니다. 사용자가 인증하지 않으면 예외가 발생합니다.

**인증 컨텍스트 검색**

사용자를 인증한 후에는 인증된 사용자를 기반으로 컨텍스트를 만들 수 있습니다. 그런 다음 컨텐츠를 사용하여 다른 AEM Forms 서비스를 호출할 수 있습니다. 예를 들어 컨텍스트를 사용하여 `EncryptionServiceClient`을 만들고 암호로 PDF 문서를 암호화할 수 있습니다. 인증된 사용자가 AEM Forms 서비스를 호출하는 데 필요한 `Services User` 역할을 가지고 있는지 확인합니다.

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[사용자 관리자 API 빠른 시작](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[암호로 PDF 문서 암호화](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API {#authenticate-a-user-using-the-java-api}를 사용하여 사용자 인증

인증 관리자 서비스 API(Java)를 사용하여 사용자 인증:

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-usermanager-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. AuthenticationManagerServices 클라이언트를 만듭니다.

   해당 생성자를 사용하고 연결 속성이 포함된 `ServiceClientFactory` 객체를 전달하여 `AuthenticationManagerServiceClient` 객체를 만듭니다.

1. 인증 작업을 호출합니다.

   `AuthenticationManagerServiceClient` 객체의 `authenticate` 메서드를 호출하고 다음 값을 전달합니다.

   * 사용자 이름이 포함된 `java.lang.String` 객체입니다.
   * 사용자의 암호를 포함하는 바이트 배열(`byte[]` 객체)입니다. `java.lang.String` 객체의 `getBytes` 메서드를 호출하여 `byte[]` 객체를 가져올 수 있습니다.

   authenticate 메서드는 인증된 사용자에 대한 정보를 포함하는 `AuthResult` 객체를 반환합니다.

1. 인증 컨텍스트를 검색합니다.

   `ServiceClientFactory` 객체의 `getContext` 메서드를 호출하여 `Context` 객체를 반환합니다.

   그런 다음 `Context` 객체의 `initPrincipal` 메서드를 호출하고 `AuthResult`를 전달합니다.

### 웹 서비스 API {#authenticate-a-user-using-the-web-service-api}을(를) 사용하여 사용자 인증

Authentication Manager Service API(웹 서비스)를 사용하여 사용자를 인증합니다.

1. 프로젝트 파일 포함

   * 인증 관리자 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다. (Base64 인코딩](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)을 사용하여 AEM Forms 호출 참조)[
   * Microsoft .NET 클라이언트 어셈블리를 참조하십시오. (Base64 인코딩](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)을 사용하여 AEM Forms 호출의 &quot;Referencing the .NET client assembly&quot;를 참조하십시오.)[

1. AuthenticationManagerService 클라이언트를 만듭니다.

   프록시 클래스의 생성자를 사용하여 `AuthenticationManagerServiceService` 개체를 만듭니다.

1. 인증 작업을 호출합니다.

   `AuthenticationManagerServiceClient` 객체의 `authenticate` 메서드를 호출하고 다음 값을 전달합니다.

   * 사용자의 이름을 포함하는 `string` 개체
   * 사용자의 암호를 포함하는 바이트 배열(`byte[]` 객체)입니다. 아래 예제에 표시된 논리를 사용하여 암호가 들어 있는 `string` 개체를 `byte[]` 배열로 변환하여 `byte[]` 개체를 가져올 수 있습니다.
   * 반환된 값은 사용자에 대한 정보를 가져오는 데 사용할 수 있는 `AuthResult` 객체입니다. 아래 예에서, 먼저 `AuthResult` 개체의 `authenticatedUser` 필드를 가져온 후 결과 `User` 개체의 `canonicalName` 및 `domainName` 필드를 가져와 사용자 정보를 검색합니다.

**참고 항목**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 프로그래밍 방식으로 사용자 동기화 {#programmatically-synchronizing-users}

사용자 관리 API를 사용하여 프로그래밍 방식으로 사용자를 동기화할 수 있습니다. 사용자를 동기화할 때 사용자 저장소에 있는 사용자 데이터와 AEM Forms이 업데이트됩니다. 예를 들어 사용자 저장소에 새 사용자를 추가한다고 가정합니다. 동기화 작업을 수행하면 새 사용자가 AEM 양식 사용자가 됩니다. 또한 더 이상 사용자 리포지토리에 있는 사용자가 AEM Forms에서 제거됩니다.

다음 다이어그램은 사용자 응답과 AEM Forms 동기화를 보여 줍니다.

![ps_ps_umauth_sync](assets/ps_ps_umauth_sync.png)

다음 표에서는 이 다이어그램의 단계를 설명합니다.

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
   <td><p>클라이언트 응용 프로그램에서 AEM Forms이 동기화 작업을 수행하도록 요청합니다.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
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

### {#summary_of_steps-6} 단계 요약

사용자를 프로그래밍 방식으로 동기화하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. UserManagerUtilServiceClient 클라이언트를 만듭니다.
1. 엔터프라이즈 도메인을 지정합니다.
1. 인증 작업을 호출합니다.
1. 동기화 작업이 완료되었는지 확인

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**UserManagerUtilServiceClientclient 만들기**

프로그램 방식으로 사용자를 동기화하려면 먼저 `UserManagerUtilServiceClient` 객체를 만들어야 합니다.

**엔터프라이즈 도메인 지정**

사용자 관리 API를 사용하여 동기화 작업을 수행하기 전에 사용자가 속한 엔터프라이즈 도메인을 지정합니다. 하나 이상의 기업 도메인을 지정할 수 있습니다. 동기화 작업을 프로그래밍 방식으로 수행하려면 [관리 콘솔]을 사용하여 엔터프라이즈 도메인을 설정해야 합니다. ([관리 도움말](https://www.adobe.com/go/learn_aemforms_admin_63)을 참조하십시오.)

**동기화 작업 호출**

하나 이상의 엔터프라이즈 도메인을 지정한 후 동기화 작업을 수행할 수 있습니다. 이 작업을 수행하는 데 걸리는 시간은 사용자 저장소에 있는 사용자 레코드 수에 따라 다릅니다.

**동기화 작업이 완료되었는지 확인**

동기화 작업을 프로그래밍 방식으로 수행한 후 작업이 완료되었는지 확인할 수 있습니다.

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[사용자 관리자 API 빠른 시작](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[암호로 PDF 문서 암호화](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API {#programmatically-synchronizing-users-using-the-java-api}을 사용하여 프로그래밍 방식으로 사용자를 동기화합니다.

사용자 관리 API(Java)를 사용하여 사용자를 동기화합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-usermanager-client.jar 및 adobe-usermanager-util-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. UserManagerUtilServiceClient 클라이언트를 만듭니다.

   해당 생성자를 사용하고 연결 속성이 포함된 `ServiceClientFactory` 객체를 전달하여 `UserManagerUtilServiceClient` 객체를 만듭니다.

1. 엔터프라이즈 도메인을 지정합니다.

   * `UserManagerUtilServiceClient` 객체의 `scheduleSynchronization` 메서드를 호출하여 사용자 동기화 작업을 시작합니다.
   * `HashSet` 생성자를 사용하여 `java.util.Set` 인스턴스를 만듭니다. 데이터 유형으로 `String`을(를) 지정해야 합니다. 이 `Java.util.Set` 인스턴스는 동기화 작업이 적용되는 도메인 이름을 저장합니다.
   * 추가할 각 도메인 이름에 대해 `java.util.Set` 객체의 add 메서드를 호출하고 도메인 이름을 전달합니다.

1. 동기화 작업을 호출합니다.

   `ServiceClientFactory` 객체의 `getContext` 메서드를 호출하여 `Context` 객체를 반환합니다.

   그런 다음 `Context` 객체의 `initPrincipal` 메서드를 호출하고 `AuthResult`를 전달합니다.

**참고 항목**

[프로그래밍 방식으로 사용자 동기화](users.md#programmatically-synchronizing-users)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
