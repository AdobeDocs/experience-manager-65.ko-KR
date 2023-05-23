---
title: 이메일 마케팅
seo-title: E-mail Marketing
description: '이메일 마케팅(예: 뉴스레터)은 콘텐츠를 리드에 푸시하는 데 사용하는 마케팅 캠페인의 중요한 부분입니다. AEM에서는 기존 AEM 콘텐츠에서 뉴스레터를 생성하고 뉴스레터에만 해당하는 새 콘텐츠를 추가할 수 있습니다.'
seo-description: E-mail marketing (for example, newsletters) are an important part of any marketing campaign as you use them to push content to your leads. In AEM, you can create newsletters from existing AEM content as well as add new content, specific to the newsletters.
uuid: 565943bf-fe37-4d5c-98c3-7c629c4ba264
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 69ca5acb-83f9-4e1b-9639-ec305779c931
docset: aem65
exl-id: a1d8b74e-67eb-4338-9e8e-fd693b1dbd48
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 1%

---

# 이메일 마케팅{#e-mail-marketing}

>[!NOTE]
>
>Adobe은 AEM SMTP 서비스에서 보낸 열기/바운스(배달할 수 없음) 전자 메일 추적을 더 강화하지 않을 계획입니다.
>권장 사항은 다음과 같습니다 [Adobe Campaign 및 AEM에 통합 활용](/help/sites-administering/campaign.md).

이메일 마케팅(예: 뉴스레터)은 콘텐츠를 리드에 푸시하는 데 사용하는 마케팅 캠페인의 중요한 부분입니다. AEM에서는 기존 AEM 콘텐츠에서 뉴스레터를 생성하고 뉴스레터에만 해당하는 새 콘텐츠를 추가할 수 있습니다.

뉴스레터가 생성되면 즉시 또는 예약된 다른 시간에(워크플로우를 통해) 특정 사용자 그룹에 뉴스레터를 전송할 수 있습니다. 또한 사용자는 원하는 형식으로 뉴스레터를 구독할 수 있습니다.

또한 AEM을 사용하여 항목 유지 관리, 뉴스레터 보관 및 뉴스레터 통계 보기를 비롯한 뉴스레터 기능을 관리할 수 있습니다.

>[!NOTE]
>
>Geometrixx에서 뉴스레터 템플릿이 이메일 편집기를 자동으로 엽니다. 전자 메일을 보낼 다른 템플릿(예: 초대)에서 전자 메일 편집기를 사용할 수 있습니다. 페이지가 상속될 때마다 이메일 편집기가 표시됩니다 **mcm/components/newsletter/page**.

이 문서에서는 AEM에서 뉴스레터를 작성하는 기본 사항에 대해 설명합니다. 이메일 마케팅 작업 방법에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [효과적인 뉴스레터 랜딩 페이지 만들기](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-landingpage.md)
* [구독 관리](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-subscriptions.md)
* [이메일 서비스 공급자에 이메일 게시](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-newsletters.md)
* [반송된 이메일 추적](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-tracking-bounces.md)

>[!NOTE]
>
>이메일 공급자를 업데이트하거나 플라이트 테스트를 수행하거나 뉴스레터를 전송하는 경우 뉴스레터가 게시 인스턴스에 먼저 게시되지 않았거나 게시 인스턴스를 사용할 수 없는 경우 이러한 작업이 실패합니다. 뉴스레터를 게시하고 게시 인스턴스가 실행 중인지 확인하십시오.

## 뉴스레터 경험 만들기 {#creating-a-newsletter-experience}

>[!NOTE]
>
>이메일 알림은 osgi 구성을 통해 구성해야 합니다. 다음을 참조하십시오 [이메일 알림을 구성하는 중입니다.](/help/sites-administering/notification.md)

1. 왼쪽 창에서 새 캠페인을 선택하거나 오른쪽 창에서 새 캠페인을 두 번 클릭합니다.

1. 아이콘을 사용하여 목록 보기를 선택합니다.

   ![](do-not-localize/mcm_icon_listview-1.png)

1. 클릭 **새로 만들기...**

   다음을 지정할 수 있습니다. **제목**, **이름** 생성할 경험 유형(이 경우 뉴스레터)입니다.

   ![mcm_createnewsleter](assets/mcm_createnewsletter.png)

1. **만들기**&#x200B;를 클릭합니다.

