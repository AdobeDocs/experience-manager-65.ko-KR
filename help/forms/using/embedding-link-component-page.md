---
title: 페이지에 링크 구성 요소 포함
seo-title: 페이지에 링크 구성 요소 포함
description: 링크 구성 요소를 사용하여 모든 페이지에서 적응형 문서 또는 적응형 양식을 연결할 수 있습니다.
seo-description: 링크 구성 요소를 사용하여 모든 페이지에서 적응형 문서 또는 적응형 양식을 연결할 수 있습니다.
uuid: 22f488fc-bb1a-40aa-a5f4-6d04d7250f29
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9d63152d-41ca-4c7c-bb20-af16c7bdec13
docset: aem65
translation-type: tm+mt
source-git-commit: f9ed171c188a4dfb71f12ae9c98105a4c1895542
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 1%

---


# 페이지에 링크 구성 요소 포함{#embedding-link-component-in-a-page}

## 전제 조건 {#prerequisites}

링크 구성 요소는 문서 서비스 범주의 멤버입니다. 문서 서비스 범주가 AEM 구성 요소 브라우저에 표시되는지 확인합니다. 카테고리가 목록에 없으면 [양식 포털 구성 요소 활성화](/help/forms/using/enabling-forms-portal-components.md)에 나열된 단계를 따릅니다.

## 링크 구성 요소 {#link-component}

양식 포털 작성자는 링크 구성 요소를 사용하여 페이지의 아무 곳에서나 응용 양식에 대한 링크를 만들 수 있습니다. 링크 구성 요소는 구성 요소 브라우저의 문서 서비스 섹션에서 사용할 수 있습니다.

페이지에 링크 구성 요소를 추가하려면 다음 단계를 수행하십시오.

1. 페이지에서 **Link** 구성 요소를 드래그합니다. 구성 요소를 선택하고 ![cmppr](assets/cmppr.png)을 누릅니다. 링크 구성 요소 편집 대화 상자가 열립니다.

   ![edit-link-component](assets/edit-link-component.png)

1. **표시** 탭에서 다음을 지정합니다.

   * **링크 캡션**:링크에 대한 링크 텍스트 또는 캡션.
   * **링크 도구 설명**:링크에 대한 도구 설명.
   * **레이아웃 템플릿**:링크 구성 요소의 레이아웃용 템플릿입니다.

1. **자산 정보** 탭을 열고 자산의 유형을 지정합니다. 자산은 **form**&#x200B;일 수 있습니다. 선택한 자산의 유형에 따라 아래 나열된 옵션이 표시됩니다.

   * **자산 경로**:자산이 저장되는 저장소 경로.

   * **렌더링 유형**:렌더링 형식(PDF, HTML 또는 자동)입니다. 자동 렌더링 유형은 사용자 환경을 감지하고 그에 따라 양식을 HTML 또는 PDF로 렌더링합니다. 예를 들어 모바일 장치에서 양식에 액세스하는 경우 자동 렌더링 유형이 양식을 HTML로 렌더링합니다.
   * **양식 데이터가**  제출되는 서블릿에 URL 제출
   * **HTML 프로필**:양식을 HTML로 렌더링하기 위한 프로필.
   * **PDF 프로필**:양식을 PDF 문서로 렌더링하기 위한 프로필

1. **고급** 탭을 엽니다. 키-값 쌍 형식으로 추가 매개 변수를 지정할 수 있습니다. 링크를 클릭하면 이러한 추가 매개 변수가 추가되고 양식과 함께 전달됩니다.

   **Done**&#x200B;을 눌러 구성을 저장합니다.

## 링크 구성 요소 {#best-practices-for-using-link-component-br} 사용에 대한 우수 사례

* 양식 경로에 지정된 경로가 PDF가 허용되는 렌더링 포맷으로 되어 있는 문서를 가리키는 경우 PDF를 렌더링 유형으로 선택해야 합니다.
* 양식에 대한 제출 URL은 여러 위치에서 지정할 수 있으며 우선 순위는 다음과 같습니다.

   1. 전송 단추에서 양식에 포함된 URL의 우선 순위가 가장 높습니다.
   1. Forms 관리자에 언급된 제출 URL은 중간 우선 순위를 갖습니다.
   1. 양식 포털에서 언급한 제출 URL의 우선 순위가 가장 낮습니다.
