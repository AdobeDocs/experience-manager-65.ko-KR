---
title: Experience Cloud 및 Creative Cloud과 AEM Assets 통합 구성
seo-title: Marketing Cloud 및 Creative Cloud과 AEM Assets 통합 구성
description: Experience Cloud 및 Creative Cloud과 AEM Assets 통합을 구성하는 방법을 알아봅니다.
seo-description: Experience Cloud 및 Creative Cloud과 AEM Assets 통합을 구성하는 방법을 알아봅니다.
uuid: ec36ea0e-607f-4c73-89df-e095067fccd4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 82a8e807-a2df-4fe3-a68c-2dabc9328eca
docset: aem65
translation-type: tm+mt
source-git-commit: 0560eb8e3c127964920827609a9982acf07b515f
workflow-type: tm+mt
source-wordcount: '1410'
ht-degree: 1%

---


# Experience Cloud 및 Creative Cloud {#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}과(와) AEM Assets 통합 구성

Adobe Experience Cloud 고객인 경우 Adobe Experience Manager Assets 내의 자산을 Adobe Creative Cloud과 동기화하거나 그 반대로 동기화할 수 있습니다. 또한 자산을 Experience Cloud과 동기화할 수 있으며 그 반대의 경우도 마찬가지입니다. [!DNL Adobe I/O]을(를) 통해 이 동기화를 설정할 수 있습니다.

이 통합을 설정하는 워크플로우는 다음과 같습니다.

1. 공용 게이트웨이를 사용하여 [!DNL Adobe I/O]에서 인증을 만들고 응용 프로그램 ID를 가져옵니다.
1. 응용 프로그램 ID를 사용하여 AEM Assets 인스턴스에 프로파일을 만듭니다.
1. 이 구성을 사용하여 AEM Assets 내의 자산을 Creative Cloud과 동기화합니다.

백 엔드에서 AEM 서버는 게이트웨이로 프로파일을 인증한 다음 AEM Assets과 Experience Cloud 간에 데이터를 동기화합니다.

>[!CAUTION]
>
>AEM-Creative Cloud 폴더 공유 기능은 AEM Assets에서 더 이상 사용되지 않습니다. 자세한 내용을 살펴보고 [AEM 및 Creative Cloud 통합 우수 사례](/help/assets/aem-cc-integration-best-practices.md)에서 대체 항목을 찾습니다.

![AEM Assets 및 Creative Cloud 통합 시 데이터 흐름](assets/chlimage_1-48.png)

AEM Assets 및 Creative Cloud 통합 시 데이터 흐름

>[!NOTE]
>
>Adobe Experience Cloud과 Adobe Creative Cloud 간에 자산을 공유하려면 AEM 인스턴스에 대한 관리자 권한이 필요합니다.

>[!CAUTION]
>
>Adobe Marketing Cloud은 Adobe Experience Cloud으로 다시 브랜딩되었습니다. 아래 절차에서는 현재 인터페이스를 반영하기 위해 Marketing Cloud을 언급합니다. 이러한 언급이 나중 날짜에 변경됩니다.

## 응용 프로그램 {#create-an-application} 만들기

