---
title: 스마트 컨텐츠 서비스를 사용하여 자산 태그 지정 구성
description: 스마트 컨텐츠 서비스를 사용하여  [!DNL Adobe Experience Manager]에서 스마트 태그 지정 및 향상된 스마트 태그 지정을 구성하는 방법에 대해 알아봅니다.
role: Admin
feature: Tagging,Smart Tags
solution: Experience Manager, Experience Manager Assets
exl-id: 9caee314-697b-4a7b-b991-10352da17f2c
source-git-commit: ab9292c491cc9dfcd8f239ba279b1e0ae6d1560f
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 6%

---

# OAuth 자격 증명에 대한 스마트 태그 문제 해결 {#oauth-config}

스마트 컨텐츠 서비스와 보안 방식으로 상호 작용하려면 [!DNL Adobe Experience Manager] 응용 프로그램에 대한 동의를 채택하려면 공개 권한 부여 구성이 필요합니다.

>[!NOTE]
>
> 2024년 6월 이후부터는 새 JWT 자격 증명을 만들 수 없습니다. 앞으로 OAuth 서버 간 자격 증명만 생성됩니다.
> JWT 통합은 기존 AMS 및 온프레미스 사용자에 대해서만 2025년 1월까지 계속 작동합니다.

## 새 AMS 사용자에 대한 OAuth 구성 {#oauth-config-existing-ams-users}

