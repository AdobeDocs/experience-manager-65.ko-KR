---
title: AEM Managed Services에 대한 Adobe IMS 인증 및 [!DNL Admin Console] 지원
seo-title: AEM Managed Services에 대한 Adobe IMS 인증 및 [!DNL Admin Console] 지원
description: AEM에서 [!DNL 관리 콘솔]을(를) 사용하는 방법을 알아봅니다.
seo-description: AEM에서 [!DNL 관리 콘솔]을(를) 사용하는 방법을 알아봅니다.
uuid: 3f5b32c7-cf62-41a4-be34-3f71bbf224eb
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f6112dea-a1eb-4fd6-84fb-f098476deab7
translation-type: tm+mt
source-git-commit: a9931024f5cd79e2e363ed46edaef5e3e66c6e14

---


# AEM Managed [!DNL Admin Console] Services에 대한 Adobe IMS 인증 및 지원 {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>이 기능은 Adobe Managed Services 고객에게만 제공됩니다.

## 소개 {#introduction}

AEM 6.4.3.0에서는 AEM Managed Services 고객을 위한 AEM 인스턴스 및 Adobe IMS(Identity Management System) 기반 인증에 [!DNL Admin Console] 대한 지원을 **** 제공합니다.

AEM Managed Services 고객은 AEM Managed Services에 대한 AEM 온보딩을 [!DNL Admin Console] 통해 하나의 콘솔에서 모든 Experience Cloud 사용자를 관리할 수 있습니다. 사용자 및 그룹을 AEM 인스턴스와 연관된 제품 프로필에 할당하여 특정 인스턴스에 로그인할 수 있도록 할 수 있습니다.

## 주요 특징 {#key-highlights}

