---
title: Adobe Target과 통합 수동 구성
seo-title: Adobe Target과 통합 수동 구성
description: Adobe Target과의 통합을 수동으로 구성하는 방법을 알아봅니다.
seo-description: Adobe Target과의 통합을 수동으로 구성하는 방법을 알아봅니다.
uuid: 0bb76a65-f981-4cc5-bee8-5feb3297137c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 20c8eb1d-5847-4902-b7d3-4c3286423b46
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Adobe Target과 통합 수동 구성 {#manually-configuring-the-integration-with-adobe-target}

마법사를 사용할 때 수행한 옵트인 마법사 구성을 수정하거나 마법사를 사용하지 않고 Adobe Target과 수동으로 통합할 수 있습니다.

## 옵트인 마법사 구성 수정 {#modifying-the-opt-in-wizard-configurations}

AEM을 [Adobe Target과](/help/sites-administering/opt-in.md) 통합하는 옵트인 마법사는 [프로비저닝된 타겟 구성이라는](/help/sites-administering/target.md) Target 클라우드 구성을 자동으로 만듭니다. 또한 마법사는 Provisioned Target Framework라는 클라우드 구성에 대한 Target 프레임워크를 만듭니다. 필요한 경우 클라우드 구성 및 프레임워크의 속성을 수정할 수 있습니다.

A4T Analytics 클라우드 구성을 구성하여 컨텐츠를 타깃팅할 때 Adobe Target을 보고 소스로 사용하도록 Adobe Target을 구성할 수도 있습니다.

클라우드 구성 및 프레임워크를 찾으려면 **도구를** 통해 **클라우드 서비스로** 이동 **>** Cloud **를**&#x200B;통해클라우드서비스로이동합니다. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))Adobe Target 아래에서 구성 표시를 클릭하거나 **탭합니다**.

### 제공된 타겟 구성 속성 {#provisioned-target-configuration-properties}

다음 속성 값은 옵트인 마법사가 생성하는 프로비전된 타겟 구성 클라우드 구성에서 사용됩니다.

* **** 클라이언트 코드:옵트인 마법사에 입력한 대로
* **** 이메일:옵트인 마법사에 입력한 대로
* **** 암호:옵트인 마법사에 입력한 대로
* **** API 유형:REST
* **** Adobe Target에서 세그먼트 동기화:선택됨.

* **** 클라이언트 라이브러리:mbox.js.
* **** DTM을 사용하여 클라이언트 라이브러리 제공:선택되지 않았습니다. DTM 또는 다른 태그 관리 시스템을 [사용하여](/help/sites-administering/dtm.md) mbox.js 또는 AT.js 파일을 호스팅하는 경우 이 옵션을 선택합니다. 라이브러리를 제공하려면 AEM이 아닌 DTM을 사용하는 것이 좋습니다.

* **** 사용자 지정 mbox.js:기본 mbox.js 파일이 사용되도록 지정되지 않았습니다. 필요에 따라 사용할 사용자 지정 mbox.js 파일을 지정합니다. mbox.js를 선택한 경우에만 나타납니다.
* **** 사용자 지정 AT.js:기본 AT.js 파일이 사용되도록 지정되지 않았습니다. 필요에 따라 사용할 사용자 지정 AT.js 파일을 지정합니다. AT.js를 선택한 경우에만 나타납니다.

>[!NOTE]
>
>AEM 6.3에서는 Target 라이브러리 파일인 [AT](https://marketing.adobe.com/resources/help/en_US/target/ov2/c_target-atjs-implementation.html).JS를 선택할 수 있습니다. AT.JS는 일반적인 웹 구현과 단일 페이지 애플리케이션 모두에 맞게 설계된 Adobe Target용 새 구현 라이브러리입니다.
>
>AT.js는 mbox.js 라이브러리에 대한 몇 가지 개선 사항을 제공합니다.
>
>* 웹 구현을 위한 페이지 로드 시간 개선
>* 향상된 보안
>* 단일 페이지 애플리케이션을 위한 향상된 구현 옵션
>* AT.js에는 target.js에 포함된 구성 요소가 포함되어 있으므로 더 이상 target.js에 대한 호출이 없습니다.
>
>
자세한 [내용은 Target 릴리스 노트를](https://marketing.adobe.com/resources/help/en_US/target/rn/201604.html) 참조하십시오.

### 제공된 타겟 프레임워크 속성 {#provisioned-target-framework-properties}

옵트인 마법사가 생성하는 프로비전된 타겟 프레임워크는 프로필 데이터 저장소에서 컨텍스트 데이터를 전송하도록 구성됩니다. 스토어의 연령 및 성별 데이터 항목은 기본적으로 Target으로 전송됩니다. 솔루션을 사용하려면 추가 매개 변수가 필요합니다.

![chlimage_1-158](assets/chlimage_1-158.png)

Target 프레임워크 추가에 설명된 대로 Target에 추가 컨텍스트 정보를 보내도록 프레임워크를 구성할 [수 있습니다](/help/sites-administering/target-configuring.md#adding-a-target-framework).

### Configuring A4T Analytics Cloud Configuration {#configuring-a-t-analytics-cloud-configuration}

컨텐츠를 타깃팅할 때 Adobe Analytics를 보고 소스로 사용하도록 Adobe Target을 구성할 수 있습니다.

이렇게 하려면 Adobe Target 클라우드 구성을 연결할 A4T 클라우드 구성을 지정해야 합니다.

1. AEM 로고를 **통해** AEM **로고** > **배포 >** 배포 **> Cloud** Services를 통해 ****&#x200B;클라우드 서비스로 이동합니다.
1. Adobe Target **섹션에서** 지금 **구성을 클릭합니다**.
1. Adobe Target 구성에 다시 연결합니다.
1. A4T **Analytics 클라우드 구성** 드롭다운 메뉴에서 프레임워크를 선택합니다.

   >[!NOTE]
   >
   >A4T에 대해 활성화된 분석 구성만 사용할 수 있습니다.
   >
   >AEM 파섹 분석 프레임워크를 선택하려면 다음을 수행합니다.
   >
   >1. 도구 > **일반** > **CRXDE** Lite로 **이동합니다**.
   1. /libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig로 이동합니다. ****
   1. 속성 **disable** 을 **false로 설정합니다**.
   1. Tap or click **Save All**.


   ![chlimage_1-159](assets/chlimage_1-159.png)

   **확인**&#x200B;을 클릭합니다. Adobe Target을 사용하여 컨텐츠를 타깃팅하는 경우 보고서 소스를 [선택할 수 있습니다](/help/sites-authoring/content-targeting-touch.md).

## Manually Integrating with Adobe Target {#manually-integrating-with-adobe-target}

옵트인 마법사를 사용하는 대신 Adobe Target과 수동으로 통합할 수 있습니다.

>[!NOTE]
Target 라이브러리 파일인 [AT](https://marketing.adobe.com/resources/help/en_US/target/ov2/c_target-atjs-implementation.html).JS는 일반적인 웹 구현과 단일 페이지 애플리케이션 모두를 위해 설계된 Adobe Target용 새로운 구현 라이브러리입니다. mbox.js 대신 AT.js를 클라이언트 라이브러리로 사용하는 것이 좋습니다.
AT.js는 mbox.js 라이브러리에 대한 몇 가지 개선 사항을 제공합니다.
* 웹 구현을 위한 페이지 로드 시간 개선
* 향상된 보안
* 단일 페이지 애플리케이션을 위한 향상된 구현 옵션
* AT.js에는 target.js에 포함된 구성 요소가 포함되어 있으므로 더 이상 target.js에 대한 호출이 없습니다.

자세한 [내용은 Target 릴리스 노트를](https://marketing.adobe.com/resources/help/en_US/target/rn/201604.html) 참조하십시오.
클라이언트 라이브러리 **** 드롭다운 메뉴에서 AT.js 또는 mbox.js를 선택할 수 있습니다.

### 타겟 클라우드 구성 만들기 {#creating-a-target-cloud-configuration}

AEM이 Adobe Target과 상호 작용할 수 있도록 하려면 Target 클라우드 구성을 만듭니다. 구성을 만들려면 Adobe Target 클라이언트 코드 및 사용자 자격 증명을 제공합니다.

구성을 여러 AEM 캠페인에 연결할 수 있으므로 Target 클라우드 구성을 한 번만 만듭니다. 여러 Adobe Target 클라이언트 코드가 있는 경우 각 클라이언트 코드에 대해 하나의 구성을 만듭니다.

Adobe Target에서 세그먼트를 동기화하도록 클라우드 구성을 구성할 수 있습니다. 동기화를 활성화하면, 세그먼트는 클라우드 구성이 저장되자마자 백그라운드에서 Target에서 가져옵니다.

AEM에서 Target 클라우드 구성을 만들려면 다음 절차를 따르십시오.

1. AEM 로고를 **통해** AEM **로고** > **배포 >** 배포 **> Cloud** Services를 통해 ****&#x200B;클라우드 서비스로 이동합니다. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   Adobe **Marketing Cloud** 개요 페이지가 열립니다.

1. Adobe Target **섹션에서** 지금 **구성을 클릭합니다**.
1. 구성 **만들기 대화** 상자에서 다음을 수행합니다.

   1. 구성에 제목을 **지정합니다**.
   1. Adobe Target **구성 템플릿을** 선택합니다.
   1. **만들기**&#x200B;를 클릭합니다.
   편집 대화 상자가 열립니다.

   ![chlimage_1-160](assets/chlimage_1-160.png)

   >[!NOTE]
   AEM 파섹 분석 프레임워크를 선택하려면 다음을 수행합니다.
   1. 도구 > **일반** > **CRXDE** Lite로 **이동합니다**.
   1. /libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig로 이동합니다. ****
   1. 속성 **disable** 을 **false로 설정합니다**.
   1. Tap or click **Save All**.


1. 대화 상자에서 이러한 속성에 대한 값을 제공합니다.

   * **클라이언트 코드**:대상 계정 클라이언트 코드
   * **이메일**:타겟 계정 이메일.
   * **암호**:타겟 계정 암호.
   * **API 유형**:REST 또는 XML
   * **A4T Analytics 클라우드 구성**:타겟 활동 목표 및 지표에 사용되는 Analytics 클라우드 구성을 선택합니다. 컨텐츠를 타깃팅할 때 Adobe Analytics를 보고 소스로 사용하는 경우 이 옵션이 필요합니다. 클라우드 구성이 표시되지 않으면 A4T Analytics 클라우드 [구성 구성을 참조하십시오](#configuring-a-t-analytics-cloud-configuration).

   * **** 정확한 타깃팅 사용:기본적으로 이 확인란이 선택되어 있습니다. 이 옵션을 선택하면 클라우드 서비스 구성이 컨텍스트를 로드한 후 콘텐츠를 로드합니다. 참고:
   * **** Adobe Target에서 세그먼트 동기화:AEM에서 사용할 Target에 정의된 세그먼트를 다운로드하려면 이 옵션을 선택합니다. 인라인 세그먼트는 지원되지 않으며 항상 Target의 세그먼트를 사용해야 하기 때문에 API 유형 속성이 REST인 경우 이 옵션을 선택해야 합니다. (&#39;segment&#39;의 AEM 용어는 Target &#39;audience&#39;와 같습니다.)
   * **** 클라이언트 라이브러리:mbox.js 또는 AT.js 클라이언트 라이브러리를 원하는지 선택합니다.
   * **DTM을 사용하여 클라이언트 라이브러리** 전달 - DTM 또는 다른 태그 관리 시스템의 AT.js 또는 mbox.js를 사용하려면 이 옵션을 선택합니다. 이 옵션을 사용하려면 DTM 통합을 [](/help/sites-administering/dtm.md) 구성해야 합니다. 라이브러리를 제공하려면 AEM이 아닌 DTM을 사용하는 것이 좋습니다.
   * **사용자 지정 mbox.js**:DTM 상자를 선택하거나 기본 mbox.js를 사용하려면 비워 둡니다. 또는 사용자 지정 mbox.js를 업로드합니다. mbox.js를 선택한 경우에만 나타납니다.
   * **사용자 지정 AT.js**:DTM 상자를 선택하거나 기본 AT.js를 사용하려면 비워 둡니다. 또는 사용자 지정 AT.js를 업로드합니다. AT.js를 선택한 경우에만 나타납니다.
   >[!NOTE]
   기본적으로 Adobe Target 구성 마법사를 선택하면 정확한 타깃팅이 활성화됩니다.
   정확한 타깃팅은 클라우드 서비스 구성이 콘텐츠를 로드하기 전에 컨텍스트가 로드되기를 기다리는 것을 의미합니다. 따라서, 성능 측면에서, 정확한 타깃팅은 컨텐츠를 로드하기 전에 몇 밀리초의 지연을 만들 수 있습니다.
   정확한 타깃팅은 항상 작성자 인스턴스에서 활성화됩니다. 하지만 게시 인스턴스에서 클라우드 서비스 구성의 정확한 타게팅 옆에 있는 확인 표시(http://localhost:4502/etc/cloudservices.html)를 지워 정확한 타게팅을 전체적으로 끌 수&#x200B;**있습니다**. 클라우드 서비스 구성의 설정에 관계없이 개별 구성 요소에 대해 정확한 타깃팅을 켜거나 끌 수도 있습니다.
   타깃팅된 구성 요소를 ***이미*** 만들고 이 설정을 변경하는 경우 변경 사항이 해당 구성 요소에 영향을 주지 않습니다. 해당 구성 요소를 직접 변경해야 합니다.

1. Target **에 연결을** 클릭하여 Target과의 연결을 초기화합니다. 연결이 성공하면 [연결 성공] **이라는 메시지가** 표시됩니다. 메시지에 **대해** 확인을 클릭한 다음 **대화** 상자에서확인을 클릭합니다.

   Target에 연결할 수 없는 경우 [문제 해결](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) 섹션을 참조하십시오.

### Target 프레임워크 추가 {#adding-a-target-framework}

Target 클라우드 구성을 구성한 후 Target 프레임워크를 추가합니다. 프레임워크는 사용 가능한 클라이언트 컨텍스트 또는 ContextHub 구성 요소에서 Adobe Target으로 전송되는 기본 [매개](/help/sites-administering/client-context.md) 변수를 [식별합니다](/help/sites-administering/contexthub-config.md) . Target은 매개 변수를 사용하여 현재 컨텍스트에 적용되는 세그먼트를 결정합니다.

단일 Target 구성에 대해 여러 프레임워크를 만들 수 있습니다. 여러 프레임워크는 웹 사이트의 여러 섹션에 대해 다른 매개 변수 세트를 Target으로 전송해야 하는 경우 유용합니다. 전송해야 하는 각 매개 변수 세트에 대한 프레임워크를 만듭니다. 웹 사이트의 각 섹션을 적절한 프레임워크와 연결합니다. 웹 페이지는 한 번에 하나의 프레임워크만 사용할 수 있습니다.

1. Target 구성 페이지에서 사용 가능한 프레임워크 옆에 있는 **+** (더하기 기호)를 클릭합니다.
1. 프레임워크 만들기 대화 상자에서 제목을 **지정하고** Adobe Target **Framework를**&#x200B;선택한 **다음 만들기를**&#x200B;클릭합니다.

   ![chlimage_1-161](assets/chlimage_1-161.png)

   프레임워크 페이지가 열립니다. 사이드 킥은 매핑할 수 있는 클라이언트 컨텍스트 [또는 ContextHub](/help/sites-administering/client-context.md) 의 정보를 [나타내는](/help/sites-administering/contexthub-config.md) 구성 요소를 제공합니다.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. 드롭 대상에 매핑하는 데 사용할 데이터를 나타내는 클라이언트 컨텍스트 구성 요소를 드래그합니다. 또는 ContextHub **저장소** 구성 요소를 프레임워크로 드래그합니다.

   >[!NOTE]
   매핑 시 매개 변수는 간단한 문자열을 통해 mbox로 전달됩니다. ContextHub에서 배열을 매핑할 수 없습니다.

   예를 들어 사이트 방문자에 **대한** 프로필 데이터를 사용하여 Target 캠페인을 제어하려면 프로필 데이터 **구성 요소를** 페이지로 드래그합니다. Target 매개 변수에 매핑하는 데 사용할 수 있는 프로필 데이터 변수가 나타납니다.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 해당 열에서 공유 **확인란을 선택하여 Adobe Target 시스템에 표시할 변수를** 선택합니다.

   ![chlimage_1-164](assets/chlimage_1-164.png)

   >[!NOTE]
   매개 변수 동기화는 AEM에서 Adobe Target에 대한 한 가지 방법일 뿐입니다.

프레임워크가 생성됩니다. 프레임워크를 게시 인스턴스에 복제하려면 사이드 킥에서 **프레임워크** 활성화 옵션을 사용합니다.

### 활동을 Target Cloud 구성과 연결 {#associating-activities-with-the-target-cloud-configuration}

AEM [활동을](/help/sites-authoring/activitylib.md) Target 클라우드 구성과 연계하여 Adobe Target의 활동을 미러링할 수 [있습니다](https://marketing.adobe.com/resources/help/en_US/target/target/c_manage_content.html).

>[!NOTE]
사용 가능한 활동 유형은 다음 방법으로 결정됩니다.
* Adobe Target에 연결하기 위해 AEM 측에 사용된 Adobe Target 임차인(clientcode)에서 **xt_only** 선택 사항이 활성화되면, AEM에서 XT 활동&#x200B;**만** 만들 수 있습니다.

* Adobe Target 임차인(clientcode)에서 **xt_only** 선택 사항이 활성화되지 **않으면** AEM에서에서 XT 활동과 A/B 활동을 **모두** 만들 수 있습니다.

**추가 참고:** **xt_only** 선택 사항은 특정 Target 임차인(clientcode)에 적용되는 설정이며, Adobe Target에서 직접 수정하는 것만 가능합니다. 이 선택 사항은 AEM에서 활성하거나 비활성화할 수 없습니다.

### 타겟 프레임워크와 사이트 연결 {#associating-the-target-framework-with-your-site}

AEM에서 Target 프레임워크를 만든 후 웹 페이지를 프레임워크에 연결합니다. 페이지의 타깃팅된 구성 요소는 추적을 위해 프레임워크 정의 데이터를 Adobe Target으로 보냅니다. (컨텐츠 [타깃팅을 참조하십시오](/help/sites-authoring/content-targeting-touch.md).)

페이지를 프레임워크와 연결하면 하위 페이지가 연결을 상속합니다.

1. 사이트 **콘솔에서** 구성할 사이트로 이동합니다.
1. [빠른 작업](/help/sites-authoring/basic-handling.md#quick-actions) 또는 [선택 모드를](/help/sites-authoring/basic-handling.md)사용하여 속성 보기를 **선택합니다.**
1. 클라우드 서비스 **탭을** 선택합니다.
1. Tap/click **Edit**.
1. 클라우드 서비스 구성 **아래에서 구성** 추가를 **탭/클릭하고** Adobe **Target을**&#x200B;선택합니다.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 구성 참조에서 원하는 프레임워크를 **선택합니다**.

   >[!NOTE]
   만들어진 Target 클라우드 구성이 아닌 사용자가 만든 특정 **프레임워크를** 선택해야 합니다.

1. 완료를 탭/ **클릭합니다**.
1. 웹 사이트의 루트 페이지를 활성화하여 게시 서버에 복제합니다. (See [How To Publish Pages](/help/sites-authoring/publishing-pages.md).)

   >[!NOTE]
   페이지에 첨부한 프레임워크가 아직 활성화되지 않은 경우 마법사를 열어 게시할 수도 있습니다.

## 대상 연결 문제 해결 {#troubleshooting-target-connection-problems}

Target에 연결할 때 발생하는 문제를 해결하려면 다음 작업을 수행하십시오.

* 제공한 사용자 자격 증명이 올바른지 확인하십시오.
* AEM 인스턴스가 Target 서버에 연결할 수 있는지 확인합니다. 예를 들어 방화벽 규칙이 아웃바운드 AEM 연결을 차단하지 않거나 AEM이 필요한 프록시를 사용하도록 구성되어 있는지 확인하십시오.
* AEM 오류 로그에서 유용한 메시지를 찾습니다. error.log 파일은 AEM이 설치된 **crx-quickstart/logs** 디렉토리에 있습니다.
* Adobe Target에서 활동을 편집할 때 URL이 localhost를 가리킵니다. AEM 외부 도우미를 올바른 URL로 설정하여 이 문제를 해결할 수 있습니다.

