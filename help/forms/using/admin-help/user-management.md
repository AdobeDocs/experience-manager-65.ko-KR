---
title: 사용자 관리
seo-title: 사용자 관리
description: 사용자 관리를 사용하면 SAML을 사용하여 AEM 양식 모듈과 NetGrity SiteMinder로 보호된 애플리케이션 간에 SSO를 활성화할 수 있습니다. 이 문서에서는 사용자 관리에 대한 자세한 정보를 제공합니다.
seo-description: 사용자 관리를 사용하면 SAML을 사용하여 AEM 양식 모듈과 NetGrity SiteMinder로 보호된 애플리케이션 간에 SSO를 활성화할 수 있습니다. 이 문서에서는 사용자 관리에 대한 자세한 정보를 제공합니다.
uuid: f0c8331a-d995-483d-97b7-259df53b1a1a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 10e6177a-8228-4515-aba9-bbe59bede449
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 1%

---


# 사용자 관리 {#user-management}

사용자 관리를 사용하면 SAML(Security Assertion Markup Language)을 사용하여 AEM 양식 모듈과 Network SiteMinder로 보호된 애플리케이션 간에 SSO(Single Sign-On)를 활성화할 수 있습니다. SSO가 구현되면 AEM 양식 사용자 로그인 페이지가 필요하지 않으며 사용자가 이미 회사 포털을 통해 인증된 경우 표시되지 않습니다.

DB2의 데이터베이스 및 디렉토리 동기화 성능 개선에 대한 자세한 내용은 [IBM DB2 데이터베이스를 참조하십시오.일반 유지 관리](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance) 명령을 실행하는 중입니다.

## SSL 지원 LDAP 서버에 대한 사용자 관리 구성 {#configuring-user-management-for-an-ssl-enabled-ldap-server}

SSL을 사용하는 LDAP 서버가 있는 경우 사용자 관리를 구성하여 해당 서버에서 작업합니다. (SSL 지원 LDAP 서버에 대해 [사용자 관리 구성](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)을 참조하십시오.)

## Document Security {#setting-user-privileges-for-use-with-document-security}에 사용할 사용자 권한 설정

사용자 및 그룹을 만들 수 있는 적절한 권한이 있는 관리자 사용자를 만듭니다. AEM 양식 환경에 Document Security가 포함되어 있는 경우 이러한 사용자의 관리자가 될 사용자에게 초대된 사용자와 로컬 사용자를 관리할 권한을 부여합니다. 또한 사용자에게 관리 콘솔에 대한 액세스 권한을 제공하도록 관리 콘솔 사용자 역할을 할당합니다. ([역할 만들기 및 구성](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)을 참조하십시오.)

정책 사용자 검색 중에 선택한 도메인의 사용자 및 그룹을 보려면 수퍼 관리자 또는 정책 집합 관리자가 만든 각 정책 집합에 대해 표시되는 사용자 및 그룹 목록에 도메인(사용자 관리에서 생성)을 선택하고 추가해야 합니다.

표시되는 사용자 및 그룹 목록은 정책 집합 코디네이터에 표시되며 최종 사용자가 정책에 추가할 사용자 또는 그룹을 선택할 때 찾을 수 있는 도메인을 제한하는 데 사용됩니다. 이 작업을 수행하지 않으면 정책 집합 코디네이터는 정책에 추가할 사용자 또는 그룹을 찾을 수 없습니다. 지정된 정책 집합에 대해 둘 이상의 정책 집합 코디네이터가 있을 수 있습니다.

>[!NOTE]
>
>정책을 만들려면 먼저 도메인을 만들어야 합니다.

### 보이는 사용자 및 그룹 {#set-visible-users-and-groups} 설정

Document Security를 사용하여 AEM 양식 환경을 설치 및 구성한 후 사용자 관리에서 모든 적절한 도메인을 설정합니다.

1. 관리 콘솔에서 서비스 > Document Security > 정책을 클릭한 다음 정책 세트 탭을 클릭합니다.
1. 글로벌 정책 세트를 선택한 다음 [보이는 사용자 및 그룹] 탭을 클릭합니다.
1. 도메인 추가를 클릭하고 필요에 따라 기존 도메인을 추가합니다.
1. [서비스] > [문서 보안] > [구성] > [내 정책]으로 이동하고 [보이는 사용자 및 그룹] 탭을 클릭합니다.
1. 도메인 추가를 클릭하고 필요에 따라 기존 도메인을 추가합니다.

## 관리자 사용자 제한 사항 {#administrator-user-restrictions}

특정 유형의 관리자 권한을 가진 사용자는 보안상의 이유로 Workspace 최종 사용자 웹 페이지에 액세스할 수 없습니다. 이러한 웹 페이지는 방화벽 외부에 존재할 수 있으므로 관리 수준 작업을 허용하는 것은 보안 위험을 초래할 수 있습니다. 작업 공간 관리자 또는 작업 공간 사용자 권한이 있는 사용자만 최종 사용자 웹 페이지에 액세스할 수 있습니다.

>[!NOTE]
>
>Flex Workflow는 AEM Forms 릴리스에서 더 이상 사용되지 않습니다.

