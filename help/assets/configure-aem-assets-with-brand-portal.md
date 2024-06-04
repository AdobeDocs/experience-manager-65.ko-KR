---
title: Brand Portal에서 AEM Assets 구성
description: Brand Portal에 자산 및 컬렉션을 게시하기 위해 Brand Portal에서 AEM Assets을 구성하는 방법을 알아봅니다.
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
docset: aem65
feature: Brand Portal
role: Admin
exl-id: ae33181c-9eec-421c-be55-4bd019de40b8
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 2a6cf0e85aace1516818ce87bc35b1b35f3da6e8
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 24%

---


# Brand Portal에서 AEM Assets 구성 {#configure-integration-65}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=ko) |
| AEM 6.5 | 이 문서 |

Adobe Experience Manager Assets Brand Portal을 사용하면 승인된 브랜드 자산을 Adobe Experience Manager Assets에서 Brand Portal으로 게시하고 Brand Portal 사용자에게 배포할 수 있습니다.

AEM Assets은 Brand Portal 테넌트의 인증을 위해 Adobe Identity Management 서비스(IMS) 계정 토큰을 조달하는 Adobe Developer 콘솔을 통해 Brand Portal으로 구성됩니다.

>[!NOTE]
>
>AEM 6.5.4.0 이상에서 Adobe 개발자 콘솔을 통해 Brand Portal에 AEM Assets을 구성할 수 있습니다.
>
<!--
>Earlier, Brand Portal was configured via legacy OAuth Gateway, which uses the JSON Web Token (JWT) exchange to obtain an IMS Access token for authorization. 
>
>Configuration via legacy OAuth Gateway is no longer supported from April 6, 2020, and is changed to Adobe Developer Console.
-->

>[!TIP]
>
>***기존 고객 전용***
>
>Adobe은 기존 OAuth 게이트웨이 구성을 계속 사용할 것을 권장합니다. 기존 OAuth 게이트웨이 구성 문제가 발생하는 경우 기존 구성을 삭제하고 Adobe Developer 콘솔을 통해 구성을 만드십시오.

<!--
This help describes the following two use-cases:

