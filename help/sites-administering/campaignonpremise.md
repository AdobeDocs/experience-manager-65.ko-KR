---
title: AEM 6.5와 Adobe Campaign Classic 통합
description: AEM 6.5를 Adobe Campaign Classic과 통합하는 방법 알아보기
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: a7281ca0-461f-4762-a631-6bb539596200
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '1583'
ht-degree: 66%

---


# AEM 6.5와 Adobe Campaign Classic 통합 {#integrating-campaign-classic}

AEM을 ACC(Adobe Campaign Classic)와 통합하여 AEM에서 이메일 게재, 콘텐츠 및 양식을 직접 관리할 수 있습니다. 솔루션 간 양방향 통신이 가능하려면 Adobe Campaign Classic과 AEM 모두에서 구성 단계를 수행해야 합니다.

이 통합을 통해 AEM 및 Adobe Campaign Classic을 독립적으로 사용할 수 있습니다. 마케터는 Adobe Campaign에서 캠페인을 만들고 타깃팅을 사용할 수 있으며, 동시에 콘텐츠 크리에이터는 AEM에서 콘텐츠 디자인 작업을 할 수 있습니다. 통합을 사용하여 AEM에서 만든 캠페인의 콘텐츠와 디자인을 Adobe Campaign에서 타겟팅하고 전달할 수 있습니다.

>[!INFO]
>
>이 문서에서는 Adobe Campaign Classic을 AEM 6.5와 통합하는 방법에 대해 자세히 설명합니다. 다른 Campaign 통합에 대해서는 문서를 참조하십시오 [AEM 6.5와 Adobe Campaign 통합.](campaign.md)

## 통합 단계 {#integration-steps}

AEM과 Campaign 간 통합을 위해서는 두 솔루션 모두에서 몇 가지 단계를 수행해야 합니다.

