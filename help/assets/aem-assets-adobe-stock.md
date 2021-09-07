---
title: 자산 관리 [!DNL Adobe Stock] 자산
description: ' [!DNL Adobe Experience Manager] 내에서 자산을 검색, 가져오기, 라이선스 및 관리합니다.  [!DNL Adobe Stock]  라이선스가 있는 자산을 다른 디지털 자산으로 사용합니다.'
contentOwner: Vishabh Gupta
feature: Search, Adobe Stock
role: User, Admin
exl-id: 8ec597df-bb64-4768-bf9c-e8cca4fea25b
source-git-commit: 6d1073003c1b78be848652be0b387889eedbc193
workflow-type: tm+mt
source-wordcount: '2443'
ht-degree: 10%

---

# [!DNL Adobe Experience Manager Assets]에서 [!DNL Adobe Stock] 자산 사용 {#use-adobe-stock-assets-in-aem-assets}

<!-- old content

[!DNL Experience Manager Assets] provides users the ability to search, preview, save, and license [!DNL Adobe Stock] assets directly from [!DNL Experience Manager]. 

Organizations can integrate their [!DNL Adobe Stock] enterprise plan with [!DNL Experience Manager Assets] to ensure that licensed assets are broadly available for their creative and marketing projects, with the powerful asset management capabilities of [!DNL Experience Manager].

[!DNL Adobe Stock] service provides designers and businesses with access to millions of high-quality, curated, royalty-free photos, vectors, illustrations, videos, templates, and 3D assets for all their creative projects. [!DNL Experience Manager] users are able to quickly find, preview, and license [!DNL Adobe Stock] assets that are saved in [!DNL Experience Manager], without leaving the [!DNL Experience Manager] interface.
-->

<!-- New overview content
-->

[!DNL Adobe Stock] 서비스는 디자이너와 기업의 모든 광고 프로젝트를 위해 고품질로 큐레이팅된 로열티가 없는 수백만 장의 사진, 벡터, 일러스트레이션, 비디오, 템플릿 및 3D 자산에 대한 액세스를 제공합니다.

[!DNL Adobe Stock] 엔터프라이즈 오퍼링의 경우 기본적으로 조직 간 공유 권한이 포함됩니다. 조직의 사용자가 자산에 라이선스를 부여하면 조직의 다른 사용자가 해당 자산에 대한 라이선스를 다시 부여하지 않고도 이 자산을 식별하고 다운로드하여 사용할 수 있습니다. 조직에서 자산을 라이선스로 부여하면 자산을 사용할 수 있는 권한이 영구적입니다.

조직은 엔터프라이즈 [!DNL Adobe Stock] 플랜을 [!DNL Experience Manager Assets]과 통합하여 라이선스가 있는 자산이 광고 및 마케팅 프로젝트에 폭넓게 사용 가능하고 [!DNL Experience Manager] 의 강력한 자산 관리 기능이 있는지 확인할 수 있습니다. [!DNL Experience Manager] 사용자는 인터페이스를 종료하지 않고도 에 저장된 Adobe Stock 자산을 빠르게 찾고, 미리  [!DNL Experience Manager]보고, 라이선스를 제공할 수  [!DNL Experience Manager] 있습니다.

<!-- Old content
## Prerequisites {#prerequisites}

The integration requires an [enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/).
-->

## [!DNL Experience Manager] 및 [!DNL Adobe Stock] 통합 {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets] 에서는 사용자가 자산을 직접 검색, 미리 보기, 저장 및 라이선스를 제공할  [!DNL Adobe Stock] 수  [!DNL Experience Manager]있습니다.

**전제 조건**