1. [https://legacy-oauth.cloud.adobe.io](https://legacy-oauth.cloud.adobe.io/)에서 로그인하여 Adobe 개발자 게이트웨이 인터페이스에 액세스합니다.

   >[!NOTE]
   >
   >응용 프로그램 ID를 만들려면 관리자 권한이 필요합니다.

1. 왼쪽 창에서 **[!UICONTROL 개발자 도구]** > **[!UICONTROL 응용 프로그램]**&#x200B;으로 이동하여 응용 프로그램 목록을 봅니다.
1. 응용 프로그램을 만들려면 **[!UICONTROL 추가]** ![aem_assets_addcircle_icon](assets/aem_assets_addcircle_icon.png)을 클릭합니다.
1. **[!UICONTROL 클라이언트 자격 증명]** 목록에서 서버 인증을 위한 서버 간 통신 서비스인 **[!UICONTROL 서비스 계정(JWT 어설션)]**&#x200B;을 선택합니다.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 응용 프로그램의 이름과 선택적 설명을 지정합니다.
1. **[!UICONTROL 조직]** 목록에서 자산을 동기화할 조직을 선택합니다.
1. **[!UICONTROL 범위]** 목록에서 **[!UICONTROL dam-read]**, **[!UICONTROL dam-sync]**, **[!UICONTROL dam-write]** 및 **[!UICONTROL cc-share]**&#x200B;를 선택합니다.
1. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 응용 프로그램이 작성되었음을 알리는 메시지가 표시됩니다.

   ![Adobe CC와 AEM Assets을 통합하기 위한 애플리케이션 제작 성공 알림](assets/chlimage_1-50.png)

1. 새 응용 프로그램에 대해 생성된 **[!UICONTROL 응용 프로그램 ID]**&#x200B;를 복사합니다.

   >[!CAUTION]
   >
   >실수로 **[!UICONTROL 응용 프로그램 ID]** 대신 **[!UICONTROL 응용 프로그램 암호]**&#x200B;를 복사하지 않도록 하십시오.

## Marketing Cloud {#add-a-new-configuration-to-marketing-cloud}에 새 구성 추가

1. 로컬 AEM Assets 인스턴스의 사용자 인터페이스에서 AEM 로고를 클릭하고 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 기존 Cloud Services]**&#x200B;으로 이동합니다.

1. **[!UICONTROL Adobe Marketing Cloud]** 서비스를 찾습니다. 구성이 없는 경우 **[!UICONTROL 지금 구성]**&#x200B;을 클릭합니다. 구성이 있는 경우 **[!UICONTROL 구성 표시]**&#x200B;를 클릭하고 `+`를 클릭하여 새 구성을 추가합니다.

   >[!NOTE]
   >
   >조직에 대한 관리자 권한이 있는 Adobe ID 계정을 사용합니다.

1. **[!UICONTROL 구성 만들기]** 대화 상자에서 새 구성의 제목과 이름을 지정하고 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

   ![AEM Assets 및 CC 통합을 위한 새로운 구성 이름 지정](assets/chlimage_1-51.png)

1. **[!UICONTROL 테넌트 URL]** 필드에서 AEM Assets의 URL을 지정합니다.

   >[!CAUTION]
   >
   >리브랜딩으로 인해 테넌트 URL을 `https://<tenant_id>.marketing.adobe.com`으로 입력한 경우 `https://<tenant_id>.experiencecloud.adobe.com.`(으)로 변경해야 합니다. 이렇게 하려면 아래 단계를 따르십시오.
   >
   >1. **도구 > Cloud Services > 이전 Cloud Services**&#x200B;으로 이동합니다.
   1. Adobe Marketing Cloud에서 **구성 표시**&#x200B;를 클릭합니다.
   1. AEM-MAC-CC 동기화를 설정하는 동안 생성된 구성을 선택합니다.
   1. cloudservice 구성을 편집하고 테넌트 URL 필드의 **marketing.adobe.com**&#x200B;을(를) **experiencecloud.adobe.com**&#x200B;으로 바꿉니다.
   1. 구성을 저장합니다.
   1. mac 동기화 복제 에이전트를 테스트합니다.


