---
title: 디렉터리 구성
description: 디렉터리를 추가, 편집 및 삭제하고 가상 목록 보기를 사용하도록 사용자 관리를 구성하는 방법에 대해 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 30edcef2-e8fa-403a-9850-b8dfeeb9ac65
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '3229'
ht-degree: 0%

---

# 디렉터리 구성 {#configuring-directories}

구성하는 각 엔터프라이즈 도메인에 대해 인증 공급자가 사용자 정보를 쿼리하는 디렉토리를 지정합니다. 한 도메인에 대해 여러 디렉터리를 구성할 수 있습니다.

## 디렉터리 또는 사용자 지정 SPI 추가 {#adding-directories-or-custom-spis}

구성하는 각 엔터프라이즈 도메인에 대해 인증 공급자가 사용자 정보를 쿼리하는 디렉토리를 지정합니다. 기존 엔터프라이즈 도메인이나 추가하려는 새 엔터프라이즈 도메인에 디렉토리를 추가할 수 있습니다. 한 도메인에 대해 여러 디렉터리를 구성할 수 있습니다. 동기화를 위해 사용자 지정 SPI(서비스 공급자 인터페이스)를 사용하도록 도메인을 구성할 수도 있습니다.

### 디렉터리 추가 {#add-a-directory}

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리 를 클릭합니다.
1. 새 Enterprise 도메인을 누르거나 기존 Enterprise 도메인을 선택합니다.
1. 디렉터리 추가를 클릭합니다.
1. 프로파일 이름 상자에 이 디렉토리를 구분할 이름을 입력하고 다음을 클릭합니다.
1. 디렉토리 서버 설정을 구성합니다. (참조: [디렉터리 설정](configuring-directories.md#directory-settings).)
1. LDAP 서버에 연결할 수 있는지 확인하려면 Test 를 클릭합니다. 테스트가 실패할 경우 Application Server 로그 파일의 예외를 검토하여 실패의 근본 원인을 파악합니다. 닫기 를 클릭한 후 다음 을 클릭합니다.
1. 사용자 설정 을 선택하고 필요에 따라 설정을 구성합니다. (참조: [디렉터리 설정](configuring-directories.md#directory-settings).)
1. 기본 DN 및 기타 구성된 속성이 올바른 사용자 배치를 수집하는지 확인하려면 테스트를 누릅니다. LDAP는 제공된 설정(예: 기본 DN, 검색 필터 및 모든 속성)을 사용하여 처음 200개의 레코드를 검색하려고 합니다.

   사용자가 반환되면 속성 세트에 따라 각 필드에 할당된 값이 결과에 표시됩니다. 존재하지 않는 서버 이름, 잘못된 인증 정보 또는 잘못된 특성으로 인해 테스트에 실패한 경우 &quot;지정된 검색 기준이 결과를 반환하지 않았습니다.&quot;라는 오류 메시지가 나타납니다. 오류의 근본 원인을 확인하려면 Application Server 로그 파일에서 예외를 검토하십시오. 닫기 를 클릭한 후 다음 을 클릭합니다.

1. 그룹 설정 을 선택하고 필요에 따라 설정을 구성합니다. (참조: [디렉터리 설정](configuring-directories.md#directory-settings).)
1. 기본 DN 및 기타 구성된 속성이 올바른 그룹 배치를 수집하는지 확인하려면 테스트를 누릅니다. 그룹이 반환되면 속성 세트에 따라 각 필드에 할당된 값이 결과에 표시됩니다. 닫기를 클릭합니다.

### 사용자 정의 SPI 추가 {#add-a-custom-spi}

사용자 지정 SPI 만들기에 대한 자세한 내용은 의 &quot;AEM Forms용 SPI 개발&quot;을 참조하십시오. [AEM Forms를 사용한 프로그래밍](https://www.adobe.com/go/learn_aemforms_programming_63). 새로 배포된 사용자 지정 SPI를 도메인과의 연결에 사용할 수 있도록 하려면 서버를 다시 시작하십시오.

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리 를 클릭합니다.
1. 새 Enterprise 도메인을 누르거나 기존 Enterprise 도메인을 선택합니다.
1. 디렉터리 추가를 클릭합니다.
1. 프로필 이름 상자에 이름을 입력하고 사용자 지정 SPI 공급자를 선택한 후 다음을 클릭합니다.
1. 목록에서 사용자 정의 사용자 공급자를 선택하고 다음을 누릅니다.
1. 목록에서 사용자 정의 그룹 공급자를 선택하고 완료를 클릭합니다.

## 디렉터리 편집 {#edit-a-directory}

이전에 구성한 디렉토리의 세부 정보를 편집할 수 있습니다.

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리 를 클릭합니다.
1. 목록에서 적절한 도메인을 클릭하고 나타나는 페이지에서 목록에서 적절한 디렉토리를 선택합니다.
1. 필요에 따라 디렉터리, 사용자 및 그룹 설정을 구성합니다. (참조: [디렉터리 설정](configuring-directories.md#directory-settings).)
1. 확인을 클릭합니다.

## 디렉터리 삭제 {#delete-a-directory}

디렉토리를 삭제한 후 도메인을 동기화할 경우 해당 디렉토리의 모든 사용자와 그룹이 데이터베이스에서 더 이상 사용되지 않는 것으로 표시됩니다. 관리 콘솔의 검색에서는 반환되지 않습니다.

>[!NOTE]
>
>엔터프라이즈 도메인에는 하나 이상의 인증 공급자와 디렉토리 공급자가 필요합니다.

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리 를 클릭합니다.
1. 목록에서 적절한 도메인을 클릭합니다.
1. 해당 디렉토리에 대한 확인란을 선택하고 삭제(Delete)를 클릭합니다.
1. 표시되는 확인 페이지에서 확인 을 클릭하고 확인 을 다시 클릭합니다.

## 디렉터리 설정 {#directory-settings}

도메인에 디렉터리를 추가할 때 다음 디렉터리 설정을 지정합니다.

**서버:** (필수) 디렉터리 서버의 FQDN(정규화된 도메인 이름)입니다. 예를 들어 adobe.com 네트워크의 x라는 컴퓨터의 경우 FQDN은 x.adobe.com입니다. FQDN 서버 이름 대신 IP 주소를 사용할 수 있습니다.

**포트:** (필수) 디렉토리 서버가 사용하는 포트입니다. SSL(Secure Sockets Layer) 프로토콜이 네트워크를 통해 인증 정보를 전송하는 데 사용되는 경우 일반적으로 389 또는 636입니다.

**SSL:** (필수) 네트워크를 통해 데이터를 전송할 때 디렉터리 서버가 SSL을 사용하는지 여부를 지정합니다. 기본값은 No입니다. Yes로 설정하면 해당 LDAP 서버 인증서를 애플리케이션 서버의 JRE(Java™ Runtime Environment)에서 신뢰해야 합니다.

**바인딩** (필수) 디렉터리에 액세스하는 방법을 지정합니다.

**익명:** 사용자 이름이나 암호는 필요하지 않습니다. 익명 사용자는 제한된 양의 데이터만 가져올 수 있습니다. 이 옵션은 초기 테스트에 유용할 수 있습니다.

**사용자:** 인증이 필요합니다. 이름 상자에 디렉토리에 액세스할 수 있는 사용자 레코드의 이름을 지정합니다. cn=Jane Doe, ou=user, dc=can, dc=com과 같은 사용자 계정의 전체 DN(식별 이름)을 입력하는 것이 가장 좋습니다. 암호 상자에서 관련 암호를 지정합니다. 이러한 설정은 사용자를 바인딩 옵션으로 선택할 때 필요합니다.

**이름:** 익명 액세스가 활성화되지 않은 경우 LDAP 데이터베이스에 연결하는 데 사용할 수 있는 이름입니다. Active Directory 2003의 경우 `[domain name]\[userid]`. Sun™ One, eDirectory 또는 IBM Tivoli Directory Server의 경우 uid=lcuser,ou=it,o=company.com 과 같이 사용자의 정규화된 이름을 지정합니다.

**암호:** 익명 액세스가 활성화되지 않은 경우 LDAP 데이터베이스에 연결하기 위해 지정한 이름과 일치하는 암호입니다.

**다음으로 페이지 채우기:** 선택하면 사용자 및 그룹 설정 페이지의 속성이 해당 기본 LDAP 값으로 채워집니다.

**기본 DN 검색:** 기본 DN을 검색하고 드롭다운 목록에 표시합니다. 이 설정은 기본 DN이 여러 개이고 값을 선택해야 하는 경우에 유용합니다.

**참조 활성화:** 이 설정은 조직에서 계층 구조로 구성된 여러 Active Directory 도메인을 사용하고 상위 도메인에만 디렉터리 설정을 지정한 경우에 적용됩니다. 이 경우 이 옵션을 선택하면 사용자 관리는 하위 도메인에서 사용자 및 그룹 세부 정보에 액세스할 수 있습니다.

>[!NOTE]
>
>Test 를 클릭하여 LDAP 서버에 연결할 수 있는지 확인합니다. 실패의 근본 원인을 확인하려면 Application Server 로그 파일에서 예외를 검토하십시오.

### 사용자 설정 {#user-settings}

**고유 식별자:** (필수) 사용자를 식별하는 데 사용되는 고유한 상수 속성입니다. 조직의 다른 부분으로 이동할 경우 사용자의 DN이 변경될 수 있으므로 DN이 아닌 속성을 고유 식별자로 사용합니다. 이 설정은 디렉터리 서버에 따라 다릅니다. 값은 Active Directory 2003의 objectGUID, Sun™ One의 nuniqueID 및 eDirectory의 guid입니다.

>[!NOTE]
>
>조직에서 고유하도록 보장된 속성을 입력해야 합니다. 잘못된 값을 입력하면 심각한 시스템 문제가 발생할 수 있습니다.

**기본 DN:** LDAP 계층에서 사용자 및 그룹 동기화를 위한 시작점으로 설정합니다. 서비스에 대해 동기화해야 하는 모든 사용자 및 그룹을 포함하는 계층의 가장 낮은 수준에서 기본 DN을 지정하는 것이 가장 좋습니다.

디렉터리 설정에서 참조 활성화 옵션을 선택한 경우 기본 DN 옵션을 로 설정합니다. *dc* DN의 일부입니다. 조회가 작동하려면 검색 범위에 상위 도메인과 하위 도메인이 모두 포함되어야 합니다.

>[!NOTE]
>
>이 설정에 사용자의 DN을 포함하지 마십시오. 특정 사용자를 동기화하려면 검색 필터 설정을 사용합니다.

기본 DN은 관리 콘솔의 필수 설정이지만 IBM Domino Enterprise Server와 같은 일부 디렉터리 서버에는 빈 BaseDN이 필요할 수 있습니다. 빈 기본 DN을 지정하려면 config.xml 파일을 내보내고 config.xml 파일에서 설정을 편집한 다음 다시 가져옵니다. (참조: [구성 파일 가져오기 및 내보내기](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**검색 필터:** (필수) 사용자와 연결된 레코드를 찾는 데 사용할 검색 필터입니다. 한 수준 검색이나 하위 수준 검색을 수행할 수 있습니다. ( 검색 필터 구문 또는 RFC 2254를 참조하십시오.) Microsoft AD 스키마에 대한 추가 정보는 Active Directory 스키마를 참조하십시오.

**설명:** 사용자 설명에 대한 스키마 속성

**전체 이름:** (필수) 사용자의 전체 이름에 대한 스키마 속성

**로그인 ID:** (필수) 사용자 로그인 ID에 대한 스키마 속성

**성:** (필수) 사용자 성에 대한 스키마 속성

**이름:** (필수) 사용자 이름에 대한 스키마 속성

**이니셜:** 사용자 이니셜에 대한 스키마 속성

**비즈니스 캘린더:** 이 설정의 값(비즈니스 캘린더 키)을 기반으로 사용자에게 비즈니스 캘린더를 매핑할 수 있습니다. 업무 달력은 업무일과 비업무일을 정의합니다. AEM forms에서는 미리 알림, 기한 및 에스컬레이션과 같은 이벤트에 대한 미래 날짜 및 시간을 계산할 때 비즈니스 달력을 사용할 수 있습니다. 사용자에게 비즈니스 캘린더 키를 할당하는 방법은 엔터프라이즈, 로컬 또는 하이브리드 도메인을 사용하는지 여부에 따라 다릅니다. ( 비즈니스 캘린더 구성을 참조하십시오.)

Enterprise 도메인을 사용하는 경우 Business Calendar 설정을 LDAP 디렉토리의 필드에 매핑할 수 있습니다. 예를 들어 디렉터리의 각 사용자 레코드에 *국가* 필드를 작성하고 사용자가 있는 국가에 따라 비즈니스 달력을 할당하려면 *국가* 비즈니스 달력 설정의 값을 나타내는 필드 이름입니다. 그런 다음 비즈니스 캘린더 키(에 대해 정의된 값)를 매핑할 수 있습니다. *국가* LDAP 디렉터리의 필드)를 참조하십시오.

양식 워크플로우 페이지에서 비즈니스 달력 키의 이름을 표시하는 데 사용되는 공간의 양이 제한됩니다. 비즈니스 달력 키의 이름을 53자 미만으로 제한하여 해당 페이지에서 잘리지 않도록 하십시오.

**타임스탬프 수정:** 델타 디렉토리 동기화를 활성화하려면 이 값을 설정하여 타임스탬프를 수정합니다. 델타 디렉토리 동기화 활성화 를 참조하십시오.

**조직:** 사용자가 속한 조직의 이름에 대한 스키마 속성.

**기본 이메일:** 사용자의 기본 이메일 주소에 대한 스키마 속성.

**보조 이메일:** 사용자의 보조 이메일 주소에 대한 스키마 속성.

**전화:** 사용자 전화번호에 대한 스키마 속성.

**우편 주소:** 사용자 메일링 주소에 대한 스키마 속성.

**로케일:** ISO 로케일 정보를 포함하는 스키마 속성. 값은 두 글자로 된 언어 코드 또는 언어 및 국가 코드입니다.

**시간대:** 사용자가 위치한 시간대를 포함하는 스키마 속성. 값은 City/Country와 같은 문자열입니다.

**VLV(가상 목록 보기) 컨트롤 사용:** AEM Forms에서 디렉토리 서버에서 데이터를 일괄적으로 검색할 수 있도록 하는 LDAP 컨트롤입니다. Sun One을 LDAP 디렉토리로 사용하고 있으며 디렉토리에 많은 사용자가 포함되어 있는 경우 VLV를 활성화하면 사용자 관리(User Management)에서 사용자를 검색할 때 사용할 수 있는 인덱스가 생성됩니다. 이 기능은 제한된 양의 데이터만 동기화할 수 있는 일반 사용자 계정을 사용할 때 유용합니다. 그룹에 대해 VLV를 활성화할 수도 있습니다. VLV(가상 목록 보기) 컨트롤 사용을 선택한 경우 정렬 필드 상자에 이름을 지정합니다.

>[!NOTE]
>
>VLV를 활성화하려면 Sun One을 구성하십시오. 다음을 참조하십시오 [VLV(가상 목록 보기)를 사용하도록 사용자 관리 구성](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**정렬 필드:** VLV(가상 목록 보기) 제어 사용을 선택한 경우 인덱스 정렬에 사용되는 속성 이름을 지정합니다. 이 속성 이름(예: uid)은 디렉토리 서버에서 VLV에 대한 인덱스를 생성할 때 지정한 이름입니다.

### 그룹 설정 {#group-settings}

**고유 식별자:** (필수) 그룹을 식별하는 데 사용되는 고유한 상수 속성입니다. DN 이외의 속성을 고유 식별자로 사용합니다. 이 설정은 디렉터리 서버에 따라 다릅니다. 값은 Active Directory 2003의 objectGUID, Sun One의 고유 ID 및 eDirectory의 guid입니다.

>[!NOTE]
>
>조직에서 고유하도록 보장된 속성을 입력해야 합니다. 잘못된 값을 입력하면 심각한 시스템 문제가 발생할 수 있습니다.

**기본 DN:** (필수) 기본 디렉터리 고유 이름입니다.

기본 DN은 관리 콘솔의 필수 설정이지만 IBM Domino Enterprise Server와 같은 일부 디렉터리 서버에는 빈 BaseDN이 필요합니다. 빈 기본 DN을 지정하려면 config.xml 파일을 내보내고 config.xml 파일에서 설정을 편집한 다음 다시 가져옵니다. (참조: [구성 파일 가져오기 및 내보내기](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**검색 필터:** (필수) 그룹과 관련된 레코드를 찾는 데 사용할 검색 필터입니다. 한 수준 검색이나 하위 수준 검색을 수행할 수 있습니다.

**설명:** 그룹 설명에 대한 스키마 속성

**전체 이름:** (필수) 그룹의 전체 이름에 대한 스키마 속성

**구성원 DN:** (필수) 그룹 내 구성원의 고유 이름에 대한 스키마 속성

**구성원 고유 식별자:** 선택한 그룹의 구성원인 사용자 또는 그룹에 대한 고유 식별자입니다. 이 값은 디렉토리 서버에 따라 다릅니다. 값은 AD2003의 objectSID, Sun One의 nuniqueID 및 eDirectory의 guid입니다.

멤버 DN이 DN이 아닌 속성으로 지정된 경우 User Management는 멤버 고유 식별자를 사용하여 LDAP를 질의하여 사용자의 DN이 고유 식별자 값에 해당하므로 해당 DN을 수집합니다.

DN이 고유 식별자로 지정된 경우 멤버 고유 식별자를 구성할 필요가 없습니다.

**조직:** 그룹이 속한 조직 이름에 대한 스키마 속성

**기본 이메일:** 그룹의 기본 이메일 주소에 대한 스키마 속성

**보조 이메일:** 그룹의 보조 이메일 주소에 대한 스키마 속성

**타임스탬프 수정:** 델타 디렉토리 동기화를 활성화하려면 이 값을 설정하여 타임스탬프를 수정합니다. 델타 디렉토리 동기화 활성화 를 참조하십시오.

**VLV(가상 목록 보기) 컨트롤 사용:** AEM Forms에서 디렉토리 서버에서 데이터를 일괄적으로 검색할 수 있도록 하는 LDAP 컨트롤입니다. Sun One을 LDAP 디렉토리로 사용하고 있고 디렉토리에 많은 그룹이 포함되어 있는 경우 VLV를 활성화하면 User Management에서 그룹을 검색할 때 사용할 수 있는 인덱스가 만들어집니다. 이 기능은 제한된 양의 데이터만 동기화할 수 있는 일반 사용자 계정을 사용할 때 유용합니다. 사용자에 대해 VLV를 활성화할 수도 있습니다. VLV(가상 목록 보기) 컨트롤 사용을 선택한 경우 정렬 필드 이름을 지정합니다.

>[!NOTE]
>
>VLV를 활성화하려면 Sun One을 구성하십시오. 다음을 참조하십시오 [VLV(가상 목록 보기)를 사용하도록 사용자 관리 구성](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**정렬 필드 이름:** VLV(가상 목록 보기) 제어 사용을 선택한 경우 인덱스 정렬에 사용되는 속성 이름을 지정합니다. 이 속성 이름은 디렉토리 서버에서 VLV에 대한 인덱스를 만들 때 지정한 이름입니다.

>[!NOTE]
>
>테스트 를 클릭하여 사용자 및 그룹 설정이 기본 DN 및 검색 기준에 따라 수집되는지 확인합니다.

사용자 및 그룹이 반환되면 속성 세트에 따라 각 필드에 할당된 값이 결과에 표시됩니다.

>[!NOTE]
>
>User Management는 도메인 내에서 중복 사용자 ID를 지원하지 않습니다. 사용자 ID가 있는 사용자 한 명만 동기화됩니다.

## VLV(가상 목록 보기)를 사용하도록 사용자 관리 구성 {#configure-user-management-to-use-virtual-list-view-vlv}

디렉터리 동기화는 사용자 관리의 중요한 요구 사항입니다. 사용자 및 그룹은 Enterprise 디렉토리에서 AEM Forms 데이터베이스로 동기화되어 롤 및 권한을 할당합니다. 사용자 수는 요구 사항에 따라 100명에서 100000+까지 다양하며, 데이터를 효율적으로 동기화하는 것은 엔지니어링의 과제를 안고 있다.

LDAP 프로토콜은 요청 컨트롤을 사용하여 페이지 번호를 매긴 방식으로 대용량 데이터 세트를 쿼리하는 메커니즘을 제공합니다. Microsoft Active Directory를 사용하는 경우 AEM Forms 데이터베이스 동기화에 대한 LDAP는 특정 크기의 배치로 데이터를 검색하기 위해 PagedResultsControl을 사용합니다. Sun ONE Directory Server는 이 컨트롤을 지원하지 않습니다. Sun ONE Directory Server에 대해 페이지가 매겨진 쿼리를 완료하려면 VLV(Virtual List View) 컨트롤을 사용하십시오. 이 컨트롤에는 디렉터리 서버측 구성과 클라이언트측 구현이 모두 포함됩니다.

>[!NOTE]
>
>이 절에서는 Sun ONE Directory Server에 VLV 컨트롤을 사용하는 방법에 대해 설명합니다. 그러나 이 컨트롤은 VLV 컨트롤을 지원하는 모든 디렉터리 서버에 사용할 수 있습니다.

1. 디렉토리를 구성할 때 [사용자 설정] 페이지와 [그룹 설정] 페이지 모두에서 [가상 목록 보기(VLV) 제어 사용]을 선택합니다. 확인란을 선택할 때는 정렬 필드 상자에 정렬 이름도 지정해야 합니다. 기본값은 uid입니다. (참조: [디렉터리 또는 사용자 지정 SPI 추가](configuring-directories.md#adding-directories-or-custom-spis) 또는 [디렉터리 편집](configuring-directories.md#edit-a-directory).)
1. Sun ONE 관리 콘솔 또는 명령줄 스크립트를 사용하여 사용자 및 그룹에 대한 LDAP VLV 항목을 만듭니다. 명령줄 스크립트를 사용하는 경우 샘플 사용자 및 그룹 LDIF 파일을 사용할 수 있습니다. (참조: [VLV용 Sun ONE Directory Server 구성](configuring-directories.md#configuring-the-sun-one-directory-server-for-vlv).)
1. 서버를 중지하고 필요한 인덱스를 만듭니다. (참조: [VLV에 대한 디렉터리 서버 인덱스 만들기](configuring-directories.md#create-the-directory-server-index-for-vlv).)

### VLV용 Sun ONE Directory Server 구성 {#configuring-the-sun-one-directory-server-for-vlv}

VLV를 만들려면 다음을 포함하는 항목 쌍이 필요합니다. `vlvSearch` 및 `vlvIndex` 객체 클래스. vlvSearch 항목에는 검색 기준과 `vlvFilter` attribute - 정렬할 특성이 포함된 개체 클래스를 지정합니다. 다음 `vlvIndex` 객체 클래스는 `vlvSort` attribute - 정렬할 속성 및 정렬 순서를 지정합니다. (빼기 기호(-)는 알파벳 역순을 나타냅니다.) AEM Forms에서 VLV를 사용하려면 사용자 및 그룹에 대한 별도의 항목이 필요합니다.

>[!NOTE]
>
>개체 항목은 Sun ONE GUI(그래픽 사용자 인터페이스)를 사용하거나 명령줄 스크립트를 통해 만들 수 있습니다. GUI를 사용하여 개체 항목을 만드는 방법에 대한 지침은 Sun ONE 설명서를 참조하십시오.

다음은 사용자의 VLV 항목용 샘플 스크립트 LDIF입니다.

```text
 dn: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 objectclass: top
 objectclass: vlvSearch
 cn: lcuser
 vlvBase: dc=corp,dc=adobe,dc=com
 vlvScope: 2
 vlvFilter: (&(objectclass=inetOrgPerson))
 aci: (target="ldap:///cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config")(targetattr="*")(version 3.0; acl "Config"
 ;allow(read,search,compare) userdn="ldap:///all"; )
 dn: cn=lcuser,cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 cn: lcuser
 vlvSort: cn
 objectclass: top
 objectclass: vlvIndex
```

**스크립트를 사용하여 개체 항목 만들기**

1. 샘플 스크립트에는 이름이 인 LDAP 항목이 있습니다. `lcuser`. 이 항목은 AEM Forms에서 사용자 동기화를 위한 VLV 관련 구성에 사용됩니다. 다음 속성을 적절하게 수정합니다.

   **항목 이름:** 이 샘플의 항목 이름은 입니다. `lcuser`. If `lcuser` 가 변경되면 샘플 스크립트의 모든 영역에서 가 변경되어야 합니다.

   **vlvBase:** 사용자 설정 페이지에 지정된 기본 DN입니다.

   **vlvFilter:** 사용자 설정 페이지에 지정된 검색 필터.

   **vlvSort:** 사용자 설정 페이지의 VLV 설정 섹션에 지정된 정렬 필드입니다. VLV 컨트롤을 사용하려면 정렬 컨트롤을 지정해야 합니다. 이 필드는 만든 vlv 인덱스의 정렬 매개 변수로 사용됩니다.

   **aci:** 샘플 스크립트에 지정된 액세스 컨트롤은 인증된 사용자에게 읽기, 검색 및 비교 작업을 위해 VLV 인덱스에 액세스할 수 있는 권한을 부여합니다. 관리자는 사용자 관리 사용자 인터페이스에 지정된 디렉토리 서버 설정 페이지에서 구성된 바인딩 사용자에 대한 액세스를 제한할 수 있습니다. 권한이 제공되지 않으면 사용자 검색에서 VLV를 사용할 수 없고 LDAP 서버에서 권한 예외가 발생합니다.

   >[!NOTE]
   >
   >vlvIndex 항목 이름도 일반적으로 로 설정됩니다. `lcuser`, 그러나 다른 이름을 지정할 수 있습니다. vlvindex 도구에서 동일한 이름을 사용합니다. (참조: [VLV에 대한 디렉터리 서버 인덱스 만들기&#x200B;](configuring-directories.md#create-the-directory-server-index-for-vlv)*.)*

1. 사용 `ldapmodify` sun ONE Server와 함께 제공되는 툴은 그룹의 기본 DN, 검색 필터 및 정렬 필드를 각각 사용하여 그룹에 대해 유사한 항목을 생성합니다.

   `server directory\shared\bin>ldapmodify -v -a -h host -p port -D "admin user" -w "password" -f "LDIF file location"`

   예를 들어, 다음 텍스트를 입력합니다.

   `D:\tools\ldap\sun\shared\bin> -v -a -h localhost -p 55850 -D "uid=admin,ou=administrators,ou=topologymanagement,o=netscaperoot" -w "admin" -f "D:\tools\ldap\data\vlv feature\users.ldif"`

### VLV에 대한 디렉터리 서버 인덱스 만들기 {#create-the-directory-server-index-for-vlv}

디렉터리 설정을 구성하고 사용자 및 그룹에 대한 LDAP VLV 항목을 만든 후 서버를 중지하고 필요한 인덱스를 만듭니다.

1. 개체 항목을 만든 후 Sun ONE Server를 중지합니다.
1. vlvindex 도구를 사용하여 다음 텍스트를 입력하여 인덱스를 생성합니다.

   *디렉토리 서버 인스턴스* `\vlvindex.bat -n userRoot -T lcuser`

   다음 출력이 생성됩니다.

   ```shell
    D:\tools\ldap\sun\shared\bin>..\..\slapd-chetanmeh-xp3\vlvindex.bat -n userRoot -T livecycle
    [21/Nov/2007:16:47:26 +051800] - userRoot: Indexing VLV: livecycle
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 1000 entries (5%).
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 2000 entries (9%).
    ...
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 20000 entries (94%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 21000 entries (99%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Finished indexing.
   ```

   vlvindex 도구는 디렉토리 서버 인스턴스 디렉토리에 있습니다. Sun ONE Server에 server1과 server2를 실행하는 인스턴스가 두 개 있는 경우 vlvindex 툴이 *Sun ONE 서버 디렉토리*\server1 디렉터리입니다. 매개 변수 값 `-T` 은(는) 의 값입니다 `cn` 샘플 LDIF에서 이전에 만든 vlvindex 항목의 특성입니다. 이 경우 `lcuser`.

1. 그룹에 대해서도 VLV를 사용할 수 있는 경우 그룹에 대해 해당 인덱스를 만듭니다. 다음 명령을 실행하여 색인이 생성되었는지 확인합니다.

   *sun one 서버 디렉토리* `\shared\bin>ldapsearch -h`*호스트 이름* `-p`*포트 번호* `-s base -b "" objectclass=*`

   다음 샘플 데이터와 같은 출력이 생성됩니다.

   ```shell
    D:\tools\ldap\sun\shared\bin>ldapsearch.exe -h localhost -p 55850 -s base -b "" objectclass=*
    ldapsearch.exe: started Tue Nov 27 16:34:20 2007
    version: 1
    dn:
    objectClass: top
    namingContexts: dc=corp,dc=adobe,dc=com
    supportedExtension: 2.16.840.1.113730.3.5.7
    ...
    vlvsearch: cn=MCC ou=testdata dc=corp dc=adobe dc=com, cn=userRoot,cn=ldbm dat
        abase,cn=plugins,cn=config
    vlvsearch: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
    vlvsearch: cn=Browsing ou=testdata,cn=userRoot,cn=ldbm database,cn=plugins,cn=
        config
    1 matches
   ```