* AEM IMS 인증 지원은 AEM 작성자, 관리자 또는 개발자에만 해당되며 사이트 방문자와 같은 고객 사이트의 외부 최종 사용자에게는 해당되지 않습니다.
* 는 AEM Managed Services 고객을 IMS 조직 및 해당 인스턴스를 제품 컨텍스트로 [!DNL Admin Console] 나타냅니다. 고객 시스템 및 제품 관리자는 인스턴스에 대한 액세스를 관리할 수 있습니다.
* AEM Managed Services는 고객 토폴로지와 [!DNL Admin Console]동기화합니다. 인스턴스당 AEM Managed Services 제품 컨텍스트의 인스턴스가 하나 [!DNL Admin Console]있습니다.
* Product Profiles in [!DNL Admin Console] will determine which instances a user can access
* 고객의 SAML 2 호환 ID 공급자를 사용한 통합 인증이 지원됩니다.
* Enterprise ID 또는 Federated ID(고객 SSO(Single Sign-On)만 지원되며 개인 Adobe ID는 지원되지 않습니다.
* [!DNL User Management](Adobe [!DNL Admin Console]에서)는 고객 관리자가 계속 소유하게 됩니다.

## 아키텍처 {#architecture}

IMS 인증은 AEM과 Adobe IMS 끝점 간의 OAuth 프로토콜을 사용하여 작동합니다. 사용자가 IMS에 추가되고 Adobe ID가 있으면 IMS 자격 증명을 사용하여 AEM Managed Services 인스턴스에 로그인할 수 있습니다.

사용자 로그인 흐름이 아래에 표시되어 있고, 사용자는 IMS로 리디렉션되고, 선택적으로 SSO용 고객 IDP 유효성 검사로 리디렉션된 다음 다시 AEM으로 리디렉션됩니다.

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## How To Set Up {#how-to-set-up}

### 온보딩 조직에 [!DNL Admin Console] 문의 {#onboarding-organizations-to-admin-console}

The customer onboarding to [!DNL Admin Console] is a pre-requisite to using Adobe IMS for AEM authentication.

첫 번째 단계로, 고객은 Adobe IMS에서 프로비저닝된 조직을 가져야 합니다. Adobe Enterprise 고객은 Adobe [!DNL Admin [Console]에서 IMS 조직으로 표시됩니다](https://helpx.adobe.com/enterprise/using/admin-console.html).

AEM Managed Services customers should already have an organization provisioned, and as part of the IMS provisioning, the customer instances will be made available in the [!DNL Admin Console] for managing user entitlements and access.

사용자 인증을 위해 IMS로 전환하는 것은 AMS와 고객 간의 공동 노력이 될 것이며, 각 고객은 워크플로우를 완료해야 합니다.

고객이 IMS 조직 및 AMS로 존재하는 경우 IMS에 대한 고객 프로비저닝을 완료하면 필요한 구성 워크플로우의 요약이 됩니다.

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. The designated System Admin receives an invite to log in to the [!DNL Admin Console]
1. 시스템 관리자는 도메인 소유권을 확인하기 위해 도메인 요청을 합니다(이 예에서는 acme.com).
1. 시스템 관리자가 사용자 디렉토리를 설정합니다.
1. 시스템 관리자는 SSO 설정에 IDP(ID Provider) [!DNL Admin Console] 를 구성합니다.
1. AEM 관리자는 평소대로 로컬 그룹, 권한 및 권한을 관리합니다. 사용자 및 그룹 동기화 참조

>[!NOTE]
>
>IDP 구성을 포함하여 Adobe Identity Management 기본 사항에 대한 자세한 내용은 [이 페이지를 참조하십시오.](https://helpx.adobe.com/enterprise/using/set-up-identity.html)
>
>Enterprise Administration에 대한 자세한 내용은 [!DNL Admin Console] 이 페이지를 [](https://helpx.adobe.com/enterprise/managing/user-guide.html)참조하십시오.

### 사용자를 [!DNL Admin Console]{#onboarding-users-to-the-admin-console}

고객의 규모와 선호도에 따라 사용자를 승선시키는 방법은 세 가지가 있습니다.

1. 사용자 및 그룹을 수동으로 [!DNL Admin Console]
1. 사용자와 함께 CSV 파일 업로드
1. 고객의 기업 Active Directory에서 사용자 및 그룹을 동기화합니다.

#### Manual Addition through [!DNL Admin Console] UI {#manual-addition-through-admin-console-ui}

Users and Groups can be manually created in the [!DNL Admin Console] UI. 이 메서드는 관리할 사용자 수가 많지 않은 경우에 사용할 수 있습니다. 예를 들어 AEM 사용자 수가 50명 미만입니다.

고객이 이미 Analytics, Target 또는 Creative Cloud 애플리케이션과 같은 다른 Adobe 제품을 관리하는 데 이 방법을 사용하고 있는 경우 사용자는 수동으로 만들 수도 있습니다.

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### UI에서 파일 [!DNL Admin Console] 업로드 {#file-upload-in-the-admin-console-ui}

사용자 작성을 쉽게 처리하기 위해 사용자를 일괄 추가하기 위해 CSV 파일을 업로드할 수 있습니다.

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### 사용자 동기화 도구 {#user-sync-tool}

UST(User Sync Tool)를 통해 기업 고객은 Active Directory 또는 기타 테스트된 OpenLDAP 디렉토리 서비스를 사용하여 Adobe 사용자를 만들거나 관리할 수 있습니다. 대상 사용자는 도구를 설치 및 구성할 수 있는 IT ID 관리자(Enterprise Directory 및 시스템 관리자)입니다. 오픈 소스 도구는 사용자 정의할 수 있으므로 고객은 개발자가 특정 요구 사항에 맞게 수정할 수 있습니다.

When User Sync runs, it fetches a list of users from the organization’s Active Directory (or any other compatible data source) and compares it with the list of users within the [!DNL Admin Console]. It then calls the Adobe [!DNL User Management] API so that the [!DNL Admin Console] is synchronized with the organization’s directory. 변경 흐름은 완전히 단방향입니다.에서 편집한 내용은 디렉토리로 푸시되지 [!DNL Admin Console] 않습니다.

시스템 관리자는 이 도구를 사용하여 고객 디렉토리의 사용자 그룹을 제품 구성 및 사용자 그룹과 매핑할 수 [!DNL Admin Console]있으며, 새 UST 버전을 사용하면 에서 사용자 그룹을 동적으로 만들 수 [!DNL Admin Console]있습니다.

To set up User Sync, the organization needs to create a set of credentials in the same way they would use the [[!DNL User Management] API](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html).

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

사용자 동기화는 다음 위치의 Adobe Github 저장소를 통해 배포됩니다.

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

시험판 버전 2.4RC1은 동적 그룹 생성 지원과 함께 사용할 수 있으며 다음 자료를 참조하십시오. [https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

The major features for this release are the ability to dynamically map new LDAP groups for user membership in the [!DNL Admin Console], as well as dynamic user group creation.

새 그룹 기능에 대한 자세한 내용은 다음 링크를 참조하십시오.

[https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options)

>[!NOTE]
>
>사용자 동기화 도구에 대한 자세한 내용은 [설명서 페이지를](https://adobe-apiplatform.github.io/user-sync.py/en/)참조하십시오.
>
>
>The User Sync Tool needs to register as an Adobe I/O client UMAPI using the procedure described [here](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).
>
>The Adobe I/O Console Documentation can be found [here](https://www.adobe.io/apis/cloudplatform/console.html).
>
>
>사용자 [!DNL User Management] 동기화 도구가 사용하는 API는 이 [위치에서](https://www.adobe.io/apis/cloudplatform/umapi-new.html)다룹니다.

>[!NOTE]
>
>AEM IMS 구성은 Adobe Managed Services 팀에서 처리합니다. 그러나 고객 관리자는 요구 사항에 따라 수정할 수 있습니다(예: 자동 그룹 구성원 자격 또는 그룹 매핑). IMS 클라이언트는 Managed Services 팀에서도 등록됩니다.

## 사용 방법 {#how-to-use}

### Managing Products and User Access in [!DNL Admin Console] {#managing-products-and-user-access-in-admin-console}

When the customer Product Administrator logs in to [!DNL Admin Console], they will see multiple instances of the AEM Managed Services Product Context as shown below:

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

In this example, the org *AEM-MS-Onboard* has 32 instances spanning different topologies and environments like Stage, Prod, etc.

![screen_shot_2018-09-17at105517pm](assets/screen_shot_2018-09-17at105517pm.png)

인스턴스 세부 사항을 확인하여 인스턴스를 식별할 수 있습니다.

![screen_shot_2018-09-17at105601pm](assets/screen_shot_2018-09-17at105601pm.png)

각 제품 컨텍스트 인스턴스에는 관련 제품 프로필이 있습니다. 이 제품 프로필은 사용자 및 그룹에 대한 액세스 권한을 할당하는 데 사용됩니다.

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

이 제품 프로필에 추가된 모든 사용자 및 그룹은 아래 예와 같이 해당 인스턴스에 로그인할 수 있습니다.

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### AEM에 로그인 {#logging-into-aem}

#### 로컬 관리자 로그인 {#local-admin-login}

로그인 화면에 로컬로 로그인하는 옵션이 있으므로 AEM은 관리 사용자에 대한 로컬 로그인을 계속 지원할 수 있습니다.

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### IMS 기반 로그인 {#ims-based-login}

다른 사용자의 경우 인스턴스에 IMS가 구성되어 있으면 IMS 기반 로그인을 사용할 수 있습니다. The user will first click on the **Sign in with Adobe** button as shown below:

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

그러면 IMS 로그인 화면으로 리디렉션되고 자격 증명을 입력합니다.

![screen_shot_2018-09-17at115629pm](assets/screen_shot_2018-09-17at115629pm.png)

If a federated IDP is configured during initial [!DNL Admin Console] setup, then the user will be redirected to the customer IDP for SSO.

아래 예에서는 IDP가 Okta입니다.

![screen_shot_2018-09-17at115734pm](assets/screen_shot_2018-09-17at115734pm.png)

인증이 완료되면 사용자는 다시 AEM으로 리디렉션되고 로그인됩니다.

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### 기존 사용자 마이그레이션 {#migrating-existing-users}

다른 인증 방법을 사용하고 현재 IMS로 마이그레이션되고 있는 기존 AEM 인스턴스의 경우 마이그레이션 단계가 있어야 합니다.

AEM 저장소의 기존 사용자(로컬에서 LDAP 또는 SAML을 통해 소스)는 사용자 마이그레이션 유틸리티를 사용하여 IMS를 가리키도록 마이그레이션될 수 있습니다.

AMS 팀에서 IMS 프로비저닝의 일부로 이 유틸리티를 실행합니다.

### AEM의 권한 및 ACL 관리 {#managing-permissions-and-acls-in-aem}

액세스 제어 및 권한은 AEM에서 계속 관리되며, 이는 권한 및 액세스 제어가 정의된 로컬 그룹과 같이 IMS에서 오는 사용자 그룹(예: 아래 예에서 AEM-GRP-008)의 분리를 사용하여 수행할 수 있습니다. IMS에서 동기화된 사용자 그룹을 로컬 그룹에 할당하고 권한을 상속할 수 있습니다.

아래 예에서는 동기화된 그룹을 로컬 *Dam_Users* 그룹에 추가하겠습니다.

여기에서 사용자는 의 일부 그룹에도 할당되었습니다 [!DNL Admin Console]. (사용자 및 그룹은 사용자 동기화 도구를 사용하여 LDAP에서 동기화되거나 로컬에서 만들 수 있습니다. 위의 [ **온보딩 사용자] 섹션을[!DNL Admin Console]**참조하십시오.)

&amp;ast;사용자 그룹은 사용자가 인스턴스에 로그인할 때에만 동기화됩니다. 사용자 및 그룹이 많은 고객의 경우 AMS에서 그룹 동기화 유틸리티를 실행하여 액세스 제어 및 권한 관리를 위해 그룹을 미리 가져올 수 있습니다.

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

사용자는 IMS에서 다음 그룹의 일부입니다.

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

사용자가 로그인하면 그룹 멤버십이 아래와 같이 동기화됩니다.

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

AEM에서 IMS에서 동기화된 사용자 그룹을 기존 로컬 그룹(예: DAM 사용자)에 멤버로 추가할 수 있습니다.

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

아래에 표시된 대로, 그룹 AEM- *GRP_008은* DAM 사용자의 권한 및 권한을 상속합니다. 이는 동기화된 그룹에 대한 권한을 효과적으로 관리하는 방법이며 LDAP 기반 인증 방법에서도 일반적으로 사용됩니다.

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)