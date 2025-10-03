---
title: 디렉터리 구성
description: 디렉터리를 추가하고 편집하며 삭제하고 가상 목록 보기를 사용하도록 사용자 관리를 구성하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 30edcef2-e8fa-403a-9850-b8dfeeb9ac65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e9afc12af78140ae0ec12cc2ee95fc9e175f8d94
workflow-type: ht
source-wordcount: '3241'
ht-degree: 100%

---


# 디렉터리 구성 {#configuring-directories}

구성하는 각 엔터프라이즈 도메인에 대해 인증 공급자가 사용자 정보를 쿼리하는 디렉터리를 지정합니다. 한 도메인에 여러 디렉터리를 구성할 수 있습니다.

## 디렉터리 또는 사용자 정의 SPI 추가 {#adding-directories-or-custom-spis}

구성하는 각 엔터프라이즈 도메인에 대해 인증 공급자가 사용자 정보를 쿼리하는 디렉터리를 지정합니다. 기존 엔터프라이즈 도메인이나 새로 추가하는 엔터프라이즈 도메인에 디렉터리를 추가할 수 있습니다. 한 도메인에 여러 디렉터리를 구성할 수 있습니다. 동기화를 위해 사용자 정의 서비스 공급자 인터페이스(SPI)를 사용하도록 도메인을 구성할 수도 있습니다.

### 디렉터리 추가 {#add-a-directory}

