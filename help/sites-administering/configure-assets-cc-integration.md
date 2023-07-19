---
title: Experience Cloud과 AEM Assets 통합 구성
description: Experience Cloud과 AEM Assets 통합을 구성하는 방법에 대해 알아봅니다.
contentOwner: AG
feature: Asset Management
role: User, Architect, Admin
exl-id: d167cf97-6829-45a7-ba46-2239d530b060
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 2%

---

# Experience Cloud과 AEM Assets 통합 구성 {#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}

Adobe Experience Cloud 고객인 경우 Adobe Experience Manager Assets 내의 에셋을 Adobe Creative Cloud과 동기화할 수 있으며 그 반대의 경우도 가능합니다. 에셋을 Experience Cloud과 동기화하거나 반대로 동기화할 수 있습니다. 다음을 통해 이 동기화를 설정할 수 있습니다. [!DNL Adobe I/O]. 의 업데이트된 이름 [!DNL Adobe Marketing Cloud] 은(는) [!DNL Adobe Experience Cloud].

이 통합을 설정하는 워크플로우는 다음과 같습니다.

1. 에서 인증 만들기 [!DNL Adobe I/O] 공용 게이트웨이를 사용하고 애플리케이션 ID를 가져옵니다.
1. 애플리케이션 ID를 사용하여 AEM Assets 인스턴스에 프로필을 만듭니다.
1. 이 구성을 사용하여 자산을 동기화합니다.

백엔드에서 AEM 서버는 게이트웨이로 프로필을 인증한 다음 에셋과 Experience Cloud 간에 데이터를 동기화합니다.

