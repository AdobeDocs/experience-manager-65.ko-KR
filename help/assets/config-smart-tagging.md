---
title: 스마트 컨텐츠 서비스를 사용하여 자산 태그 지정 구성
description: 스마트 컨텐츠 서비스를 사용하여  [!DNL Adobe Experience Manager]에서 스마트 태그 지정 및 향상된 스마트 태그 지정을 구성하는 방법에 대해 알아봅니다.
contentOwner: AG
role: Admin
feature: Tagging,Smart Tags
exl-id: 9f68804f-ba15-4f83-ab1b-c249424b1396
solution: Experience Manager, Experience Manager Assets
source-git-commit: 5aff321eb52c97e076c225b67c35e9c6d3371154
workflow-type: tm+mt
source-wordcount: '2415'
ht-degree: 19%

---

# 스마트 태그 지정을 위해 [!DNL Assets] 준비 {#configure-asset-tagging-using-the-smart-content-service}

스마트 컨텐츠 서비스를 사용하여 자산에 태그를 지정하려면 [!DNL Experience Manager Assets]을(를) Adobe Developer Console과 통합하여 [!DNL Adobe Sensei]의 스마트 서비스를 사용하십시오. 구성이 완료되면 몇 개의 이미지와 태그를 사용하여 서비스를 교육합니다.

>[!NOTE]
>
>* 새 [!DNL Experience Manager Assets] On-Premise 고객은 스마트 콘텐츠 서비스를 더 이상 사용할 수 없습니다. 이미 이 기능이 활성화되어 있는 기존 온-프레미스 고객은 스마트 컨텐츠 서비스를 계속 사용할 수 있습니다.
>* 스마트 컨텐츠 서비스는 이미 이 기능이 활성화되어 있는 기존 [!DNL Experience Manager Assets] Managed Services 고객이 사용할 수 있습니다.
>* 새로운 [!DNL Experience Manager Assets] Managed Services 고객은 이 문서에 언급된 지침에 따라 스마트 컨텐츠 서비스를 설정할 수 있습니다.

스마트 컨텐츠 서비스를 사용하기 전에 다음을 확인하십시오.