>[!NOTE]
>
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리를 클릭합니다.
1. 새 엔터프라이즈 도메인을 클릭하거나 기존 엔터프라이즈 도메인을 선택합니다.
1. 디렉터리 추가를 클릭합니다.
1. 프로필 이름 상자에 이 디렉터리를 구별하는 이름을 입력한 후 다음을 클릭합니다.
1. 디렉터리 서버 설정을 구성합니다. ([디렉터리 설정](configuring-directories.md#directory-settings)을 참조하십시오.)
1. LDAP 서버에 연결할 수 있는지 확인하려면 테스트를 클릭합니다. 테스트가 실패하면 애플리케이션 서버 로그 파일에서 예외를 검토하여 실패의 근본 원인을 파악합니다. 닫기를 클릭한 후 다음을 클릭합니다.
1. 사용자 설정을 선택하고 필요에 따라 해당 설정을 구성합니다. ([디렉터리 설정](configuring-directories.md#directory-settings)을 참조하십시오.)
1. 기본 DN과 구성된 다른 속성이 올바른 사용자 배치를 수집하는지 확인하려면 테스트를 클릭합니다. LDAP에서 제공된 설정(예: 기본 DN, 검색 필터, 모든 속성)을 사용하여 처음 200개 레코드를 가져오려고 시도합니다.

   사용자가 반환되면 결과에는 속성 집합에 따라 각 필드에 할당된 값이 표시됩니다. 서버 이름이 존재하지 않거나, 인증 정보가 잘못되었거나, 속성이 잘못되어 테스트가 실패하면 다음과 같은 오류 메시지가 나타납니다. “지정된 검색 기준에 따라 결과가 반환되지 않았습니다.” 실패의 근본 원인을 파악하려면 애플리케이션 서버 로그 파일에서 예외를 검토합니다. 닫기를 클릭한 후 다음을 클릭합니다.

1. 그룹 설정을 선택하고 필요에 따라 해당 설정을 구성합니다. ([디렉터리 설정](configuring-directories.md#directory-settings)을 참조하십시오.)
1. 기본 DN과 구성된 다른 속성이 올바른 그룹 배치를 수집하는지 확인하려면 테스트를 클릭합니다. 그룹이 반환되면 결과에는 속성 집합에 따라 각 필드에 할당된 값이 표시됩니다. 닫기를 클릭합니다.

### 사용자 정의 SPI 추가 {#add-a-custom-spi}

사용자 정의 SPI를 만드는 방법에 대한 자세한 내용은 [AEM Forms를 사용한 프로그래밍](https://www.adobe.com/go/learn_aemforms_programming_63)의 &#39;AEM Forms용 SPI 개발&#39;을 참조하십시오. 새로 배포된 사용자 정의 SPI를 도메인과 연결되도록 하려면 서버를 다시 시작하십시오.

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리를 클릭합니다.
1. 새 엔터프라이즈 도메인을 클릭하거나 기존 엔터프라이즈 도메인을 선택합니다.
1. 디렉터리 추가를 클릭합니다.
1. 프로필 이름 상자에 이름을 입력하고 사용자 정의 SPI 공급자를 선택한 후 다음을 클릭합니다.
1. 목록에서 사용자 정의 사용자 공급자를 선택하고 다음을 클릭합니다.
1. 목록에서 사용자 정의 그룹 공급자를 선택하고 완료를 클릭합니다.

## 디렉터리 편집 {#edit-a-directory}

이전에 구성한 디렉터리의 세부 정보를 편집할 수 있습니다.

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리를 클릭합니다.
1. 목록에서 적절한 도메인을 클릭하고 표시되는 페이지의 목록에서 적절한 디렉터리를 선택합니다.
1. 필요에 따라 디렉터리, 사용자 및 그룹 설정을 구성합니다. ([디렉터리 설정](configuring-directories.md#directory-settings)을 참조하십시오.)
1. 확인을 클릭합니다.

## 디렉터리 삭제 {#delete-a-directory}

디렉터리를 삭제한 후 도메인을 동기화하면 해당 디렉터리에 있는 모든 사용자 및 그룹이 데이터베이스에서 더 이상 사용되지 않는 것으로 표시됩니다. 관리 콘솔에서 검색해도 해당 사용자 및 그룹이 반환되지 않습니다.

>[!NOTE]
>
>엔터프라이즈 도메인에는 인증 공급자와 디렉터리 공급자가 하나 이상 필요합니다.

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리를 클릭합니다.
1. 목록에서 해당 도메인을 클릭합니다.
1. 해당 디렉터리의 확인란을 선택하고 삭제를 클릭합니다.
1. 확인 페이지가 나타나면 확인을 클릭하고 다시 확인을 클릭합니다.

## 디렉터리 설정 {#directory-settings}

도메인에 디렉터리를 추가할 때 다음과 같은 디렉터리 설정을 지정합니다.

**서버:** (필수) 디렉터리 서버의 정규화된 도메인 이름(FQDN)입니다. 예를 들어 adobe. com 네트워크에 있는 x라는 컴퓨터의 경우 FQDN은 x. adobe. com입니다. FQDN 서버 이름 대신 IP 주소를 사용할 수 있습니다.

**포트:** (필수) 디렉터리 서버에서 사용하는 포트입니다. 일반적으로 389이거나 네트워크를 통해 인증 정보를 전송하는 데 SSL(Secure Sockets Layer) 프로토콜을 사용하는 경우에는 636입니다.

**SSL:** (필수) 디렉터리 서버에서 네트워크를 통해 데이터를 전송할 때 SSL을 사용할지 여부를 지정합니다. 기본값은 아니요입니다. 예로 설정하면 해당 LDAP 서버 인증서는 애플리케이션 서버의 Java™ 런타임 환경(JRE)에서 신뢰할 수 있어야 합니다.

**바인딩** (필수) 디렉터리에 액세스하는 방법을 지정합니다.

**익명:** 사용자 이름 또는 암호가 필요하지 않습니다. 익명 사용자는 제한된 양의 데이터만 가져올 수 있습니다. 이 옵션은 초기 테스트에 유용할 수 있습니다.

**사용자:** 인증이 필요합니다. 이름 상자에 디렉터리에 액세스할 수 있는 사용자 레코드 이름을 지정합니다. 사용자 계정의 전체 고유 이름(DN)을 입력하는 것이 가장 좋습니다(예: cn=Jane Doe, ou=user, dc=can, dc=com). 암호 상자에 연결된 암호를 지정합니다. 해당 설정은 바인딩 옵션으로 사용자를 선택할 때 필요합니다.

**이름:** 익명 액세스가 활성화되지 않은 경우 LDAP 데이터베이스에 연결하는 데 사용할 수 있는 이름입니다. Active Directory 2003의 경우 `[domain name]\[userid]`를 지정합니다. Sun™ One, eDirectory 또는 IBM Tivoli Directory Server의 경우 uid=lcuser,ou=it,o=company.com과 같이 사용자의 정규화된 이름을 지정합니다.

**암호:** 익명 액세스가 활성화되지 않은 경우 LDAP 데이터베이스에 연결하기 위해 지정한 이름에 해당하는 암호입니다.

**다음 값으로 페이지 채우기:** 이 구성을 선택하면 사용자 및 그룹 설정 페이지의 속성이 해당 기본 LDAP 값으로 채워집니다.

**기본 DN 가져오기:** 기본 DN을 가져와서 드롭다운 목록에 표시합니다. 이 설정은 여러 개의 기본 DN이 있고 값을 선택해야 할 때 유용합니다.

**참조 활성화:** 이 설정은 조직에서 계층 구조로 구성된 여러 Active Directory 도메인을 사용하고 상위 도메인에 대해서만 디렉터리 설정을 지정한 경우에 적용됩니다. 이러한 상황에서 이 옵션을 선택하면 사용자 관리자에서 하위 도메인의 사용자 및 그룹 세부 정보에 액세스할 수 있습니다.

>[!NOTE]
>
>테스트를 클릭하여 LDAP 서버에 연결할 수 있는지 확인하십시오. 모든 실패의 근본 원인을 파악하려면 애플리케이션 서버 로그 파일에서 예외를 검토합니다.

### 사용자 설정 {#user-settings}

**고유 식별자:** (필수) 사용자를 식별하는 데 사용되는 고유하고 변하지 않는 속성입니다. 사용자가 조직 내 다른 부서로 이동하면 사용자 DN이 변경될 수 있으므로 고유 식별자로 DN이 아닌 속성을 사용하십시오. 이 설정은 디렉터리 서버에 따라 달라집니다. 해당 값은 Active Directory 2003의 경우 objectGUID이고, Sun™ One의 경우 nsuniqueID이고, eDirectory의 경우 guid입니다.

>[!NOTE]
>
>조직에서 고유함이 보장되는 속성을 입력하십시오. 잘못된 값을 입력하면 심각한 시스템 문제가 발생할 수 있습니다.

**기본 DN:** LDAP 계층에서 사용자 및 그룹을 동기화하기 위한 시작점으로 설정합니다. 서비스를 위해 동기화해야 하는 모든 사용자 및 그룹을 포함하는 가장 낮은 수준의 계층에서 기본 DN을 지정하는 것이 가장 좋습니다.

디렉터리 설정에서 참조 활성화 옵션을 선택한 경우 기본 DN 옵션을 DN의 *dc* 부분으로 설정합니다. 참조가 작동하려면 검색 범위에 상위 도메인과 하위 도메인이 모두 포함되어야 합니다.

>[!NOTE]
>
>해당 설정에 사용자의 DN을 포함하지 마십시오. 특정 사용자를 동기화하려면 검색 필터 설정을 사용합니다.

기본 DN은 관리 콘솔에서 필수 설정이지만 IBM Domino Enterprise Server와 같은 일부 디렉터리 서버에서는 비어 있는 BaseDN이 필요할 수 있습니다. 비어 있는 기본 DN을 지정하려면 config. xml 파일을 내보내고 config. xml 파일의 설정을 편집한 후 다시 가져옵니다. ([구성 파일 가져오기 및 내보내기](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)를 참조하십시오.)

**검색 필터:** (필수) 사용자와 연결된 레코드를 찾는 데 사용할 검색 필터입니다. 한 수준 검색이나 하위 수준 검색을 수행할 수 있습니다. (검색 필터 구문 또는 RFC 2254를 참조하십시오.) Microsoft AD 스키마에 대한 추가 정보는 Active Directory 스키마를 참조하십시오.

**설명:** 사용자 설명에 대한 스키마 속성입니다.

**전체 이름:** (필수) 사용자의 전체 이름에 대한 스키마 속성입니다.

**로그인 ID:** (필수) 사용자 로그인 ID에 대한 스키마 속성입니다.

**성:** (필수) 사용자 성에 대한 스키마 속성입니다.

**이름:** (필수) 사용자 이름에 대한 스키마 속성입니다.

**이니셜:** 사용자 이니셜에 대한 스키마 속성입니다.

**비즈니스 캘린더:** 이 설정(비즈니스 캘린더 키) 값에 따라 비즈니스 캘린더를 사용자에게 매핑할 수 있습니다. 비즈니스 캘린더는 영업일과 비영업일을 정의합니다. AEM Forms는 미리 알림, 기한, 에스컬레이션과 같은 이벤트에 대한 미래 일자 및 시간을 계산할 때 비즈니스 캘린더를 사용할 수 있습니다. 사용자에게 비즈니스 캘린더 키를 할당하는 방법은 엔터프라이즈, 로컬 또는 하이브리드 도메인을 사용하는지에 따라 달라집니다. (비즈니스 캘린더 구성을 참조하십시오.)

엔터프라이즈 도메인을 사용하는 경우 비즈니스 캘린더 설정을 LDAP 디렉터리 필드에 매핑할 수 있습니다. 예를 들어 디렉터리의 각 사용자 레코드에 *국가* 필드가 포함되어 있고 사용자가 위치한 국가에 따라 비즈니스 캘린더를 할당하려는 경우 비즈니스 캘린더 설정 값으로 *국가* 필드 이름을 지정합니다. 그런 다음, 비즈니스 캘린더 키(LDAP 디렉터리의 *국가* 필드에 정의된 값)를 Forms Workflow의 비즈니스 캘린더에 매핑할 수 있습니다.

Forms Workflow 페이지에서 비즈니스 캘린더 키 이름을 표시하는 데 사용되는 공간은 제한되어 있습니다. 해당 페이지에서 비즈니스 캘린더 키 이름이 잘리지 않도록 이름을 53자 미만으로 제한하십시오.

**타임스탬프 수정:** 델타 디렉터리 동기화를 활성화하려면 이 값을 설정하여 타임스탬프를 수정합니다. (델타 디렉터리 동기화 활성화를 참조하십시오.)

**조직:** 사용자가 속한 조직 이름에 대한 스키마 속성입니다.

**기본 이메일:** 사용자의 기본 이메일 주소에 대한 스키마 속성입니다.

**보조 이메일:** 사용자의 보조 이메일 주소에 대한 스키마 속성입니다.

**전화번호:** 사용자의 전화번호에 대한 스키마 속성입니다.

**우편 주소:** 사용자의 우편 주소에 대한 스키마 속성입니다.

**로케일:** ISO 로케일 정보를 포함하는 스키마 속성입니다. 이 값은 두 글자 언어 코드이거나 언어 및 국가 코드입니다.

**시간대:** 사용자가 위치한 지역의 시간대를 포함하는 스키마 속성입니다. 이 값은 도시/국가와 같은 문자열입니다.

**가상 목록 보기(VLV) 제어 활성화:** AEM Forms가 디렉터리 서버에서 데이터를 일괄적으로 가져올 수 있도록 하는 LDAP 제어입니다. Sun One을 LDAP 디렉터리로 사용하고 이 디렉터리에 많은 사용자가 있는 경우 VLV를 활성화하면 사용자 관리자에서 사용자를 검색할 때 사용할 수 있는 색인이 생성됩니다. 이 기능은 제한된 양의 데이터만 동기화할 수 있는 일반 사용자 계정을 사용할 때 유용합니다. 그룹에 대해서도 VLV를 활성화할 수 있습니다. 가상 목록 보기(VLV) 제어 활성화를 선택하는 경우 정렬 필드 상자에 이름을 지정합니다.

>[!NOTE]
>
>VLV를 활성화하려면 Sun One을 구성하십시오. [가상 목록 보기(VLV)를 사용하도록 사용자 관리 구성](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv)을 참조하십시오.

**정렬 필드:** 가상 목록 보기(VLV) 제어 활성화를 선택한 경우 색인을 정렬하는 데 사용되는 속성 이름을 지정합니다. 이 속성 이름(예: uid)은 디렉터리 서버에서 VLV에 대한 색인을 만들 때 지정한 이름입니다.

### 그룹 설정 {#group-settings}

**고유 식별자:** (필수) 그룹을 식별하는 데 사용되는 고유하고 변하지 않는 속성입니다. 고유 식별자로 DN이 아닌 속성을 사용하십시오. 이 설정은 디렉터리 서버에 따라 달라집니다. 해당 값은 Active Directory 2003의 경우 objectGUID이고, Sun One의 경우 nsuniqueID이고, eDirectory의 경우 guid입니다.

>[!NOTE]
>
>조직에서 고유함이 보장되는 속성을 입력하십시오. 잘못된 값을 입력하면 심각한 시스템 문제가 발생할 수 있습니다.

**기본 DN:** (필수) 디렉터리의 기본 고유 이름입니다.

기본 DN은 관리 콘솔에서 필수 설정이지만 IBM Domino Enterprise Server와 같은 일부 디렉터리 서버에서는 비어 있는 BaseDN이 필요합니다. 비어 있는 기본 DN을 지정하려면 config. xml 파일을 내보내고 config. xml 파일의 설정을 편집한 후 다시 가져옵니다. ([구성 파일 가져오기 및 내보내기](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)를 참조하십시오.)

**검색 필터:** (필수) 그룹과 연결된 레코드를 찾는 데 사용할 검색 필터입니다. 한 수준 검색이나 하위 수준 검색을 수행할 수 있습니다.

**설명:** 그룹 설명에 대한 스키마 속성입니다.

**전체 이름:** (필수) 그룹의 전체 이름에 대한 스키마 속성입니다.

**멤버 DN:** (필수) 그룹에 속한 멤버의 고유 이름에 대한 스키마 속성입니다.

**멤버 고유 식별자:** 선택한 그룹의 멤버인 사용자 또는 그룹의 고유 식별자입니다. 이 값은 디렉터리 서버에 따라 달라집니다. 해당 값은 AD2003의 경우 objectSID이고, Sun One의 경우 nsuniqueID이고, eDirectory의 경우 guid입니다.

멤버 DN이 DN이 아닌 속성과 함께 지정된 경우 사용자 관리에서는 멤버 고유 식별자를 사용하여 LDAP를 쿼리하고 고유 식별자 값에 해당하는 사용자 DN을 수집합니다.

DN을 고유 식별자로 지정한 경우 멤버 고유 식별자를 구성할 필요가 없습니다.

**조직:** 그룹이 속한 조직 이름에 대한 스키마 속성입니다.

**기본 이메일:** 그룹의 기본 이메일 주소에 대한 스키마 속성입니다.

**보조 이메일:** 그룹의 보조 이메일 주소에 대한 스키마 속성입니다.

**타임스탬프 수정:** 델타 디렉터리 동기화를 활성화하려면 이 값을 설정하여 타임스탬프를 수정합니다. (델타 디렉터리 동기화 활성화를 참조하십시오.)

**가상 목록 보기(VLV) 제어 활성화:** AEM Forms가 디렉터리 서버에서 데이터를 일괄적으로 가져올 수 있도록 하는 LDAP 제어입니다. Sun One을 LDAP 디렉터리로 사용하고 이 디렉터리에 많은 그룹이 있는 경우 VLV를 활성화하면 사용자 관리자에서 그룹을 검색할 때 사용할 수 있는 색인이 생성됩니다. 이 기능은 제한된 양의 데이터만 동기화할 수 있는 일반 사용자 계정을 사용할 때 유용합니다. 사용자에 대해서도 VLV를 활성화할 수 있습니다. 가상 목록 보기(VLV) 제어 활성화를 선택하는 경우 정렬 필드 이름을 지정합니다.

>[!NOTE]
>
>VLV를 활성화하려면 Sun One을 구성하십시오. [가상 목록 보기(VLV)를 사용하도록 사용자 관리 구성](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv)을 참조하십시오.

**정렬 필드 이름:** 가상 목록 보기(VLV) 제어 활성화를 선택한 경우 색인을 정렬하는 데 사용되는 속성 이름을 지정합니다. 이 속성 이름은 디렉터리 서버에서 VLV에 대한 색인을 만들 때 지정한 이름입니다.

>[!NOTE]
>
>테스트를 클릭하여 사용자 및 그룹 설정이 기본 DN 및 검색 기준에 따라 수집되는지 확인하십시오.

사용자 및 그룹이 반환되면 결과에는 속성 집합에 따라 각 필드에 할당된 값이 표시됩니다.

>[!NOTE]
>
>사용자 관리에서는 도메인 내에서 중복된 사용자 ID를 지원하지 않습니다. 해당 사용자 ID를 가진 사용자 한 명만 동기화됩니다.

## 가상 목록 보기(VLV)를 사용하도록 사용자 관리 구성 {#configure-user-management-to-use-virtual-list-view-vlv}

디렉터리 동기화는 사용자 관리에 중요한 요구 사항입니다. 사용자 및 그룹은 역할과 권한을 할당하기 위해 엔터프라이즈 디렉터리에서 AEM Forms 데이터베이스로 동기화됩니다. 사용자 수는 요구 사항에 따라 100명에서 100,000명 이상까지 다양하며, 이에 따라 엔지니어링 측면에서 데이터를 효율적으로 동기화하는 것이 도전 과제가 됩니다.

LDAP 프로토콜은 요청 제어를 사용하여 페이지 지정 방식으로 대규모 데이터 집합을 쿼리하는 메커니즘을 제공합니다. Microsoft Active Directory를 사용하는 경우 LDAP와 AEM Forms 데이터베이스 동기화는 특정 크기 배치로 데이터를 가져오기 위해 PagedResultsControl을 사용합니다. Sun ONE Directory Server는 이 제어를 지원하지 않습니다. Sun ONE Directory Server에 대한 페이지 지정 쿼리를 완료하려면 가상 목록 보기(VLV) 제어를 사용합니다. 이 제어에는 디렉터리 서버측 구성과 클라이언트측 구현이 모두 포함됩니다.

>[!NOTE]
>
>이 섹션에서는 Sun ONE Directory Server에서 VLV 제어를 사용하는 방법을 설명합니다. 하지만 VLV 제어를 지원하는 모든 디렉터리 서버에서 이 제어를 사용할 수 있습니다.

1. 디렉터리를 구성할 때 사용자 설정 페이지와 그룹 설정 페이지 모두에서 가상 목록 보기(VLV) 제어 활성화를 선택합니다. 확인란을 선택하면 정렬 필드 상자에 정렬 이름도 지정해야 합니다. 기본값은 uid입니다. ([디렉터리 또는 사용자 정의 SPI 추가](configuring-directories.md#adding-directories-or-custom-spis) 또는 [디렉터리 편집](configuring-directories.md#edit-a-directory)을 참조하십시오.)
1. Sun ONE 관리 콘솔이나 명령줄 스크립트를 사용하여 사용자 및 그룹에 대한 LDAP VLV 항목을 만듭니다. 명령줄 스크립트를 사용하면 샘플 사용자 및 그룹 LDIF 파일을 사용할 수 있습니다. ([VLV용 Sun ONE 디렉터리 서버 구성](configuring-directories.md#configuring-the-sun-one-directory-server-for-vlv)을 참조하십시오.)
1. 서버를 중지하고 필요한 색인을 만듭니다. ([VLV용 디렉터리 서버 색인 만들기](configuring-directories.md#create-the-directory-server-index-for-vlv)를 참조하십시오.)

### VLV용 Sun ONE 디렉터리 서버 구성 {#configuring-the-sun-one-directory-server-for-vlv}

VLV를 만들려면 `vlvSearch` 및 `vlvIndex` 오브젝트 클래스를 포함하는 항목 쌍이 필요합니다. vlvSearch 항목에는 검색 기준과 정렬하려는 속성이 포함된 오브젝트 클래스를 지정하는 `vlvFilter` 속성이 포함됩니다. `vlvIndex` 오브젝트 클래스에는 정렬할 하나 이상의 속성과 속성 정렬 순서를 지정하는 `vlvSort` 속성이 포함됩니다. (빼기 기호(-)는 알파벳 역순을 나타냅니다). AEM Forms와 함께 VLV를 사용하려면 사용자 및 그룹에 대해 별도의 항목이 필요합니다.

>[!NOTE]
>
>오브젝트 항목은 Sun ONE 그래픽 사용자 인터페이스(GUI)를 사용하거나 명령줄 스크립트를 통해 만들 수 있습니다. GUI를 사용하여 오브젝트 항목을 만드는 방법에 대한 지침은 Sun ONE 설명서를 참조하십시오.

다음은 사용자의 VLV 항목에 대한 샘플 스크립트 LDIF입니다.

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

**스크립트를 사용하여 오브젝트 항목 만들기**

1. 샘플 스크립트에는 `lcuser`라는 LDAP 항목이 있습니다. 이 항목은 AEM Forms의 사용자 동기화를 위한 VLV 관련 구성을 위한 것입니다. 다음 속성을 그에 따라 수정하십시오.

   **항목 이름:** 이 샘플의 항목 이름은 `lcuser`입니다. `lcuser`가 변경되면 샘플 스크립트의 모든 영역에서 해당 이름을 변경해야 합니다.

   **vlvBase:** 사용자 설정 페이지에 지정된 기본 DN입니다.

   **vlvFilter:** 사용자 설정 페이지에 지정된 검색 필터입니다.

   **vlvSort:** 사용자 설정 페이지의 VLV 설정 섹션에 지정된 정렬 필드입니다. VLV 제어를 사용하려면 정렬 제어를 지정해야 합니다. 이 필드는 생성된 vlv 색인에 대한 정렬 매개변수로 사용됩니다.

   **aci:** 샘플 스크립트에 지정된 액세스 제어는 인증된 모든 사용자에게 VLV 색인에 액세스할 수 있는 권한을 부여하여 읽기, 검색, 비교 작업을 수행할 수 있도록 합니다. 관리자는 사용자 관리 사용자 인터페이스에 지정된 디렉터리 서버 설정 페이지에서 구성된 바인딩 사용자에 대한 액세스를 제한할 수 있습니다. 권한이 부여되지 않으면 사용자 검색에서 VLV를 사용할 수 없으며 LDAP 서버에서 권한 예외가 발생합니다.

   >[!NOTE]
   >
   >관례에 따라 vlvIndex 항목 이름도 `lcuser`로 설정되지만 다른 이름을 지정할 수도 있습니다. vlvindex 도구에서 동일한 이름을 사용하십시오. ([VLV용 디렉터리 서버 색인 만들기&#x200B;](configuring-directories.md#create-the-directory-server-index-for-vlv)*를 참조하십시오.)*

1. Sun ONE Server와 함께 제공되는 `ldapmodify` 도구를 사용하여 그룹의 기본 DN, 검색 필터, 정렬 필드를 각각 사용함으로써 그룹에 대한 유사한 항목을 만듭니다.

   `server directory\shared\bin>ldapmodify -v -a -h host -p port -D "admin user" -w "password" -f "LDIF file location"`

   예를 들어 다음 텍스트를 입력합니다.

   `D:\tools\ldap\sun\shared\bin> -v -a -h localhost -p 55850 -D "uid=admin,ou=administrators,ou=topologymanagement,o=netscaperoot" -w "admin" -f "D:\tools\ldap\data\vlv feature\users.ldif"`

### VLV용 디렉터리 서버 색인 만들기 {#create-the-directory-server-index-for-vlv}

디렉터리 설정을 구성하고 사용자 및 그룹에 대한 LDAP VLV 항목을 만든 후 서버를 중지하고 필요한 색인을 만듭니다.

1. 오브젝트 항목을 만든 후 Sun ONE Server를 중지합니다.
1. vlvindex 도구를 사용하여 다음 텍스트를 입력하고 색인을 생성합니다.

   *디렉터리 서버 인스턴스* `\vlvindex.bat -n userRoot -T lcuser`

   생성되는 출력은 다음과 같습니다.

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

   vlvindex 도구는 디렉터리 서버 인스턴스 디렉터리에 있습니다. Sun ONE Server에 server1과 server2를 실행하는 두 개의 인스턴스가 있는 경우 vlvindex 도구는 *Sun ONE server directory*\server1 디렉터리에 있습니다. 매개변수 `-T` 값은 이전에 샘플 LDIF에서 생성된 vlvindex 항목의 `cn` 속성 값입니다. 이 경우에는 `lcuser`입니다.

1. 그룹에 대해서도 VLV를 활성화하는 경우 그룹에 해당하는 색인을 만듭니다. 다음 명령을 실행하여 색인이 생성되었는지 여부를 확인하십시오.

   *sun one server directory* `\shared\bin>ldapsearch -h`*hostname* `-p`*port no* `-s base -b "" objectclass=*`

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
