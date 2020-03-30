---
title: AEM Forms와 Adobe Sign 통합
seo-title: AEM Forms와 Adobe Sign 통합
description: AEM Forms용 Adobe Sign 구성 방법 살펴보기
seo-description: AEM Forms용 Adobe Sign 구성 방법 살펴보기
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# AEM Forms와 Adobe Sign 통합{#integrate-adobe-sign-with-aem-forms}

Adobe Sign을 사용하면 적응형 양식을 위한 전자 서명 워크플로우를 수행할 수 있습니다. 전자 서명은 법률, 영업, 급여, 인사 관리 등 다양한 분야의 문서를 처리하는 워크플로우를 향상시켜 줍니다.

일반적인 Adobe Sign 및 적응형 양식 시나리오에서 사용자는 적응형 양식을 채워 서비스에 ****&#x200B;적용합니다. 예를 들어 신용 카드 신청서와 시민 혜택 양식이 있습니다. 사용자가 애플리케이션 양식을 채우고 제출 및 서명하면 추가 작업을 위해 양식이 서비스 공급업체에 전송됩니다. 서비스 제공업체는 애플리케이션을 검토하고 Adobe Sign을 사용하여 애플리케이션을 승인했음을 표시합니다. 유사한 전자 서명 워크플로우를 사용하려면 AEM Forms와 Adobe Sign을 통합할 수 있습니다.

AEM Forms에서 Adobe Sign을 사용하려면 AEM Cloud Services에서 Adobe Sign을 구성하십시오.

## 전제 조건 {#prerequisites}

Adobe Sign을 AEM Forms와 통합하려면 다음이 필요합니다.

