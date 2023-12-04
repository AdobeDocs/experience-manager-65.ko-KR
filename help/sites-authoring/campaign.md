---
title: Adobe Campaign Classic 및 Adobe Campaign Standard 작업
description: AEM에서 이메일 콘텐츠를 만들고 Adobe Campaign 이메일에서 처리할 수 있습니다
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: d7e4d424-0ca7-449f-95fb-c4fe19dd195d
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '2770'
ht-degree: 2%

---

# Adobe Campaign Classic 및 Adobe Campaign Standard 작업{#working-with-adobe-campaign-classic-and-adobe-campaign-standard}

AEM에서 이메일 콘텐츠를 만들고 Adobe Campaign 이메일에서 처리할 수 있습니다. 이렇게 하려면 다음을 수행해야 합니다.

1. Adobe Campaign 관련 템플릿으로 AEM 뉴스레터를 생성할 수 있습니다.
1. 선택 [Adobe Campaign 서비스](#selecting-the-adobe-campaign-cloud-service-and-template) 모든 기능에 액세스하기 위해 컨텐츠를 편집하기 전에
1. 콘텐츠를 편집합니다.
1. 콘텐츠의 유효성을 검사합니다.

그런 다음 콘텐츠를 Adobe Campaign의 게재와 동기화할 수 있습니다. 자세한 지침은 이 문서에 설명되어 있습니다.

참조: [AEM에서 Adobe Campaign Forms 만들기](/help/sites-authoring/adobe-campaign-forms.md).

>[!NOTE]
>
>이 기능을 사용하려면 먼저 AEM을 다음 중 하나와 통합하도록 구성해야 합니다 [Adobe Campaign](/help/sites-administering/campaignonpremise.md) 또는 [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md).

## Adobe Campaign을 통해 이메일 콘텐츠 전송 {#sending-email-content-via-adobe-campaign}

AEM 및 Adobe Campaign을 구성한 후 AEM에서 직접 이메일 게재 콘텐츠를 만든 다음 Adobe Campaign에서 처리할 수 있습니다.

AEM에서 Adobe Campaign 콘텐츠를 만들 때 모든 기능에 액세스하려면 콘텐츠를 편집하기 전에 Adobe Campaign 서비스에 연결해야 합니다.

두 가지 가능한 경우가 있습니다.

* 콘텐츠는 Adobe Campaign의 게재와 동기화할 수 있습니다. 이렇게 하면 게재에서 AEM 컨텐츠를 사용할 수 있습니다.
* (Adobe Campaign Classic만 해당) 콘텐츠를 Adobe Campaign으로 직접 전송할 수 있으며, 이렇게 하면 자동으로 새 이메일 게재가 생성됩니다. 이 모드에는 제한이 있습니다.

자세한 지침은 이 문서에 설명되어 있습니다.

### 새 이메일 콘텐츠 만들기 {#creating-new-email-content}

>[!NOTE]
>
>이메일 템플릿을 추가할 때는 아래에 추가해야 합니다. **/content/campaigns** 사용할 수 있도록 설정합니다.

#### 새 이메일 콘텐츠 만들기 {#creating-new-email-content-1}

1. AEM에서 선택 **사이트** 그러면 **캠페인**&#x200B;그런 다음 이메일 캠페인이 관리되는 위치로 이동합니다. 다음 예제에서 경로는 **사이트** > **캠페인** > **Geometrixx Outdoors** > **이메일 캠페인**.

   >[!NOTE]
   >
   >[이메일 샘플은 Geometrixx에서만 사용할 수 있습니다.](/help/sites-developing/we-retail.md). 패키지 공유에서 샘플 Geometrixx 콘텐츠를 다운로드합니다.

   ![chlimage_1-15](assets/chlimage_1-15a.png)

1. 선택 **만들기** 그러면 **페이지 만들기**.
1. 연결 중인 Adobe Campaign과 관련된 사용 가능한 템플릿 중 하나를 선택한 다음 을 클릭합니다. **다음**. 기본적으로 다음 세 가지 템플릿을 사용할 수 있습니다.

   * **Adobe Campaign Classic 이메일**: 콘텐츠를 Adobe Campaign Classic에 전송하여 전달하기 전에 사전 정의된 템플릿(2개 열)에 추가할 수 있습니다.
   * **Adobe Campaign Standard 이메일**: 콘텐츠를 Adobe Campaign Standard에 전송하여 전달하기 전에 사전 정의된 템플릿(2개 열)에 추가할 수 있습니다.

1. 다음을 입력합니다. **제목** 및 선택적으로 **설명** 및 클릭 **만들기**. 제목을 이메일 편집 중에 덮어쓰지 않는 한 뉴스레터/이메일의 제목으로 사용합니다.

### Adobe Campaign 클라우드 서비스 및 템플릿 선택 {#selecting-the-adobe-campaign-cloud-service-and-template}

Adobe Campaign과 통합하려면 페이지에 Adobe Campaign 클라우드 서비스를 추가해야 합니다. 이렇게 하면 개인화 및 기타 Adobe Campaign 정보에 액세스할 수 있습니다.

또한 Adobe Campaign 템플릿을 선택하고 제목을 변경한 다음 HTML에서 이메일을 보지 않을 사용자에 대한 일반 텍스트 컨텐츠를 추가해야 할 수 있습니다.

다음 중 하나에서 클라우드 서비스를 선택할 수 있습니다. **사이트** 이메일/뉴스레터를 작성한 후 탭이나 을(를) 클릭합니다.

에서 클라우드 서비스 선택 **사이트** 탭은 권장되는 방법입니다. 이메일/뉴스레터에서 클라우드 서비스를 선택하려면 해결 방법이 필요합니다.

다음에서 **사이트** 페이지:

1. AEM에서 이메일 페이지를 선택하고 **속성 보기**.

   ![chlimage_1-16](assets/chlimage_1-16a.png)

1. 선택 **편집** 그리고 **클라우드 서비스** tab을 누른 채 아래쪽으로 스크롤하여 + 기호를 클릭하여 구성을 추가한 다음 을 선택합니다. **Adobe Campaign**.

   ![chlimage_1-17](assets/chlimage_1-17a.png)

1. 드롭다운 목록에서 Adobe Campaign 인스턴스와 일치하는 구성을 선택한 다음 를 클릭하여 확인합니다. **저장**.
1. 을(를) 클릭하여 이메일이 적용된 템플릿을 볼 수 있습니다.**Adobe Campaign** 탭. 다른 템플릿을 선택하려면 편집하는 동안 이메일 내에서 해당 템플릿에 액세스할 수 있습니다.

   기본 메일 템플릿 이외의 특정 이메일 게재 템플릿(Adobe Campaign)을 **속성**&#x200B;를 선택하고 **Adobe Campaign** 탭. 관련 Adobe Campaign 인스턴스에 이메일 게재 템플릿의 내부 이름을 입력합니다.

   선택하는 템플릿에 따라 Adobe Campaign에서 사용할 수 있는 개인화 필드가 결정됩니다.

   ![chlimage_1-18](assets/chlimage_1-18a.png)

작성 중인 뉴스레터/이메일 내에서에서 의 Adobe Campaign 클라우드 서비스 구성을 선택하지 못할 수 있습니다. **페이지 속성** 레이아웃 문제로 인해. 여기에 설명된 해결 방법을 사용할 수 있습니다.

1. AEM에서 이메일 페이지를 선택하고 **편집**. 클릭 **속성 열기**.

   ![chlimage_1-19](assets/chlimage_1-19a.png)

1. 선택 **클라우드 서비스** 및 클릭 **+** 구성을 추가합니다. 표시되는 구성을 선택합니다(어느 구성이든 상관없음). 다음을 클릭합니다. **+** 다른 구성을 추가하려면 로그인한 다음 선택 **Adobe Campaign**.

   >[!NOTE]
   >
   >또는 을 선택하여 클라우드 서비스를 선택할 수 있습니다. **속성 보기** 다음에서 **사이트** 탭.

1. 드롭다운 목록에서 Adobe Campaign 인스턴스와 일치하는 구성을 선택하고, Adobe Campaign에 대해 작성되지 않은 첫 번째 구성을 삭제한 다음 확인 표시를 클릭하여 확인합니다.
1. 이전 절차의 4단계를 계속 진행하여 템플릿을 선택하고 일반 텍스트를 추가합니다.

### 이메일 콘텐츠 편집 {#editing-email-content}

이메일 콘텐츠를 편집하려면:

1. 이메일을 열고 기본적으로 편집 모드를 시작합니다.

   ![chlimage_1-20](assets/chlimage_1-20a.png)

1. HTML에서 이메일을 보지 않을 사용자에 대해 이메일 제목을 변경하거나 일반 텍스트를 추가하려면 **이메일** 제목과 텍스트를 추가합니다. HTML 아이콘을 선택하여 페이지에서 일반 텍스트 버전을 자동으로 생성합니다. 완료되면 확인 표시를 클릭합니다.

   Adobe Campaign 개인화 필드를 사용하여 뉴스레터를 개인화할 수 있습니다. 개인화 필드를 추가하려면 Adobe Campaign 로고를 표시하는 버튼을 클릭하여 개인화 필드 선택기를 엽니다. 그런 다음 이 뉴스레터에 사용할 수 있는 모든 필드 중에서 선택할 수 있습니다.

   >[!NOTE]
   >
   >편집기 내 속성의 개인화 필드가 회색으로 표시되면 구성을 다시 검사합니다.

   ![chlimage_1-21](assets/chlimage_1-21a.png)

1. 화면 왼쪽에서 구성 요소 패널을 열고 을(를) 선택합니다 **Adobe Campaign 뉴스레터** 을 클릭하여 해당 구성 요소를 찾을 수 있습니다.

   ![chlimage_1-22](assets/chlimage_1-22a.png)

1. 구성 요소를 페이지로 직접 드래그하여 적절하게 편집합니다. 예를 들어 **텍스트 및 개인화(캠페인)** 구성 요소를 추가하고 개인화된 텍스트를 추가합니다.

   ![chlimage_1-23](assets/chlimage_1-23a.png)

   다음을 참조하십시오 [Adobe Campaign 구성 요소](/help/sites-authoring/adobe-campaign-components.md) 각 구성 요소에 대한 자세한 설명.

   ![chlimage_1-24](assets/chlimage_1-24a.png)

### 개인화 삽입 {#inserting-personalization}

콘텐츠를 편집할 때 다음을 삽입할 수 있습니다.

* Adobe Campaign 컨텍스트 필드. 받는 사람의 데이터(예: 이름, 성 또는 대상 차원의 모든 데이터)에 따라 달라지는 텍스트 내에 삽입할 수 있는 필드입니다.
* Adobe Campaign 개인화 블록. 브랜드 로고나 미러 페이지 링크와 같이 수신자의 데이터와 관련이 없는 사전 정의된 콘텐츠 블록입니다.

다음을 참조하십시오 [Adobe Campaign 구성 요소](/help/sites-authoring/adobe-campaign-components.md) Campaign 구성 요소에 대한 전체 설명.

>[!NOTE]
>
>* Adobe Campaign 필드만 **프로필** 타겟팅 차원이 고려됩니다.
>* 다음에서 속성을 볼 때 **사이트**, Adobe Campaign 컨텍스트 필드에 대한 액세스 권한이 없습니다. 편집하는 동안 이메일에서 직접 액세스할 수 있습니다.

개인화를 삽입하려면:

1. 새 항목 삽입 **뉴스레터** > **텍스트 및 개인화(캠페인)** 구성 요소를 페이지로 끌어 옵니다.

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. 연필 아이콘을 클릭하여 구성 요소를 엽니다. 즉석 편집기가 열립니다.

   ![chlimage_1-26](assets/chlimage_1-26a.png)

   >[!NOTE]
   >
   >**Adobe Campaign Standard의 경우**
   >
   >* 사용 가능한 컨텍스트 필드는 **프로필** Adobe Campaign의 차원 타겟팅.
   >* 다음을 참조하십시오 [Adobe Campaign 이메일에 AEM 페이지 연결](#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard).
   >
   >**Adobe Campaign Classic의 경우**
   >
   >* 사용 가능한 컨텍스트 필드는 Adobe Campaign에서 동적으로 복구됩니다 **nms:seedMember** 스키마. Target 확장 데이터는 콘텐츠와 동기화된 게재가 포함된 워크플로우에서 동적으로 복구됩니다. (다음을 참조하십시오. [AEM에서 만든 콘텐츠를 Adobe Campaign의 게재와 동기화](#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic) 섹션에 있는 마지막 항목이 될 필요가 없습니다.
   >
   >* 개인화 요소를 추가하거나 숨기려면 다음을 참조하십시오. [개인화 필드 및 블록 관리](/help/sites-administering/campaignonpremise.md#managing-personalization-fields-and-blocks).
   >* **중요 사항**: 모든 시드 테이블 필드는 수신자 테이블(또는 해당 연락처 테이블)에도 있어야 합니다.

1. 입력하여 텍스트를 삽입합니다. Adobe Campaign 구성 요소를 클릭하고 선택하여 컨텍스트 필드 또는 개인화 블록을 삽입합니다. 완료되면 확인 표시를 선택합니다.

   ![chlimage_1-27](assets/chlimage_1-27a.png)

   컨텍스트 필드 또는 개인화 블록을 삽입한 후 뉴스레터를 미리 보고 필드를 테스트할 수 있습니다. 다음을 참조하십시오 [뉴스레터 미리 보기](#previewing-a-newsletter).

### 뉴스레터 미리 보기 {#previewing-a-newsletter}

뉴스레터의 모습을 미리 보고 개인화를 미리 볼 수 있습니다.

1. 뉴스레터를 연 상태에서 **미리 보기** AEM의 오른쪽 상단에 있습니다. AEM은 사용자가 뉴스레터를 수신할 때 뉴스레터의 모양을 표시합니다.

   ![chlimage_1-28](assets/chlimage_1-28a.png)

   >[!NOTE]
   >
   >Adobe Campaign Standard을 사용하고 샘플 템플릿을 사용하는 경우 초기 콘텐츠를 표시하는 두 개의 개인화 블록 - **&quot;&lt;%@ include view=&quot;MirrorPage&quot; %>&quot;** 및 **&quot;&lt;%@ include view=&quot;UnsubscriptionLink&quot; %>&quot;** - 전달 중 콘텐츠를 가져올 때 오류가 발생합니다. 개인화 블록 선택기를 사용하여 해당 블록을 선택하여 이를 조정할 수 있습니다.

1. 개인화를 미리 보려면 도구 모음에서 해당 아이콘을 클릭/탭하여 ContextHub를 엽니다. 이제 개인화 필드 태그가 선택한 담당자의 시드 데이터로 대체됩니다. ContextHub에서 가상 사용자를 전환할 때 변수가 어떻게 조정되는지 확인하십시오.

   ![chlimage_1-29](assets/chlimage_1-29a.png)

1. 현재 선택한 담당자와 연결된 Adobe Campaign에서 제공되는 시드 데이터를 볼 수 있습니다. 이렇게 하려면 ContextHub 막대에서 Adobe Campaign 모듈을 클릭합니다. 그러면 현재 프로필의 모든 시드 데이터를 표시하는 대화 상자가 열립니다. 다시 말하지만, 데이터는 다른 성향으로 전환할 때 조정됩니다.

   ![chlimage_1-30](assets/chlimage_1-30a.png)

### AEM에서 콘텐츠 승인 {#approving-content-in-aem}

콘텐츠가 완료되면 승인 프로세스를 시작할 수 있습니다. 로 이동 **워크플로** 도구 상자의 탭을 클릭하고 **Adobe Campaign 승인** 워크플로입니다.

이 기본 워크플로에는 개정 후 승인 또는 개정 후 거부라는 두 단계가 있습니다. 그러나 이 워크플로우는 보다 복잡한 프로세스에 확장 및 조정될 수 있습니다.

![chlimage_1-31](assets/chlimage_1-31a.png)

Adobe Campaign에 대한 콘텐츠를 승인하려면 다음을 선택하여 워크플로를 적용합니다. **워크플로** 및 선택 **Adobe Campaign 승인** 및 클릭 **워크플로우 시작**. 단계를 진행하고 콘텐츠를 승인합니다. 을 선택하여 컨텐츠를 거부할 수도 있습니다 **거부** 대신 **승인** 마지막 워크플로우 단계에서 다음을 수행합니다.

![chlimage_1-32](assets/chlimage_1-32a.png)

콘텐츠가 승인되면 Adobe Campaign에서 승인된 것으로 표시됩니다. 그런 다음 이메일을 보낼 수 있습니다.

Adobe Campaign Standard:

![chlimage_1-33](assets/chlimage_1-33a.png)

Adobe Campaign Classic:

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
>
승인되지 않은 컨텐츠는 Adobe Campaign의 게재와 동기화할 수 있지만 게재를 실행할 수 없습니다. 승인된 콘텐츠만 Campaign 게재를 통해 보낼 수 있습니다.

## Adobe Campaign Standard 및 Adobe Campaign Classic과 AEM 연결 {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic}

AEM을 Adobe Campaign과 연결하거나 동기화하는 방법은 구독 기반 Adobe Campaign Standard을 사용하는지 또는 온프레미스 기반 Adobe Campaign Classic을 사용하는지에 따라 다릅니다.

Adobe Campaign 솔루션을 기반으로 하는 지침은 다음 섹션을 참조하십시오.

* [Adobe Campaign 이메일에 AEM 페이지 연결(Adobe Campaign Standard)](#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard)
* [AEM에서 만든 콘텐츠를 Adobe Campaign Classic의 게재와 동기화](#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic)

### Adobe Campaign 이메일에 AEM 페이지 연결(Adobe Campaign Standard) {#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard}

Adobe Campaign Standard을 사용하면 AEM에서 만든 컨텐츠를 다음과 같이 복구하고 연결할 수 있습니다.

* 이메일.
* 이메일 템플릿.

이렇게 하면 콘텐츠를 전달할 수 있습니다. 뉴스레터가 페이지에 표시되는 코드별로 단일 게재에 연결되어 있는지 여부를 확인할 수 있습니다.

![chlimage_1-35](assets/chlimage_1-35a.png)

>[!NOTE]
>
뉴스레터가 여러 게재에 연결된 경우 연결된 게재 수(일부 ID는 표시되지 않음)가 표시됩니다.

AEM에서 만든 페이지를 Adobe Campaign의 이메일과 연결하려면 다음을 수행하십시오.

1. AEM 관련 이메일 템플릿을 기반으로 이메일을 만듭니다. 을(를) 참조하십시오 [Adobe Campaign Standard에서 이메일 만들기](https://helpx.adobe.com/campaign/standard/channels/using/creating-an-email.html) 추가 정보.

   ![chlimage_1-36](assets/chlimage_1-36a.png)

1. 를 엽니다. **콘텐츠** 게재 대시보드에서 차단합니다.

   ![chlimage_1-37](assets/chlimage_1-37a.png)

1. 선택 **Adobe Experience Manager 콘텐츠와 연결** 을 클릭하여 AEM에서 사용할 수 있는 콘텐츠 목록에 액세스합니다.

   >[!NOTE]
   >
   다음과 같은 경우 **Adobe Experience Manager에 연결** 옵션이 작업 표시줄에 나타나지 않으면 **컨텐츠 편집 모드** 이(가) (으)로 올바르게 구성되었습니다. **Adobe Experience Manager** 이메일 속성에서.

   ![chlimage_1-38](assets/chlimage_1-38a.png)

1. 이메일에 사용할 콘텐츠를 선택합니다.

   이 목록은 다음을 지정합니다.

   * AEM의 콘텐츠 레이블입니다.
   * AEM에 있는 콘텐츠의 승인 상태입니다. 콘텐츠가 승인되지 않은 경우 콘텐츠를 동기화할 수 있지만 게재를 보내기 전에 승인해야 합니다. 그러나 증명 전송이나 미리보기 테스트와 같은 특정 작업을 실행할 수 있습니다.
   * 마지막으로 콘텐츠를 수정한 날짜입니다.
   * 게재에 이미 연결된 모든 콘텐츠.

   >[!NOTE]
   >
   기본적으로 게재와 이미 동기화된 콘텐츠는 숨겨집니다. 그러나 표시하고 사용할 수 있습니다. 예를 들어, 여러 게재에 대한 템플릿으로 콘텐츠를 사용하려는 경우,

   이메일이 AEM 컨텐츠에 연결된 경우 Adobe Campaign에서 컨텐츠를 편집할 수 없습니다.

1. 대시보드에서 이메일의 다른 매개 변수(대상, 실행 일정)를 지정합니다.
1. 이메일 게재를 실행합니다. 게재 분석 중에 AEM 콘텐츠의 최신 버전이 검색됩니다.

   >[!NOTE]
   >
   이메일에 연결된 상태에서 AEM에서 콘텐츠가 업데이트되면 분석 중에 Adobe Campaign에서 자동으로 업데이트됩니다. 동기화를 다음을 사용하여 수동으로 실행할 수도 있습니다. **Adobe Experience Manager 컨텐츠 새로 고침** 컨텐츠 작업 표시줄에서 을 참조하십시오.
   >
   다음을 사용하여 이메일과 AEM 콘텐츠 간의 링크를 취소할 수 있습니다. **Adobe Experience Manager 콘텐츠로 링크 삭제** 컨텐츠 작업 표시줄에서 을 참조하십시오. 이 단추는 콘텐츠가 이미 게재에 연결되어 있는 경우에만 사용할 수 있습니다. 다른 콘텐츠를 게재와 연결하려면 새 링크를 설정하기 전에 현재 콘텐츠 링크를 삭제해야 합니다.
   >
   링크가 삭제되면 로컬 콘텐츠가 유지되고 Adobe Campaign에서 편집할 수 있게 됩니다. 콘텐츠를 수정한 후 다시 연결하면 모든 변경 사항이 손실됩니다.

### AEM에서 만든 콘텐츠를 Adobe Campaign Classic의 게재와 동기화 {#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic}

Adobe Campaign을 사용하면 AEM에서 만든 콘텐츠를 다음과 같이 복구하고 동기화할 수 있습니다.

* 캠페인 게재
* 캠페인 워크플로우의 게재 활동
* 반복 게재
* 연속 게재
* 메시지 센터 게재
* 게재 템플릿

AEM에서 뉴스레터가 단일 게재에 연결된 경우 게재 코드가 페이지에 표시됩니다.

![chlimage_1-39](assets/chlimage_1-39a.png)

>[!NOTE]
>
뉴스레터가 여러 게재에 연결된 경우 연결된 게재 수(일부 ID는 표시되지 않음)가 표시됩니다.
>
[!NOTE]
>
워크플로 단계 **Adobe Campaign에 게시** 는 AEM 6.1에서 더 이상 사용되지 않습니다. 이 단계는 Adobe Campaign과의 AEM 6.0 통합의 일부였으며 더 이상 필요하지 않습니다.

AEM에서 만든 콘텐츠를 Adobe Campaign의 게재와 동기화하려면 다음 작업을 수행하십시오.

1. 게재를 만들거나 을 선택하여 캠페인 워크플로우에 게재 활동을 추가합니다. **AEM 콘텐츠를 사용한 이메일 게재(mailAEMContent)** 게재 템플릿.

   ![chlimage_1-40](assets/chlimage_1-40a.png)

1. 선택 **동기화** 을 클릭하여 AEM에서 사용할 수 있는 콘텐츠 목록에 액세스합니다.

   >[!NOTE]
   >
   다음과 같은 경우 **동기화** 옵션이 게재 도구 모음에 표시되지 않는지 확인하고 **컨텐츠 편집 모드** 다음에서 필드가 올바르게 구성됨: **AEM** 을(를) 선택하여 **속성** > **고급**.

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. 게재와 동기화할 콘텐츠를 선택합니다.

   이 목록은 다음을 지정합니다.

   * AEM의 콘텐츠 레이블입니다.
   * AEM에 있는 콘텐츠의 승인 상태입니다. 콘텐츠가 승인되지 않은 경우 콘텐츠를 동기화할 수 있지만 게재를 보내기 전에 승인해야 합니다. 그러나 BAT 또는 미리보기 테스트 전송과 같은 특정 작업을 실행할 수 있습니다.
   * 콘텐츠에 대한 마지막 수정 날짜입니다.
   * 게재에 이미 연결된 모든 콘텐츠.

   >[!NOTE]
   >
   기본적으로 게재와 이미 동기화된 콘텐츠는 숨겨집니다. 그러나 표시하고 사용할 수 있습니다. 예를 들어, 여러 게재에 대한 템플릿으로 콘텐츠를 사용하려는 경우,

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. 게재의 다른 매개 변수(target 등)를 지정합니다.
1. 필요한 경우 Adobe Campaign에서 게재 승인 프로세스를 시작합니다. Adobe Campaign에 구성된 승인(예산, 대상 등) 외에 AEM의 콘텐츠 승인이 필요합니다. Adobe Campaign의 콘텐츠 승인은 콘텐츠가 AEM에서 이미 승인된 경우에만 가능합니다.
1. 게재를 실행합니다. 게재 분석 중에 AEM 콘텐츠의 최신 버전이 복구됩니다.

   >[!NOTE]
   >
   * 게재 및 콘텐츠가 동기화되면 Adobe Campaign의 게재 콘텐츠는 읽기 전용이 됩니다. 이메일 제목과 해당 콘텐츠는 더 이상 수정할 수 없습니다.
   * 콘텐츠가 Adobe Campaign의 게재에 연결되어 있는 동안 AEM에서 업데이트되면 게재 분석 중에 게재에서 자동으로 업데이트됩니다. 동기화를 다음을 사용하여 수동으로 실행할 수도 있습니다. **지금 콘텐츠 새로 고침** 단추를 클릭합니다.
   * 를 사용하여 게재 및 AEM 콘텐츠 간의 동기화를 취소할 수 있습니다. **동기화 해제** 단추를 클릭합니다. 콘텐츠가 게재와 이미 동기화된 경우에만 사용할 수 있습니다. 다른 콘텐츠를 게재와 동기화하려면 새 링크를 설정하기 전에 현재 콘텐츠 동기화를 취소해야 합니다.
   * 동기화가 해제되면 로컬 콘텐츠가 유지되어 Adobe Campaign에서 편집할 수 있게 됩니다. 콘텐츠를 수정한 후 다시 동기화하면 모든 변경 내용이 손실됩니다.
   * 반복 및 연속 게재의 경우 게재가 실행될 때마다 AEM 콘텐츠와의 동기화가 중지됩니다.
