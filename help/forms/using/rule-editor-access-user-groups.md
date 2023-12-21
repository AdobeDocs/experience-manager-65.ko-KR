---
title: 사용자 그룹을 선택하는 규칙 편집기 액세스 부여
description: 규칙 편집기에 대한 제한된 액세스 권한을 부여하여 사용자 그룹을 선택합니다.
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: a1a2b277-3133-404b-a7fc-337cedddb12c
source-git-commit: 4ecdcb2659b26043f95ba1dc3e907c33f65b8834
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 15%

---

# 사용자 그룹을 선택하는 규칙 편집기 액세스 부여{#grant-rule-editor-access-to-select-user-groups}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 Forms을 작성하는 이전 방법에 대해 설명합니다. </span>

## 개요 {#overview}

적응형 Forms과 작동하는 다양한 스킬을 가진 다양한 유형의 사용자가 있을 수 있습니다. 전문가 사용자는 스크립트와 복잡한 규칙으로 작업할 수 있는 적절한 지식을 보유할 수 있지만 적응형 양식의 레이아웃과 기본 속성으로만 작업해야 하는 기본 수준 사용자가 있을 수 있습니다.

AEM Forms을 사용하면 규칙 편집기의 역할이나 기능에 따라 사용자에 대한 액세스를 제한할 수 있습니다. 적응형 Forms 구성 서비스 설정에서 다음을 지정할 수 있습니다. [사용자 그룹](/help/sites-administering/security.md) 규칙 편집기를 보고 액세스할 수 있습니다.

## 규칙 편집기에 액세스할 수 있는 사용자 그룹 지정 {#specify-user-groups-that-can-access-rule-editor}

1. 관리자로 AEM Forms에 로그인합니다.
1. 작성자 인스턴스에서 ![adobeexperiencemanger](assets/adobeexperiencemanager.png)Adobe Experience Manager > 도구 ![망치](assets/hammer.png) > 작업 > 웹 콘솔. 웹 콘솔이 새 창에 열립니다.

   ![1-2](assets/1-2.png)

1. 웹 콘솔 창에서 을 찾아 클릭합니다. **[!UICONTROL 적응형 양식 및 대화형 통신 웹 채널 구성]**. **[!UICONTROL 적응형 양식 및 대화형 통신 웹 채널 구성]** 대화 상자가 나타납니다. 값을 변경하지 말고 클릭 **저장**.

   CRX-repository에 /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config 파일이 만들어집니다.

1. CRXDE에 관리자로 로그인합니다. 편집할 /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config 파일을 엽니다.
1. 다음 속성을 사용하여 규칙 편집기(예: RuleEditorsUserGroup)에 액세스할 수 있는 그룹의 이름을 지정하고 **모두 저장**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   여러 그룹에 대한 액세스를 활성화하려면 쉼표로 구분된 값 목록을 지정합니다.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![사용자 만들기](assets/create_user_new.png)

   이제 지정된 사용자 그룹(여기서는 RuleEditorsUserGroup)에 속하지 않는 사용자가 필드를 탭하면 규칙 편집 아이콘( ![edit-rules1](assets/edit-rules1.png))은 구성 요소 도구 모음에서 사용할 수 없습니다.

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   규칙 편집기 액세스 권한이 있는 사용자가 볼 수 있는 구성 요소 도구 모음

   ![componentstoolbarwithout](assets/componentstoolbarwithoutre.png)

   규칙 편집기 액세스 권한 없이 사용자가 볼 수 있는 구성 요소 도구 모음

   그룹에 사용자를 추가하는 방법에 대한 지침은 [사용자 관리 및 보안](/help/sites-administering/security.md).
