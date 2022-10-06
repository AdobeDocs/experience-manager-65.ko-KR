---
title: 사용자 그룹을 선택하는 규칙 편집기 액세스 부여
seo-title: Grant rule editor access to select user groups
description: 사용자 그룹을 선택하려면 규칙 편집기에 대한 제한된 액세스 권한을 부여합니다.
seo-description: Grant restricted access to rule editor to select user groups.
uuid: efa2570a-20ac-4b43-8a0e-38247f84d02f
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab694a93-00d2-44d7-8ded-68ab2ad50693
docset: aem65
feature: Adaptive Forms
exl-id: a1a2b277-3133-404b-a7fc-337cedddb12c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 6%

---

# 사용자 그룹을 선택하는 규칙 편집기 액세스 부여{#grant-rule-editor-access-to-select-user-groups}

## 개요 {#overview}

적응형 Forms과 함께 작동하는 다양한 기술을 사용하는 다양한 유형의 사용자가 있을 수 있습니다. 전문가 사용자는 스크립트 및 복잡한 규칙으로 작업하는 데 필요한 올바른 지식을 가지고 있을 수 있지만 적응형 양식의 레이아웃 및 기본 속성으로만 작업해야 하는 기본 수준 사용자가 있을 수 있습니다.

AEM Forms에서는 규칙 편집기 액세스를 사용자의 역할이나 기능을 기준으로 제한합니다. 응용 Forms 구성 서비스 설정에서 [사용자 그룹](/help/sites-administering/security.md) 규칙 편집기를 보고 액세스할 수 있습니다.

## 규칙 편집기에 액세스할 수 있는 사용자 그룹을 지정합니다 {#specify-user-groups-that-can-access-rule-editor}

1. 관리자로 AEM Forms에 로그인합니다.
1. 작성자 인스턴스에서 를 클릭합니다. ![adobeexperiencemanager](assets/adobeexperiencemanager.png)Adobe Experience Manager > 도구 ![망치](assets/hammer.png) > 작업 > 웹 콘솔. 웹 콘솔이 새 창에 열립니다.

   ![1-2](assets/1-2.png)

1. 웹 콘솔 창에서 을(를) 찾아 클릭합니다. **[!UICONTROL 적응형 양식 및 대화형 통신 웹 채널 구성]**. **[!UICONTROL 적응형 양식 및 대화형 통신 웹 채널 구성]** 대화 상자가 나타납니다. 값을 변경하지 않고 **저장**.

   CRX-repository에 /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config 파일을 만듭니다.

1. 관리자로 CRXDE에 로그인합니다. 편집할 /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config 파일을 엽니다.
1. 다음 속성을 사용하여 규칙 편집기에 액세스할 수 있는 그룹 이름(예: RuleEditorsUserGroup)을 지정하고 **모두 저장**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   여러 그룹에 대한 액세스를 활성화하려면 쉼표로 구분된 값 목록을 지정합니다.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![사용자 만들기](assets/create_user_new.png)

   이제 지정된 사용자 그룹(여기서는 RuleEditorsUserGroup)의 일부가 아닌 사용자가 필드를 탭하면 규칙 편집 아이콘( ![edit-rules1](assets/edit-rules1.png))은 구성 요소 도구 모음에서 사용할 수 없습니다.

   ![componentstoolbarwitter](assets/componentstoolbarwithre.png)

   구성 요소 도구 모음이 규칙 편집기 액세스 권한을 가진 사용자에게 표시되는 대로 표시됩니다

   ![componentstoolbarwithout](assets/componentstoolbarwithoutre.png)

   규칙 편집기 액세스 권한이 없는 사용자에게 표시되는 구성 요소 도구 모음

   그룹에 사용자 추가에 대한 지침은 [사용자 관리 및 보안](/help/sites-administering/security.md).