>[!NOTE]
>
>이 기능은에서 더 이상 사용되지 않습니다. [!DNL Assets]. 에서 대체 항목 찾기 [AEM 및 Creative Cloud 통합 우수 사례](/help/assets/aem-cc-integration-best-practices.md). 문의사항이 있으시면, [Adobe 고객 지원 문의](https://www.adobe.com/kr/account/sign-in.supportportal.html).

<!-- Hiding this for now via cqdoc-16834.
![Flow of data when AEM Assets and Creative Cloud are integrated](assets/chlimage_1-48.png)

>[!NOTE]
>
>Sharing assets between Adobe Experience Cloud and Adobe Creative Cloud requires administrator privileges on the AEM instance.
-->

## 애플리케이션 만들기 {#create-an-application}

1. 에 로그인하여 Adobe Developer 게이트웨이 인터페이스에 액세스 [https://legacy-oauth.cloud.adobe.io](https://legacy-oauth.cloud.adobe.io/).

   >[!NOTE]
   >
   >응용 프로그램 ID를 생성하려면 관리자 권한이 필요합니다.

1. 왼쪽 창에서 다음으로 이동합니다. **[!UICONTROL 개발자 도구]** > **[!UICONTROL 애플리케이션]** 응용 프로그램 목록을 봅니다.
1. 클릭 **[!UICONTROL 추가]** ![aem_assets_addcircle_icon](assets/aem_assets_addcircle_icon.png) 응용 프로그램을 만듭니다.
1. 다음에서 **[!UICONTROL 클라이언트 자격 증명]** 목록, 선택 **[!UICONTROL 서비스 계정(JWT 어설션)]**- 서버 인증을 위한 서버 간 통신 서비스입니다.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 응용 프로그램의 이름과 설명(선택 사항)을 지정합니다.
1. 다음에서 **[!UICONTROL 조직]** 목록에서 자산을 동기화할 조직을 선택합니다.
1. 다음에서 **[!UICONTROL 범위]** 목록, 선택 **[!UICONTROL dam-read]**, **[!UICONTROL dam-sync]**, **[!UICONTROL dam-write]**, 및 **[!UICONTROL cc-share]**.
1. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 애플리케이션이 생성되었음을 알리는 메시지가 표시됩니다.

   ![AEM Assets을 Creative Cloud과 통합할 애플리케이션 만들기 성공 알림](assets/chlimage_1-50.png)

1. 다음을 복사합니다. **[!UICONTROL 애플리케이션 ID]** 새 애플리케이션에 대해 생성됩니다.

   >[!CAUTION]
   >
   >실수로 **[!UICONTROL 애플리케이션 암호]** 대신 **[!UICONTROL 애플리케이션 ID]**.

## Experience Cloud에 새 구성 추가 {#add-a-new-configuration}

1. 로컬 AEM Assets 인스턴스의 사용자 인터페이스에서 AEM 로고를 클릭하고 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 이전 Cloud Services]**.

1. 를 찾습니다. **[!UICONTROL Adobe Experience Cloud]** 서비스. 구성이 없는 경우 **[!UICONTROL 지금 구성]**. 구성이 있는 경우 **[!UICONTROL 구성 표시]** 및 클릭 `+` 새 구성을 추가합니다.

   >[!NOTE]
   >
   >조직에 대한 관리자 권한이 있는 Adobe ID 계정을 사용합니다.

1. 다음에서 **[!UICONTROL 구성 만들기]** 대화 상자에서 새 구성의 제목과 이름을 지정하고 **[!UICONTROL 만들기]**.

   ![AEM Assets 및 Creative Cloud을 통합할 새 구성 이름 지정](assets/aem-ec-integration-config1.png)

1. 다음에서 **[!UICONTROL 임차인 URL]** 필드에서 AEM Assets의 URL을 지정합니다. 이전에는 URL이 로 정의된 경우 `https://<tenant_id>.marketing.adobe.com`, 다음으로 변경 `https://<tenant_id>.experiencecloud.adobe.com`.

   1. Navigate to **Tools > Cloud Services > Legacy Cloud Services**. Adobe Experience Cloud에서 **구성 표시**.
   1. 편집할 기존 구성을 선택합니다. 구성 편집 및 바꾸기 `marketing.adobe.com` 끝 `experiencecloud.adobe.com`.
   1. 구성을 저장합니다. Mac 동기화 복제 에이전트를 테스트합니다.

1. 다음에서 **[!UICONTROL 클라이언트 ID]** 필드, 프로시저 끝에 복사한 응용 프로그램 ID를 붙여 넣습니다. [응용 프로그램 만들기](#create-an-application).

   ![AEM Assets 및 Creative Cloud 통합에 필요한 애플리케이션 ID 값 제공](assets/cloudservices_tenant_info.png)

1. 아래 **[!UICONTROL 동기화]** 선택 **[!UICONTROL 활성화됨]** 동기화를 활성화하려면 다음을 클릭하십시오. **[!UICONTROL 확인]**. 다음을 선택하는 경우 **비활성화됨**, 동기화는 단일 방향으로 작동합니다.

1. 구성 페이지에서 **[!UICONTROL 공개 키 표시]** 을 클릭하여 인스턴스에 대해 생성된 공개 키를 표시합니다. 또는 를 클릭합니다 **[!UICONTROL OAuth 게이트웨이용 공개 키 다운로드]** 을 클릭하여 공개 키가 포함된 파일을 다운로드합니다. 그런 다음 파일을 열어 공개 키를 표시합니다.

## 동기화 활성화 {#enable-synchronization}

1. 절차의 마지막 단계에서 언급된 다음 방법 중 하나를 사용하여 공개 키를 표시합니다 [Experience Cloud에 새 구성 추가](#add-a-new-configuration). 클릭 **[!UICONTROL 공개 키 표시]**.

1. 공개 키를 복사하여 **[!UICONTROL 공개 키]** 만든 응용 프로그램의 구성 인터페이스 필드 [응용 프로그램 만들기](#create-an-application).

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. **[!UICONTROL 업데이트]**&#x200B;를 클릭합니다. 이제 자산을 AEM Assets 인스턴스와 동기화합니다.

## 동기화 테스트 {#test-the-synchronization}

1. 로컬 AEM Assets 인스턴스의 사용자 인터페이스에서 AEM 로고를 클릭하고 **[!UICONTROL 도구]**> **[!UICONTROL 배포]**> **[!UICONTROL 복제]**동기화를 위해 생성된 복제 프로필을 찾습니다.
1. 다음에서 **[!UICONTROL 복제]** 페이지, 클릭 **[!UICONTROL 작성자의 에이전트]**.
1. 프로필 목록에서 조직의 기본 복제 프로필을 클릭하여 엽니다.
1. 대화 상자에서 **[!UICONTROL 연결 테스트]**.

   ![연결을 테스트하고 조직의 기본 복제 프로필 설정](assets/chlimage_1-54.png)

1. 복제 중단이 완료되면 테스트 결과가 끝날 때 성공 메시지를 확인합니다.

## Experience Cloud에 사용자 추가 {#add-users-to-experience-cloud}

1. 관리자 자격 증명을 사용하여 Experience Cloud에 로그인합니다.
1. 레일에서 로 이동합니다. **[!UICONTROL 관리]** 그런 다음 을 클릭합니다. **[!UICONTROL Enterprise Dashboard 시작]**.
1. 레일에서 **[!UICONTROL 사용자]** 을(를) 열려면 **[!UICONTROL 사용자 관리]** 페이지를 가리키도록 업데이트하는 중입니다.
1. 도구 모음에서 를 클릭합니다 **추가** ![aem_assets_add_icon](assets/aem_assets_add_icon.png).
1. Creative Cloud과 에셋을 공유하는 기능을 제공할 사용자를 한 명 이상 추가합니다.

<!-- TBD: Check.
   >[!NOTE]
   >
   >Only the users that you add to Experience Cloud can share assets from AEM Assets to Creative Cloud.

-->

## AEM Assets과 Experience Cloud 간 자산 교환 {#exchange-assets-between-aem-and-experience-cloud}

1. AEM Assets에 로그인.
1. 에셋 콘솔에서 폴더를 만들고 일부 에셋을 업로드합니다. 예를 들어 폴더를 만듭니다 **mc-demo** 에셋을 업로드할 수 있습니다.
1. 폴더를 선택하고 **공유** ![assets_share](assets/do-not-localize/assets_share.png).
1. 메뉴에서 을(를) 선택합니다 **[!UICONTROL Adobe Experience Cloud]** 및 클릭 **[!UICONTROL 공유]**. 폴더가 Experience Cloud과 공유되었다는 메시지가 표시됩니다.

   >[!NOTE]
   >
   >유형의 에셋 폴더 공유 `sling:OrderedFolder`는 Adobe Experience Cloud의 공유 컨텍스트에서 지원되지 않습니다. 폴더를 공유하려면 AEM Assets에서 폴더를 만들 때 **[!UICONTROL 주문됨]** 옵션을 선택합니다.

1. AEM Assets 사용자 인터페이스를 새로 고칩니다. 로컬 AEM Assets 인스턴스의 Assets 콘솔에서 만든 폴더가 Experience Cloud 사용자 인터페이스에 복사됩니다. AEM Assets의 폴더에 업로드하는 에셋은 AEM 서버에서 처리된 후 Experience Cloud의 폴더 사본에 표시됩니다.
1. Experience Cloud 폴더의 복제된 복사본에 에셋을 업로드할 수도 있습니다. 자산이 처리되면 AEM Assets의 공유 폴더에 자산이 표시됩니다.

<!-- Removing as per PM guidance via https://jira.corp.adobe.com/browse/CQDOC-16834?focusedCommentId=22881523&page=com.atlassian.jira.plugin.system.issuetabpanels:comment-tabpanel#comment-22881523.

## Exchange assets between AEM Assets and Creative Cloud {#exchange-assets-between-aem-assets-and-creative-cloud}

>[!CAUTION]
>
>The AEM to Creative Cloud Folder Sharing feature is deprecated. Customers are strongly advised to use newer capabilities, like [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) or [AEM desktop app](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html). Learn more in [AEM and Creative Cloud Integration Best Practices](/help/assets/aem-cc-integration-best-practices.md).

AEM Assets lets you share folders containing assets with Adobe Creative Cloud users.

1. In the Assets console, select the folder to share with Creative Cloud.
1. From the toolbar, click **[!UICONTROL Share]** ![assets_share](assets/do-not-localize/assets_share.png).
1. From the list, select the **[!UICONTROL Adobe Creative Cloud]** option.

   >[!NOTE]
   >
   >The options are available for users with read permissions on the root. Users must have the required permission to access the replication agent information of Marketing Cloud.

1. In the **[!UICONTROL Creative Cloud Sharing]** page, add the user to share the folder with and choose a role for the user. Click **[!UICONTROL Save]** and click **[!UICONTROL OK]**.

1. Log on to Creative Cloud with the credentials of the user you shared the folder with. The shared folder is available in Creative Cloud.

The AEM Assets-Marketing Cloud synchronization is designed in a way that the user machine instance from where the asset is uploaded retains the right to modify the asset. Only these changes are propagated to the other instance.

For example, if an asset is uploaded from an AEM Assets (on premises) instance, the changes to the asset from this instance are propagated to the Marketing Cloud instance. However, the changes done from the Marketing Cloud instance to the same asset aren’t propagated to the AEM instance and conversely for asset uploaded from Marketing Cloud.
-->

>[!MORELIKETHIS]
>
>* [자산 및 Creative Cloud 통합 우수 사례](/help/assets/aem-cc-integration-best-practices.md)
