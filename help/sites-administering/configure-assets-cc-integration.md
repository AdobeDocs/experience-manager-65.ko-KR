---
title: Experience Cloud과 AEM Assets 통합 구성
description: Experience Cloud과 AEM Assets 통합을 구성하는 방법을 알아봅니다.
contentOwner: AG
feature: Asset Management
role: Business Practitioner, Architect, Administrator
translation-type: tm+mt
source-git-commit: a9c9194ac1d163be3ab642ab5a6323de02d67363
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 1%

---


# Experience Cloud {#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}과(와) AEM Assets 통합 구성

Adobe Experience Cloud 고객인 경우 Adobe Experience Manager Assets 내의 자산을 Adobe Creative Cloud과 동기화하거나 그 반대로 동기화할 수 있습니다. 또한 자산을 Experience Cloud과 동기화할 수 있으며 그 반대의 경우도 마찬가지입니다. [!DNL Adobe I/O]을 통해 이 동기화를 설정할 수 있습니다. 업데이트된 [!DNL Adobe Marketing Cloud] 이름은 [!DNL Adobe Experience Cloud]입니다.

이 통합을 설정하는 워크플로우는 다음과 같습니다.

1. 공용 게이트웨이를 사용하여 [!DNL Adobe I/O]에서 인증을 만들고 응용 프로그램 ID를 가져옵니다.
1. 응용 프로그램 ID를 사용하여 AEM Assets 인스턴스에 프로파일을 만듭니다.
1. 이 구성을 사용하여 자산을 동기화합니다.

백 엔드에서 AEM 서버는 게이트웨이로 프로파일을 인증한 다음 에셋과 Experience Cloud 간에 데이터를 동기화합니다.

