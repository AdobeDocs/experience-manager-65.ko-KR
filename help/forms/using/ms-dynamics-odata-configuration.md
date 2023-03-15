---
title: Microsoft Dynamics OData 구성
seo-title: Microsoft Dynamics ODtata configuration
description: 양식 데이터 모델을 통해 온라인 및 온프레미스 Microsoft Dynamics 서비스를 활용, 통합 및 사용할 수 있습니다.
seo-description: Learn how to leverage integrate and work with online and on-premises Microsoft Dynamics services through form data model.
uuid: 37e59633-484b-4a20-808d-2a0bc0d336cc
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 627507f5-1ffc-48f8-8cc9-5dbc5e409ae3
docset: aem65
feature: Form Data Model
exl-id: 90cc9452-e107-4e57-80a3-f44f0bde132e
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 0%

---

# Microsoft Dynamics OData 구성{#microsoft-dynamics-odata-configuration}

![데이터 통합](assets/data-integeration.png)

Microsoft Dynamics는 고객 계정, 연락처, 리드, 기회 및 사례를 만들고 관리하기 위한 엔터프라이즈 솔루션을 제공하는 고객 관계 관리(CRM) 및 엔터프라이즈 리소스 계획(ERP) 소프트웨어입니다. [AEM Forms 데이터 통합](../../forms/using/data-integration.md) 은(는) Forms을 온라인 및 온프레미스 Microsoft Dynamics 서버와 통합하기 위한 OData 클라우드 서비스 구성을 제공합니다. 이를 통해 Microsoft Dynamics 서비스에 정의된 엔티티, 속성 및 서비스를 기반으로 양식 데이터 모델을 만들 수 있습니다. 양식 데이터 모델을 사용하여 Microsoft Dynamics 서버와 상호 작용하여 비즈니스 워크플로우를 가능하게 하는 적응형 양식을 만들 수 있습니다. 예:

* Microsoft Dynamics 서버에 데이터를 쿼리하고 적응형 양식을 미리 채웁니다.
* 적응형 양식 제출 시 Microsoft Dynamics에 데이터 쓰기
* 양식 데이터 모델에 정의된 사용자 지정 엔터티를 통해 Microsoft Dynamics에서 데이터를 쓰고 그 반대의 경우도 마찬가지입니다

AEM Forms 추가 기능 패키지에는 Microsoft Dynamics를 AEM Forms과 빠르게 통합하는 데 활용할 수 있는 참조 OData 구성도 포함되어 있습니다.

패키지를 설치하면 AEM Forms 인스턴스에서 다음 엔티티 및 서비스를 사용할 수 있습니다.

* MS Dynamics OData Cloud Service(OData 서비스)
* 미리 구성된 Microsoft Dynamics 엔터티 및 서비스를 사용하여 데이터 모델을 만듭니다.

양식 데이터 모델에 사전 구성된 Microsoft Dynamics 엔티티 및 서비스는 AEM 인스턴스에 대한 실행 모드가 로 설정된 경우에만 AEM Forms 인스턴스에서 사용할 수 있습니다 `samplecontent` (기본값). MS Dynamics OData Cloud Service(OData 서비스)는 다른 실행 모드에서도 사용할 수 있습니다. AEM 인스턴스의 실행 모드 구성에 대한 자세한 내용은 [실행 모드](/help/sites-deploying/configure-runmodes.md).

## 사전 요구 사항 {#prerequisites}

Microsoft Dynamics 설정 및 구성을 시작하기 전에 다음 사항이 있는지 확인하십시오.

* 다음을 설치했습니다. [AEM Forms 추가 기능 패키지](../../forms/using/installing-configuring-aem-forms-osgi.md)
* Microsoft Dynamics 365를 온라인으로 구성하거나 다음 Microsoft Dynamics 버전 중 하나의 인스턴스를 설치했습니다.

   * Microsoft Dynamics 365 온-프레미스
   * Microsoft Dynamics 2016 온-프레미스

* [Microsoft Azure Active Directory에 Microsoft Dynamics 온라인 서비스에 대한 응용 프로그램을 등록했습니다.](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). 등록된 서비스에 대한 클라이언트 ID(애플리케이션 ID라고도 함) 및 클라이언트 암호의 값을 기록해 두십시오. 이 값은 다음 기간 동안 사용됩니다. [Microsoft Dynamics 서비스를 위한 클라우드 서비스 구성](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service).

