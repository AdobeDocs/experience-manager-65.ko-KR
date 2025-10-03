---
title: 인증 공급자 구성
description: 인증 공급자를 추가, 편집 또는 삭제하고, 인증 설정을 변경하고, 사용자 적시 프로비저닝을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d72a3977-1423-49e0-899b-234bb76be378
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1592'
ht-degree: 100%

---

# 인증 공급자 구성 {#configuring-authentication-providers}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

하이브리드 도메인에는 인증 공급자가 하나 이상 필요하고 엔터프라이즈 도메인에는 인증 공급자 또는 디렉터리 공급자가 하나 이상 필요합니다.

SPNEGO를 사용하여 SSO를 활성화하는 경우 SPNEGO가 활성화된 Kerberos 인증 공급자와 백업으로 LDAP 공급자를 추가합니다. 이 구성을 사용하면 SPNEGO가 작동하지 않을 때 사용자 ID와 암호를 사용하여 사용자를 인증할 수 있습니다. ([SPNEGO를 사용하여 SSO 활성화](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego)를 참조하십시오.)

## 인증 공급자 추가 {#add-an-authentication-provider}

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리를 클릭합니다.
1. 목록에서 기존 도메인을 클릭합니다. 새 도메인에 대한 인증을 추가하는 경우 [엔터프라이즈 도메인 추가](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain) 또는 [하이브리드 도메인 추가](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain)를 참조하십시오.
1. 인증 추가를 클릭하고 인증 공급자 목록에서 조직이 사용하는 인증 메커니즘에 따라 공급자를 선택합니다.
1. 해당 페이지에 필요한 추가 정보를 제공합니다. ([인증 설정](configuring-authentication-providers.md#authentication-settings)을 참조하십시오.)
1. (선택 사항) 테스트를 클릭하여 구성을 테스트합니다.
1. 확인을 클릭한 후 다시 확인을 클릭합니다.

## 기존 인증 공급자 편집 {#edit-an-existing-authentication-provider}

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리를 클릭합니다.
1. 목록에서 해당 도메인을 클릭합니다.
1. 페이지가 표시되면 목록에서 해당 인증 공급자를 선택하고 필요에 따라 변경합니다. ([인증 설정](configuring-authentication-providers.md#authentication-settings)을 참조하십시오.)
1. 확인을 클릭합니다.

## 인증 공급자 삭제 {#delete-an-authentication-provider}

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리를 클릭합니다.
1. 목록에서 해당 도메인을 클릭합니다.
1. 삭제할 인증 공급자의 확인란을 선택하고 삭제를 클릭합니다.
1. 확인 페이지가 나타나면 확인을 클릭하고 다시 확인을 클릭합니다.

## 인증 설정 {#authentication-settings}

선택한 도메인 유형과 인증 유형에 따라 다음 설정을 사용할 수 있습니다.

### LDAP 설정 {#ldap-settings}

엔터프라이즈 또는 하이브리드 도메인에 대한 인증을 구성하고 LDAP 인증을 선택하는 경우 디렉터리 구성에 지정된 LDAP 서버를 사용하거나 인증에 사용할 다른 LDAP 서버를 선택할 수 있습니다. 다른 서버를 선택하는 경우 사용자는 두 LDAP 서버에 모두 있어야 합니다.

디렉터리 구성에 지정된 LDAP 서버를 사용하려면 인증 공급자로 LDAP를 선택하고 확인을 클릭합니다.

다른 LDAP 서버를 사용하여 인증을 수행하려면 인증 공급자로 LDAP를 선택하고 사용자 정의 LDAP 인증 확인란을 선택합니다. 다음과 같은 구성 설정이 표시됩니다.

**서버:** (필수) 디렉터리 서버의 정규화된 도메인 이름(FQDN)입니다. 예를 들어 example. com 네트워크에 있는 x라는 컴퓨터의 경우 FQDN은 x. example. com입니다. FQDN 서버 이름 대신 IP 주소를 사용할 수 있습니다.

**포트:** (필수) 디렉터리 서버에서 사용하는 포트입니다. 일반적으로 389이거나 네트워크를 통해 인증 정보를 전송하는 데 SSL(Secure Sockets Layer) 프로토콜을 사용하는 경우에는 636입니다.

**SSL:** (필수) 디렉터리 서버에서 네트워크를 통해 데이터를 전송할 때 SSL을 사용할지 여부를 지정합니다. 기본값은 아니요입니다. 예로 설정하면 해당 LDAP 서버 인증서는 애플리케이션 서버의 Java™ 런타임 환경(JRE)에서 신뢰할 수 있어야 합니다.

**바인딩** (필수) 디렉터리에 액세스하는 방법을 지정합니다.

**익명:** 사용자 이름 또는 암호가 필요하지 않습니다.

**사용자:** 인증이 필요합니다. 이름 상자에 디렉터리에 액세스할 수 있는 사용자 레코드 이름을 지정합니다. 사용자 계정의 전체 고유 이름(DN)을 입력하는 것이 가장 좋습니다(예: cn=Jane Doe, ou=user, dc=can, dc=com). 암호 상자에 연결된 암호를 지정합니다. 해당 설정은 바인딩 옵션으로 사용자를 선택할 때 필요합니다.

**기본 DN 가져오기:** (필수 아님) 기본 DN을 가져와서 드롭다운 목록에 표시합니다. 이 설정은 여러 개의 기본 DN이 있고 값을 선택해야 할 때 유용합니다.

**기본 DN:** (필수) LDAP 계층에서 사용자 및 그룹을 동기화하기 위한 시작점으로 사용됩니다. 서비스를 위해 동기화해야 하는 모든 사용자 및 그룹을 포함하는 가장 낮은 수준의 계층에서 기본 DN을 지정하는 것이 가장 좋습니다. 해당 설정에 사용자의 DN을 포함하지 마십시오. 특정 사용자를 동기화하려면 검색 필터 설정을 사용합니다.

**다음 값으로 페이지 채우기:** (필수 아님) 이 구성을 선택하면 사용자 및 그룹 설정 페이지의 속성이 해당 기본 LDAP 값으로 채워집니다.

**검색 필터:** (필수) 사용자와 연결된 레코드를 찾는 데 사용할 검색 필터입니다. 검색 필터 구문을 참조하십시오.

### Kerberos 설정 {#kerberos-settings}

엔터프라이즈 또는 하이브리드 도메인에 대한 인증을 구성하고 Kerberos 인증을 선택하는 경우 다음 설정을 사용할 수 있습니다.

**DNS IP:** AEM Forms가 실행되는 서버의 DNS IP 주소입니다. Windows 명령줄에서 ipconfig/all을 실행하면 해당 IP 주소를 확인할 수 있습니다.

**KDC 호스트:** 인증에 사용되는 Active Directory 서버의 정규화된 호스트 이름 또는 IP 주소입니다.

**서비스 사용자:** Active Directory 2003을 사용하는 경우 이 값은 `HTTP/<server name>` 양식의 서비스 주체에 대해 생성된 매핑입니다. Active Directory 2008을 사용하는 경우 이 값은 서비스 주체의 로그인 ID입니다. 예를 들어 서비스 주체의 이름이 um spnego이고 사용자 ID가 spnegodemo이며 매핑이 HTTP/example.yourcompany.com이라고 가정해 보겠습니다. Active Directory 2003에서는 서비스 사용자를 HTTP/example.yourcompany.com으로 설정합니다. Active Directory 2008에서는 서비스 사용자를 spnegodemo로 설정합니다. (SPNEGO를 사용하여 SSO 활성화를 참조하십시오.)

**서비스 영역:** Active Directory의 도메인 이름입니다.

**서비스 암호:** 서비스 사용자의 암호입니다.

**SPNEGO 활성화:** SSO(Single Sign-On)를 위해 SPNEGO 사용을 활성화합니다. (SPNEGO를 사용하여 SSO 활성화를 참조하십시오.)

### SAML 설정 {#saml-settings}

엔터프라이즈 또는 하이브리드 도메인에 대한 인증을 구성하고 SAML 인증을 선택하는 경우 다음 설정을 사용할 수 있습니다. 추가 SAML 설정에 대한 자세한 내용은 [SAML 서비스 공급자 설정 구성](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings)을 참조하십시오.

**가져올 SAML ID 공급자 메타데이터
파일을 선택하십시오:** 찾아보기를 클릭하여 IDP에서 생성된 SAML ID 공급자 메타데이터 파일을 선택한 후 가져오기를 클릭합니다. IDP의 세부 정보가 표시됩니다.

**제목:** EntityID로 표시되는 URL 별칭입니다. 이 제목은 엔터프라이즈 및 로컬 사용자의 로그인 페이지에도 표시됩니다.

**ID 공급자가 클라이언트 기본 인증을 지원함:** IDP가 SAML 아티팩트 확인 프로필을 사용하는 경우 클라이언트 기본 인증이 사용됩니다. 이 프로필에서 사용자 관리는 IDP에서 실행되는 웹 서비스에 다시 연결하여 실제 SAML 어설션을 가져옵니다. IDP에는 인증이 필요할 수 있습니다. IDP에 인증이 필요한 경우 이 옵션을 선택하고 제공된 상자에 사용자 이름 및 암호를 지정합니다.

**사용자 정의 속성:** 추가 속성을 지정할 수 있습니다. 추가 속성은 새 줄로 구분된 이름=값 쌍입니다.

아티팩트 바인딩을 사용하는 경우 다음과 같은 사용자 정의 속성이 필요합니다.

* IDP 아티팩트 확인 서비스를 인증하는 데 사용되는 AEM Forms 서비스 공급자를 나타내는 사용자 이름을 지정하려면 다음과 같은 사용자 정의 속성을 추가합니다.
  `saml.idp.resolve.username=<username>`

* `saml.idp.resolve.username`에 지정된 사용자의 암호를 지정하려면 다음과 같은 사용자 정의 속성을 추가합니다.
  `saml.idp.resolve.password=<password>`

* 서비스 공급자가 SSL을 통해 아티팩트 해결 서비스와의 연결을 설정하는 동안 인증서 유효성 검사를 무시할 수 있도록 하려면 다음과 같은 사용자 정의 속성을 추가합니다.
  `saml.idp.resolve.ignorecert=true`

### 사용자 정의 설정 {#custom-settings}

엔터프라이즈 또는 하이브리드 도메인에 대한 인증을 구성하고 사용자 정의 인증을 선택하는 경우 사용자 정의 인증 공급자의 이름을 선택합니다.

## 사용자 적시 프로비저닝 {#just-in-time-provisioning-of-users}

적시 프로비저닝은 사용자가 인증 공급자를 통해 인증된 후 사용자 관리 데이터베이스에 사용자를 자동으로 만듭니다. 새 사용자에게는 관련 역할과 그룹도 동적으로 할당됩니다. 엔터프라이즈 및 하이브리드 도메인에 대해 적시 프로비저닝을 활성화할 수 있습니다.

이 절차에서는 기존 인증이 AEM Forms에서 작동하는 방식을 설명합니다.

1. 사용자가 AEM Forms에 로그인을 시도하면 사용자 관리에서 해당 자격 증명을 사용 가능한 모든 인증 공급자에게 순차적으로 전달합니다. (로그인 자격 증명에는 사용자 이름/암호 조합, Kerberos 티켓, PKCS7 서명 등이 포함됩니다.)
1. 인증 공급자가 자격 증명의 유효성을 검사합니다.
1. 그런 다음, 인증 공급자는 사용자가 사용자 관리 데이터베이스에 있는지 확인합니다. 가능한 상태는 다음과 같습니다.

   **존재함** 사용자가 현재 상태이고 잠금 해제된 경우 사용자 관리에서 인증 성공을 반환합니다. 그러나 사용자가 현재 상태가 아니거나 잠겨 있는 경우 사용자 관리에서 인증 실패를 반환합니다.

   **존재하지 않음** 사용자 관리에서 인증 실패를 반환합니다.

   **잘못됨** 사용자 관리에서 인증 실패를 반환합니다.

1. 인증 공급자가 반환한 결과를 평가합니다. 인증 공급자가 인증 성공을 반환하면 사용자는 로그인할 수 있습니다. 그렇지 않은 경우 사용자 관리에서는 다음 인증 공급자에게 확인합니다(2~3단계).
1. 사용 가능한 인증 공급자가 사용자 자격 증명의 유효성을 검사하지 못하면 인증 실패가 반환됩니다.

적시 프로비저닝이 활성화된 경우 인증 공급자 중 하나가 자격 증명의 유효성을 검사하면 사용자 관리에서 새 사용자가 동적으로 생성됩니다. (위 절차의 3단계 이후)

적시 프로비저닝이 없으면 사용자가 인증되었지만 사용자 관리 데이터베이스에서 해당 사용자를 찾을 수 없는 경우 인증이 실패합니다. 적시 프로비저닝은 인증 절차에 사용자를 만들고 사용자에게 역할과 그룹을 할당하는 단계를 추가합니다.

### 도메인 적시 프로비저닝 활성화 {#enable-just-in-time-provisioning-for-a-domain}

1. IdentityCreator 및 AssignmentProvider 인터페이스를 구현하는 서비스 컨테이너를 작성합니다. ([AEM Forms를 사용한 프로그래밍](https://www.adobe.com/go/learn_aemforms_programming_63)을 참조하십시오.)
1. 서비스 컨테이너를 Forms 서버에 배포합니다.
1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리를 클릭합니다.

   기존 도메인을 선택하거나 새 엔터프라이즈 도메인을 클릭합니다.

1. 도메인을 만들려면 새 엔터프라이즈 도메인 또는 새 하이브리드 도메인을 클릭합니다. 기존 도메인을 편집하려면 도메인 이름을 클릭합니다.
1. 적시 프로비저닝 활성화를 선택합니다.

   ***참고&#x200B;**: 적시 프로비저닝 활성화 확인란이 없으면 홈 > 설정 > 사용자 관리 > 구성 > 고급 시스템 속성을 클릭한 후 다시 로드를 클릭합니다.*

1. 인증 공급자를 추가합니다. 인증 공급자를 추가하는 동안 새 인증 화면에서 등록된 ID 생성자와 할당 공급자를 선택합니다. ([인증 공급자 구성](configuring-authentication-providers.md#configuring-authentication-providers)을 참조하십시오.)
1. 도메인을 저장합니다.
