---
title: ExactTarget과 통합
seo-title: ExactTarget과 통합
description: AEM과 ExactTarget을 통합하는 방법을 살펴보십시오.
seo-description: AEM과 ExactTarget을 통합하는 방법을 살펴보십시오.
uuid: a53bbdaa-98f7-4035-b842-aa7ea63712ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5b2f624d-e5b8-4484-a773-7784ebce58bd
docset: aem65
translation-type: tm+mt
source-git-commit: 0eda6ee61acf737abc91d1e5df731e719663b3f2
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---


# ExactTarget{#integrating-with-exacttarget}과 통합

AEM과 Exact Target을 통합하면 AEM에서 만든 이메일을 정확한 Target을 통해 관리하고 보낼 수 있습니다. AEM 페이지에서 AEM 양식을 통해 정확한 Target의 리드 관리 기능을 사용할 수도 있습니다.

통합은 다음과 같은 기능을 제공합니다.

* AEM에서 이메일을 만들어 배포를 위해 정확한 Target에 게시하는 기능
* AEM 양식의 작업을 설정하여 정확한 Target 구독자를 만드는 기능

ExactTarget이 구성된 후 ExactTarget에 뉴스레터 또는 이메일을 게시할 수 있습니다. [이메일 서비스에 뉴스레터 게시](/help/sites-authoring/personalization.md)를 참조하십시오.

## ExactTarget 구성 만들기 {#creating-an-exacttarget-configuration}

ExactTarget 구성은 Cloudservices 또는 도구를 통해 추가할 수 있습니다. 두 방법 모두 이 섹션에 설명되어 있습니다.

### Cloudservices {#configuring-exacttarget-via-cloudservices}을 통해 ExactTarget 구성

Cloud Services에서 ExactTarget 구성을 만들려면:

1. 시작 페이지에서 **Cloud Services**&#x200B;을 클릭합니다. (또는 `https://<hostname>:<port>/etc/cloudservices.html`에서 직접 액세스합니다.)
1. **ExactTarget**&#x200B;을 클릭한 다음 **구성**&#x200B;을 클릭합니다. ExactTarget 구성 창이 열립니다.

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. 제목을 입력하고 원할 경우 이름을 입력하고 **만들기**&#x200B;를 클릭합니다. **ExactTarget 설정** 구성 창이 열립니다.

   ![chlimage_1](assets/chlimage_1.jpeg)

1. 사용자 이름, 암호를 입력하고 API 끝점을 선택합니다(예: **https://webservice.exacttarget.com/Service.asmx**).
1. **ExactTarget에 연결을 클릭합니다.** 성공적으로 연결되면 성공 대화 상자가 표시됩니다. **확인**&#x200B;을 클릭하여 창을 종료합니다.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 가능한 경우 계정을 선택합니다. 이 계정은 Enterprise 2.0 고객을 위한 것입니다. **확인**&#x200B;을 클릭합니다.

   ExactTarget이 구성되었습니다. **편집**&#x200B;을 클릭하여 구성을 편집할 수 있습니다. **ExactTarget**&#x200B;으로 이동을 클릭하여 ExactTarget으로 이동할 수 있습니다.

1. 이제 AEM에서 데이터 확장 기능을 제공합니다. ExactTarget 데이터 확장 열을 가져올 수 있습니다. 성공적으로 생성된 ExactTarget 구성 옆에 있는 &quot;+&quot; 기호를 클릭하여 구성할 수 있습니다. 드롭다운 목록에서 기존 데이터 확장명을 선택할 수 있습니다. 데이터 확장을 구성하는 방법에 대한 자세한 내용은 [ExactTarget 설명서](https://help.exacttarget.com/en/documentation/exacttarget/subscribers/data_extensions_and_data_relationships)를 참조하십시오.

   가져온 데이터 확장 열은 나중에 **텍스트 및 개인화** 구성 요소를 통해 사용할 수 있습니다.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### {#configuring-exacttarget-via-tools} 도구를 통해 ExactTarget 구성

도구에서 ExactTarget 구성을 만들려면:

1. 시작 페이지에서 **도구**&#x200B;를 클릭합니다. 또는 `https://<hostname>:<port>/misadmin#/etc`으로 이동하여 직접 탐색합니다.
1. **도구**&#x200B;를 선택하고 **Cloud Services 구성**&#x200B;을 선택한 다음 **ExactTarget**&#x200B;을 선택합니다.
1. **새로 만들기**&#x200B;를 클릭하여 **페이지 만들기 ** 창을 엽니다.

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. **제목**&#x200B;과 선택적으로 **이름**&#x200B;을 입력하고 **만들기**&#x200B;를 클릭합니다.
1. 이전 절차의 4단계에서 설명한 대로 구성 정보를 입력합니다. 해당 절차를 따라 ExactTarget 구성을 완료합니다.

### 여러 구성 추가 중 {#adding-multiple-configurations}

여러 구성을 추가하려면:

1. 시작 페이지에서 **Cloud Services**&#x200B;을 클릭하고 **ExactTarget**&#x200B;을 클릭합니다. 하나 이상의 ExactTarget 구성을 사용할 수 있는 경우 나타나는 **구성 표시** 단추를 클릭합니다. 사용 가능한 모든 구성이 나열됩니다.
1. 사용 가능한 구성 옆에 있는 **+** 기호를 클릭합니다. **구성 만들기** 창이 열립니다. 이전 구성 절차를 따라 새 구성을 만듭니다.