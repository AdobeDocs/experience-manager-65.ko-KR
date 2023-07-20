---
title: 도메인 추가
description: 도메인 이름 및 ID에 대한 도메인 관리 설정 및 일반 고려 사항을 사용하여 엔터프라이즈, 로컬 또는 하이브리드 도메인을 추가하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c708936d-7aa7-4b92-be2d-d97008f187d2
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 0%

---

# 도메인 추가 {#adding-domains}

## Enterprise 도메인 추가 {#add-an-enterprise-domain}

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리 를 클릭합니다.
1. 새 엔터프라이즈 도메인을 클릭합니다.
1. ID 상자에 도메인의 고유 식별자를 입력하고 이름 상자에 도메인을 설명하는 이름을 입력합니다. (참조: [도메인 이름 및 ID에 대한 중요 고려 사항](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. 계정 잠금을 활성화할지 여부를 지정합니다. (참조: [계정 잠금 설정 구성](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) 기본적으로 계정 잠금 활성화가 선택되어 있습니다.
1. 인증 추가를 클릭하고 인증 공급자 목록에서 조직에서 사용하는 인증 메커니즘에 따라 공급자를 선택합니다. 가능한 값은 LDAP, Kerberos, SAML 또는 사용자 지정 인증 공급자입니다.

   LDAP를 선택하는 경우 디렉토리 구성에 지정된 LDAP 서버를 사용하거나 인증에 사용할 다른 LDAP 서버를 선택할 수 있습니다. 다른 서버를 선택하는 경우 사용자가 두 LDAP 서버 모두에 있어야 합니다.

1. 페이지에 필요한 추가 정보를 제공합니다. (참조: [인증 설정](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. 디렉터리 또는 SPI(사용자 지정 서비스 공급자 인터페이스)를 추가합니다. (참조: [디렉터리 또는 사용자 지정 SPI 추가](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. 마침 을 클릭한 다음 확인 을 클릭합니다.

Enterprise 도메인을 생성한 후 User Management에서 사용하기 전에 수동으로 디렉토리를 동기화하거나 트리거를 생성하여 동기화를 수행합니다. 그런 다음 디렉터리 동기화 일정을 설정하고 필요에 따라 수동 동기화를 수행할 수 있습니다. (참조: [디렉터리 동기화](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories).)

## 로컬 도메인 추가 {#add-a-local-domain}

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리 를 클릭합니다.
1. 새 로컬 도메인 을 클릭합니다.
1. ID 상자에 도메인의 고유 식별자를 입력하고 이름 상자에 도메인을 설명하는 이름을 입력합니다. (참조: [도메인 이름 및 ID에 대한 중요 고려 사항](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. 계정 잠금을 사용할지 여부를 지정한 다음 [확인]을 클릭합니다. (참조: [계정 잠금 설정 구성](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) 기본적으로 계정 잠금 활성화가 선택되어 있습니다.

## 하이브리드 도메인 추가 {#add-a-hybrid-domain}

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리 를 클릭합니다.
1. 새 하이브리드 도메인을 클릭합니다.
1. ID 상자에 도메인의 고유 식별자를 입력하고 이름 상자에 도메인을 설명하는 이름을 입력합니다. (참조: [도메인 이름 및 ID에 대한 중요 고려 사항](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. 인증 추가를 클릭하고 인증 공급자 목록에서 조직에서 사용하는 인증 메커니즘에 따라 공급자를 선택합니다. 가능한 값은 LDAP, Kerberos, SAML 또는 사용자 지정 인증 공급자입니다.
1. 페이지에 필요한 추가 정보를 제공합니다. (참조: [인증 설정](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. 확인 을 클릭한 다음 확인 을 다시 클릭합니다.

## 도메인 이름 및 ID에 대한 중요 고려 사항 {#important-considerations-for-domain-names-and-ids}

도메인 이름과 ID를 선택할 때는 다음 사항을 고려해야 합니다.

### 일반 고려 사항 {#general-considerations}

* DB2 이외의 데이터베이스 공급자를 사용하는 경우 도메인 ID는 최대 50바이트를 포함할 수 있습니다. 싱글바이트 ASCII 문자를 사용하는 경우 제한은 50자입니다. 도메인 식별자에 멀티바이트 문자가 포함된 경우 이 제한이 줄어듭니다. 예를 들어 식별자에 3바이트 문자가 포함된 도메인을 만드는 경우 제한은 16자입니다. 또한 4바이트 문자가 포함된 도메인은 만들 수 없습니다. 이 제한을 초과하는 도메인 ID를 만드는 경우 AEM Forms가 불안정한 상태가 됩니다. 이 불안정한 상태에서 복구하려면 다음을 참조하십시오. [확장 문자 또는 멀티바이트 문자가 포함된 도메인 제거](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)이 페이지의 &quot;.
* AEM Forms 내에서 만들 수 있는 Enterprise 도메인 및 로컬 도메인의 수는 각 도메인 ID의 길이에 따라 다릅니다. 엔터프라이즈 또는 하이브리드 도메인을 추가하면 User Management에서 AEM Forms 구성 파일(config.xml)의 AuthProviders 노드에 있는 configInstance 문자열을 업데이트합니다. configInstance 문자열에는 인증 공급자와 연결된 모든 도메인의 절대 경로에 대한 콜론으로 구분된 목록이 포함되어 있습니다. 이 문자열의 크기 제한은 8,192자입니다. 해당 제한에 도달하면 추가 도메인을 만들 수 없습니다.

### DB2 사용 시 고려 사항 {#considerations-when-using-db2}

AEM Forms 데이터베이스에 DB2를 사용할 때 도메인 ID의 최대 허용 길이는 사용된 문자 유형에 따라 달라집니다.

* 100개의 1바이트(ASCII)(예: 영어, 프랑스어 또는 독일어에서 사용되는 문자)
* 50개의 더블바이트(예: 중국어, 일본어 또는 한국어에 사용되는 문자)
* 25개의 4바이트(예: 중국어 번체에 사용되는 문자)

### MySQL 사용 시 고려 사항 {#considerations-when-using-mysql}

MySQL을 AEM Forms 데이터베이스로 사용할 때 다음 제한 사항이 적용됩니다.

* 도메인 ID 및 도메인 이름에는 1바이트(ASCII) 문자만 사용하십시오. 확장 ASCII 문자를 사용하는 경우 AEM Forms가 불안정한 상태가 되며 도메인을 삭제하려고 하면 예외가 발생할 수 있습니다. 이 불안정한 상태에서 복구하려면 다음을 참조하십시오. [확장 문자 또는 멀티바이트 문자가 포함된 도메인 제거](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)&quot;이 페이지의 주제.
* 이름은 같지만 대/소문자가 다른 두 도메인은 만들 수 없습니다. 예를 들어 이라는 도메인을 생성하려고 합니다. *Adobe* 도메인 이름이 인 경우 *adobe* 가 이미 존재합니다. 오류가 발생합니다.
* User Management에서는 확장 문자만 사용하는 것과 다른 두 도메인 이름을 구별할 수 없습니다. 예를 들어, 다음 이름의 도메인을 만드는 경우 *abcde* 및 라는 도메인 *âbcdè*, 동일한 것으로 간주됩니다.

### 확장 문자 또는 멀티바이트 문자가 포함된 도메인 제거 {#remove-a-domain-that-contains-extended-or-multi-byte-characters}

1. 에 설명된 대로 구성 파일을 내보냅니다 [구성 파일 가져오기 및 내보내기](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
1. 구성 파일을 열고 Domains 노드 아래에서 name 속성이 확장 문자 또는 멀티바이트 문자로 만든 도메인 이름과 일치하는 노드를 찾습니다. 해당 도메인과 관련된 전체 노드를 삭제합니다.
1. 데이터베이스에서 edcprincipaldomainentity 테이블에서 도메인을 검색합니다.

   * 선택 `*` edcprincipaldomainentity에서.
   * 확장 문자 또는 멀티바이트 문자가 포함된 도메인 이름을 찾아 해당 상태를 OBSOLETE로 설정합니다.

1. 에 설명된 대로 업데이트된 구성 파일을 가져옵니다. [구성 파일 가져오기 및 내보내기](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