1. [Campaign에서 AEM 통합 패키지 설치](#install-package)
1. [Campaign에서 AEM에 대한 연산자 생성](#create-operator)
1. [AEM에서 Campaign 통합 구성](#campaign-integration)
1. [AEM 외부화 구성](#externalizer)
1. [AEM에서 캠페인 원격 사용자 구성](#configure-user)
1. [Campaign에서 AEM 외부 계정 구성](#acc-setup)

이 문서는 이러한 각 단계를 자세히 안내합니다..

## 사전 요구 사항 {#prerequisites}

* Adobe Campaign Classic에 대한 관리자 액세스
   * 통합을 수행하려면 구성된 데이터베이스를 포함하는 작동 중인 Adobe Campaign Classic 인스턴스가 필요합니다.
   * Adobe Campaign Classic 설정 및 구성 방법에 관한 자세한 정보가 필요한 경우 [Adobe Campaign Classic 문서](https://experienceleague.adobe.com/docs/campaign-classic/using/campaign-classic-home.html)를 참조하시고 특히 설치 및 구성 안내서를 참조하십시오.
* AEM에 대한 관리자 액세스

## Campaign에 AEM 통합 패키지 설치 {#install-package}

Adobe Campaign의 **AEM 통합** 패키지는 AEM에 연결하는 데 필요한 다양한 표준 구성을 포함하고 있습니다.

1. 관리자 자격으로 클라이언트 콘솔을 사용해 Adobe Campaign 인스턴트에 로그인합니다.

1. **도구** > **고급** > **패키지 가져오기...**&#x200B;를 선택합니다.

   ![패키지 가져오기](assets/import-package.png)

1. Click **표준 패키지 설치**&#x200B;를 클릭한 뒤 **다음**&#x200B;을 클릭합니다.

1. **AEM 통합** 패키지에 체크 표시합니다.

   ![표준 패키지 설치](assets/select-package.png)

1. **다음**&#x200B;을 클릭한 뒤 **시작**&#x200B;을 클릭하여 설치를 시작합니다.

   ![설치 진행률](assets/installation.png)

1. 설치가 완료되면 **닫기**&#x200B;를 클릭합니다.

통합 패키지 설치가 완료되었습니다.

## Campaign에서 AEM에 대한 연산자 생성 {#create-operator}

통합 패키지는 AEM이 Adobe Campaign에 연결할 때 사용하는 `aemserver` 연산자를 자동으로 생성합니다. 이 연산자에 대한 보안 영역을 정의하고 그 암호를 설정해야 합니다.

1. 클라이언트 콘솔을 사용해 관리자 자격으로 Adobe Campaign에 로그인합니다.

1. 메뉴 표시줄에서 **도구** -> **탐색기**&#x200B;를 선택합니다.

1. 탐색기에서 **관리** > **액세스 관리** > **연산자** 노드로 이동합니다.

1. `aemserver` 연산자를 선택합니다.

1. 연산자의 **편집** 탭에서 **액세스 권한** 하위 탭을 선택하고 **액세스 매개변수 편집...** 링크를 클릭합니다.

   ![보안 영역 설정](assets/access-rights.png)

1. 적절한 보안 영역을 선택하고 필요에 따라 신뢰할 수 있는 IP 마스크를 정의합니다.

1. **저장**&#x200B;을 클릭합니다.

1. Adobe Campaign 클라이언트에서 로그아웃합니다.

1. Adobe Campaign 서버의 파일 시스템에서 Campaign 설치 위치로 이동하여 관리자 자격으로 `serverConf.xml` 파일을 편집합니다. 이 파일의 위치는 보통 다음과 같습니다.
   * Windows의 `C:\Program Files\Adobe\Adobe Campaign Classic v7\conf`.
   * Linux에서 `/usr/local/neolane/nl6/conf/eng`.

1. `securityZone` 을 검색한 뒤 AEM 연산자의 보안 영역에 대해 다음 매개변수가 설정되었는지 확인합니다.

   * `allowHTTP="true"`
   * `sessionTokenOnly="true"`
   * `allowUserPassword="true"`.

1. 파일을 저장합니다.

1. `config-<server name>.xml` 파일의 해당 설정이 보안 영역을 덮어쓰지 않도록 합니다.

   * 구성 파일에 별개의 보안 영역 설정이 포함되어 있는 경우 `allowUserPassword` 속성을 `true`로 바꿉니다.

1. Adobe Campaign Classic 서버 포트를 바꾸려면 `8080`을 원하는 포트로 바꿉니다.

   >[!CAUTION]
   >
   >기본적으로, 연산자에 대해 보안 영역이 구성되어 있지 않습니다. AEM이 Adobe Campaign에 연결되려면 앞의 단계들에서 자세히 설명한 대로 영역을 반드시 선택해야 합니다.
   >
   >Adobe는 잠재적인 보안 문제를 예방할 수 있도록 AEM 전용 보안 영역을 생성할 것을 적극 권장합니다. 이 주제에 관한 자세한 내용은 [Adobe Campaign Classic 문서](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/security-zones.html)를 참조하십시오.

1. Campaign 클라이언트에서 `aemserver` 연산자로 돌아간 뒤 **일반** 탭을 선택합니다.

1. **암호 재설정** 링크를 클릭합니다.

1. 암호를 지정하고, 나중에 사용할 수 있도록 안전한 위치에 저장합니다.

1. **확인**&#x200B;을 클릭해 `aemserver` 연산자에 대한 암호를 저장합니다.

## AEM에서 Campaign 통합 구성 {#campaign-integration}

AEM은 [Campaign에서 사용자가 이미 설정해 둔 연산자](#create-operator)를 사용하여 Campaign과 통신합니다.

1. 관리자 자격으로 AEM 제작 인스턴스에 로그인합니다.

1. 전역 탐색 측면 레일에서 **Tools** > **Cloud Services** > **레거시 Cloud Services** > **Adobe Campaign**&#x200B;을 선택한 뒤 **지금 구성**&#x200B;을 클릭합니다.

   ![Adobe Campaign 구성](assets/configure-campaign-service.png)

1. 대화 상자에서 **제목**&#x200B;을 입력하여 Campaign 서비스 구성을 생성하고 **생성**&#x200B;을 클릭합니다.

   ![Campaign 구성 대화 상자](assets/configure-campaign-dialog.png)

1. 구성 편집을 위한 새 창과 대화 상자가 열립니다. 필요한 정보를 입력합니다.

   * **사용자 이름** - 이전 단계에서 생성한 [Adobe Campaign AEM 통합 패키지 연산자입니다.](#create-operator) 이는 기본적으로 `aemserver`입니다.
   * **암호** - [이전 단계에서 생성한 Adobe Campaign AEM 통합 패키지 연산자의 암호입니다.](#create-operator)
   * **API 끝점** - Adobe Campaign 인스턴스 URL입니다.

   ![AEM에서 Adobe Campaign 구성](assets/configure-campaign.png)

1. **Adobe Campaign에 연결**&#x200B;을 선택하여 연결을 확인한 뒤 **확인**&#x200B;을 클릭합니다.

이제 AEM에서 Adobe Campaign과 통신할 수 있습니다.

>[!NOTE]
>
>Adobe Campaign 서버가 인터넷을 통해 접근 가능해야 합니다. AEM에서 개인 네트워크에 액세스할 수 없습니다.

## AEM 게시 인스턴스에 대한 복제 구성 {#replication}

캠페인 콘텐츠는 AEM 작성 인스턴스의 콘텐츠 작성자가 작성합니다. 이 인스턴스는 일반적으로 조직 내부에서만 사용할 수 있습니다. 이미지 및 에셋과 같은 콘텐츠를 캠페인 수신자가 액세스할 수 있도록 하려면 해당 콘텐츠를 게시해야 합니다.

복제 에이전트는 AEM 작성자 인스턴스에서 게시 인스턴스로 콘텐츠를 게시하는 역할을 하며 통합이 제대로 작동하도록 설정되어야 합니다. 이 단계는 특정 작성 인스턴스 구성을 게시 인스턴스로 복제하는 데에도 필요합니다.

AEM 작성자 인스턴스에서 게시 인스턴스로의 복제를 구성하려면 다음 작업을 수행하십시오.

1. 관리자 자격으로 AEM 제작 인스턴스에 로그인합니다.

1. 전역 탐색 측면 레일에서 을 선택합니다. **도구** > **배포** > **복제** > **작성자의 에이전트**&#x200B;을 클릭한 다음 을 탭하거나 클릭합니다 **기본 에이전트(게시)**.

   ![복제 에이전트 구성](assets/acc-replication-config.png)

1. 탭 또는 클릭 **편집** 그런 다음 **전송** 탭.

1. 구성 **URI** 기본값을 대체한 필드 `localhost` AEM 게시 인스턴스의 IP 주소가 있는 값입니다.

   ![전송 탭](assets/acc-transport-tab.png)

1. 탭 또는 클릭 **확인** 에이전트 설정에 대한 변경 사항을 저장합니다.

캠페인 수신자가 콘텐츠에 액세스할 수 있도록 AEM 게시 인스턴스에 대한 복제를 구성했습니다.

>[!NOTE]
>
>복제 URL을 사용하지 않고 대신 공개 URL을 사용하려는 경우 OSGi를 통해 다음 구성 설정에서 공개 URL을 설정할 수 있습니다
>
>전역 탐색 측면 레일에서 을 선택합니다. **도구** > **작업** > **웹 콘솔** > **OSGi 구성** 및 검색 **AEM Campaign 통합 - 구성**. 구성 편집 및 필드 변경 **공개 URL** (`com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl`).

## AEM 외부화 구성 {#externalizer}

[외부화는 AEM의 OSGi 서비스로, 리소스 경로를 외부 및 절대 URL로 변환합니다. 이는 Campaign에서 사용 가능한 콘텐츠를 AEM이 제공하는 데 필요합니다. ](/help/sites-developing/externalizer.md) Campaign 통합이 작동하려면 구성해야 합니다.

1. 관리자 자격으로 AEM 제작 인스턴스에 로그인합니다.
1. 전역 탐색 측면 레일에서 을 선택합니다. **도구** > **작업** > **웹 콘솔** > **OSGi 구성** 및 검색 **일별 CQ 링크 외부화**.
1. 기본적으로 의 마지막 항목은 **도메인** 필드는 게시 인스턴스를 위한 것입니다. 기본값에서 URL 변경 `http://localhost:4503` 을 클릭하여 공개적으로 사용할 수 있는 게시 인스턴스에 게시합니다.

   ![외부화 구성](assets/acc-externalizer-config.png)

1. **저장**&#x200B;을 탭하거나 클릭합니다.

외부화를 구성했으므로 Adobe Campaign에서 이제 콘텐츠에 액세스할 수 있습니다.

>[!NOTE]
>
게시 인스턴스는 Adobe Campaign 서버에서 접근 가능해야 합니다. 다음을 가리킬 경우 `localhost:4503` 또는 Adobe Campaign에서 연결할 수 없는 다른 서버에서는 AEM의 이미지가 Adobe Campaign 콘솔에 표시되지 않습니다.

## AEM에서 캠페인 원격 사용자 구성 {#configure-user}

Campaign에서 AEM과 통신하려면 AEM에서 `campaign-remote` 사용자에 대한 암호를 설정해야 합니다.

1. 관리자로 AEM에 로그인합니다.
1. 메인 탐색 콘솔에서 왼쪽 레일의 **도구**&#x200B;를 클릭합니다.
1. 그리고 **보안** -> **사용자**&#x200B;를 클릭하여 사용자 관리 콘솔을 엽니다.
1. `campaign-remote` 사용자를 찾습니다.
1. `campaign-remote` 사용자를 선택한 뒤 **속성**&#x200B;을 클릭하여 사용자를 편집합니다.
1. **사용자 설정 편집** 창에서 **암호 변경**&#x200B;을 클릭합니다.
1. 사용자에 대한 새 암호를 제공하고, 나중에 사용할 수 있도록 안전한 위치에 기록해 둡니다.
1. **저장**&#x200B;을 클릭하여 암호 변경사항을 저장합니다.
1. **저장 및 닫기**&#x200B;를 클릭하여 `campaign-remote` 사용자에 대한 변경사항을 저장합니다.

## Campaign에서 AEM 외부 계정 구성 {#acc-setup}

[**AEM 통합** 패키지를 Campaign에 설치할 때,](#install-package) AEM에 대한 외부 계정이 생성됩니다. Adobe Campaign은 이 외부 계정을 구성하여 AEM에 연결할 수 있으며, 이를 통해 솔루션 간에 양방향 통신이 가능합니다.

1. 클라이언트 콘솔을 사용해 관리자 자격으로 Adobe Campaign에 로그인합니다.

1. 메뉴 표시줄에서 **도구** -> **탐색기**&#x200B;를 선택합니다.

1. 탐색기에서 **관리** > **플랫폼** > **외부 계정** 노드로 이동합니다.

   ![외부 계정](assets/external-accounts.png)

1. 외부 AEM 계정을 찾습니다. 기본적으로 그 값은 다음과 같습니다.

   * **유형** - `AEM`
   * **레이블** - `AEM Instance`
   * **내부 이름** - `aemInstance`

1. [캠페인 원격 사용자 비밀번호 설정](#set-campaign-remote-password) 단계 수행 시 정의한 사용자 정보를 이 계정의 **일반** 탭에 입력합니다.

   * **서버** - AEM 제작자 서버 주소
      * AEM 제작자 서버는 Adobe Campaign Classic 서버 인스턴스에서 접근 가능해야 합니다.
      * 서버 주소가 뒤쪽 슬래시로 끝나지 **않아야** 합니다.
   * **계정** - 기본적으로, [캠페인 원격 사용자 암호 설정](#set-campaign-remote-password) 단계 수행 시 AEM에서 설정한 `campaign-remote` 사용자입니다.
   * **암호** - 이 암호는 [캠페인 원격 사용자 암호 설정](#set-campaign-remote-password) 단계 수행 시 AEM에서 설정한 `campaign-remote` 사용자와 동일합니다.

1. **활성화** 확인란을 선택합니다.

1. **저장**&#x200B;을 클릭합니다.

이제 Adobe Campaign이 AEM과 통신할 수 있습니다.

## 다음 단계 {#next-steps}

Adobe Campaign Classic과 AEM이 모두 구성되면 통합이 완료된 것입니다.

이번에는 [이 문서](/help/sites-authoring/campaign.md)를 계속 읽으며 Adobe Experience Manager에서 뉴스레터를 생성하는 방법에 대해 알아볼 수 있습니다.
