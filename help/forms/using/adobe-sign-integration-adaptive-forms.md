---
title: Adobe Sign과 AEM Forms 통합
description: AEM 적응형 Forms에 대한 Adobe Sign을 구성하는 방법에 대해 알아봅니다. Adobe Sign은 워크플로우를 개선하고 법률, 판매, 급여, 인적 자원 관리 등의 다양한 영역에 대한 문서를 처리합니다.
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Foundation Components,Acrobat Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2071'
ht-degree: 16%

---

# [!DNL Adobe Sign]을(를) AEM [!DNL Forms]과(와) 통합{#integrate-adobe-sign-with-aem-forms}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms.html?lang=en#adobe-acrobat-sign-for-government) |
| AEM 6.5 | 이 문서 |

[!DNL Adobe Sign]은(는) 적응형 양식용 전자 서명 워크플로를 사용합니다. 전자 서명은 법무, 판매, 임금, 인적 자원 관리 등의 다양한 분야에서 문서를 처리하는 워크플로를 개선합니다.

대표적인 [!DNL Adobe Acrobat Sign] 및 적응형 양식 시나리오에서 사용자는 서비스에 적용할 적응형 양식에 정보를 입력합니다. 신용 카드 신청 양식과 시민 혜택 양식을 예로 들 수 있습니다. 사용자가 신청 양식에 정보를 입력하고 이를 제출한 뒤 서명하면, 이후의 액션이 가능하도록 양식이 서비스 제공자에게 전달됩니다. 서비스 제공자는 신청서를 검토하고 [!DNL Adobe Acrobat Sign]을 사용해 신청을 승인된 것으로 표시합니다. AEM Forms은 정부용 Adobe Acrobat Sign 및 Adobe Acrobat Sign Solutions을 모두 지원합니다. 라이선스 및 요구 사항에 따라 다음 솔루션 중 하나와 AEM Forms을 통합하거나 연결할 수 있습니다.

