---
title: Adobe Campaign Standard과 통합
seo-title: Adobe Campaign Standard과 통합
description: Adobe Campaign Standard과 통합.
seo-description: Adobe Campaign Standard과 통합.
uuid: ef31339e-d925-499c-b8fb-c00ad01e38ad
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5c0fec99-7b1e-45d6-a115-e498d288e9e1
exl-id: caa43d80-1f38-46fc-a8b9-9485c235c0ca
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 1%

---

# Adobe Campaign Standard과 통합{#integrating-with-adobe-campaign-standard}

>[!NOTE]
>
>이 설명서는 AEM을 구독 기반 솔루션인 Adobe Campaign Standard과 통합하는 방법을 설명합니다. Adobe Campaign 6.1을 사용하는 경우 해당 지침은 [Adobe Campaign 6.1과 통합](/help/sites-administering/campaignonpremise.md)을 참조하십시오.

Adobe Campaign을 사용하면 Adobe Experience Manager에서 직접 이메일 게재 콘텐츠 및 양식을 관리할 수 있습니다.

두 솔루션을 동시에 사용하려면 먼저 서로 연결하도록 구성해야 합니다. 여기에는 Adobe Campaign과 Adobe Experience Manager 모두의 구성 단계가 포함됩니다. 이러한 단계는 이 문서에 자세히 설명되어 있습니다.

AEM에서 Adobe Campaign을 사용한 작업에는 Adobe Campaign을 통해 이메일과 양식을 전송하는 기능이 포함되며 [Adobe Campaign 작업](/help/sites-authoring/campaign.md)에 설명되어 있습니다.

