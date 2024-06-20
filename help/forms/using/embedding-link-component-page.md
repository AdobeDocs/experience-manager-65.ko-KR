---
title: 페이지에 링크 구성 요소 포함
description: 링크 구성 요소를 사용하여 모든 페이지에서 적응형 문서 또는 적응형 양식을 연결할 수 있습니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: eb45adf2-d0f3-4de6-92ac-fb146953e989
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 페이지에 링크 구성 요소 포함{#embedding-link-component-in-a-page}

## 사전 요구 사항 {#prerequisites}

링크 구성 요소는 문서 서비스 범주의 구성원입니다. 문서 서비스 카테고리가 AEM 구성 요소 브라우저에 표시되는지 확인합니다. 범주가 나열되지 않으면 다음 단계를 따릅니다. [Forms 포털 구성 요소 활성화](/help/forms/using/enabling-forms-portal-components.md).

## 링크 구성 요소 {#link-component}

링크 구성 요소를 사용하여 양식 포털 작성자는 페이지의 어디에서든 적응형 양식에 대한 링크를 만들 수 있습니다. 링크 구성 요소는 구성 요소 브라우저의 문서 서비스 섹션에서 사용할 수 있습니다.

페이지에 링크 구성 요소를 추가하려면 다음 단계를 수행하십시오.

1. 드래그 **링크** 구성 요소를 추가합니다. 구성 요소를 선택하고 을 선택합니다. ![cmppr](assets/cmppr.png). 링크 구성 요소 편집 대화 상자가 열립니다.

   ![edit-link-component](assets/edit-link-component.png)

1. 다음에서 **표시** 탭에서 다음을 지정합니다.

   * **링크 캡션**: 링크의 링크 텍스트 또는 캡션입니다.
   * **링크 툴팁**: 링크의 도구 설명
   * **레이아웃 템플릿**: 링크 구성 요소 레이아웃용 템플릿입니다.

1. 를 엽니다. **자산 정보** 을 탭하고 에셋의 유형을 지정합니다. 자산은 다음이 될 수 있습니다. **양식**. 선택한 에셋 유형에 따라 아래 나열된 옵션이 표시됩니다.

   * **자산 경로**: 에셋이 저장되는 저장소 경로입니다.

   * **렌더링 유형**: 렌더링 형식(PDF, HTML 또는 자동) 자동 렌더링 유형은 사용자 환경을 감지하므로 양식을 HTML 또는 PDF으로 렌더링합니다. 예를 들어, 모바일 장치에서 양식에 액세스하는 경우 자동 렌더링 유형은 HTML에서 양식을 렌더링합니다.
   * **제출 URL:**  양식 데이터가 제출되는 서블릿에 대한 URL.
   * **HTML 프로필**: 양식을 HTML으로 렌더링하기 위한 프로필입니다.
   * **PDF 프로필**: 양식을 PDF 문서로 렌더링하기 위한 프로필입니다.

1. 를 엽니다. **고급** 탭. 키-값 쌍 형식으로 추가 매개변수를 지정할 수 있습니다. 링크를 클릭하면 이러한 추가 매개 변수가 양식과 함께 전달됩니다.

   선택 **완료** 구성을 저장합니다.

## 링크 구성 요소 사용에 대한 우수 사례 {#best-practices-for-using-link-component-br}

* 양식 PDF에 지정된 경로가 허용된 렌더링 형식으로 PDF이 있는 문서를 가리키는 경우 경로를 렌더링 형식으로 선택해야 합니다.
* 양식의 제출 URL은 여러 위치에서 지정할 수 있으며, 우선 순위는 다음과 같습니다.

   1. 양식(제출 단추)에 포함된 제출 URL의 우선순위가 가장 높습니다.
   1. Forms Manager에 언급된 제출 URL은 우선 순위가 보통입니다.
   1. Forms 포털에 언급된 제출 URL의 우선 순위가 가장 낮습니다.
