---
title: 스마트 컨텐츠 서비스를 사용하여 자산 태그 지정 구성
description: 에서 스마트 태그 지정 및 향상된 스마트 태그 지정을 구성하는 방법에 대해 알아봅니다 [!DNL Adobe Experience Manager](스마트 컨텐츠 서비스 사용)
role: Admin
feature: Tagging,Smart Tags
solution: Experience Manager, Experience Manager Assets
source-git-commit: d8d821a64b39b312168733126de8929c04016ff1
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 7%

---

# OAuth 자격 증명에 대한 스마트 태그 문제 해결 {#oauth-config}

에 대한 동의를 채택하려면 개방형 인증 구성이 필요합니다. [!DNL Adobe Experience Manager] 스마트 컨텐츠 서비스와 안전한 방식으로 상호 작용하는 애플리케이션.

>[!NOTE]
>
> 2024년 6월 이후부터는 새 JWT 자격 증명을 만들 수 없습니다. 앞으로 OAuth 서버 간 자격 증명만 생성됩니다.
> JWT 통합은 기존 AMS 및 온프레미스 사용자에 대해서만 2025년 1월까지 계속 작동합니다.

## 새 AMS 사용자에 대한 OAuth 구성 {#oauth-config-existing-ams-users}

을(를) 참조하십시오 [스마트 컨텐츠 서비스 구성](#integrate-adobe-io) 새 사용자에 대한 OAuth 서비스 구성 완료되면 다음을 따르십시오 [단계](#prereqs-config-oauth-onprem).

>[!NOTE]
>
>필요한 경우 다음 사항에 따라 지원 티켓을 제출할 수 있습니다. [지원 프로세스](https://experienceleague.adobe.com/?lang=en&amp;support-tab=home#support).

## 기존 AMS 사용자에 대한 OAuth 구성 {#oauth-config-new-ams-users}

이 방법론의 단계를 수행하기 전에 다음을 구현해야 합니다.

### 사전 요구 사항 {#prereqs-config-oauth-onprem}

OAuth 구성을 사용하려면 다음 사전 요구 사항이 필요합니다.

* 에서 새 OAuth 통합 만들기 [개발자 콘솔](https://developer.adobe.com/console/user/servicesandapis). 사용 `ClientID`, `ClientSecret`, `OrgID`및 아래 단계의 기타 속성:
* 이 경로에서 다음 파일을 찾을 수 있습니다. `/apps/system/config in crx/de`:
   * `com.**adobe**.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`
   * `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`

### 기존 AMS 및 On prem 사용자에 대한 OAuth 구성 {#steps-config-oauth-onprem}

시스템 관리자가 아래 단계를 수행할 수 있습니다. AMS 고객은 Adobe 담당자에게 연락하거나 다음 사항에 따라 지원 티켓을 제출할 수 있습니다. [지원 프로세스](https://experienceleague.adobe.com/?lang=en&amp;support-tab=home#support).

1. 에서 아래 속성을 추가하거나 업데이트합니다. `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`:

   * `auth.token.provider.authorization.grants="client_credentials"`
   * `auth.token.provider.orgId="<OrgID>"`
   * `auth.token.provider.default.claims=("\"iss\"\ :\ \"<OrgID>\"")`
   * `auth.token.provider.scope="read_pc.dma_smart_content,\ openid,\ AdobeID,\ additional_info.projectedProductContext"`
     `auth.token.validator.type="adobe-ims-similaritysearch"`
   * 업데이트 `auth.token.provider.client.id` (새 OAuth 구성의 클라이언트 ID 포함)
   * 업데이트 `auth.access.token.request` 끝 `"https://ims-na1.adobelogin.com/ims/token/v3"`
1. 파일 이름을 로 변경합니다. `com.adobe.granite.auth.oauth.accesstoken.provider-<randomnumber>.config`.
1. 에서 아래 단계를 수행합니다. `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`:
   * 새 OAuth 통합에서 클라이언트 암호로 auth.ims.client.secret 속성을 업데이트합니다.
   * 파일 이름을 로 변경합니다. `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl-<randomnumber>.config`
1. CRXDE와 같은 콘텐츠 저장소 개발 콘솔의 모든 변경 사항을 저장합니다.
<!--
1. Navigate to `/system/console/configMgr` and replace the OSGi configuration from `.<randomnumber>` to `-<randomnumber>`.
1. Delete the old OSGi configuration for `"Access Token provider name: adobe-ims-similaritysearch"` in `/system/console/configMgr`.
-->
1. 위치 `System/console/configMgr`, 의 이전 구성을 삭제합니다. `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl` 및 액세스 토큰 공급자 이름 `adobe-ims-similaritysearch`.
1. 콘솔을 다시 시작합니다.

## 구성 유효성 검사 {#validate-the-configuration}

구성을 완료한 후 JMX MBean을 사용하여 구성의 유효성을 검사할 수 있습니다. 유효성을 검사하려면 다음 단계를 수행합니다.

1. 액세스 권한 [!DNL Experience Manager] 서버 위치 `https://[aem_server]:[port]`.

1. 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]** OSGi 콘솔을 엽니다. 클릭 **[!UICONTROL 기본] > [!UICONTROL JMX]**.

1. `com.day.cq.dam.similaritysearch.internal.impl`를 클릭합니다. 열림 **[!UICONTROL 유사성기타 작업 검색]**.

1. `validateConfigs()`를 클릭합니다. 다음에서 **[!UICONTROL 구성 유효성 검사]** 대화 상자, 클릭 **[!UICONTROL 호출]**.

유효성 검사 결과는 동일한 대화 상자에 표시됩니다.

## Adobe Developer 콘솔과 통합 {#integrate-adobe-io}

새 사용자로서 Adobe Developer 콘솔과 통합하면 [!DNL Experience Manager] 서버는 요청을 스마트 컨텐츠 서비스로 전달하기 전에 Adobe Developer 콘솔 게이트웨이로 서비스 자격 증명을 인증합니다. 통합하려면 조직에 대한 관리자 권한이 있는 Adobe ID 계정과, 조직에 대해 구매 및 활성화된 Smart Content Service 라이선스가 필요합니다.

스마트 컨텐츠 서비스를 구성하려면 다음 최상위 단계를 수행합니다.

1. 공개 키를 생성하려면 [스마트 컨텐츠 서비스 만들기](#obtain-public-certificate) 에서 구성 [!DNL Experience Manager]. [공개 인증서 다운로드](#obtain-public-certificate) OAuth 통합용.

1. *[기존 사용자인 경우 적용할 수 없음]* [Adobe Developer 콘솔에서 통합 만들기](#create-adobe-i-o-integration).

1. [배포 구성](#configure-smart-content-service) Adobe Developer 콘솔에서 API 키 및 기타 자격 증명 사용.

1. [구성을 테스트합니다](#validate-the-configuration).

## 스마트 컨텐츠 서비스 구성을 만들어 공개 인증서 다운로드 {#download-public-certificate}

공개 인증서를 사용하면 Adobe Developer 콘솔에서 프로필을 인증할 수 있습니다.

1. 다음에서 [!DNL Experience Manager] 사용자 인터페이스, 액세스 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL 이전 Cloud Service]**.

1. Cloud Service 페이지에서 **[!UICONTROL 지금 구성]** 아래에 **[!UICONTROL 에셋 스마트 태그]**.

1. 다음에서 **[!UICONTROL 구성 만들기]** 대화 상자에서 스마트 태그 구성의 제목과 이름을 지정합니다. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

1. 다음에서 **[!UICONTROL AEM 스마트 컨텐츠 서비스]** 대화 상자에서 다음 값을 사용합니다.

   **[!UICONTROL 서비스 URL]**: `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   예, `https://smartcontent.adobe.io/apac`. 다음을 지정할 수 있습니다. `na`, `emea`, 또는, `apac` 는 Experience Manager 작성자 인스턴스가 호스팅되는 지역입니다.

   >[!NOTE]
   >
   >Experience Manager Managed Service가 2022년 9월 1일 이전에 프로비저닝된 경우 다음 서비스 URL을 사용하십시오.
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 인증 서버]**: `https://ims-na1.adobelogin.com`

   지금은 다른 필드를 비워 둡니다(나중에 제공). **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

   ![컨텐츠 서비스 URL을 제공하는 스마트 컨텐츠 서비스 Experience Manager 대화 상자](assets/aem_scs12.png)

   *그림: 콘텐츠 서비스 URL을 제공하는 스마트 콘텐츠 서비스 대화 상자*

   >[!NOTE]
   >
   >다음으로 제공된 URL [!UICONTROL 서비스 URL] 는 브라우저를 통해 액세스할 수 없으며 404 오류를 생성합니다. 구성이 의 동일한 값으로 정상 작동합니다. [!UICONTROL 서비스 URL] 매개 변수. 전체 서비스 상태 및 유지 관리 일정은 다음을 참조하십시오. [https://status.adobe.com](https://status.adobe.com).

1. 클릭 **[!UICONTROL OAuth 통합을 위한 공개 인증서 다운로드]**&#x200B;및 공개 인증서 파일 다운로드 `AEM-SmartTags.crt`. 또한 Adobe 개발자 콘솔에서 이 인증서를 더 이상 업로드할 필요가 없습니다.

   ![스마트 태그 지정 서비스를 위해 만들어진 설정의 표현입니다](assets/smart-tags-download-public-cert1.png)

   *그림: 스마트 태그 지정 서비스 설정*

## Adobe Developer 콘솔 통합 만들기 {#create-adobe-i-o-integration}

스마트 컨텐츠 서비스 API를 사용하려면 Adobe Developer 콘솔에서 통합을 만들어 다음을 얻으십시오 [!UICONTROL API 키] (생성된 위치 [!UICONTROL 클라이언트 ID] Adobe Developer 콘솔 통합 필드 [!UICONTROL 기술 계정 ID], [!UICONTROL 조직 ID], 및 [!UICONTROL 클라이언트 암호] 대상 [!UICONTROL 자산 스마트 태그 지정 서비스 설정] 의 클라우드 구성 [!DNL Experience Manager].

1. 액세스 [https://developer.adobe.com/console/](https://developer.adobe.com/console/) 을 클릭합니다. 적절한 계정을 선택하고 관련 조직 역할이 시스템 관리자인지 확인합니다.

1. 원하는 이름으로 프로젝트를 만듭니다. **[!UICONTROL API 추가]**&#x200B;를 클릭합니다.

1. **[!UICONTROL API 추가]** 페이지에서 **[!UICONTROL Experience Cloud]**&#x200B;를 선택하고 **[!UICONTROL 스마트 컨텐츠]**&#x200B;를 선택합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. 다음을 선택합니다. **[!UICONTROL OAuth 서버 간]** 인증 방법을 참조하십시오.

1. 추가/수정 **[!UICONTROL 자격 증명 이름]** 필요에 따라. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. 제품 프로필 선택 **[!UICONTROL 스마트 컨텐츠 서비스]**. 클릭 **[!UICONTROL 구성된 API 저장]**. OAuth API는 추가 사용을 위해 연결된 자격 증명 아래에 추가됩니다. 다음을 복사할 수 있습니다. [!UICONTROL API 키(클라이언트 ID)] 또는 [!UICONTROL 액세스 토큰 생성] 거기서...
<!--
1. On the **[!UICONTROL Select product profiles]** page, select **[!UICONTROL Smart Content Services]**. Click **[!UICONTROL Save configured API]**.

   A page displays more information about the configuration. Keep this page open to copy and add these values in [!UICONTROL Assets Smart Tagging Service Settings] of cloud configuration in [!DNL Experience Manager] to configure smart tags.

   ![In the Overview tab, you can review the information provided for integration.](assets/integration_details.png)


   *Figure: Details of integration in Adobe Developer Console*
-->

![oauth 구성](assets/oauth-config.png)
*그림: Adobe Developer 콘솔에서 구성된 OAuth 서버 간*

## 스마트 컨텐츠 서비스 구성 {#configure-smart-content-service}

통합을 구성하려면 다음 값을 사용합니다. [!UICONTROL 기술 계정 ID], [!UICONTROL 조직 ID], [!UICONTROL 클라이언트 암호], 및 [!UICONTROL 클라이언트 ID] Adobe Developer 콘솔 통합의 필드입니다. 스마트 태그 클라우드 구성을 만들면 [!DNL Experience Manager] 배포.

1. 위치 [!DNL Experience Manager], 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL 이전 Cloud Service]** 을(를) 열려면 [!UICONTROL Cloud Service] 콘솔.

1. 아래 **[!UICONTROL 에셋 스마트 태그]**&#x200B;위에서 만든 구성을 엽니다. 서비스 설정 페이지에서 **[!UICONTROL 편집]**.

1. In the **[!UICONTROL AEM Smart Content Service]** dialog, use the pre-populated values for the **[!UICONTROL Service URL]** and **[!UICONTROL Authorization Server]** fields.

1. 필드용 [!UICONTROL Api 키], [!UICONTROL 기술 계정 ID], [!UICONTROL 조직 ID], 및 [!UICONTROL 클라이언트 암호]에서 생성된 다음 값을 복사하여 사용합니다. [Adobe Developer 콘솔 통합](#create-adobe-i-o-integration).

   | [!UICONTROL 자산 스마트 태그 지정 서비스 설정] | [!DNL Adobe Developer Console] 통합 필드 |
   |--- |--- |
   | [!UICONTROL Api 키] | [!UICONTROL 클라이언트 ID] |
   | [!UICONTROL 기술 계정 ID] | [!UICONTROL 기술 계정 ID] |
   | [!UICONTROL 조직 ID] | [!UICONTROL 조직 ID] |
   | [!UICONTROL 클라이언트 암호] | [!UICONTROL 클라이언트 암호] |

>[!MORELIKETHIS]
>
>* [개요 및 스마트 태그 교육 방법](enhanced-smart-tags.md)
>* [스마트 태깅 구성](config-smart-tagging.md)
>* [스마트 태그에 대한 비디오 튜토리얼](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)