* [AEM Forms과 Adobe Acrobat Sign 연결](#adobe-sign)
* [AEM Forms과 Adobe Acrobat Sign Solutions for Government 연결](#adobe-acrobat-sign-for-government)

## AEM Forms과 Adobe Acrobat Sign 연결 {#adobe-sign}

**[!DNL AEM Forms]**&#x200B;을(를) **[!DNL Adobe Acrobat Sign]**&#x200B;과(와) 연결하려면 필수 구성 요소 섹션에 나열된 소프트웨어 및 계정을 설정하고 Adobe Sign을 모든 AEM Forms 작성자 및 Publish 인스턴스에 연결합니다.

## 사전 요구 사항 {#prerequisites}

[!DNL Adobe Sign]을(를) AEM [!DNL Forms]과(와) 통합하려면 다음이 필요합니다.

* 활성 [Adobe Sign 개발자 계정.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* [SSL이 활성화됨](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms] 서버.
* [Adobe Sign API 애플리케이션](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* [!DNL Adobe Sign] API 애플리케이션의 자격 증명(클라이언트 ID 및 클라이언트 보안).
* 다시 구성할 때는 작성자 및 게시 인스턴스 모두에서 기존 [!DNL Adobe Sign] 구성을 제거하십시오.
* 작성자에 대해 [동일한 암호 키](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)를 사용하고 인스턴스를 게시합니다.

## AEM [!DNL Forms]을(를) 사용하여 [!DNL Adobe Sign] 구성 {#configure-adobe-sign-with-aem-forms}

전제 조건이 갖추어지면 작성자 인스턴스에서 AEM [!DNL Forms]을(를) 사용하여 [!DNL Adobe Sign]을(를) 구성하려면 다음 단계를 수행하십시오.

1. AEM [!DNL Forms] 작성자 인스턴스에서 **도구** ![hammer](assets/hammer.png) > **[!UICONTROL 일반]** > **[!UICONTROL 구성 브라우저]**&#x200B;로 이동합니다.
1. **[!UICONTROL 구성 브라우저]** 페이지에서 **[!UICONTROL 만들기]**&#x200B;를 선택합니다.
   * 자세한 내용은 [구성 브라우저](/help/sites-administering/configurations.md) 설명서를 참조하십시오.
1. **[!UICONTROL 구성 만들기]** 대화 상자에서 구성에 대한 **[!UICONTROL 제목]**&#x200B;을 지정하고 **[!UICONTROL 클라우드 구성]**&#x200B;을 사용하도록 설정하고 **[!UICONTROL 만들기]**&#x200B;를 선택합니다. 구성 컨테이너를 만듭니다.
1. **도구** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Sign]**(으)로 이동한 다음 위의 단계에서 만든 구성 컨테이너를 선택합니다.

   >[!NOTE]
   >
   >1~4단계를 실행하여 구성 컨테이너를 만들고 컨테이너에 [!DNL Adobe Sign] 구성을 만들거나 **도구** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Sign]**&#x200B;에서 기존 `global` 폴더를 사용할 수 있습니다. 새 구성 컨테이너에서 구성을 만드는 경우 적응형 양식을 만들 때 **[!UICONTROL 구성 컨테이너]** 필드에 컨테이너 이름을 지정해야 합니다.

   >[!NOTE]
   >
   >Cloud Service 구성 페이지의 URL이 **HTTPS**(으)로 시작하는지 확인하십시오. 그렇지 않으면 AEM [!DNL Forms] 서버에 대해 [SSL을 사용하도록 설정](/help/sites-administering/ssl-by-default.md)합니다.


1. 구성 페이지에서 **[!UICONTROL 만들기]**&#x200B;를 탭하여 AEM [!DNL Forms]에서 [!DNL Adobe Sign] 구성을 만듭니다.
1. **[!UICONTROL Adobe Sign 구성 만들기]** 페이지의 **[!UICONTROL 일반]** 탭에서 구성에 대한 **[!UICONTROL 이름]**&#x200B;을 지정하고 **[!UICONTROL 다음]**&#x200B;을 탭합니다. 원할 경우 제목을 지정하고 구성에 대한 썸네일을 찾아 선택할 수 있습니다.
1. 이제 **[!UICONTROL 솔루션을 선택]**&#x200B;하여 [!DNL Adobe Acrobat Sign]을(를) 선택할 수 있습니다.

   ![Adobe Acrobat Sign Solutions](/help/forms/using/assets/adobe-sign-solution.png)

1. 현재 브라우저 창의 URL을 메모장에 복사하고 URL에서 /`ui#/aem` 부분을 제거합니다. 이후 단계에서 [!DNL AEM Forms] (으)로 [!DNL Adobe Acrobat Sign] 응용 프로그램을 구성하려면 수정된 URL이 필요합니다. [!UICONTROL 다음]을 누릅니다.

1. **[!UICONTROL 설정]** 탭에서,
   * **[!UICONTROL OAuth URL]** 필드에 Adobe Sign 데이터베이스 분할이 포함된 기본 URL이 포함되어 있습니다. URL 형식은 다음과 같습니다.

     `https://<shard>/public/oauth/v2`

     예:
     `https://secure.na1.echosign.com/public/oauth/v2`

   * **[!UICONTROL 액세스 토큰 URL]** 필드에 Adobe Sign 데이터베이스 분할이 포함된 기본 URL이 있습니다. URL 형식은 다음과 같습니다.

     `https://<shard>/oauth/v2/token`

     예:
     `https://api.na1.echosign.com/oauth/v2/token`

   여기에서

   **na1**&#x200B;은 기본값 데이터베이스 분할을 의미합니다. 데이터베이스 분할의 값을 수정할 수 있습니다. [!DNL &#x200B; Adobe Acrobat Sign] 클라우드 구성이 [올바른 분할](https://helpx.adobe.com/sign/using/identify-account-shard.html)을 가리켜야 합니다.

   >[!NOTE]
   >
   >* **Adobe Acrobat Sign 구성 만들기** 페이지를 열어 두십시오. 닫지 마세요. 향후 단계에 설명된 대로 [!DNL Adobe Acrobat Sign] 응용 프로그램에 대한 OAuth 설정을 구성한 후 **클라이언트 ID** 및 **클라이언트 암호**&#x200B;을(를) 검색할 수 있습니다.
   >* Adobe Sign 계정에 로그인한 후 **[!UICONTROL Acrobat Sign API]** > **[!UICONTROL API 정보]** > **[!UICONTROL REST API 메서드 설명서]** > **[!UICONTROL OAuth 액세스 토큰]**&#x200B;으로 이동하여 Adobe Sign OAuth URL 및 액세스 토큰 URL과 관련된 정보에 액세스합니다.

1. [!DNL Adobe Sign] 애플리케이션에 대한 OAuth 설정을 구성합니다.

   1. 브라우저 창을 열고 [!DNL Adobe Sign] 개발자 계정에 로그인합니다.
   1. AEM [!DNL Forms]에 대해 구성된 응용 프로그램을 선택하고 **[!UICONTROL 응용 프로그램에 대한 OAuth 구성]**&#x200B;을 선택합니다.
   1. **[!UICONTROL 클라이언트 ID]** 및 **[!UICONTROL 클라이언트 암호]**&#x200B;를 메모장에 복사합니다.
   1. **[!UICONTROL 리디렉션 URL]** 상자에서 이전 단계에서 복사한 HTTPS URL을 추가합니다.
   1. [!DNL Adobe Sign] 응용 프로그램에 대해 다음 OAuth 설정을 사용하도록 설정하고 **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

   * agreement_read
   * agreement_write
   * agreement_send
   * widget_write
   * workflow_read

   [!DNL Adobe Sign] 애플리케이션에 대한 OAuth 설정을 구성하고 키를 얻는 방법에 대한 단계별 정보는 [애플리케이션에 대한 oAuth 설정 구성](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) 개발자 문서를 참조하십시오.

   ![OAuth Config](assets/oauthconfig_new.png)

<!--
1. Go back to the **[!UICONTROL Create Adobe Sign Configuration]** page. In the **[!UICONTROL Settings]** tab, the **[!UICONTROL OAuth URL]** field mentions the  default URL. The format of the URL is:

   `https://<shard>/public/oAuth/v2`

   For example: 
   `https://secure.na1.echosign.com/public/oauth/v2`

   where:

   **na1** refers to the default database shard.

   You can modify the value for the database shard. Restart the server to be able to use the new value for the database shard.

   >[!NOTE]
   >
   >Ensure that your author and publish instance configurations point to the same shard. If you create multiple Adobe Sign configurations for an organization, ensure all the configurations utilize the same shard. -->

1. **[!UICONTROL Adobe Sign 구성 만들기]** 페이지로 돌아갑니다. **[!UICONTROL 설정]** 탭에서 **클라이언트 ID**(응용 프로그램 ID라고도 함) 및 **클라이언트 암호**&#x200B;를 지정합니다. AEM Forms용으로 만든 [Adobe Sign 응용 프로그램의 클라이언트 ID 및 클라이언트 암호](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret)를 사용하십시오.

1. **[!UICONTROL 첨부 파일에도 Adobe Sign 사용]** 옵션을 선택하여 적응형 양식에 첨부된 파일을 서명을 위해 전송된 해당 [!DNL Adobe Sign] 문서에 연결합니다.

1. **[!UICONTROL Adobe Sign에 연결]**&#x200B;을 선택합니다. 자격 증명을 입력하라는 메시지가 표시되면 [!DNL Adobe Sign] 응용 프로그램을 만드는 동안 사용한 계정의 사용자 이름과 암호를 제공하십시오.

   ![Adobe Acrobat Sign 클라우드 구성 성공](assets/adobe-sign-cloud-configuration-success.png)

1. **[!UICONTROL 만들기]**&#x200B;를 눌러 [!DNL Adobe Sign] 구성을 만듭니다.
1. AEM 웹 콘솔을 엽니다. URL은 `https://'[server]:[port]'/system/console/configMgr`입니다.
1. **[!UICONTROL Forms 일반 구성 서비스].** 열기
1. **[!UICONTROL 허용]** 필드에서 모든 사용자(익명 또는 로그인한 모든 사용자)를 **선택**&#x200B;하고 첨부 파일을 미리 보고 양식을 확인 및 서명할 수 있으며 **[!UICONTROL 저장]을 클릭합니다.** 작성자 인스턴스가 [!DNL Adobe Sign]을(를) 사용하도록 구성되어 있습니다.
1. 구성을 Publish에 추가합니다.
1. [복제](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html)를 사용하여 해당 게시 인스턴스에 동일한 구성을 만드십시오.

이제 [!DNL Adobe Sign]이(가) AEM [!DNL Forms]과(와) 통합되어 적응형 양식에서 사용할 수 있습니다. [적응형 양식에서 Adobe Sign 서비스를 사용하려면](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form) 적응형 양식 속성에서 위에서 만든 구성 컨테이너를 지정하십시오.

>[!NOTE]
>
>Adobe Sign 샌드박스를 구성하려면 [Adobe Sign](#adobe-sign)에 설명된 것과 동일한 구성 단계를 따를 수 있습니다.

## AEM Forms과 Adobe Acrobat Sign Solutions for Government 연결 {#adobe-acrobat-sign-for-government}

AEM Forms과 Adobe Acrobat Sign Solutions for Government를 연결하는 것은 여러 단계로 구성됩니다. 여기에는 다음이 포함됩니다.

* AEM 인스턴스에 대한 리디렉션 URL 만들기
* 리디렉션 URL 및 범위를 Adobe Sign Solutions for Government 팀과 공유
* Adobe Sign 팀으로부터 자격 증명 받기
* 수신한 자격 증명을 사용하여 AEM Forms과 Adobe Acrobat Sign Solutions for Government 연결

![adobe-acrobat-sign-govt-workflow](/help/forms/using/assets/adobe-acrobat-sign-govt-workflow.png)

### 시작하기 전 {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

AEM Forms과 Adobe Acrobat Sign 솔루션 연결을 시작하기 전에

* [Adobe Acrobat Sign Solutions for Government](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning) 계정이 프로비저닝되었는지 확인하십시오.
* AEM [!DNL Forms] 서버가 [SSL 사용](/help/sites-administering/ssl-by-default.md) 상태입니다.
* AEM [!DNL Forms] 서버에서 작성자 및 게시 인스턴스에 대해 [동일한 암호 키](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)를 사용하고 있습니다.

### AEM Forms을 Adobe Acrobat Sign Solutions for Government에 연결 {#connect-adobe-acrobat-sign-for-government}

#### AEM 인스턴스에 대한 리디렉션 URL 만들기

1. AEM Forms 인스턴스에서 **[!UICONTROL 도구]** ![hammer](assets/hammer.png) > **[!UICONTROL 일반]** > **[!UICONTROL 구성 브라우저]**&#x200B;로 이동합니다.
1. **[!UICONTROL 구성 브라우저]** 페이지에서 **[!UICONTROL 만들기]**&#x200B;를 선택합니다.
1. **[!UICONTROL 구성 만들기]** 대화 상자에서 구성에 대한 **[!UICONTROL 제목]**&#x200B;을 지정하고 **[!UICONTROL 클라우드 구성]**&#x200B;을 사용하도록 설정하고 **[!UICONTROL 만들기]**&#x200B;를 선택합니다. 구성 컨테이너를 만듭니다. 컨테이너/폴더 이름에 공백이 없는지 확인합니다.

1. **[!UICONTROL 도구]** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Acrobat Sign]**(으)로 이동한 다음 이전 단계에서 만든 구성 컨테이너를 엽니다. 적응형 양식을 만들 때 **[!UICONTROL 구성 컨테이너]** 필드에 컨테이너 이름을 지정하십시오.
1. 구성 페이지에서 **[!UICONTROL 만들기]**&#x200B;를 선택하여 AEM Forms에서 [!DNL Adobe Acrobat Sign] 구성을 만듭니다.
1. URL에서 현재 브라우저 창의 URL을 메모장에 복사합니다. 이 URL을 `re-direct URL`(으)로 합니다. 다음 섹션에서는 `re-direct URL` 및 `Scopes`을(를) Adobe Sign 팀과 공유하고 자격 증명(클라이언트 ID 및 클라이언트 암호)을 요청합니다.

>[!NOTE]
>
>
>* `re-direct URL`은(는) [최상위](https://en.wikipedia.org/wiki/Top-level_domain) 도메인을 포함해야 합니다. 예, `https://adobe.com/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`
>* 로컬 URL을 `re-direct URL`(으)로 사용하지 마십시오. 예: `https://localhost:4502/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`


#### 리디렉션 URL 및 범위를 Adobe Sign 팀과 공유하고 자격 증명을 받습니다

Adobe Acrobat Sign for Government Solutions 팀은 AEM Forms을 Adobe Acrobat Sign Solutions for Government에 연결할 수 있는 자격 증명(클라이언트 ID 및 클라이언트 암호)을 생성하려면 Adobe Acrobat Sign 응용 프로그램(아래 나열됨)에 대해 `re-direct URL` 및 특정 범위를 활성화해야 합니다.

Adobe Acrobat Sign `scopes`(아래 나열)과 이전 섹션의 마지막 단계에서 만들고 기록한 `re-direct URL`을(를) 정부 솔루션 담당자 [Adobe Professional Services 팀 구성원](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password)과(와) 공유합니다.

**_범위_**

* [!DNL agreement_read]
* [!DNL agreement_write]
* [!DNL agreement_send]
* [!DNL widget_read]
* [!DNL widget_write]
* [!DNL workflow_read]
* [!DNL offline_access]

담당자는 자격 증명을 생성하고 사용자와 공유합니다. 다음 섹션에서는 자격 증명(클라이언트 ID 및 클라이언트 암호)을 사용하여 AEM Forms을 Adobe Acrobat Sign Solutions for Government에 연결합니다.

#### 수신한 자격 증명을 사용하여 AEM Forms과 Adobe Acrobat Sign Solutions for Government를 연결합니다.

1. 브라우저에서 `re-direct URL`을(를) 엽니다. [AEM 인스턴스에 리디렉션 URL 만들기](#create-redirect-url) 섹션의 마지막 단계에서 `re-direct URL`을(를) 만들고 기록했습니다.

1. **[!UICONTROL Adobe Sign 구성 만들기]** 페이지의 **[!UICONTROL 일반]** 탭에서 구성에 대한 **[!UICONTROL 이름]**&#x200B;을 지정하고 **[!UICONTROL 다음]**&#x200B;을 선택합니다. 필요에 따라 **[!UICONTROL 제목]**&#x200B;을 지정하고 구성에 대한 **[!UICONTROL 썸네일]**&#x200B;을 찾아 선택할 수 있습니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. **[!UICONTROL Adobe Sign 구성 만들기]** 페이지의 **[!UICONTROL 설정]** 탭에서 **[!UICONTROL 솔루션 선택]** 옵션에 대해 [!DNL Adobe Acrobat Sign Solutions for Government]을(를) 선택합니다.

   ![정부용 Adobe Acrobat Sign Solutions](/help/forms/using/assets/adobe-sign-for-govt.png)

1. **[!UICONTROL 전자 메일]** 필드에서 Adobe Acrobat Sign Solutions for Government 계정과 연결된 전자 메일 주소를 지정합니다.

1. **[!UICONTROL 설정]** 탭에서,
   * **[!UICONTROL OAuth URL]** 필드에 Adobe Sign 데이터베이스 분할이 포함된 기본 URL이 포함되어 있습니다. URL 형식은 다음과 같습니다.

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/authorize`

     예:
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/authorize`

   * **[!UICONTROL 액세스 토큰 URL]** 필드에 Adobe Sign 데이터베이스 분할이 포함된 기본 URL이 있습니다. URL 형식은 다음과 같습니다.

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/token`

     예:
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/token`

   여기에서

   **na1**&#x200B;은 기본값 데이터베이스 분할을 의미합니다. 데이터베이스 분할의 값을 수정할 수 있습니다. [!DNL &#x200B; Adobe Acrobat Sign] 클라우드 구성이 [올바른 분할](https://helpx.adobe.com/sign/using/identify-account-shard.html)을 가리켜야 합니다.

   >[!NOTE]
   >
   >* Adobe Sign 계정에 로그인한 후 **[!UICONTROL Acrobat Sign API]** > **[!UICONTROL API 정보]** > **[!UICONTROL REST API 메서드 설명서]** > **[!UICONTROL OAuth 액세스 토큰]**(으)로 이동하여 Adobe Sign oAuth URL 및 액세스 토큰 URL과 관련된 정보에 액세스합니다.

1. 이전 섹션의 정부 솔루션 담당자([Adobe Professional Services 팀 구성원])용 Adobe Acrobat Sign에서 공유한 자격 증명을 [**[!UICONTROL 클라이언트 ID]** 및 **[!UICONTROL 클라이언트 암호]**]로 사용합니다.

1. **[!UICONTROL 첨부 파일에 Adobe Acrobat Sign 사용]** 옵션을 선택하여 적응형 양식에 첨부된 파일을 서명을 위해 전송된 해당 [!DNL Adobe Acrobat Sign] 문서에 추가하십시오.

1. **[!UICONTROL Adobe Sign에 연결]**&#x200B;을 선택합니다. 자격 증명을 입력하라는 메시지가 뜨면 [!DNL Adobe Acrobat Sign] 애플리케이션 생성 시 사용한 계정의 사용자 이름과 비밀번호를 입력합니다. `Adobe Acrobat Sign for Government Solutions` 및 의 액세스를 확인하는 메시지가 표시되면 **[!UICONTROL 액세스 허용]**&#x200B;을 클릭합니다. 자격 증명이 올바르고 [!DNL Adobe Acrobat Sign] 개발자 계정에 대한 [!DNL AEM Forms]의 액세스를 허용하면 아래에 제시된 것과 비슷한 성공 메시지가 표시됩니다.

   ![Adobe Acrobat Sign 클라우드 구성 성공](/help/forms/using/assets/adobe-sign-cloud-configuration-success.png)

   자격 증명을 입력하라는 메시지가 뜨면 [!DNL Adobe Acrobat Sign] 애플리케이션 생성 시 사용한 계정의 사용자 이름과 비밀번호를 입력합니다. `your account`에 대한 액세스를 확인하는 메시지가 표시되면 **[!UICONTROL 액세스 허용]**&#x200B;을 클릭합니다.

1. 구성을 만들려면 **[!UICONTROL 만들기]**&#x200B;를 선택하십시오.
1. AEM 웹 콘솔을 엽니다. URL은 `https://'[server]:[port]'/system/console/configMgr`입니다.
1. **[!UICONTROL Forms 일반 구성 서비스].** 열기
1. **[!UICONTROL 허용]** 필드에서 모든 사용자(익명 또는 로그인한 모든 사용자)를 **선택**&#x200B;하고 첨부 파일을 미리 보고 양식을 확인 및 서명할 수 있으며 **[!UICONTROL 저장]을 클릭합니다.** 작성자 인스턴스가 [!DNL Adobe Sign]을(를) 사용하도록 구성되어 있습니다.

1. 구성을 Publish에 추가합니다.
1. [복제](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html)를 사용하여 해당 게시 인스턴스에 동일한 구성을 만드십시오.

이제 [적응형 양식에서 Adobe Acrobat Sign 필드 추가](working-with-adobe-sign.md) 또는 [AEM 워크플로](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)를 사용할 수 있습니다. Cloud Service 구성에 사용된 구성 컨테이너를 [!DNL Adobe Acrobat Sign]에 대해 사용 중인 모든 적응형 Forms에 추가해야 합니다. 적응형 양식의 속성에서 구성 컨테이너를 지정할 수 있습니다.


## 서명 상태를 동기화하도록 [!DNL Adobe Sign] 스케줄러 구성 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

[!DNL Adobe Sign] 사용 적응형 양식은 모든 서명자가 서명 프로세스를 완료한 후에만 제출됩니다. 기본적으로 [!DNL Adobe Sign] 스케줄러 서비스는 서명자 응답을 24시간마다 확인(폴링)하도록 예약되어 있습니다. 환경에 대한 기본 간격을 변경할 수 있습니다. 기본 간격을 변경하려면 다음 단계를 수행하십시오.

1. 관리자 자격 증명으로 AEM [!DNL Forms] 서버에 로그인하고 **도구** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**&#x200B;로 이동합니다.

   브라우저 창에서 다음 URL을 열 수도 있습니다.
   `https://[localhost]:'port'/system/console/configMgr`

1. **[!UICONTROL Adobe Sign 구성 서비스]** 옵션을 찾아 엽니다. **[!UICONTROL 상태 업데이트 스케줄러 표현식]** 필드에 [cron 표현식](https://en.wikipedia.org/wiki/Cron#CRON_expression)을 지정하고 **[!UICONTROL 저장]**&#x200B;을 클릭합니다. 예를 들어 매일 오전 00:00에 구성 서비스를 실행하려면 **[!UICONTROL 상태 업데이트 스케줄러 표현식]** 필드에 `0 0 0 1/1 * ? *`을(를) 지정합니다.

[!DNL Adobe Sign]의 동기화 상태 기본 간격이 변경되었습니다.

## 관련 문서 {#related-articles}

* [적응형 양식에서 Adobe Sign 사용](../../forms/using/working-with-adobe-sign.md)
* [양식 중심 워크플로가 포함된 Adobe Sign](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)
* [AEM Forms에서 Adobe Sign 사용(비디오)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