* 유효한 [Adobe Sign 개발자 계정](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* SSL [이 활성화된](/help/sites-administering/ssl-by-default.md) AEM Forms 서버
* Adobe [Sign API 애플리케이션](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Adobe Sign API 응용 프로그램의 자격 증명(클라이언트 ID 및 클라이언트 암호)

## AEM Forms로 Adobe Sign 구성 {#configure-adobe-sign-with-aem-forms}

사전 요구 사항이 준비되면 다음 단계를 수행하여 작성자 인스턴스에서 AEM Forms로 Adobe Sign을 구성합니다.

1. AEM Forms 작성자 인스턴스에서 도구 > **일반** ![](assets/hammer.png) > **구성** 브라우저로 **이동합니다**.
1. 구성 **[!UICONTROL 브라우저]** 페이지에서 만들기를 **[!UICONTROL 누릅니다]**.
1. 구성 **[!UICONTROL 만들기 대화 상자에서]** 구성에 대한 **[!UICONTROL 제목을]** 지정하고 **[!UICONTROL , 클라우드 구성을 활성화하고,]**&#x200B;만들기 **[!UICONTROL 및]**&#x200B;수행을 탭합니다. 클라우드 서비스에 대한 구성 컨테이너를 만듭니다.
1. 도구 **> 클라우드** 서비스 ![](assets/hammer.png) > **Adobe** Sign **으로 이동하여 위** 단계에서 만든 구성 컨테이너를 선택합니다.

   >[!NOTE]
   >
   >클라우드 서비스 구성 페이지의 URL이 HTTPS로 시작되는지 **확인합니다**. 그렇지 않은 경우 AEM [Forms](/help/sites-administering/ssl-by-default.md) 서버에 대해 SSL을 활성화합니다.

1. 구성 페이지에서 만들기를 탭하여 **[!UICONTROL AEM]** Forms에서 Adobe Sign 구성을 만듭니다.
1. Adobe **[!UICONTROL Sign 구성]** 만들기 **[!UICONTROL 페이지의]** 일반 **탭에서** 구성에 대한 **이름을 지정하고 다음 구성을**&#x200B;탭합니다. 원하는 경우 제목을 지정하고 구성에 대한 축소판을 찾아 선택할 수 있습니다.

   현재 브라우저 창에서 URL을 복사합니다. AEM Forms를 사용하여 Adobe Sign 애플리케이션을 구성해야 합니다.

1. Adobe Sign 응용 프로그램에 대한 OAuth 설정을 구성합니다.

   1. 브라우저 창을 열고 Adobe Sign 개발자 계정에 로그인합니다.
   1. AEM Forms에 대해 구성된 응용 프로그램을 선택하고 응용 프로그램에 대한 OAuth 구성을 누릅니다.
   1. 리디렉션 URL **상자에서** 이전 단계에서 복사한 HTTPS URL을 추가하고 저장을 **클릭합니다**.
   1. Adobe Sign 응용 프로그램에 대해 다음 OAuth 설정을 활성화하고 저장을 **클릭합니다**.
   * aggregation_read
   * aggregation_write
   * aggregation_send
   * widget_write
   * workflow_read
   Adobe Sign 응용 프로그램의 OAuth 설정을 구성하고 키를 얻는 단계별 정보는 응용 프로그램 [개발자 설명서의](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobeio/adobeio-documentation/master/sign/gstarted/configure_oauth.md) Auth 설정 구성을 참조하십시오.

   ![OAuth 구성](assets/oauthconfig_new.png)

1. Adobe Sign 구성 **만들기 페이지로** 돌아갑니다. 설정 **[!UICONTROL 탭에서]** OAuth URL **[!UICONTROL 필드에]** 다음 기본 URL이 언급됩니다.

   https://secure.na1.echosign.com/public/oauth

   where:

   **na1은** 기본 데이터베이스 공유를 나타냅니다.

   데이터베이스 공유 값을 수정할 수 있습니다. 데이터베이스 공유 값에 새 값을 사용할 수 있도록 서버를 다시 시작합니다.

1. 클라이언트 **ID** (응용 프로그램 ID라고도 함)와 클라이언트 암호를 **지정합니다**. 첨부 **파일에 대해 Adobe Sign 사용 옵션을 선택하여** 서명을 위해 전송된 해당 Adobe Sign 문서에 적응형 양식에 첨부된 파일을 추가합니다.

   Tap **[!UICONTROL Connect to Adobe Sign]**. 자격 증명을 입력하라는 메시지가 표시되면 Adobe Sign 응용 프로그램을 만들 때 사용한 계정의 사용자 이름과 암호를 입력합니다.

   만들기를 **[!UICONTROL 눌러]** Adobe Sign 구성을 만듭니다.

1. AEM 웹 콘솔을 엽니다. URL은 `https://'[server]:[port]'/system/console/configMgr`
1. Forms **Common Configuration Service를 엽니다.**
1. 허용 **필드에서** 모든 사용자 - 익명 사용자 또는 로그인한 모든 사용자가 첨부 파일을 미리 보고 양식을 확인 및 서명하고 저장을 **클릭합니다** **.** 작성자 인스턴스가 Adobe Sign을 사용하도록 구성되어 있습니다.
1. 게시 [인스턴스에서](/help/sites-deploying/deploy.md) 로그인하고 다음 URL을 엽니다.

   `https://<server-name>:<port>/libs/granite/configurations/content/view.html/conf`

1. 1단계부터 12단계를 반복하여 AEM Forms로 Adobe Sign을 구성합니다. 구성에 동일한 제목(3단계에서 지정한 제목)과 동일한 이름(6단계에서 지정한 이름)을 사용하여 작성자 인스턴스에 구성된 설정을 복제합니다.

   이제 Adobe Sign은 AEM Forms와 통합되어 적응형 양식에 사용할 수 있습니다. 적응형 양식에서 [Adobe Sign 서비스를](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)사용하려면 응용 양식 속성으로 위에서 만든 구성 컨테이너를 지정하십시오.

## 서명 상태를 동기화하도록 Adobe Sign 스케줄러 구성 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Adobe Sign이 활성화된 적응형 양식은 모든 서명자가 서명 프로세스를 완료한 후에만 제출됩니다. 기본적으로 Adobe Sign 스케줄러 서비스는 24시간마다 서명자 응답을 확인(투표)할 예정입니다. 환경의 기본 간격을 변경할 수 있습니다. 기본 간격을 변경하려면 다음 단계를 수행하십시오.

1. 관리 자격 증명으로 AEM Forms 서버에 로그인하고 도구 > 작업 **>** 웹 **콘솔로** 이동합니다 ****.

   브라우저 창에서 다음 URL을 열 수도 있습니다.
   `https://[localhost]:'port'/system/console/configMgr`

1. Adobe Sign 구성 서비스 **옵션을 찾아 엽니다** . 상태 [업데이트 스케줄러 표현식](https://en.wikipedia.org/wiki/Cron#CRON_expression) 필드에 **cron 표현식을** 지정하고 저장을 **클릭합니다**. 예를 들어 오전 00:00에 구성 서비스를 매일 실행하려면 상태 업데이트 스케줄러 `0 0 0 1/1 * ? *` 표현식 **** 필드에 지정합니다.

이제 Adobe Sign의 동기화 상태에 대한 기본 간격이 변경되었습니다.

## 관련 문서 {#related-articles}

* [적응형 양식에서 Adobe Sign 사용](../../forms/using/working-with-adobe-sign.md)
* [AEM Forms에서 Adobe Sign 사용(비디오)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
* [AEM Forms와 Adobe Sign 통합](../../forms/using/adobe-sign-integration-adaptive-forms.md)