* [New configuration](#configure-new-integration-65): If you are a new Brand Portal user and want to configure your AEM Assets Author instance with Brand Portal, you can create a configuration by way of the Adobe Developer Console. 
* [Upgrade configuration](#upgrade-integration-65): If you are an existing Brand Portal user having configuration on legacy OAuth Gateway, delete the existing configuration and create a configuration by way of Adobe Developer Console.
-->
제공된 정보는 이 도움말을 읽는 사람이 다음 기술을 잘 알고 있다는 가정을 기반으로 합니다.

* Adobe Experience Manager 및 AEM 패키지 설치, 구성 및 관리

* Linux® 및 Microsoft® Windows 운영 체제를 사용합니다.

## 사전 요구 사항 {#prerequisites}

Brand Portal을 사용하여 AEM Assets를 구성하려면 다음 항목이 필요합니다.

* 최신 서비스 팩으로 실행 중인 AEM Assets 작성자 인스턴스
* Brand Portal 테넌트 URL
* Brand Portal 테넌트의 IMS 조직에 대한 시스템 관리자 권한이 있는 사용자

[AEM 6.5 다운로드 및 설치](#aemquickstart)

[최신 AEM 서비스 팩 다운로드 및 설치](#servicepack)

### AEM 6.5 다운로드 및 설치 {#aemquickstart}

AEM 작성자 인스턴스를 설정하려면 AEM 6.5가 있어야 합니다. AEM을 실행하지 않은 경우 다음 위치에서 다운로드하십시오.

* 기존 AEM AEM 고객의 경우 [Adobe 라이선스 웹 사이트](https://licensing.adobe.com).

* Adobe 파트너인 경우 [Adobe 파트너 교육 프로그램](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) AEM 6.5를 요청합니다.

AEM을 다운로드한 후 AEM 작성자 인스턴스를 설정하는 방법은 를 참조하십시오. [배포 및 유지 관리](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html#default-local-install).

### AEM 최신 서비스 팩 다운로드 및 설치 {#servicepack}

자세한 지침은 현재 를 참조하십시오. [AEM 6.5 서비스 팩 릴리스 노트](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html).

**Adobe 고객 지원 문의** 최신 AEM 패키지 또는 서비스 팩을 찾을 수 없는 경우.

## 구성 만들기 {#configure-new-integration-65}

>[!NOTE]
>
>2024년 6월 이후부터는 새 JWT 자격 증명을 만들 수 없습니다. 앞으로 OAuth 자격 증명만 생성됩니다. OAuth 구성 만들기에 대해 자세히 알아보십시오.

Brand Portal을 사용하여 AEM Assets을 구성하려면 AEM Assets 작성자 인스턴스와 Adobe Developer 콘솔 모두에서 구성해야 합니다.

1. Adobe 개발자 콘솔에서 Brand Portal 테넌트(조직)에 대한 프로젝트를 만듭니다.
1. Experience Manager Assets에서 IMS 계정 및 Brand Portal 끝점(조직 URL)을 사용하여 Brand Portal 클라우드 서비스를 구성합니다.
1. Experience Manager Assets에서 Brand Portal으로 자산을 게시하여 구성을 테스트합니다.

<!--
1. In AEM Assets, create an IMS account and generate a public certificate (public key).
1. In Adobe Developer Console, create a project for your Brand Portal tenant (organization).
1. Under the project, configure an API using the public key to create a service account (JWT) connection.
1. Get the service account credentials and JWT payload information.
1. In AEM Assets, configure the IMS account using the service account credentials and JWT payload.
1. In AEM Assets, configure the Brand Portal cloud service using the IMS account and Brand Portal endpoint (organization URL).
1. Test your configuration by publishing an asset from AEM Assets to Brand Portal.
-->

>[!NOTE]
>
>AEM Assets 작성자 인스턴스는 한 개의 Brand Portal 테넌트로만 구성해야 합니다.

Brand Portal을 사용하여 AEM Assets을 처음 구성하는 경우 나열된 순서로 다음 단계를 수행하십시오.

### 새 구성 만들기 {#create-new-configuration}

지정된 시퀀스에서 다음 단계를 수행하여 Brand Portal을 사용하여 Experience Manager Assets을 구성합니다.

1. [Adobe Developer 콘솔에서 OAuth 자격 증명 구성](#config-oauth)
1. [OAuth를 사용하여 새 Adobe IMS 통합 만들기](#create-ims-account-configuration)
1. [클라우드 서비스 구성](#configure-cloud-service)

#### Adobe Developer 콘솔에서 OAuth 자격 증명 구성 {#config-oauth}

[Adobe Developer 콘솔에서 OAuth 자격 증명 구성](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/setting-up-ims-integrations-for-aem#credentials-in-the-developer-console)  Brand Portal API를 선택합니다.

#### OAuth를 사용하여 새 Adobe IMS 통합 만들기 {#create-ims-account-configuration}

[OAuth를 사용하여 새 Adobe IMS 통합 만들기](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/setting-up-ims-integrations-for-aem#creating-oauth-configuration) 드롭다운에서 Brand Portal 를 선택합니다.

#### 클라우드 서비스 구성 {#configure-cloud-service}

<!--
1. [Obtain a public certificate](#public-certificate)
1. [Create service account (JWT) connection](#createnewintegration) 
1. [Configure an IMS account](#create-ims-account-configuration)
1. [Configure cloud service](#configure-cloud-service)
1. [Test configuration](#test-integration)
-->
<!--
### Create IMS configuration {#create-ims-configuration}

The IMS configuration authenticates your AEM Assets Author instance with the Brand Portal tenant. 

IMS configuration includes two steps:

* [Obtain a public certificate](#public-certificate) 
* [Configure an IMS account](#create-ims-account-configuration)

### Obtain public certificate {#public-certificate}

The public key (certificate) authenticates your profile on Adobe Developer Console.

1. Log in to your AEM Assets Author instance. The default URL is `http://localhost:4502/aem/start.html`.

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

1. In the Adobe IMS Configurations page, click **[!UICONTROL Create]**. It redirects to the **[!UICONTROL Adobe IMS Technical Account Configuration]** page. By default, the **Certificate** tab opens.

1. Select **[!UICONTROL Adobe Brand Portal]** in the **[!UICONTROL Cloud Solution]** dropdown list.  

1. Select the **[!UICONTROL Create new certificate]** check box and specify an **alias** for the public key. The alias serves as the name of the public key. 

1. Click **[!UICONTROL Create certificate]**. Then, click **[!UICONTROL OK]** to generate the public key.

   ![Create Certificate](assets/ims-config2.png)

1. Click the **[!UICONTROL Download Public Key]** icon and save the public key (.crt) file on your machine. 

   The public key is used later to configure the API for your Brand Portal tenant and generate service account credentials in Adobe Developer Console.

   ![Download Certificate](assets/ims-config3.png)

1. Click **[!UICONTROL Next]**. 

   In the **Account** tab, an Adobe IMS account is created which requires the service account credentials that are generated in Adobe Developer Console. Keep this page open for now.

   Open a new tab and [create a service account (JWT) connection in Adobe Developer Console](#createnewintegration) so you can get the credentials and JWT payload for configuring the IMS account. 

### Create the service account (JWT) connection {#createnewintegration}

In Adobe Developer Console, projects and APIs are configured at the Brand Portal tenant (organization) level. Configuring an API creates a service account (JWT) connection. There are two methods to configure the API, by generating a key pair (private and public keys) or by uploading a public key. To configure AEM Assets with Brand Portal, you must generate a public key (certificate) in AEM Assets and create credentials in Adobe Developer Console by uploading the public key. These credentials are required to configure the IMS account in AEM Assets. Once the IMS account is configured, you can configure the Brand Portal cloud service in AEM Assets.

To create the service account credentials and JWT payload, do the following:

1. Log in to Adobe Developer Console with system administrator privileges on the IMS organization (Brand Portal tenant). The default URL is [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Ensure that you have selected the correct IMS organization (Brand Portal tenant) from the drop-down (organization) list in the upper-right corner.

1. Click **[!UICONTROL Create new project]**. A blank project with a system-generated name is created for your organization. 

   Click **[!UICONTROL Edit project]** so you can update the **[!UICONTROL Project Title]** and **[!UICONTROL Description]**, and click **[!UICONTROL Save]**.
   
1. In the **[!UICONTROL Project overview]** tab, click **[!UICONTROL Add API]**.

1. In the **[!UICONTROL Add an API window]**, select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Next]**. 

   Ensure that you have access to the AEM Brand Portal service.

1. In the **[!UICONTROL Configure API]** window, click **[!UICONTROL Upload your public key]**. Then, click **[!UICONTROL Select a File]** and upload the public key (.crt file) that you have downloaded in the [obtain public certificate](#public-certificate) section. 

   Click **[!UICONTROL Next]**.

   ![Upload Public Key](assets/service-account3.png)

1. Verify the public key and click **[!UICONTROL Next]**.

1. Select **[!UICONTROL Assets Brand Portal]** as the default product profile and click **[!UICONTROL Save configured API]**. 
-->
<!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->
<!--
   ![Select Product Profile](assets/service-account4.png)

1. Once the API is configured, you are redirected to the API overview page. From the left navigation under **[!UICONTROL Credentials]**, click the **[!UICONTROL Service Account (JWT)]** option.

   >[!NOTE]
   >
   >You can view the credentials and perform actions such as generate JWT tokens, copy credential details, and retrieve client secret.

1. From the **[!UICONTROL Client Credentials]** tab, copy the **[!UICONTROL client ID]**. 

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![Service Account Credentials](assets/service-account5.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]** information. 

You can now use the client ID (API key), client secret, and JWT payload to [configure the IMS account](#create-ims-account-configuration) in AEM Assets.

<!--
### Create Adobe I/O integration {#createnewintegration}

Adobe I/O integration generates API Key, Client Secret, and Payload (JWT) which is required in setting up the IMS Account configurations.

1. Login to Adobe Developer Console with system administrator privileges on the IMS organization of the Brand Portal tenant.

   Default URL: [https://console.adobe.io/](https://console.adobe.io/) 

1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create a new integration page opens. 
   
   Select your organization from the drop-down list.

   In **[!UICONTROL Experience Cloud]**, Select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Continue]**. 

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. If you do not know your organization, contact your administrator.

   ![Create Integration](assets/create-new-integration2.png)

1. Specify a name and description for the integration. Click **[!UICONTROL Select a File from your computer]** and upload the `AEM-Adobe-IMS.crt` file downloaded in the [obtain public certificates](#public-certificate) section.

1. Select the profile of your organization. 

   Or, select the default profile **[!UICONTROL Assets Brand Portal]** and click **[!UICONTROL Create Integration]**. The integration is created.

1. Click **[!UICONTROL Continue to integration details]** to view the integration information. 

   Copy the **[!UICONTROL API Key]** 
   
   Click **[!UICONTROL Retrieve Client Secret]** and copy the Client Secret key.

   ![API Key, Client Secret, and payload information of an integration](assets/create-new-integration3.png)

1. Navigate to **[!UICONTROL JWT]** tab, and copy the **[!UICONTROL JWT payload]**.

   The API Key, Client Secret key, and JWT payload information that is used to create IMS account configuration.
-->
<!--
### Configure the IMS account {#create-ims-account-configuration}

Ensure that you have already performed the following steps:

* [Obtain a public certificate](#public-certificate)
* [Create service account (JWT) connection](#createnewintegration)

To configure the IMS account: 

1. Open the IMS Configuration and navigate to the **[!UICONTROL Account]** tab. You kept the page open while [obtaining the public certificate](#public-certificate).

1. Specify a **[!UICONTROL Title]** for the IMS account.

   In the **[!UICONTROL Authorization Server]** field, specify the URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).  

   Specify client ID in the **[!UICONTROL API key]** field, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]** (JWT payload) that you have copied while [creating the service account (JWT) connection](#createnewintegration).

   Click **[!UICONTROL Create]**.

   The IMS account is configured. 

   ![IMS Account configuration](assets/create-new-integration6.png)
   
1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   Click **[!UICONTROL Check]** in the dialog box. On successful configuration, a message appears that the *Token is retrieved successfully*.

   ![Healthy Configuration confirmation dialog](assets/create-new-integration5.png)

>[!CAUTION]
>
>You must have only one IMS configuration.
>
>Ensure that the IMS configuration passes the health check. If the configuration does not pass the health check, it is invalid. Delete it and create another valid configuration.
-->

1. AEM Assets 작성자 인스턴스에 로그인합니다.

1. **도구** ![도구](assets/do-not-localize/tools.png) 패널에서 **[!UICONTROL 클라우드 서비스]** > **[!UICONTROL AEM Brand Portal]**&#x200B;로 이동합니다.

1. Brand Portal 구성 페이지에서 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

1. 구성에 대한 **[!UICONTROL 제목]**&#x200B;을 지정합니다.

   [IMS 계정을 구성](#create-ims-account-configuration)하는 동안 만든 IMS 구성을 선택합니다.

   다음에서 **[!UICONTROL 서비스 URL]** 필드에 Brand Portal 테넌트 URL을 지정합니다.

   ![Brand Portal 구성 창](assets/create-cloud-service.png)

1. 클릭 **[!UICONTROL 저장 및 닫기]**. 클라우드 구성이 생성됩니다.

   이제 AEM Assets 작성자 인스턴스가 Brand Portal 테넌트로 구성됩니다.

<!--

### Test and validate the configuration {#test-integration}

1. Log in to your AEM Assets cloud instance.

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Replication]**.

   ![The Tools panel](assets/test-integration1.png)

1. In the Replication page, click **[!UICONTROL Agents on Author]**.

   ![Replication page](assets/test-integration2.png)

   You can see the four replication agents created for your Brand Portal tenant. 

   Locate the replication agents of your Brand Portal tenant and click the replication agent URL. 

   ![Assets replication configuration](assets/test-integration3.png)

   >[!NOTE]
   >
   >The replication agents work in parallel and share the job distribution equally, so that it increases the publishing speed by four times the original speed. After the cloud service is configured, additional configuration is not required to enable the replication agents that are activated by default to enable parallel publishing of multiple assets.

1. To verify the connection between AEM Assets and Brand Portal, click the **[!UICONTROL Test Connection]** icon.

   ![Verifying the assets replication settings](assets/test-integration4.png)

   A message appears that your *test package is successfully delivered*.

   ![Test confirmation output](assets/test-integration5.png)

1. Verify the test results on all four replication agents.


   >[!NOTE]
   >
   >Avoid disabling any of the replication agents, as it can cause the replication of the assets (running-in-queue) to fail.
   >
   >Ensure that all the four replication agents are configured to avoid timeout error. See [troubleshoot issues in parallel publishing to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html#connection-timeout).
   >
   >Do not modify any autogenerated settings.

You can now:

* [Publish assets from AEM Assets to Brand Portal](../assets/brand-portal-publish-assets.md)
* [Publish assets from Brand Portal to AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) - Asset Sourcing in Brand Portal 
* [Publish folders from AEM Assets to Brand Portal](../assets/brand-portal-publish-folder.md)
* [Publish collections from AEM Assets to Brand Portal](../assets/brand-portal-publish-collection.md) 
* [Publish presets, schemas, and facets to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publish tags to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

See the [Brand Portal documentation](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) for more information.

-->
<!--
## Upgrade configuration {#upgrade-integration-65}

To upgrade your existing configurations to Adobe Developer Console, do the following steps, in the listed sequence : 

1. [Verify running jobs](#verify-jobs)
1. [Delete existing configurations](#delete-existing-configuration)
1. [Create configuration](#configure-new-integration-65)

### Verify running jobs {#verify-jobs}

Ensure that no publishing job is running on your AEM Assets Author instance before you make any edits. For that, you can verify the status of active jobs on all the four replication agents and ensure that the queues are idle.  

1. Log in to your AEM Assets Author instance.

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Deployment Replication]**.

1. In the Replication page, click **[!UICONTROL Agents on Author]**.

   ![Replication agents for assets](assets/test-integration2.png)

1. Locate the replication agents of your Brand Portal tenant. 
   
   Ensure that the **Queue is Idle** for all the replication agents, and no publishing job is active. 

   ![Replication queue settings](assets/test-integration3.png)

### Delete existing configurations {#delete-existing-configuration}

Run the following checklist while deleting the existing configurations:

* Delete all four replication agents
* Delete Brand Portal cloud service
* Delete Mac user 

1. Log in to your AEM Assets Author instance and open CRX Lite as an administrator. The default URL is `http://localhost:4502/crx/de/index.jsp`.

1. Navigate to `/etc/replications/agents.author` and delete all the four replication agents of your Brand Portal tenant.

   ![Replication agent in CRXDE](assets/delete-replication-agent.png)

1. Navigate to `/etc/cloudservices/mediaportal` and delete the Brand Portal cloud service configuration.

   ![Detail of replication agent in CRXDE](assets/delete-cloud-service.png)

1. Navigate to `/home/users/mac` and delete the **Mac user** of your Brand Portal tenant.

   ![More detail of replication agent in CRXDE](assets/delete-mac-user.png)


You can now [create a configuration](#configure-new-integration-65) by way of the Adobe Developer Console on your AEM 6.5 Author instance. 
-->
