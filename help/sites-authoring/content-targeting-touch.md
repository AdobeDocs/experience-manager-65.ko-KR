---
title: 타깃팅 모드를 사용한 타깃팅된 컨텐츠 작성
seo-title: 타깃팅 모드를 사용한 타깃팅된 컨텐츠 작성
description: 타깃팅 모드 및 타겟 구성 요소는 경험을 위한 컨텐츠를 만드는 도구를 제공합니다.
seo-description: 타깃팅 모드 및 타겟 구성 요소는 경험을 위한 컨텐츠를 만드는 도구를 제공합니다.
uuid: cea85c1b-1bc3-4498-9eaa-4ad10dc58ea4
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 9d940744-3b00-4721-829a-96d17bb738e8
docset: aem65
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '5374'
ht-degree: 78%

---


# 타깃팅 모드를 사용한 타깃팅된 컨텐츠 작성{#authoring-targeted-content-using-targeting-mode}

AEM의 타깃팅 모드를 사용하여 타깃팅된 컨텐츠를 작성하십시오. 타깃팅 모드 및 타겟 구성 요소는 경험을 위한 컨텐츠를 만드는 도구를 제공합니다.

* 페이지에 있는 타깃팅된 컨텐츠를 쉽게 인식할 수 있습니다. 점선이 모든 타깃팅된 컨텐츠 주변에 테두리를 표시합니다.
* 경험을 볼 브랜드 및 활동을 선택합니다.
* 경험을 활동에 추가하거나 경험을 제거합니다.
* A/B 테스트를 수행하고 우승자를 변환합니다(Adobe Target만 해당).
* 오퍼를 작성하거나 라이브러리에서 제공하는 오퍼를 사용하여 오퍼를 경험에 추가합니다.
* 목표를 구성하고 성과를 모니터링합니다.
* 사용자 경험을 시뮬레이션합니다.
* 사용자 지정이 더 필요하면 타겟 구성 요소를 구성합니다.

타깃팅 엔진으로 AEM 또는 Adobe Target을 사용할 수 있습니다(Adobe Target을 사용하려면 올바른 Adobe Target 계정이 있어야 합니다). Adobe Target을 사용하는 경우 먼저 통합을 구성해야 합니다. See [instructions for integrating with Adobe Target](/help/sites-administering/target.md).

![chlimage_1-8](assets/chlimage_1-8.png)

타겟 모드에 표시되는 활동과 경험은 [활동 콘솔](/help/sites-authoring/activitylib.md)을 반영합니다.

* 타깃팅 모드를 사용하여 활동 및 경험에 수행하는 변경 내용은 활동 콘솔에 반영됩니다.
* 활동 콘솔에서 수행된 변경 내용은 타깃팅 모드에서 반영됩니다.

>[!NOTE]
>
>Adobe Target에서 캠페인을 만들 때 각 캠페인에 `thirdPartyId`라는 속성을 지정하게 됩니다. Adobe Target에서 이 캠페인을 삭제해도 thirdPartyId는 삭제되지 않습니다. `thirdPartyId`는 다른 유형의 캠페인(AB, XT)에 대해 다시 사용할 수 없으며 수동으로 제거할 수 없습니다. 이 문제를 방지하려면 각 캠페인의 이름을 고유한 이름으로 지정합니다. 따라서 캠페인 이름을 다른 캠페인 유형에서 다시 사용할 수 없습니다.
>
>동일한 캠페인 유형에서 동일한 이름을 사용하는 경우 기존 캠페인을 덮어쓰게 됩니다.
>
>동기화 중에 &quot;Request Failed. `thirdPartyId` already exists&quot;(요청이 실패했습니다. thirdPartyId가 이미 있습니다)라는 오류가 발생하는 경우, 캠페인 이름을 변경하고 다시 동기화하십시오.

>[!NOTE]
>
>타깃팅할 때 브랜딩 및 활동 조합은 채널 레벨이 아닌 사용자 레벨에서 지속됩니다.

## 타겟 모드로 전환 {#switching-to-targeting-mode}

타깃팅된 컨텐츠를 작성하는 도구에 액세스하려면 타겟 모드로 전환하십시오.

타겟 모드로 전환하려면 다음을 수행하십시오.

1. 타깃팅된 컨텐츠를 작성할 페이지를 엽니다.
1. 페이지 상단의 도구 모음에서 모드 드롭다운 메뉴를 클릭하거나 탭하여 사용 가능한 모드 유형을 표시합니다.

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. Click or tap **Targeting**. 페이지 상단에 타깃팅 선택 사항이 표시됩니다.

   ![chlimage_1-10](assets/chlimage_1-10.png)

## 타깃팅 모드를 사용한 활동 추가 {#adding-an-activity-using-targeting-mode}

활동을 브랜드에 추가하려면 타겟 모드를 사용하십시오. 활동을 추가하면 활동에 기본 경험이 포함됩니다. 활동을 추가했으면 활동에 대한 컨텐츠 타깃팅 프로세스를 시작합니다.

타겟 엔진(AEM 또는 Adobe Target)을 선택하거나 활동 유형(경험 타깃팅 또는 A/B 테스트)을 선택하는 선택 사항을 사용하여 AEM에서 Adobe Target 활동을 생성하고 관리할 수도 있습니다.

또한 모든 Adobe Target 활동에 대한 목표와 지표를 관리하고 Adobe Target 대상을 관리할 수도 있습니다. A/B 테스트에 대한 우승자 변환을 포함하여 Adobe Target 활동을 보고할 수도 있습니다.

활동을 추가하면 [활동 콘솔](/help/sites-authoring/activitylib.md)에도 나타납니다.

활동을 추가하려면 다음을 수행하십시오.

