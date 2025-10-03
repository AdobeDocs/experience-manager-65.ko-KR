---
title: 사용자 관리
description: 사용자 관리를 통해 SAML을 사용하여 AEM Forms 모듈과 Netegrity SiteMinder로 보호되는 애플리케이션 간에 SSO를 활성화할 수 있습니다. 이 문서에서는 사용자 관리에 대한 자세한 정보를 제공합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1da1f6de-ac0d-4e0d-b8bb-956420e42699
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '484'
ht-degree: 100%

---

# 사용자 관리 {#user-management}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

사용자 관리를 통해 SAML(Security Assertion Markup Language)을 사용하여 AEM Forms 모듈과 Netegrity SiteMinder로 보호되는 애플리케이션 간에 SSO(Single Sign-On)를 활성화할 수 있습니다. SSO를 구현하면 사용자가 이미 회사 포털을 통해 인증된 경우 AEM Forms 사용자 로그인 페이지가 필요하지 않으며 표시되지 않습니다.

DB2의 데이터베이스 및 디렉터리 동기화 성능을 향상하는 방법에 대한 자세한 내용은 [IBM DB2 데이터베이스: 정기적 유지 관리를 위한 명령 실행](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance)을 참조하십시오.

## SSL이 활성화된 LDAP 서버에 대한 사용자 관리 구성 {#configuring-user-management-for-an-ssl-enabled-ldap-server}

SSL이 활성화된 LDAP 서버가 있는 경우 사용자 관리를 구성하여 해당 서버를 사용하십시오. ([SSL이 활성화된 LDAP 서버에 대한 사용자 관리 구성](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)을 참조하십시오.)

## 문서 보안에 사용할 사용자 권한 설정 {#setting-user-privileges-for-use-with-document-security}

사용자 및 그룹을 만드는 데 적합한 권한이 있는 관리자 사용자를 만듭니다. AEM Forms 환경에 문서 보안이 포함되어 있는 경우 초대된 사용자와 로컬 사용자를 관리하는 권한을 해당 사용자의 관리자가 될 사용자에게 부여합니다. 또한 사용자에게 관리 콘솔에 대한 액세스 권한을 제공하려면 관리 콘솔 사용자 역할을 할당합니다. ([역할 만들기 및 구성](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)을 참조하십시오.)

정책 사용자 검색 중에 선택한 도메인에 속한 사용자 및 그룹을 보려면 슈퍼 관리자 또는 정책 세트 관리자가 도메인(사용자 관리에서 생성됨)을 선택하여 생성된 각 정책 세트에 대해 표시되는 사용자 및 그룹 목록에 추가해야 합니다.

표시되는 사용자 및 그룹 목록은 정책 세트 코디네이터에게 표시되며 최종 사용자가 정책에 추가할 사용자 또는 그룹을 선택할 때 찾아볼 수 있는 도메인을 제한하는 데 사용됩니다. 이 작업을 수행하지 않으면 정책 세트 코디네이터는 정책에 추가할 사용자 또는 그룹을 찾을 수 없습니다. 지정된 정책 세트에는 두 명 이상의 정책 세트 코디네이터가 있을 수 있습니다.

>[!NOTE]
>
>정책을 만들기 전에 도메인을 만들어야 합니다.

### 표시되는 사용자 및 그룹 설정 {#set-visible-users-and-groups}

문서 보안을 사용하여 AEM Forms 환경을 설치하고 구성한 후 사용자 관리에서 적절한 도메인을 모두 설정합니다.

1. 관리 콘솔에서 서비스 > 문서 보안 > 정책을 클릭한 후 정책 세트 탭을 클릭합니다.
1. 전역 정책 세트를 선택한 후 표시되는 사용자 및 그룹 탭을 클릭합니다.
1. 도메인 추가를 클릭하고 필요에 따라 기존 도메인을 추가합니다.
1. 서비스 > 문서 보안 > 구성 > 내 정책으로 이동하여 표시되는 사용자 및 그룹 탭을 클릭합니다.
1. 도메인 추가를 클릭하고 필요에 따라 기존 도메인을 추가합니다.

## 관리자 사용자 제한 사항 {#administrator-user-restrictions}

보안상의 이유로 특정 유형의 관리자 권한이 있는 사용자는 Workspace 최종 사용자 웹 페이지에 액세스할 수 없습니다. 해당 웹 페이지는 방화벽 외부에 존재할 수 있으므로 관리자 수준의 작업을 허용하면 보안 위험이 발생할 수 있습니다. Workspace 관리자 또는 Workspace 사용자 권한이 있는 사용자만 최종 사용자 웹 페이지에 액세스할 수 있습니다.

>[!NOTE]
>
>Flex Worksapce는 AEM Forms 릴리스에서 더 이상 사용되지 않습니다.
