---
title: Adobe Sign과 AEM Forms 통합
seo-title: Integrate Adobe Sign with AEM Forms
description: AEM Forms용 Adobe Sign 구성 방법 알아보기
seo-description: Learn how to configure Adobe Sign for AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: Adaptive Forms, Adobe Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
source-git-commit: e46d77caf831324f077315df43b8f3a0267bef9a
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 25%

---

# 통합 [!DNL Adobe Sign] AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] 적응형 양식을 위해 전자 서명 워크플로우를 활성화합니다. 전자 서명은 법무, 판매, 임금, 인적 자원 관리 등의 다양한 분야에서 문서를 처리하는 워크플로를 개선합니다.

일반적인 [!DNL Adobe Sign] 및 적응형 양식 시나리오는 사용자가 적응형 양식을 **서비스 신청**. 신용 카드 신청 양식과 시민 혜택 양식을 예로 들 수 있습니다. 사용자가 신청 양식에 정보를 입력하고 이를 제출한 뒤 서명하면, 이후의 액션이 가능하도록 양식이 서비스 제공자에게 전달됩니다. 서비스 제공자는 신청서를 검토하고 [!DNL Adobe Sign]을 사용해 신청을 승인된 것으로 표시합니다. 유사한 전자 서명 워크플로우를 사용하려면 다음을 통합할 수 있습니다 [!DNL Adobe Sign] AEM [!DNL Forms].

를 사용하려면 [!DNL Adobe Sign] AEM [!DNL Forms], 구성 [!DNL Adobe Sign] AEM 클라우드 서비스에서:

## 사전 요구 사항 {#prerequisites}

통합하려면 다음을 수행해야 합니다 [!DNL Adobe Sign] AEM [!DNL Forms]:

