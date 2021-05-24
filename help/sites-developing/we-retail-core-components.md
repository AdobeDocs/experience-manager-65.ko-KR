---
title: We.Retail에서 핵심 구성 요소 시험 사용
seo-title: We.Retail에서 핵심 구성 요소 시험 사용
description: We.Retail에서 핵심 구성 요소 시험 사용
seo-description: 'null'
uuid: 8d1cea0b-99d9-49b2-b275-41f14864b1ff
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: af3cd818-61cf-4da1-bfb5-87540911ddd5
exl-id: b5f2be67-c93c-4dbc-acc0-3edd8f1a282f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 8%

---

# We.Retail에서 핵심 구성 요소 시험 사용{#trying-out-core-components-in-we-retail}

핵심 구성 요소는 쉬운 확장성을 제공하고 프로젝트에 간편하게 통합할 수 있는 현대적이고 유연한 구성 요소입니다. 핵심 구성 요소는 HTL, 사용 편의성, 구성 기능, 버전 관리 및 확장성과 같은 몇 가지 주요 디자인 원칙에 따라 구축되었습니다. We.Retail은 핵심 구성 요소를 기반으로 구축되었습니다.

## {#trying-it-out} 시험 사용

1. We.Retail 샘플 컨텐츠로 AEM을 시작하고 [구성 요소 콘솔](/help/sites-authoring/default-components-console.md)을 엽니다.

   **전역 탐색 -> 도구 -> 구성 요소**

1. 구성 요소 콘솔에서 레일을 열면 특정 구성 요소 그룹에 대해 필터링할 수 있습니다. 핵심 구성 요소는

   * `.core-wcm`:표준 코어 구성 요소
   * `.core-wcm-form`:양식 제출 핵심 구성 요소

   `.core-wcm`을 선택합니다.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. 모든 코어 구성 요소의 이름은 **v1** 이며, 이것이 이 코어 구성 요소의 첫 번째 버전임을 나타냅니다. 앞으로 일반 버전은 AEM과 버전 호환되며 간편한 업그레이드를 통해 최신 기능을 이용할 수 있습니다.
1. **텍스트(v1)**&#x200B;를 클릭합니다.

   구성 요소의 **리소스 유형**&#x200B;이 `/apps/core/wcm/components/text/v1/text`인지 확인합니다. 코어 구성 요소는 `/apps/core/wcm/components` 아래에 있으며 구성 요소별로 버전이 지정됩니다.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. **설명서** 탭을 클릭하여 구성 요소에 대한 개발자 설명서를 확인합니다.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 구성 요소 콘솔로 돌아갑니다. **We.Retail** 그룹을 필터링하고 **Text** 구성 요소를 선택합니다.
1. **리소스 유형**&#x200B;이 `/apps/weretail`에서 예상대로 구성 요소를 가리키지만 **리소스 슈퍼 유형**&#x200B;은 코어 구성 요소 `/apps/core/wcm/components/text/v1/text`를 다시 가리킵니다.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. **라이브 사용량** 탭을 클릭하여 이 구성 요소가 현재 사용 중인 페이지를 확인합니다. 첫 번째 **감사 인사** 페이지를 클릭하여 페이지를 편집합니다.

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. 감사 인사 페이지에서 텍스트 구성 요소를 선택하고 구성 요소의 편집 메뉴에서 상속 취소 아이콘을 클릭합니다.

   [We.Retail에는 ](/help/sites-developing/we-retail-globalized-site-structure.md) 상속이라는 메커니즘을 통해 컨텐츠를 언어 마스터에서  [Live Copy로 푸시하는 세계화된 사이트 구조가 있습니다](/help/sites-administering/msm.md). 이러한 이유로 사용자가 수동으로 텍스트를 편집할 수 있도록 하려면 상속을 취소해야 합니다.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. **예**&#x200B;를 클릭하여 취소를 확인합니다.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 상속이 취소되고 텍스트 구성 요소를 선택하면 더 많은 옵션을 사용할 수 있습니다. 편집** 클릭합니다**.

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. 이제 텍스트 구성 요소에 사용할 수 있는 편집 옵션을 확인할 수 있습니다.

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. **페이지 정보** 메뉴에서 **템플릿 편집**&#x200B;을 선택합니다.
1. 페이지의 템플릿 편집기에서 페이지의 **레이아웃 컨테이너**&#x200B;에 있는 텍스트 구성 요소의 **정책** 아이콘을 클릭합니다.

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. 핵심 구성 요소를 사용하면 템플릿 작성자가 페이지 작성자가 사용할 수 있는 속성을 구성할 수 있습니다. 여기에는 허용되는 붙여넣기 소스, 서식 옵션, 사용 가능한 단락 스타일 등과 같은 기능이 포함됩니다.

   이러한 디자인 대화 상자는 많은 핵심 구성 요소에 대해 사용할 수 있으며 템플릿 편집기와 함께 작동합니다. 활성화되면 구성 요소 편집기를 통해 작성자가 사용할 수 있습니다.

   ![chlimage_1-172](assets/chlimage_1-172.png)

## 추가 정보 {#further-information}

핵심 구성 요소에 대한 자세한 내용은 작성 문서 [핵심 구성 요소](https://docs.adobe.com/content/help/ko-KR/experience-manager-core-components/using/introduction.html) 와 핵심 구성 요소의 기능에 대한 개요를 참조하십시오. 기술 개요는 개발자 문서 [핵심 구성 요소 개발](https://helpx.adobe.com/experience-manager/core-components/using/developing.html)을 참조하십시오.

또한 [편집 가능한 템플릿](/help/sites-developing/we-retail-editable-templates.md)을 추가로 조사할 수도 있습니다. 편집 가능한 템플릿에 대한 전체 정보는 작성 문서 [페이지 템플릿 만들기](/help/sites-authoring/templates.md) 또는 개발자 문서 페이지 [템플릿 - 편집 가능](/help/sites-developing/page-templates-editable.md)을 참조하십시오.
