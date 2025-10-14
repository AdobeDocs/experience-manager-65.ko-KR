---
title: ExactTarget과 통합
description: Adobe Experience Manager을 ExactTarget과 통합하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 4183fe78-5055-4b77-8a54-55666e86a04e
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 2%

---

# ExactTarget과 통합{#integrating-with-exacttarget}

Adobe Experience Manager(AEM)를 정확한 타겟과 통합하면 정확한 타겟을 통해 AEM에서 생성된 이메일을 관리하고 전송할 수 있습니다. 또한 AEM 페이지에서 AEM Forms를 통해 Exact Target의 리드 관리 기능을 사용할 수 있습니다.

통합은 다음과 같은 기능을 제공합니다.

* AEM에서 이메일을 만들고 배포를 위해 정확한 Target에 게시하는 기능입니다.
* 정확한 Target 구독자를 만들기 위해 AEM 양식의 작업을 설정하는 기능입니다.

ExactTarget이 구성되면 뉴스레터 또는 이메일을 ExactTarget에 게시할 수 있습니다. [전자 메일 서비스에 뉴스레터 게시](/help/sites-authoring/personalization.md)를 참조하십시오.

## ExactTarget 구성 만들기 {#creating-an-exacttarget-configuration}

ExactTarget 구성은 Cloudservices 또는 도구를 통해 추가할 수 있습니다. 두 방법 모두 이 섹션에 설명되어 있습니다.

### Cloudservices를 통해 ExactTarget 구성 {#configuring-exacttarget-via-cloudservices}

Cloud Service에서 ExactTarget 구성을 만들려면 다음 작업을 수행하십시오.

1. 시작 페이지에서 **Cloud Service**&#x200B;을 클릭합니다. 또는 `https://<hostname>:<port>/etc/cloudservices.html`에서 직접 액세스할 수 있습니다.
1. **ExactTarget**&#x200B;을 클릭한 다음 **구성**&#x200B;을 클릭합니다. ExactTarget 구성 창이 열립니다.

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. 제목과 이름을 입력하고 **만들기**&#x200B;를 클릭합니다. **ExactTarget 설정** 구성 창이 열립니다.

   ![chlimage_1](assets/chlimage_1.jpeg)

1. 사용자 이름과 암호를 입력하고 API 끝점을 선택합니다(예: **https://webservice.exacttarget.com/Service.asmx**).
1. **ExactTarget에 연결을 클릭합니다.** 연결되면 성공 대화 상자가 표시됩니다. 상자 창을 종료하려면 **확인**&#x200B;을 클릭합니다.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 가능한 경우 계정을 선택합니다. 이 계정은 Enterprise 2.0 고객용입니다. **확인**&#x200B;을 클릭합니다.

   ExactTarget이 구성되었습니다. **편집**&#x200B;을 클릭하여 구성을 편집할 수 있습니다. **ExactTarget으로 이동**&#x200B;을 클릭하여 ExactTarget으로 이동할 수 있습니다.

1. 이제 AEM에서 데이터 확장 기능을 제공합니다. ExactTarget 데이터 확장 열을 가져올 수 있습니다. ExactTarget 구성을 만든 것 외에 표시되는 &quot;+&quot; 기호를 클릭하여 구성할 수 있습니다. 드롭다운 목록에서 기존 데이터 확장을 선택할 수 있습니다. 데이터 확장을 구성하는 방법에 대한 자세한 내용은 [ExactTarget 설명서](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_relationships_classic.htm&type=5)를 참조하십시오.

   가져온 데이터 확장 열은 나중에 **Text 및 Personalization** 구성 요소를 통해 사용할 수 있습니다.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### 도구를 통한 ExactTarget 구성 {#configuring-exacttarget-via-tools}

도구에서 ExactTarget 구성을 만들려면 다음 작업을 수행하십시오.

1. 시작 페이지에서 **도구**&#x200B;를 클릭합니다. 또는 `https://<hostname>:<port>/misadmin#/etc`(으)로 이동하여 바로 탐색하십시오.
1. **도구**, **Cloud Service 구성,**, **ExactTarget**&#x200B;을 선택하십시오.
1. **새로 만들기**&#x200B;를 클릭하여 **페이지 만들기**&#x200B;창을 엽니다.

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. **제목** 및 **이름**(선택 사항)을 입력하고 **만들기**&#x200B;를 클릭합니다.
1. 이전 절차의 4단계에 설명된 대로 구성 정보를 입력합니다. 다음 절차에 따라 ExactTarget 구성을 완료합니다.

### 여러 구성 추가 {#adding-multiple-configurations}

여러 구성을 추가하려면 다음 작업을 수행하십시오.

1. 시작 페이지에서 **Cloud Service**&#x200B;을 클릭하고 **ExactTarget**&#x200B;을 클릭합니다. 하나 이상의 ExactTarget 구성을 사용할 수 있는 경우 표시되는 **구성 표시**&#x200B;를 클릭합니다. 사용 가능한 모든 구성이 나열됩니다.
1. 사용 가능한 구성 옆에 있는 **+** 기호를 클릭합니다. **구성 만들기** 창이 열립니다. 구성을 만들려면 이전 구성 절차를 따르십시오.
