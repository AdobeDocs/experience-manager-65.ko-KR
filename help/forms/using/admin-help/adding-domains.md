---
title: 도메인 추가
description: 도메인 관리 설정을 사용하여 엔터프라이즈, 로컬 또는 하이브리드 도메인을 추가하는 방법과 도메인 이름 및 ID에 대한 일반적인 고려 사항을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c708936d-7aa7-4b92-be2d-d97008f187d2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '941'
ht-degree: 100%

---

# 도메인 추가 {#adding-domains}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

## 엔터프라이즈 도메인 추가 {#add-an-enterprise-domain}

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리를 클릭합니다.
1. 새 엔터프라이즈 도메인을 클릭합니다.
1. ID 상자에 도메인의 고유 식별자를 입력하고 이름 상자에 도메인에 대한 설명적인 이름을 입력합니다. ([도메인 이름 및 ID에 대한 중요 고려 사항](adding-domains.md#important-considerations-for-domain-names-and-ids)을 참조하십시오.)
1. 계정 잠금을 활성화할지 여부를 지정합니다. ([계정 잠금 설정 구성](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings)을 참조하십시오.) 기본적으로 계정 잠금 활성화가 선택되어 있습니다.
1. 인증 추가를 클릭하고 인증 공급자 목록에서 조직이 사용하는 인증 메커니즘에 따라 공급자를 선택합니다. 가능한 값은 LDAP, Kerberos, SAML 또는 사용자 정의 인증 공급자입니다.

   LDAP를 선택하면 디렉터리 구성에 지정된 LDAP 서버를 사용할 수도 있고 인증에 사용할 다른 LDAP 서버를 선택할 수도 있습니다. 다른 서버를 선택하는 경우 사용자는 두 LDAP 서버에 모두 있어야 합니다.

1. 해당 페이지에 필요한 추가 정보를 제공합니다. ([인증 설정](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings)을 참조하십시오.)
1. 디렉터리 또는 사용자 정의 서비스 공급자 인터페이스(SPI)를 추가합니다. ([디렉터리 또는 사용자 정의 SPI 추가](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis)를 참조하십시오.)
1. 완료를 클릭한 후 확인을 클릭합니다.

엔터프라이즈 도메인을 만든 후 사용자 관리에서 해당 도메인을 사용하기 전에 디렉터리를 수동으로 동기화하거나 동기화를 수행하는 트리거를 만듭니다. 그런 다음, 디렉터리 동기화 일정을 설정하고 필요에 따라 수동 동기화를 수행할 수 있습니다. ([디렉터리 동기화](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories)를 참조하십시오.)

## 로컬 도메인 추가 {#add-a-local-domain}

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리를 클릭합니다.
1. 새 로컬 도메인을 클릭합니다.
1. ID 상자에 도메인의 고유 식별자를 입력하고 이름 상자에 도메인에 대한 설명적인 이름을 입력합니다. ([도메인 이름 및 ID에 대한 중요 고려 사항](adding-domains.md#important-considerations-for-domain-names-and-ids)을 참조하십시오.)
1. 계정 잠금을 활성화할지 여부를 지정한 후 확인을 클릭합니다. ([계정 잠금 설정 구성](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings)을 참조하십시오.) 기본적으로 계정 잠금 활성화가 선택되어 있습니다.

## 하이브리드 도메인 추가 {#add-a-hybrid-domain}

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리를 클릭합니다.
1. 새 하이브리드 도메인을 클릭합니다.
1. ID 상자에 도메인의 고유 식별자를 입력하고 이름 상자에 도메인에 대한 설명적인 이름을 입력합니다. ([도메인 이름 및 ID에 대한 중요 고려 사항](adding-domains.md#important-considerations-for-domain-names-and-ids)을 참조하십시오.)
1. 인증 추가를 클릭하고 인증 공급자 목록에서 조직이 사용하는 인증 메커니즘에 따라 공급자를 선택합니다. 가능한 값은 LDAP, Kerberos, SAML 또는 사용자 정의 인증 공급자입니다.
1. 해당 페이지에 필요한 추가 정보를 제공합니다. ([인증 설정](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings)을 참조하십시오.)
1. 확인을 클릭한 후 다시 확인을 클릭합니다.

## 도메인 이름 및 ID에 대한 중요 고려 사항 {#important-considerations-for-domain-names-and-ids}

도메인 이름 및 ID를 선택할 때 다음 사항을 고려하십시오.

### 일반적인 고려 사항 {#general-considerations}

* DB2 이외의 데이터베이스 공급자를 사용하는 경우 도메인 ID는 최대 50바이트까지 포함할 수 있습니다. 싱글바이트 ASCII 문자를 사용하는 경우 문자 수는 50자로 제한됩니다. 도메인 식별자에 멀티바이트 문자가 포함되어 있는 경우 헤딩 제한이 줄어듭니다. 예를 들어 식별자에 3바이트 문자가 포함된 도메인을 만드는 경우 문자 수는 16자로 제한됩니다. 또한 4바이트 문자를 포함하는 도메인은 만들 수 없습니다. 이 제한을 초과하는 도메인 ID를 만들면 AEM Forms가 불안정한 상태가 됩니다. 이러한 불안정한 상태에서 복구하려면 이 페이지의 &#39;[확장 문자 또는 멀티바이트 문자가 포함된 도메인 제거](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)&#39;를 참조하십시오.
* AEM Forms 내에서 만들 수 있는 엔터프라이즈 도메인과 로컬 도메인의 수는 각 도메인 ID의 길이에 따라 달라집니다. 엔터프라이즈 도메인 또는 하이브리드 도메인을 추가하면 사용자 관리에서 AEM Forms 구성 파일(config. xml)의 AuthProviders 노드에 있는 configInstance 문자열을 업데이트합니다. 이 configInstance 문자열에는 인증 공급자와 연결된 모든 도메인의 절대 경로를 콜론으로 구분한 목록이 포함되어 있습니다. 이 문자열의 크기는 8,192자로 제한됩니다. 해당 제한에 도달하면 추가 도메인을 만들 수 없습니다.

### DB2 사용 시 고려 사항 {#considerations-when-using-db2}

AEM Forms 데이터베이스에 DB2를 사용하는 경우 도메인 ID의 최대 허용 길이는 사용된 문자 유형에 따라 달라집니다.

* 100개의 싱글바이트(ASCII)(예: 영어, 프랑스어, 독일어에서 사용되는 문자)
* 50개의 더블바이트(예: 중국어, 일본어, 한국어에서 사용되는 문자)
* 25개의 4바이트(예: 중국어 번체에서 사용되는 문자)

### MySQL 사용 시 고려 사항 {#considerations-when-using-mysql}

AEM Forms 데이터베이스로 MySQL을 사용하는 경우 다음과 같은 제한 사항이 적용됩니다.

* 도메인 ID와 도메인 이름에는 싱글바이트(ASCII) 문자만 사용합니다. 확장된 ASCII 문자를 사용하면 AEM Forms가 불안정한 상태가 되고 도메인을 삭제하려고 하면 예외가 발생할 수 있습니다. 이러한 불안정한 상태에서 복구하려면 이 페이지의 &#39;[확장 문자 또는 멀티바이트 문자가 포함된 도메인 제거](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)&#39; 항목을 참조하십시오.
* 이름은 같지만 대소문자가 다른 두 개의 도메인을 만들 수 없습니다. 예를 들어 *adobe*&#x200B;라는 도메인이 이미 있는 상태에서 *Adobe*&#x200B;라는 도메인을 만들려고 하면 오류가 발생합니다.
* 사용자 관리자는 확장 문자 사용만 다른 두 도메인 이름을 구별할 수 없습니다. 예를 들어 *abcde*&#x200B;라는 도메인과 *âbcdè*&#x200B;라는 도메인을 만드는 경우 두 도메인은 동일한 것으로 간주됩니다.

### 확장 문자 또는 멀티바이트 문자가 포함된 도메인 제거 {#remove-a-domain-that-contains-extended-or-multi-byte-characters}

1. [구성 파일 가져오기 및 내보내기](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)에서 설명된 대로 구성 파일을 내보냅니다.
1. 구성 파일을 열고 도메인 노드에서 확장 문자 또는 멀티바이트 문자로 생성된 도메인 이름과 이름 속성이 일치하는 노드를 찾습니다. 해당 도메인과 관련된 노드 전체를 삭제합니다.
1. 데이터베이스에서 edcprincipaldomainentity 테이블의 도메인을 검색합니다.

   * edcprincipaldomainentity에서 `*`를 선택합니다.
   * 확장 문자 또는 멀티바이트 문자가 포함된 도메인 이름을 찾아 상태를 더 이상 사용되지 않음으로 설정합니다.

1. [구성 파일 가져오기 및 내보내기](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)에서 설명된 대로 업데이트된 구성 파일을 가져옵니다.
