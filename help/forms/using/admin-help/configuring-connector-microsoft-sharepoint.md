---
title: Microsoft SharePoint용 커넥터 구성
description: AEM Forms와 Microsoft SharePoint 간에 통신할 수 있도록 Microsoft SharePoint용 커넥터를 구성합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 98cbaaf64c0268be1afe7196a7bbbf5c93f02148
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 1%

---


# Microsoft SharePoint용 커넥터 구성

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인합니다.

Microsoft SharePoint용 커넥터를 사용하면 AEM Forms와 Microsoft SharePoint 간에 통신할 수 있습니다. 추가 배경 정보는 [서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)의 &quot;ECM용 커넥터&quot;를 참조하십시오.

1. 관리 콘솔에서 서비스 > Microsoft SharePoint용 커넥터 를 클릭합니다.
2. SharePoint 서버에 대해 다음 설정을 지정합니다.

   **SharePoint 서버 호스트 이름:** SharePoint 서버에 있는 웹 응용 프로그램의 호스트 이름 포트 번호(`[hostname]:'port'` 형식)입니다.

   **사용자 이름:** SharePoint 서버에 연결하는 데 사용되는 사용자 계정입니다.

   **암호:** SharePoint 서버에 연결하는 데 사용되는 사용자 계정의 암호입니다

   SharePoint 서버가 있는 **도메인 이름:** 도메인.

3. 저장을 클릭합니다.

## Microsoft SharePoint 구성 서비스 {#microsoft-sharepoint-configuration-service}

Microsoft SharePoint 구성 서비스 `(MSSharePointConfigService)`을(를) 사용하면 가장 권한이 있는 AEM Forms 사용자에 대한 자격 증명을 지정할 수 있습니다. 가장 권한에 대한 자세한 내용은 [Microsoft SharePoint에 대한 커넥터 구성](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html)을 참조하십시오. `MSSharePointConfigService`에 대한 설정을 지정하려면 다음 단계를 따르십시오.

1. 관리 콘솔에서 서비스 > 애플리케이션 및 서비스 > 서비스 관리 를 클릭합니다.
1. 서비스 목록을 탐색하고 `MSSharePointConfigService`을(를) 클릭합니다.
1. [구성] 페이지에서 다음 설정을 지정합니다.

   * 가장 권한이 있는 사용자의 사용자 이름
   * 위 사용자의 암호

1. 저장을 클릭합니다.
