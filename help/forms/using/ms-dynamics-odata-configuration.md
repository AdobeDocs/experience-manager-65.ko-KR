---
title: Microsoft Dynamics OData 구성
seo-title: Microsoft Dynamics ODtata 구성
description: 양식 데이터 모델을 통해 온라인 및 온프레미스 Microsoft Dynamics 서비스를 활용하고 통합 및 사용할 수 있습니다.
seo-description: 양식 데이터 모델을 통해 온라인 및 온프레미스 Microsoft Dynamics 서비스를 통합 및 사용하는 방법을 알아봅니다.
uuid: 37e59633-484b-4a20-808d-2a0bc0d336cc
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 627507f5-1ffc-48f8-8cc9-5dbc5e409ae3
docset: aem65
feature: 양식 데이터 모델
exl-id: 90cc9452-e107-4e57-80a3-f44f0bde132e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 0%

---

# Microsoft Dynamics OData 구성{#microsoft-dynamics-odata-configuration}

![데이터 통합](assets/data-integeration.png)

Microsoft Dynamics는 고객 계정, 연락처, 리드, 기회 및 사례를 만들고 관리하는 엔터프라이즈 솔루션을 제공하는 CRM(Customer Relationship Management) 및 ERP(Enterprise Resource Planning) 소프트웨어입니다. [AEM Forms 데이터 ](../../forms/using/data-integration.md) 통합은 온라인 및 온프레미스 Microsoft Dynamics 서버와 Forms을 통합하는 OData 클라우드 서비스 구성을 제공합니다. Microsoft Dynamics 서비스에 정의된 엔터티, 특성 및 서비스를 기반으로 양식 데이터 모델을 만들 수 있습니다. 양식 데이터 모델을 사용하여 Microsoft Dynamics 서버와 상호 작용하는 적응형 양식을 만들어 비즈니스 워크플로우를 활성화할 수 있습니다. 예:

* Microsoft Dynamics 서버에 데이터를 쿼리하고 적응형 양식 미리 채우기
* 적응형 양식 제출 시 Microsoft Dynamics에 데이터 쓰기
* 양식 데이터 모델에 정의된 사용자 지정 엔터티를 통해 Microsoft Dynamics에서 데이터를 쓰고 그 반대로

AEM Forms 추가 기능 패키지에는 Microsoft Dynamics를 AEM Forms과 빠르게 통합할 수 있는 참조 OData 구성이 포함되어 있습니다.

패키지가 설치되면 AEM Forms 인스턴스에서 다음 엔티티 및 서비스를 사용할 수 있습니다.

* MS Dynamics OData Cloud Service(OData 서비스)
* 미리 구성된 Microsoft Dynamics 및 서비스를 사용하는 양식 데이터 모델.

양식 데이터 모델의 미리 구성된 Microsoft Dynamics 및 서비스는 AEM 인스턴스에 대한 실행 모드가 `samplecontent`(기본값)으로 설정된 경우에만 AEM Forms 인스턴스에서 사용할 수 있습니다. 다른 실행 모드에서도 MS Dynamics OData Cloud Service(OData 서비스)를 사용할 수 있습니다. AEM 인스턴스에 대한 실행 모드 구성에 대한 자세한 내용은 [실행 모드](/help/sites-deploying/configure-runmodes.md)를 참조하십시오.

## 전제 조건 {#prerequisites}

Microsoft Dynamics 설정 및 구성을 시작하기 전에 다음을 확인하십시오.

* [AEM Forms 추가 기능 패키지를 설치함](../../forms/using/installing-configuring-aem-forms-osgi.md)
* Microsoft Dynamics 365를 온라인으로 구성하거나 다음 Microsoft Dynamics 버전 중 하나의 인스턴스를 설치했습니다.

   * Microsoft Dynamics 365 온-프레미스
   * Microsoft Dynamics 2016 온-프레미스

