---
title: 스마트 컨텐츠 서비스를 사용하여 자산 태그 지정 구성
description: 에서 스마트 태그 지정 및 향상된 스마트 태그 지정을 구성하는 방법에 대해 알아봅니다 [!DNL Adobe Experience Manager](스마트 컨텐츠 서비스 사용)
contentOwner: AG
role: Admin
feature: Tagging,Smart Tags
exl-id: 9f68804f-ba15-4f83-ab1b-c249424b1396
source-git-commit: 83e9ab570fac686fd53c9c2594cbfb2c05a89a0c
workflow-type: tm+mt
source-wordcount: '2262'
ht-degree: 25%

---

# 준비 [!DNL Assets] 스마트 태그 지정용 {#configure-asset-tagging-using-the-smart-content-service}

스마트 컨텐츠 서비스를 사용하여 자산에 태그를 지정하려면 다음을 통합하십시오 [!DNL Experience Manager Assets] 의 스마트 서비스를 활용하는 Adobe Developer 콘솔 포함 [!DNL Adobe Sensei]. 구성이 완료되면 몇 개의 이미지와 태그를 사용하여 서비스를 교육합니다.

>[!NOTE]
>
>* 스마트 컨텐츠 서비스를 더 이상 새 사용자에게 제공할 수 없습니다. [!DNL Experience Manager Assets] On-Premise 고객 이미 이 기능이 활성화되어 있는 기존 온-프레미스 고객은 스마트 컨텐츠 서비스를 계속 사용할 수 있습니다.
>* 스마트 컨텐츠 서비스는 기존 서비스에 사용할 수 있습니다 [!DNL Experience Manager Assets] 이 기능이 이미 활성화되어 있는 Managed Services 고객.
>* 신규 [!DNL Experience Manager Assets] Managed Services 고객은 이 문서에 나열된 지침에 따라 스마트 컨텐츠 서비스를 설정할 수 있습니다.


스마트 컨텐츠 서비스를 사용하기 전에 다음을 확인하십시오.

