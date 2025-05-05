---
title: ' [!DNL Adobe Stock] 자산 관리'
description: ' [!DNL Adobe Experience Manager] 내에서  [!DNL Adobe Stock] 자산을 검색, 가져오기, 라이선스 및 관리합니다. 라이센스가 부여된 자산을 다른 디지털 자산으로 사용합니다.'
contentOwner: Vishabh Gupta
feature: Search, Adobe Stock
role: User, Admin
exl-id: 8ec597df-bb64-4768-bf9c-e8cca4fea25b
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 18dd655887293188224f51fa713d0345991d20d7
workflow-type: tm+mt
source-wordcount: '2191'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager Assets]에서 [!DNL Adobe Stock]개 자산 사용 {#use-adobe-stock-assets-in-aem-assets}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/aem-assets-adobe-stock.html?lang=ko) |
| AEM 6.5 | 이 문서 |

<!-- old content

[!DNL Experience Manager Assets] provides users the ability to search, preview, save, and license [!DNL Adobe Stock] assets directly from [!DNL Experience Manager].. 

Organizations can integrate their [!DNL Adobe Stock] enterprise plan with [!DNL Experience Manager Assets] to ensure that licensed assets are broadly available for their creative and marketing projects, with the powerful asset management capabilities of [!DNL Experience Manager].

[!DNL Adobe Stock] service provides designers and businesses with access to millions of high-quality, curated, royalty-free photos, vectors, illustrations, videos, templates, and 3D assets for all their creative projects. [!DNL Experience Manager] users are able to quickly find, preview, and license [!DNL Adobe Stock] assets that are saved in [!DNL Experience Manager], without leaving the [!DNL Experience Manager] interface.
-->

<!-- New overview content
-->

[!DNL Adobe Stock] 서비스는 디자이너와 기업의 모든 광고 프로젝트를 위해 고품질로 큐레이팅된 로열티가 없는 수백만 장의 사진, 벡터, 일러스트레이션, 비디오, 템플릿 및 3D 자산에 대한 액세스를 제공합니다.

엔터프라이즈 오퍼링의 [!DNL Adobe Stock]은(는) 기본적으로 조직 전체에서 공유 권한을 포함합니다. 조직의 사용자가 에셋에 라이선스를 부여한 후에는 다시 라이선스를 부여하지 않고도 조직의 다른 사용자가 이 에셋을 식별하고, 다운로드하고, 사용할 수 있습니다. 조직에서 에셋에 라이선스를 부여한 후에는 에셋을 사용할 수 있는 권한이 영구적으로 유지됩니다.

조직은 기업 [!DNL Adobe Stock] 계획을 [!DNL Experience Manager Assets]과(와) 통합하여 라이선스가 있는 자산이 [!DNL Experience Manager]의 강력한 자산 관리 기능을 통해 광고 및 마케팅 프로젝트에 폭넓게 사용 가능한지 확인할 수 있습니다. [!DNL Experience Manager] 사용자는 [!DNL Experience Manager] 인터페이스를 벗어나지 않고도 [!DNL Experience Manager]에 저장된 Adobe Stock 자산을 빠르게 찾고, 미리 보고, 라이선스를 제공할 수 있습니다.

<!-- Old content
## Prerequisites {#prerequisites}

The integration requires an [enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/).
-->

## [!DNL Experience Manager]과(와) [!DNL Adobe Stock]을(를) 통합하기 위한 필수 구성 요소 {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets]은(는) 사용자에게 [!DNL Experience Manager]에서 직접 [!DNL Adobe Stock] 자산을 검색, 미리 보기, 저장 및 라이선스를 제공할 수 있는 기능을 제공합니다.

이 통합을 활성화하려면 다음 요구 사항을 충족해야 합니다.

* 엔터프라이즈 [!DNL Adobe Stock] 계획입니다.
* 기본 Stock 제품 프로필에 대한 [!DNL Admin Console]의 권한이 있는 사용자입니다.
* [!DNL Adobe Developer Console]에서 통합을 만들기 위해 [!DNL Developer Access profile]에 대한 권한이 있는 사용자입니다.

엔터프라이즈 [!DNL Adobe Stock] 계획,

* [!DNL Adobe Stock]에 대한 제품 권한을 제공합니다(Experience Manager에 연결된 재고).
* 주식 특권을 위해 [!DNL Adobe Admin Console]에 구입한 크레딧입니다.
* [!DNL Adobe Admin Console] 내에서 크레딧과 라이선스를 전체적으로 관리할 수 있습니다.

권한 내에서 [!DNL Adobe Stock]에 대한 기본 제품 프로필이 [!DNL Admin Console]에 있습니다. 여러 프로필을 만들 수 있으며 이러한 프로필에 따라 Stock 자산에 라이센스를 부여할 수 있는 사람이 결정됩니다. 제품 프로필에 직접 액세스하는 사용자는 [https://stock.adobe.com/](https://stock.adobe.com/)에 액세스하여 Stock 자산에 라이선스를 부여할 수 있습니다. 반면 개발자 액세스를 사용하여 통합(API)을 만드는 다른 방법이 있습니다. 이 통합은 [!DNL Experience Manager Assets]과(와) [!DNL Adobe Stock] 간의 통신을 인증합니다.

<!-- old content
## Integrate [!DNL Experience Manager] and [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets] provides users the ability to search, preview, save, and license [!DNL Adobe Stock] assets directly from [!DNL Experience Manager].

**Prerequisites**

The integration requires: 

* An [enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/)
* A user with permissions in Admin Console to the default Stock product profile
* A user with permissions to the Developer Access profile for creating integration in Adobe Developer Console

An enterprise [!DNL Adobe Stock] plan,

* Provides product entitlement for [!DNL Adobe Stock] (Stocks connected to Experience Manager)
* Credits purchased into the [!DNL Adobe Admin Console] for your stock entitlement
* Enables Service Account (JWT) authentication within [!DNL Adobe Developer Console] for your stock entitlement
* Enables managing the credits and licensing globally from within [!DNL Adobe Admin Console]

Within the entitlement, a default product profile for [!DNL Adobe Stock] exists in [!DNL Admin Console]. Multiple profiles can be created, and these profiles determines who can license Stock assets. A user having access directly to the product profile can access [https://stock.adobe.com/](https://stock.adobe.com/) and license Stock assets. Whereas there is another method of using the Developer Access to create integration (API) to authenticate communication between [!DNL Experience Manager] and [!DNL Adobe Stock].

>[!NOTE]
>
>The Stock service account (JWT) authentication comes with the enterprise Stock entitlement.
>
>The integration does not support Oauth authentication for enterprise Stock entitlement.

<!-- old content
To allow communication between [!DNL Experience Manager] and [!DNL Adobe Stock], create an IMS configuration and an [!DNL Adobe Stock] configuration in [!DNL Experience Manager].

>[!NOTE]
>
>Only [!DNL Experience Manager] administrators and [!DNL Admin Console] administrators for an organization can perform the integration as it requires administrator privileges.
-->

## [!DNL Experience Manager]과(와) [!DNL Adobe Stock] 통합 {#integrate-adobe-stock-with-aem-assets}

개발자로서 다음 단계를 실행하여 [!DNL Adobe Experience Manager]과(와) [!DNL Adobe Stock]을(를) 통합하십시오.

1. [ [!DNL Developer Console]에서 프로그램 설정](#set-up-a-program-in-developer-console)
1. [ [!DNL AEM] 작성자 인스턴스에 구성 추가](#add-configuration-in-the-aem-author-instance)

### [!DNL Developer Console]에서 프로그램 설정 {#set-up-a-program-in-developer-console}

[!DNL Developer Console]에서 프로그램을 설정하려면 다음 단계를 수행하십시오.
1. [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/14431/user/servicesandapis)&#x200B;(으)로 이동하여 조직에 로그인합니다.
1. **[!UICONTROL 프로젝트]** 대시보드에서 사용할 수 있는 **[!UICONTROL 새 프로젝트 만들기]**&#x200B;를 선택하십시오.
   ![aem assets와 adobe stock 통합](/help/assets/assets/create-new-project-in-adobe-dev-console.png)
1. **[!UICONTROL 프로젝트에 추가]**&#x200B;를 클릭하고 **[!UICONTROL API]**&#x200B;을(를) 선택합니다.
1. **[!UICONTROL Adobe Stock]**&#x200B;을(를) 선택하고 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 자격 증명 이름]**&#x200B;을(를) 지정하고 **[!UICONTROL OAuth 서버 간]**&#x200B;이(가) 선택되었는지 확인하고 **[!UICONTROL 다음]**&#x200B;을(를) 클릭합니다.
1. **[!UICONTROL AEM Assets]** **[!UICONTROL 제품 프로필]**&#x200B;을 선택하고 **[!UICONTROL 구성된 API 저장]**&#x200B;을 클릭합니다. [!DNL Developer Console]에서 프로젝트를 만들었음을 확인하는 성공 메시지가 표시됩니다. 프로젝트 대시보드가 열리고 맨 위에 프로젝트 이름이 표시됩니다. **[!UICONTROL API]**&#x200B;에 **[!UICONTROL Adobe Stock]**, **[!UICONTROL 제품 프로필]**&#x200B;에 **[!UICONTROL AEM Assets]**, **[!UICONTROL 연결된 자격 증명]**&#x200B;에 **[!UICONTROL OAuth 서버 간]** 자격 증명 카드입니다.
   ![aem assets와 adobe stock 통합](/help/assets/assets/adc-project-name.png)
1. **[!UICONTROL OAuth 서버 간]** 자격 증명 카드를 선택하면 **[!UICONTROL 자격 증명 세부 정보]**&#x200B;가 표시됩니다. **[!UICONTROL 클라이언트 ID]**, **[!UICONTROL 클라이언트 암호]**, **[!UICONTROL 범위]**, **[!UICONTROL 자격 증명 이름]**, **[!UICONTROL 기술 계정 ID]**, **[!UICONTROL 조직 ID]**&#x200B;부터 [AEM 작성자 인스턴스에 구성을 추가](#add-configuration-in-the-aem-author-instance)까지 프로젝트의 이러한 [!DNL OAuth Server-to-Server] 자격 증명 세부 정보를 사용하십시오.
   ![aem assets 및 adobe stock](/help/assets/assets/oauth-server-server-credentials-details-page.png)

### [!DNL AEM] 작성자 인스턴스에 구성 추가 {#add-configuration-in-the-aem-author-instance}

다음 단계를 실행하여 [!DNL AEM] 작성자 인스턴스에 구성을 추가합니다.

1. [ [!DNL AEM] 작성자 인스턴스에서 새  [!DNL Adobe Stock IMS configuration] 을(를) 설정합니다.](#set-up-adobe-stock-ims-configuration-in-aem-author-instance)
1. [ [!DNL Adobe Stock]에 연결할 클라우드 구성 추가](#add-cloud-configuration-to-connect-adobe-stock)

#### [!DNL AEM author] 인스턴스에서 새 [!DNL Adobe Stock IMS configuration] 설정 {#set-up-adobe-stock-ims-configuration-in-aem-author-instance}

다음 단계를 실행하여 [!DNL AEM] 작성자 인스턴스에서 새 [!DNL Adobe Stock IMS configuration]을(를) 설정합니다.
1. [!DNL AEM] 작성자 인스턴스로 이동합니다.
1. ![aem assets 및 adobe stock](/help/assets/assets/Hammer.svg)을 클릭하고 **[!UICONTROL 보안]**&#x200B;을 선택한 다음 **[!UICONTROL Adobe IMS 구성]**&#x200B;을 선택합니다.
1. 새 IMS 구성을 만들려면 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. **[!UICONTROL Adobe IMS 기술 계정 구성]** 페이지에는 **[!UICONTROL 클라우드 솔루션]**, **[!UICONTROL 제목]**, **[!UICONTROL 인증 서버]**, **[!UICONTROL 클라이언트 ID]**, **[!UICONTROL 클라이언트 암호]**, **[!UICONTROL 범위]** 및 **[!UICONTROL 조직 ID]**&#x200B;와 같은 여러 필드가 표시됩니다. 다음 지침에 따라 다음 필드에 세부 사항을 지정합니다.
   * **[!UICONTROL 클라우드 솔루션]**: **[!UICONTROL Adobe Stock]**&#x200B;을(를) 선택합니다.
   * **[!UICONTROL 제목]**: 이 통합의 이름을 지정하십시오.
   * **[!UICONTROL 인증 서버]**: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)을(를) 인증 서버로 추가합니다.
   * **[!UICONTROL 클라이언트 ID]**: 프로젝트 대시보드로 이동하여 왼쪽 창에서 사용할 수 있는 **[!UICONTROL OAuth 서버 간]** 옵션을 클릭하고 **[!UICONTROL 자격 증명 세부 정보]**&#x200B;를 선택한 다음 **[!UICONTROL 클라이언트 ID]**&#x200B;을(를) 복사하여 여기에 붙여넣으십시오([7](#set-up-a-program-in-developer-console)단계 참조).

   * **[!UICONTROL 클라이언트 암호]**: 프로젝트 대시보드로 이동하여 왼쪽 창에서 사용할 수 있는 **[!UICONTROL OAuth 서버 간]** 옵션을 클릭하고 **[!UICONTROL 자격 증명 세부 정보]**&#x200B;를 선택하고 **[!UICONTROL 클라이언트 암호 검색]**&#x200B;을 클릭하고 **[!UICONTROL 클라이언트 암호 검색]**&#x200B;을 복사하여 여기에 붙여 넣으십시오([7단계](#set-up-a-program-in-developer-console) 참조).

   * **[!UICONTROL 범위]**: 프로젝트 대시보드로 이동하여 왼쪽 창에서 사용할 수 있는 **[!UICONTROL OAuth 서버 간]** 옵션을 클릭하고 **[!UICONTROL 자격 증명 세부 정보]**&#x200B;를 선택한 다음 **[!UICONTROL 범위]**&#x200B;를 복사하여 여기에 붙여넣으십시오([7](#set-up-a-program-in-developer-console)단계 참조).

   * **[!UICONTROL 조직 ID]**: 프로젝트 대시보드로 이동하여 왼쪽 창에서 사용할 수 있는 **[!UICONTROL OAuth 서버 간]** 옵션을 클릭하고 **[!UICONTROL 자격 증명 세부 정보]**&#x200B;를 선택한 다음 **[!UICONTROL 조직 ID]**&#x200B;을(를) 복사하여 여기에 붙여넣으십시오([7](#set-up-a-program-in-developer-console)단계 참조).

     ![aem assets 및 adobe stock](/help/assets/assets/adobe-ims-technical-account-configuration.png)
1. **[!UICONTROL 만들기]**&#x200B;를 클릭하면 **[!UICONTROL Adobe IMS 구성]** 페이지가 열리고 사용자가 만든 [!DNL Adobe Stock] 통합이 표시됩니다.

#### [!DNL Adobe Stock]에 연결할 클라우드 구성 추가 {#add-cloud-configuration-to-connect-adobe-stock}

다음 단계를 실행하여 [!DNL Adobe Stock]에 연결할 클라우드 구성을 추가하십시오.

1. [!DNL AEM author] 인스턴스로 이동합니다.
1. ![aem assets 및 adobe stock](/help/assets/assets/Hammer.svg)을(를) 클릭하고 **[!UICONTROL 클라우드 서비스]**&#x200B;를 선택한 다음 **[!UICONTROL Adobe Stock]**&#x200B;을(를) 찾아 선택합니다.
   ![aem과 adobe stock 사용](/help/assets/assets/adding-cloud-config-to-adobe-stock.png)
1. **[!UICONTROL 만들기]**&#x200B;를 클릭하면 **[!UICONTROL Adobe Stock 구성]** 페이지에 여러 필드가 표시됩니다. 다음 지침에 따라 다음 필드에 세부 사항을 지정합니다.
   * **[!UICONTROL 제목]**: **[!UICONTROL Adobe IMS 기술 계정 구성]** 페이지([단계 3](#set-up-adobe-stock-ims-configuration-in-aem-author-instance) 참조)로 이동하여 제목을 복사하고 여기에 붙여넣으십시오.
   * **[!UICONTROL 연결된 Adobe IMS 구성]**: 만든 [!DNL Adobe Stock] 통합을 선택하십시오.
   * **[!UICONTROL 로케일]**: **[!UICONTROL 영어(미국)]**&#x200B;를 선택합니다.
1. **[!UICONTROL 저장 및 닫기]**&#x200B;를 클릭합니다.
   ![aem과 adobe stock 사용](/help/assets/assets/adobe-stock-config-page.png)
<!-- old content
## Steps to integrate [!DNL Experience Manager] and [!DNL Adobe Stock] {#integration-steps}

To integrate [!DNL Experience Manager] and [!DNL Adobe Stock], perform the following steps in the listed sequence: 

1. [Obtain public certificate](#public-certificate)
   
   In [!DNL Experience Manager], create an IMS account and generate a public certificate (public key).

1. [Create service account (JWT) connection](#createnewintegration) 
   
   In [!DNL Adobe Developer Console], create a project for your [!DNL Adobe Stock] organization. Under the project, configure an API using the public key to create a service account (JWT) connection. Get the service account credentials and JWT payload information.

1. [Configure IMS account](#create-ims-account-configuration)

   In [!DNL Experience Manager], configure the IMS account using the service account credentials and JWT payload.

1. [Configure cloud service](#configure-the-cloud-service)

   In [!DNL Experience Manager], configure an [!DNL Adobe Stock] cloud service using the IMS account.


### Create an IMS configuration {#create-an-ims-configuration}

The IMS configuration authenticates your [!DNL Experience Manager Assets] author instance with the [!DNL Adobe Stock] entitlement. 

IMS configuration includes two steps:

* [Obtain public certificate](#public-certificate) 
* [Configure IMS account](#create-ims-account-configuration)

### Obtain public certificate {#public-certificate}

The public key (certificate) authenticates your product profile in Adobe Developer Console.

1. Log in to your [!DNL Experience Manager Assets] author instance. The default URL is `http://localhost:4502/aem/start.html`.

1. From the **[!UICONTROL Tools]** panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

1. In Adobe IMS Configurations page, click **[!UICONTROL Create]**. The **[!UICONTROL Adobe IMS Technical Account Configuration]** page opens. 

1. In the **[!UICONTROL Certificate]** tab, select **[!UICONTROL Adobe Stock]** from the **[!UICONTROL Cloud Solution]** dropdown list.  

1. You can create a certificate or reuse an existing certificate for the configuration. 

   To create a certificate, select the **[!UICONTROL Create new certificate]** check box and specify an **alias** for the public key. The alias serves as name of the public key. 

1. Click **[!UICONTROL Create certificate]**. Then, click **[!UICONTROL OK]** to generate the public key.

1. Click the **[!UICONTROL Download Public Key]** icon and save the public key (.crt) file on your machine. The public key is used later to configure API for your Brand Portal tenant and generate service account credentials in Adobe Developer Console.

   Click **[!UICONTROL Next]**.

   ![generate-certificate](assets/stock-integration-ims-account.png)

1. In the **Account** tab, Adobe IMS account is created which requires the service account credentials.

   Open a new tab and [create a service account (JWT) connection in Adobe Developer Console](#createnewintegration). 

### Create service account (JWT) connection {#createnewintegration}

In Adobe Developer Console, projects and APIs are configured at organization level. Configuring an API creates a service account (JWT) connection. There are two methods to configure API, by generating a key pair (private and public keys) or by uploading a public key. In this example, the service account credentials are generated by uploading the public key.

To generate the service account credentials and JWT payload:

1. Log in to Adobe Developer Console with system administrator privileges. The default URL is [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   Ensure that you have selected the correct IMS organization (Stock entitlement) from the dropdown (organization) list.

1. Click **[!UICONTROL Create new project]**. A blank project with a system-generated name is created for your organization. 

   Click **[!UICONTROL Edit project]**. Update the **[!UICONTROL Project Title]** and **[!UICONTROL Description]**, and then click **[!UICONTROL Save]**.
   
1. In the **[!UICONTROL Project overview]** tab, click **[!UICONTROL Add API]**.

1. In the **[!UICONTROL Add an API window]**, select **[!UICONTROL Adobe Stock]**. Click **[!UICONTROL Next]**. 

1. In the **[!UICONTROL Configure API]** window, select **[!UICONTROL Service Account (JWT)]** authentication. Click **[!UICONTROL Next]**.

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. Click **[!UICONTROL Upload your public key]**. Click **[!UICONTROL Select a File]** and upload the public key (.crt file) that you have downloaded in the [obtain public certificate](#public-certificate) section. Click **[!UICONTROL Next]**.

1. Verify the public key and click **[!UICONTROL Next]**.

1. Select the default **[!UICONTROL Adobe Stock]** product profile and click **[!UICONTROL Save configured API]**. 

1. Once the API is configured, you are redirected to the API overview page. From the left navigation under **[!UICONTROL Credentials]**, click the **[!UICONTROL Service Account (JWT)]** option. Here, you can view the credentials and perform actions such as generate JWT tokens, copy credential details, and retrieve client secret.

1. From the **[!UICONTROL Client Credentials]** tab, copy the **[!UICONTROL client ID]**. 

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]** information. 

You can now use the client ID (API key), client secret, and JWT payload to [configure the IMS account](#create-ims-account-configuration) in [!DNL Experience Manager Assets].

### Configure IMS account {#create-ims-account-configuration}

You must have the [certificate](#public-certificate) and [service account (JWT) credentials](#createnewintegration) to configure the IMS account.

To configure the IMS account: 

1. Open the IMS Configuration and navigate to the **[!UICONTROL Account]** tab. You kept the page open while [obtaining the public certificate](#public-certificate).

1. Specify a **[!UICONTROL Title]** for the IMS account.

   In the **[!UICONTROL Authorization Server]** field, enter the URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).  

   Enter the client ID in the **[!UICONTROL API key]** field, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]** (JWT payload) that you have copied while [creating the service account (JWT) connection](#createnewintegration).

1. Click **[!UICONTROL Create]**. An IMS account configuration is created. 

   ![configure-ims-acount](assets/aem-stock-ims-config.png)
   
1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   Click **[!UICONTROL Check]** in the dialog box. On successful configuration, a message appears that the *Token is retrieved successfully*.

   ![health-check](assets/aem-stock-healthcheck.png)


### Configure cloud service {#configure-the-cloud-service}

To configure the [!DNL Adobe Stock] cloud service:

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.

1. In the [!DNL Adobe Stock Configurations] page, click **[!UICONTROL Create]**.

1. Specify a **[!UICONTROL Title]** for the cloud configuration. 

   Select the IMS configuration that you have created while [configuring the IMS account](#create-ims-account-configuration).

   Select your locale from the dropdown list.

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. Click **[!UICONTROL Save & Close]**. 
 -->
[!DNL Experience Manager Assets] 작성자 인스턴스가 이제 [!DNL Adobe Stock]과(와) 통합되었습니다. 여러 [!DNL Adobe Stock] 구성(예: 로케일 기반 구성)을 만들 수 있습니다. 이제 [!DNL Experience Manager] 사용자 인터페이스 내에서 [!DNL Adobe Stock] 자산에 액세스하고, 검색하고, 라이선스를 부여할 수 있습니다.

![search-stock-assets](assets/aem-stock-searchstocks.png)

>[!NOTE]
>
>이 통합 단계에서는 관리자만 [!DNL Adobe Stock] 자산에 액세스하고, omnisearch를 사용하여 Stock 자산을 검색하고, [!DNL Adobe Stock] 자산에 라이선스를 부여할 수 있습니다.
>
>관리자는 [!DNL Adobe Stock] 클라우드 서비스에 사용자 또는 그룹을 추가하고 [!DNL Experience Manager]에서 관리자가 아닌 사용자에게 Stock 구성에 액세스할 수 있는 권한을 부여할 수 있습니다.

1. 사용자 또는 그룹을 추가하려면 [!DNL Adobe Stock] 클라우드 구성을 선택하고 **[!UICONTROL 속성]**&#x200B;을 클릭합니다.

1. 검색하여 Adobe Stock 구성에 액세스할 수 있는 권한을 할당한 사용자 또는 그룹을 추가합니다. [사용자 그룹에 권한 할당](#assign-permissions-to-group)을 참조하세요.


## 사용자 그룹에 권한 할당 {#assign-permissions-to-group}

관리자는 사용자 그룹을 만들고 특정 사용자 또는 그룹에 [!DNL Adobe Stock] 클라우드 서비스에 액세스할 수 있는 권한을 부여할 수 있습니다.

사용자가 Adobe Stock 에셋을 검색하고 라이선스하는 데 필요한 권한은 다음과 같습니다.

* 경로 구성: `/conf/global/settings/stock`
* 권한: `jcr:read`
* 권한 유형: `Allow`

사용자 그룹을 만들거나 기존 사용자 그룹에 권한을 할당할 수 있습니다. [!DNL Experience Manager Assets] 인터페이스 또는 [!DNL User Admin] 콘솔에서 권한을 할당할 수 있습니다.

**[!DNL Experience Manager]에서 사용자 그룹에 대한 액세스 권한을 제공하려면:**

1. [!DNL Experience Manager] 사용자 인터페이스에서 **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 그룹]**(으)로 이동합니다. [!DNL Adobe Stock]에 대한 사용자 그룹을 만듭니다.

1. **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 권한]**(으)로 이동합니다.

1. 왼쪽 패널에서 사용자 그룹을 검색하고 Adobe Stock에 새 **[!UICONTROL ACE(액세스 제어 항목)]**&#x200B;을(를) 추가합니다.

   * 경로 구성: `/conf/global/settings/stock`
   * 권한: `jcr:read`
   * 권한 유형: `Allow`

   **[!UICONTROL 추가]**&#x200B;를 클릭합니다.

   ![사용자 권한](assets/aem-stock-user-permissions.png)

1. **[!UICONTROL 도구]** > **[!UICONTROL 클라우드 서비스]** > **[!UICONTROL Adobe Stock]**(으)로 이동합니다. [!DNL Adobe Stock] 클라우드 구성을 선택하고 **[!UICONTROL 속성]**&#x200B;을 클릭합니다.

1. 새로 만든 사용자 그룹을 [!DNL Adobe Stock] 구성에 추가합니다. **[!UICONTROL 저장 및 닫기]**&#x200B;를 클릭합니다.

   ![assign-user](assets/aem-stock-adduser.png)

**[!DNL User Admin Console]에서 사용자에게 액세스 권한을 제공하려면:**

1. [!DNL Experience Manager] 사용 Admin Console을 엽니다. 기본 URL은 `http://localhost:4502/userdamin`입니다.

1. 왼쪽 패널에서 `user_id` 또는 `name`을(를) 입력하여 사용자를 검색합니다. 두 번 클릭하여 사용자 속성을 엽니다.

1. **[!UICONTROL 권한]** 탭으로 이동하여 [!DNL Adobe Stock] 클라우드 구성에 `read` 권한을 허용합니다. `/conf/global/settings/stock`.

   >[!CAUTION]
   >
   >클라우드 구성이 허용되지 않으면 사용자는 [!DNL Experience Manager] 인터페이스에서 **[!UICONTROL Assets]**&#x200B;에만 액세스할 수 있습니다.
   >
   >[!UICONTROL Assets] 및 [!DNL Adobe Stock] 자산에 대한 액세스를 허용하려면 사용자에게 클라우드 구성이 허용되는지 확인하십시오.

1. 권한을 업데이트하려면 **[!UICONTROL 저장]**&#x200B;을 클릭하세요.

   ![assign-user-in-user-admin](assets/aem-stock-user-admin-console.png)

1. [!DNL Adobe Stock] 클라우드 구성에 사용자 또는 그룹을 추가합니다.

## Adobe Stock 에셋 액세스 {#access-stock-assets}

[!DNL Adobe Stock] 클라우드 구성에 대한 권한이 있는 관리자가 아닌 사용자는 [!DNL Experience Manager] 인터페이스에서 [!DNL Adobe Stock] 자산을 검색하고 라이선스를 부여할 수 있습니다.

[!DNL Adobe Stock]개의 자산에 액세스하기 전에 [!DNL Adobe Stock] 클라우드 구성을 활성화하는 추가 단계를 수행해야 합니다. 일회성 활동입니다. 사용자에게 여러 [!DNL Adobe Stock] 클라우드 구성에 대한 권한이 할당된 경우 사용자는 **[!UICONTROL 사용자 환경 설정]**&#x200B;에서 원하는 구성을 선택할 수 있습니다.

[!DNL Adobe Stock] 클라우드 구성을 활성화하려면 다음을 수행하십시오.

1. [!DNL Experience Manager]에 로그인합니다.

1. 오른쪽 상단에서 사용자 아이콘을 클릭한 다음 **[!UICONTROL 내 환경 설정]**&#x200B;을 클릭합니다. **[!UICONTROL 사용자 환경 설정]** 창이 열립니다.

1. 드롭다운 목록에서 원하는 **[!UICONTROL Stock 구성]**&#x200B;을(를) 선택하고 **[!UICONTROL 승인]**&#x200B;을(를) 클릭하여 구성을 활성화합니다.

   ![사용자 환경 설정](assets/aem-stock-preferences.png)

1. **[!UICONTROL Assets]** > **[!UICONTROL Adobe Stock]**(으)로 이동합니다. 이제 [!DNL Adobe Stock]개의 자산을 보고 검색하고 라이선스를 제공할 수 있습니다.

다음 표에서는 [!DNL Adobe Stock] 자산에 액세스하는 동안 사용자 권한이 작동하는 방식을 설명합니다.

| 사용자 | 그룹 | 권한 | 사용자 환경 설정에서 Stock 구성 수락 | Assets 액세스 | Adobe Stock 액세스 |
| --- | --- | --- | --- | --- | --- |
| admin | 해당 사항 없음 | 모두 | 해당 사항 없음 | 예 | 예 |
| test-doc1 | DAM 사용자 | /conf/global /settings/stock/cloud-config | 예 | 예 | 예 |
| test-doc1 | DAM 사용자 | /conf/global /settings/stock/cloud-config | 아니요 | 오류: 데이터를 로드하지 못했습니다. | 아니요 |
| test-doc1 | DAM 사용자 | **allow**: /conf/global /settings/stock     **거부**: /cloud-config | Stock 구성이 표시되지 않음 | 예 | 아니요 |


## [!DNL Experience Manager]에서 [!DNL Adobe Stock]개 자산 사용 및 관리 {#usemanage}

조직에서 이 기능을 사용하여 해당 사용자가 [!DNL Experience Manager Assets]에서 [!DNL Adobe Stock]개의 자산을 사용하여 작업하도록 허용할 수 있습니다. [!DNL Experience Manager] 사용자 인터페이스에서 [!DNL Adobe Stock]개의 자산을 검색하고 필요한 자산의 라이선스를 제공할 수 있습니다.

[!DNL Experience Manager]에서 [!DNL Adobe Stock] 자산에 라이센스가 부여되면 일반 자산처럼 사용하고 관리할 수 있습니다. [!DNL Experience Manager]에서 사용자는 자산을 검색 및 미리 보고, 자산을 복사 및 게시하고, [!DNL Brand Portal]에서 자산을 공유하고, [!DNL Experience Manager] 데스크톱 앱을 통해 자산에 액세스하고 사용할 수 있습니다.

![[!DNL Adobe Experience Manager] 작업 공간에서 [!DNL Adobe Stock]개 에셋 검색 및 결과 필터링](assets/adobe-stock-search-results-workspace.png)

**A.** 제공된 [!DNL Adobe Stock] ID의 자산과 유사한 자산을 검색합니다. **B.** Search assets that match your selection of shape or orientation. **C.** 지원되는 자산 유형 중 하나 검색 **D.** 필터 창 열기 또는 축소 **E.** 라이선스 및 [!DNL Experience Manager]에 선택한 자산 저장 **F.** 워터마크 [!DNL Experience Manager]에 자산 저장 **G.** 선택한 자산과 유사한 [!DNL Adobe Stock] 웹 사이트에서 자산 탐색 **H.** [!DNL Adobe Stock] 웹 사이트에서 선택한 자산 보기 **I.** 검색 결과에서 선택한 자산 수 **J.** 카드 보기와 목록 보기 간 전환

### 에셋 찾기 {#find-assets}

[!DNL Experience Manager] 사용자는 [!DNL Experience Manager] 및 [!DNL Adobe Stock] 모두에서 자산을 검색할 수 있습니다. 검색 위치가 [!DNL Adobe Stock]&#x200B;(으)로 제한되지 않으면 [!DNL Experience Manager] 및 [!DNL Adobe Stock]의 검색 결과가 표시됩니다.

* [!DNL Adobe Stock]개의 자산을 검색하려면 **[!UICONTROL 탐색]** > **[!UICONTROL Assets]** > **[!UICONTROL Adobe Stock 검색]**&#x200B;을 클릭합니다.

* [!DNL Adobe Stock] 및 [!DNL Experience Manager Assets]에서 자산을 검색하려면 ![검색](assets/do-not-localize/search_icon.png) 검색을 클릭하세요.

또는 검색 창에서 `Location: Adobe Stock`을(를) 입력하여 [!DNL Adobe Stock]개의 자산을 선택합니다. [!DNL Experience Manager]은(는) 검색된 에셋에 대한 고급 필터링 기능을 제공하므로 사용자는 지원되는 에셋 유형, 이미지 방향 및 라이선스 상태와 같은 필터를 사용하여 필요한 에셋을 빠르게 필터링할 수 있습니다.

>[!NOTE]
>
>[!DNL Adobe Stock]에서 검색한 Assets이 [!DNL Experience Manager]에 표시됩니다. 사용자가 [자산을 저장](/help/assets/aem-assets-adobe-stock.md#saveassets) 또는 [라이선스를 사용하고 자산을 저장](/help/assets/aem-assets-adobe-stock.md#licenseassets)한 후에만 [!DNL Adobe Stock]자산을 가져와서 [!DNL Experience Manager] 저장소에 저장합니다. [!DNL Experience Manager]에 이미 저장된 Assets은 쉽게 참조하고 액세스할 수 있도록 표시되고 강조 표시됩니다. 또한 [!DNL Stock] 자산은 소스를 [!DNL Stock]&#x200B;(으)로 표시하기 위해 일부 추가 메타데이터와 함께 저장됩니다.

![검색 필터 [!DNL Experience Manager] 및 강조 표시된 [!DNL Adobe Stock]개 자산을 검색 결과에서](assets/aem-search-filters2.jpg)

### 필요한 에셋 저장 및 보기 {#saveassets}

[!DNL Experience Manager]에 저장할 자산을 선택하십시오. 상단의 도구 모음에서 [!UICONTROL 저장]을 클릭하고 자산의 이름과 위치를 지정하십시오. 라이센스가 없는 자산은 워터마크로 로컬에 저장됩니다.

다음에 자산을 검색할 때 저장된 자산은 배지로 강조 표시되어 해당 자산을 [!DNL Experience Manager Assets]에서 사용할 수 있음을 나타냅니다.

>[!NOTE]
>
>최근에 추가된 에셋에는 라이센스가 부여된 배지 대신 새 배지가 표시됩니다.

### 에셋 라이센스 부여 {#licenseassets}

사용자는 [!DNL Adobe Stock] 엔터프라이즈 플랜의 할당량을 사용하여 [!DNL Adobe Stock] 자산의 라이선스를 부여할 수 있습니다. 에셋에 라이선스를 부여하면 에셋은 워터마크 없이 저장되고 [!DNL Experience Manager Assets]에서 검색 및 사용에 사용할 수 있습니다.

[!DNL Experience Manager Assets]![&#128279;](assets/aem-stock_licenseandsave.jpg)에서 [!DNL Adobe Stock]개 자산을 라이선스하고 저장하는 대화 상자


### 메타데이터 및 자산 속성 액세스 {#access-metadata-and-asset-properties}

사용자는 [!DNL Experience Manager]에 저장된 에셋에 대한 [!DNL Adobe Stock] 메타데이터 속성을 포함하여 메타데이터에 액세스하고 미리 볼 수 있으며 에셋에 대해 **[!UICONTROL 라이선스 참조]**&#x200B;를 추가할 수 있습니다. 그러나 라이선스 참조에 대한 업데이트는 [!DNL Experience Manager]과(와) [!DNL Adobe Stock] 웹 사이트 간에 동기화되지 않습니다.

사용자는 라이선스가 부여된 에셋과 라이선스가 없는 에셋 모두에 대한 속성을 볼 수 있습니다.

![저장된 자산의 메타데이터 및 라이선스 참조 보기 및 액세스](assets/metadata_properties.jpg)


## 알려진 제한 사항 {#known-limitations}

* **[!DNL Experience Manager] 서비스 팩 6.5.7.0 이상**&#x200B;과(와) 통합되는 동안 문제 발생: [!DNL Experience Manager] 6.5.7.0 이상과 통합하는 동안 예기치 않은 문제가 확인되었습니다. 이 문제는 테스트 중이며 [!DNL Experience Manager] 6.5.11.0에서 사용할 수 있습니다. [!DNL Customer Support]에게 연락하여 즉시 핫픽스를 받으십시오.

* **사용자 라이선스를 제한하는 기능이 제대로 작동하지 않습니다**: 스톡 구성에 대한 `read` 권한이 있는 모든 사용자는 [!DNL Adobe Stock] 자산을 검색하고 라이선스를 부여할 수 있습니다.

* **관리자가 아닌 사용자는 [!DNL Adobe Stock] 클라우드 구성을 수동으로 활성화해야 합니다**: **[!UICONTROL 사용자 환경 설정]** 창에서 **[!UICONTROL Stock 구성]**&#x200B;이(가) [!DNL Adobe Stock] 클라우드 구성을 활성화됨으로 표시하지만 관리자가 아닌 사용자에게는 작동하지 않습니다. Stock 구성을 활성화하려면 **[!UICONTROL 승인]** 단추를 클릭해야 합니다. 이 단계가 없으면 **[!UICONTROL Assets]**&#x200B;에 액세스할 때 오류 메시지가 반영됩니다.

* **편집 이미지 경고가 표시되지 않습니다**: 이미지에 라이선스를 부여할 때 사용자가 이미지가 편집 사용 전용인지 확인할 수 없습니다. 오용을 방지하기 위해 관리자는 Admin Console에서 편집 에셋에 대한 액세스를 중단할 수 있습니다.

* **잘못된 라이선스 유형이 표시됨**: 자산의 [!DNL Experience Manager]에 잘못된 라이선스 유형이 표시되었을 수 있습니다. 사용자는 [!DNL Adobe Stock] 웹 사이트에 로그인하여 라이선스 유형을 볼 수 있습니다.

* **참조 필드 및 메타데이터가 동기화되지 않음**: 사용자가 라이선스 참조 필드를 업데이트할 때 라이선스 참조 정보가 [!DNL Experience Manager]에서 업데이트되지만 [!DNL Adobe Stock] 웹 사이트에서는 업데이트되지 않습니다. 마찬가지로 사용자가 [!DNL Adobe Stock] 웹 사이트의 참조 필드를 업데이트하는 경우 [!DNL Experience Manager]에서 업데이트가 동기화되지 않습니다.

>[!MORELIKETHIS]
>
>* [자산 사용  [!DNL Adobe Stock] 에 대한 비디오 튜토리얼 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html?lang=ko)
>* [[!DNL Adobe Stock] 엔터프라이즈 플랜 도움말](https://helpx.adobe.com/kr/enterprise/using/adobe-stock-enterprise.html)
>* [[!DNL Adobe Stock] FAQ](https://helpx.adobe.com/kr/stock/faq.html)


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