* 활성 [Adobe Sign 개발자 계정.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* An [SSL 활성화](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms] server.
* [Adobe Sign API 애플리케이션](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* [!DNL Adobe Sign] API 애플리케이션의 자격 증명(클라이언트 ID 및 클라이언트 보안).
* 다시 구성할 때 기존 [!DNL Adobe Sign] 작성자 및 게시 인스턴스 둘 다의 구성입니다.
* 작성자에 대해 [동일한 암호 키](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)를 사용하고 인스턴스를 게시합니다.

## 구성 [!DNL Adobe Sign] AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

사전 요구 사항이 준비되면 다음 단계를 수행하여 을 구성합니다 [!DNL Adobe Sign] AEM [!DNL Forms] 작성자 인스턴스에서:

1. AEM에서 [!DNL Forms] 작성자 인스턴스, 탐색 **도구** ![망치](assets/hammer.png) > **[!UICONTROL 일반]** > **[!UICONTROL 구성 브라우저]**.
1. 설정 **[!UICONTROL 구성 브라우저]** 페이지, 탭 **[!UICONTROL 만들기]**.
   * 자세한 내용은 [구성 브라우저](/help/sites-administering/configurations.md) 설명서 를 참조하십시오.
1. 에서 **[!UICONTROL 구성 만들기]** 대화 상자에서 다음을 지정합니다 **[!UICONTROL 제목]** 구성에 대해 **[!UICONTROL 클라우드 구성]**, 탭 **[!UICONTROL 만들기]**. 클라우드 서비스용 구성 컨테이너를 만듭니다.
1. 다음으로 이동 **도구** ![망치](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** 및 위의 단계에서 만든 구성 컨테이너를 선택합니다.

   >[!NOTE]
   >
   >1-4단계를 실행하여 새 구성 컨테이너를 만들고 [!DNL Adobe Sign] 컨테이너에서 구성 또는 기존 `global` 폴더 **도구** ![망치](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. 새 구성 컨테이너에서 구성을 만드는 경우 **[!UICONTROL 구성 컨테이너]** 적응형 양식을 만들 때 필드를 추가합니다.

   >[!NOTE]
   클라우드 서비스 구성 페이지의 URL이 **HTTPS**. 그렇지 않으면, [ssl 활성화](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms] server.

1. 구성 페이지에서 **[!UICONTROL 만들기]** 만들기 [!DNL Adobe Sign] AEM의 구성 [!DNL Forms].
1. 에서 **[!UICONTROL 일반]** 의 탭 **[!UICONTROL Adobe Sign 구성 만들기]** 페이지에서, **[!UICONTROL 이름]** 를 사용하려면 를 탭하고 **[!UICONTROL 다음]**. 원하는 경우 제목을 지정하고 구성 축소판을 찾아 선택할 수 있습니다.

1. 현재 브라우저 창의 URL을 메모장에 복사합니다. 를 구성해야 합니다 [!DNL Adobe Sign] AEM을 사용한 애플리케이션[!DNL Forms].

1. 에서 **[!UICONTROL 설정]** 탭, **[!UICONTROL OAuth URL]** 필드에 기본 URL이 포함되어 있습니다. URL 형식은 다음과 같습니다.

   `https://<shard>/public/oAuth/v2`

   예:
   `https://secure.na1.echosign.com/public/oauth/v2`

   여기에서

   **na1**&#x200B;은 기본값 데이터베이스 분할을 의미합니다. 데이터베이스 분할의 값을 수정할 수 있습니다. [!DNL  Adobe Sign] 클라우드 구성이 [올바른 분할](https://helpx.adobe.com/sign/using/identify-account-shard.html)을 가리켜야 합니다.

   Adobe Experience Manager 기능이나 구성 요소에 대한 또 다른 [!DNL Adobe Sign] 구성을 생성하는 경우, 모든 [!DNL Adobe Sign] 클라우드 구성이 동일한 분할을 가리켜야 합니다.

   >[!NOTE]
   유지 **Adobe Sign 구성 만들기** 페이지를 엽니다. 닫지 마세요. 검색할 수 있습니다 **클라이언트 Id** 및 **클라이언트 암호** 및에 대한 OAuth 설정 구성 후 [!DNL Adobe Sign] 향후 단계에 설명된 대로 응용 프로그램을 사용할 수 있습니다.


1. [!DNL Adobe Sign] 애플리케이션에 대한 OAuth 설정을 구성합니다.

   1. 브라우저 창을 열고 [!DNL Adobe Sign] 개발자 계정.
   1. AEM용으로 구성된 응용 프로그램을 선택합니다 [!DNL Forms], 탭 **[!UICONTROL 애플리케이션에 대한 OAuth 구성]**.
   1. 를 복사합니다. **[!UICONTROL 클라이언트 ID]** 및 **[!UICONTROL 클라이언트 암호]** 메모장에 넣을 수 있습니다.
   1. 에서 **[!UICONTROL 리디렉션 URL]** 상자를 열고 이전 단계에서 복사한 HTTPS URL을 추가합니다.
   1. 에 대해 다음 OAuth 설정을 사용하도록 설정합니다. [!DNL Adobe Sign] 응용 프로그램을 클릭하고 **[!UICONTROL 저장]**.
   * aggregation_read
   * aggregation_write
   * aggregation_send
   * widget_write
   * workflow_read

   [!DNL Adobe Sign] 애플리케이션에 대한 OAuth 설정을 구성하고 키를 얻는 방법에 대한 단계별 정보는 [애플리케이션에 대한 oAuth 설정 구성](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) 개발자 문서를 참조하십시오.

   ![OAuth Config](assets/oauthconfig_new.png)

1. 로 돌아갑니다. **[!UICONTROL Adobe Sign 구성 만들기]** 페이지. 에서 **[!UICONTROL 설정]** 탭, **[!UICONTROL OAuth URL]** 필드에 기본 URL이 설명되어 있습니다. URL 형식은 다음과 같습니다.

   `https://<shard>/public/oAuth/v2`

   예:
   `https://secure.na1.echosign.com/public/oauth/v2`

   여기에서

   **na1**&#x200B;은 기본값 데이터베이스 분할을 의미합니다.

   데이터베이스 분할의 값을 수정할 수 있습니다. 데이터베이스 공유 값을 사용할 수 있도록 서버를 다시 시작합니다.

   >[!NOTE]
   작성자 및 게시 인스턴스 구성이 동일한 공유 항목을 가리키는지 확인합니다. 조직에 대해 여러 Adobe Sign 구성을 만드는 경우 모든 구성이 동일한 샤드를 활용하는지 확인하십시오.

1. 로 돌아갑니다. **[!UICONTROL Adobe Sign 구성 만들기]** 페이지. 에서 **[!UICONTROL 설정]** 탭에서 다음을 지정합니다 **클라이언트 ID** (응용 프로그램 ID라고도 함) 및 **클라이언트 암호**. 를 사용하십시오 [Adobe Sign 애플리케이션의 클라이언트 ID 및 클라이언트 암호](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) AEM Forms용으로 만들어졌습니다.

1. 을(를) 선택합니다 **[!UICONTROL 첨부 파일용 Adobe Sign을 사용할 수도 있습니다]** 적응형 양식에 첨부된 파일을 해당 양식에 추가 옵션 [!DNL Adobe Sign] 서명을 위해 문서를 보냈습니다.

1. 탭 **[!UICONTROL Adobe Sign에 연결]**. 자격 증명을 입력하라는 메시지가 뜨면 [!DNL Adobe Sign] 애플리케이션 생성 시 사용한 계정의 사용자 이름과 비밀번호를 입력합니다.

1. 탭 **[!UICONTROL 만들기]** 를 클릭하여 [!DNL Adobe Sign] 구성.

1. AEM 웹 콘솔을 엽니다. URL은 `https://'[server]:[port]'/system/console/configMgr`
1. 열기 **[!UICONTROL Forms 일반 구성 서비스].**
1. 에서 **[!UICONTROL 허용]** 필드, **선택** 모든 사용자 - 익명 또는 로그인한 모든 사용자는 첨부 파일을 미리 보고, 양식을 확인 및 서명하고, **[!UICONTROL 저장].** 작성자 인스턴스가 을 사용하도록 구성되었습니다 [!DNL Adobe Sign].
1. 구성을 게시합니다.
1. 사용 [복제](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html) 해당 게시 인스턴스에 동일한 구성을 만들려면

자, [!DNL Adobe Sign] 는 AEM과 통합됩니다 [!DNL Forms] 적응형 양식에 사용할 수 있습니다. 종료 [적응형 양식에서 Adobe Sign 서비스 사용](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)적응형 양식 속성에서 위에 만든 구성 컨테이너를 지정합니다.



## 구성 [!DNL Adobe Sign] 서명 상태를 동기화할 스케줄러 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

An [!DNL Adobe Sign] 활성화된 적응형 양식은 모든 서명자가 서명 프로세스를 완료한 후에만 제출됩니다. 기본적으로 [!DNL Adobe Sign] 스케줄러 서비스는 24시간마다 후에 (폴링) 서명자 응답을 확인하도록 예약됩니다. 해당 환경에 맞게 기본값 간격을 변경할 수 있습니다. 기본 간격을 변경하려면 다음 단계를 수행하십시오.

1. AEM에 로그인 [!DNL Forms] 관리 자격 증명이 있는 서버 및 **도구** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**.

   브라우저 창에서 다음 URL을 열 수도 있습니다.
   `https://[localhost]:'port'/system/console/configMgr`

1. 을(를) 찾아 엽니다. **[!UICONTROL Adobe Sign 구성 서비스]** 선택 사항입니다. 을(를) 지정합니다 [cron 식](https://en.wikipedia.org/wiki/Cron#CRON_expression) 에서 **[!UICONTROL 상태 업데이트 스케줄러 표현식]** 필드를 입력하고 **[!UICONTROL 저장]**. 예를 들어 매일 오전 00:00에 구성 서비스를 실행하려면 `0 0 0 1/1 * ? *` 에서 **[!UICONTROL 상태 업데이트 스케줄러 표현식]** 필드.

동기화 상태에 대한 기본 간격 [!DNL Adobe Sign] 이제 가 변경되었습니다.

## 관련 문서 {#related-articles}

* [적응형 양식에서 Adobe Sign 사용](../../forms/using/working-with-adobe-sign.md)
* [AEM Forms에서 Adobe Sign 사용(비디오)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
