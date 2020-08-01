---
title: 스마트 콘텐츠 서비스를 사용하여 자산 태그 지정을 구성합니다.
description: 스마트 콘텐츠 서비스를 사용하여 스마트 태그 지정 및 고급 스마트 태그 [!DNL Adobe Experience Manager]기능을 구성하는 방법을 알아봅니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 35%

---


# 스마트 콘텐츠 서비스를 사용하여 자산 태그 지정 구성 {#configure-asset-tagging-using-the-smart-content-service}

Adobe 개발자 콘솔 [!DNL Adobe Experience Manager] 을 사용하여 스마트 콘텐츠 서비스와 통합할 수 있습니다. 이 구성을 사용하여 내에서 스마트 콘텐츠 서비스에 액세스합니다 [!DNL Experience Manager].

이 문서에서는 스마트 콘텐츠 서비스를 구성하는 데 필요한 다음 주요 작업에 대해 자세히 설명합니다. At the back end, the [!DNL Experience Manager] server authenticates your service credentials with the Adobe Developer Console gateway before forwarding your request to the Smart Content Service.

1. Create a Smart Content Service configuration in [!DNL Experience Manager] to generate a public key. OAuth 통합을 위한 [공개 인증서를 받습니다](#obtain-public-certificate).
1. [Adobe 개발자 콘솔에서 통합을 만들고](#create-adobe-i-o-integration) 생성된 공개 키를 업로드합니다.
1. [Adobe 개발자 콘솔의 API 키 및 기타 자격 증명을 사용하여 배포를](#configure-smart-content-service) 구성합니다.
1. [구성을 테스트합니다](#validate-the-configuration).
1. 자산 업로드 시 자동 태그 지정 [을 활성화할 수도 있습니다](#enable-smart-tagging-in-the-update-asset-workflow-optional).

## 전제 조건 {#prerequisites}

스마트 콘텐츠 서비스를 사용하려면 먼저 Adobe 개발자 콘솔에서 통합을 만들려면 다음을 확인하십시오.

* 조직에 대한 관리자 권한이 부여된 Adobe ID 계정이 있습니다.
* 조직에서 스마트 콘텐츠 서비스 서비스를 사용할 수 있습니다.

<!-- TBD: This link will update soon after the new articles goes live on docs.adobe.com. Change it when new URL is available.
-->

고급 스마트 태그를 활성화하려면 위의 [Experience Manager 서비스 팩도 설치합니다](https://helpx.adobe.com/kr/experience-manager/aem-releases-updates.html).

## 공개 인증서 받기 {#obtain-public-certificate}

공개 인증서를 사용하면 Adobe 개발자 콘솔에서 프로필을 인증할 수 있습니다.

1. 사용자 [!DNL Experience Manager] 인터페이스에서 **[!UICONTROL 도구]** > Cloud Service **** > **[!UICONTROL 기존 Cloud Service에]**&#x200B;액세스합니다.

1. Cloud Service 페이지에서 자산 스마트 태그 아래의 **[!UICONTROL 지금]** 구성을 **[!UICONTROL 클릭합니다]**.
1. 구성 **[!UICONTROL 만들기]** 대화 상자에서 스마트 태그 구성의 제목과 이름을 지정합니다. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.
1. AEM **[!UICONTROL 스마트 콘텐츠 서비스]** 대화 상자에서 다음 값을 사용합니다.

   **[!UICONTROL 서비스 URL]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 인증 서버]**: `https://ims-na1.adobelogin.com`

   다른 필드는 비워 둡니다(나중에 제공). **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

   ![컨텐츠 서비스 URL을 제공하는 Experience Manager 스마트 콘텐츠 서비스 대화 상자](assets/aem_scs.png)

   >[!NOTE]
   >
   >서비스 URL로 제공된 URL은 [!UICONTROL 브라우저를 통해] 액세스할 수 없으며 404 오류를 생성합니다. 구성은 [!UICONTROL 서비스 URL] 매개 변수와 동일한 값으로 작동합니다. 전체 서비스 상태 및 유지 관리 일정은 https://status.adobe.com을 [참조하십시오](https://status.adobe.com).

1. OAuth **[!UICONTROL 통합용]**&#x200B;공용 인증서 다운로드를 클릭하고 공용 인증서 파일을 다운로드합니다 `AEM-SmartTags.crt`.

   ![스마트 태깅 서비스를 위해 만들어진 설정 표현](assets/smart-tags-download-public-cert.png)

### Reconfigure when a certificate expires {#certrenew}

인증서가 만료되면 더 이상 신뢰되지 않습니다. 만료된 인증서는 갱신할 수 없습니다. 새 인증서를 추가하려면 다음 단계를 따르십시오.

1. 관리자로 [!DNL Experience Manager] 배포에 로그인합니다. **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 사용자]**&#x200B;를 클릭합니다.

1. **[!UICONTROL dam-update-service]** 사용자를 찾아 클릭합니다. **[!UICONTROL 키 저장소]** 탭을 클릭합니다.
1. 만료된 인증서로 기존의 **[!UICONTROL 유사 검색]** 키 저장소를 삭제합니다. **[!UICONTROL 저장 후 닫기]**&#x200B;를 클릭합니다.

   ![새 보안 인증서를 추가하려면 Keystore에서 기존 유사 검색검색 항목을 삭제합니다.](assets/smarttags_delete_similaritysearch_keystore.png)

   *그림: 새 보안 인증서를 추가하려면 키 저장소에서 기존`similaritysearch`항목을 삭제합니다.*

1. 도구 **[!UICONTROL > Cloud Service]** **** > **[!UICONTROL 기존 Cloud Service]**&#x200B;로이동합니다. 자산 **[!UICONTROL 스마트 태그]** > 구성 **[!UICONTROL 표시]** > 사용 가능한 구성 **[!UICONTROL 을 클릭합니다]**. 필요한 구성을 클릭합니다.

1. To download a public certificate, click **[!UICONTROL Download Public Certificate for OAuth Integration]**.
1. 통합 [페이지에서 https://console.adobe.io](https://console.adobe.io) 에 액세스하여 기존 Smart Content Services로 **[!UICONTROL 이동합니다]** . 새 인증서를 업로드합니다. For more information, see the instructions in [Create Adobe Developer Console integration](#create-adobe-i-o-integration).

## Adobe 개발자 콘솔 통합 만들기 {#create-adobe-i-o-integration}

스마트 콘텐츠 서비스 API를 사용하려면 Adobe 개발자 콘솔에서 통합을 만들어 API 키, 기술 계정 ID, 조직 ID 및 클라이언트 암호를 생성합니다.

1. 브라우저에서 [https://console.adobe.io](https://console.adobe.io/)에 액세스합니다. 적절한 계정을 선택하고 관련 조직 역할이 시스템 관리자인지 확인합니다.
1. 원하는 이름으로 프로젝트를 만듭니다. **[!UICONTROL API 추가]**&#x200B;를 클릭합니다.
1. **[!UICONTROL API 추가]** 페이지에서 **[!UICONTROL Experience Cloud]**&#x200B;를 선택하고 **[!UICONTROL 스마트 컨텐츠]**&#x200B;를 선택합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 공개 키 업로드]**&#x200B;를 선택합니다. [!DNL Experience Manager]에서 다운로드한 인증서 파일을 제공합니다. [!UICONTROL 공개 키가 업로드되었습니다] 메시지가 표시됩니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. [!UICONTROL 새 서비스 계정(JWT) 자격 증명 만들기] 페이지에는 방금 구성된 서비스 계정에 대한 공개 키가 표시됩니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 제품 프로필 선택]** 페이지에서 **[!UICONTROL 스마트 컨텐츠 서비스]**&#x200B;를 선택합니다. **[!UICONTROL 구성된 API 저장]**&#x200B;을 클릭합니다. 페이지에 구성에 대한 자세한 정보가 표시됩니다. [!DNL Experience Manager]에서 스마트 태그를 추가로 구성할 때 Experience Manager에서 이러한 값을 복사하고 추가하려면 이 페이지를 열어 둡니다.

   ![개요 탭에서 통합에 제공된 정보를 검토할 수 있습니다.](assets/integration_details.png)

## 스마트 콘텐츠 서비스 구성 {#configure-smart-content-service}

통합을 구성하려면 Adobe 개발자 콘솔 통합에서 기술 계정 ID, 조직 ID, 클라이언트 암호, 인증 서버 및 API 키 필드의 값을 사용하십시오. 스마트 태그 클라우드 구성을 만들면 배포에서 API 요청을 인증할 수 [!DNL Experience Manager] 있습니다.

1. 에서 [!DNL Experience Manager]열려 있는 기존 Cloud ServiceConsole을 **[!UICONTROL 탐색하는]** [도구] > **[!UICONTROL Cloud Service]** > **[!UICONTROL 레거시 Cloud Service]**  으로 이동합니다.
1. 자산 **[!UICONTROL 스마트 태그]**&#x200B;아래에서 위에서 만든 구성을 엽니다. 서비스 설정 페이지에서 편집을 **[!UICONTROL 클릭합니다]**.
1. [ **[!UICONTROL AEM 스마트 콘텐츠 서비스]** ] 대화 상자에서 **[!UICONTROL 서비스 URL]** 및 **[!UICONTROL 인증 서버]** 필드에 대해 미리 채워진 값을사용합니다.
1. 필드 API 키, **[!UICONTROL 기술 계정]** ID **[!UICONTROL ,]**&#x200B;조직 ID **[!UICONTROL 및 클라이언트 암호]**&#x200B;의 경우 위에서 생성된 값을 ****&#x200B;사용합니다.

## 구성 유효성 확인 {#validate-the-configuration}

구성을 완료한 후 JMX MBean을 사용하여 구성을 확인할 수 있습니다. 유효성을 확인하려면 다음 단계를 따르십시오.

1. 에서 [!DNL Experience Manager] 서버에 액세스합니다 `https://[aem_server]:[port]`.
1. 도구 > **[!UICONTROL 작업]** **** > **[!UICONTROL 웹 콘솔]** 로 이동하여 OSGi 콘솔을엽니다. 기본 **[!UICONTROL > JMX]를[!UICONTROL 클릭합니다]**.
1. 클릭 `com.day.cq.dam.similaritysearch.internal.impl`. 유사성 **[!UICONTROL 검색 기타 작업을 엽니다]**.
1. 클릭 `validateConfigs()`. 구성 유효성 **[!UICONTROL 확인]** 대화 상자에서 호출 **[!UICONTROL 을 클릭합니다]**. 유효성 검사 결과가 동일한 대화 상자에 표시됩니다.

## DAM 자산 [!UICONTROL 업데이트 워크플로우에서 스마트 태그] 설정(선택 사항) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. In [!DNL Experience Manager], go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. **[!UICONTROL 워크플로우 모델]** 페이지에서 **[!UICONTROL DAM 자산 업데이트]** 워크플로우 모델을 선택합니다.
1. 도구 모음에서 **[!UICONTROL 편집]**&#x200B;을 클릭합니다.
1. 사이드 패널을 확장하여 단계를 표시합니다. DAM 워크플로우 섹션에서 사용할 수 있는 **[!UICONTROL 스마트 태그 자산]** 단계를 드래그하여 **[!UICONTROL 프로세스 썸네일]** 단계 이후에 배치합니다.

   ![DAM 자산 업데이트 워크플로우에서 프로세스 썸네일 단계 이후 스마트 태그 자산 단계 추가](assets/smart-tag-in-dam-update-asset-workflow.png)

   *그림: DAM 자산 업데이트 워크플로우에서 프로세스 썸네일 단계 이후에 스마트 태그 자산 단계를 추가합니다.*

1. 편집 모드에서 단계를 엽니다. **[!UICONTROL 고급 설정]**&#x200B;에서 **[!UICONTROL 핸들러 고급]** 옵션을 선택해야 합니다.

   ![DAM 자산 업데이트 워크플로우 구성 및 스마트 태그 단계 추가](assets/smart-tag-step-properties-workflow1.png)

1. 자동 태그 지정 단계 **[!UICONTROL 에]** 실패하는 경우에도 워크플로우를 완료하려면 인수 탭에서 오류 **** 무시를 선택합니다.

   폴더에서 스마트 태그 지정 사용 여부와 관계없이 업로드될 때 자산에 태그를 지정하려면 **[!UICONTROL 스마트 태그 플래그 무시]**&#x200B;를 선택합니다.

   ![스마트 태그 단계를 추가하고 스마트 태그 플래그 무시를 선택하도록 DAM 자산 업데이트 워크플로우 구성](assets/smart-tag-step-properties-workflow2.png)

1. **[!UICONTROL 확인]**&#x200B;을 클릭하여 프로세스 단계를 닫은 다음 워크플로우를 저장합니다.

>[!MORELIKETHIS]
>
>* [스마트 태그 관리](managing-smart-tags.md)
>* [스마트 태그 교육 개요 및 방법](enhanced-smart-tags.md)
>* [스마트 콘텐츠 서비스 트레이닝을 위한 지침 및 규칙](smart-tags-training-guidelines.md)
>* [스마트 태그 구성 방법에 대한 비디오 자습서](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)