* [Adobe Developer Console과 통합](#integrate-adobe-io).
* [스마트 컨텐츠 서비스를 교육합니다](#training-the-smart-content-service).

* 최신 [[!DNL Experience Manager] 서비스 팩](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html)을 설치하십시오.

## Adobe Developer Console과 통합 {#integrate-adobe-io}

Adobe Developer Console과 통합하면 요청을 스마트 컨텐츠 서비스로 전달하기 전에 [!DNL Experience Manager] 서버에서 Adobe Developer Console 게이트웨이로 서비스 자격 증명을 인증합니다. 통합하려면 조직에 대한 관리자 권한이 있는 Adobe ID 계정과, 조직에 대해 구매 및 활성화된 Smart Content Service 라이선스가 필요합니다.

스마트 컨텐츠 서비스를 구성하려면 다음 최상위 단계를 수행합니다.

1. 공개 키를 생성하려면 [!DNL Experience Manager]에서 [스마트 콘텐츠 서비스를 만들기](#obtain-public-certificate) 구성하십시오. OAuth 통합을 위한 [공개 인증서를 받습니다](#obtain-public-certificate).

1. [Adobe 개발자 콘솔에서 통합을 만들고](#create-adobe-i-o-integration) 생성된 공개 키를 업로드합니다.

1. API 키 및 Adobe Developer Console의 기타 자격 증명을 사용하여 [배포를 구성](#configure-smart-content-service)합니다.

1. [구성을 테스트합니다](#validate-the-configuration).

1. 필요한 경우 [자산 업로드 시 자동 태그 지정을 활성화](#enable-smart-tagging-in-the-update-asset-workflow-optional)합니다.

### 스마트 컨텐츠 서비스 구성을 만들어 공개 인증서 받기 {#obtain-public-certificate}

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

   콘텐츠 서비스 URL을 제공하기 위한 ![스마트 콘텐츠 서비스 Experience Manager 대화 상자](assets/aem_scs.png)


   *그림: 콘텐츠 서비스 URL을 제공하는 스마트 콘텐츠 서비스 대화 상자*

   >[!NOTE]
   >
   >[!UICONTROL 서비스 URL](으)로 제공된 URL은 브라우저를 통해 액세스할 수 없으며 404 오류가 발생합니다. [!UICONTROL 서비스 URL] 매개 변수의 동일한 값으로 구성이 정상적으로 작동합니다. 전체 서비스 상태 및 유지 관리 일정은 [https://status.adobe.com](https://status.adobe.com)을(를) 참조하십시오.

1. **[!UICONTROL OAuth 통합을 위한 공개 인증서 다운로드]**&#x200B;를 클릭하고 공개 인증서 파일 `AEM-SmartTags.crt`을(를) 다운로드합니다.

   ![스마트 태그 지정 서비스에 대해 만들어진 설정의 표현](assets/smart-tags-download-public-cert.png)


   *그림: 스마트 태그 지정 서비스 설정.*

#### 인증서가 만료되면 다시 구성 {#certrenew}

인증서가 만료되면 더 이상 신뢰할 수 없습니다. 만료된 인증서는 갱신할 수 없습니다. 인증서를 추가하려면 다음 단계를 따르십시오.

1. 관리자로 [!DNL Experience Manager] 배포에 로그인합니다. **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 사용자]**&#x200B;를 클릭합니다.

1. **[!UICONTROL dam-update-service]** 사용자를 찾아 클릭합니다. **[!UICONTROL 키 저장소]** 탭을 클릭합니다.

1. 만료된 인증서로 기존의 **[!UICONTROL 유사 검색]** 키 저장소를 삭제합니다. **[!UICONTROL 저장 후 닫기]**&#x200B;를 클릭합니다.

   ![보안 인증서를 추가하려면 키 저장소에서 기존 유사성 검색 항목을 삭제하십시오](assets/smarttags_delete_similaritysearch_keystore.png)


   *그림: 보안 인증서를 추가하려면 키 저장소에서 기존 `similaritysearch` 항목을 삭제하십시오.*

1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Legacy Cloud Services]**. Click **[!UICONTROL Asset Smart Tags]** > **[!UICONTROL Show Configuration]** > **[!UICONTROL Available Configurations]**. Click the required configuration.

1. 공개 인증서를 다운로드하려면 **[!UICONTROL OAuth 통합을 위한 공개 인증서 다운로드]**&#x200B;를 클릭하십시오.

1. [https://console.adobe.io](https://console.adobe.io)에 액세스하여 **[!UICONTROL 통합]** 페이지에서 기존 스마트 콘텐츠 서비스로 이동합니다. 새 인증서를 업로드합니다. 자세한 내용은 [Adobe Developer Console 통합 만들기](#create-adobe-i-o-integration)의 지침을 참조하십시오.

### Adobe Developer Console 통합 만들기 {#create-adobe-i-o-integration}

스마트 컨텐츠 서비스 API를 사용하려면 Adobe Developer Console에서 통합을 만들어 [!DNL Experience Manager]의 클라우드 구성 [!UICONTROL Assets 스마트 태깅 서비스 설정]에 대한 [!UICONTROL API 키](Adobe Developer Console 통합의 [!UICONTROL 클라이언트 ID] 필드에서 생성됨), [!UICONTROL 기술 계정 ID], [!UICONTROL 조직 ID] 및 [!UICONTROL 클라이언트 암호]를 얻으십시오.

1. 브라우저에서 [https://console.adobe.io](https://console.adobe.io/)에 액세스합니다. 적절한 계정을 선택하고 관련 조직 역할이 시스템 관리자인지 확인합니다.

1. 원하는 이름으로 프로젝트를 만듭니다. **[!UICONTROL API 추가]**&#x200B;를 클릭합니다.

1. **[!UICONTROL API 추가]** 페이지에서 **[!UICONTROL Experience Cloud]**&#x200B;를 선택하고 **[!UICONTROL 스마트 컨텐츠]**&#x200B;를 선택합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. **[!UICONTROL 공개 키 업로드]**&#x200B;를 선택합니다. [!DNL Experience Manager]에서 다운로드한 인증서 파일을 제공합니다. [!UICONTROL 공개 키가 업로드되었습니다] 메시지가 표시됩니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   [!UICONTROL 새 서비스 계정(JWT) 자격 증명을 만듭니다] 페이지에 서비스 계정에 대한 공개 키가 표시됩니다.

1. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. **[!UICONTROL 제품 프로필 선택]** 페이지에서 **[!UICONTROL 스마트 컨텐츠 서비스]**&#x200B;를 선택합니다. **[!UICONTROL 구성된 API 저장]**&#x200B;을 클릭합니다.

   페이지에 구성에 대한 자세한 정보가 표시됩니다. 스마트 태그를 구성하려면 [!DNL Experience Manager]에 있는 클라우드 구성의 [!UICONTROL Assets 스마트 태그 지정 서비스 설정]에서 이 값을 복사하고 추가하려면 이 페이지를 열어 두십시오.

   ![개요 탭에서 통합에 제공된 정보를 검토할 수 있습니다.](assets/integration_details.png)


   *그림: Adobe Developer Console 통합 세부 정보*

### 스마트 컨텐츠 서비스 구성 {#configure-smart-content-service}

>[!CAUTION]
>
>이전에는 JWT 자격 증명으로 구성된 구성은 이제 Adobe Developer Console에서 더 이상 사용되지 않습니다. 2024년 6월 3일 이후에는 새 JWT 자격 증명을 만들 수 없습니다. 이러한 구성은 더 이상 만들거나 업데이트할 수 없지만 OAuth 구성으로 마이그레이션할 수 있습니다.
> [AEM용 IMS 통합 설정](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service)을 참조하세요.
>[온-프레미스 사용자를 위한 OAuth 구성 단계](#config-oauth-onprem)를 참조하세요.
> [OAuth 자격 증명에 대한 스마트 태그 문제 해결](#config-smart-tagging.md)을 참조하십시오.

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

### 온-프레미스 사용자를 위한 OAuth 구성 {#config-oauth-onprem}

#### 사전 요구 사항 {#prereqs-config-oauth-onprem}

인증 범위는 다음 사전 요구 사항을 포함하는 OAuth 문자열입니다.

* `ClientID`, `ClientSecretID` 및 `OrgID`을(를) 사용하여 [Developer Console](https://developer.adobe.com/console/user/servicesandapis)에서 새 OAuth 통합을 만듭니다.
* 이 경로 `/apps/system/config in crx/de`에 다음 파일을 추가하십시오.
   * `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`
   * `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`

#### 온-프레미스 사용자를 위한 OAuth 구성 {#steps-config-oauth-onprem}

1. `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`에서 아래 속성을 추가하거나 업데이트하십시오.

   * `auth.token.provider.authorization.grants="client_credentials"`
   * `auth.token.provider.orgId="<OrgID>"`
   * `auth.token.provider.default.claims=("\"iss\"\ :\ \"<OrgID>\"")`
   * `auth.token.provider.scope="read_pc.dma_smart_content,\ openid,\ AdobeID,\ additional_info.projectedProductContext"`
     `auth.token.validator.type="adobe-ims-similaritysearch"`
   * 새 OAuth 구성의 클라이언트 ID로 `auth.token.provider.client.id`을(를) 업데이트합니다.
   * `auth.access.token.request`을(를) `"https://ims-na1.adobelogin.com/ims/token/v3"`(으)로 업데이트
2. 파일 이름을 `com.adobe.granite.auth.oauth.accesstoken.provider-<randomnumber>.config`(으)로 바꾸십시오.
3. `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`에서 아래 단계를 수행합니다.
   * 새 OAuth 통합에서 클라이언트 암호로 auth.ims.client.secret 속성을 업데이트합니다.
   * 파일 이름을 `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl-<randomnumber>.config`(으)로 바꾸기
4. CRXDE와 같은 콘텐츠 저장소 개발 콘솔의 모든 변경 사항을 저장합니다.
5. `/system/console/configMgr`(으)로 이동하여 OSGi 구성을 `.<randomnumber>`에서 `-<randomnumber>`(으)로 바꿉니다.
6. `/system/console/configMgr`에서 `"Access Token provider name: adobe-ims-similaritysearch"`에 대한 이전 구성을 삭제합니다.
7. 콘솔을 다시 시작합니다.

### 구성 유효성 검사 {#validate-the-configuration}

구성을 완료한 후 JMX MBean을 사용하여 구성의 유효성을 검사할 수 있습니다. 유효성을 검사하려면 다음 단계를 수행합니다.

1. `https://[aem_server]:[port]`에서 [!DNL Experience Manager] 서버에 액세스합니다.

1. **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**(으)로 이동하여 OSGi 콘솔을 엽니다. **[!UICONTROL 기본] > [!UICONTROL JMX]**&#x200B;을(를) 클릭합니다.

1. `com.day.cq.dam.similaritysearch.internal.impl`를 클릭합니다. **[!UICONTROL SimilaritySearch 기타 작업]**&#x200B;을 엽니다.

1. `validateConfigs()`를 클릭합니다. **[!UICONTROL 구성 유효성 검사]** 대화 상자에서 **[!UICONTROL 호출]**&#x200B;을 클릭합니다.

유효성 검사 결과는 동일한 대화 상자에 표시됩니다.

### [!UICONTROL DAM 자산 업데이트] 워크플로우에서 스마트 태그 지정 사용(선택 사항) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. [!DNL Experience Manager]에서 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 모델]**(으)로 이동합니다.

1. **[!UICONTROL 워크플로우 모델]** 페이지에서 **[!UICONTROL DAM 자산 업데이트]** 워크플로우 모델을 선택합니다.

1. 도구 모음에서 **[!UICONTROL 편집]**&#x200B;을 클릭합니다.

1. 사이드 패널을 확장하여 단계를 표시합니다. DAM 워크플로우 섹션에서 사용할 수 있는 **[!UICONTROL 스마트 태그 자산]** 단계를 드래그하여 **[!UICONTROL 프로세스 썸네일]** 단계 이후에 배치합니다.

   ![DAM 자산 업데이트 워크플로우에서 프로세스 썸네일 단계 이후 스마트 태그 자산 단계 추가](assets/smart-tag-in-dam-update-asset-workflow.png)

   *그림: [!UICONTROL DAM 자산 업데이트] 워크플로우에서 프로세스 썸네일 단계 뒤에 스마트 태그 자산 단계를 추가하십시오.*

1. Open the step in edit mode. **[!UICONTROL 고급 설정]**&#x200B;에서 **[!UICONTROL 핸들러 고급]** 옵션을 선택해야 합니다.

   ![DAM 자산 업데이트 워크플로우를 구성하고 스마트 태그 단계 추가](assets/smart-tag-step-properties-workflow1.png)


   *그림: DAM 자산 업데이트 워크플로우를 구성하고 스마트 태그 단계 추가*

1. In the **[!UICONTROL Arguments]** tab, select **[!UICONTROL Ignore Errors]** if you want the workflow to complete even if the automatic tagging step fails.

   ![스마트 태그 단계를 추가하고 핸들러를 미리 선택하도록 DAM 자산 업데이트 워크플로우를 구성합니다](assets/smart-tag-step-properties-workflow2.png)


   *그림: 스마트 태그 단계를 추가하고 핸들러를 미리 선택하도록 DAM 자산 업데이트 워크플로우를 구성합니다*

   폴더에서 스마트 태그 지정 사용 여부와 관계없이 업로드될 때 자산에 태그를 지정하려면 **[!UICONTROL 스마트 태그 플래그 무시]**&#x200B;를 선택합니다.

   ![스마트 태그 단계를 추가하고 스마트 태그 플래그 무시를 선택하도록 DAM 자산 업데이트 워크플로우를 구성합니다](assets/smart-tag-step-properties-workflow3.png)


   *그림: DAM 자산 업데이트 워크플로우를 구성하여 스마트 태그 단계를 추가하고 스마트 태그 플래그 무시를 선택합니다.*

1. **[!UICONTROL 확인]**&#x200B;을 클릭하여 프로세스 단계를 닫은 다음 워크플로우를 저장합니다.

## 스마트 컨텐츠 서비스 교육 {#training-the-smart-content-service}

스마트 컨텐츠 서비스가 비즈니스 분류법을 인식하도록 하려면 비즈니스와 관련된 태그가 이미 포함된 자산 세트에서 실행합니다. 브랜드 이미지에 효과적으로 태그를 지정하려면 스마트 컨텐츠 서비스는 교육 이미지가 특정 지침을 준수해야 합니다. 교육 후 서비스는 유사한 에셋 세트에 동일한 분류법을 적용할 수 있습니다.

관련 태그를 적용하는 기능을 개선하기 위해 서비스를 여러 번 교육할 수 있습니다. 각 교육 주기 후에 태그 지정 워크플로우를 실행하고 자산에 적절하게 태그가 지정되었는지 확인합니다.

스마트 컨텐츠 서비스를 정기적으로 또는 요구 사항에 따라 교육할 수 있습니다.

>[!NOTE]
>
>교육 워크플로우는 폴더에서만 실행됩니다.

### 교육 지침 {#guidelines-for-training}

최상의 결과를 얻기 위해 교육 세트의 이미지는 다음 지침을 따릅니다.

**Quantity and size:** Minimum 30 images per tag. Minimum of 500 pixels on the longer side.

**일관성**: 특정 태그에 사용되는 이미지가 시각적으로 유사합니다.

예를 들어 이러한 모든 이미지는 시각적으로 유사하지 않으므로 `my-party`(교육용)으로 태그를 지정하는 것은 좋지 않습니다.

![교육에 대한 지침을 설명하는 그림 이미지](/help/assets/assets/do-not-localize/coherence.png)

**적용 범위**: 교육에 있는 이미지에 충분한 다양성을 사용하십시오. 아이디어는 Experience Manager이 올바른 것에 초점을 맞추는 방법을 배울 수 있도록 몇 가지 그러나 합리적으로 다양한 사례를 제공하는 것입니다. 시각적으로 다른 이미지에 동일한 태그를 적용하는 경우에는 각 종류의 예제를 5개 이상 포함하십시오.

예를 들어 태그 *모델-아래-포즈*&#x200B;의 경우 태그 지정 중에 유사한 이미지를 더 정확하게 식별하기 위해 서비스에 대해 아래 강조 표시된 이미지와 유사한 교육 이미지를 더 포함하십시오.

![교육에 대한 지침을 설명하는 그림 이미지](/help/assets/assets/do-not-localize/coverage_1.png)

**주의 산만함/방해**: 서비스는 주의 산만함이 적은 이미지(주요 주체가 있는 개체/사람과 같이 눈에 띄는 배경, 관련 없는 반주)에서 더 잘 훈련합니다.

예를 들어 태그 *캐주얼 신발*&#x200B;의 경우 두 번째 이미지는 좋은 교육 후보가 아닙니다.

![교육에 대한 지침을 설명하는 그림 이미지](/help/assets/assets/do-not-localize/distraction.png)

**Completeness:** If an image qualifies for more than one tag, add all applicable tags before including the image for training. 예를 들어 `raincoat` 및 `model-side-view`과(와) 같은 태그의 경우 교육을 위해 태그를 포함하기 전에 적격 에셋에 태그를 모두 추가하십시오.

![교육에 대한 지침을 설명하는 그림 이미지](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>태그에 대해 교육하고 다른 이미지에 적용하는 스마트 컨텐츠 서비스의 기능은 교육에 사용하는 이미지의 품질에 따라 다릅니다. Adobe 최상의 결과를 얻으려면 시각적으로 유사한 이미지를 사용하여 각 태그에 대한 서비스를 교육하는 것이 좋습니다.

### 정기 교육 {#periodic-training}

스마트 컨텐츠 서비스를 사용하여 폴더 내의 자산 및 관련 태그에 대해 정기적으로 교육할 수 있습니다. 자산 폴더의 [!UICONTROL 속성] 페이지를 열고 **[!UICONTROL 세부 정보]** 탭에서 **[!UICONTROL 스마트 태그 사용]**&#x200B;을 선택한 다음 변경 내용을 저장합니다.

![enable_smart_tags](assets/enable_smart_tags.png)

폴더에 대해 이 옵션을 선택하면 [!DNL Experience Manager]에서 자동으로 교육 워크플로를 실행하여 폴더 자산 및 해당 태그에 대한 스마트 컨텐츠 서비스를 교육합니다. 기본적으로 교육 워크플로우는 매주 토요일 오전 12시 30분에 실행됩니다.

### 온디맨드 교육 {#on-demand-training}

필요할 때마다 워크플로우 콘솔에서 스마트 컨텐츠 서비스를 교육할 수 있습니다.

1. [!DNL Experience Manager] 인터페이스에서 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 모델]**(으)로 이동합니다.
1. **[!UICONTROL 워크플로 모델]** 페이지에서 **[!UICONTROL 스마트 태그 교육]** 워크플로를 선택한 다음 도구 모음에서 **[!UICONTROL 워크플로 시작]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 워크플로 실행]** 대화 상자에서 서비스 교육을 위해 태그가 지정된 자산이 포함된 페이로드 폴더를 찾습니다.
1. 워크플로우의 제목을 지정하고 댓글을 추가합니다. 그런 다음 **[!UICONTROL 실행]**&#x200B;을 클릭합니다. 에셋 및 태그가 교육을 위해 제출됩니다.

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>폴더의 에셋이 교육에 대해 처리되면 수정된 에셋만 후속 교육 주기에서 처리됩니다.

### 교육 보고서 보기 {#viewing-training-reports}

스마트 컨텐츠 서비스가 교육 에셋 세트의 태그에 대해 교육되었는지 확인하려면 보고서 콘솔에서 교육 워크플로우 보고서를 검토하십시오.

1. [!DNL Experience Manager] 인터페이스에서 **[!UICONTROL 도구]** > **[!UICONTROL Assets]** > **[!UICONTROL 보고서]**(으)로 이동합니다.
1. **[!UICONTROL 자산 보고서]** 페이지에서 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.
1. **[!UICONTROL 스마트 태그 교육]** 보고서를 선택한 다음 도구 모음에서 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. Specify a title and description for the report. Under **[!UICONTROL Schedule Report]**, leave the **[!UICONTROL Now]** option selected. If you want to schedule the report for later, select **[!UICONTROL Later]** and specify a date and time. 그런 다음 도구 모음에서 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.
1. In the **[!UICONTROL Asset Reports]** page, select the report you generated. 보고서를 보려면 도구 모음에서 **[!UICONTROL 보기]**&#x200B;를 클릭하십시오.
1. 보고서의 세부 사항을 검토합니다.

   The report displays the training status for the tags you trained. The green color in the **[!UICONTROL Training Status]** column indicates that the Smart Content Service is trained for the tag. Yellow color indicates that the service is not completely trained for a particular tag. In this case, add more images with the particular tag and run the training workflow to train the service completely on the tag.

   이 보고서에 태그가 표시되지 않으면 이러한 태그에 대한 교육 워크플로우를 다시 실행하십시오.

1. 보고서를 다운로드하려면 목록에서 선택한 다음 도구 모음에서 **[!UICONTROL 다운로드]**&#x200B;를 클릭하십시오. 보고서는 Microsoft Excel 스프레드시트로 다운로드됩니다.

## 제한 사항 {#limitations}

* 향상된 스마트 태그는 이미지 및 해당 태그의 학습 모델을 기반으로 합니다. 이러한 모델이 태그를 식별하는 데 항상 완벽하지는 않습니다. 현재 버전의 스마트 컨텐츠 서비스에는 다음과 같은 제한 사항이 있습니다.

   * 이미지의 미묘한 차이를 인식할 수 없음. 예를 들어, 슬림과 일반 맞춤 셔츠.
   * 이미지의 작은 패턴/부분을 기반으로 태그를 식별할 수 없음. 예를 들어 T 셔츠의 로고.
   * [!DNL Experience Manager]이(가) 지원되는 로케일에서 태깅이 지원됩니다.

* 스마트 태그(일반 또는 고급)로 자산을 검색하려면 [!DNL Assets] Omnisearch(전체 텍스트 검색)를 사용하십시오. 스마트 태그에 대한 별도의 검색 조건자는 없습니다.

>[!MORELIKETHIS]
>
>* [개요 및 스마트 태그 교육 방법](enhanced-smart-tags.md)
>* [OAuth 자격 증명에 대한 스마트 태그 문제 해결](config-oauth.md)
>* 스마트 태그에 대한 [비디오 튜토리얼](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)
