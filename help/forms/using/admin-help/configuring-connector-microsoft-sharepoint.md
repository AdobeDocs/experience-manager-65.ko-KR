---
title: Microsoft SharePoint용 커넥터 구성
description: AEM Forms와 Microsoft SharePoint 간의 통신을 활성화하도록 Microsoft SharePoint용 커넥터를 구성합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 100%
---

# Microsoft SharePoint용 커넥터 구성

>[!NOTE]
> 
> 사용자에게 관리 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

Microsoft SharePoint용 커넥터를 사용하면 AEM Forms와 Microsoft SharePoint 간의 통신이 가능합니다. 추가 배경 정보는 [서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)의 &#39;ECM용 커넥터&#39;를 참조하십시오.

1. 관리 콘솔에서 서비스 > Microsoft SharePoint용 커넥터를 클릭합니다.
2. SharePoint 서버에 대해 다음 설정을 지정합니다.

   **SharePoint 서버 호스트 이름:** SharePoint 서버의 웹 애플리케이션에 `[hostname]:'port'` 형식으로 지정된 호스트 이름 포트 번호입니다.

   **사용자 이름:** SharePoint 서버에 연결하는 데 사용되는 사용자 계정입니다.

   **암호:** SharePoint 서버에 연결하는 데 사용되는 사용자 계정의 암호입니다.

   **도메인 이름:** SharePoint 서버가 위치한 도메인입니다.

3. 저장을 클릭합니다.

## Microsoft SharePoint 구성 서비스 {#microsoft-sharepoint-configuration-service}

Microsoft SharePoint 구성 서비스`(MSSharePointConfigService)`를 사용하면 가장 권한이 있는 AEM Forms 사용자에 대한 자격 증명을 지정할 수 있습니다. 가장 권한에 대한 자세한 내용은[Microsoft SharePoint용 커넥터 구성](https://help.adobe.com/ko_KR/AEMForms/6.1/SharePointConfig/index.html)을 참조하십시오. 다음 단계를 따라 `MSSharePointConfigService`에 대한 설정을 지정합니다.

1. 관리 콘솔에서 서비스 > 애플리케이션 및 서비스 > 서비스 관리를 클릭합니다.
1. 서비스 목록을 탐색하고 `MSSharePointConfigService`를 클릭합니다.
1. 구성 페이지에서 다음 설정을 지정합니다.

   * 가장 권한이 있는 사용자의 사용자 이름
   * 위 사용자의 암호

1. 저장을 클릭합니다.