또한 AEM을 [Adobe Campaign](https://docs.campaign.adobe.com/doc/standard/en/home.html)과 통합할 때 다음 주제가 관심이 있을 수 있습니다.

* [이메일 템플릿에 대한 우수 사례](/help/sites-administering/best-practices-for-email-templates.md)
* [Adobe Campaign 통합 문제 해결](/help/sites-administering/troubleshooting-campaignintegration.md)

Adobe Campaign과의 통합을 확장하는 경우 다음 페이지를 볼 수 있습니다.

* [사용자 지정 확장 프로그램 만들기](/help/sites-developing/extending-campaign-extensions.md)
* [사용자 지정 양식 매핑 만들기](/help/sites-developing/extending-campaign-form-mapping.md)

## Adobe Campaign 구성 {#configuring-adobe-campaign}

Adobe Campaign 구성에 다음이 포함됩니다.

1. **aemserver** 사용자 구성.
1. 전용 외부 계정 만들기
1. AEMRessourceTypeFilter 옵션을 확인하는 중입니다.
1. 전용 게재 템플릿 만들기

>[!NOTE]
>
>이러한 작업을 수행하려면 Adobe Campaign에 **관리** 역할이 있어야 합니다.

### 전제 조건 {#prerequisites}

미리 다음 요소가 있는지 확인합니다.

* [AEM 작성 인스턴스](/help/sites-deploying/deploy.md#getting-started)
* [AEM 게시 인스턴스](/help/sites-deploying/deploy.md#author-and-publish-installs)
* [Adobe Campaign 인스턴스](https://docs.adobe.com/content/docs/en/campaign/ACS.html)

>[!CAUTION]
>
>[Adobe Campaign 구성](#configuring-adobe-campaign) 및 [Adobe Experience Manager 구성](#configuring-adobe-experience-manager) 섹션에 설명된 작업은 AEM과 Adobe Campaign 간의 통합 기능이 제대로 작동하려면 필요합니다.

### aemserver 사용자 구성 {#configuring-the-aemserver-user}

**aemserver** 사용자는 Adobe Campaign에서 구성해야 합니다. **aemserver**&#x200B;는 AEM 서버를 Adobe Campaign에 연결하는 데 사용할 기술 사용자입니다.

**관리** > **사용자 및 보안** > **사용자**&#x200B;로 이동하고 **aemserver** 사용자를 선택합니다. 사용자 설정을 열려면 이 아이콘을 클릭합니다.

* 이 사용자의 암호를 설정해야 합니다. UI를 통해 이 작업을 수행할 수 없습니다. 이 구성은 기술 관리자가 REST에서 수행해야 합니다.
* 이 사용자에게 **deliveryPrepare** 등의 특정 역할을 할당하여 사용자가 게재를 만들고 편집할 수 있습니다.

### Adobe Experience Manager 외부 계정 구성 {#configuring-an-adobe-experience-manager-external-account}

Adobe Campaign을 AEM 인스턴스에 연결할 수 있도록 외부 계정을 구성해야 합니다.

>[!NOTE]
>
>AEM에서 campaign-remote 사용자의 암호를 설정해야 합니다. Adobe Campaign과 AEM을 연결하려면 이 암호를 설정해야 합니다. 관리자로 로그인하고 사용자 관리 콘솔에서 campaign-remote 사용자를 검색하고 **암호 설정**&#x200B;을 클릭합니다.

AEM 외부 계정을 구성하려면

1. **관리** > **애플리케이션 설정** > **외부 계정**&#x200B;으로 이동합니다.

   ![chlimage_1-124](assets/chlimage_1-124a.png)

1. 기본 **aemInstance** 외부 계정을 선택하거나 **만들기** 단추를 클릭하여 새 계정을 만듭니다.
1. **유형** 필드에서 **Adobe Experience Manager**&#x200B;을 선택하고 AEM 작성 인스턴스에 사용되는 액세스 매개 변수를 입력합니다.서버 주소, 계정 이름 및 암호

   >[!NOTE]
   >
   >URL의 끝에 끝 **/** 슬래시를 추가하지 않으면 연결이 작동하지 않습니다.

1. **Enabled** 확인란이 선택되어 있는지 확인한 다음 **Save**&#x200B;를 클릭하여 수정 내용을 저장합니다.

### AEMRessourceTypeFilter 옵션 확인 중 {#verifying-the-aemresourcetypefilter-option}

**AEMResourceTypeFilter** 옵션은 Adobe Campaign에서 사용할 수 있는 AEM 리소스 유형을 필터링하는 데 사용됩니다. 이렇게 하면 Adobe Campaign에서 Adobe Campaign에서만 사용하도록 특별히 설계된 AEM 컨텐츠를 검색할 수 있습니다.

이 옵션은 사전 구성되어 있습니다.그러나 이 옵션을 변경하면 작동하지 않는 통합이 발생할 수 있습니다.

**AEMResourceTypeFilter** 옵션이 구성되어 있는지 확인하려면:

1. **관리** > **애플리케이션 설정** > **옵션**&#x200B;으로 이동합니다.
1. 목록에서 **AEMRessourceTypeFilter** 옵션이 나열되고 경로가 올바른지 확인할 수 있습니다.

### AEM 관련 이메일 게재 템플릿 만들기 {#creating-an-aem-specific-email-delivery-template}

기본적으로 AEM 기능은 Adobe Campaign의 이메일 템플릿에서 활성화되지 않습니다. AEM 콘텐츠으로 이메일을 만드는 데 사용할 새 이메일 게재 템플릿을 구성할 수 있습니다.

AEM 관련 이메일 게재 템플릿을 만들려면 다음을 수행하십시오.

1. **리소스** > **템플릿** > **게재 템플릿**&#x200B;으로 이동합니다.
1. **작업** 표시줄에서 확인 표시를 클릭하고 기존  **표준 이메일(메일)**  기본 템플릿을 선택하여 선택 **** 을 활성화한 다음 복사 아이콘을 클릭하고  **확인**&#x200B;을 클릭하여 복제합니다.
1. **x**&#x200B;을 클릭하여 선택 모드를 비활성화하고 새로 만든 **표준 전자 메일 복사(메일)** 템플릿을 연 다음, 템플릿 대시보드의 작업 표시줄에서 **속성 편집**&#x200B;을 선택합니다.

   템플릿의 **Label**&#x200B;을 수정할 수 있습니다.

1. 속성 **Content** 섹션에서 **컨텐츠 소스**&#x200B;를 **Adobe Experience Manager**&#x200B;로 변경합니다. 그런 다음 이전에 만든 외부 계정을 선택하고 **확인**&#x200B;을 클릭합니다.

   **확인**&#x200B;을 클릭하고 **저장.**&#x200B;을 클릭하여 수정 내용을 저장합니다.

   이 템플릿에서 만든 이메일 게재에는 AEM 컨텐츠 기능이 활성화되어 있습니다.

   ![chlimage_1-125](assets/chlimage_1-125a.png)

## Adobe Experience Manager 구성 {#configuring-adobe-experience-manager}

AEM을 구성하려면 다음을 수행해야 합니다.

* 인스턴스 간 복제를 구성합니다.
* Adobe Campaign에 AEM 연결.
* 외부 도우미를 구성합니다.

### AEM 인스턴스 간 복제 구성 {#configuring-replication-between-aem-instances}

AEM 작성 인스턴스에서 만든 컨텐츠가 먼저 게시 인스턴스로 전송됩니다. 그런 다음 이 게시 인스턴스는 컨텐츠를 Adobe Campaign에 전송합니다. 따라서 AEM 작성 인스턴스에서 AEM 게시 인스턴스로 복제하도록 복제 에이전트를 구성해야 합니다.

>[!NOTE]
>
>복제 URL을 사용하지 않고 대신 공개 URL을 사용하는 경우, OSGi(**도구** > **웹 콘솔** > **OSGi 구성 > AEM Campaign 통합 - 구성**)의 다음 구성 설정에서 **공용 URL**&#x200B;을 설정할 수 있습니다.
**공개 URL:** com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl

이 단계는 특정 작성 인스턴스 구성을 게시 인스턴스에 복제하는 데도 필요합니다.

AEM 인스턴스 간 복제를 구성하려면:

1. 작성 인스턴스에서 **AEM 로고** **도구** > **배포** > **복제** > **작성자**&#x200B;의 에이전트를 선택한 다음 **기본 에이전트**&#x200B;를 클릭합니다.

   ![chlimage_1-126](assets/chlimage_1-126a.png)

   >[!NOTE]
   게시 및 작성자 인스턴스가 모두 동일한 컴퓨터에 있는 경우가 아니라면 Adobe Campaign과 통합을 구성할 때 localhost(AEM의 로컬 복사본)를 사용하지 마십시오.

1. **편집**&#x200B;을 클릭한 다음 **전송** 탭을 선택합니다.
1. **localhost** 를 AEM 게시 인스턴스의 IP 주소 또는 주소로 대체하여 URI를 구성합니다.

   ![chlimage_1-127](assets/chlimage_1-127a.png)

### AEM을 Adobe Campaign에 연결 {#connecting-aem-to-adobe-campaign}

AEM과 Adobe Campaign을 함께 사용하려면 먼저 두 솔루션 간에 링크를 설정하여 통신할 수 있어야 합니다.

1. AEM 작성 인스턴스에 연결합니다.
1. **도구** > **작업** > **클라우드** > **Cloud Services**&#x200B;을 선택한 다음 Adobe Campaign 섹션에서 **지금 구성**&#x200B;을 선택합니다.

   ![chlimage_1-128](assets/chlimage_1-128a.png)

1. **제목**&#x200B;을 입력하고 **만들기**&#x200B;를 클릭하거나 Adobe Campaign 인스턴스에 연결할 기존 구성을 선택하십시오.
1. Adobe Campaign 인스턴스의 매개 변수와 일치하도록 구성을 편집합니다.

   * **사용자 이름**: **aemserver**, 두 솔루션 간에 링크를 설정하는 데 사용되는 Adobe Campaign AEM 통합 패키지 연산자입니다.
   * **암호**:Adobe Campaign aemserver 운영자 암호. Adobe Campaign에서 직접 이 연산자의 암호를 다시 지정해야 할 수 있습니다.
   * **API 종료 지점**:Adobe Campaign 인스턴스 URL.

1. **Adobe Campaign에 연결**&#x200B;을 선택하고 **확인**&#x200B;을 클릭합니다.

   ![chlimage_1-129](assets/chlimage_1-129a.png)

   >[!NOTE]
   [이메일을 만들어 게시](/help/sites-authoring/campaign.md)하면 구성을 게시 인스턴스에 다시 게시해야 합니다.

   ![chlimage_1-130](assets/chlimage_1-130a.png)

>[!NOTE]
연결에 실패하면 다음을 확인하십시오.
* Adobe Campaign 인스턴스(https)에 대한 보안 연결을 사용할 때 인증서 문제가 발생할 수 있습니다. Adobe Campaign 인스턴스 인증서를 JDK의 **cacerts ** 파일에 추가해야 합니다.
* 또한 [AEM/Adobe Campaign 통합 문제 해결](/help/sites-administering/troubleshooting-campaignintegration.md)을 참조하십시오.



### 외부 도우미 구성 {#configuring-the-externalizer}

작성자 인스턴스에서 AEM에서 [외부 도우미](/help/sites-developing/externalizer.md)를 구성해야 합니다. Externalizer는 리소스 경로를 외부 및 절대 URL로 변환할 수 있는 OSGi 서비스입니다. 이 서비스는 이러한 외부 URL을 구성하고 빌드할 수 있는 중앙 위치를 제공합니다.

일반적인 지침은 [외부 도우미 구성](/help/sites-developing/externalizer.md)을 참조하십시오. Adobe Campaign 통합의 경우 `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`에서 게시 서버를 `localhost:4503`이 아닌 Adobe Campaign 콘솔에서 연결할 수 있는 서버에 구성해야 합니다.

`localhost:4503` 또는 Adobe Campaign이 연결할 수 없는 다른 서버를 가리키면 이미지가 Adobe Campaign 콘솔에 표시되지 않습니다.

![chlimage_1-131](assets/chlimage_1-131a.png)
