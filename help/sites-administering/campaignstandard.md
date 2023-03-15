---
title: Adobe Campaign Standard과 통합
seo-title: Integrating with Adobe Campaign Standard
description: AEM을 Adobe Campaign Standard과 통합하는 방법을 알아봅니다.
seo-description: Learn how to integrate AEM with Adobe Campaign Standard.
uuid: ef31339e-d925-499c-b8fb-c00ad01e38ad
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5c0fec99-7b1e-45d6-a115-e498d288e9e1
exl-id: caa43d80-1f38-46fc-a8b9-9485c235c0ca
source-git-commit: a0062ffbdd6477eca494fea4142d271f3015599a
workflow-type: tm+mt
source-wordcount: '1807'
ht-degree: 16%

---


# Adobe Campaign Standard과 통합 {#integrating-with-adobe-campaign-standard}

AEM을 Adobe Campaign과 통합하여 AEM에서 직접 이메일 게재, 콘텐츠 및 양식을 관리할 수 있습니다. 솔루션 간에 양방향 통신을 사용하려면 Adobe Campaign Standard과 AEM 모두에서 구성 단계가 필요합니다.

이 통합을 사용하면 AEM 및 Adobe Campaign Standard을 독립적으로 사용할 수 있습니다. 마케터는 캠페인을 만들고 Adobe Campaign에서 타깃팅을 사용할 수 있지만 동시에 컨텐츠 작성자는 AEM에서 컨텐츠 디자인에서 작업할 수 있습니다. 통합을 사용하여 AEM에서 만든 캠페인의 컨텐츠 및 디자인을 Adobe Campaign에서 타깃팅하고 전달할 수 있습니다.

## 통합 단계 {#integration-steps}

AEM과 Adobe Campaign Standard 간의 통합을 구성하려면 두 솔루션에 모두 몇 개의 단계가 필요합니다.

