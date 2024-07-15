---
title: Adobe Campaign 6.1 및 Adobe Campaign Standard 작업
description: AEM에서 이메일 콘텐츠를 만들고 Adobe Campaign 이메일에서 처리할 수 있습니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: a4717cb8-b70c-4150-b816-35e9b871e792
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 2%

---

# Adobe Campaign 6.1 및 Adobe Campaign Standard 작업{#working-with-adobe-campaign-and-adobe-campaign-standard}

AEM에서 이메일 콘텐츠를 만들고 Adobe Campaign 이메일에서 처리할 수 있습니다. 이렇게 하려면 다음을 수행해야 합니다.

1. Adobe Campaign 관련 템플릿으로 AEM 뉴스레터를 생성할 수 있습니다.
1. 모든 기능에 액세스하려면 콘텐츠를 편집하기 전에 [Adobe Campaign 서비스](#selectingtheadobecampaigncloudservice)를 선택하십시오.
1. 콘텐츠를 편집합니다.
1. 콘텐츠의 유효성을 검사합니다.

그런 다음 콘텐츠를 Adobe Campaign의 게재와 동기화할 수 있습니다. 자세한 지침은 이 문서에 설명되어 있습니다.

>[!NOTE]
>
>이 기능을 사용하려면 먼저 [Adobe Campaign](/help/sites-administering/campaignonpremise.md) 또는 [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md)과 통합되도록 AEM을 구성해야 합니다.

## Adobe Campaign을 통해 이메일 콘텐츠 전송 {#sending-email-content-via-adobe-campaign}

AEM 및 Adobe Campaign을 구성한 후 AEM에서 직접 이메일 게재 콘텐츠를 만든 다음 Adobe Campaign에서 처리할 수 있습니다.

AEM에서 Adobe Campaign 콘텐츠를 만들 때 모든 기능에 액세스하려면 콘텐츠를 편집하기 전에 Adobe Campaign 서비스에 연결해야 합니다.

두 가지 가능한 경우가 있습니다.

* 콘텐츠는 Adobe Campaign의 게재와 동기화할 수 있습니다. 이렇게 하면 게재에서 AEM 컨텐츠를 사용할 수 있습니다.
* (Adobe Campaign 온프레미스만 해당) 콘텐츠를 Adobe Campaign으로 직접 전송할 수 있으며 이렇게 하면 자동으로 새 이메일 게재가 생성됩니다. 이 모드에는 제한이 있습니다.

자세한 지침은 이 문서에 설명되어 있습니다.

### 새 이메일 콘텐츠 만들기 {#creating-new-email-content}

>[!NOTE]
>
>전자 메일 템플릿을 추가할 때는 **/content/campaigns**&#x200B;에 추가하여 사용할 수 있도록 해야 합니다.
>

1. AEM에서 **웹 사이트** 폴더를 선택한 다음 탐색기를 탐색하여 이메일 캠페인이 관리되는 위치를 찾습니다. 다음 예에서는 관련 노드가 **웹 사이트** > **캠페인** > **Geometrixx Outdoors** > **이메일 캠페인**&#x200B;입니다.

   >[!NOTE]
   >
   >[전자 메일 샘플은 Geometrixx](/help/sites-developing/we-retail.md#weretail)에서만 사용할 수 있습니다. 패키지 공유에서 샘플 Geometrixx 콘텐츠를 다운로드합니다.

   ![chlimage_1-172](assets/chlimage_1-172.png)

1. 새 전자 메일 콘텐츠를 만들려면 **새로 만들기** > **새 페이지**&#x200B;를 선택하십시오.
1. Adobe Campaign과 관련된 사용 가능한 템플릿 중 하나를 선택한 다음 페이지의 일반 속성을 채웁니다. 기본적으로 다음 세 가지 템플릿을 사용할 수 있습니다.

   * **Adobe Campaign 전자 메일(AC 6.1)**: 배달을 위해 Adobe Campaign 6.1로 보내기 전에 미리 정의된 템플릿에 콘텐츠를 추가할 수 있습니다.
   * **ACS(Adobe Campaign Email)**: 콘텐츠를 게재하기 위해 Adobe Campaign Standard으로 보내기 전에 미리 정의된 템플릿에 콘텐츠를 추가할 수 있습니다.

   ![chlimage_1-173](assets/chlimage_1-173.png)

1. 전자 메일 또는 뉴스레터를 만들려면 **만들기**&#x200B;를 클릭하세요.

### Adobe Campaign 클라우드 서비스 및 템플릿 선택 {#selecting-the-adobe-campaign-cloud-service-and-template}

Adobe Campaign과 통합하려면 페이지에 Adobe Campaign 클라우드 서비스를 추가해야 합니다. 이렇게 하면 개인화 및 기타 Adobe Campaign 정보에 액세스할 수 있습니다.

또한 Adobe Campaign 템플릿을 선택하고 제목을 변경한 다음 HTML에서 이메일을 보지 않을 사용자에 대한 일반 텍스트 컨텐츠를 추가해야 할 수 있습니다.

1. 사이드 킥에서 **페이지** 탭을 선택한 다음 **페이지 속성을 선택합니다.**
1. 팝업 창의 **클라우드 서비스** 탭에서 **서비스 추가**&#x200B;를 선택하여 Adobe Campaign 서비스를 추가하고 **확인**&#x200B;을 클릭합니다.

   ![chlimage_1-174](assets/chlimage_1-174.png)

1. 드롭다운 목록에서 Adobe Campaign 인스턴스와 일치하는 구성을 선택한 다음 **확인**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >클라우드 서비스를 추가한 후 **확인** 또는 **적용**&#x200B;을 클릭하세요. 이렇게 하면 **Adobe Campaign** 탭이 제대로 작동합니다.

1. 기본 **메일** 템플릿 이외의 특정 이메일 게재 템플릿(Adobe Campaign)을 적용하려면 **페이지 속성**&#x200B;을 다시 선택합니다. **Adobe Campaign** 탭에서 관련 Adobe Campaign 인스턴스에 전자 메일 게재 템플릿의 내부 이름을 입력합니다.

   Adobe Campaign Standard에서 템플릿은 **AEM 콘텐츠가 포함된 게재**&#x200B;입니다. Adobe Campaign 6.1에서 템플릿은 **AEM 콘텐츠가 포함된 이메일 게재**&#x200B;입니다.

   템플릿을 선택하면 AEM에서 **Adobe Campaign 뉴스레터** 구성 요소를 자동으로 활성화합니다.

### 이메일 콘텐츠 편집 {#editing-email-content}

클래식 사용자 인터페이스 또는 터치에 적합한 사용자 인터페이스에서 이메일 콘텐츠를 편집할 수 있습니다.

1. 도구 상자에서 **페이지 속성** > **전자 메일**&#x200B;을 선택하여 전자 메일의 제목과 텍스트 버전을 입력합니다.

   ![chlimage_1-175](assets/chlimage_1-175.png)

1. 사이드 킥에서 사용할 수 있는 요소에서 원하는 요소를 추가하여 이메일 콘텐츠를 편집합니다. 이렇게 하려면 드래그 앤 드롭하십시오. 그런 다음 편집할 요소를 두 번 클릭합니다.

   예를 들어 개인화 필드가 포함된 텍스트를 추가할 수 있습니다.

   ![chlimage_1-176](assets/chlimage_1-176.png)

   Adobe Campaign 뉴스레터/이메일 캠페인에 사용할 수 있는 구성 요소에 대한 설명은 [Adobe Campaign 구성 요소](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md)를 참조하십시오.

   ![chlimage_1-177](assets/chlimage_1-177.png)

### 개인화 삽입 {#inserting-personalization}

콘텐츠를 편집할 때 다음을 삽입할 수 있습니다.

* Adobe Campaign 컨텍스트 필드. 받는 사람의 데이터(예: 이름, 성 또는 대상 차원의 모든 데이터)에 따라 조정될 텍스트 내에 삽입할 수 있는 필드입니다.
* Adobe Campaign 개인화 블록. 브랜드 로고나 미러 페이지 링크와 같이 수신자의 데이터와 관련이 없는 사전 정의된 콘텐츠 블록입니다.

Campaign 구성 요소에 대한 자세한 설명은 [Adobe Campaign 구성 요소](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md)를 참조하십시오.

>[!NOTE]
>
>* Adobe Campaign **프로필** 타겟팅 차원의 필드만 고려됩니다.
>* **사이트**&#x200B;에서 속성을 볼 때 Adobe Campaign 컨텍스트 필드에 액세스할 수 없습니다. 편집하는 동안 이메일에서 직접 액세스할 수 있습니다.
>

1. 새 **뉴스레터** > **텍스트 및 Personalization(캠페인)** 구성 요소를 삽입합니다.
1. 구성 요소를 두 번 클릭하여 엽니다. **편집** 창에는 개인화 요소를 삽입할 수 있는 기능이 있습니다.

   >[!NOTE]
   >
   >사용 가능한 컨텍스트 필드는 Adobe Campaign의 **프로필** 타겟팅 차원에 해당합니다.
   >
   >[AEM 페이지를 Adobe Campaign 전자 메일에 연결](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#linkinganaempagetoanadobecampaignemail)을 참조하세요.

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. 개인 프로필의 데이터를 사용하여 개인화 필드를 테스트하려면 사이드 킥에서 **Client Context**&#x200B;을(를) 선택하십시오.

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. 창이 나타나고 원하는 담당자를 선택할 수 있습니다. 개인화 필드는 선택한 프로필의 데이터로 자동으로 대체됩니다.

   ![chlimage_1-180](assets/chlimage_1-180.png)

### 뉴스레터 미리 보기 {#previewing-a-newsletter}

뉴스레터의 모습을 미리 보고 개인화를 미리 볼 수 있습니다.

1. 미리 보려는 뉴스레터를 열고 미리 보기(돋보기)를 클릭하여 사이드 킥을 축소합니다.
1. 이메일 클라이언트 아이콘 중 하나를 클릭하여 각 이메일 클라이언트에서 뉴스레터의 모습을 확인할 수 있습니다.

   ![chlimage_1-181](assets/chlimage_1-181.png)

1. 사이드 킥을 확장하여 다시 편집을 시작합니다.

### AEM에서 콘텐츠 승인 {#approving-content-in-aem}

콘텐츠가 완료되면 승인 프로세스를 시작할 수 있습니다. 도구 상자의 **워크플로** 탭으로 이동하여 **Adobe Campaign에 대해 승인** 워크플로를 선택합니다.

이 기본 워크플로에는 개정 후 승인 또는 개정 후 거부라는 두 단계가 있습니다. 그러나 이 워크플로우는 보다 복잡한 프로세스에 확장 및 조정될 수 있습니다.

![chlimage_1-182](assets/chlimage_1-182.png)

Adobe Campaign에 대한 콘텐츠를 승인하려면 사이드 킥에서 **워크플로**&#x200B;를 선택하고 **Adobe Campaign에 대해 승인**&#x200B;을 선택하여 워크플로를 적용한 다음 **워크플로 시작**&#x200B;을 클릭합니다. 단계를 진행하고 콘텐츠를 승인합니다. 마지막 워크플로 단계에서 **승인** 대신 **거부**&#x200B;를 선택하여 콘텐츠를 거부할 수도 있습니다.

![chlimage_1-183](assets/chlimage_1-183.png)

콘텐츠가 승인되면 Adobe Campaign에서 승인된 것으로 표시됩니다. 그런 다음 이메일을 보낼 수 있습니다.

Adobe Campaign Standard:

![chlimage_1-184](assets/chlimage_1-184.png)

Adobe Campaign 6.1에서:

![chlimage_1-185](assets/chlimage_1-185.png)

>[!NOTE]
>
>승인되지 않은 컨텐츠는 Adobe Campaign의 게재와 동기화할 수 있지만 게재를 실행할 수 없습니다. 승인된 콘텐츠만 Campaign 게재를 통해 보낼 수 있습니다.

## Adobe Campaign Standard 및 Adobe Campaign 6.1과 AEM 연결 {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign}

>[!NOTE]
>
>자세한 내용은 표준 작성 문서에서 [Adobe Campaign 6.1 및 Adobe Campaign Standard 작업](/help/sites-authoring/campaign.md)에서 [Adobe Campaign Standard 및 Adobe Campaign 6.1과 AEM 연결](/help/sites-authoring/campaign.md#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic)을 참조하십시오.
