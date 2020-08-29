---
title: Adobe Sign과 AEM Forms 통합
seo-title: Adobe Sign과 AEM Forms 통합
description: AEM Forms용 Adobe Sign 구성 방법 살펴보기
seo-description: AEM Forms용 Adobe Sign 구성 방법 살펴보기
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
translation-type: tm+mt
source-git-commit: 2e5cf93eb3ce47b65298b8de13c7d874d1989073
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---


# Adobe Sign과 AEM Forms 통합{#integrate-adobe-sign-with-aem-forms}

Adobe Sign을 사용하면 적응형 양식에 전자 서명 워크플로우를 적용할 수 있습니다. 전자 서명을 사용하면 법률, 영업, 급여, 인사 관리 등 다양한 영역에서 문서를 처리할 수 있는 워크플로우를 향상시킬 수 있습니다.

일반적인 Adobe Sign 및 적응형 양식 시나리오에서 사용자는 적응형 양식을 채워 서비스에 **적용합니다**. 예를 들어 신용 카드 신청서와 시민 혜택 양식입니다. 사용자가 응용 프로그램 양식을 채우고 제출하고 서명하면 추가 작업을 위해 서비스 제공업체에 양식이 전송됩니다. 서비스 제공업체는 애플리케이션을 검토하고 Adobe Sign을 사용하여 승인된 애플리케이션을 표시합니다. 유사한 전자 서명 워크플로우를 사용하려면 Adobe Sign을 AEM Forms과 통합할 수 있습니다.

AEM Forms과 함께 Adobe Sign을 사용하려면 AEM Cloud 서비스에서 Adobe Sign을 구성하십시오.

## 전제 조건 {#prerequisites}

Adobe Sign을 AEM Forms과 통합하려면 다음이 필요합니다.

