---
title: Adobe Sign과 AEM Forms 통합
seo-title: Adobe Sign과 AEM Forms 통합
description: AEM Forms용 Adobe Sign 구성 방법 알아보기
seo-description: AEM Forms용 Adobe Sign 구성 방법 알아보기
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: 응용 Forms, Adobe Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---

# [!DNL Adobe Sign]을 AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}과 통합

[!DNL Adobe Sign] 적응형 양식을 위해 전자 서명 워크플로우를 활성화합니다. 전자 서명은 법률, 영업, 급여, 인적 자원 관리 및 기타 여러 분야에 대한 문서를 처리하기 위한 워크플로우를 개선합니다.

일반적인 [!DNL Adobe Sign] 및 적응형 양식 시나리오에서 사용자는 적응형 양식을 작성하여 **서비스**&#x200B;에 적용합니다. 예를 들어, 신용카드 신청서와 시민 혜택 양식입니다. 사용자가 애플리케이션 양식을 작성, 제출 및 서명하면 추가 작업을 위해 양식이 서비스 공급자에게 전송됩니다. 서비스 공급자는 애플리케이션을 검토하고 [!DNL Adobe Sign] 을 사용하여 승인된 애플리케이션을 표시합니다. 유사한 전자 서명 워크플로우를 활성화하려면 [!DNL Adobe Sign]을 AEM [!DNL Forms]과 통합할 수 있습니다.

AEM [!DNL Forms]과 함께 [!DNL Adobe Sign]을 사용하려면 AEM 클라우드 서비스에서 [!DNL Adobe Sign]를 구성하십시오.

## 전제 조건 {#prerequisites}

[!DNL Adobe Sign]을 AEM [!DNL Forms]과 통합하려면 다음 항목이 필요합니다.

