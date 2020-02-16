---
title: Adobe Campaign 6.1 및 Adobe Campaign Standard 작업
seo-title: Adobe Campaign 6.1 및 Adobe Campaign Standard 작업
description: 'AEM에서 이메일 컨텐츠를 만들고 Adobe Campaign 이메일에서 처리할 수 있습니다. '
seo-description: 'AEM에서 이메일 컨텐츠를 만들고 Adobe Campaign 이메일에서 처리할 수 있습니다. '
uuid: 439df7fb-590b-45b8-9768-565b022a808b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 61b2bd47-dcef-4107-87b1-6bf7bfd3043b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Adobe Campaign 6.1 및 Adobe Campaign Standard 작업{#working-with-adobe-campaign-and-adobe-campaign-standard}

AEM에서 이메일 컨텐츠를 만들고 Adobe Campaign 이메일에서 처리할 수 있습니다. 이를 위해 다음을 수행해야 합니다.

1. Adobe Campaign 관련 템플릿에서 AEM의 새 뉴스레터를 만듭니다.
1. 모든 기능에 액세스하려면 컨텐츠를 편집하기 전에 [Adobe Campaign 서비스](#selectingtheadobecampaigncloudservice)를 선택합니다.
1. 컨텐츠를 편집합니다.
1. 컨텐츠를 확인합니다.

그러면 컨텐츠가 Adobe Campaign의 게재와 동기화될 수 있습니다. 자세한 지침은 이 문서에 설명되어 있습니다.

>[!NOTE]
>
>이 기능을 사용하려면 먼저 [Adobe Campaign](/help/sites-administering/campaignonpremise.md) 또는 [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md)와 통합되도록 AEM을 구성해야 합니다.

## Adobe Campaign을 통해 이메일 컨텐츠 보내기 {#sending-email-content-via-adobe-campaign}

AEM 및 Adobe Campaign을 구성한 후에는 AEM에서 직접 이메일 게재 컨텐츠를 만든 후 Adobe Campaign에서 처리할 수 있습니다.

AEM에서 Adobe Campaign 컨텐츠를 만들 때 모든 기능에 액세스하려면 컨텐츠를 편집하기 전에 Adobe Campaign 서비스에 연결해야 합니다.

다음 두 가지 경우가 가능합니다.

* 컨텐츠가 Adobe Campaign의 게재와 동기화될 수 있습니다. 이를 통해 게재에서 AEM 컨텐츠를 사용할 수 있습니다.
* (Adobe Campaign 온-프레미스만) 컨텐츠를 Adobe Campaign으로 직접 전송할 수 있으며, 이 경우 자동으로 새 이메일 게재가 생성됩니다. 이 모드에는 제한 사항이 있습니다.

자세한 지침은 이 문서에 설명되어 있습니다.

### 새 이메일 컨텐츠 만들기 {#creating-new-email-content}

>[!NOTE]
>
>When adding email templates, be sure to add them under **/content/campaigns** to make them available.


1. In AEM, select the **Websites** folder then browse your explorer to find where your email campaigns are managed. In the following example, the node concerned is **Websites** > **Campaigns** > **Geometrixx Outdoors** > **Email Campaigns**.

   >[!NOTE]
   >
   >[이메일 샘플은 Geometrixx에서만 사용할 수 있습니다](/help/sites-developing/we-retail.md#weretail). 패키지 공유에서 샘플 Geometrixx 콘텐츠를 다운로드하십시오.

   ![chlimage_1-172](assets/chlimage_1-172.png)

1. Select **New** > **New Page** to create new email content.
1. Adobe Campaign용으로 만들어진 템플릿 중 하나를 선택한 다음, 페이지의 일반 속성을 입력합니다. 기본적으로 다음과 같은 세 가지 템플릿을 사용할 수 있습니다.

   * **Adobe Campaign Email(AC 6.1)**: 배달을 위해 Adobe Campaign 6.1에 보내기 전에 미리 정의된 템플릿에 컨텐츠를 추가할 수 있습니다.
   * **Adobe Campaign Email(ACS)**: 배달을 위해 Adobe Campaign Standard에 보내기 전에 미리 정의된 템플릿에 컨텐츠를 추가할 수 있습니다.
   ![chlimage_1-173](assets/chlimage_1-173.png)

1. Click **Create** to create your email or newsletter.

### Adobe Campaign 클라우드 서비스 및 템플릿 선택 {#selecting-the-adobe-campaign-cloud-service-and-template}

Adobe Campaign과 통합하려면 페이지에 Adobe Campaign 클라우드 서비스를 추가해야 합니다. 이렇게 하면 개인화 및 기타 Adobe Campaign 정보에 액세스할 수 있습니다.

또한 Adobe Campaign 템플릿을 선택하고 제목을 변경한 후, HTML에서 이메일을 보지 않는 사용자를 위해 일반 텍스트 컨텐츠를 추가해야 할 수도 있습니다.

1. Select the **Page** tab in the sidekick, then select **Page properties.**
1. In the **Cloud services** tab in the pop-up window, select **Add Service** to add the Adobe Campaign service and click **OK**.

   ![chlimage_1-174](assets/chlimage_1-174.png)

1. Select the configuration that matches your Adobe Campaign instance from the drop-down list, then click **OK**.

   >[!NOTE]
   >
   >클라우드 서비스를 추가한 후에는 반드시 **확인** 또는 **적용**&#x200B;을 탭/클릭하십시오. 이렇게 하면 **Adobe Campaign** 탭이 제대로 작동할 수 있습니다.

1. If you would like to apply a specific email delivery template (from Adobe Campaign), other than the default **mail** template, select **Page properties** again. In the **Adobe Campaign** tab, enter the email delivery template&#39;s internal name in the related Adobe Campaign instance.

   Adobe Campaign Standard에서 템플릿은 **AEM 컨텐츠 포함 배달**&#x200B;입니다. Adobe Campaign 6.1에서는 **AEM 컨텐츠 포함 이메일 배달**&#x200B;입니다.

   When you select the template, AEM automatically enables the **Adobe Campaign Newsletter** components.

### 이메일 컨텐츠 편집 {#editing-email-content}

클래식 사용자 인터페이스나 터치에 적합한 사용자 인터페이스에서 이메일 컨텐츠를 편집할 수 있습니다.

1. Enter the subject and the text version of the email by selecting **Page properties** > **Email** from the toolbox.

   ![chlimage_1-175](assets/chlimage_1-175.png)

1. 사이드 킥에서 원하는 요소를 추가하여 이메일 컨텐츠를 편집합니다. 이렇게 하려면 요소를 드래그하여 놓으십시오. 그런 다음 편집하려는 요소를 두 번 클릭합니다.

   예를 들어, 개인화 필드가 포함된 텍스트를 추가할 수 있습니다.

   ![chlimage_1-176](assets/chlimage_1-176.png)

   Adobe Campaign 뉴스레터/이메일 캠페인에 사용할 수 있는 구성 요소에 대한 설명은 [Adobe Campaign 구성 요소](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md)를 참조하십시오.

   ![chlimage_1-177](assets/chlimage_1-177.png)

### 개인화 삽입 {#inserting-personalization}

컨텐츠를 편집할 때 다음을 삽입할 수 있습니다.

* Adobe Campaign 컨텍스트 필드. 이러한 필드는 수신자의 데이터(예: 이름, 성 또는 대상 차원의 데이터)에 따라 적용될 텍스트 내에 삽입할 수 있는 필드입니다.
* Adobe Campaign 개인화 블록. 브랜드 로고 또는 미러 페이지에 대한 링크와 같이 수신자의 데이터와 관련되지 않은 사전 정의된 컨텐츠 블록입니다.

캠페인 구성 요소에 대한 전체 설명을 보려면 [Adobe Campaign 구성 요소](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md)를 참조하십시오.

>[!NOTE]
>
>* Adobe Campaign **프로필** 타깃팅 차원의 필드만 고려됩니다.
>* When viewing Properties from **Sites**, you do not have access to the Adobe Campaign context fields. 편집하는 동안 이메일에서 직접 액세스할 수 있습니다.
>



1. Insert a new **Newsletter** > **Text &amp; Personalization (Campaign)** component.
1. 구성 요소를 두 번 클릭하여 엽니다. **편집** 창에는 개인화 요소를 삽입할 수 있는 기능이 있습니다.

   >[!NOTE]
   >
   >사용 가능한 컨텍스트 필드는 Adobe Campaign의 **프로필** 타깃팅 차원에 해당합니다.
   >
   >See [Linking an AEM page to an Adobe Campaign email](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#linkinganaempagetoanadobecampaignemail).

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. Select **Client Context** in the sidekick to test the personalization fields using the data in the persona profiles.

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. 창이 표시되고 원하는 모습을 선택할 수 있습니다. 개인화 필드는 선택된 프로필의 데이터로 자동 교체됩니다.

   ![chlimage_1-180](assets/chlimage_1-180.png)

### 뉴스레터 미리 보기 {#previewing-a-newsletter}

뉴스레터의 모양을 미리 보고 개인화도 미리 볼 수 있습니다.

1. 미리 보려는 뉴스레터를 열고 [미리 보기](확대경)를 클릭하여 사이드 킥을 축소합니다.
1. 이메일 클라이언트 아이콘 중 하나를 클릭하여 각 이메일 클라이언트에서 표시되는 뉴스레터 모습을 확인합니다.

   ![chlimage_1-181](assets/chlimage_1-181.png)

1. 사이드 킥을 확장하여 편집을 다시 시작합니다.

### AEM에서 컨텐츠 승인 {#approving-content-in-aem}

컨텐츠가 완료되면 승인 프로세스를 시작할 수 있습니다. Go to the **Workflow** tab of the toolbox and select the **Approve for Adobe Campaign** workflow.

곧바로 사용할 수 있는 이 워크플로우에는 개정 후 개정 또는 개정 후 거부의 두 단계가 포함되어 있습니다. 그렇지만 이 워크플로우를 확장하고 좀 더 복잡한 프로세스에 맞게 조정할 수 있습니다.

![chlimage_1-182](assets/chlimage_1-182.png)

To approve content for Adobe Campaign, apply the workflow by selecting **Workflow** in the sidekick and selecting **Approve for Adobe Campaign** and click **Start Workflow**. 단계를 거쳐 컨텐츠를 승인합니다. 마지막 워크플로우 단계에서 **승인** 대신 **거부**&#x200B;를 선택하여 컨텐츠를 거부할 수도 있습니다.

![chlimage_1-183](assets/chlimage_1-183.png)

컨텐츠가 승인되면 Adobe Campaign에 승인된 것으로 나타납니다. 그러면 이메일을 전송할 수 있습니다.

Adobe Campaign Standard:

![chlimage_1-184](assets/chlimage_1-184.png)

Adobe Campaign 6.1:

![chlimage_1-185](assets/chlimage_1-185.png)

>[!NOTE]
>
>승인되지 않은 컨텐츠는 Adobe Campaign의 게재와 동기화할 수 있지만 게재를 실행할 수는 없습니다. 승인된 컨텐츠만 캠페인 게재를 통해 전송할 수 있습니다.

## Adobe Campaign Standard 및 Adobe Campaign 6.1에 AEM 연결 {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign}

>[!NOTE]
>
>See [Linking AEM with Adobe Campaign Standard and Adobe Campaign 6.1](/help/sites-authoring/campaign.md#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic) under [Working with Adobe Campaign 6.1 and Adobe Campaign Standard](/help/sites-authoring/campaign.md) in the standard authoring docurmentation for details.

