---
title: Adobe Sign과 AEM Forms 통합
seo-title: Integrate Adobe Sign with AEM Adaptive Forms
description: AEM 적응형 Forms에 대한 Adobe Sign을 구성하는 방법에 대해 알아봅니다. Adobe Sign은 워크플로우를 개선하고 법률, 판매, 급여, 인적 자원 관리 등의 다양한 영역에 대한 문서를 처리합니다.
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: Adaptive Forms, Acrobat Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 17%

---

# 통합 [!DNL Adobe Sign] AEM 사용 [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms.html?lang=en#adobe-acrobat-sign-for-government) |
| AEM 6.5 | 이 문서 |

[!DNL Adobe Sign] 은 적응형 양식용 전자 서명 워크플로를 가능하게 합니다. 전자 서명은 법무, 판매, 임금, 인적 자원 관리 등의 다양한 분야에서 문서를 처리하는 워크플로를 개선합니다.

대표적인 [!DNL Adobe Acrobat Sign] 및 적응형 양식 시나리오에서 사용자는 서비스에 적용할 적응형 양식에 정보를 입력합니다. 신용 카드 신청 양식과 시민 혜택 양식을 예로 들 수 있습니다. 사용자가 신청 양식에 정보를 입력하고 이를 제출한 뒤 서명하면, 이후의 액션이 가능하도록 양식이 서비스 제공자에게 전달됩니다. 서비스 제공자는 신청서를 검토하고 [!DNL Adobe Acrobat Sign]을 사용해 신청을 승인된 것으로 표시합니다. AEM Forms은 정부용 Adobe Acrobat Sign 및 Adobe Acrobat Sign Solutions을 모두 지원합니다. 라이선스 및 요구 사항에 따라 다음 솔루션 중 하나와 AEM Forms을 통합하거나 연결할 수 있습니다.