1. [구성 ](#aemserver-user)
1. [확인 ](#resource-type-filter)
1. [Campaign에서 AEM별 이메일 게재 템플릿 만들기](#aem-email-delivery-template)
1. [AEM에서 Campaign 통합 구성](#campaign-integration)
1. [AEM 게시 인스턴스에 복제 구성](#replication)
1. [AEM 외부화 구성](#externalizer)
1. [구성 ](#campaign-remote-user)
1. [Campaign에서 AEM 외부 계정 구성](#acc-external-user)

이 문서에서는 이러한 각 단계를 자세히 설명합니다.

## 사전 요구 사항 {#prerequisites}

* Adobe Campaign Standard에 대한 관리자 액세스
   * Adobe Campaign Standard 설정 및 구성 방법에 대한 자세한 내용은 [Adobe Campaign Standard 설명서.](https://experienceleague.adobe.com/docs/campaign-standard/using/campaign-standard-home.html)
* AEM에 대한 관리자 액세스

## Campaign에서 aem 서버 사용자 구성 {#aemserver-user}

Adobe Campaign Standard은 기본적으로 다음과 같이 제공됩니다 `aemserver` AEM에서 Adobe Campaign에 연결하는 데 사용하는 사용자. 이 사용자에게 적절한 보안 그룹을 할당하고 암호를 설정해야 합니다.

1. 관리자로 Adobe Campaign에 로그인합니다.

1. 메뉴 모음 왼쪽 상단에 있는 Adobe Campaign 로고를 탭하거나 클릭하여 전역 탐색을 연 다음, 을 선택합니다 **관리** > **사용자 및 보안** > **사용자** 탐색 메뉴에서 를 클릭합니다.

1. 을(를) 탭하거나 클릭합니다 `aemserver` 사용자 콘솔의 사용자.

1. 다음을 확인합니다. `aemserver` 사용자는 최소한 역할이 있는 보안 그룹에 할당됩니다 `deliveryPrepare` 할당됨. 기본적으로 그룹 `Standard Users` 이 역할이 있습니다.

   ![Adobe Campaign의 emserver 사용자](assets/acs-aemserver-user.png)

1. 탭 또는 클릭 **저장** 변경 사항을 저장하려면 을 클릭합니다.

사용자 `aemserver` 이제 AEM에서 Adobe Campaign과 통신하는 데 사용할 수 있도록 사용자에게 필요한 권한이 있습니다.

그러나 AEM에서 `aemserver` 사용자가 암호를 설정해야 합니다. 이 작업은 Adobe Campaign을 통해 수행할 수 없습니다. Adobe 지원 엔지니어가 이를 수행해야 합니다. [Adobe 고객 지원 센터에서 티켓을 발행하십시오](https://experienceleague.adobe.com/?support-tab=home#support) 의 재설정을 요청하려면 `aemserver` 암호. Adobe 고객 지원 센터에서 암호를 확인했으면 안전한 위치에 보관하십시오.

## Campaign에서 AEMResourceTypeFilter 확인 {#resource-type-filter}

다음 `AEMResourceTypeFilter` 은 Adobe Campaign에서 사용할 수 있는 AEM 리소스를 필터링하는 데 사용되는 Adobe Campaign의 옵션입니다. AEM에는 많은 콘텐츠가 포함되어 있으므로 이 옵션은 Adobe Campaign에서 Adobe Campaign에 사용하도록 특별히 설계된 유형의 AEM 콘텐츠만 검색할 수 있도록 해주는 필터 역할을 합니다.

이 옵션은 사전 구성되어 있습니다. 그러나 AEM의 Campaign 구성 요소를 사용자 지정한 경우 업데이트해야 할 수 있습니다. 를 확인하려면 `AEMResourceTypeFilter` 옵션이 구성되면 다음 단계를 따르십시오.

1. 관리자로 Adobe Campaign에 로그인합니다.

1. 메뉴 모음 왼쪽 상단에 있는 Adobe Campaign 로고를 탭하거나 클릭하여 전역 탐색을 연 다음, 을 선택합니다 **관리** > **애플리케이션 설정** > **옵션** 탐색 메뉴에서 를 클릭합니다.

1. 을(를) 탭하거나 클릭합니다 `AEMResourceTypeFilter` 옵션 콘솔에서 을 클릭합니다.

1. 구성 확인 `AEMResourceTypeFilter`. 경로는 쉼표로 구분되며 기본적으로 다음이 포함됩니다.

   * `mcm/campaign/components/newsletter`
   * `mcm/campaign/components/campaign_newsletterpage`
   * `mcm/neolane/components/newsletter`

   ![AEMRessourceTypeFilter](assets/acs-aem-resource-type-filter.png)

1. 탭 또는 클릭 **저장** 변경 사항을 저장하려면 을 클릭합니다.

사용자 `AEMResourceTypeFilter` 이제 AEM에서 올바른 컨텐츠를 검색하도록 구성되었습니다.

## Campaign에서 AEM별 이메일 게재 템플릿 만들기 {#aem-email-delivery-template}

기본적으로 AEM은 Adobe Campaign의 이메일 템플릿에서 활성화되지 않습니다. AEM 콘텐츠를 사용하여 이메일을 만드는 데 사용할 수 있는 새 이메일 게재 템플릿을 구성해야 합니다. AEM별 이메일 게재 템플릿을 만들려면 다음 단계를 수행하십시오.

1. 관리자로 Adobe Campaign에 로그인합니다.

1. 메뉴 모음 왼쪽 상단에 있는 Adobe Campaign 로고를 탭하거나 클릭하여 전역 탐색을 연 다음, 을 선택합니다 **리소스** > **템플릿** > **게재 템플릿** 탐색 메뉴에서 를 클릭합니다.

1. 게재 템플릿 콘솔에서 기본 이메일 템플릿을 찾습니다 **전자 메일(메일)을 통해 보내기** 카드를 나타내는 카드(또는 선) 위로 마우스를 가져가면 옵션이 표시됩니다. 클릭 **중복 요소**.

   ![중복 요소](assets/acs-copy-template.png)

1. 에서 **확인** 대화 상자 **확인** 템플릿을 복제하려면 다음을 수행하십시오.

   ![확인 대화 상자](assets/acs-confirmation.png)

1. 템플릿 편집기가 페이지의 복사본을 사용하여 열립니다 **전자 메일(메일)을 통해 보내기** 템플릿. 을(를) 클릭합니다. **속성 편집** 창 오른쪽 상단의 아이콘을 클릭합니다.

   ![템플릿 편집기](assets/acs-template-editor.png)

1. 속성 창에서 **레이블** 새 AEM 템플릿을 설명하는 필드입니다.

1. 을(를) 클릭합니다. **컨텐츠** 을(를) 확장하고 을(를) 선택합니다. **Adobe Experience Manager** 에서 **컨텐츠 소스** 드롭다운.

1. 이렇게 하면 다음 내용이 표시됩니다 **Adobe Experience Manager 계정** 필드. 드롭다운을 사용하여 선택 **Adobe Experience Manager 인스턴스(aemInstance)** 사용자. AEM 통합을 위한 기본 외부 사용자입니다.

![템플릿 속성 구성](assets/acs-template-properties.png)

1. 클릭 **확인** 속성에 대한 변경 사항을 저장하려면

1. 템플릿 편집기에서 **저장** AEM에서 사용할 이메일 템플릿의 수정된 복사본을 저장하려면 을 클릭합니다.

이제 AEM 콘텐츠를 사용할 수 있는 이메일 템플릿이 있습니다.

## AEM에서 Campaign 통합 구성 {#campaign-integration}

AEM은 내장된 통합 및 `aemserver` Adobe Campaign에서 구성한 사용자입니다. 다음 단계에 따라 이 통합을 구성합니다.

1. 관리자 자격으로 AEM 제작 인스턴스에 로그인합니다.

1. 전역 탐색 측면 레일에서 **Tools** > **Cloud Services** > **레거시 Cloud Services** > **Adobe Campaign**&#x200B;을 선택한 뒤 **지금 구성**&#x200B;을 클릭합니다.

   ![Adobe Campaign 구성](assets/configure-campaign-service.png)

1. 대화 상자에서 **제목**&#x200B;을 입력하여 Campaign 서비스 구성을 생성하고 **생성**&#x200B;을 클릭합니다.

   ![Campaign 구성 대화 상자](assets/configure-campaign-dialog.png)

1. 구성 편집을 위한 새 창과 대화 상자가 열립니다. 필요한 정보를 입력합니다.

   * **사용자 이름** - 다음 [a `aemserver` 이전 단계에서 구성한 Adobe Campaign의 사용자입니다.](#aemserver-user) 이는 기본적으로 `aemserver`입니다.
   * **암호** - 다음 암호입니다. [a `aemserver` 이전 단계의 고객 지원 Adobe에서 요청한 Adobe Campaign의 사용자.](#aemserver-user)
   * **API 끝점** - Adobe Campaign 인스턴스 URL입니다.

   ![AEM에서 Adobe Campaign 구성](assets/configure-campaign.png)

1. **Adobe Campaign에 연결**&#x200B;을 선택하여 연결을 확인한 뒤 **확인**&#x200B;을 클릭합니다.

이제 AEM에서 Adobe Campaign과 통신할 수 있습니다.

>[!NOTE]
>
>Adobe Campaign 서버가 인터넷을 통해 접근 가능해야 합니다. AEM이 개인 네트워크에 액세스할 수 없습니다.

## AEM 게시 인스턴스에 복제 구성 {#replication}

캠페인 컨텐츠는 AEM 작성 인스턴스의 컨텐츠 작성자가 만듭니다. 이 인스턴스는 일반적으로 조직에서만 사용할 수 있습니다. 캠페인 수신자가 액세스할 수 있는 이미지 및 자산 등의 컨텐츠의 경우 해당 컨텐츠를 게시해야 합니다.

복제 에이전트는 AEM 작성자 인스턴스의 컨텐츠를 게시 인스턴스에 게시할 책임이 있으며 통합이 제대로 작동하려면 설정되어야 합니다. 이 단계는 특정 작성 인스턴스 구성을 게시 인스턴스에 복제하는 데도 필요합니다.

AEM 작성자 인스턴스에서 게시 인스턴스로 복제를 구성하려면:

1. 관리자 자격으로 AEM 제작 인스턴스에 로그인합니다.

1. 전역 탐색 사이드 레일에서 를 선택합니다. **도구** > **배포** > **복제** > **작성자의 에이전트**&#x200B;를 탭하거나 클릭합니다 **기본 에이전트(게시)**.

   ![복제 에이전트 구성](assets/acc-replication-config.png)

1. 탭 또는 클릭 **편집** 그런 다음 **전송** 탭.

1. 구성 **URI** 필드를 기본 값으로 바꿉니다 `localhost` 값을 AEM 게시 인스턴스의 IP 주소로 할 수도 있습니다.

   ![전송 탭](assets/acc-transport-tab.png)

1. 탭 또는 클릭 **확인** 에이전트 설정에 대한 변경 사항을 저장하려면 다음을 수행합니다.

캠페인 수신자가 콘텐츠에 액세스할 수 있도록 AEM 게시 인스턴스에 대한 복제를 구성했습니다.

>[!NOTE]
>
>복제 URL을 사용하지 않고 대신 공개 URL을 사용하는 경우 OSGi를 통해 다음 구성 설정에서 공개 URL을 설정할 수 있습니다
>
>전역 탐색 사이드 레일에서 를 선택합니다. **도구** > **작업** > **웹 콘솔** > **OSGi 구성** 및 검색 **AEM Campaign 통합 - 구성**. 구성 편집 및 필드 변경 **공개 URL** (`com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl`).

## AEM 외부화 구성 {#externalizer}

[외부화는 AEM의 OSGi 서비스로, 리소스 경로를 외부 및 절대 URL로 변환합니다. 이는 Campaign에서 사용 가능한 콘텐츠를 AEM이 제공하는 데 필요합니다. ](/help/sites-developing/externalizer.md) Campaign 통합이 작동하려면 구성해야 합니다.

1. 관리자 자격으로 AEM 제작 인스턴스에 로그인합니다.
1. 전역 탐색 사이드 레일에서 를 선택합니다. **도구** > **작업** > **웹 콘솔** > **OSGi 구성** 및 검색 **Day CQ link Externalizer**.
1. 기본적으로 **도메인** 게시 인스턴스에 대한 필드입니다. 기본값에서 URL 변경 `http://localhost:4503` 을 사용 가능한 게시 인스턴스에 업로드합니다.

   ![외부 도우미 구성](assets/acc-externalizer-config.png)

1. **저장**&#x200B;을 탭하거나 클릭합니다.

이제 Externalizer를 구성하고 Adobe Campaign이 콘텐츠에 액세스할 수 있습니다.

>[!NOTE]
게시 인스턴스는 Adobe Campaign 서버에서 접근 가능해야 합니다. 이 URL이 `localhost:4503` 또는 Adobe Campaign이 연결할 수 없는 다른 서버는 AEM의 이미지가 Adobe Campaign 콘솔에 표시되지 않습니다.

## AEM에서 campaign-remote 사용자 구성 {#campaign-remote-user}

AEM에서 Adobe Campaign과 통신하는 데 사용할 수 있는 Adobe Campaign의 사용자가 필요한 것처럼 Adobe Campaign에도 AEM과 통신하기 위한 AEM의 사용자가 필요합니다. 기본적으로 캠페인 통합은 `campaign-remote` AEM의 사용자. 다음 단계에 따라 이 사용자를 구성합니다.

1. 관리자로 AEM에 로그인합니다.
1. 메인 탐색 콘솔에서 왼쪽 레일의 **도구**&#x200B;를 클릭합니다.
1. 그런 다음 **보안** > **사용자** 를 클릭하여 사용자 관리 콘솔을 엽니다.
1. `campaign-remote` 사용자를 찾습니다.
1. `campaign-remote` 사용자를 선택한 뒤 **속성**&#x200B;을 클릭하여 사용자를 편집합니다.
1. **사용자 설정 편집** 창에서 **암호 변경**&#x200B;을 클릭합니다.
1. 사용자에 대한 새 암호를 제공하고, 나중에 사용할 수 있도록 안전한 위치에 기록해 둡니다.
1. **저장**&#x200B;을 클릭하여 암호 변경사항을 저장합니다.
1. **저장 및 닫기**&#x200B;를 클릭하여 `campaign-remote` 사용자에 대한 변경사항을 저장합니다.

## Campaign에서 AEM 외부 계정 구성 {#acc-external-user}

다음 경우에 [AEM 관련 이메일 게재 템플릿을 만들었습니다.](#aem-email-delivery-template) 템플릿에 `aemInstance` AEM과 통신할 외부 계정입니다. 두 솔루션 간에 양방향 통신을 사용하려면 Adobe Campaign에서 이 계정을 구성해야 합니다.

1. 관리자로 Adobe Campaign에 로그인합니다.

1. 메뉴 모음 왼쪽 상단에 있는 Adobe Campaign 로고를 탭하거나 클릭하여 전역 탐색을 연 다음, 을 선택합니다 **관리** > **애플리케이션 설정** > **외부 계정** 탐색 메뉴에서 를 클릭합니다.

1. 을(를) 탭하거나 클릭합니다 **Adobe Experience Manager 인스턴스(aemInstance)** 사용자 콘솔의 사용자.

1. 사용자가 **Adobe Experience Manager** 로서의 **유형**.

1. 에서 **연결** 섹션에서 다음 필드를 정의합니다.

   1. 서버: AEM 작성 서버의 URL입니다. 슬래시로 끝나지 않아야 합니다.
   1. 계정: 이것은 `campaign-remote` 사용자 [이전에 AEM에서 구성되었습니다.](#campaign-remote-user)
   1. 암호: 이 암호는 `campaign-remote`사용자 [이전에 AEM에서 구성되었습니다.](#campaign-remote-user)

   ![aemInstance 사용자 편집](assets/acs-external-acount-editor.png)

1. 다음을 확인합니다. **활성화됨** 확인란을 선택한 다음 를 클릭합니다. **저장** 변경 사항을 저장하려면 을 클릭합니다.

축하합니다! AEM과 Adobe Campaign Standard 간의 통합을 완료했습니다!

## 다음 단계 {#next-steps}

Adobe Campaign Classic과 AEM이 모두 구성되어 이제 통합이 완료됩니다.

이번에는 [이 문서](/help/sites-authoring/campaign.md)를 계속 읽으며 Adobe Experience Manager에서 뉴스레터를 생성하는 방법에 대해 알아볼 수 있습니다.
