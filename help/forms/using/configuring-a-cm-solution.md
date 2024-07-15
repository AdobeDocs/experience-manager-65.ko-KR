---
title: 서신 관리 솔루션 구성
description: AEM Forms 환경에서 서신 관리 솔루션을 구성하는 방법을 알아봅니다.
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
feature: Correspondence Management
exl-id: f7f5eb0d-a283-45ea-84d3-d6375d2bb95b
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# 서신 관리 솔루션 구성 {#configuring-a-correspondence-management-solution}

## VersionRestoreManagerImpl의 작성자 인스턴스 URL 정의 {#defining-author-instance-url-for-versionrestoremanagerimpl}

작성자 인스턴스 버전 복원에 대한 작성자 인스턴스 URL을 정의하려면 다음 단계를 따르십시오.

1. *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr*(으)로 이동합니다. OSGi 관리 콘솔 사용자 자격 증명으로 로그인합니다. 기본 자격 증명은 관리자/관리자입니다.
1. **[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]** 설정 옆에 있는 **[!UICONTROL 편집]** 아이콘을 찾아 클릭합니다.
1. **[!UICONTROL VersionRestoreManager 작성자 URL]** 필드에 VersionRestoreManager 작성자 인스턴스의 URL을 지정하십시오.

   **URL 문자열**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >로드 밸런서에 의해 앞쪽에 작성자 인스턴스(클러스터됨)가 여러 개 있는 경우 **[!UICONTROL VersionRestoreManager 작성자 URL]** 필드에 로드 밸런서에 대한 URL을 지정하십시오.

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

## ActivationManagerImpl(공개 인스턴스 활성화 관리자)에 대한 Publish 인스턴스 URL 정의 {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

공개 인스턴스 활성화 관리자에 대한 Publish 인스턴스 URL을 정의할 수 있도록 다음 단계를 수행합니다.

1. *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr*(으)로 이동합니다. OSGi 관리 콘솔 사용자 자격 증명으로 로그인합니다. 기본 자격 증명은 관리자/관리자입니다.
1. **[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]** 설정 옆에 있는 **[!UICONTROL 편집]** 아이콘을 찾아 클릭합니다.
1. **[!UICONTROL ActivationManager Publish URL]** 필드에서 Publish 인스턴스 ActivationManager에 액세스하기 위한 URL을 지정합니다. 다음 URL을 제공할 수 있습니다.

   * **로드 밸런서 URL(권장)**: 게시 팜(클러스터되지 않은 여러 게시 인스턴스) 앞에 로드 밸런서 역할을 하는 웹 서버가 있는 경우 로드 밸런서 URL을 제공합니다.
   * **Publish 인스턴스 URL**: 단일 게시 인스턴스가 있거나 제한 사항으로 인해 작성 환경에서 게시 팜을 연결하는 웹 서버에 액세스할 수 없는 경우 게시 인스턴스 URL을 제공합니다. 지정된 게시 인스턴스가 다운된 경우 작성자 측에서 처리할 대체 메커니즘이 있습니다.
   * **URL 문자열**:

     `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

서신 관리 구성에 대한 자세한 내용은 [서신 관리 구성 속성](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html)을 참조하세요.