1. 새 대화 상자가 즉시 열립니다. 여기에서 뉴스레터의 속성을 입력할 수 있습니다.

   다음 **기본 수신자 목록** 뉴스레터의 터치포인트를 형성하므로 필수 필드입니다( 참조). [목록 작업](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists) 목록)에 대한 자세한 내용을 참조하십시오.

   ![mcm_newsletterdialog](assets/mcm_newnewsletterdialog.png)

   * **보낸 사람 이름**
뉴스레터 발송자로 표시되는 이름입니다.

   * **보낸 주소**
뉴스레터 발송자로 표시되는 메일 주소입니다.

   * **제목**
뉴스레터의 제목입니다.

   * **회신 대상**
발송된 뉴스레터에 대해 회신 가능한 메일 주소입니다.

   * **설명**
뉴스레터에 대한 설명.

   * **정시**
뉴스레터 전송 정시.

   * **기본 수신자 목록**
뉴스레터를 수신할 기본 목록입니다.
   이러한 수정 사항은 의 이후 단계에서 업데이트할 수 있습니다. **속성...** 대화 상자.

1. 클릭 **확인** 저장.

## 뉴스레터에 콘텐츠 추가 {#adding-content-to-newsletters}

AEM 구성 요소에서처럼 뉴스레터에 다이내믹 콘텐츠를 포함한 콘텐츠를 추가할 수 있습니다. Geometrixx에서 뉴스레터 템플릿에는 뉴스레터의 콘텐츠를 추가 및 수정하는 데 사용할 수 있는 특정 구성 요소가 있습니다.

1. MCM에서 **캠페인** 콘텐츠를 추가하거나 편집할 뉴스레터를 탭하고 두 번 클릭합니다. 뉴스레터가 열립니다.

1. 구성 요소가 표시되지 않으면 디자인 보기로 이동하여 필요한 구성 요소(예: 뉴스레터 구성 요소)를 활성화한 후 편집을 시작합니다.
1. 새 텍스트, 이미지 또는 기타 구성 요소를 적절히 입력합니다. 이 Geometrixx 예에서는 텍스트, 이미지, 제목, 2열 등 4가지 구성 요소를 사용할 수 있습니다. 뉴스레터에는 설정 방법에 따라 더 많거나 적은 구성 요소가 있을 수 있습니다.

   >[!NOTE]
   >
   >변수를 사용하여 뉴스레터를 개인화할 수 있습니다. Geometrixx 뉴스레터에서 텍스트 구성 요소에서 변수를 사용할 수 있습니다. 변수의 값은 사용자 프로필의 정보에서 상속됩니다.

   ![mcm_newsletter_content](assets/mcm_newsletter_content.png)

1. 변수를 삽입하려면 목록에서 변수를 선택하고 **삽입**. 변수는 프로필에서 채워집니다.

## 뉴스레터 개인화 {#personalizing-newsletters}

Geometrixx의 뉴스레터 텍스트 구성 요소에 사전 정의된 변수를 삽입하여 뉴스레터를 개인화할 수 있습니다. 변수의 값은 사용자 프로필의 정보에서 상속됩니다.

클라이언트 컨텍스트를 사용하고 프로필을 로드하여 뉴스레터가 개인화되는 방식을 시뮬레이션할 수도 있습니다.

뉴스레터를 개인화하고 모양을 시뮬레이션하려면 다음 작업을 수행하십시오.

1. MCM에서 설정을 사용자 지정할 뉴스레터를 엽니다.

1. 개인화할 텍스트 구성 요소를 엽니다.

1. 변수를 표시할 위치에 커서를 놓고 드롭다운 목록에서 변수를 선택한 다음 를 클릭합니다 **삽입**. 필요한 수만큼 변수에 대해 이 작업을 수행하고 을 클릭합니다. **확인**.

   ![mcm_newsletter_variables](assets/mcm_newsletter_variables.png)

1. 전송 시 변수가 표시되는 방식을 시뮬레이션하려면 Ctrl+Alt+c를 눌러 클라이언트 컨텍스트를 열고 을 선택합니다 **로드**. 목록에서 로드할 프로필을 가진 사용자를 선택하고 을(를) 클릭합니다 **확인**.

   로드한 프로필의 정보가 변수를 채웠습니다.

   ![mc_newsletter_testvariables](assets/mc_newsletter_testvariables.png)

## 다른 이메일 클라이언트의 뉴스레터 테스트 {#testing-newsletters-in-different-e-mail-clients}

