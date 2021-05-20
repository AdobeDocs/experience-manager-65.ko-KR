---
title: AEM DS 설정 구성
seo-title: AEM DS 설정 구성
description: 양식을 제출하기 전에 처리 서버 URL을 지정해야 합니다.
seo-description: 양식을 제출하기 전에 처리 서버 URL을 지정해야 합니다.
uuid: 55a6d434-7352-48a8-8387-8a5c1a48fafc
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: a7387bd3-8b31-4bd0-a861-daa8f7cb2d05
docset: aem65
role: Administrator
exl-id: c43cab7b-3421-4e1b-a834-b2dd6eb23c1d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# AEM DS 설정 구성{#configuring-aem-ds-settings}

이 문서에서는 **AEM DS 설정 서비스**&#x200B;를 구성하는 방법에 대해 설명합니다. 이 설정은 다음과 같이 여러 시나리오에서 사용할 수 있습니다.

* 서신 관리

   * AEM Forms 워크플로우 구성
   * 양식 포털을 사용하여 초안/제출 원격 저장

* 게시 인스턴스에서 적응형 양식을 제출할 때 사례에 대한 적응형 양식에서

다음은 **[!UICONTROL AEM DS 설정]**&#x200B;을 구성하는 단계입니다.

1. URL을 사용하여 게시 인스턴스에서 구성 관리자를 엽니다.\
   *https://localhost:port/system/console/configMgr*&#x200B;에서 확인하십시오.

   ![AEM 웹 콘솔 구성](assets/web_configuration_console_new.png)

1. **[!UICONTROL Adobe Experience Manager 웹 콘솔 구성]** 창에서 **[!UICONTROL AEM DS 설정]** 옵션을 찾아 클릭합니다.

   ![DS 설정](assets/ds_settings_new.png)

1. **[!UICONTROL AEM DS 설정 서비스]** 창에는 AEM DS 구성 요소에 대한 공통 구성 설정이 표시됩니다.

   ![DS 설정 서비스](assets/ds_settings_service_new.png)

1. 각 필드에 다음 정보를 추가합니다.

   **[!UICONTROL 처리 서버 URL]**:처리 서버는 Forms 또는 AEM 워크플로우를 트리거해야 하는 서버입니다. AEM 작성자 인스턴스의 URL 또는 다른 서버 URL(즉, https://localhost:port/)과 같을 수 있습니다.

   **[!UICONTROL 처리 서버 사용자 이름]**:사용 중인 서버 URL을  [기반으로 하는 워크플로우 사용자의 사용자 이름]

   **[!UICONTROL 처리 서버 암호]**:워크플로우 사용자 암호

   >[!NOTE]
   >
   >
   >    
   >    
   >    * Forms 또는 AEM 워크플로우를 사용하는 동안 게시 서버에서 제출하기 전에 DS 설정 서비스를 구성해야 합니다. 그렇지 않으면 양식 제출이 실패합니다.