1. **브랜드** 드롭다운 메뉴를 사용하여 활동을 생성할 브랜드를 선택합니다.

   >[!NOTE]
   >
   >[활동 콘솔을 통해 브랜드를 작성](/help/sites-authoring/activitylib.md#creating-a-brand-using-the-activities-console)하는 것이 좋습니다.
   >
   >
   >If you create a brand in any other way, make certain that the node `/campaigns/<brand>/master` exists or an error will result when you attempt to create an activity.

1. **활동** 드롭다운 메뉴 옆에 있는 +를 클릭하거나 탭합니다.
1. 활동 이름을 입력합니다.

   >[!NOTE]
   >
   >새 활동을 생성하고 페이지 또는 그 상위 항목 중 하나에 연결된 Adobe Target 클라우드 구성이 있으면, AEM은 자동으로 Adobe Target을 엔진으로 가정합니다.

1. **타깃팅** 엔진 드롭다운 메뉴에서 타깃팅 엔진을 선택합니다.

   * If you select **ContextHub AEM**, the remaining fields are dimmed and not available. **만들기**&#x200B;를 클릭하거나 탭합니다.

   * **Adobe Target**&#x200B;을 선택하는 경우 구성(기본적으로 [계정을 구성](/help/sites-administering/opt-in.md)할 때 제공했던 구성임)과 활동 유형을 선택할 수 있습니다.

   * AEM/Adobe 캠페인 통합을 사용하고 타깃팅된 컨텐츠(뉴스레터)를 전송하는 중이라면 **Adobe Campaign**&#x200B;을 선택하십시오. 자세한 내용은 [Adobe Campaign과 통합](/help/sites-administering/campaign.md)을 참조하십시오.

1. 활동 메뉴에서 **경험 타깃팅** 또는 **A/B 테스트**&#x200B;를 선택합니다.

   * 경험 타깃팅 - AEM에서 Adobe Target 활동을 관리합니다.
   * A/B 테스트 - AEM에서 Adobe Target에 있는 A/B 테스트 활동을 생성/관리합니다.

## 타깃팅 프로세스: 만들기, 타겟, 목표 및 설정 {#the-targeting-process-create-target-and-goals-settings}

타깃팅 모드를 사용하면 활동의 몇 가지 측면을 구성할 수 있습니다. 브랜드 활동을 위한 타깃팅된 컨텐츠를 생성하는 다음의 3단계 프로세스를 사용하십시오.

1. [만들기](#create-authoring-the-experiences): 경험을 추가 또는 제거하고 각 경험에 대한 오퍼를 추가합니다.
1. [타겟](#diagramtargetconfiguringtheaudiences): 각 경험이 타깃팅하는 대상을 지정합니다. 특정 대상을 타깃팅할 수 있으며, A/B 테스트를 사용하는 경우에는 트래픽 중 어느 정도의 비율이 어느 경험으로 가는지를 결정할 수 있습니다.
1. [목표 및 설정](#settingsgoalssettingsconfiguringtheactivityandsettinggoals): 활동을 예약하고 우선 순위를 설정합니다. 또한 성공 지표 목표를 설정할 수도 있습니다.

다음 절차를 사용하여 활동에 대한 컨텐츠 타깃팅 프로세스를 시작하십시오.

>[!NOTE]
>
>타깃팅 프로세스를 사용하려면 Target 활동 작성자 사용자 그룹의 구성원이어야 합니다.

활동을 추가하려면 다음을 수행하십시오.

1. **브랜드** 드롭다운 메뉴에서 작업 중인 활동이 포함된 브랜드를 선택합니다.
1. **활동** 드롭다운 메뉴에서 타깃팅된 컨텐츠를 작성 중인 활동을 선택합니다.
1. 타깃팅 프로세스를 안내하는 컨트롤을 표시하려면 **타깃팅 시작**&#x200B;을 클릭하거나 탭합니다.

   ![chlimage_1-11](assets/chlimage_1-11.png)

   >[!NOTE]
   >
   >작업 중인 활동을 변경하려면 **뒤로**&#x200B;를 클릭하거나 탭하십시오.

## 만들기: 경험 작성 {#create-authoring-the-experiences}

컨텐츠 타깃팅의 만들기 단계에는 경험 생성이 포함됩니다. 이 단계 동안 활동의 경험을 생성하거나 삭제하고 각 경험에 오퍼를 추가할 수 있습니다.

### 타깃팅 모드에서 경험 오퍼 보기 {#seeing-experience-offers-in-targeting-mode}

[타깃팅 프로세스를 시작](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings)했으면 경험을 선택하여 해당 경험을 위해 제공된 오퍼를 확인하십시오. 경험을 선택하면 페이지에 있는 타깃팅된 구성 요소가 해당 경험에 대한 오퍼를 표시하도록 변경됩니다.

>[!CAUTION]
>
>작성자 인스턴스에서 이미 타깃팅된 구성 요소에 대한 타깃팅을 비활성화할 때는 주의하십시오. 게시 인스턴스에서도 해당 활동이 자동으로 삭제됩니다.

>[!NOTE]
>
>오퍼는 타깃팅된 구성 요소의 컨텐츠입니다.

경험은 [대상자] 창에 표시됩니다. In the following example, experiences include **Default**, **Female**, **Female over 30**, and **Female under 30**. 이 예는 타깃팅된 **이미지** 구성 요소의 기본값 오퍼를 보여줍니다.

![chlimage_1-12](assets/chlimage_1-12.png)

다른 경험을 선택하면 이미지 구성 요소에 해당 경험에 대한 오퍼가 표시됩니다.

![chlimage_1-13](assets/chlimage_1-13.png)

경험을 선택했는데 타깃팅된 구성 요소에 해당 경험에 대한 오퍼가 포함되어 있지 않으면, 구성 요소에는 반투명 기본 오퍼 위에 **오퍼 추가**&#x200B;가 겹쳐진 채 표시됩니다. 경험용으로 생성된 오퍼가 없으면, 경험에 매핑된 세그먼트에 대해 **기본값** 오퍼가 표시됩니다.

![chlimage_1-14](assets/chlimage_1-14.png)

방문자 속성이 경험에 매핑된 세그먼트와 일치하지 않아도 기본값 경험이 표시됩니다. See [Adding Experiences using Targeting Mode](#adding-and-removing-experiences-using-targeting-mode).

### 사용자 정의 오퍼와 라이브러리 오퍼 {#custom-offers-and-library-offers}

[페이지에서 작성](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer)되고 단일 경험에 사용되는 오퍼를 사용자 지정 오퍼라고 합니다. 사용자 지정 오퍼의 컨텐츠 위에 다음 이미지가 겹쳐집니다.

![chlimage_1-15](assets/chlimage_1-15.png)

[오퍼 라이브러리에서 추가](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library)된 오퍼는 다음 이미지와 함께 겹쳐집니다.

![chlimage_1-16](assets/chlimage_1-16.png)

사용자 지정 오퍼를 다시 사용하려는 경우 이 오퍼를 오퍼 라이브러리에 저장할 수 있습니다. 경험 컨텐츠를 수정하려는 경우에는 라이브러리 오퍼를 사용자 지정 오퍼로 변환할 수도 있습니다. 편집 후에는 오퍼를 다시 한 번 라이브러리에 저장할 수 있습니다.

### 타깃팅 모드를 사용한 경험 추가 및 제거 {#adding-and-removing-experiences-using-targeting-mode}

[타깃팅 프로세스](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings)의 만들기 단계를 사용하면 경험을 추가하거나 제거할 수 있습니다. 또한 경험을 복제하고 이름을 변경할 수도 있습니다.

#### 타깃팅 모드를 사용한 경험 추가 {#adding-experiences-using-targeting-mode}

경험을 추가하려면 다음을 수행하십시오.

1. To add an experience, click or tap **+** **Add Experience Targeting** that appears below existing experiences in the **Audiences** pane.
1. 대상을 선택합니다. 기본적으로 해당 이름은 경험의 이름입니다. 원하는 경우 다른 이름을 입력할 수 있습니다. **확인**&#x200B;을 클릭하거나 탭하십시오.

#### 타깃팅 모드를 사용한 경험 제거 {#removing-experiences-using-targeting-mode}

경험을 삭제하려면 다음을 수행하십시오.

1. 경험 이름 옆에 있는 화살표를 클릭하거나 탭합니다.

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. **삭제**&#x200B;를 클릭합니다. 

#### 타깃팅 모드를 사용한 경험 이름 변경 {#renaming-experiences-using-targeting-mode}

타깃팅 모드를 사용하여 경험의 이름을 변경하려면 다음을 수행하십시오.

1. 경험 이름 옆에 있는 화살표를 클릭하거나 탭합니다.
1. Click **Rename Experience** and type in the new name.
1. 화면의 다른 곳을 클릭하거나 탭하여 변경 사항을 저장합니다.

#### 타깃팅 모드를 사용한 대상자 편집 {#editing-audiences-using-targeting-mode}

타깃팅 모드를 사용하여 대상을 편집하려면 다음을 수행하십시오.

1. 경험 이름 옆에 있는 화살표를 클릭하거나 탭합니다.
1. Click **Edit Audience** and select a new audience.
1. **확인**&#x200B;을 클릭합니다.

#### 타깃팅 모드를 사용한 경험 복제 {#duplicating-experiences-using-targeting-mode}

타깃팅 모드를 사용하여 경험을 복사하려면 다음을 수행하십시오.

1. 경험 이름 옆에 있는 화살표를 클릭하거나 탭합니다.
1. **복제**&#x200B;를 클릭하고 대상을 선택합니다.
1. 원하는 경우 경험의 이름을 변경하고 **확인**&#x200B;을 클릭합니다.

### 타깃팅 모드를 사용한 오퍼 생성 {#creating-offers-using-targeting-mode}

경험을 위한 오퍼를 생성할 구성 요소를 타깃팅하십시오. 타깃팅된 구성 요소는 경험을 위한 오퍼로 사용되는 컨텐츠를 제공합니다.

* [기존 구성 요소를 타깃팅하십시오](/help/sites-authoring/content-targeting-touch.md#creating-a-default-offer-by-targeting-an-existing-component). 컨텐츠는 기본 경험의 오퍼가 됩니다.
* [타겟 구성 요소를 추가](/help/sites-authoring/content-targeting-touch.md#creating-an-offer-by-adding-a-target-component)한 다음, 컨텐츠를 구성 요소에 추가하십시오.

구성 요소가 타깃팅되면 각 경험에 대한 오퍼를 추가할 수 있습니다.

* [사용자 지정 오퍼를 추가합니다](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer).
* [라이브러리에서 오퍼를 추가합니다](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library).

오퍼를 사용한 작업에 다음 도구를 사용할 수 있습니다.

* [사용자 지정 오퍼를 오퍼 라이브러리에 추가합니다](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer-to-a-library).
* [라이브러리 오퍼를 사용자 지정 오퍼로 변환합니다](/help/sites-authoring/content-targeting-touch.md#converting-a-library-offer-to-a-custom-library).
* [라이브러리 오퍼를 열고 컨텐츠를 편집합니다](/help/sites-authoring/content-targeting-touch.md#editing-a-library-offer).

#### 기존 구성 요소를 타깃팅하여 기본 오퍼 생성 {#creating-a-default-offer-by-targeting-an-existing-component}

페이지에서 구성 요소를 타깃팅하여 활동의 기본값 경험을 위한 오퍼로 사용하십시오. 구성 요소를 타깃팅하면 이 구성 요소는 타겟 구성 요소에 포함되고 해당 컨텐츠는 기본값 경험을 위한 오퍼가 됩니다.

구성 요소를 타깃팅하면 해당 구성 요소만 오퍼에서 사용할 수 있습니다. 오퍼에서 구성 요소를 제거하거나 다른 구성 요소를 오퍼에 추가할 수는 없습니다.

[타깃팅 프로세스를 시작](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings)한 후 다음 절차를 수행하십시오.

1. 타깃팅할 구성 요소를 클릭하거나 탭합니다. 다음 예와 유사한 구성 요소용 도구 모음이 나타납니다.

   ![chlimage_1-18](assets/chlimage_1-18.png)

1. 타겟 아이콘을 클릭하거나 탭합니다.

   ![](do-not-localize/chlimage_1.png)

   구성 요소 컨텐츠는 기본값 경험을 위한 오퍼입니다. 구성 요소가 타깃팅되면 각 경험에 대해 기본 노드가 복제됩니다. 이러한 복제는 경험별 작성 작업 동안 올바른 컨텐츠 노드를 편집하는 데 필요합니다. For these non-default experiences, either [add a custom offer](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer) or [add a library offer](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library).

#### 타겟 구성 요소를 추가하여 오퍼 생성 {#creating-an-offer-by-adding-a-target-component}

기본값 경험을 위한 오퍼를 생성하려면 타겟 구성 요소를 추가하십시오. Target 구성 요소는 다른 구성 요소의 컨테이너이며, 해당 구성 요소 내에 배치된 구성 요소는 타깃팅됩니다. 타겟 구성 요소를 사용하는 경우 몇 개의 구성 요소를 추가하여 오퍼를 생성할 수 있습니다. 또한 각 경험에서 다른 구성 요소를 사용하여 서로 다른 오퍼를 생성할 수도 있습니다.

See [Configuring Target component options](/help/sites-authoring/content-targeting-touch.md#configuring-target-component-options) for information on customizing this component.

>[!NOTE]
>
>Offers that you create using the [Offers console](/help/sites-authoring/offerlib.md) can also contain several components. 이러한 오퍼는 오퍼 라이브러리에 속하며 여러 경험에 사용할 수 있습니다.

타겟 구성 요소는 컨테이너이므로 다른 구성 요소에 대한 드롭 영역으로 표시됩니다.

타겟 모드에서 타겟 구성 요소에는 파란색 테두리가 있고, 드롭-타겟 메시지는 타깃팅된 특성을 나타냅니다.

![chlimage_1-19](assets/chlimage_1-19.png)

편집 모드에서 타겟 구성 요소에는 과녁 중앙 아이콘이 있습니다.

![](do-not-localize/chlimage_1-1.png)

구성 요소를 타겟 구성 요소로 드래그하면 이 구성 요소가 타깃팅된 구성 요소입니다.

![chlimage_1-20](assets/chlimage_1-20.png)

타겟 구성 요소에 구성 요소를 추가하면 이 구성 요소가 특정 경험을 위한 컨텐츠를 제공합니다. 경험을 지정하려면 구성 요소를 추가하기 전에 경험을 선택하십시오.

페이지에 타겟 구성 요소를 추가하는 것은 편집 모드 또는 타겟 모드에서 가능하고, 구성 요소를 타겟 구성 요소에 추가하는 것은 타겟 모드에서만 가능합니다. 타겟 구성 요소는 개인화 구성 요소 그룹에 속합니다.

타깃팅된 컨텐츠를 편집하는 경우 그렇게 할 수 있으려면 먼저 **타깃팅 시작**&#x200B;을 클릭하거나 탭해야 합니다.

1. 타겟 구성 요소를 오퍼를 표시할 페이지로 드래그합니다.
1. 기본적으로 설정된 위치 ID는 없습니다. 위치를 설정하려면 구성 톱니바퀴를 클릭하거나 탭하십시오.

   >[!NOTE]
   >
   >관리자가 설정하는 경우 위치를 명시적으로 설정해야 할 수 있습니다.
   >
   >
   >Administrators can decide whether setting this configuration is required at **https://&lt;host>:&lt;port>/system/console/configMgr/com.day.cq.personalization.impl.servlets.TargetingConfigurationServlet**
   사용자가 위치를 입력하도록 하려면 **강제 위치 **확인란을 선택합니다.

1. 오퍼를 생성할 경험을 선택합니다.
1. 다음과 같이 오퍼를 생성합니다.

   * 기본 경험의 경우 구성 요소를 타깃팅된 드롭 영역으로 드래그하고 구성 요소 속성을 평소대로 편집하여 오퍼에 대한 컨텐츠를 만듭니다.
   * 기본값이 아닌 경험의 경우 [사용자 지정 오퍼를 추가](#adding-a-custom-offer)하거나 [라이브러리 오퍼를 추가](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library)합니다.

#### 사용자 지정 오퍼 추가 {#adding-a-custom-offer}

타깃팅 모드에서 타깃팅된 구성 요소의 컨텐츠를 작성하여 오퍼를 생성할 수 있습니다. 사용자 지정 오퍼를 생성하는 경우 이 오퍼는 단일 경험에 대한 오퍼로 사용됩니다.

If you decide that the offer can be used for other experiences, you can create a custom offer and [add it to the library](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer-to-a-library). For information about using the Offers console to create a reusable offer, see [Add an Offer to an Offer Library](/help/sites-authoring/offerlib.md#add-an-offer-to-an-offer-library).

1. 오퍼를 추가할 경험을 선택합니다.
1. 구성 요소 메뉴를 표시하려면 오퍼를 추가할 타깃팅된 구성 요소를 클릭하거나 탭합니다.

   ![chlimage_1-21](assets/chlimage_1-21.png)

1. + 아이콘을 클릭하거나 탭합니다.

   기본값 오퍼의 컨텐츠는 현재 경험을 위한 오퍼로 사용됩니다.

1. 오퍼를 클릭하거나 탭하여 오퍼 메뉴를 표시한 다음, 편집 아이콘을 클릭하거나 탭합니다.

   ![](do-not-localize/chlimage_1-2.png)

1. 구성 요소의 컨텐츠를 편집합니다.

#### 오퍼 라이브러리의 오퍼 추가 {#adding-an-offer-from-an-offer-library}

Add an offer from the [offer library](/help/sites-authoring/offerlib.md) to an experience. 현재 타깃팅하는 브랜드의 라이브러리에 있는 오퍼를 추가할 수 있습니다.

기본값 경험에는 라이브러리 오퍼를 추가할 수 없습니다.

1. 오퍼를 추가할 경험을 선택합니다.
1. 구성 요소 메뉴를 표시하려면 오퍼를 추가할 타깃팅된 구성 요소를 클릭하거나 탭합니다.

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. 폴더 아이콘을 클릭하거나 탭합니다.

   ![](do-not-localize/chlimage_1-3.png)

1. 라이브러리에서 오퍼를 선택한 다음, 확인 표시 아이콘을 클릭하거나 탭합니다.

   ![chlimage_1-23](assets/chlimage_1-23.png)

   오퍼 선택기를 사용하면 오퍼를 탐색하거나 필터링할 수 있습니다. 탐색 또는 필터링할 때 오퍼를 정렬하고 오퍼를 표시하는 방법을 변경할 수도 있습니다. 오른쪽 위에 있는 숫자는 현재 라이브러리에서 사용할 수 있는 오퍼의 수를 나타냅니다.

   * Click or tap **Browse** to navigate to another folder. 탐색 창이 열리면 화살표를 클릭하여 폴더로 드릴다운합니다. Click or tap **Browse** again to close the navigation pane.

   ![chlimage_1-24](assets/chlimage_1-24.png)

   * 키워드 또는 태그를 기준으로 오퍼를 필터링하려면 **필터**&#x200B;를 클릭하거나 탭하십시오. 키워드를 입력하고 드롭다운 메뉴에서 태그를 선택합니다. 필터링 창을 닫으려면 다시 **필터**&#x200B;를 클릭하거나 탭합니다.

   ![chlimage_1-25](assets/chlimage_1-25.png)

   * **가장 최근에서 가장 오래된 순으로** 옆에 있는 화살표를 클릭하거나 탭하여 오퍼를 정렬하는 방법을 변경합니다. 오퍼를 가장 최근 오퍼에서 가장 오래된 오퍼순으로 또는 가장 오래된 오퍼에서 가장 최근 오퍼순으로 정렬할 수 있습니다.

   ![chlimage_1-26](assets/chlimage_1-26.png)

   오퍼를 타일이나 목록으로 표시하려면 **다르게 보기** 옆에 있는 아이콘을 클릭하거나 탭하십시오.

   ![chlimage_1-27](assets/chlimage_1-27.png)

#### 라이브러리에 사용자 지정 오퍼 추가 {#adding-a-custom-offer-to-a-library}

사용자 지정 오퍼를 여러 경험을 위한 오퍼로 재사용하려면 [오퍼 라이브러리](/help/sites-authoring/offerlib.md)에 사용자 지정 오퍼를 추가하십시오. 타깃팅 중인 현재 브랜드의 라이브러리에 오퍼를 추가할 수 있습니다.

For information about using the Offers console to create a reusable offer, see [Add an Offer to an Offer Library](/help/sites-authoring/offerlib.md#add-an-offer-to-an-offer-library).

1. 사용자 지정 오퍼를 표시할 경험을 선택합니다.
1. 사용자 지정 오퍼를 클릭하거나 탭하여 오퍼 메뉴를 표시한 다음, **오퍼 라이브러리에 오퍼 저장** 아이콘을 클릭하거나 탭합니다.

   ![](do-not-localize/chlimage_1-4.png)

1. 오퍼에 사용할 이름을 입력하고 오퍼를 추가할 라이브러리를 선택한 다음, 확인 표시 아이콘을 클릭하거나 탭합니다.

#### 라이브러리 오퍼를 사용자 지정 라이브러리로 변환 {#converting-a-library-offer-to-a-custom-library}

다른 경험에 있는 오퍼는 변경하지 않고 라이브러리 오퍼를 사용자 지정 오퍼로 변환하여 현재 경험을 위한 오퍼를 변경할 수 있습니다.

1. 사용자 지정 라이브러리를 표시할 경험을 선택합니다.
1. 사용자 지정 라이브러리를 클릭하거나 탭하여 오퍼 메뉴를 표시한 다음, [인라인 오퍼로 전환] 아이콘을 클릭하거나 탭합니다.

   ![](do-not-localize/chlimage_1-5.png)

#### 라이브러리 오퍼 편집 {#editing-a-library-offer}

오퍼를 편집하려면 타깃팅됨 모드의 경험에서 라이브러리 오퍼를 여십시오. 변경한 내용이 오퍼를 사용하는 모든 경험에 표시됩니다.

1. 사용자 지정 라이브러리를 표시할 경험을 선택합니다.
1. 라이브러리 오퍼를 로컬/사용자 지정 오퍼로 변환합니다. See [Converting a Library Offer to a Custom Library](#converting-a-library-offer-to-a-custom-library).
1. 오퍼의 컨텐츠를 편집합니다.

1. 다시 라이브러리에 저장합니다. See [Adding a Custom Offer to a Library](#adding-a-custom-offer-to-a-library).

## 타겟: 대상 구성 {#target-configuring-the-audiences}

[타깃팅 프로세스](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings)의 타겟 단계에는 만들기 단계에서 작업에 사용한 경험과 대상을 매핑하는 작업이 포함됩니다. 타겟 페이지에는 각 경험이 타깃팅하는 대상이 표시됩니다. 각 경험의 대상을 지정하거나 변경할 수 있습니다. Adobe Target을 사용하는 경우 대상에 대한 트래픽 비율을 특정 경험으로 타깃팅할 수 있도록 해주는 A/B 테스트를 생성할 수도 있습니다.

### AEM 타깃팅 또는 Adobe Target(경험 타깃팅)을 사용하는 경우... {#if-you-are-using-aem-targeting-or-adobe-target-experience-targeting}

대상이 매핑 다이어그램의 왼쪽에 표시되고 경험이 오른쪽에 표시됩니다.

![chlimage_1-28](assets/chlimage_1-28.png)

세그먼트를 사용하여 대상을 정의하십시오. 페이지에 대한 클라우드 구성은 사용자가 사용할 수 있는 세그먼트를 판별합니다. 페이지가 Adobe Target 클라우드 구성과 연결되어 있지 않으면 대상을 정의하는 데 AEM 세그먼트를 사용할 수 있습니다. 페이지가 Adobe Target 클라우드 구성과 연결되어 있으면 타겟 세그먼트를 사용합니다.

타깃팅 엔진에 대한 자세한 내용은 [타깃팅 엔진](/help/sites-authoring/personalization.md#targeting-engine)을 참조하십시오.

한 대상을 두 개 이상의 경험이 사용해서는 안 됩니다. 경험이 다른 경험에 매핑된 대상에 매핑되면 경험 옆에 경고 기호가 나타납니다.

![](do-not-localize/chlimage_1-6.png)

### 경험을 대상(AEM 또는 Adobe Target)과 연결 {#associating-experiences-with-audiences-aem-or-adobe-target}

AEM 타깃팅(또는 Adobe Target 경험 타깃팅)을 사용할 때 경험을 대상과 연결하려면 다음 절차를 사용하십시오.

1. 경험에 매핑된 대상 상자 옆의 드롭다운 화살표를 클릭하거나 탭합니다.
1. (Optional) Click or tap **Edit** and then type a keyword to search for the desired segment.
1. 대상 목록에서 대상을 선택하고 **확인**&#x200B;을 클릭하거나 탭합니다.

### A/B 테스트(Adobe Target)를 사용하는 경우... {#if-you-are-using-a-b-testing-adobe-target}

A/B 테스트 활동이 있는 경우, 대상은 왼쪽에 있고, 각 경험이 표시되는 비율은 가운데에 있으며, 경험은 오른쪽에 있습니다.

비율을 최대 100%까지 변경할 수 있습니다. 대상은 A/B 테스트의 여러 경험에서 사용할 수 있습니다.

![chlimage_1-29](assets/chlimage_1-29.png)

### 대상 및 트래픽 비율을 A/B 테스트와 연결 {#associating-audiences-and-traffic-percentages-with-a-b-testing}

1. 경험에 매핑된 대상의 옆에 있는 드롭다운 화살표를 클릭하거나 탭합니다.
1. (선택 사항) **편집**&#x200B;을 클릭한 다음, 키워드를 입력하여 원하는 세그먼트를 검색합니다.
1. Click or tap **OK.**
1. 대상 트래픽이 각 경험으로 라우팅되는 방법을 구성하려면 비율(%)을 입력하십시오. 합계는 100이어야 합니다.
1. (선택 사항) 경험 이름 옆의 드롭다운 메뉴를 클릭하여 경험 이름을 편집합니다.

## 목표 및 설정: 활동 및 설정 목표 구성 {#goals-settings-configuring-the-activity-and-setting-goals}

The Goals &amp; Settings step of [the targeting process](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings) involves configuring the behavior of the brand activity. 활동의 시작 및 종료 시점과 활동 우선 순위를 지정하십시오. 또한 목표도 추적합니다. 특히, 활동과 관련하여 측정할 항목을 결정할 수 있습니다.

목표 지표는 타깃팅 엔진으로 Adobe Target을 사용하는 경우에만 사용할 수 있습니다. 하나 이상의 목표 지표를 정의해야 합니다. Adobe Analytics가 구성되어 있고 A4T Analytics 클라우드 구성이 있는 경우, 보고 소스를 Adobe Target으로 할지 또는 Adobe Analytics으로 할지를 선택할 수 있습니다.

목표 지표는 게시된 캠페인에 대해서만 측정됩니다.

타깃팅 엔진으로 AEM을 사용하는 경우:

![chlimage_1-30](assets/chlimage_1-30.png)

타깃팅 엔진으로 Adobe Target을 사용하는 경우:

![chlimage_1-31](assets/chlimage_1-31.png)

타깃팅 엔진으로 Adobe Target을 사용하고 계정에 대해 A4T Analytics가 구성되어 있다면 추가 **보고 소스** 드롭다운 메뉴가 표시됩니다.

![chlimage_1-32](assets/chlimage_1-32.png)

다음 성공 지표를 사용할 수 있습니다(게시용으로만 사용됨).

<table>
 <tbody>
  <tr>
   <td><strong>변환</strong></td>
   <td><p>테스트되는 경험의 일부를 클릭한 방문자 비율. 전환은 방문자당 한 번씩 또는 방문자가 전환을 완료할 때마다 계산됩니다. 전환 지표는 다음 중 하나로 설정됩니다.</p>
    <ul>
     <li><strong>페이지</strong> 보기 - URL을 선택한 다음 <strong>URL 또는 여러 URL을</strong> 정의하거나, URL이 포함된 <strong></strong> 것을 선택한 다음 경로나 키워드를 추가하여 대상이 본 페이지를 정의할 수있습니다.</li>
     <li><strong>mbox</strong> 조회 - mbox의 이름을 입력하여 대상이 본 mbox를 정의할 수 있습니다. You can enter multiple mboxes by clicking <strong>Add an Mbox</strong>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>수입</strong></td>
   <td><p>방문으로 생성된 매출입니다. 다음 매출 지표 중에서 선택할 수 있습니다.</p>
    <ul>
     <li>방문자당 매출(RPV)</li>
     <li>AOV(평균 주문 가격)</li>
     <li>총 판매 수 </li>
     <li>주문</li>
    </ul> <p>이러한 옵션의 경우 mbox를 보았는지 여부는 목표에 도달했음을 나타냅니다. mbox 또는 여러 mbox를 정의할 수 있습니다.</p> </td>
  </tr>
  <tr>
   <td><strong>참여</strong></td>
   <td><p>세 가지 유형의 참여를 측정할 수 있습니다.</p>
    <ul>
     <li>페이지 조회수</li>
     <li>사용자 지정 점수</li>
     <li>사이트에서 보낸 시간</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

또한 성공 지표의 수를 계산하는 방법을 결정할 수 있는 고급 설정이 있습니다. 선택 사항에는 노출당 지표나 방문자당 한 번씩 계산하는 작업과, 활동에 사용자를 유지할지 여부를 선택하거나 사용자를 제거하는 작업이 포함됩니다.

고급 설정을 사용하여 사용자가 목표 지표를 찾은 **후** 발생하는 일을 결정하십시오. 다음 표는 사용 가능한 선택 사항을 보여줍니다.

<table>
 <tbody>
  <tr>
   <td><strong>사용자가 이 목표 지표를 찾은 후..</strong></td>
   <td><strong>다음 중 하나를 선택합니다.</strong></td>
  </tr>
  <tr>
   <td><strong>증분 카운트 및 사용자를 활동에 유지</strong></td>
   <td>카운트가 증가되는 방식을 지정합니다.
    <ul>
     <li>참가자당 한 번</li>
     <li>페이지 새로 고침 제외 노출 횟수</li>
     <li>모든 노출</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>증분 카운트, 사용자 해제 및 재입력 허용</strong></td>
   <td>활동에 다시 입장할 경우 방문자가 보는 경험을 선택합니다.
    <ul>
     <li>동일한 경험</li>
     <li>무작위 경험</li>
     <li>보이지 않는 경험</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>증분 카운트, 릴리스 사용자 및 막대 재입력</strong></td>
   <td>사용자가 활동 컨텐츠 대신 보게 되는 내용을 결정합니다.
    <ul>
     <li>추적 없이 동일한 경험</li>
     <li>기본 컨텐츠 또는 기타 활동 컨텐츠</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

성공 지표에 대한 자세한 내용은 [Adobe Target 설명서](https://docs.adobe.com/content/help/en/target/using/activities/success-metrics/success-metrics.html)를 참조하십시오.

### 설정 구성(AEM 타깃팅) {#configuring-settings-aem-targeting}

AEM 타깃팅을 사용할 경우 설정을 구성하려면 다음을 수행하십시오.

1. 활동이 시작되는 시점을 지정하려면 **시작** 드롭다운 메뉴를 사용하여 다음 값 중 하나를 선택하십시오.

   * **활성화 시**: 타깃팅된 컨텐츠가 포함된 페이지가 활성화되면 활동이 시작됩니다.
   * **지정한 날짜 및 시간**: 구체적인 시점입니다. 이 선택 사항을 선택하면 달력 아이콘을 클릭하거나 탭하고 날짜를 선택한 다음, 활동을 시작할 시간을 지정하십시오.

1. 활동이 끝나는 시점을 지정하려면 **끝** 드롭다운 메뉴를 사용하여 다음 값 중 하나를 선택하십시오.

   * **비활성화 시**: 타깃팅된 컨텐츠가 포함된 페이지가 비활성화되면 활동이 끝납니다.
   * **지정한 날짜 및 시간**: 구체적인 시점입니다. 이 선택 사항을 선택하면 달력 아이콘을 클릭하거나 탭하고 날짜를 선택한 다음, 활동을 끝낼 시간을 지정하십시오.

1. 활동의 우선 순위를 지정하려면 슬라이더를 사용하여 **낮음**, **일반** 또는 **높음**&#x200B;을 선택합니다.

### 목표 및 설정 구성(Adobe Target) {#configuring-goals-settings-adobe-target}

Adobe Target을 사용할 경우 목표 및 설정을 구성하려면 다음을 수행하십시오.

1. 활동이 시작되는 시점을 지정하려면 **시작** 드롭다운 메뉴를 사용하여 다음 값 중 하나를 선택하십시오.

   * **활성화 시**: 타깃팅된 컨텐츠가 포함된 페이지가 활성화되면 활동이 시작됩니다.
   * **지정한 날짜 및 시간**: 구체적인 시점입니다. 이 선택 사항을 선택하면 달력 아이콘을 클릭하거나 탭하고 날짜를 선택한 다음, 활동을 시작할 시간을 지정하십시오.

1. 활동이 끝나는 시점을 지정하려면 **끝** 드롭다운 메뉴를 사용하여 다음 값 중 하나를 선택하십시오.

   * **비활성화 시**: 타깃팅된 컨텐츠가 포함된 페이지가 비활성화되면 활동이 끝납니다.
   * **지정한 날짜 및 시간**: 구체적인 시점입니다. 이 선택 사항을 선택하면 달력 아이콘을 클릭하거나 탭하고 날짜를 선택한 다음, 활동을 끝낼 시간을 지정하십시오.

1. 활동의 우선 순위를 지정하려면 슬라이더를 사용하여 **낮음**, **일반** 또는 **높음**&#x200B;을 선택합니다.
1. Adobe Target 계정으로 Adobe Anaytics를 구성했다면 **보고 소스** 드롭다운 메뉴가 표시됩니다. 소스로 **Adobe Target**&#x200B;이나 **Adobe Analytics**&#x200B;를 선택하십시오.

   **Adobe Analytics**&#x200B;를 선택하는 경우 회사와 보고서 세트를 선택하십시오. **Adobe Target**&#x200B;을 선택하는 경우에는 아무 작업도 필요하지 않습니다.

   ![chlimage_1-33](assets/chlimage_1-33.png)

1. **목표 지표** 영역의 **기본 목표** 아래에서 추적하려는 성공 지표(전환, 수입, 참여)를 선택하고 지표를 측정하는 방법(또는 목표에 도달했음을 나타내기 위해 대상이 취하는 조치)을 입력합니다. 이전 표에서 목표 지표의 정의를 참조하고 성공 지표에 대해 [Adobe Target 설명서](https://docs.adobe.com/content/help/en/target/using/activities/success-metrics/success-metrics.html)를 참조하십시오.

   You can rename the goal by clicking the three dots in the upper right corner and selecting **Rename**.

   모든 필드를 지워야 하는 경우 오른쪽 위 모서리에 있는 세 개의 점을 클릭하고 **모든 필드 지우기**&#x200B;를 선택하십시오.

   모든 지표에는 사용자가 정의할 수 있는 고급 설정도 있습니다. 이 고급 설정에 액세스하려면 **고급 설정**&#x200B;을 선택하십시오. See definition of how success metrics are counted in previous table and see [Adobe Target documentation](https://docs.adobe.com/content/help/en/target/using/activities/success-metrics/success-metrics.html).

   >[!NOTE]
   정의된 목표가 하나 이상 있어야 합니다.

   ![chlimage_1-34](assets/chlimage_1-34.png)

   >[!NOTE]
   지표에 누락된 정보가 있으면 빨간색 선이 지표를 둘러쌉니다.

1. 성공 지표를 더 구성하려면 **새 지표 추가**&#x200B;를 클릭합니다.

   ![chlimage_1-35](assets/chlimage_1-35.png)

   >[!NOTE]
   세 개의 점을 클릭하거나 탭하고 **삭제**&#x200B;를 클릭하거나 탭하여 목표를 추가로 제거할 수 있습니다. AEM을 사용하려면 정의된 목표가 하나 이상 있어야 합니다.

1. If you want more control over how success metrics are counted, click or tap **Advanced Settings** to access those.
1. **저장**&#x200B;을 클릭합니다.

구성 후에는 Adobe Target을 사용하는(경험 또는 A/B 테스트 타깃팅) [활동의 성과를 볼](/help/sites-authoring/activitylib.md#viewing-performance-and-converting-winning-experiences-a-b-test) 수 있습니다. 또한 A/B 테스트 타깃팅을 사용하는 경우에는 [우승자를 전환](/help/sites-authoring/activitylib.md#viewing-performance-and-converting-winning-experiences-a-b-test)할 수 있습니다.

## 경험 시뮬레이션 {#simulating-an-experience}

방문자의 경험을 시뮬레이션하여 페이지 컨텐츠가 타깃팅된 컨텐츠의 디자인에 따라 예상대로 표시되는지 확인하십시오. 시뮬레이션 시 다른 사용자 프로필을 로드하고 해당 사용자에 대한 타깃팅된 컨텐츠를 확인하십시오.

다음 기준은 방문자의 경험을 시뮬레이션할 때 나타나는 컨텐츠를 결정합니다.

* 사용자의 세션 저장소에 있는 데이터(Context Hub를 통해)
* ](/help/sites-authoring/activitylib.md)설정 상태의 활동[
* [세그먼트를 정의하는 규칙](/help/sites-administering/campaign-segmentation.md)
* 타겟 구성 요소에 있는 경험의 컨텐츠
* [타깃팅 엔진의 구성](/help/sites-authoring/activitylib.md)

프로필을 로드할 때 페이지에 예기치 않은 컨텐츠가 나타나면 이 목록에 있는 각 항목의 구성을 확인하십시오.

>[!NOTE]
A/B 테스트를 사용하는 경우에는 시뮬레이션할 때 경험이 트래픽 비율을 기반으로 표시됩니다. 이것은 Adobe Target에 의해 제어되므로 이로 인해 작성자가 예상하지 못한 결과가 발생할 수 있습니다. (작성자 활동은 시뮬레이션 중에 재평가를 허용하는 특정 설정과 동기화됩니다.) 작성자가 트래픽 설정에 따라 다른 경험을 보려면 새로 고침을 해야 할 수 있습니다.

방문자의 경험을 시뮬레이션하려면 다음 도구를 사용하십시오.

* 타깃팅 모드의 시뮬레이션 활동: 현재 Context Hub에서 선택된 사용자에 대한 오퍼가 페이지에 표시됩니다. 사용자를 타깃팅하는 오퍼를 편집할 수 있습니다.
* 미리 보기 모드: Context Hub를 사용하여 경험이 기반으로 하는 세그먼트의 기준을 충족하는 사용자 및 위치를 선택하십시오. Context Hub 선택 내용이 변경되면 타깃팅된 컨텐츠가 그에 따라 변경됩니다.

1. To switch to Preview mode, on the toolbar click or tap **Preview**.
1. 도구 모음에서 Context Hub 아이콘을 클릭하거나 탭합니다.

   ![](do-not-localize/chlimage_1-7.png)

1. Context Hub를 사용하여 컨텍스트 속성을 변경합니다. 예를 들어 다른 사용자를 선택하려면 [모습] 속성을 클릭하거나 탭하십시오.

   ![chlimage_1-36](assets/chlimage_1-36.png)

   페이지가 현재 컨텍스트에 대해 타깃팅되는 컨텐츠를 표시하도록 변경됩니다.

1. 표시되는 오퍼에 변경 작업을 수행하려면 타깃팅 모드로 전환합니다. 시뮬레이션 활동을 선택한 상태에서 미리 보기 모드에서 구성한 컨텍스트에 대한 오퍼를 편집하십시오.

## 타겟 구성 요소 선택 사항 구성 {#configuring-target-component-options}

다음 두 가지 방법 중 하나로 구성 요소의 선택 사항에 액세스하여 타겟 구성 요소를 사용자 지정할 수 있습니다.

1. 구성 요소를 타깃팅했으면 타겟 구성 요소에서 구성 요소를 클릭하거나 탭한 다음, 설정 아이콘(톱니바퀴)을 클릭하거나 탭합니다.

   ![](do-not-localize/chlimage_1-8.png)

   AEM에 타겟 구성 요소 선택 사항 창이 표시됩니다.

   ![chlimage_1-37](assets/chlimage_1-37.png)

1. 또는 전체 화면 모드에서 이러한 설정에 액세스하려면 타겟 구성 요소 선택 사항 창에서 전체 화면 아이콘을 클릭하거나 탭합니다.

   ![](do-not-localize/chlimage_1-9.png)

   AEM에 전체 화면으로 타겟 구성 요소 선택 사항 창이 표시됩니다.

   ![chlimage_1-38](assets/chlimage_1-38.png)

1. 다음 표에 설명된 대로 타겟 구성 요소 설정을 구성합니다.

<table>
 <tbody>
  <tr>
   <td><strong>옵션</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td><strong>위치</strong></td>
   <td><p>위치는 타깃팅된 컨텐츠 위치에 이름을 지정하고 오퍼를 배치할 페이지의 위치(또는 위치 또는 구성 요소)와 오퍼를 연결하는 문자열입니다.</p> <p>이 필드는 일반 값입니다.</p> <p>오퍼를 구성 요소에 넣으면 오퍼는 위치 ID를 기억합니다. 페이지가 실행되면 엔진은 사용자의 세그먼트를 평가하고 이를 기반으로 하여 표시해야 하는 활성 캠페인의 경험을 해결합니다. 그런 다음, 페이지에서 위치 ID를 확인하고 해당 위치 ID를 사용하는 오퍼를 위치 ID에 대응시킵니다.</p> </td>
  </tr>
  <tr>
   <td><strong>엔진</strong></td>
   <td>사용할 엔진에 <strong>따라 클라이언트 측 규칙(추적 없음), Adobe Target, ContextHub </strong>및<strong> Adobe Campaign </strong>을 선택합니다.</td>
  </tr>
 </tbody>
</table>

Adobe Target을 엔진으로 선택하는 경우:

![chlimage_1-39](assets/chlimage_1-39.png)

<table>
 <tbody>
  <tr>
   <td><strong>옵션</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td><strong>정확한 타겟 지정</strong></td>
   <td><p>정확한 타깃팅을 활성화하면 구성 요소에 요청을 Adobe Target으로 보내기 전에 클라이언트 컨텍스트 또는 컨텍스트 허브 데이터를 사용할 수 있을 때까지 대기하도록 지시합니다. 이것으로 로드 시간이 늘어날 수 있습니다. 작성을 위해 항상 정확한 타깃팅이 활성화되어 있습니다.</p> <p>If you select the <strong>Accurate targeting</strong> check box, the mbox performs an <code>mboxDefine</code> first and an <code>mboxUpdate</code> later resulting in an Ajax request once the data is available.</p> <p>If you do not select the <strong>Accurate targeting</strong> check box, the mbox performs an <code>mboxCreate</code> resulting in a synchronous request right away (in this case, not all context data may be available yet).</p> <p><strong>참고:</strong> 특정 구성 요소에 대해 정확한 타깃팅을 활성화하거나 비활성화해도 전체적으로 설정한 설정에 영향을 주지 않습니다. 구성 요소에서 [정확한 타겟 지정]을 선택하여 전역 설정을 항상 무시할 수 있습니다.</p> </td>
  </tr>
  <tr>
   <td><strong>해결된 세그먼트 포함</strong></td>
   <td><p>이 확인란을 선택하면 mbox 호출의 모든 해결된 세그먼트와 페이지 및 프레임워크에 구성된 모든 매개 변수가 포함됩니다.</p> <p>이 기능은 AEM 세그먼트를 동기화하는 XML API가 있는 상황에서만 작동합니다. Adobe Target으로 처리되지 않는 AEM의 세그먼트(예: 스크립트 세그먼트)가 있다면 이 선택 사항을 사용할 경우 AEM에서 세그먼트를 해결하고 세그먼트가 활성 상태인 Adobe Target에 정보를 전송할 수 있습니다.</p> </td>
  </tr>
  <tr>
   <td><strong>상속된 컨텍스트 매개 변수</strong></td>
   <td>Adobe Target 프레임워크에서 상속된 컨텍스트 매개 변수(있는 경우)를 선택한 페이지와 연관시킵니다.</td>
  </tr>
  <tr>
   <td><strong>컨텍스트 매개 변수</strong></td>
   <td>추가 컨텍스트 매개 변수 <strong>를 구성하려면 필드</strong> 추가를 클릭하거나 탭하십시오(Target 프레임워크에서 사용 가능한 것과 동일함). Context parameters added to the component apply <i>only</i> to the component and not to other component as would be the case if you added context parameters directly to the framework.</td>
  </tr>
  <tr>
   <td><strong>정적 매개 변수</strong></td>
   <td>추가 정적 매개 변수를 구성하려면 <strong>필드</strong> 추가를 클릭하거나 탭하십시오(Target 프레임워크에서 사용 가능한 것과 동일). Static parameters added to the component apply <i>only</i> to the component and not to other component as would be the case if you added static parameters directly to the framework. 정적 매개 변수는 컨텍스트(컨텐츠 허브의 Client Context)에서 가져오지 않습니다.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
구성 요소를 선택하여 이것을 타깃팅이 가능하도록 만들면 AEM도 이 구성 요소를 교체하고 Adobe Target 구성 요소를 주입합니다. (Adobe Target 구성 요소는 수동으로 페이지에 추가할 때에만 사용되는 것이 아니라, 기존 구성 요소를 타깃팅할 때에도 사용됩니다.)

Client Context(클라이언트측)를 엔진으로 선택하는 경우:

![chlimage_1-40](assets/chlimage_1-40.png)

<table>
 <tbody>
  <tr>
   <td><strong>옵션</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td><strong>클라이언트측 옵션 - 전략</strong></td>
   <td><p>다음 중 하나를 선택합니다.</p>
    <ul>
     <li><strong>첫 번째</strong>: 캠페인에서 순서가 지정된 목록에서 가장 높은 경험입니다.</li>
     <li><strong>임의</strong>: 모든 경험이 사용됩니다.</li>
     <li><strong>클릭스트림 점수</strong>: 클라이언트 컨텍스트에서 추적된 태그 및 관련 태그 히트가 사용됩니다. 티저 페이지에 정의된 태그의 조회수가 비교됩니다.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

AEM을 Adobe Campaign과 통합하는 경우 엔진으로 **Adobe Campaign**&#x200B;을 선택합니다. 자세한 내용은 [Adobe Campaign과 AEM 통합](/help/sites-administering/campaign.md)을 참조하십시오.

타깃팅에 ContextHub를 사용하는 경우에는 엔진으로 **ContextHub**&#x200B;를 선택하십시오. [ContextHub 구성](/help/sites-administering/contexthub-config.md)을 참조하십시오.