## 등록된 Microsoft Dynamics 응용 프로그램에 대한 회신 URL 설정 {#set-reply-url-for-registered-microsoft-dynamics-application}

등록된 Microsoft Dynamics 응용 프로그램의 회신 URL을 설정하려면 다음을 수행하십시오.

>[!NOTE]
>
>이 절차는 AEM Forms을 온라인 Microsoft Dynamics 서버와 통합하는 경우에만 사용하십시오.

1. Microsoft Azure Active Directory 계정으로 이동하여 다음 클라우드 서비스 구성 URL을에 추가합니다. **회신 URL** 등록된 응용 프로그램에 대한 설정:

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure 디렉터리](assets/azure_directory_new.png)

1. 구성을 저장합니다.

## IFD를 위한 Microsoft Dynamics 구성 {#configure-microsoft-dynamics-for-ifd}

Microsoft Dynamics는 클레임 기반 인증을 사용하여 외부 사용자에게 Microsoft Dynamics CRM 서버의 데이터에 액세스할 수 있도록 합니다. 이를 활성화하려면 다음을 수행하여 IFD(인터넷 연결 배포)용 Microsoft Dynamics를 구성하고 클레임 설정을 구성합니다.

>[!NOTE]
>
>AEM Forms을 온-프레미스 Microsoft Dynamics 서버와 통합하는 경우에만 이 절차를 사용하십시오.

