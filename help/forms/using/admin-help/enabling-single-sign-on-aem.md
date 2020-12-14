---
title: AEM 양식에서 Single Sign-On 사용
seo-title: AEM 양식에서 Single Sign-On 사용
description: HTTP 헤더 및 SPNEGO를 사용하여 SSO(Single Sign-On)를 활성화하는 방법을 알아봅니다.
seo-description: HTTP 헤더 및 SPNEGO를 사용하여 SSO(Single Sign-On)를 활성화하는 방법을 알아봅니다.
uuid: 2bc08b4f-dcbe-4a16-9025-32fc14605e13
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ee54d9d4-190d-4665-925a-9740ac65fbd5
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '1538'
ht-degree: 0%

---


# AEM 양식에서 Single Sign-On 활성화{#enabling-single-sign-on-in-aem-forms}

AEM 양식은 SSO(Single Sign-On)를 활성화하는 두 가지 방법(HTTP 헤더 및 SPNEGO)을 제공합니다.

SSO가 구현되면 AEM 양식 사용자 로그인 페이지가 필요하지 않으며 사용자가 회사 포털을 통해 이미 인증된 경우 나타나지 않습니다.

AEM 양식에서 이러한 방법 중 하나를 사용하여 사용자를 인증할 수 없는 경우 사용자가 로그인 페이지로 리디렉션됩니다.

## HTTP 헤더 {#enable-sso-using-http-headers}을(를) 사용하여 SSO 활성화

포털 구성 페이지에서 HTTP 헤더를 통해 ID를 전달하는 것을 지원하는 응용 프로그램과 응용 프로그램 간 SSO(Single Sign-On)를 활성화할 수 있습니다. SSO가 구현되면 AEM 양식 사용자 로그인 페이지가 필요하지 않으며 사용자가 회사 포털을 통해 이미 인증된 경우 나타나지 않습니다.