>[!NOTE]
>
>이 기능은 AEM Assets에서 더 이상 사용되지 않습니다. [AEM 및 Creative Cloud 통합 우수 사례](/help/assets/aem-cc-integration-best-practices.md)에서 대체 항목을 찾습니다. 질문이 있으면 [Adobe 고객 지원 센터](https://www.adobe.com/account/sign-in.supportportal.html)에 문의하십시오.

<!-- Hiding this for now via cqdoc-16834.
![Flow of data when AEM Assets and Creative Cloud are integrated](assets/chlimage_1-48.png)

>[!NOTE]
>
>Sharing assets between Adobe Experience Cloud and Adobe Creative Cloud requires administrator privileges on the AEM instance.
-->

## 응용 프로그램 {#create-an-application} 만들기

1. [https://legacy-oauth.cloud.adobe.io](https://legacy-oauth.cloud.adobe.io/)에서 로그인하여 Adobe 개발자 게이트웨이 인터페이스에 액세스합니다.

   >[!NOTE]
   >
   >응용 프로그램 ID를 만들려면 관리자 권한이 필요합니다.

1. 왼쪽 창에서 **[!UICONTROL 개발자 도구]** > **[!UICONTROL 응용 프로그램]**&#x200B;으로 이동하여 응용 프로그램 목록을 봅니다.
1. **[!UICONTROL 추가]** ![aem_assets_addcircle_icon](assets/aem_assets_addcircle_icon.png)을 클릭하여 애플리케이션을 만듭니다.
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

## Experience Cloud {#add-a-new-configuration}에 새 구성 추가

1. 로컬 AEM Assets 인스턴스의 사용자 인터페이스에서 AEM 로고를 클릭하고 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 기존 Cloud Services]**&#x200B;으로 이동합니다.

1. **[!UICONTROL Adobe Experience Cloud]** 서비스를 찾습니다. 구성이 없는 경우 **[!UICONTROL 지금 구성]**&#x200B;을 클릭합니다. 구성이 있는 경우 **[!UICONTROL 구성 표시]**&#x200B;를 클릭하고 `+`를 클릭하여 새 구성을 추가합니다.

   >[!NOTE]
   >
   >조직에 대한 관리자 권한이 있는 Adobe ID 계정을 사용합니다.

1. **[!UICONTROL 구성 만들기]** 대화 상자에서 새 구성의 제목과 이름을 지정하고 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

   ![AEM Assets 및 CC 통합을 위한 새로운 구성 이름 지정](assets/aem-ec-integration-config1.png)

1. **[!UICONTROL 테넌트 URL]** 필드에서 AEM Assets의 URL을 지정합니다. 과거에는 URL이 `https://<tenant_id>.marketing.adobe.com`으로 정의된 경우 `https://<tenant_id>.experiencecloud.adobe.com`으로 변경하십시오.

   1. **도구 > Cloud Services > 이전 Cloud Services**&#x200B;으로 이동합니다. Adobe Experience Cloud에서 **구성 표시**&#x200B;를 클릭합니다.
   1. 편집할 기존 구성을 선택합니다. 구성을 편집하고 `marketing.adobe.com`을(를) `experiencecloud.adobe.com`로 바꿉니다.
   1. 구성을 저장합니다. MAC 동기화 복제 에이전트를 테스트합니다.

1. **[!UICONTROL 클라이언트 ID]** 필드에서 [응용 프로그램](#create-an-application) 만들기 절차의 끝에 복사한 응용 프로그램 ID를 붙여 넣습니다.

   ![AEM Assets 및 Creative Cloud을 통합하는 데 필요한 응용 프로그램 ID 값을 제공합니다.](assets/cloudservices_tenant_info.png)

1. **[!UICONTROL 동기화]**&#x200B;에서 **[!UICONTROL 활성화됨]**&#x200B;을 선택하여 동기화를 활성화하고 **[!UICONTROL 확인]**&#x200B;을 클릭합니다. **disabled**&#x200B;를 선택하면 동기화가 한 방향으로 작동합니다.

1. 구성 페이지에서 **[!UICONTROL 공개 키 표시]**&#x200B;를 클릭하여 인스턴스에 대해 생성된 공개 키를 표시합니다. 또는 **[!UICONTROL OAuth 게이트웨이에 대한 공개 키 다운로드]**&#x200B;를 클릭하여 공개 키가 포함된 파일을 다운로드합니다. 그런 다음 파일을 열어 공개 키를 표시합니다.

## 동기화 사용 {#enable-synchronization}

1. [Experience Cloud](#add-a-new-configuration)에 새 구성을 추가하는 절차의 마지막 단계에서 언급한 다음 방법 중 하나를 사용하여 공개 키를 표시합니다. **[!UICONTROL 공개 키 표시]**&#x200B;를 클릭합니다.

1. 공개 키를 복사하여 [만들기 응용 프로그램](#create-an-application)에서 만든 구성 인터페이스의 **[!UICONTROL 공개 키]** 필드에 붙여 넣습니다.

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. **[!UICONTROL 업데이트]**&#x200B;를 클릭합니다. 지금 AEM Assets 인스턴스와 자산을 동기화합니다.

## 동기화 테스트 {#test-the-synchronization}

1. 로컬 AEM Assets 인스턴스의 사용자 인터페이스에서 AEM 로고를 클릭하고 **[!UICONTROL 도구]** **[!UICONTROL 배포]** **[!UICONTROL 복제]**로 이동하여 동기화를 위해 만든 복제 프로필을 찾습니다.
1. **[!UICONTROL 복제]** 페이지에서 작성자&#x200B;]**의**[!UICONTROL &#x200B;에이전트를 클릭합니다.
1. 프로파일 목록에서 조직의 기본 복제 프로필을 클릭하여 엽니다.
1. 대화 상자에서 **[!UICONTROL 연결 테스트]**&#x200B;를 클릭합니다.

   ![연결 테스트 및 조직에 대한 기본 복제 프로필 설정](assets/chlimage_1-54.png)

1. 복제 공간이 완료되면 테스트 결과 마지막에 성공 메시지를 확인합니다.

## Experience Cloud {#add-users-to-experience-cloud}에 사용자 추가

1. 관리자 자격 증명을 사용하여 Experience Cloud에 로그인합니다.
1. 레일에서 **[!UICONTROL 관리]**&#x200B;로 이동한 다음 **[!UICONTROL Enterprise Dashboard 시작]**&#x200B;을 클릭합니다.
1. 레일에서 **[!UICONTROL 사용자]**&#x200B;를 클릭하여 **[!UICONTROL 사용자 관리]** 페이지를 엽니다.
1. 도구 모음에서 **추가** ![aem_assets_add_icon](assets/aem_assets_add_icon.png)을 클릭합니다.
1. Creative Cloud과 자산을 공유할 수 있는 기능을 제공할 사용자를 하나 이상 추가합니다.

<!-- TBD: Check.
   >[!NOTE]
   >
   >Only the users that you add to Experience Cloud can share assets from AEM Assets to Creative Cloud.

-->

## AEM Assets과 Experience Cloud {#exchange-assets-between-aem-and-experience-cloud} 간 에셋 교환

1. AEM Assets에 로그인합니다.
1. 자산 콘솔에서 폴더를 만들고 여기에 자산을 업로드합니다. 예를 들어 **mc-demo** 폴더를 만들고 에셋을 이 폴더에 업로드합니다.
1. 폴더를 선택하고 **공유** ![assets_share](assets/do-not-localize/assets_share.png)를 클릭합니다.
1. 메뉴에서 **[!UICONTROL Adobe Experience Cloud]**&#x200B;을 선택하고 **[!UICONTROL 공유]**&#x200B;를 클릭합니다. 폴더가 Experience Cloud과 공유되고 있음을 알리는 메시지가 표시됩니다.

   >[!NOTE]
   >
   >`sling:OrderedFolder` 유형의 자산 폴더 공유는 Adobe Experience Cloud에서 공유하는 컨텍스트에서 지원되지 않습니다. 폴더를 공유하려면 AEM Assets에서 폴더를 만들 때 **[!UICONTROL 주문됨]** 옵션을 선택하지 마십시오.

1. AEM Assets 사용자 인터페이스를 새로 고칩니다. 로컬 AEM Assets 인스턴스의 자산 콘솔에서 만든 폴더가 Experience Cloud 사용자 인터페이스에 복사됩니다. AEM Assets의 폴더에 업로드하는 자산은 AEM 서버에서 처리한 후 Experience Cloud의 폴더 사본에 나타납니다.
1. Experience Cloud에 있는 폴더의 복제된 사본에 자산을 업로드할 수도 있습니다. 처리가 완료되면 AEM Assets의 공유 폴더에 자산이 표시됩니다.

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

For example, if an asset is uploaded from an AEM Assets (on premises) instance, the changes to the asset from this instance are propagated to the Marketing Cloud instance. However, the changes done from the Marketing Cloud instance to the same asset aren’t propagated to the AEM instance and vice versa for asset uploaded from Marketing Cloud.
-->

>[!MORELIKETHIS]
>
>* [자산 및 Creative Cloud 통합 우수 사례](/help/assets/aem-cc-integration-best-practices.md)
>* [최상의 작업 방법을 공유하는 Creative Cloud 폴더에 에셋 공유](/help/assets/aem-cc-folder-sharing-best-practices.md)