* [Microsoft Azure Active Directory에 Microsoft Dynamics 온라인 서비스의 응용 프로그램을 등록했습니다](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). 등록된 서비스에 대한 클라이언트 ID(애플리케이션 ID라고도 함)와 클라이언트 암호 값을 기록해 두십시오. 이 값은 Microsoft Dynamics 서비스](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service)에 대해 클라우드 서비스를 구성하는 동안 사용됩니다.[

## 등록된 Microsoft Dynamics 응용 프로그램에 대한 회신 URL 설정 {#set-reply-url-for-registered-microsoft-dynamics-application}

등록된 Microsoft Dynamics 응용 프로그램의 회신 URL을 설정하려면 다음을 수행하십시오.

>[!NOTE]
>
>AEM Forms을 온라인 Microsoft Dynamics 서버와 통합하는 동안에만 이 절차를 사용하십시오.

1. Microsoft Azure Active Directory 계정으로 이동하여 등록된 응용 프로그램의 **회신 URL** 설정에 다음 클라우드 서비스 구성 URL을 추가하십시오.

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure 디렉토리](assets/azure_directory_new.png)

1. 구성을 저장합니다.

## IFD {#configure-microsoft-dynamics-for-ifd}에 대한 Microsoft Dynamics 구성

Microsoft Dynamics에서는 클레임 기반 인증을 사용하여 Microsoft Dynamics CRM 서버의 데이터에 외부 사용자에게 액세스를 제공합니다. 이 기능을 사용하려면 다음을 수행하여 IFD(인터넷 연결 배포)를 위한 Microsoft Dynamics를 구성하고 클레임 설정을 구성합니다.

>[!NOTE]
>
>이 절차는 AEM Forms과 온-프레미스 Microsoft Dynamics 서버를 통합하는 동안에만 사용합니다.