새 사용자에 대한 OAuth 서비스 구성은 [스마트 콘텐츠 서비스 구성](#integrate-adobe-io)을 참조하십시오. 완료되면 다음 [단계](#prereqs-config-oauth-onprem)를 수행합니다.

>[!NOTE]
>
>필요한 경우 [지원 프로세스](https://experienceleague.adobe.com/?lang=en&amp;support-tab=home#support)에 따라 지원 티켓을 제출할 수 있습니다.

## 기존 AMS 사용자에 대한 OAuth 구성 {#oauth-config-new-ams-users}

이 방법론의 단계를 수행하기 전에 다음을 구현해야 합니다.

### 사전 요구 사항 {#prereqs-config-oauth-onprem}

OAuth 구성을 사용하려면 다음 사전 요구 사항이 필요합니다.

* [Developer Console](https://developer.adobe.com/console/user/servicesandapis)에서 새 OAuth 통합을 만듭니다. 아래 단계에서 `ClientID`, `ClientSecret`, `OrgID` 및 기타 속성을 사용하십시오.
* 이 경로 `/apps/system/config in crx/de`에서 다음 파일을 찾을 수 있습니다.
   * `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`
   * `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`

### 기존 AMS 및 On prem 사용자에 대한 OAuth 구성 {#steps-config-oauth-onprem}

시스템 관리자는 **CRXDE**&#x200B;에서 아래 단계를 수행할 수 있습니다. AMS 고객은 Adobe 담당자에게 연락하거나 [지원 프로세스](https://experienceleague.adobe.com/?lang=en&amp;support-tab=home#support)에 따라 지원 티켓을 제출할 수 있습니다.

1. `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`에서 아래 속성을 추가하거나 업데이트하십시오.

   * `auth.token.provider.authorization.grants="client_credentials"`
   * `auth.token.provider.orgId="<OrgID>"`
   * `auth.token.provider.default.claims=("\"iss\"\ :\ \"<OrgID>\"")`
   * `auth.token.provider.scope="read_pc.dma_smart_content,\ openid,\ AdobeID,\ additional_info.projectedProductContext"`
     `auth.token.validator.type="adobe-ims-similaritysearch"`
   * 새 OAuth 구성의 클라이언트 ID로 `auth.token.provider.client.id`을(를) 업데이트합니다.
   * `auth.access.token.request`을(를) `"https://ims-na1.adobelogin.com/ims/token/v3"`(으)로 업데이트
1. 파일 이름을 `com.adobe.granite.auth.oauth.accesstoken.provider-<randomnumber>.config`(으)로 바꾸십시오.

   >[!IMPORTANT]
   >
   >점(.)을 하이픈(-)을 접두사로 사용하여 `<randomnumber>`에 대체합니다.

1. `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`에서 아래 단계를 수행합니다.
   * 새 OAuth 통합에서 클라이언트 암호로 auth.ims.client.secret 속성을 업데이트합니다.
   * 파일 이름을 `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl-<randomnumber>.config`(으)로 바꾸기
1. CRXDE와 같은 콘텐츠 저장소 개발 콘솔의 모든 변경 사항을 저장합니다.
<!--
1. Navigate to `/system/console/configMgr` and replace the OSGi configuration from `.<randomnumber>` to `-<randomnumber>`.
1. Delete the old OSGi configuration for `"Access Token provider name: adobe-ims-similaritysearch"` in `/system/console/configMgr`.
-->
1. `System/console/configMgr`에서 이전 구성 파일과 새 구성 파일을 모두 볼 수 있습니다. `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl` 및 액세스 토큰 공급자 이름 `adobe-ims-similaritysearch`에 대한 이전 구성을 삭제하십시오. 이전 구성이 아니라 업데이트된 구성만 있는지 확인합니다.
1. 콘솔을 다시 시작합니다.

## 구성 유효성 검사 {#validate-the-configuration}

구성을 완료한 후 JMX MBean을 사용하여 구성의 유효성을 검사할 수 있습니다. 유효성을 검사하려면 다음 단계를 수행합니다.

1. `https://[aem_server]:[port]`에서 [!DNL Experience Manager] 서버에 액세스합니다.

1. **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**(으)로 이동하여 OSGi 콘솔을 엽니다. **[!UICONTROL 기본] > [!UICONTROL JMX]**&#x200B;을(를) 클릭합니다.

1. `com.day.cq.dam.similaritysearch.internal.impl`를 클릭합니다. **[!UICONTROL SimilaritySearch 기타 작업]**&#x200B;을 엽니다.

1. `validateConfigs()`를 클릭합니다. **[!UICONTROL 구성 유효성 검사]** 대화 상자에서 **[!UICONTROL 호출]**&#x200B;을 클릭합니다.

유효성 검사 결과는 동일한 대화 상자에 표시됩니다.

>[!NOTE]
>
>`unsupported_grant_type` 오류가 발생하면 Granite 핫픽스를 설치해 보십시오. [서비스 계정(JWT)에서 OAuth 서버 간 자격 증명으로 마이그레이션](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-24660)을 참조하세요.

## Adobe Developer Console과 통합 {#integrate-adobe-io}

새 사용자는 [!DNL Experience Manager] 서버에서 Adobe Developer Console과 통합하면 요청을 스마트 컨텐츠 서비스로 전달하기 전에 Adobe Developer Console 게이트웨이로 서비스 자격 증명을 인증합니다. 통합하려면 조직에 대한 관리자 권한이 있는 Adobe ID 계정과, 조직에 대해 구매 및 활성화된 Smart Content Service 라이선스가 필요합니다.

스마트 컨텐츠 서비스를 구성하려면 다음 최상위 단계를 수행합니다.

<!--![Experience Manager Smart Content Service dialog to provide content service URL](assets/config-oauth.png)-->

1. 공개 키를 생성하려면 [!DNL Experience Manager]에서 [스마트 콘텐츠 서비스를 만들기](#oauth-config) 구성하십시오. OAuth 통합을 위해 [공개 인증서를 다운로드합니다](#oauth-config).

1. *[기존 사용자인 경우 적용할 수 없음]* [Adobe Developer Console에서 통합 만들기](#create-adobe-i-o-integration).

1. API 키 및 Adobe Developer Console의 기타 자격 증명을 사용하여 [배포를 구성](#configure-smart-content-service)합니다.

1. [구성을 테스트합니다](#validate-the-configuration).

## 스마트 컨텐츠 서비스 구성을 만들어 공개 인증서 다운로드 {#download-public-certificate}

공개 인증서를 사용하면 Adobe Developer Console에서 프로필을 인증할 수 있습니다.

1. [!DNL Experience Manager] 사용자 인터페이스에서 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL 기존 Cloud Service]**&#x200B;에 액세스합니다.

1. Cloud Service 페이지에서 **[!UICONTROL Assets 스마트 태그]**&#x200B;의 **[!UICONTROL 지금 구성]**&#x200B;을 클릭합니다.

1. **[!UICONTROL 구성 만들기]** 대화 상자에서 스마트 태그 구성의 제목과 이름을 지정합니다. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

1. **[!UICONTROL AEM 스마트 컨텐츠 서비스]** 대화 상자에서 다음 값을 사용하십시오.

   **[!UICONTROL 서비스 URL]**: `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   예, `https://smartcontent.adobe.io/apac`. `na`, `emea` 또는 `apac`을(를) Experience Manager 작성자 인스턴스가 호스팅되는 지역으로 지정할 수 있습니다.

   >[!NOTE]
   >
   >Experience Manager Managed Service가 2022년 9월 1일 이전에 프로비저닝된 경우 다음 서비스 URL을 사용하십시오.
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 인증 서버]**: `https://ims-na1.adobelogin.com`

   지금은 다른 필드를 비워 둡니다(나중에 제공). **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

   콘텐츠 서비스 URL을 제공하기 위한 ![스마트 콘텐츠 서비스 Experience Manager 대화 상자](assets/aem_scs12.png)

   *그림: 콘텐츠 서비스 URL을 제공하는 스마트 콘텐츠 서비스 대화 상자*

   >[!NOTE]
   >
   >[!UICONTROL 서비스 URL](으)로 제공된 URL은 브라우저를 통해 액세스할 수 없으며 404 오류가 발생합니다. [!UICONTROL 서비스 URL] 매개 변수의 동일한 값으로 구성이 정상적으로 작동합니다. 전체 서비스 상태 및 유지 관리 일정은 [https://status.adobe.com](https://status.adobe.com)을(를) 참조하십시오.

1. **[!UICONTROL OAuth 통합을 위한 공개 인증서 다운로드]**&#x200B;를 클릭하고 공개 인증서 파일 `AEM-SmartTags.crt`을(를) 다운로드합니다. 또한 Adobe Developer 콘솔에서 이 인증서를 더 이상 업로드할 필요가 없습니다.

   ![스마트 태그 지정 서비스에 대해 만들어진 설정의 표현](assets/smart-tags-download-public-cert1.png)

   *그림: 스마트 태그 지정 서비스 설정.*

## Adobe Developer Console 통합 만들기 {#create-adobe-i-o-integration}

스마트 컨텐츠 서비스 API를 사용하려면 Adobe Developer Console에서 통합을 만들어 [!DNL Experience Manager]의 클라우드 구성 [!UICONTROL Assets 스마트 태깅 서비스 설정]에 대한 [!UICONTROL API 키](Adobe Developer Console 통합의 [!UICONTROL 클라이언트 ID] 필드에서 생성됨), [!UICONTROL 기술 계정 ID], [!UICONTROL 조직 ID] 및 [!UICONTROL 클라이언트 암호]를 얻으십시오.

1. 브라우저에서 [https://developer.adobe.com/console/](https://developer.adobe.com/console/)에 액세스합니다. 적절한 계정을 선택하고 관련 조직 역할이 시스템 관리자인지 확인합니다.

1. 원하는 이름으로 프로젝트를 만듭니다. **[!UICONTROL API 추가]**&#x200B;를 클릭합니다.

1. **[!UICONTROL API 추가]** 페이지에서 **[!UICONTROL Experience Cloud]**&#x200B;를 선택하고 **[!UICONTROL 스마트 컨텐츠]**&#x200B;를 선택합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. **[!UICONTROL OAuth 서버 간]** 인증 방법을 선택하십시오.

1. 필요에 따라 **[!UICONTROL 자격 증명 이름]**&#x200B;을(를) 추가/수정합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. 제품 프로필 **[!UICONTROL 스마트 컨텐츠 서비스]**&#x200B;를 선택하십시오. **[!UICONTROL 구성된 API 저장]**&#x200B;을 클릭합니다. OAuth API는 추가 사용을 위해 연결된 자격 증명에 추가됩니다. [!UICONTROL API 키(클라이언트 ID)] 또는 [!UICONTROL 액세스 토큰 생성]을 복사할 수 있습니다.
<!--
1. On the **[!UICONTROL Select product profiles]** page, select **[!UICONTROL Smart Content Services]**. Click **[!UICONTROL Save configured API]**.

   A page displays more information about the configuration. Keep this page open to copy and add these values in [!UICONTROL Assets Smart Tagging Service Settings] of cloud configuration in [!DNL Experience Manager] to configure smart tags.

   ![In the Overview tab, you can review the information provided for integration.](assets/integration_details.png)


   *Figure: Details of integration in Adobe Developer Console*
-->

![oauth 구성](assets/oauth-config.png)
*그림: Adobe Developer Console에서 OAuth 서버 간 구성*

## 스마트 컨텐츠 서비스 구성 {#configure-smart-content-service}

통합을 구성하려면 Adobe Developer Console 통합에서 [!UICONTROL 기술 계정 ID], [!UICONTROL 조직 ID], [!UICONTROL 클라이언트 암호] 및 [!UICONTROL 클라이언트 ID] 필드 값을 사용합니다. 스마트 태그 클라우드 구성을 만들면 [!DNL Experience Manager] 배포의 API 요청을 인증할 수 있습니다.

1. [!DNL Experience Manager]에서 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL 기존 Cloud Services]**(으)로 이동하여 [!UICONTROL Cloud Services] 콘솔을 엽니다.

1. **[!UICONTROL Assets 스마트 태그]**&#x200B;에서 위에서 만든 구성을 엽니다. 서비스 설정 페이지에서 **[!UICONTROL 편집]**&#x200B;을 클릭합니다.

1. In the **[!UICONTROL AEM Smart Content Service]** dialog, use the pre-populated values for the **[!UICONTROL Service URL]** and **[!UICONTROL Authorization Server]** fields.

1. 필드 [!UICONTROL Api 키], [!UICONTROL 기술 계정 ID], [!UICONTROL 조직 ID] 및 [!UICONTROL 클라이언트 암호]의 경우 [Adobe Developer Console 통합](#create-adobe-i-o-integration)에서 생성된 다음 값을 복사하여 사용하십시오.

   | [!UICONTROL Assets 스마트 태그 지정 서비스 설정] | [!DNL Adobe Developer Console] 통합 필드 |
   |--- |--- |
   | [!UICONTROL Api 키] | [!UICONTROL 클라이언트 ID] |
   | [!UICONTROL 기술 계정 ID] | [!UICONTROL 기술 계정 ID] |
   | [!UICONTROL 조직 ID] | [!UICONTROL 조직 ID] |
   | [!UICONTROL 클라이언트 암호] | [!UICONTROL 클라이언트 암호] |

>[!MORELIKETHIS]
>
>* [개요 및 스마트 태그 교육 방법](enhanced-smart-tags.md)
>* [스마트 태그 지정 구성](config-smart-tagging.md)
>* 스마트 태그에 대한 [비디오 튜토리얼](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)