* 활성 [Adobe Sign 개발자 계정입니다.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* [SSL이 활성화됨](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms] 서버.
* [Adobe Sign API 애플리케이션](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)
* [!DNL Adobe Sign] API 응용 프로그램의 자격 증명(클라이언트 ID 및 클라이언트 암호).
* 다시 구성할 때 작성자 및 게시 인스턴스 모두에서 기존 [!DNL Adobe Sign] 구성을 제거합니다.
* 작성자 및 게시 인스턴스에 대해 [동일한 암호화 키](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)를 사용하십시오.

## AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}로 [!DNL Adobe Sign] 구성

사전 요구 사항이 준비되면 다음 단계를 수행하여 작성자 인스턴스에서 AEM [!DNL Forms]을 사용하여 [!DNL Adobe Sign]을 구성합니다.

1. AEM [!DNL Forms] 작성자 인스턴스에서 **도구** ![햄머](assets/hammer.png) > **[!UICONTROL 일반]** > **[!UICONTROL 구성 브라우저]**&#x200B;로 이동합니다.
1. **[!UICONTROL 구성 브라우저]** 페이지에서 **[!UICONTROL 만들기]**&#x200B;를 탭합니다.
   * 자세한 내용은 [구성 브라우저](/help/sites-administering/configurations.md) 설명서를 참조하십시오.
1. **[!UICONTROL 구성 만들기]** 대화 상자에서 구성에 대해 **[!UICONTROL 제목]**&#x200B;을 지정하고, **[!UICONTROL 클라우드 구성]**&#x200B;을 사용하도록 설정하고 **[!UICONTROL 만들기]**&#x200B;를 탭합니다. 클라우드 서비스용 구성 컨테이너를 만듭니다.
1. **도구** ![햄머](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**&#x200B;로 이동하여 위의 단계에서 만든 구성 컨테이너를 선택합니다.

   >[!NOTE]
   >
   >1-4단계를 실행하여 새 구성 컨테이너를 만들고 컨테이너에 [!DNL Adobe Sign] 구성을 만들거나 **도구** ![햄머](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**&#x200B;에서 기존 `global` 폴더를 사용할 수 있습니다. 새 구성 컨테이너에서 구성을 만드는 경우 적응형 양식을 만들 때 **[!UICONTROL 구성 컨테이너]** 필드에 컨테이너 이름을 지정해야 합니다.

   >[!NOTE]
   클라우드 서비스 구성 페이지의 URL이 **HTTPS**&#x200B;로 시작하는지 확인합니다. 없는 경우 [AEM [!DNL Forms] 서버에 대해 SSL](/help/sites-administering/ssl-by-default.md)을 활성화합니다.

1. 구성 페이지에서 **[!UICONTROL 만들기]**&#x200B;를 탭하여 AEM [!DNL Forms]에서 [!DNL Adobe Sign] 구성을 만듭니다.
1. **[!UICONTROL Adobe Sign 구성 만들기]** 페이지의 **[!UICONTROL 일반]** 탭에서 구성에 대해 **[!UICONTROL 이름]**&#x200B;을 지정하고 **[!UICONTROL 다음]**&#x200B;을 탭합니다. 원하는 경우 제목을 지정하고 구성 축소판을 찾아 선택할 수 있습니다.

1. 현재 브라우저 창의 URL을 메모장에 복사합니다. AEM[!DNL Forms]을 사용하여 [!DNL Adobe Sign] 응용 프로그램을 구성해야 합니다.

1. [!DNL Adobe Sign] 응용 프로그램에 대한 OAuth 설정을 구성합니다.

   1. 브라우저 창을 열고 [!DNL Adobe Sign] 개발자 계정에 로그인합니다.
   1. AEM [!DNL Forms]에 대해 구성된 응용 프로그램을 선택하고 **[!UICONTROL Configure OAuth for Application]**&#x200B;을(를) 탭합니다.
   1. **[!UICONTROL 클라이언트 ID]** 및 **[!UICONTROL 클라이언트 암호]**&#x200B;를 메모장에 복사합니다.
   1. **[!UICONTROL 리디렉션 URL]** 상자에서 이전 단계에서 복사한 HTTPS URL을 추가합니다.
   1. [!DNL Adobe Sign] 응용 프로그램에 대해 다음 OAuth 설정을 사용하도록 설정하고 **[!UICONTROL 저장]**&#x200B;을 클릭합니다.
   * aggregation_read
   * aggregation_write
   * aggregation_send
   * widget_write
   * workflow_read

   [!DNL Adobe Sign] 애플리케이션에 대한 OAuth 설정을 구성하고 키를 가져오는 단계별 정보는 [애플리케이션](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) 개발자 설명서에 대한 oAuth 설정 구성 을 참조하십시오.

   ![OAuth 구성](assets/oauthconfig_new.png)

1. **[!UICONTROL Adobe Sign 구성 만들기]** 페이지로 돌아갑니다. **[!UICONTROL 설정]** 탭에서 **[!UICONTROL OAuth URL]** 필드에 다음 기본 URL이 표시됩니다.

   https://secure.na1.echosign.com/public/oauth

   위치:

   **na1** 은 기본 데이터베이스 공유 항목을 나타냅니다.

   데이터베이스 공유 값에 대한 값을 수정할 수 있습니다. 데이터베이스 공유 값을 사용할 수 있도록 서버를 다시 시작합니다.

   >[!NOTE]
   작성자 및 게시 인스턴스 구성이 동일한 공유 항목을 가리키는지 확인합니다. 조직에 대해 여러 Adobe Sign 구성을 만드는 경우 모든 구성이 동일한 샤드를 활용하는지 확인하십시오.

1. 8단계에서 작성된 **클라이언트 ID**(응용 프로그램 ID라고도 함) 및 **클라이언트 암호**&#x200B;를 지정합니다. 적응형 양식에 첨부된 파일을 서명을 위해 전송된 해당 [!DNL Adobe Sign] 문서에 추가하려면 **[!UICONTROL 첨부 파일용 Adobe Sign 활성화]** 옵션을 선택합니다.

   **[!UICONTROL Adobe Sign에 연결]**&#x200B;을 누릅니다. 자격 증명을 입력하라는 메시지가 표시되면 [!DNL Adobe Sign] 응용 프로그램을 만드는 동안 사용되는 계정의 사용자 이름과 암호를 입력합니다.

   **[!UICONTROL 만들기]**&#x200B;를 탭하여 [!DNL Adobe Sign] 구성을 만듭니다.

1. AEM 웹 콘솔을 엽니다. URL은 `https://'[server]:[port]'/system/console/configMgr`입니다.
1. **[!UICONTROL Forms 일반 구성 서비스]를 엽니다.**
1. **[!UICONTROL 허용]** 필드에서 **모든 사용자 선택** - 익명 또는 로그인한 모든 사용자는 첨부 파일을 미리 보고 양식을 확인하고 서명할 수 있으며 **[!UICONTROL 저장]을 클릭합니다.** 작성자 인스턴스가 를 사용하도록 구성되어 있습니다  [!DNL Adobe Sign].
1. 구성을 게시합니다.
1. 해당 게시 인스턴스에 동일한 구성을 만들려면 [replication](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html)을 사용하십시오.

이제 [!DNL Adobe Sign]은(는) AEM [!DNL Forms]에 통합되어 적응형 양식에 사용할 수 있습니다. [적응형 양식](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)에서 Adobe Sign 서비스를 사용하려면 적응형 양식 속성에서 위에 만든 구성 컨테이너를 지정하십시오.



## 서명 상태 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}를 동기화하도록 [!DNL Adobe Sign] 스케줄러를 구성합니다

모든 서명자가 서명 프로세스를 완료한 후에만 [!DNL Adobe Sign] 활성화된 적응형 양식이 제출됩니다. 기본적으로 [!DNL Adobe Sign] 스케줄러 서비스는 24시간마다 후에 서명자 응답을 확인(폴링)하도록 예약됩니다. 환경의 기본 간격을 변경할 수 있습니다. 기본 간격을 변경하려면 다음 단계를 수행하십시오.

1. 관리자 자격 증명을 사용하여 AEM [!DNL Forms] 서버에 로그인하고 **도구** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**&#x200B;로 이동합니다.

   브라우저 창에서 다음 URL을 열 수도 있습니다.
   `https://[localhost]:'port'/system/console/configMgr`

1. **[!UICONTROL Adobe Sign 구성 서비스]** 옵션을 찾아 엽니다. **[!UICONTROL 상태 업데이트 스케줄러 표현식]** 필드에 [콘 표현식](https://en.wikipedia.org/wiki/Cron#CRON_expression)을 지정하고 **[!UICONTROL 저장]**&#x200B;을 클릭합니다. 예를 들어, 매일 오전 00:00에 구성 서비스를 실행하려면 **[!UICONTROL 상태 업데이트 스케줄러 표현식]** 필드에 `0 0 0 1/1 * ? *`을 지정합니다.

이제 [!DNL Adobe Sign] 의 동기화 상태에 대한 기본 간격이 변경되었습니다.

## 관련 문서 {#related-articles}

* [적응형 양식에서 Adobe Sign 사용](../../forms/using/working-with-adobe-sign.md)
* [AEM Forms에서 Adobe Sign 사용(비디오)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