* [Adobe 개발자 콘솔과 통합](#integrate-adobe-io).
* [스마트 컨텐츠 서비스 교육](#training-the-smart-content-service).

* 최신 버전 설치 [[!DNL Experience Manager] 서비스 팩](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html).

## Adobe 개발자 콘솔과 통합 {#integrate-adobe-io}

Adobe Developer 콘솔과 통합하면 [!DNL Experience Manager] 서버는 요청을 스마트 컨텐츠 서비스로 전달하기 전에 Adobe Developer 콘솔 게이트웨이로 서비스 자격 증명을 인증합니다. 통합하려면 조직에 대한 관리자 권한이 있는 Adobe ID 계정과, 조직에 대해 구매 및 활성화된 Smart Content Service 라이선스가 필요합니다.

스마트 컨텐츠 서비스를 구성하려면 다음 최상위 단계를 수행합니다.

1. 공개 키를 생성하려면 [스마트 컨텐츠 서비스 만들기](#obtain-public-certificate) 에서 구성 [!DNL Experience Manager]. OAuth 통합을 위한 [공개 인증서를 받습니다](#obtain-public-certificate).

1. [Adobe 개발자 콘솔에서 통합을 만들고](#create-adobe-i-o-integration) 생성된 공개 키를 업로드합니다.

1. [배포 구성](#configure-smart-content-service) Adobe Developer 콘솔에서 API 키 및 기타 자격 증명 사용.

1. [구성을 테스트합니다](#validate-the-configuration).

1. 선택적으로, [자산 업로드 시 자동 태그 지정 활성화](#enable-smart-tagging-in-the-update-asset-workflow-optional).

### 스마트 컨텐츠 서비스 구성을 만들어 공개 인증서 받기 {#obtain-public-certificate}

공개 인증서를 사용하면 Adobe 개발자 콘솔에서 프로필을 인증할 수 있습니다.

1. 다음에서 [!DNL Experience Manager] 사용자 인터페이스, 액세스 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 이전 Cloud Services]**.

1. Cloud Services 페이지에서 **[!UICONTROL 지금 구성]** 아래에 **[!UICONTROL 에셋 스마트 태그]**.

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

   ![컨텐츠 서비스 URL을 제공하는 스마트 컨텐츠 서비스 Experience Manager 대화 상자](assets/aem_scs.png)


   *그림: 콘텐츠 서비스 URL을 제공하는 스마트 콘텐츠 서비스 대화 상자*

   >[!NOTE]
   >
   >다음으로 제공된 URL [!UICONTROL 서비스 URL] 는 브라우저를 통해 액세스할 수 없으며 404 오류를 생성합니다. 구성이 의 동일한 값으로 정상 작동합니다. [!UICONTROL 서비스 URL] 매개 변수. 전체 서비스 상태 및 유지 관리 일정은 다음을 참조하십시오. [https://status.adobe.com](https://status.adobe.com).

1. 클릭 **[!UICONTROL OAuth 통합을 위한 공개 인증서 다운로드]**&#x200B;및 공개 인증서 파일 다운로드 `AEM-SmartTags.crt`.

   ![스마트 태그 지정 서비스를 위해 만들어진 설정의 표현입니다](assets/smart-tags-download-public-cert.png)


   *그림: 스마트 태그 지정 서비스 설정*

#### 인증서가 만료되면 다시 구성 {#certrenew}

인증서가 만료되면 더 이상 신뢰할 수 없습니다. 만료된 인증서는 갱신할 수 없습니다. 인증서를 추가하려면 다음 단계를 따르십시오.

1. 관리자로 [!DNL Experience Manager] 배포에 로그인합니다. **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 사용자]**&#x200B;를 클릭합니다.

1. **[!UICONTROL dam-update-service]** 사용자를 찾아 클릭합니다. 클릭 **[!UICONTROL 키 저장소]** 탭.

1. 만료된 인증서로 기존의 **[!UICONTROL 유사 검색]** 키 저장소를 삭제합니다. **[!UICONTROL 저장 후 닫기]**&#x200B;를 클릭합니다.

   ![보안 인증서를 추가하려면 키 저장소에서 기존 유사성 검색 항목을 삭제하십시오.](assets/smarttags_delete_similaritysearch_keystore.png)


   *그림: 기존 항목 삭제 `similaritysearch` 키 저장소에 보안 인증서를 추가하는 항목을 추가했습니다.*

1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Legacy Cloud Services]**. Click **[!UICONTROL Asset Smart Tags]** > **[!UICONTROL Show Configuration]** > **[!UICONTROL Available Configurations]**. Click the required configuration.

1. 공개 인증서를 다운로드하려면 **[!UICONTROL OAuth 통합을 위한 공개 인증서 다운로드]**.

1. 액세스 [https://console.adobe.io](https://console.adobe.io) 및 의 기존 스마트 컨텐츠 서비스로 이동합니다. **[!UICONTROL 통합]** 페이지를 가리키도록 업데이트하는 중입니다. 새 인증서를 업로드합니다. 자세한 내용은 의 지침을 참조하십시오 [Adobe Developer 콘솔 통합 만들기](#create-adobe-i-o-integration).

### Adobe Developer 콘솔 통합 만들기 {#create-adobe-i-o-integration}

스마트 컨텐츠 서비스 API를 사용하려면 Adobe Developer 콘솔에서 통합을 만들어 다음을 얻으십시오 [!UICONTROL API 키] (생성된 위치 [!UICONTROL 클라이언트 ID] Adobe Developer 콘솔 통합 필드 [!UICONTROL 기술 계정 ID], [!UICONTROL 조직 ID], 및 [!UICONTROL 클라이언트 암호] 대상 [!UICONTROL 자산 스마트 태그 지정 서비스 설정] 의 클라우드 구성 [!DNL Experience Manager].

1. 브라우저에서 [https://console.adobe.io](https://console.adobe.io/)에 액세스합니다. 적절한 계정을 선택하고 관련 조직 역할이 시스템 관리자인지 확인합니다.

1. 원하는 이름으로 프로젝트를 만듭니다. **[!UICONTROL API 추가]**&#x200B;를 클릭합니다.

1. **[!UICONTROL API 추가]** 페이지에서 **[!UICONTROL Experience Cloud]**&#x200B;를 선택하고 **[!UICONTROL 스마트 컨텐츠]**&#x200B;를 선택합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. **[!UICONTROL 공개 키 업로드]**&#x200B;를 선택합니다. [!DNL Experience Manager]에서 다운로드한 인증서 파일을 제공합니다. [!UICONTROL 공개 키가 업로드되었습니다] 메시지가 표시됩니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   [!UICONTROL 새 서비스 계정(JWT) 자격 증명 만들기] 페이지에 서비스 계정에 대한 공개 키가 표시됩니다.

1. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. **[!UICONTROL 제품 프로필 선택]** 페이지에서 **[!UICONTROL 스마트 컨텐츠 서비스]**&#x200B;를 선택합니다. **[!UICONTROL 구성된 API 저장]**&#x200B;을 클릭합니다.

   페이지에 구성에 대한 자세한 정보가 표시됩니다. 이 값을 복사하고 추가하려면 이 페이지를 열어 두십시오. [!UICONTROL 자산 스마트 태그 지정 서비스 설정] 의 클라우드 구성 [!DNL Experience Manager] 스마트 태그를 구성합니다.

   ![개요 탭에서 통합에 제공된 정보를 검토할 수 있습니다.](assets/integration_details.png)


   *그림: Adobe Developer 콘솔의 통합 세부 정보*

### 스마트 컨텐츠 서비스 구성 {#configure-smart-content-service}

통합을 구성하려면 다음 값을 사용합니다. [!UICONTROL 기술 계정 ID], [!UICONTROL 조직 ID], [!UICONTROL 클라이언트 암호], 및 [!UICONTROL 클라이언트 ID] Adobe Developer 콘솔 통합의 필드입니다. 스마트 태그 클라우드 구성을 만들면 [!DNL Experience Manager] 배포.

1. 위치 [!DNL Experience Manager], 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL 이전 Cloud Services]** 을(를) 열려면 [!UICONTROL Cloud Services] 콘솔.

1. 아래 **[!UICONTROL 에셋 스마트 태그]**&#x200B;위에서 만든 구성을 엽니다. 서비스 설정 페이지에서 **[!UICONTROL 편집]**.

1. In the **[!UICONTROL AEM Smart Content Service]** dialog, use the pre-populated values for the **[!UICONTROL Service URL]** and **[!UICONTROL Authorization Server]** fields.

1. 필드용 [!UICONTROL Api 키], [!UICONTROL 기술 계정 ID], [!UICONTROL 조직 ID], 및 [!UICONTROL 클라이언트 암호]에서 생성된 다음 값을 복사하여 사용합니다. [Adobe Developer 콘솔 통합](#create-adobe-i-o-integration).

   | [!UICONTROL 자산 스마트 태깅 서비스 설정] | [!DNL Adobe Developer Console] 통합 필드 |
   |--- |--- |
   | [!UICONTROL Api 키] | [!UICONTROL 클라이언트 ID] |
   | [!UICONTROL 기술 계정 ID] | [!UICONTROL 기술 계정 ID] |
   | [!UICONTROL 조직 ID] | [!UICONTROL 조직 ID] |
   | [!UICONTROL 클라이언트 암호] | [!UICONTROL 클라이언트 암호] |

### 구성 유효성 확인 {#validate-the-configuration}

구성을 완료한 후 JMX MBean을 사용하여 구성의 유효성을 검사할 수 있습니다. 유효성을 검사하려면 다음 단계를 수행합니다.

1. 액세스 권한 [!DNL Experience Manager] 서버 위치 `https://[aem_server]:[port]`.

1. 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]** OSGi 콘솔을 엽니다. 클릭 **[!UICONTROL 기본] > [!UICONTROL JMX]**.

1. 클릭 `com.day.cq.dam.similaritysearch.internal.impl`. 열림 **[!UICONTROL 유사성기타 작업 검색]**.

1. 클릭 `validateConfigs()`. 다음에서 **[!UICONTROL 구성 유효성 검사]** 대화 상자, 클릭 **[!UICONTROL 호출]**.

유효성 검사 결과는 동일한 대화 상자에 표시됩니다.

### 에서 스마트 태그 지정 활성화 [!UICONTROL DAM 자산 업데이트] 워크플로(선택 사항) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. 위치 [!DNL Experience Manager]로 이동합니다. **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 모델]**.

1. **[!UICONTROL 워크플로우 모델]** 페이지에서 **[!UICONTROL DAM 자산 업데이트]** 워크플로우 모델을 선택합니다.

1. 도구 모음에서 **[!UICONTROL 편집]**&#x200B;을 클릭합니다.

1. 사이드 패널을 확장하여 단계를 표시합니다. DAM 워크플로우 섹션에서 사용할 수 있는 **[!UICONTROL 스마트 태그 자산]** 단계를 드래그하여 **[!UICONTROL 프로세스 썸네일]** 단계 이후에 배치합니다.

   ![DAM 자산 업데이트 워크플로우에서 프로세스 썸네일 단계 이후 스마트 태그 자산 단계 추가](assets/smart-tag-in-dam-update-asset-workflow.png)

   *그림: DAM 자산 업데이트 워크플로우에서 프로세스 썸네일 단계 이후에 스마트 태그 자산 단계를 추가합니다.*

1. Open the step in edit mode. **[!UICONTROL 고급 설정]**&#x200B;에서 **[!UICONTROL 핸들러 고급]** 옵션을 선택해야 합니다.

   ![DAM 자산 업데이트 워크플로우 구성 및 스마트 태그 단계 추가](assets/smart-tag-step-properties-workflow1.png)


   *그림: DAM 자산 업데이트 워크플로우 구성 및 스마트 태그 단계 추가*

1. In the **[!UICONTROL Arguments]** tab, select **[!UICONTROL Ignore Errors]** if you want the workflow to complete even if the automatic tagging step fails.

   ![스마트 태그 단계를 추가하고 핸들러를 미리 선택하도록 DAM 자산 업데이트 워크플로우 구성](assets/smart-tag-step-properties-workflow2.png)


   *그림: 스마트 태그 단계를 추가하고 핸들러를 미리 선택하도록 DAM 자산 업데이트 워크플로우 구성*

   폴더에서 스마트 태그 지정 사용 여부와 관계없이 업로드될 때 자산에 태그를 지정하려면 **[!UICONTROL 스마트 태그 플래그 무시]**&#x200B;를 선택합니다.

   ![스마트 태그 단계를 추가하고 스마트 태그 플래그 무시를 선택하도록 DAM 자산 업데이트 워크플로우 구성](assets/smart-tag-step-properties-workflow3.png)


   *그림: 스마트 태그 단계를 추가하도록 DAM 자산 업데이트 워크플로우를 구성하고 스마트 태그 플래그 무시 를 선택합니다.*

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

예를 들어 이러한 모든 이미지에 태그를 지정하는 것은 좋지 않습니다. `my-party` (훈련용) 시각적으로 유사하지 않기 때문입니다.

![교육 지침을 설명하는 예제 이미지](/help/assets/assets/do-not-localize/coherence.png)

**적용 범위**: 교육에서 이미지의 다양한 요소를 사용할 수 있습니다. 아이디어는 Experience Manager이 올바른 것에 초점을 맞추는 방법을 배울 수 있도록 몇 가지 그러나 합리적으로 다양한 사례를 제공하는 것입니다. 시각적으로 다른 이미지에 동일한 태그를 적용하는 경우에는 각 종류의 예제를 5개 이상 포함하십시오.

(예: 태그) *모델 다운 포즈*&#x200B;에는 태깅 중에 유사한 이미지를 더 정확하게 식별할 수 있도록 아래 강조 표시된 이미지와 유사한 교육 이미지가 더 포함됩니다.

![교육 지침을 설명하는 예제 이미지](/help/assets/assets/do-not-localize/coverage_1.png)

**산만/폐쇄**: 이 서비스는 산만함이 적은 이미지(두드러진 배경, 주요 주체가 있는 오브젝트/사람과 같은 관련 없는 반주)에 대해 더 나은 교육을 제공합니다.

(예: 태그) *캐주얼 신발*, 두 번째 이미지는 좋은 교육 후보가 아닙니다.

![교육 지침을 설명하는 예제 이미지](/help/assets/assets/do-not-localize/distraction.png)

**Completeness:** If an image qualifies for more than one tag, add all applicable tags before including the image for training. For example, for tags, such as `raincoat` and `model-side-view`, add both the tags on the eligible asset before including it for training.

![교육 지침을 설명하는 예제 이미지](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>태그에 대해 교육하고 다른 이미지에 적용하는 스마트 컨텐츠 서비스의 기능은 교육에 사용하는 이미지의 품질에 따라 다릅니다. Adobe 최상의 결과를 얻으려면 시각적으로 유사한 이미지를 사용하여 각 태그에 대한 서비스를 교육하는 것이 좋습니다.

### 정기 교육 {#periodic-training}

스마트 컨텐츠 서비스를 사용하여 폴더 내의 자산 및 관련 태그에 대해 정기적으로 교육할 수 있습니다. 를 엽니다. [!UICONTROL 속성] 에셋 폴더의 페이지에서 **[!UICONTROL 스마트 태그 활성화]** 다음 아래에 **[!UICONTROL 세부 사항]** 을 탭하고 변경 내용을 저장합니다.

![enable_smart_tag](assets/enable_smart_tags.png)

폴더에 대해 이 옵션을 선택하면 [!DNL Experience Manager] 폴더 자산 및 해당 태그에 대한 스마트 컨텐츠 서비스를 교육하기 위해 교육 워크플로를 자동으로 실행합니다. 기본적으로 교육 워크플로우는 매주 토요일 오전 12시 30분에 실행됩니다.

### 온디맨드 교육 {#on-demand-training}

필요할 때마다 워크플로우 콘솔에서 스마트 컨텐츠 서비스를 교육할 수 있습니다.

1. 위치 [!DNL Experience Manager] 인터페이스, 이동 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 모델]**.
1. 다음에서 **[!UICONTROL 워크플로 모델]** 페이지에서 **[!UICONTROL 스마트 태그 교육]** 워크플로우를 클릭한 다음 **[!UICONTROL 워크플로우 시작]** 을 클릭합니다.
1. 다음에서 **[!UICONTROL 워크플로우 실행]** 대화 상자에서 서비스 교육을 위해 태그가 지정된 에셋이 포함된 페이로드 폴더를 찾습니다.
1. 워크플로우의 제목을 지정하고 댓글을 추가합니다. 그런 다음 을 클릭합니다. **[!UICONTROL 실행]**. 에셋 및 태그가 교육을 위해 제출됩니다.

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>폴더의 에셋이 교육에 대해 처리되면 수정된 에셋만 후속 교육 주기에서 처리됩니다.

### 교육 보고서 보기 {#viewing-training-reports}

스마트 컨텐츠 서비스가 교육 에셋 세트의 태그에 대해 교육되었는지 확인하려면 보고서 콘솔에서 교육 워크플로우 보고서를 검토하십시오.

1. 위치 [!DNL Experience Manager] 인터페이스, 이동 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL 보고서]**.
1. 다음에서 **[!UICONTROL 자산 보고서]** 페이지, 클릭 **[!UICONTROL 만들기]**.
1. 다음 항목 선택 **[!UICONTROL 스마트 태그 교육]** 보고한 다음 **[!UICONTROL 다음]** 을 클릭합니다.
1. Specify a title and description for the report. Under **[!UICONTROL Schedule Report]**, leave the **[!UICONTROL Now]** option selected. If you want to schedule the report for later, select **[!UICONTROL Later]** and specify a date and time. 그런 다음 을 클릭합니다. **[!UICONTROL 만들기]** 을 클릭합니다.
1. In the **[!UICONTROL Asset Reports]** page, select the report you generated. 보고서를 보려면 **[!UICONTROL 보기]** 을 클릭합니다.
1. 보고서의 세부 사항을 검토합니다.

   The report displays the training status for the tags you trained. The green color in the **[!UICONTROL Training Status]** column indicates that the Smart Content Service is trained for the tag. Yellow color indicates that the service is not completely trained for a particular tag. In this case, add more images with the particular tag and run the training workflow to train the service completely on the tag.

   이 보고서에 태그가 표시되지 않으면 이러한 태그에 대한 교육 워크플로우를 다시 실행하십시오.

1. 보고서를 다운로드하려면 목록에서 해당 보고서를 선택하고 **[!UICONTROL 다운로드]** 을 클릭합니다. 보고서는 Microsoft Excel 스프레드시트로 다운로드됩니다.

## 제한 사항 {#limitations}

* 향상된 스마트 태그는 이미지 및 해당 태그의 학습 모델을 기반으로 합니다. 이러한 모델이 태그를 식별하는 데 항상 완벽하지는 않습니다. 현재 버전의 스마트 컨텐츠 서비스에는 다음과 같은 제한 사항이 있습니다.

   * 이미지의 미묘한 차이를 인식할 수 없음. 예를 들어, 슬림과 일반 맞춤 셔츠.
   * 이미지의 작은 패턴/부분을 기반으로 태그를 식별할 수 없음. 예를 들어 T 셔츠의 로고.
   * 태깅은 [!DNL Experience Manager] 는에서 지원됩니다. 언어 목록은 다음을 참조하십시오 [스마트 컨텐츠 서비스 릴리스 노트](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html).

* 스마트 태그(일반 또는 고급)로 자산을 검색하려면 [!DNL Assets] Omnisearch(전체 텍스트 검색). 스마트 태그에 대한 별도의 검색 조건자는 없습니다.

>[!MORELIKETHIS]
>
>* [스마트 태그 개요 및 교육 방법](enhanced-smart-tags.md)
>* [스마트 태그에 대한 비디오 튜토리얼](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)