>[!NOTE]
>
>뉴스레터를 전송하기 전에 다음에서 Day CQ 링크 외부화에 대한 OSGi 구성을 확인하십시오. `https://localhost:4502/system/console/configMgr`.
>
>기본적으로 매개 변수의 값은 입니다. `localhost:4502` 실행 중인 인스턴스의 포트가 변경되면 및 작업을 완료할 수 없습니다.

널리 사용되는 여러 이메일 클라이언트에서 뉴스레터가 리드에게 어떻게 표시되는지 시험해 봅니다. 기본적으로 뉴스레터는 선택된 이메일 클라이언트가 없는 상태로 열립니다.

현재 다음 이메일 클라이언트에서 뉴스레터를 볼 수 있습니다.

* Yahoo 메일
* Gmail
* Hotmail
* Thunderbird
* Microsoft Outlook 2007
* Apple 메일

클라이언트 간에 전환하려면 해당 아이콘을 클릭하여 해당 이메일 클라이언트에서 뉴스레터를 확인합니다.

1. MCM에서 설정을 사용자 지정할 뉴스레터를 엽니다.

1. 상단 표시줄에서 이메일 클라이언트를 클릭하여 해당 클라이언트의 뉴스레터 모양을 확인합니다.

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 보려는 추가 이메일 클라이언트에 대해 이 단계를 반복합니다.

   ![chlimage_1-120](assets/chlimage_1-120.png)

## 뉴스레터 설정 사용자 지정 {#customizing-newsletter-settings}

승인된 사용자만 뉴스레터를 전송할 수 있지만 다음을 사용자 정의해야 합니다.

* 제목란을 통해 사용자가 이메일을 열고 뉴스레터가 스팸으로 표시되지 않도록 할 수 있습니다.
* 보낸 사람 주소(예: noreply@geometrixx.com)로 지정된 주소에서 이메일을 받습니다.

뉴스레터 설정을 사용자 지정하려면:

1. MCM에서 설정을 사용자 지정할 뉴스레터를 엽니다.

   ![mcm_newsletter_open](assets/mcm_newsletter_open.png)

1. 뉴스레터 상단에서 **설정**.

   ![mcm_newsletter_settings](assets/mcm_newsletter_settings.png)
1. 다음을 입력합니다. **출처:** 이메일 주소

1. 수정 **제목** 필요한 경우 이메일.

1. 선택 **기본 수신자 목록** 드롭다운 목록에서 선택합니다.

1. **확인**&#x200B;을 클릭합니다.

   뉴스레터를 테스트하거나 전송하면 수신자는 지정된 전자 메일 주소와 제목이 포함된 전자 메일을 받게 됩니다.

## 비행 테스트 뉴스레터 {#flight-testing-newsletters}

비행 테스트는 필수가 아니지만 뉴스레터를 발송하기 전에 원하는 방식으로 나타나는지 테스트해 볼 수 있습니다.

비행 테스트를 통해 다음을 수행할 수 있습니다.