1. **[!UICONTROL 클라이언트 ID]** 필드에서 [응용 프로그램 만들기](/help/sites-administering/configure-assets-cc-integration.md#create-an-application) 절차의 끝에 복사한 응용 프로그램 ID를 붙여 넣습니다.

   ![AEM Assets 및 Creative Cloud을 통합하는 데 필요한 응용 프로그램 ID 값을 제공합니다.](assets/cloudservices_tenant_info.png)

1. **[!UICONTROL 동기화]**&#x200B;에서 **[!UICONTROL 활성화됨]**&#x200B;을 선택하여 동기화를 활성화하고 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

   >[!NOTE]
   **disabled**&#x200B;를 선택하면 동기화가 한 방향으로 작동합니다.

1. 구성 페이지에서 **[!UICONTROL 공개 키 표시]**&#x200B;를 클릭하여 인스턴스에 대해 생성된 공개 키를 표시합니다. 또는 **[!UICONTROL OAuth 게이트웨이에 대한 공개 키 다운로드]**&#x200B;를 클릭하여 공개 키가 포함된 파일을 다운로드합니다. 그런 다음 파일을 열어 공개 키를 표시합니다.

## 동기화 사용 {#enable-synchronization}

1. [Marketing Cloud](/help/sites-administering/configure-assets-cc-integration.md#add-a-new-configuration-to-marketing-cloud)에 새 구성을 추가합니다. 절차의 마지막 단계에서 언급한 다음 방법 중 하나를 사용하여 공개 키를 표시합니다. **[!UICONTROL 공개 키 표시]**&#x200B;를 클릭합니다.

   ![chlimage_1-52](assets/chlimage_1-52.png)

1. 공개 키를 복사하여 [응용 프로그램 만들기](/help/sites-administering/configure-assets-cc-integration.md#create-an-application)에서 만든 응용 프로그램의 구성 인터페이스의 **[!UICONTROL 공개 키]** 필드에 붙여 넣습니다.

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. **[!UICONTROL 업데이트]**&#x200B;를 클릭합니다. 지금 AEM Assets 인스턴스와 자산을 동기화합니다.

## 동기화 테스트 {#test-the-synchronization}

1. 로컬 AEM Assets 인스턴스의 사용자 인터페이스에서 AEM 로고를 클릭하고 **[!UICONTROL 도구]** **[!UICONTROL 배포]** **[!UICONTROL 복제]**로 이동하여 동기화를 위해 만든 복제 프로필을 찾습니다.
1. **[!UICONTROL 복제]** 페이지에서 작성자&#x200B;]**의**[!UICONTROL &#x200B;에이전트를 클릭합니다.
1. 프로파일 목록에서 조직의 기본 복제 프로필을 클릭하여 엽니다.
1. 대화 상자에서 **[!UICONTROL 연결 테스트]**&#x200B;를 클릭합니다.

   ![연결 테스트 및 조직에 대한 기본 복제 프로필 설정](assets/chlimage_1-54.png)

1. 복제 공간이 완료되면 테스트 결과 마지막에 성공 메시지를 확인합니다.

## Marketing Cloud {#add-users-to-marketing-cloud}에 사용자 추가

1. 관리자 자격 증명을 사용하여 Marketing Cloud에 로그인합니다.
1. 레일에서 **[!UICONTROL 관리]**&#x200B;로 이동한 다음 **[!UICONTROL Enterprise Dashboard 시작]**&#x200B;을 클릭/탭합니다.
1. 레일에서 **[!UICONTROL 사용자]**&#x200B;를 클릭하여 **[!UICONTROL 사용자 관리]** 페이지를 엽니다.
1. 도구 모음에서 **추가** ![aem_assets_add_icon](assets/aem_assets_add_icon.png)을 클릭/탭합니다.
1. Creative Cloud과 자산을 공유할 수 있는 기능을 제공할 사용자를 하나 이상 추가합니다.

   >[!NOTE]
   Marketing Cloud에 추가한 사용자만 AEM Assets의 자산을 Creative Cloud에 공유할 수 있습니다.

## AEM Assets과 Marketing Cloud {#exchange-assets-between-aem-assets-and-marketing-cloud} 간 에셋 교환

1. AEM Assets에 로그인합니다.
1. 자산 콘솔에서 폴더를 만들고 여기에 자산을 업로드합니다. 예를 들어 **mc-demo** 폴더를 만들고 에셋을 이 폴더에 업로드합니다.
1. 폴더를 선택하고 **공유** ![assets_share](assets/assets_share.png)를 클릭합니다.
1. 메뉴에서 **[!UICONTROL Adobe Marketing Cloud]**&#x200B;을 선택하고 **[!UICONTROL 공유]**&#x200B;를 클릭합니다. 폴더가 Marketing Cloud과 공유되고 있음을 알리는 메시지가 표시됩니다.

   ![chlimage_1-55](assets/chlimage_1-55.png)

   >[!NOTE]
   `sling:OrderedFolder` 유형의 자산 폴더 공유는 Adobe Marketing Cloud에서 공유하는 컨텍스트에서 지원되지 않습니다. 폴더를 공유하려면 AEM Assets에서 폴더를 만들 때 **[!UICONTROL 주문됨]** 옵션을 선택하지 마십시오.

1. AEM Assets 사용자 인터페이스를 새로 고칩니다. 로컬 AEM Assets 인스턴스의 자산 콘솔에서 만든 폴더가 Marketing Cloud UI에 복사됩니다. AEM Assets의 폴더에 업로드하는 자산은 AEM 서버에서 처리한 후 Marketing Cloud의 폴더 사본에 나타납니다.
1. Marketing Cloud에 있는 폴더의 복제된 사본에 자산을 업로드할 수도 있습니다. 처리가 완료되면 AEM Assets의 공유 폴더에 자산이 표시됩니다.

## AEM Assets과 Creative Cloud {#exchange-assets-between-aem-assets-and-creative-cloud} 간 에셋 교환

>[!CAUTION]
AEM-Creative Cloud 폴더 공유 기능은 더 이상 사용되지 않습니다. 고객은 [Adobe 에셋 링크](https://helpx.adobe.com/kr/enterprise/using/adobe-asset-link.html) 또는 [AEM 데스크탑 앱](https://helpx.adobe.com/kr/experience-manager/desktop-app/aem-desktop-app.html)과 같은 최신 기능을 사용해야 합니다. [AEM 및 Creative Cloud 통합 우수 사례](/help/assets/aem-cc-integration-best-practices.md)에서 자세한 내용을 살펴보십시오.

AEM Assets을 사용하면 에셋이 포함된 폴더를 Adobe Creative Cloud 사용자와 공유할 수 있습니다.

1. 자산 콘솔에서 Creative Cloud과 공유할 폴더를 선택합니다.
1. 도구 모음에서 **[!UICONTROL 공유]** ![assets_share](assets/assets_share.png)를 클릭합니다.
1. 목록에서 **[!UICONTROL Adobe Creative Cloud]** 옵션을 선택합니다.

   >[!NOTE]
   루트에 대한 읽기 권한이 있는 사용자는 이 옵션을 사용할 수 있습니다. Marketing Cloud의 복제 에이전트 정보에 액세스하려면 사용자에게 필요한 권한이 있어야 합니다.

1. **[!UICONTROL Creative Cloud 공유]** 페이지에서 폴더를 공유할 사용자를 추가하고 사용자의 역할을 선택합니다. **[!UICONTROL 저장]**&#x200B;을 클릭하고 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

1. 폴더를 공유한 사용자의 자격 증명으로 Creative Cloud에 로그온합니다. 공유 폴더는 Creative Cloud에서 사용할 수 있습니다.

AEM Assets-Marketing Cloud 동기화는 자산이 업로드된 곳의 사용자 시스템 인스턴스가 자산을 수정할 수 있는 권한을 유지하는 방식으로 설계되었습니다. 이러한 변경 사항만 다른 인스턴스로 전파됩니다.

예를 들어 에셋이 AEM Assets(온-프레미스) 인스턴스에서 업로드된 경우 이 인스턴스의 에셋 변경 사항이 Marketing Cloud 인스턴스로 전파됩니다. 그러나 Marketing Cloud 인스턴스에서 동일한 에셋으로 수행된 변경 사항은 Marketing Cloud에서 업로드한 에셋에 대해 AEM 인스턴스로 전파되지 않으며 그 반대의 경우도 마찬가지입니다.

>[!MORELIKETHIS]
* [AEM 및 Creative Cloud 통합 우수 사례](/help/assets/aem-cc-integration-best-practices.md)
* [AEM에서 Creative Cloud으로 폴더 공유 우수 사례](/help/assets/aem-cc-folder-sharing-best-practices.md)