1. 에 설명된 대로 IFD에 대한 Microsoft Dynamics 온-프레미스 인스턴스 구성 [Microsoft Dynamics용 IFD 구성](https://technet.microsoft.com/en-us/library/dn609803.aspx).
1. Windows PowerShell을 사용하여 다음 명령을 실행하여 IFD가 활성화된 Microsoft Dynamics에서 클레임 설정을 구성합니다.

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   다음을 참조하십시오 [CRM 온-프레미스(IFD)에 대한 앱 등록](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) 을 참조하십시오.

## AD FS 컴퓨터에서 OAuth 클라이언트 구성 {#configure-oauth-client-on-ad-fs-machine}

AD FS(Active Directory Federation Services) 컴퓨터에 OAuth 클라이언트를 등록하고 AD FS 컴퓨터에 대한 액세스 권한을 부여하려면 다음을 수행하십시오.

>[!NOTE]
>
>AEM Forms을 온-프레미스 Microsoft Dynamics 서버와 통합하는 경우에만 이 절차를 사용하십시오.

1. 다음 명령을 실행합니다.

   `Add-AdfsClient -ClientId "<Client-ID>" -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   위치:

   * `Client-ID` 는 GUID 생성기를 사용하여 생성할 수 있는 클라이언트 ID입니다.
   * `redirect-uri` 는 AEM Forms에서 Microsoft Dynamics OData 클라우드 서비스의 URL입니다. AEM Forms 패키지와 함께 설치된 기본 클라우드 서비스는 다음 URL에 배포됩니다.
      `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. 다음 명령을 실행하여 AD FS 컴퓨터에 대한 액세스 권한을 부여합니다.

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier "<Client-ID>" -ServerRoleIdentifier <resource> -ScopeNames openid`

   위치:

   * `resource` 는 Microsoft Dynamics 조직 URL입니다.

1. Microsoft Dynamics에서는 HTTPS 프로토콜을 사용합니다. Forms 서버에서 AD FS 끝점을 호출하려면 다음을 사용하여 Microsoft Dynamics 사이트 인증서를 Java 인증서 저장소에 설치합니다. `keytool` AEM Forms을 실행하는 컴퓨터의 명령입니다.

## Microsoft Dynamics 서비스를 위한 클라우드 서비스 구성 {#configure-cloud-service-for-your-microsoft-dynamics-service}

다음 **MS Dynamics OData Cloud Service(OData 서비스)** 구성은 기본 OData 구성과 함께 제공됩니다. Microsoft Dynamics 서비스와 연결하도록 구성하려면 다음을 수행하십시오.

1. 다음으로 이동 **[!UICONTROL 도구 > Cloud Services > 데이터 소스]**&#x200B;을 누르고 `global` 구성 폴더입니다.
1. 선택 **MS Dynamics OData Cloud Service(OData 서비스)** 구성 및 탭 **[!UICONTROL 속성]**. 클라우드 서비스 구성 속성 대화 상자가 열립니다.

   다음에서 **인증 설정** 탭:

   1. 다음에 대한 값 입력 **서비스 루트** 필드. Dynamics 인스턴스로 이동하여 다음 위치로 이동 **개발자 리소스** 서비스 루트 필드에 대한 값을 보려면 다음을 수행하십시오. 예: https://&lt;tenant-name>/api/data/v9.1/

   1. 에서 기본값 바꾸기 **클라이언트 ID**(또한으로 지칭됨) **애플리케이션 ID**), **클라이언트 암호**, **OAuth URL**, **토큰 URL 새로 고침**, **토큰 URL 액세스**, 및 **리소스** Microsoft Dynamics 서비스 구성의 값이 있는 필드입니다. 에서 dynamics 인스턴스 URL을 지정해야 합니다. **리소스** 양식 데이터 모델로 Microsoft Dynamics를 구성하는 필드입니다. 서비스 루트 URL을 사용하여 dynamics 인스턴스 URL을 파생시킵니다. 예를 들어, [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. 지정 **openid** 다음에서 **인증 범위** Microsoft Dynamics의 인증 프로세스용 필드입니다.

   ![인증 설정](assets/dynamics_authentication_settings_new.png)

1. 클릭 **[!UICONTROL OAuth에 연결]**. Microsoft Dynamics 로그인 페이지로 리디렉션됩니다.
1. Microsoft Dynamics 자격 증명으로 로그인하여 을(를) 수락하여 클라우드 서비스 구성이 Microsoft Dynamics 서비스에 연결할 수 있도록 합니다. 클라우드 서비스와 서비스 간 연결을 구축하는 것이 일회성 작업이다.

   그런 다음 OData 구성이 저장되었다는 메시지를 표시하는 클라우드 서비스 구성 페이지로 리디렉션됩니다.

MS Dynamics OData Cloud Service(OData 서비스) 클라우드 서비스가 구성되어 있으며 Dynamics 서비스와 연결되어 있습니다.

## 양식 데이터 모델 만들기 {#create-form-data-model}

양식 데이터 모델인 AEM Forms 패키지를 설치할 때&#x200B;**Microsoft Dynamics FDM**&#x200B;는 AEM 인스턴스에 배포됩니다. 기본적으로 양식 데이터 모델은 MS Dynamics OData Cloud Service(OData 서비스)에 구성된 Microsoft Dynamics 서비스를 데이터 소스로 사용합니다.

양식 데이터 모델을 처음 열 때 구성된 Microsoft Dynamics 서비스에 연결되고 Microsoft Dynamics 인스턴스에서 엔티티를 가져옵니다. Microsoft Dynamics의 &quot;연락처&quot; 및 &quot;리드&quot; 엔티티가 양식 데이터 모델에 이미 추가되었습니다.

양식 데이터 모델을 검토하려면 **[!UICONTROL Forms > 데이터 통합]**. 선택 **Microsoft Dynamics FDM** 및 클릭 **편집** 편집 모드에서 양식 데이터 모델을 엽니다. 또는 다음 URL에서 직접 양식 데이터 모델을 열 수 있습니다.

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![default-fdm-1](assets/default-fdm-1.png)

다음으로 양식 데이터 모델을 기반으로 적응형 양식을 만들어 다음과 같은 다양한 적응형 양식 사용 사례에 사용할 수 있습니다.

* Microsoft Dynamics 엔터티 및 서비스에서 정보를 쿼리하여 적응형 양식 미리 채우기
* 적응형 양식 규칙을 사용하여 양식 데이터 모델에 정의된 Microsoft Dynamics 서버 작업 호출
* 제출된 양식 데이터를 Microsoft Dynamics 엔티티에 쓰기

AEM Forms 패키지와 함께 제공되는 양식 데이터 모델의 사본을 만들고 요구 사항에 맞게 데이터 모델 및 서비스를 구성하는 것이 좋습니다. 향후 패키지에 대한 업데이트가 양식 데이터 모델을 재정의하지 않도록 합니다.

비즈니스 워크플로우에서 양식 데이터 모델을 만들고 사용하는 방법에 대한 자세한 내용은 [데이터 통합](../../forms/using/data-integration.md).