통합에는 다음이 필요합니다.
* [enterprise [!DNL Adobe Stock] 계획](https://stockenterprise.adobe.com/)
* 기본 Stock 제품 프로필에 대한 Admin Console 권한이 있는 사용자
* 개발자 콘솔에서 통합을 만들기 위해 개발자 액세스 프로필에 대한 권한이 있는 사용자

Enterprise [!DNL Adobe Stock] 계획,
* [!DNL Adobe Stock]에 대한 제품 자격 제공(Experience Manager에 연결된 주식)
* 재고 권한에 대해 [!DNL Adobe Admin Console]에 구매된 실적
* 재고 권한에 대해 [!DNL Adobe Developer Console] 내에서 JWT(서비스 계정) 인증을 활성화합니다
* [!DNL Adobe Admin Console] 내에서 전체적으로 크레딧과 라이센스를 관리할 수 있습니다.

권한 내에 [!DNL Adobe Stock]에 대한 기본 제품 프로필이 [!DNL Admin Console]에 있습니다. 여러 프로필을 만들 수 있으며, 이러한 프로필은 Stock 자산의 라이선스를 제공할 수 있는 사용자를 결정합니다. 제품 프로필에 직접 액세스할 수 있는 사용자는 [https://stock.adobe.com/](https://stock.adobe.com/)에 액세스하여 Stock 자산의 라이선스를 제공할 수 있습니다. 반면 개발자 액세스를 사용하여 통합(API)을 만들어 [!DNL Experience Manager] 과 [!DNL Adobe Stock] 간의 통신을 인증하는 다른 방법이 있습니다.

>[!NOTE]
>
>Stock 서비스 계정(JWT) 인증은 enterprise Stock 권한 과 함께 제공됩니다.
>
>통합이 enterprise Stock 권한에 대한 Oauth 인증을 지원하지 않습니다.

<!-- old content
To allow communication between [!DNL Experience Manager] and [!DNL Adobe Stock], create an IMS configuration and an [!DNL Adobe Stock] configuration in [!DNL Experience Manager].

>[!NOTE]
>
>Only [!DNL Experience Manager] administrators and [!DNL Admin Console] administrators for an organization can perform the integration as it requires administrator privileges.
-->

## [!DNL Experience Manager] 및 [!DNL Adobe Stock] 통합 절차 {#integration-steps}

[!DNL Experience Manager] 및 [!DNL Adobe Stock]을 통합하려면 나열된 순서로 다음 단계를 수행하십시오.

1. [공개 인증서 받기](#public-certificate)

   [!DNL Experience Manager]에서 IMS 계정을 만들고 공개 인증서(공개 키)를 생성합니다.

1. [서비스 계정(JWT) 연결 만들기](#createnewintegration)

   [!DNL Adobe Developer Console]에서 [!DNL Adobe Stock] 조직에 대한 프로젝트를 만듭니다. 프로젝트에서 공개 키로 API를 구성하여 서비스 계정(JWT) 연결을 만듭니다. 서비스 계정 자격 증명과 JWT 페이로드 정보를 가져옵니다.

1. [IMS 계정 구성](#create-ims-account-configuration)

   [!DNL Experience Manager]에서 서비스 계정 자격 증명과 JWT 페이로드를 사용하여 IMS 계정을 구성합니다.

1. [클라우드 서비스 구성](#configure-the-cloud-service)

   [!DNL Experience Manager]에서 IMS 계정을 사용하여 [!DNL Adobe Stock] 클라우드 서비스를 구성합니다.


### IMS 구성 만들기 {#create-an-ims-configuration}

IMS 구성은 [!DNL Adobe Stock] 권한 부여로 [!DNL Experience Manager Assets] 작성자 인스턴스를 인증합니다.

IMS 구성에는 두 단계가 포함됩니다.

* [공개 인증서 받기](#public-certificate)
* [IMS 계정 구성](#create-ims-account-configuration)

### 공개 인증서 받기 {#public-certificate}

공개 키(인증서)는 Adobe 개발자 콘솔에서 제품 프로필을 인증합니다.

1. [!DNL Experience Manager Assets] 작성자 인스턴스에 로그인합니다. 기본 URL은 `http://localhost:4502/aem/start.html`.

1. **[!UICONTROL 도구]** 패널에서 **[!UICONTROL 보안]** > **[!UICONTROL Adobe IMS 구성]**&#x200B;으로 이동합니다.

1. Adobe IMS 구성 페이지에서 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. **[!UICONTROL Adobe IMS 기술 계정 구성]** 페이지가 열립니다.

1. **[!UICONTROL 인증서]** 탭의 **[!UICONTROL 클라우드 솔루션]** 드롭다운 목록에서 **[!UICONTROL Adobe Stock]**&#x200B;을(를) 선택합니다.

1. 인증서를 만들거나 구성에 대한 기존 인증서를 다시 사용할 수 있습니다.

   인증서를 만들려면 **[!UICONTROL 새 인증서 만들기]** 확인란을 선택하고 공개 키에 대해 **별칭**&#x200B;을 지정합니다. 별칭은 공개 키의 이름으로 사용됩니다.

1. **[!UICONTROL 인증서 만들기]**&#x200B;를 클릭합니다. 그런 다음 **[!UICONTROL 확인]**&#x200B;을 클릭하여 공개 키를 생성합니다.

1. **[!UICONTROL 공개 키 다운로드]** 아이콘을 클릭하고 공개 키(.crt) 파일을 컴퓨터에 저장합니다. 공개 키는 나중에 Brand Portal 테넌트에 대한 API를 구성하고 Adobe 개발자 콘솔에서 서비스 계정 자격 증명을 생성하는 데 사용됩니다.

   **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   ![인증서 생성](assets/stock-integration-ims-account.png)

1. **계정** 탭에서 서비스 계정 자격 증명이 필요한 Adobe IMS 계정이 만들어집니다.

   새 탭을 열고 [Adobe 개발자 콘솔에 서비스 계정(JWT) 연결을 만듭니다](#createnewintegration).

### 서비스 계정(JWT) 연결 만들기 {#createnewintegration}

Adobe 개발자 콘솔에서 프로젝트 및 API는 조직 수준에서 구성됩니다. API를 구성하면 서비스 계정(JWT) 연결이 만들어집니다. 키 쌍(개인 및 공개 키)을 생성하거나 공개 키를 업로드하여 API를 구성하는 두 가지 방법이 있습니다. 이 예에서는 서비스 계정 자격 증명이 공개 키를 업로드하여 생성됩니다.

서비스 계정 자격 증명과 JWT 페이로드를 생성하려면 다음을 수행합니다.

1. 시스템 관리자 권한으로 Developer Console에 로그인합니다. 기본 URL은 [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui)입니다.


   드롭다운(조직) 목록에서 올바른 IMS 조직(Stock entitlement)을 선택했는지 확인합니다.

1. **[!UICONTROL 새 프로젝트 만들기]**&#x200B;를 클릭합니다. 조직에 대해 시스템 생성 이름이 있는 빈 프로젝트가 만들어집니다.

   **[!UICONTROL 프로젝트 편집]**&#x200B;을 클릭합니다. **[!UICONTROL 프로젝트 제목]** 및 **[!UICONTROL 설명]**&#x200B;을 업데이트한 다음 **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

1. **[!UICONTROL 프로젝트 개요]** 탭에서 **[!UICONTROL API 추가]**&#x200B;를 클릭합니다.

1. **[!UICONTROL API 추가 창]**&#x200B;에서 **[!UICONTROL Adobe Stock]**&#x200B;을 선택합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. **[!UICONTROL API 구성]** 창에서 **[!UICONTROL 서비스 계정(JWT)]** 인증을 선택합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. **[!UICONTROL 공개 키를 업로드합니다]**. **[!UICONTROL 파일]**&#x200B;을 선택하고 [공개 인증서 가져오기](#public-certificate) 섹션에서 다운로드한 공개 키(.crt 파일)를 업로드합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. 공개 키를 확인하고 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. 기본 **[!UICONTROL Adobe Stock]** 제품 프로필을 선택하고 **[!UICONTROL 구성된 API]**&#x200B;를 클릭합니다.

1. API가 구성되면 API 개요 페이지로 리디렉션됩니다. **[!UICONTROL 자격 증명]** 아래의 왼쪽 탐색에서 **[!UICONTROL 서비스 계정(JWT)]** 옵션을 클릭합니다. 여기에서 자격 증명을 보고 JWT 토큰 생성, 자격 증명 세부 사항 복사 및 클라이언트 암호 검색과 같은 작업을 수행할 수 있습니다.

1. **[!UICONTROL 클라이언트 자격 증명]** 탭에서 **[!UICONTROL 클라이언트 ID]**&#x200B;를 복사합니다.

   **[!UICONTROL 클라이언트 암호 검색]**&#x200B;을 클릭하고 **[!UICONTROL 클라이언트 암호 키]**&#x200B;를 복사합니다.

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. **[!UICONTROL JWT 생성]** 탭으로 이동하여 **[!UICONTROL JWT 페이로드]** 정보를 복사합니다.

이제 클라이언트 ID(API 키), 클라이언트 암호 및 JWT 페이로드를 [에 사용하여 [!DNL Experience Manager Assets]에서 IMS 계정](#create-ims-account-configuration)을 구성할 수 있습니다.

### IMS 계정 구성 {#create-ims-account-configuration}

IMS 계정을 구성하려면 [인증서](#public-certificate) 및 [서비스 계정(JWT) 자격 증명](#createnewintegration)이 있어야 합니다.

IMS 계정을 구성하려면 다음을 수행하십시오.

1. IMS 구성을 열고 **[!UICONTROL 계정]** 탭으로 이동합니다. 공개 인증서](#public-certificate)를 가져오는 동안 페이지를 열어 두었습니다.[

1. IMS 계정에 대한 **[!UICONTROL 제목]**&#x200B;을 지정합니다.

   **[!UICONTROL 인증 서버]** 필드에 URL을 입력합니다. [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   [서비스 계정(JWT) 연결](#createnewintegration)을 만드는 동안 복사한 **[!UICONTROL API 키]** 필드, **[!UICONTROL 클라이언트 암호]** 및 **[!UICONTROL 페이로드]**(JWT 페이로드)에 클라이언트 ID를 입력합니다.

1. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. IMS 계정 구성이 만들어집니다.

   ![configure-ims-account](assets/aem-stock-ims-config.png)

1. IMS 계정 구성을 선택하고 **[!UICONTROL 상태 확인]**&#x200B;을 클릭합니다.

   대화 상자에서 **[!UICONTROL 확인]**&#x200B;을 클릭합니다. 구성이 성공하면 *토큰이 성공적으로 검색되었습니다.*&#x200B;라는 메시지가 나타납니다.

   ![상태 점검](assets/aem-stock-healthcheck.png)


### 클라우드 서비스 구성 {#configure-the-cloud-service}

[!DNL Adobe Stock] 클라우드 서비스를 구성하려면:

1. [!DNL Experience Manager] 사용자 인터페이스에서 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**&#x200B;로 이동합니다.

1. [!DNL Adobe Stock Configurations] 페이지에서 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

1. 클라우드 구성에 대해 **[!UICONTROL 제목]**&#x200B;을 지정합니다.

   [IMS 계정을 구성](#create-ims-account-configuration)하는 동안 만든 IMS 구성을 선택합니다.

   드롭다운 목록에서 로케일을 선택합니다.

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. **[!UICONTROL 저장 후 닫기]**&#x200B;를 클릭합니다.

   이제 [!DNL Experience Manager Assets] 작성자 인스턴스가 [!DNL Adobe Stock]과 통합됩니다. 여러 [!DNL Adobe Stock] 구성(예: 로케일 기반 구성)을 만들 수 있습니다. 이제 [!DNL Experience Manager] 사용자 인터페이스 내에서 [!DNL Adobe Stock] 자산에 액세스하고, 검색하고, 라이선스를 제공할 수 있습니다.

   ![search-stock-assets](assets/aem-stock-searchstocks.png)

   >[!NOTE]
   >
   >이 통합 단계에서는 관리자만이 [!DNL Adobe Stock] 자산에 액세스하고, Stock 자산(omnisearch 사용)을 검색하고, [!DNL Adobe Stock] 자산에 대한 라이선스를 제공할 수 있습니다.
   >
   >관리자는 추가 [!DNL Adobe Stock] 클라우드 서비스에 사용자 또는 그룹을 추가하고 [!DNL Experience Manager]에서 이러한 관리자가 아닌 사용자에게 Stock 구성에 액세스할 수 있는 권한을 제공할 수 있습니다.

1. 사용자 또는 그룹을 추가하려면 [!DNL Adobe Stock] 클라우드 구성을 선택하고 **[!UICONTROL 속성]**&#x200B;을 클릭합니다.

1. Adobe Stock 구성에 액세스할 수 있는 권한을 할당한 사용자 또는 그룹을 추가하려면 검색합니다. [사용자 그룹에 권한 할당](#assign-permissions-to-group)을 참조하십시오.


## 사용자 그룹에 권한 할당 {#assign-permissions-to-group}

관리자는 사용자 그룹을 만들고 특정 사용자 또는 그룹에 권한을 지정하여 [!DNL Adobe Stock] 클라우드 서비스에 액세스할 수 있습니다.

다음은 사용자가 Adobe Stock 자산을 검색하고 라이선스를 부여하는 데 필요한 권한입니다.

* 경로를 구성합니다. `/conf/global/settings/stock`
* 권한: `jcr:read`
* 권한 유형: `Allow`

사용자 그룹을 만들거나 기존 사용자 그룹에 권한을 할당할 수 있습니다. [!DNL Experience Manager Assets] 인터페이스 또는 [!DNL User Admin] 콘솔에서 권한을 할당할 수 있습니다.

**사용자 그룹에 대한 액세스 권한을 제공하려면 다음을  [!DNL Experience Manager]수행하십시오.**

1. [!DNL Experience Manager] 사용자 인터페이스에서 **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 그룹]**&#x200B;으로 이동합니다. [!DNL Adobe Stock]에 대한 사용자 그룹을 만듭니다.

1. **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 권한]**&#x200B;으로 이동합니다.

1. 왼쪽 패널에서 사용자 그룹을 검색하고 Adobe Stock에 대해 새 **[!UICONTROL Access Control Entry(ACE)]**&#x200B;를 추가합니다.

   * 경로를 구성합니다. `/conf/global/settings/stock`
   * 권한: `jcr:read`
   * 권한 유형: `Allow`

   **[!UICONTROL 추가]**&#x200B;를 클릭합니다.

   ![user-permissions](assets/aem-stock-user-permissions.png)

1. **[!UICONTROL 도구]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**&#x200B;로 이동합니다. [!DNL Adobe Stock] 클라우드 구성을 선택하고 **[!UICONTROL 속성]**&#x200B;을 클릭합니다.

1. 새로 만든 사용자 그룹을 [!DNL Adobe Stock] 구성에 추가합니다. **[!UICONTROL 저장 후 닫기]**&#x200B;를 클릭합니다.

   ![사용자 지정](assets/aem-stock-adduser.png)

**사용자에게 액세스 권한을 제공하려면 다음을 수행하십시오.  [!DNL User Admin Console]**

1. [!DNL Experience Manager] 사용자 Admin Console을 엽니다. 기본 URL은 `http://localhost:4502/userdamin`.

1. 왼쪽 패널에서 `user_id` 또는 `name`을 입력하여 사용자를 검색합니다. 사용자 속성을 두 번 클릭하여 엽니다.

1. **[!UICONTROL 권한]** 탭으로 이동하여 [!DNL Adobe Stock] 클라우드 구성에 대해 `read` 권한을 허용합니다. `/conf/global/settings/stock`

   >[!CAUTION]
   >
   >클라우드 구성이 허용되지 않는 경우 사용자는 [!DNL Experience Manager] 인터페이스의 **[!UICONTROL Assets]**&#x200B;에만 액세스할 수 있습니다.
   >
   >[!UICONTROL Assets] 및 [!DNL Adobe Stock] 자산에 대한 액세스를 허용하려면 사용자에 대해 클라우드 구성이 허용되는지 확인하십시오.

1. **[!UICONTROL 저장]**&#x200B;을 클릭하여 권한을 업데이트합니다.

   ![assign-user-in-user-admin](assets/aem-stock-user-admin-console.png)

1. 사용자 또는 그룹을 [!DNL Adobe Stock] 클라우드 구성에 추가합니다.


## Adobe Stock 자산 액세스 {#access-stock-assets}

[!DNL Adobe Stock] 클라우드 구성에 대한 권한이 있는 관리자가 아닌 사용자는 [!DNL Experience Manager] 인터페이스에서 [!DNL Adobe Stock] 자산을 검색하고 라이선스를 제공할 수 있습니다.

[!DNL Adobe Stock] 자산에 액세스하기 전에 [!DNL Adobe Stock] 클라우드 구성을 활성화하는 추가 단계를 수행해야 합니다. 일회성 활동입니다. 사용자에게 여러 [!DNL Adobe Stock] 클라우드 구성에 대한 권한이 할당된 경우 사용자는 **[!UICONTROL 사용자 환경 설정]**&#x200B;에서 원하는 구성을 선택할 수 있습니다.

[!DNL Adobe Stock] 클라우드 구성을 활성화하려면

1. [!DNL Experience Manager]에 로그인합니다.

1. 오른쪽 상단 모서리에서 사용자 아이콘을 클릭한 다음 **[!UICONTROL 내 환경 설정]**&#x200B;을 클릭합니다. **[!UICONTROL 사용자 환경 설정]** 창이 열립니다.

1. 드롭다운 목록에서 원하는 **[!UICONTROL Stock 구성]**&#x200B;을 선택하고 **[!UICONTROL Accept]**&#x200B;를 클릭하여 구성을 활성화합니다.

   ![사용자 환경 설정](assets/aem-stock-preferences.png)

1. **[!UICONTROL 자산]** > **[!UICONTROL Adobe Stock]**&#x200B;로 이동합니다. 이제 [!DNL Adobe Stock] 자산을 보고 검색하고 라이선스를 제공할 수 있습니다.

다음 표에서는 [!DNL Adobe Stock] 자산에 액세스하는 동안 사용자 권한이 어떻게 작동하는지 설명합니다.

| 사용자 | 그룹 | 권한 | 사용자 기본 설정에서 Stock 구성 수락 | 자산 액세스 | Adobe Stock 액세스 |
| --- | --- | --- | --- | --- | --- |
| admin | N/A | 모든 | 해당 없음 | 예 | 예 |
| test-doc1 | DAM 사용자 | `/conf/global/settings/stock/cloud-config` | 예 | 예 | 예 |
| test-doc1 | DAM 사용자 | `/conf/global/settings/stock/cloud-config` | 아니오 | 오류: 데이터를 로드하지 못했습니다. | 아니오 |
| test-doc1 | DAM 사용자 | 허용: `/conf/global/settings/stock` 거부: `/cloud-config` | 스톡 구성이 표시되지 않음 | 예 | 아니오 |


## [!DNL Experience Manager]에서 [!DNL Adobe Stock] 자산 사용 및 관리 {#usemanage}

이 기능을 사용하면 조직에서 해당 사용자가 [!DNL Experience Manager Assets]에서 [!DNL Adobe Stock] 자산을 사용하여 작업할 수 있도록 허용할 수 있습니다. [!DNL Experience Manager] 사용자 인터페이스 내에서 사용자는 [!DNL Adobe Stock] 자산을 검색하고 필요한 자산에 대한 라이선스를 제공할 수 있습니다.

[!DNL Adobe Stock] 자산이 [!DNL Experience Manager]에서 라이선스가 부여되면 일반적인 자산처럼 사용하고 관리할 수 있습니다. [!DNL Experience Manager]에서 사용자는 자산을 검색하고 미리 볼 수 있습니다. 자산을 복사하여 게시합니다. [!DNL Brand Portal]에서 자산 공유 [!DNL Experience Manager] 데스크탑 앱을 통해 자산에 액세스하고 사용합니다. 기타.

![작업  [!DNL Adobe Stock] 공간에서 자산 검색 및 결과  [!DNL Adobe Experience Manager] 필터링](assets/adobe-stock-search-results-workspace.png)

**A.** ID가 제공된 자산과 유사한  [!DNL Adobe Stock] 자산을 검색합니다. **B.** 선택한 모양 또는 방향과 일치하는 자산을 검색합니다. **C.** 지원되는 자산 유형 중 하나 검색  **D.**  필터 창 열기 또는 축소  **예**  라이선스 및 선택한 자산을  [!DNL Experience Manager] **F에 저장** 워터마크  [!DNL Experience Manager] G. **선택한 자산과 유사한** 웹 사이트에서 자산 탐색 [!DNL Adobe Stock] H. **** 웹 사이트에서 선택한 자산 보기 [!DNL Adobe Stock] 웹 사이트 **I.** 검색 결과  **J.** 카드 보기와 목록 보기 간에 선택한 자산 수J.스위치

### 자산 찾기 {#find-assets}

[!DNL Experience Manager] 사용자는 [!DNL Experience Manager] 및 [!DNL Adobe Stock]에서 자산을 검색할 수 있습니다. 검색 위치가 [!DNL Adobe Stock]으로 제한되지 않으면 [!DNL Experience Manager] 및 [!DNL Adobe Stock]의 검색 결과가 표시됩니다.

* [!DNL Adobe Stock] 자산을 검색하려면 **[!UICONTROL 탐색]** > **[!UICONTROL 자산]** > **[!UICONTROL Adobe Stock]**&#x200B;을 클릭합니다.

* [!DNL Adobe Stock] 및 [!DNL Experience Manager Assets]에서 자산을 검색하려면 ![검색](assets/do-not-localize/search_icon.png)을 클릭합니다.

또는 검색 막대에 `Location: Adobe Stock` 을 입력하여 [!DNL Adobe Stock] 자산을 선택합니다. [!DNL Experience Manager] 에서는 검색된 자산에 고급 필터링 기능을 제공하여 사용자가 지원되는 자산 유형, 이미지 방향 및 라이선스가 있는 상태 등의 필터를 사용하여 필요한 자산을 빠르게 작성할 수 있도록 합니다.

>[!NOTE]
>
>[!DNL Adobe Stock]에서 검색된 자산은 [!DNL Experience Manager]에 표시됩니다. [!DNL Adobe Stock] 자산을 가져와서 사용자가 자산  [!DNL Experience Manager] 라이선스를  [저장하고 자산](/help/assets/aem-assets-adobe-stock.md#saveassets) 을  [저장한 후에만 저장소에 저장됩니다](/help/assets/aem-assets-adobe-stock.md#licenseassets). 쉽게 참조하고 액세스할 수 있도록 [!DNL Experience Manager]에 이미 저장된 자산이 표시되고 강조 표시됩니다. 또한 [!DNL Stock] 자산은 소스를 [!DNL Stock](으)로 나타내기 위해 일부 추가 메타데이터와 함께 저장됩니다.

![검색 결과에서  [!DNL Experience Manager] 및 강조 표시된  [!DNL Adobe Stock] 자산 검색 필터](assets/aem-search-filters2.jpg)

### 필요한 자산을 저장하고 봅니다 {#saveassets}

[!DNL Experience Manager]에 저장할 자산을 선택합니다. 맨 위의 도구 모음에서 [!UICONTROL 저장] 을 클릭하고 자산의 이름과 위치를 제공합니다. 라이센스가 없는 자산은 워터마크로 로컬에 저장됩니다.

다음번에 자산을 검색할 때 저장된 자산이 배지로 강조 표시되어 이러한 자산을 [!DNL Experience Manager Assets]에서 사용할 수 있음을 나타냅니다.

>[!NOTE]
>
>최근에 추가된 자산에 라이센스 배지 대신 새 배지가 표시됩니다.

### 자산 라이선스 {#licenseassets}

사용자는 [!DNL Adobe Stock] 엔터프라이즈 계획의 할당량을 사용하여 [!DNL Adobe Stock] 자산에 대한 라이선스를 제공할 수 있습니다. 자산에 대한 라이선스를 부여하면 워터마크 없이 저장되며 [!DNL Experience Manager Assets]에서 검색하고 사용할 수 있습니다.

![자산에 라이센스를 부여하고 저장하는 대화  [!DNL Adobe Stock] 상자  [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)


### 메타데이터 및 자산 속성에 액세스 {#access-metadata-and-asset-properties}

사용자는 [!DNL Experience Manager]에 저장된 자산에 대한 [!DNL Adobe Stock] 메타데이터 속성을 포함하여 메타데이터에 액세스하고 미리 볼 수 있으며, 자산에 대해 **[!UICONTROL 라이센스 참조]**&#x200B;를 추가할 수 있습니다. 그러나 라이센스 참조에 대한 업데이트는 [!DNL Experience Manager] 웹 사이트와 [!DNL Adobe Stock] 웹 사이트 간에 동기화되지 않습니다.

사용자는 라이선스가 있는 자산과 라이선스가 없는 자산 모두에 대한 속성을 볼 수 있습니다.

![저장된 자산의 메타데이터 및 라이선스 참조를 보고 액세스합니다](assets/metadata_properties.jpg)


## 알려진 제한 사항 {#known-limitations}

* **서비스  [!DNL Experience Manager] 팩 6.5.7.0 이상과의 통합 문제**: 6.5.7.0  [!DNL Experience Manager] 이상과의 통합 중에 예기치 않은 문제가 식별됩니다. 문제가 테스트 중이며 [!DNL Experience Manager] 6.5.11.0에서 사용할 수 있을 것으로 예상됩니다. 즉시 핫픽스를 확인하려면 [!DNL Customer Support]에 문의하십시오.

* **사용자의 라이선스 사용을 제한하는 기능이 제대로 작동하지 않습니다**. 재고 구성에  `read` 대한 권한이 있는 모든 사용자는 자산을 검색하고 라이선스를 제공할 수  [!DNL Adobe Stock] 있습니다.

* **관리자가 아닌 사용자는  [!DNL Adobe Stock] 클라우드 구성을 수동으로 활성화해야 합니다**. 사용자  **[!UICONTROL 환경]** 설정 창에서  **[!UICONTROL 스톡 구성]** 은  [!DNL Adobe Stock] 클라우드 구성을 활성화됨으로 표시하지만 관리자가 아닌 사용자에게는 작동하지 않습니다. Stock 구성을 활성화하려면 **[!UICONTROL Accept]** 단추를 클릭해야 합니다. 이 단계가 없는 경우, 시스템은 **[!UICONTROL Assets]**&#x200B;에 액세스할 때 오류 메시지를 반영합니다.

* **편집 이미지 경고가 표시되지 않습니다**. 이미지에 라이센스를 부여할 때 이미지가 편집 전용 인지 확인할 수 없습니다. 관리 관리자는 Admin Console에서 편집 자산에 대한 액세스를 중단할 수 있습니다.

* **잘못된 라이센스 유형이 표시됩니다**. 자산에 대해 잘못된 라이선스 유형이  [!DNL Experience Manager] 에 표시될 수 있습니다. 사용자는 [!DNL Adobe Stock] 웹 사이트에 로그인하여 라이센스 유형을 확인할 수 있습니다.

* **참조 필드 및 메타데이터가 동기화되지 않습니다**. 사용자가 라이센스 참조 필드를 업데이트하면 라이센스 참조 정보가 웹 사이트 [!DNL Experience Manager] 에서 업데이트되지만 웹 사이트에서는 업데이트되지  [!DNL Adobe Stock] 않습니다. 마찬가지로, 사용자가 [!DNL Adobe Stock] 웹 사이트의 참조 필드를 업데이트하면 업데이트가 [!DNL Experience Manager]에서 동기화되지 않습니다.

>[!MORELIKETHIS]
>
>* [와 함께 자산을  [!DNL Adobe Stock] 사용하는 방법에 대한 비디오 자습서 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [[!DNL Adobe Stock] 엔터프라이즈 플랜 도움말](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [[!DNL Adobe Stock] FAQ](https://helpx.adobe.com/stock/faq.html)



<!--old content

### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Click **[!UICONTROL Create]** and select **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Either reuse an existing certificate or select **[!UICONTROL Create new certificate]**.
1. Click **[!UICONTROL Create certificate]**. Once created, download the public key. Click **[!UICONTROL Next]**. Leave the [!UICONTROL Adobe IMS Technical Account Configuration] screen open to provide the required values shortly.
1. Access [Adobe Developer Console](https://console.adobe.io). Ensure that your account has administrator permissions for the organization for which the integration is required.
1. Click **[!UICONTROL Create new project]** and click **[!UICONTROL Add API]**. Select **[!UICONTROL Adobe Stock]** from the list of APIs that are available to you. Select [!UICONTROL OAUTH 2.0 Web].
1. Provide **[!UICONTROL Default redirect URI]** and **[!UICONTROL Redirect URI pattern]** values. Click **[!UICONTROL Save configured API]**. Copy the generated ID and secret.
1. In [!UICONTROL Adobe IMS Technical Account Configuration] screen, provide the values in the boxes titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. For detailed information about these values, see [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

-->

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

<!--
### Create [!DNL Adobe Stock] configuration in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Click **[!UICONTROL Create]** to create a configuration and associate it with your existing IMS Configuration. Select `PROD` as the environment parameter.
1. In **[!UICONTROL Licensed Assets Path]** field, leave a location as is. Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. Complete creation by adding all the required properties. Click **[!UICONTROL Save & Close]**.
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>If there are multiple [!DNL Adobe Stock] configurations, select the desired configuration in [!UICONTROL User Preferences] panel. To access the panel from [!DNL Experience Manager] home page, click the user icon and then click **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**.

-->