* 활성 [Adobe Sign 개발자 계정.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* SSL이 [활성화된](/help/sites-administering/ssl-by-default.md) AEM Forms 서버
* Adobe Sign [API 애플리케이션입니다](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Adobe Sign API 응용 프로그램의 자격 증명(클라이언트 ID 및 클라이언트 암호).
* 다시 구성할 때 작성자 및 게시 인스턴스 모두에서 기존 Adobe Sign 구성을 제거합니다.
* 작성 및 게시 인스턴스에 [동일한 암호화](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) 키를 사용합니다.

## AEM Forms과 Adobe Sign 구성 {#configure-adobe-sign-with-aem-forms}

사전 요구 사항이 준비되면 작성자 인스턴스에서 AEM Forms을 사용하여 Adobe Sign을 구성하려면 다음 단계를 수행하십시오.

1. AEM Forms 작성자 인스턴스의 경우 **도구** > ![일반](assets/hammer.png)********> 구성 브라우저를탐색합니다.
1. 구성 **[!UICONTROL 브라우저]** 페이지에서 만들기를 **[!UICONTROL 누릅니다]**.
1. 구성 **[!UICONTROL 만들기 대화]** 상자에서 구성에 대한 **[!UICONTROL 제목]** 을 지정하고 **[!UICONTROL 클라우드 구성]**&#x200B;을 활성화하고 **[!UICONTROL , Create]** Publishing을 누릅니다. 클라우드 서비스를 위한 구성 컨테이너를 만듭니다.
1. 도구 **망치**![>](assets/hammer.png) Cloud Services **>** Adobe Sign **** 로 이동하고 위 단계에서 생성한 구성 컨테이너를 선택합니다.

   >[!NOTE]
   >
   >클라우드 서비스 구성 페이지의 URL이 **HTTPS로 시작되는지 확인하십시오**. 그렇지 않은 경우 AEM Forms 서버에 대해 [SSL을](/help/sites-administering/ssl-by-default.md) 활성화합니다.

1. 구성 페이지에서 만들기 **[!UICONTROL 를]** 눌러 AEM Forms에서 Adobe Sign 구성을 만듭니다.
1. Adobe Sign 구성 **** 생성 **[!UICONTROL 페이지의]** 일반 **** 탭에서 구성에 **대한**&#x200B;이름을 지정하고Next을누릅니다. 원하는 경우 제목을 지정하고 원하는 대로 이동하여 구성에 대한 축소판을 선택할 수 있습니다.

1. 현재 브라우저 창의 URL을 메모장으로 복사합니다. AEM Forms으로 Adobe Sign 애플리케이션을 구성해야 합니다.

1. Adobe Sign 응용 프로그램의 OAuth 설정을 구성합니다.

   1. 브라우저 창을 열고 Adobe Sign 개발자 계정에 로그인합니다.
   1. AEM Forms에 대해 구성된 응용 프로그램을 선택하고 응용 프로그램에 대한 OAuth 구성을 누릅니다.
   1. 리디렉션 URL **** 상자에서 이전 단계에서 복사한 HTTPS URL을 추가하고 **저장을 클릭합니다**.
   1. Adobe Sign 응용 프로그램에 대해 다음 OAuth 설정을 활성화하고 **저장을 클릭합니다**.
   * aggregation_read
   * aggregation_write
   * aggregation_send
   * widget_write
   * workflow_read

   Adobe Sign 응용 프로그램에 대한 OAuth 설정을 구성하고 키를 획득하기 위한 단계별 정보는 응용 프로그램 [개발자 설명서에 대한](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) Auth 설정 구성을 참조하십시오.

   ![OAuth 구성](assets/oauthconfig_new.png)

1. Adobe Sign 구성 **만들기 페이지로** 돌아갑니다. 설정 **[!UICONTROL 탭]** 에서 **[!UICONTROL OAuth URL]** 필드에는 다음 기본 URL이 언급됩니다.

   https://secure.na1.echosign.com/public/oauth

   where:

   **na1** is the default database shared.

   데이터베이스 공유 값을 수정할 수 있습니다. 데이터베이스 공유 값에 새 값을 사용할 수 있도록 서버를 다시 시작합니다.

1. 클라이언트 **ID** (응용 프로그램 ID라고도 함)와 클라이언트 암호를 **지정합니다**. 첨부 파일에 **Adobe Sign 활성화 옵션을 선택하여 서명을 위해 보낸 해당 Adobe Sign 문서에 적응형 양식에 첨부된 파일을 첨부합니다** .

   Tap **[!UICONTROL Connect to Adobe Sign]**. 자격 증명을 입력하라는 메시지가 표시되면 Adobe Sign 응용 프로그램을 만드는 동안 사용된 계정의 사용자 이름과 암호를 입력합니다.

   만들기 **[!UICONTROL 를]** 눌러 Adobe Sign 구성을 만듭니다.

1. AEM 웹 콘솔을 엽니다. URL은 `https://'[server]:[port]'/system/console/configMgr`
1. Forms **일반 구성 서비스를 엽니다.**
1. 허용 **필드에서 모든 사용자** - 익명 또는 로그인한 모든 사용자가 첨부 파일을 미리 보고 양식을 확인 및 서명하고 **저장을 클릭합니다** **.** 작성자 인스턴스가 Adobe Sign을 사용하도록 구성되어 있습니다.
1. 구성을 게시합니다.
1. 복제 [를](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html) 사용하여 해당 게시 인스턴스에 동일한 구성을 만듭니다.

이제 Adobe Sign은 AEM Forms과 통합되어 적응형 양식으로 사용할 수 있습니다. 적응형 양식에서 Adobe Sign 서비스를 [사용하려면 위에 만든 구성 컨테이너를 적응형 양식](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)속성으로 지정합니다.



## 서명 상태를 동기화하도록 Adobe Sign 스케줄러 구성 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Adobe Sign 지원 적응형 양식은 모든 서명자가 서명 프로세스를 완료한 후에만 제출됩니다. 기본적으로 Adobe Sign 스케줄러 서비스는 24시간마다 후에 서명자 응답을 확인(투표)할 예정입니다. 환경에 대한 기본 간격을 변경할 수 있습니다. 기본 간격을 변경하려면 다음 단계를 수행하십시오.

1. 관리 자격 증명을 사용하여 AEM Forms 서버에 로그인하고 **도구** > 작업 **>** 웹 콘솔 **로**&#x200B;이동합니다.

   브라우저 창에서 다음 URL을 열 수도 있습니다.
   `https://[localhost]:'port'/system/console/configMgr`

1. Adobe Sign 구성 서비스 **옵션을 찾아** 엽니다. 상태 업데이트 스케줄러 [표현식](https://en.wikipedia.org/wiki/Cron#CRON_expression) 필드에 **cron 표현식을** 지정하고 저장을 **클릭합니다**. 예를 들어 오전 00:00에 구성 서비스를 매일 실행하려면 [상태 업데이트 스케줄러 표현식] 필드 `0 0 0 1/1 * ? *` 에서 **지정합니다** .

이제 Adobe Sign의 동기화 상태에 대한 기본 간격이 변경되었습니다.

## 관련 문서 {#related-articles}

* [적응형 양식에서 Adobe Sign 사용](../../forms/using/working-with-adobe-sign.md)
* [Adobe Sign과 AEM Forms 사용(비디오)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
* [Adobe Sign과 AEM Forms 통합](../../forms/using/adobe-sign-integration-adaptive-forms.md)

