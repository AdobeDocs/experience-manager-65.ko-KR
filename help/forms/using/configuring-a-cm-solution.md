---
title: 통신 관리 솔루션 구성
seo-title: 통신 관리 솔루션 구성
description: 'null'
seo-description: 'null'
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444

---


# 통신 관리 솔루션 구성 {#configuring-a-correspondence-management-solution}

## VersionRestoreManagerImpl에 대한 작성자 인스턴스 URL 정의 {#defining-author-instance-url-for-versionrestoremanagerimpl}

다음 단계를 사용하여 작성자 인스턴스 버전 복원에 대한 작성자 인스턴스 URL을 정의합니다.

1. https://:&lt; *PublishHost>:&lt;PublishPort>/lc/system/console/configMgr로 이동합니다*. OSGi 관리 콘솔 사용자 자격 증명으로 로그인합니다. 기본 자격 증명은 admin/admin입니다.
1. com.adobe.livecycle. **[!UICONTROL content]** .activate.impl.VersionRestoreManagerImpl.name **** 설정 옆에 있는 편집 아이콘을 찾아 클릭합니다.
1. VersionRestoreManager **[!UICONTROL 작성자 URL]** 필드에서 VersionRestoreManager의 작성자 인스턴스의 URL을 지정합니다.

   **URL 문자열**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >로드 밸런서에 의해 앞에 작성자 인스턴스(클러스터됨)가 여러 개 있는 경우 VersionRestoreManager 작성자 URL **[!UICONTROL 필드에서 로드 밸런서에 대한 URL을 지정합니다]** .

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

## ActivationManagerImpl(공개 인스턴스 활성화 관리자)에 대한 게시 인스턴스 URL 정의 {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

공개 인스턴스 활성화 관리자를 위한 게시 인스턴스 URL을 정의하려면 다음 단계를 수행합니다.

1. https://:&lt; *authorHost>:&lt;authorPort>/lc/system/console/configMgr로 이동합니다*. OSGi 관리 콘솔 사용자 자격 증명으로 로그인합니다. 기본 자격 증명은 admin/admin입니다.
1. com.adobe.livecycle. **[!UICONTROL content]** .activate.impl.ActivationManagerImpl.name **** 설정 옆에 있는 편집 아이콘을 찾아 클릭합니다.
1. ActivationManager **[!UICONTROL 게시 URL]** 필드에서 게시 인스턴스 ActivationManager에 액세스할 URL을 지정합니다. 다음 URL을 제공할 수 있습니다.

   * **부하 균형 조정기 URL(권장)**:부하 균형 조정기 URL 제공, 웹 서버가 게시 팜 앞에 부하 균형 조정기 역할을 하는 경우(클러스터되지 않은 다중 게시 인스턴스).
   * **게시 인스턴스 URL**:모든 게시 인스턴스 URL 제공, 단일 게시 인스턴스가 있거나 제한 사항으로 인해 게시 팜을 앞에 있는 웹 서버에 액세스할 수 없는 경우. 지정된 게시 인스턴스가 다운된 경우 작성자 측에서 처리할 폴백 메커니즘이 있습니다.
   * **URL 문자열**:

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

통신 관리 구성에 대한 자세한 내용은 통신 관리 [구성 속성을 참조하십시오](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html).
