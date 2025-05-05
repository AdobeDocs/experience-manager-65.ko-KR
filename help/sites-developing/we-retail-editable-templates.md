---
title: We.Retail에서 편집 가능한 템플릿 시험 사용
description: We.Retail을 사용하여 Adobe Experience Manager에서 편집 가능한 템플릿을 테스트하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: efebe66d-3d30-4033-9c4c-ae347e134f2f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 2%

---

# We.Retail에서 편집 가능한 템플릿 시험 사용{#trying-out-editable-templates-in-we-retail}

편집 가능한 템플릿을 사용하면 템플릿 작성 및 유지 관리가 더 이상 개발자 전용 작업이 아닙니다. 이제 템플릿 작성자라고 하는 고급 사용자 유형이 템플릿을 만들 수 있습니다. 개발자는 여전히 환경을 설정하고, 클라이언트 라이브러리를 만들고, 사용할 구성 요소를 만들어야 하지만, 이러한 기본 사항이 갖추어지면 템플릿 작성자는 개발 프로젝트 없이 템플릿을 만들고 구성할 수 있는 유연성을 갖게 됩니다.

We.Retail의 모든 페이지는 편집 가능한 템플릿을 기반으로 하므로 개발자가 아닌 사용자도 템플릿을 조정하고 맞춤화할 수 있습니다.

## 시험 사용 {#trying-it-out}

1. 언어 마스터 분기의 장비 페이지를 편집합니다.

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html

1. 모드 선택기에서 더 이상 디자인 모드를 제공하지 않습니다. We.Retail의 모든 페이지는 편집 가능한 템플릿을 기반으로 하며 편집 가능한 템플릿의 디자인을 변경하려면 템플릿 편집기에서 편집해야 합니다.
1. **페이지 정보** 메뉴에서 **템플릿 편집**&#x200B;을 선택합니다.
1. 이제 Hero 페이지 템플릿을 편집하고 있습니다.

   페이지의 구조 모드에서는 템플릿의 구조를 수정할 수 있습니다. 예를 들어 레이아웃 컨테이너에서 허용되는 구성 요소가 여기에 포함됩니다.

   ![chlimage_1-138](assets/chlimage_1-138.png)

1. 레이아웃 컨테이너 정책을 구성하여 컨테이너에 허용되는 구성 요소를 정의합니다.

   정책은 디자인 구성과 동일합니다.

   ![chlimage_1-139](assets/chlimage_1-139.png)

1. 레이아웃 컨테이너의 디자인 대화 상자에서 다음 작업을 수행할 수 있습니다

   * 기존 정책을 선택하거나 컨테이너에 대한 정책을 만듭니다.
   * 컨테이너에서 허용되는 구성 요소 선택
   * 자산을 컨테이너로 드래그할 때 배치할 기본 구성 요소 정의

   ![chlimage_1-140](assets/chlimage_1-140.png)

1. 템플릿 편집기로 돌아가 레이아웃 컨테이너 내에서 텍스트 구성 요소의 정책을 편집할 수 있습니다.

   이렇게 하면 다음 작업을 수행할 수 있습니다.

   * 기존 정책을 선택하거나 컨테이너에 대한 정책을 만듭니다.
   * 다음과 같은 이 구성 요소를 사용할 때 페이지 작성자가 사용할 수 있는 기능을 정의합니다.

      * 허용된 붙여넣기 소스
      * 서식 옵션
      * 허용된 단락 스타일
      * 허용되는 특수 문자

   핵심 구성 요소를 기반으로 하는 다양한 구성 요소를 통해 편집 가능한 템플릿을 통해 구성 요소 수준에서 옵션을 구성할 수 있으므로 개발자는 맞춤화를 수행할 필요가 없습니다.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 템플릿 편집기로 돌아가서 모드 선택기를 사용하여 **초기 콘텐츠** 모드로 변경하여 페이지에 필요한 콘텐츠를 정의할 수 있습니다.

   **레이아웃** 모드를 일반 페이지에서 그대로 사용하여 템플릿의 레이아웃을 정의할 수 있습니다.

## 추가 정보 {#more-information}

자세한 내용은 작성 문서 [페이지 템플릿 만들기](/help/sites-authoring/templates.md) 또는 개발자 문서 페이지 [템플릿 - 편집 가능](/help/sites-developing/page-templates-editable.md)에서 편집 가능한 템플릿에 대한 전체 기술 정보를 참조하십시오.

[핵심 구성 요소](/help/sites-developing/we-retail-core-components.md)를 조사할 수도 있습니다. 핵심 구성 요소의 기능에 대한 개요는 작성 문서 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ko-KR)를 참조하고, 기술 개요는 개발자 문서 [핵심 구성 요소 개발](https://helpx.adobe.com/kr/experience-manager/core-components/using/developing.html)을 참조하십시오.