* 에서 뉴스레터 보기 [모든 의도한 클라이언트](#testing-newsletters-in-different-e-mail-clients).
* 메일 서버가 올바르게 설정되었는지 확인합니다.
* 이메일이 스팸으로 플래그가 지정되는지 확인합니다. (수신자 목록에 자신을 포함해야 합니다.)

>[!NOTE]
>
>이메일 공급자를 업데이트하거나 플라이트 테스트를 수행하거나 뉴스레터를 전송하는 경우 뉴스레터가 게시 인스턴스에 먼저 게시되지 않았거나 게시 인스턴스를 사용할 수 없는 경우 이러한 작업이 실패합니다. 뉴스레터를 게시하고 게시 인스턴스가 실행 중인지 확인하십시오.

테스트 뉴스레터를 게재하려면

1. MCM에서 테스트하고 전송할 뉴스레터를 엽니다.

1. 뉴스레터 상단에서 **테스트** 보내기 전에 테스트합니다.

   ![mcm_newsletter_testsettings](assets/mcm_newsletter_testsettings.png)

1. 뉴스레터를 전송할 테스트 메일 주소를 입력하고 **보내기**. 프로파일을 변경하려면 클라이언트 컨텍스트에서 다른 프로파일을 로드합니다. 이렇게 하려면 Ctrl+Alt+C를 누르고 프로파일 로드 및 로드를 선택합니다.

## 뉴스레터 보내기 {#sending-newsletters}

>[!NOTE]
>
>Adobe은 AEM SMTP 서비스에서 보낸 열기/바운스(배달할 수 없음) 전자 메일 추적을 더 강화하지 않을 계획입니다.
>권장 사항은 다음과 같습니다 [Adobe Campaign 및 AEM에 통합 활용](/help/sites-administering/campaign.md).

뉴스레터 또는 목록에서 뉴스레터를 전송할 수 있습니다. 두 절차 모두 설명되어 있습니다.

>[!NOTE]
>
>뉴스레터를 전송하기 전에 다음에서 Day CQ 링크 외부화에 대한 OSGi 구성을 확인하십시오. `https://localhost:4502/system/console/configMgr`.
>
>기본적으로 매개 변수의 값은 입니다. `localhost:4502` 실행 중인 인스턴스의 포트가 변경되면 및 작업을 완료할 수 없습니다.

>[!NOTE]
>
>이메일 공급자를 업데이트하거나 플라이트 테스트를 수행하거나 뉴스레터를 전송하는 경우 뉴스레터가 게시 인스턴스에 먼저 게시되지 않았거나 게시 인스턴스를 사용할 수 없는 경우 이러한 작업이 실패합니다. 뉴스레터를 게시하고 게시 인스턴스가 실행 중인지 확인하십시오.

### 캠페인에서 뉴스레터 보내기 {#sending-newsletters-from-a-campaign}

캠페인 내에서 뉴스레터를 발송하려면 다음 작업을 수행하십시오.

1. MCM에서 전송할 뉴스레터를 엽니다.

   >[!NOTE]
   >
   >발송하기 전에 다음 방법으로 뉴스레터의 제목과 원래 이메일 주소를 사용자 지정했는지 확인하십시오. [설정 사용자 지정](#customizing-newsletter-settings).
   >
   >
   >[비행 테스트](#flight-testing-newsletters) 전송 전 뉴스레터를 사용하는 것이 좋습니다.

1. 뉴스레터 상단에서 **보내기**. 뉴스레터 마법사가 열립니다.

1. 받는 사람 목록에서 뉴스레터를 받을 목록을 선택하고 **다음**.

   ![mcm_newslettersend](assets/mcm_newslettersend.png)

1. 설치 완료가 확인되었습니다. 클릭 **보내기** 뉴스레터를 실제로 전송합니다.

   ![mcm_newslettersendconfirm](assets/mcm_newslettersendconfirm.png)

   >[!NOTE]
   >
   >뉴스레터가 수신되었는지 확인할 수 있도록 수신자 중 하나인지 확인합니다.

### 목록에서 뉴스레터 보내기 {#sending-newsletters-from-a-list}

목록에서 뉴스레터를 전송하려면 다음을 수행하십시오.

1. MCM에서 **목록** 왼쪽 창에서 을 클릭합니다.

   >[!NOTE]
   >
   >발송하기 전에 다음 방법으로 뉴스레터의 제목과 원래 이메일 주소를 사용자 지정했는지 확인하십시오. [설정 사용자 지정](#customizing-newsletter-settings). 목록에서 뉴스레터를 전송하는 경우 테스트할 수 없으며 다음을 수행할 수 있습니다. [비행 시험](#flight-testing-newsletters) 뉴스레터에서 보내주시면 감사하겠습니다.

1. 뉴스레터를 전송할 잠재 고객 목록 옆에 있는 확인란을 선택합니다.

1. 다음에서 **도구** 메뉴, 선택 **뉴스레터 전송**. 다음 **뉴스레터 전송** 창이 열립니다.

   ![mcm_newslettersendfromlist](assets/mcm_newslettersendfromlist.png)

1. 다음에서 **뉴스레터** 필드에서 전송할 뉴스레터를 선택하고 **다음**.

   ![mcm_newslettersenddialog](assets/mcm_newslettersenddialog.png)

1. 설치 완료가 확인되었습니다. 클릭 **보내기** 선택한 뉴스레터를 지정된 잠재 고객 목록으로 보냅니다.

   ![mcm_newslettersenddialog_confirmation](assets/mcm_newslettersenddialog_confirmation.png)

   선택한 수신자에게 뉴스레터가 전송됩니다.

## 뉴스레터 구독 {#subscribing-to-a-newsletter}

이 섹션에서는 뉴스레터를 구독하는 방법에 대해 설명합니다.

### 뉴스레터 구독 {#subscribing-to-a-newsletter-1}

뉴스레터를 구독하려면(Geometrixx 웹 사이트를 예로 사용):

1. 클릭 **웹 사이트** Geometrixx으로 이동 **도구 모음** 열어봐

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. Geometrixx 뉴스레터 **등록** 필드에 전자 메일 주소를 입력하고 **등록**. 이제 뉴스레터를 구독합니다.
