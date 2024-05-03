---
title: Forms 포털 구성 요소 활성화
description: 기본적으로 Forms 포털 구성 요소는 비활성화됩니다. Document Services 및 Document Services 술어 그룹을 활성화하여 Forms 포털 구성 요소를 활성화합니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
feature: Forms Portal
exl-id: 572194b7-063b-4c38-af43-aba78e9c51c6
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 5%

---

# Forms 포털 구성 요소 활성화 {#enabling-forms-portal-components}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-forms-portal.html) |
| AEM 6.5 | 이 문서 |

기본적으로 Forms 포털 구성 요소는 사용할 수 없습니다. 구성 요소가 AEM 사이드 킥에서 사용 가능한 구성 요소 목록에 표시되도록 하려면 다음 단계를 수행하십시오.

1. 웹 사이트의 작성자 인스턴스에 로그인하고 AEM Sites 페이지를 엽니다.

1. 정적 템플릿을 사용하는 페이지의 경우 다음 단계를 수행하십시오.

   1. 페이지 헤더에서 을 선택합니다. ![캔버스 드롭다운](assets/canvas-drop-down.png) > **디자인** 디자인 모드에서 페이지를 엽니다.
   1. 파란색 테두리로 구성 요소를 선택한 다음 를 선택합니다 ![필드 수준](assets/field-level.png) 현재 구성 요소가 포함된 단락 시스템을 선택합니다.
   1. 단락 시스템에서 을 선택합니다. ![settings_icon](assets/settings_icon.png) 를 클릭하여 단락 시스템의 편집 대화 상자를 엽니다.
   1. 목록에서 **[!UICONTROL 허용된 구성 요소]**, 확인란 활성화 **[!UICONTROL 문서 서비스]** 및 **[!UICONTROL 문서 서비스 조건자]** 구성 요소. 선택 **[!UICONTROL 확인]**.

1. 동적 템플릿을 사용하는 페이지의 경우 다음 단계를 수행하십시오.

   1. 페이지 헤더에서 을 선택합니다. ![속성](assets/properties.png) > **템플릿 편집** 을 클릭하여 페이지의 템플릿을 엽니다.
   1. 선택 **레이아웃 컨테이너** 및 선택 ![FeedManagement](/help/forms/using/assets/feedmanagement.png). 다음에서 **허용된 구성 요소** 탭, 활성화 **문서 서비스 및 문서 서비스 조건자** 옵션 및 선택 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

>[!NOTE]
>
>구성 요소를 선택하여 이러한 범주의 특정 구성 요소를 활성화할 수도 있습니다. 구성 요소 및 그 사용에 대한 자세한 내용은 [양식 포털 페이지 만들기](/help/forms/using/creating-form-portal-page.md) 및 [페이지에 링크 구성 요소 포함](/help/forms/using/embedding-link-component-page.md).

이제 구성 요소 브라우저에서 문서 서비스 및 문서 서비스 조건자 구성 요소 범주를 사용할 수 있습니다. 구성 요소는 동일한 템플릿을 사용하는 모든 페이지에 대해 활성화됩니다.

## 관련 문서

* [Forms 포털 구성 요소 활성화](/help/forms/using/enabling-forms-portal-components.md)
* [Forms 포털 페이지 만들기](/help/forms/using/creating-form-portal-page.md)
* [API를 사용하여 웹 페이지의 목록 양식](/help/forms/using/listing-forms-webpage-using-apis.md)
* [초안 및 제출 구성 요소 사용](/help/forms/using/draft-submission-component.md)
* [초안 및 제출된 양식의 스토리지 사용자 지정](/help/forms/using/draft-submission-component.md)
* [초안 및 제출 구성 요소와 데이터베이스를 통합하기 위한 샘플](/help/forms/using/integrate-draft-submission-database.md)
* [Forms 포털 구성 요소에 대한 템플릿 맞춤화](/help/forms/using/customizing-templates-forms-portal-components.md)
* [포털에 양식 게시 소개](/help/forms/using/introduction-publishing-forms.md)