* [AEM Forms과 Adobe Acrobat Sign 연결](#adobe-sign)
* [AEM Forms과 Adobe Acrobat Sign Solutions for Government 연결](#adobe-acrobat-sign-for-government)

## AEM Forms과 Adobe Acrobat Sign 연결 {#adobe-sign}

연결하려면 **[!DNL AEM Forms]** 포함 **[!DNL Adobe Acrobat Sign]**&#x200B;의 사전 요구 사항 섹션에 나열된 소프트웨어 및 계정을 설정하고 Adobe Sign을 모든 AEM Forms 작성자 및 게시 인스턴스에 연결합니다.

## 사전 요구 사항 {#prerequisites}

다음을 통합해야 합니다. [!DNL Adobe Sign] AEM 사용 [!DNL Forms]:

* 활성 [Adobe Sign 개발자 계정입니다.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* An [SSL 활성화됨](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms] 서버입니다.
* [Adobe Sign API 애플리케이션](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* [!DNL Adobe Sign] API 애플리케이션의 자격 증명(클라이언트 ID 및 클라이언트 보안).
* 재구성할 때 기존 제거 [!DNL Adobe Sign] 작성자 및 게시 인스턴스 모두로부터의 구성.
* 작성자에 대해 [동일한 암호 키](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)를 사용하고 인스턴스를 게시합니다.

## 구성 [!DNL Adobe Sign] AEM 사용 [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

전제 조건이 갖추어지면 다음 단계를 수행하여 을 구성합니다 [!DNL Adobe Sign] AEM 사용 [!DNL Forms] 작성자 인스턴스에서 다음을 수행합니다.

1. AEM에서 [!DNL Forms] 작성자 인스턴스, 다음으로 이동 **도구** ![망치](assets/hammer.png) > **[!UICONTROL 일반]** > **[!UICONTROL 구성 브라우저]**.
1. 다음에서 **[!UICONTROL 구성 브라우저]** 페이지, 선택 **[!UICONTROL 만들기]**.
   * 다음을 참조하십시오. [구성 브라우저](/help/sites-administering/configurations.md) 설명서 를 참조하십시오.
1. 다음에서 **[!UICONTROL 구성 만들기]** 대화 상자, 지정 **[!UICONTROL 제목]** 구성의 경우 활성화 **[!UICONTROL 클라우드 구성]**, 및 선택 **[!UICONTROL 만들기]**. 구성 컨테이너를 만듭니다.
1. 다음으로 이동 **도구** ![망치](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Sign]** 위의 단계에서 생성한 구성 컨테이너를 선택합니다.

   >[!NOTE]
   >
   >1-4단계를 실행하여 구성 컨테이너를 만들고 [!DNL Adobe Sign] 컨테이너에서 구성 또는 기존 사용 `global` 폴더 위치 **도구** ![망치](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Sign]**. 새 구성 컨테이너에서 구성을 생성하는 경우 **[!UICONTROL 구성 컨테이너]** 적응형 양식을 만들 때 필드.

   >[!NOTE]
   >
   Cloud Service 구성 페이지의 URL이 다음으로 시작하는지 확인합니다. **HTTPS**. 그렇지 않은 경우, [ssl 활성화](/help/sites-administering/ssl-by-default.md) AEM용 [!DNL Forms] 서버입니다.

1. 구성 페이지에서 을 선택합니다 **[!UICONTROL 만들기]** 만들려면 [!DNL Adobe Sign] AEM의 구성 [!DNL Forms].
1. 다음에서 **[!UICONTROL 일반]** 의 탭 **[!UICONTROL Adobe Sign 구성 만들기]** 페이지, 지정 **[!UICONTROL 이름]** 구성 및 선택 **[!UICONTROL 다음]**. 원할 경우 제목을 지정하고 구성에 대한 썸네일을 찾아 선택할 수 있습니다.

1. 현재 브라우저 창의 URL을 메모장에 복사합니다. 를 구성하는 데 필요합니다. [!DNL Adobe Sign] AEM이 있는 애플리케이션[!DNL Forms].

1. 다음에서 **[!UICONTROL 설정]** 탭, **[!UICONTROL OAuth URL]** 필드에는 기본 URL이 포함되어 있습니다. URL 형식은 다음과 같습니다.

   `https://<shard>/public/oAuth/v2`

   예:
   `https://secure.na1.echosign.com/public/oauth/v2`

   여기에서

   **na1**&#x200B;은 기본값 데이터베이스 분할을 의미합니다. 데이터베이스 분할의 값을 수정할 수 있습니다. [!DNL  Adobe Sign] 클라우드 구성이 [올바른 분할](https://helpx.adobe.com/sign/using/identify-account-shard.html)을 가리켜야 합니다.

   Adobe Experience Manager 기능이나 구성 요소에 대한 또 다른 [!DNL Adobe Sign] 구성을 생성하는 경우, 모든 [!DNL Adobe Sign] 클라우드 구성이 동일한 분할을 가리켜야 합니다.

   >[!NOTE]
   >
   유지 **Adobe Sign 구성 만들기** 페이지가 열립니다. 닫지 마세요. 다음을 검색할 수 있습니다. **클라이언트 ID** 및 **클라이언트 암호** 에 대한 OAuth 설정을 구성한 후 [!DNL Adobe Sign] 다음 단계에 설명된 대로 애플리케이션.


1. [!DNL Adobe Sign] 애플리케이션에 대한 OAuth 설정을 구성합니다.

   1. 브라우저 창을 열고 [!DNL Adobe Sign] 개발자 계정입니다.
   1. AEM에 대해 구성된 애플리케이션 선택 [!DNL Forms], 및 선택 **[!UICONTROL 애플리케이션에 대한 OAuth 구성]**.
   1. 다음을 복사합니다. **[!UICONTROL 클라이언트 ID]** 및 **[!UICONTROL 클라이언트 암호]** 메모장에.
   1. 다음에서 **[!UICONTROL 리디렉션 URL]** 이전 단계에서 복사한 HTTPS URL을 추가합니다.
   1. 에 대해 다음 OAuth 설정을 활성화합니다. [!DNL Adobe Sign] 애플리케이션 및 클릭 **[!UICONTROL 저장]**.

   * agreement_read
   * agreement_write
   * agreement_send
   * widget_write
   * workflow_read

   [!DNL Adobe Sign] 애플리케이션에 대한 OAuth 설정을 구성하고 키를 얻는 방법에 대한 단계별 정보는 [애플리케이션에 대한 oAuth 설정 구성](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) 개발자 문서를 참조하십시오.

   ![OAuth Config](assets/oauthconfig_new.png)

1. 로 돌아가기 **[!UICONTROL Adobe Sign 구성 만들기]** 페이지를 가리키도록 업데이트하는 중입니다. 다음에서 **[!UICONTROL 설정]** 탭, **[!UICONTROL OAuth URL]** 필드에는 기본 URL이 언급되어 있습니다. URL 형식은 다음과 같습니다.

   `https://<shard>/public/oAuth/v2`

   예:
   `https://secure.na1.echosign.com/public/oauth/v2`

   여기에서

   **na1** 는 기본 데이터베이스 분할을 나타냅니다.

   데이터베이스 분할의 값을 수정할 수 있습니다. 데이터베이스 분할에 새 값을 사용하려면 서버를 다시 시작합니다.

   >[!NOTE]
   >
   작성자 및 게시 인스턴스 구성이 동일한 분할을 가리켜야 합니다. 조직에 대해 여러 Adobe Sign 구성을 만드는 경우 모든 구성이 동일한 분할을 활용하는지 확인하십시오.

1. 로 돌아가기 **[!UICONTROL Adobe Sign 구성 만들기]** 페이지를 가리키도록 업데이트하는 중입니다. 다음에서 **[!UICONTROL 설정]** 탭에서 **클라이언트 ID** (애플리케이션 ID라고도 함) 및 **클라이언트 암호**. 사용 [Adobe Sign 애플리케이션의 클라이언트 ID 및 클라이언트 암호](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) AEM Forms용으로 만들어졌습니다.

1. 다음 항목 선택 **[!UICONTROL 첨부 파일에도 Adobe Sign 활성화]** 적응형 양식에 첨부된 파일을 해당 파일에 추가하는 옵션 [!DNL Adobe Sign] 서명을 위해 문서를 보냈습니다.

1. 선택 **[!UICONTROL Adobe Sign에 연결]**. 자격 증명을 입력하라는 메시지가 뜨면 생성 시 사용한 계정의 사용자 이름과 비밀번호를 입력합니다 [!DNL Adobe Sign] 응용 프로그램.

1. 선택 **[!UICONTROL 만들기]** 을(를) 만들려면 [!DNL Adobe Sign] 구성.

1. AEM 웹 콘솔을 엽니다. URL은 `https://'[server]:[port]'/system/console/configMgr`
1. 열기 **[!UICONTROL Forms 공통 구성 서비스].**
1. 다음에서 **[!UICONTROL 허용]** 필드, **선택** 모든 사용자 - 익명 또는 로그인한 모든 사용자는 첨부 파일을 미리 보고, 양식을 확인 및 서명하고, **[!UICONTROL 저장].** 작성자 인스턴스가 다음을 사용하도록 구성되었습니다. [!DNL Adobe Sign].
1. 구성을 게시합니다.
1. 사용 [복제](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html) 를 클릭하여 해당 게시 인스턴스에 동일한 구성을 만듭니다.

자, [!DNL Adobe Sign] AEM과 통합됨 [!DNL Forms] 적응형 양식에서 사용할 수 있습니다. 종료 [적응형 양식에서 Adobe Sign 서비스 사용](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), 적응형 양식 속성에서 위에서 만든 구성 컨테이너를 지정합니다.

## AEM Forms과 Adobe Acrobat Sign Solutions for Government 연결 {#adobe-acrobat-sign-for-government}

AEM Forms과 Adobe Acrobat Sign Solutions for Government를 연결하는 것은 여러 단계로 구성됩니다. 여기에는 다음이 포함됩니다.

* AEM 인스턴스에 대한 리디렉션 URL 만들기
* 리디렉션 URL 및 범위를 Adobe Sign Solutions for Government 팀과 공유
* Adobe Sign 팀으로부터 자격 증명 받기
* 수신한 자격 증명을 사용하여 AEM Forms과 Adobe Acrobat Sign Solutions for Government 연결

![adobe-acrobat-sign-govt-workflow](/help/forms/using/assets/adobe-acrobat-sign-govt-workflow.png)

### 시작하기 전 {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

AEM Forms과 Adobe Acrobat Sign 솔루션 연결을 시작하기 전에

* 다음을 확인합니다. [Adobe Acrobat Sign Solutions for Government](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning) 계정이 프로비저닝되었습니다.
* 내 AEM [!DNL Forms] 서버는 [SSL 활성화됨](/help/sites-administering/ssl-by-default.md) .
* 내 AEM [!DNL Forms] 서버에서 다음을 사용 중 [동일한 암호 키](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) 작성자 및 게시 인스턴스용

### AEM Forms을 Adobe Acrobat Sign Solutions for Government에 연결 {#connect-adobe-acrobat-sign-for-government}

#### AEM 인스턴스에 대한 리디렉션 URL 만들기

1. AEM Forms 인스턴스에서 **[!UICONTROL 도구]** ![망치](assets/hammer.png) > **[!UICONTROL 일반]** > **[!UICONTROL 구성 브라우저]**.
1. 다음에서 **[!UICONTROL 구성 브라우저]** 페이지, 선택 **[!UICONTROL 만들기]**.
1. 다음에서 **[!UICONTROL 구성 만들기]** 대화 상자, 지정 **[!UICONTROL 제목]** 구성의 경우 활성화 **[!UICONTROL 클라우드 구성]**, 및 선택 **[!UICONTROL 만들기]**. 구성 컨테이너를 만듭니다. 컨테이너/폴더 이름에 공백이 없는지 확인합니다.

1. 다음으로 이동 **[!UICONTROL 도구]** ![망치](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Acrobat Sign]** 이전 단계에서 생성한 구성 컨테이너를 엽니다. 적응형 양식을 만들 때에서 컨테이너 이름을 지정합니다 **[!UICONTROL 구성 컨테이너]** 필드.
1. 구성 페이지에서 을 선택합니다 **[!UICONTROL 만들기]** 만들려면 [!DNL Adobe Acrobat Sign] AEM Forms의 구성
1. URL에서 현재 브라우저 창의 URL을 메모장에 복사합니다. 이 URL을 라고 합니다. `re-direct URL`. 다음 섹션에서는 `re-direct URL` 및 `Scopes` Adobe Sign 팀 및 요청 자격 증명(클라이언트 ID 및 클라이언트 암호)과 함께 사용할 수 있습니다.

>[!NOTE]
>
>
* A `re-direct URL` 다음을 포함해야 함: [최상위](https://en.wikipedia.org/wiki/Top-level_domain) 도메인. 예, `https://adobe.com/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`
* 로컬 URL을 (으)로 사용하지 않음 `re-direct URL`. 예: `https://localhost:4502/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`


#### 리디렉션 URL 및 범위를 Adobe Sign 팀과 공유하고 자격 증명을 받습니다

Adobe Acrobat Sign for Government Solutions 팀은 `re-direct URL` 또한 Adobe Acrobat Sign 애플리케이션(아래 나열됨)에 대해 활성화할 특정 범위를 사용하여 AEM Forms을 Adobe Acrobat Sign Solutions for Government에 연결할 수 있는 자격 증명(클라이언트 ID 및 클라이언트 암호)을 생성할 수 있습니다.

공유 `scopes` (아래에 나열됨) 및 `re-direct URL` Adobe Acrobat Sign for 정부 솔루션 담당자와 함께 이전 섹션의 마지막 단계를 만들고 기록했습니다. [Adobe Professional Services 팀원](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password).

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

1. 를 엽니다. `re-direct URL` 을 클릭합니다. 을(를) 만들고 적어 두었습니다. `re-direct URL` 의 마지막 단계에서 [AEM 인스턴스에 리디렉션 URL 만들기](#create-redirect-url) 섹션.

1. 다음에서 **[!UICONTROL 일반]** 의 탭 **[!UICONTROL Adobe Sign 구성 만들기]** 페이지, 지정 **[!UICONTROL 이름]** 을(를) 위해 다음을 선택합니다. **[!UICONTROL 다음]**. 다음을 선택적으로 지정할 수 있습니다. **[!UICONTROL 제목]** 을(를) 찾아 선택 **[!UICONTROL 축소판]** 구성. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. 다음에서 **[!UICONTROL 설정]** 의 탭 **[!UICONTROL Adobe Sign 구성 만들기]** 페이지, **[!UICONTROL 솔루션 선택]** 옵션, 선택 [!DNL Adobe Acrobat Sign Solutions for Government].

   ![Adobe Acrobat Sign Solutions for Government](/help/forms/using/assets/adobe-sign-for-govt.png)

1. 다음에서 **[!UICONTROL 이메일]** 필드를 생성하고 정부 계정용 Adobe Acrobat Sign Solutions과 연결된 이메일 주소를 지정합니다.

1. 다음 **[!UICONTROL OAuth URL]** 필드는 Adobe Sign 데이터베이스 분할을 지정합니다. 필드에는 기본 URL이 포함되어 있습니다. URL은 변경하지 마십시오.

1. 정부 솔루션 담당자용 Adobe Acrobat Sign에서 공유한 자격 증명 사용([Adobe Professional Services 팀원]) 이전 섹션에서 [**[!UICONTROL 클라이언트 ID]** 및 **[!UICONTROL 클라이언트 암호]**].

1. 다음 항목 선택 **[!UICONTROL 첨부 파일에 Adobe Acrobat Sign 사용]** 적응형 양식에 첨부된 파일을 해당 파일에 추가하는 옵션 [!DNL Adobe Acrobat Sign] 서명을 위해 문서를 보냈습니다.

1. 선택 **[!UICONTROL Adobe Sign에 연결]**. 자격 증명을 입력하라는 메시지가 뜨면 [!DNL Adobe Acrobat Sign] 애플리케이션 생성 시 사용한 계정의 사용자 이름과 비밀번호를 입력합니다. 다음에 대한 액세스를 확인해달라는 메시지가 뜨는 경우 `Adobe Acrobat Sign for Government Solutions` 및 을 클릭합니다. **[!UICONTROL 액세스 허용]**. 자격 증명이 올바르고 [!DNL Adobe Acrobat Sign] 개발자 계정에 대한 [!DNL AEM Forms]의 액세스를 허용하면 아래에 제시된 것과 비슷한 성공 메시지가 표시됩니다.

   ![Adobe Acrobat Sign 클라우드 구성 성공](/help/forms/using/assets/adobe-sign-cloud-configuration-success.png)

   자격 증명을 입력하라는 메시지가 뜨면 [!DNL Adobe Acrobat Sign] 애플리케이션 생성 시 사용한 계정의 사용자 이름과 비밀번호를 입력합니다. 다음에 대한 액세스를 확인해달라는 메시지가 뜨는 경우 `your account`, 및 클릭 **[!UICONTROL 액세스 허용]**.

1. 선택 **[!UICONTROL 만들기]** 을 클릭하여 구성을 만듭니다.
1. AEM 웹 콘솔을 엽니다. URL은 `https://'[server]:[port]'/system/console/configMgr`
1. 열기 **[!UICONTROL Forms 공통 구성 서비스].**
1. 다음에서 **[!UICONTROL 허용]** 필드, **선택** 모든 사용자 - 익명 또는 로그인한 모든 사용자는 첨부 파일을 미리 보고, 양식을 확인 및 서명하고, **[!UICONTROL 저장].** 작성자 인스턴스가 다음을 사용하도록 구성되었습니다. [!DNL Adobe Sign].

1. 구성을 게시합니다.
1. 사용 [복제](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html) 를 클릭하여 해당 게시 인스턴스에 동일한 구성을 만듭니다.

이제 다음을 수행할 수 있습니다. [적응형 양식에서 Adobe Acrobat Sign 필드 추가 사용](working-with-adobe-sign.md) 또는 [AEM 워크플로](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step). Cloud Service 구성에 사용되는 구성 컨테이너를 활성화할 모든 적응형 Forms에 추가해야 합니다 [!DNL Adobe Acrobat Sign]. 적응형 양식의 속성에서 구성 컨테이너를 지정할 수 있습니다.


## 구성 [!DNL Adobe Sign] 서명 상태를 동기화하는 스케줄러 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

An [!DNL Adobe Sign] 활성화된 적응형 양식은 모든 서명자가 서명 프로세스를 완료한 후에만 제출됩니다. 기본적으로 [!DNL Adobe Sign] 스케줄러 서비스는 서명자 응답을 24시간마다 점검(폴링)하도록 예약되어 있습니다. 환경에 대한 기본 간격을 변경할 수 있습니다. 기본 간격을 변경하려면 다음 단계를 수행하십시오.

1. AEM에 로그인 [!DNL Forms] 관리자 자격 증명이 있는 서버 및 다음으로 이동 **도구** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**.

   브라우저 창에서 다음 URL을 열 수도 있습니다.
   `https://[localhost]:'port'/system/console/configMgr`

1. 을(를) 찾아 엽니다. **[!UICONTROL Adobe Sign 구성 서비스]** 옵션을 선택합니다. 지정 [크론 표현식](https://en.wikipedia.org/wiki/Cron#CRON_expression) 다음에서 **[!UICONTROL 상태 업데이트 스케줄러 표현식]** 필드 및 클릭 **[!UICONTROL 저장]**. 예를 들어 매일 오전 00:00에 구성 서비스를 실행하려면 `0 0 0 1/1 * ? *` 다음에서 **[!UICONTROL 상태 업데이트 스케줄러 표현식]** 필드.

동기화 상태 기본 간격 [!DNL Adobe Sign] 이(가) 변경되었습니다.

## 관련 문서 {#related-articles}

* [적응형 양식에서 Adobe Sign 사용](../../forms/using/working-with-adobe-sign.md)
* [양식 중심 워크플로가 포함된 Adobe Sign](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)
* [AEM Forms과 함께 Adobe Sign 사용(비디오)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
