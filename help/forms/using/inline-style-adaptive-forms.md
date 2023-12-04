---
title: 적응형 양식 구성 요소의 인라인 스타일 지정
seo-title: Inline CSS properties for adaptive form components
description: 적응형 양식에 사용자 지정 스타일을 적용할 수 있지만 적응형 양식의 개별 구성 요소에 인라인 CSS 속성을 적용할 수도 있습니다.
seo-description: While you can apply custom styles on an adaptive form, you can also apply inline CSS properties on individual components of an adaptive form.
uuid: e863780e-2250-4bea-9569-22be5638d54e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 21dec713-c76d-408b-baea-fc585377b429
docset: aem65
feature: Adaptive Forms
exl-id: 67cfecb8-c31d-4192-904d-7bfaa1a31ea5
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 13%

---

# 적응형 양식 구성 요소의 인라인 스타일 지정 {#inline-styling-of-adaptive-form-components}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/inline-style-adaptive-forms.html) |
| AEM 6.5 | 이 문서 |

다음을 사용하여 스타일을 지정하여 적응형 양식의 전체 모양과 스타일을 정의할 수 있습니다. [테마 편집기](../../forms/using/themes.md). 또한 개별 적응형 양식 구성 요소에 인라인 CSS 스타일을 적용하고 변경 사항을 즉시 미리 볼 수 있습니다. 인라인 스타일은 테마에 제공된 스타일을 재정의합니다.

## 인라인 CSS 속성 적용 {#apply-inline-css-properties}

구성 요소에 인라인 스타일을 추가하려면 다음 작업을 수행하십시오.

1. 양식 편집기에서 양식을 열고 모드를 스타일 모드로 변경합니다. 모드를 스타일 모드로 변경하려면 페이지 도구 모음에서 를 선택합니다 ![캔버스 드롭다운](assets/canvas-drop-down.png) > **스타일**.
1. 페이지에서 구성 요소를 선택하고 편집 버튼을 선택합니다 ![편집 단추](assets/edit-button.png). 스타일 속성이 사이드바에서 열립니다.

   사이드바의 양식 계층 구조 트리에서 구성 요소를 선택할 수도 있습니다. 양식 계층 구조 트리는 사이드바에서 양식 객체로 사용할 수 있습니다.

   사이드바에서 구성 요소를 선택할 수도 있습니다. 스타일 모드에서는 양식 개체 아래에 나열된 구성 요소를 볼 수 있습니다. 그러나 사이드바의 양식 개체 목록에는 필드 및 패널과 같은 구성 요소가 나열됩니다. 필드 및 패널은 텍스트 상자 및 라디오 버튼과 같은 구성 요소를 포함할 수 있는 일반 구성 요소입니다.

   사이드바에서 구성 요소를 선택하면 나열된 모든 하위 구성 요소와 선택한 구성 요소의 속성이 표시됩니다. 특정 하위 구성 요소를 선택하고 스타일을 지정할 수 있습니다.

1. 사이드바에서 탭을 클릭하여 CSS 속성을 지정합니다. 다음과 같은 속성을 지정할 수 있습니다.

   * Dimension 및 위치(표시 설정, 패딩, 높이, 너비, 여백, 위치, z-색인, 부동, 지우기, 오버플로)
   * 텍스트(글꼴 모음, 두께, 색상, 크기, 선 높이 및 맞춤)
   * 배경(이미지 및 그라데이션, 배경색)
   * 테두리(폭, 스타일, 색상, 반경)
   * 효과(그림자, 강도)
   * 고급(구성 요소에 대한 사용자 지정 CSS를 쓸 수 있음)

1. 마찬가지로 구성 요소의 다른 부분(예: 위젯, 캡션 및 도움말)에 스타일을 적용할 수 있습니다.
1. 선택 **완료** 변경 사항을 확인하거나 **취소** 변경 내용을 취소합니다.

## 예: 필드 구성 요소의 인라인 스타일 {#example-inline-styles-for-a-field-component}

다음 이미지는 인라인 스타일이 적용되기 전후의 텍스트 필드를 나타냅니다.

![인라인 스타일이 적용되기 전의 텍스트 상자 구성 요소](assets/no-style.png)

인라인 스타일 속성을 적용하기 전의 텍스트 상자 구성 요소

다음 CSS 속성을 적용한 후 다음 이미지에 표시된 대로 텍스트 상자 스타일이 변경되었는지 확인합니다.

<table>
 <tbody>
  <tr>
   <td><p>선택기</p> </td>
   <td><p>CSS 속성</p> </td>
   <td><p>값</p> </td>
   <td><p>효과</p> </td>
  </tr>
  <tr>
   <td><p>필드</p> </td>
   <td><p>테두리</p> </td>
   <td><p>테두리 너비 =2px</p> <p>테두리 스타일=단색</p> <p>테두리 색상=#1111</p> </td>
   <td><p>필드 주위에 2px 너비의 검정 테두리를 만듭니다.</p> </td>
  </tr>
  <tr>
   <td><p>텍스트 상자</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>배경색을 CornflowerBlue(#6495ED)로 변경합니다.</p> <p>참고: 값 필드에 색상 이름 또는 16진수 코드를 지정할 수 있습니다.</p> </td>
  </tr>
  <tr>
   <td><p>레이블</p> </td>
   <td><p>치수 및 위치 &gt; 너비</p> </td>
   <td><p>100픽셀</p> </td>
   <td><p>레이블의 너비를 100px로 수정합니다.</p> </td>
  </tr>
  <tr>
   <td>필드 도움말 아이콘</td>
   <td>텍스트 &gt; 글꼴 색상</td>
   <td>#2ECC40</td>
   <td>도움말 아이콘 면의 색상을 변경합니다.</td>
  </tr>
  <tr>
   <td><p>긴 설명</p> </td>
   <td><p>text-align</p> </td>
   <td><p>가운데</p> </td>
   <td><p>도움말의 긴 설명을 가운데에 맞춥니다.</p> </td>
  </tr>
 </tbody>
</table>

![인라인 스타일이 적용된 후 텍스트 상자 스타일](assets/applied-style.png)

인라인 스타일 속성을 적용한 후 텍스트 상자 구성 요소

위의 단계에 따라 패널, 제출 단추 및 라디오 단추와 같은 다른 구성 요소를 선택하고 스타일을 지정할 수 있습니다.

>[!NOTE]
>
>스타일 속성은 선택하는 구성 요소에 따라 다릅니다.