SPNEGO를 사용하여 SSO를 활성화할 수도 있습니다. ([SPNEGO](enabling-single-sign-on-aem.md#enable-sso-using-spnego)을 사용하여 SSO 활성화를 참조하십시오.)

1. 관리 콘솔에서 설정 > 사용자 관리 > 구성 > 포털 속성 구성을 클릭합니다.
1. SSO를 활성화하려면 예를 선택합니다. 아니요를 선택하면 페이지의 나머지 설정을 사용할 수 없습니다.
1. 필요에 따라 페이지의 나머지 옵션을 설정하고 확인을 클릭합니다.

   * **SSO 유형:** (필수) HTTP 헤더를 선택하여 HTTP 헤더를 사용하여 SSO를 활성화합니다.
   * **사용자 식별자에 대한 HTTP 헤더:** (필수) 값이 로그인한 사용자의 고유 식별자를 포함하는 헤더의 이름입니다. 사용자 관리는 이 값을 사용하여 사용자 관리 데이터베이스에서 사용자를 찾습니다. 이 헤더에서 얻은 값은 LDAP 디렉토리에서 동기화된 사용자의 고유 식별자와 일치해야 합니다. ([사용자 설정](/help/forms/using/admin-help/adding-configuring-users.md#user-settings)을 참조하십시오.)
   * **식별자 값이 사용자의 고유 식별자 대신 사용자의 사용자 ID에 매핑됩니다.** 사용자의 고유 식별자 값을 사용자 ID에 매핑합니다. 사용자 고유 식별자가 HTTP 헤더를 통해 쉽게 전파할 수 없는 이진 값이면 이 옵션을 선택합니다(예: Active Directory에서 사용자를 동기화하는 경우 objectGUID).
   * **도메인의 HTTP 헤더:** (필수 아님) 값이 도메인 이름을 포함하는 헤더의 이름입니다. 단일 HTTP 헤더가 사용자를 고유하게 식별하는 경우에만 이 설정을 사용하십시오. 여러 도메인이 있고 고유 식별자가 도메인 내에만 고유한 경우에 이 설정을 사용합니다. 이 경우 이 텍스트 상자에 머리글 이름을 지정하고 도메인 매핑 상자에서 여러 도메인에 대한 도메인 매핑을 지정합니다. ([기존 도메인 편집 및 변환](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)을 참조하십시오.)
   * **도메인 매핑:** (필수)  *헤더 값=도메인 이름* 형식의 여러 도메인에 대한 매핑을 지정합니다.

      예를 들어 도메인의 HTTP 헤더가 domainName이고 도메인1, 도메인2 또는 domain3 값을 가질 수 있는 상황을 가정해 보십시오. 이 경우 도메인 매핑을 사용하여 domainName 값을 사용자 관리 도메인 이름에 매핑합니다. 각 매핑은 다른 줄에 있어야 합니다.

      domain1=UMdomain1

      domain2=UMdomain2

      domain3=UMdomain3

### 허용되는 참조 구성 {#configure-allowed-referers}

허용되는 참조를 구성하는 단계는 [허용된 참조 구성](/help/forms/using/admin-help/preventing-csrf-attacks.md#configure-allowed-referers)을 참조하십시오.

## SPNEGO {#enable-sso-using-spnego}을 사용하여 SSO 활성화

Windows 환경에서 LDAP 서버로 Active Directory를 사용할 때 단순 및 보호된 GSSAPI 협상 메커니즘(SPNEGO)을 사용하여 SSO(Single Sign-On)를 활성화할 수 있습니다. SSO가 활성화되면 AEM 양식 사용자 로그인 페이지가 필요하지 않으며 나타나지 않습니다.

HTTP 헤더를 사용하여 SSO를 활성화할 수도 있습니다. (HTTP 헤더[를 사용하여 SSO 활성화를 참조하십시오.)](enabling-single-sign-on-aem.md#enable-sso-using-http-headers)

>[!NOTE]
>
>AEM Forms on JEE는 여러 하위 도메인 환경에서 Kerberos/SPNEGO를 사용하여 SSO 구성을 지원하지 않습니다.

1. SSO를 활성화하는 데 사용할 도메인을 결정합니다. AEM 양식 서버와 사용자는 동일한 Windows 도메인 또는 트러스트된 도메인의 일부여야 합니다.
1. Active Directory에서 AEM 양식 서버를 나타내는 사용자를 만듭니다. ([사용자 계정 만들기](enabling-single-sign-on-aem.md#create-a-user-account)를 참조하십시오.) SPNEGO를 사용하도록 두 개 이상의 도메인을 구성하는 경우 이러한 각 사용자의 암호가 서로 달라야 합니다. 암호가 다를 경우 SPNEGO SSO가 작동하지 않습니다.
1. 서비스 사용자 이름을 매핑합니다. ([SPN(서비스 사용자 이름)](enabling-single-sign-on-aem.md#map-a-service-principal-name-spn) 매핑을 참조하십시오.)
1. 도메인 컨트롤러를 구성합니다. ([Kerberos 무결성 검사 실패 방지](enabling-single-sign-on-aem.md#prevent-kerberos-integrity-check-failures)를 참조하십시오.)
1. [도메인 추가](/help/forms/using/admin-help/adding-domains.md#adding-domains) 또는 [기존 도메인 편집 및 변환](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)에 설명된 대로 엔터프라이즈 도메인을 추가하거나 편집합니다. 엔터프라이즈 도메인을 생성하거나 편집할 때 다음 작업을 수행합니다.

   * Active Directory 정보가 포함된 디렉터리를 추가하거나 편집합니다.
   * LDAP를 인증 공급자로 추가합니다.
   * Kerberos를 인증 공급자로 추가합니다. Kerberos에 대한 새 인증 또는 편집 인증 페이지에 다음 정보를 입력합니다.

      * **인증 공급자:** Kerberos
      * **DNS IP:** AEM 양식이 실행 중인 서버의 DNS IP 주소입니다. 명령줄에서 `ipconfig/all`을(를) 실행하여 이 IP 주소를 확인할 수 있습니다.
      * **KDC 호스트: 인증에 사용되는** Active Directory 서버의 정규화된 호스트 이름 또는 IP 주소
      * **서비스 사용자:** KtPass 도구에 전달된 SPN(서비스 사용자 이름)입니다. 이전에 사용된 예에서 서비스 사용자는 `HTTP/lcserver.um.lc.com`입니다.
      * **서비스 영역:** Active Directory의 도메인 이름입니다. 이전에 사용된 예에서 도메인 이름은 `UM.LC.COM.`입니다.
      * **서비스 암호:** 서비스 사용자의 암호입니다. 이전에 사용된 예에서 서비스 암호는 `password`입니다.
      * **SPNEGO 사용:** SSO(Single Sign-On)에 SPNEGO 사용을 활성화합니다. 이 옵션을 선택합니다.

1. SPNEGO 클라이언트 브라우저 설정을 구성합니다. ([SPNEGO 클라이언트 브라우저 설정 구성](enabling-single-sign-on-aem.md#configuring-spnego-client-browser-settings)을 참조하십시오.)

### 사용자 계정 {#create-a-user-account} 만들기

1. SPNEGO에서 도메인 컨트롤러의 Active Directory 사용자로 서비스를 등록하여 AEM 양식을 표시합니다. 도메인 컨트롤러에서 시작 메뉴 > 관리 도구 > Active Directory 사용자 및 컴퓨터로 이동합니다. [시작] 메뉴에 [관리 도구]가 없으면 Campaign 컨트롤 패널을 사용합니다.
1. 사용자 목록을 표시하려면 사용자 폴더를 클릭합니다.
1. 사용자 폴더를 마우스 오른쪽 단추로 클릭하고 [새로 만들기] > [사용자]를 선택합니다.
1. 이름/성 및 사용자 로그온 이름을 입력한 다음 다음을 클릭합니다. 예를 들어 다음 값을 설정합니다.

   * **이름**:umspnego
   * **사용자 로그온 이름**:spnegodemo

1. 암호를 입력합니다. 예를 들어 *password*&#x200B;로 설정합니다. [만료되지 않음]이 선택되어 있고 다른 옵션이 선택되어 있지 않아야 합니다.
1. 다음을 클릭한 다음 마침을 클릭합니다.

### SPN(서비스 사용자 이름) {#map-a-service-principal-name-spn} 매핑

1. KtPass 유틸리티를 구입합니다. 이 유틸리티는 SPN을 REALM에 매핑하는 데 사용됩니다. KtPass 유틸리티는 Windows Server 도구 팩 또는 리소스 키트의 일부로 구입할 수 있습니다. ([Windows Server 2003 서비스 팩 1 지원 도구](https://support.microsoft.com/kb/892777)를 참조하십시오.)
1. 명령 프롬프트에서 다음 인수를 사용하여 `ktpass`을 실행합니다.

   `ktpass -princ HTTP/`** `@`** `-mapuser`*hostREALMuser*

   예를 들어 다음 텍스트를 입력합니다.

   `ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo`

   제공해야 하는 값은 다음과 같이 설명되어 있습니다.

   **호스트:** 양식 서버의 정규화된 이름 또는 고유한 URL입니다. 이 예에서는 lcserver.um.lc.com으로 설정됩니다.

   **영역:** 도메인 컨트롤러의 Active Directory 영역입니다. 이 예에서는 UM.LC.COM으로 설정됩니다. 영역을 대문자로 입력해야 합니다. Windows 2003의 영역을 결정하려면 다음 단계를 완료하십시오.

   * [내 컴퓨터]를 마우스 오른쪽 단추로 클릭하고 [속성]을 선택합니다
   * 컴퓨터 이름 탭을 클릭합니다. Domain Name 값은 영역 이름입니다.

   **사용자:** 이전 작업에서 만든 사용자 계정의 로그인 이름입니다. 이 예에서는 spnegodemo로 설정됩니다.

이 오류가 발생하는 경우:

```shell
DsCrackNames returned 0x2 in the name entry for spnegodemo.
ktpass:failed getting target domain for specified user.
```

사용자를 spnegodemo@um.lc.com으로 지정합니다.

```shell
ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo
```

### Kerberos 무결성 검사 실패 방지 {#prevent-kerberos-integrity-check-failures}

1. 도메인 컨트롤러에서 시작 메뉴 > 관리 도구 > Active Directory 사용자 및 컴퓨터로 이동합니다. [시작] 메뉴에 [관리 도구]가 없으면 Campaign 컨트롤 패널을 사용합니다.
1. 사용자 목록을 표시하려면 사용자 폴더를 클릭합니다.
1. 이전 작업에서 만든 사용자 계정을 마우스 오른쪽 단추로 클릭합니다. 이 예에서 사용자 계정은 `spnegodemo`입니다.
1. 암호 재설정을 클릭합니다.
1. 이전에 입력한 암호와 동일한 암호를 입력하고 확인합니다. 이 예제에서는 `password`으로 설정됩니다.
1. [다음 로그온 시 암호 변경]을 선택 해제한 다음 [확인]을 클릭합니다.

### SPNEGO 클라이언트 브라우저 설정 구성 중 {#configuring-spnego-client-browser-settings}

SPNEGO 기반 인증이 작동하려면 클라이언트 컴퓨터가 사용자 계정이 만든 도메인의 일부여야 합니다. 또한 SPNEGO 기반 인증을 허용하도록 클라이언트 브라우저를 구성해야 합니다. 또한 SPNEGO 기반 인증이 필요한 사이트는 신뢰할 수 있는 사이트여야 합니다.

https://lcserver:8080과 같이 컴퓨터 이름을 사용하여 서버에 액세스하는 경우에는 Internet Explorer에 설정이 필요하지 않습니다. 점이 없는 URL(&quot;.&quot;)을 입력하면 Internet Explorer는 사이트를 로컬 인트라넷 사이트로 처리합니다. 사이트에 정규화된 이름을 사용하는 경우 사이트를 신뢰할 수 있는 사이트로 추가해야 합니다.

**Internet Explorer 6.x 구성**

1. 도구 > 인터넷 옵션으로 이동하고 보안 탭을 클릭합니다.
1. 로컬 인트라넷 아이콘을 클릭한 다음 사이트를 클릭합니다.
1. 고급을 클릭하고 [이 웹 사이트를 영역에 추가] 상자에 양식 서버의 URL을 입력합니다. 예를 들어 `https://lcserver.um.lc.com`
1. 모든 대화 상자가 닫힐 때까지 확인을 클릭합니다.
1. AEM 양식 서버의 URL에 액세스하여 구성을 테스트합니다. 예를 들어 브라우저 URL 상자에 `https://lcserver.um.lc.com:8080/um/login?um_no_redirect=true` 입력

**Mozilla Firefox 구성**

1. 브라우저 URL 상자에 `about:config` 입력

   about:config - Mozilla Firefox 대화 상자가 나타납니다.

1. 필터 상자에 `negotiate` 입력
1. 표시된 목록에서 network.negotiate-auth.trusted-uri를 클릭하고 환경에 적합한 다음 명령 중 하나를 입력합니다.

   `.um.lc.com`- um.lc.com으로 끝나는 모든 URL에 대해 SPNEGO를 허용하도록 Firefox를 구성합니다. 도트(&quot;.&quot;)를 포함해야 합니다. 을 클릭합니다.

   `lcserver.um.lc.com` - 특정 서버에 대해서만 SPNEGO를 허용하도록 Firefox를 구성합니다. 도트(&quot;.&quot;)로 이 값을 시작하지 마십시오.

1. 애플리케이션에 액세스하여 구성을 테스트합니다. 대상 애플리케이션에 대한 시작 페이지가 나타납니다.