1. [Microsoft Dynamics](https://technet.microsoft.com/en-us/library/dn609803.aspx)에 설명된 대로 IFD에 대한 Microsoft Dynamics 온-프레미스 인스턴스를 구성합니다.
1. Windows PowerShell을 사용하여 다음 명령을 실행하여 IFD가 활성화된 Microsoft Dynamics에서 클레임 설정을 구성합니다.

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   자세한 내용은 [CRM 온-프레미스(IFD)에 대한 앱 등록](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd)을 참조하십시오.

## AD FS 시스템에서 OAuth 클라이언트 구성 {#configure-oauth-client-on-ad-fs-machine}

AD FS(Active Directory Federation Services) 시스템에 OAuth 클라이언트를 등록하고 AD FS 컴퓨터에 대한 액세스 권한을 부여하려면 다음을 수행합니다.

>[!NOTE]
>
>이 절차는 AEM Forms과 온-프레미스 Microsoft Dynamics 서버를 통합하는 동안에만 사용합니다.

1. 다음 명령을 실행합니다.

   `Add-AdfsClient -ClientId “<Client-ID>” -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   위치:

   * `Client-ID` 는 GUID 생성기를 사용하여 생성할 수 있는 클라이언트 ID입니다.
   * `redirect-uri` 은 AEM Forms에서 Microsoft Dynamics OData 클라우드 서비스의 URL입니다. AEM Forms 패키지와 함께 설치된 기본 클라우드 서비스는 다음 URL에 배포됩니다.
      `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. 다음 명령을 실행하여 AD FS 컴퓨터에 대한 액세스 권한을 부여합니다.

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier “<Client-ID>” -ServerRoleIdentifier <resource> -ScopeNames openid`

   위치:

   * `resource` 는 Microsoft Dynamics 조직 URL입니다.

1. Microsoft Dynamics에서는 HTTPS 프로토콜을 사용합니다. Forms 서버에서 AD FS 끝점을 호출하려면 AEM Forms을 실행하는 컴퓨터에서 `keytool` 명령을 사용하여 Microsoft Dynamics 사이트 인증서를 Java 인증서 저장소에 설치합니다.

## Microsoft Dynamics 서비스 {#configure-cloud-service-for-your-microsoft-dynamics-service}에 대한 클라우드 서비스 구성

**MS Dynamics OData Cloud Service(OData 서비스)** 구성은 기본 OData 구성과 함께 제공됩니다. Microsoft Dynamics 서비스와 연결하도록 구성하려면 다음을 수행합니다.

1. **[!UICONTROL 도구 > Cloud Services > Data Sources]**&#x200B;로 이동하고 `global` 구성 폴더를 탭합니다.
1. **MS Dynamics OData Cloud Service(OData 서비스)** 구성을 선택하고 **[!UICONTROL 속성]**&#x200B;을 탭합니다. 클라우드 서비스 구성 속성 대화 상자가 열립니다.

   **인증 설정** 탭에서 다음을 수행합니다.

   1. **서비스 루트** 필드의 값을 입력합니다. Dynamics 인스턴스로 이동하고 **개발자 리소스**&#x200B;로 이동하여 서비스 루트 필드에 대한 값을 확인합니다. 예: https://&lt;tenant-name>/api/data/v9.1/

   1. **클라이언트 Id**(**응용 프로그램 ID**)와 **클라이언트 암호**, **OAuth URL**, **새로 고침 토큰 URL**, **액세스 토큰 URL** 및 **리소스**&#x200B;의 기본값을 사용자의 Dynamics 구성/Microsoft Dynamics 구성 값으로 바꿉니다. 양식 데이터 모델로 Microsoft Dynamics를 구성하려면 **리소스** 필드에 Dynamics 인스턴스 URL을 지정해야 합니다. 서비스 루트 URL을 사용하여 Dynamics 인스턴스 URL을 파생하십시오. 예: [https://org.crm.dynamics.com](https://org.crm.dynamics.com/)

   1. Microsoft Dynamics에서 인증 프로세스를 위해 **인증 범위** 필드에 **openid**&#x200B;을 지정하십시오.

   ![인증 설정](assets/dynamics_authentication_settings_new.png)

1. **[!UICONTROL OAuth]**&#x200B;에 연결 을 클릭합니다. Microsoft Dynamics 로그인 페이지로 리디렉션됩니다.
1. Microsoft Dynamics 자격 증명으로 로그인하고 클라우드 서비스 구성이 Microsoft Dynamics 서비스에 연결되도록 허용하려면 수락하십시오. 클라우드 서비스와 서비스 간의 연결을 설정하는 일회성 작업입니다.

   그러면 OData 구성이 성공적으로 저장되었다는 메시지가 표시되는 클라우드 서비스 구성 페이지로 리디렉션됩니다.

MS Dynamics OData Cloud Service(OData 서비스) 클라우드 서비스가 구성되어 Dynamics 서비스와 연결되어 있습니다.

## 양식 데이터 모델 {#create-form-data-model} 만들기

AEM Forms 패키지를 설치하면 양식 데이터 모델&#x200B;**Microsoft Dynamics FDM**&#x200B;이 AEM 인스턴스에 배포됩니다. 기본적으로 양식 데이터 모델은 MS Dynamics OData Cloud Service(OData 서비스)에 구성된 Microsoft Dynamics 서비스를 데이터 소스로 사용합니다.

양식 데이터 모델을 처음 열면 구성된 Microsoft Dynamics 서비스에 연결하고 Microsoft Dynamics 인스턴스에서 엔터티를 가져옵니다. Microsoft Dynamics의 &quot;연락처&quot; 및 &quot;리드&quot; 엔터티가 이미 양식 데이터 모델에 추가되었습니다.

양식 데이터 모델을 검토하려면 **[!UICONTROL Forms > 데이터 통합]**&#x200B;으로 이동합니다. **Microsoft Dynamics FDM**&#x200B;을 선택하고 **편집**&#x200B;을 클릭하여 편집 모드에서 양식 데이터 모델을 엽니다. 또는 다음 URL에서 직접 양식 데이터 모델을 열 수 있습니다.

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![default-fdm-1](assets/default-fdm-1.png)

다음으로, 양식 데이터 모델을 기반으로 적응형 양식을 만들고 다음과 같은 다양한 적응형 양식 사용 사례에 사용할 수 있습니다.

* Microsoft Dynamics 엔터티 및 서비스에서 정보를 쿼리하여 적응형 양식 미리 채우기
* 적응형 양식 규칙을 사용하여 양식 데이터 모델에 정의된 Microsoft Dynamics 서버 작업 호출
* Microsoft Dynamics 엔터티에 제출된 양식 데이터를 작성합니다

AEM Forms 패키지와 함께 제공되는 양식 데이터 모델의 사본을 만들고 요구 사항에 맞게 데이터 모델 및 서비스를 구성하는 것이 좋습니다. 향후 패키지 업데이트가 양식 데이터 모델을 무시하지 않도록 합니다.

비즈니스 워크플로우에서 양식 데이터 모델을 만들고 사용하는 방법에 대한 자세한 내용은 [데이터 통합](../../forms/using/data-integration.md)을 참조하십시오.
