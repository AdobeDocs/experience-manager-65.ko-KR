---
title: 적응형 양식 단편 이란 무엇입니까?
description: 적응형 Forms은 적응형 양식에서 사용할 패널 또는 필드 그룹과 같은 양식 세그먼트를 만드는 메커니즘을 제공합니다. 기존 패널을 조각으로 저장할 수도 있습니다.
topic-tags: author
keywords: 적응형 양식 조각, 적응형 양식 조각 만들기, 양식 단편을 추가 하 고, 적응형 양식에 단편을 추가 하 고, 조각을 관리 합니다.
feature: Adaptive Forms, Core Components
source-git-commit: 304b1bf2e19942fb728944330512a83a9006cb2a
workflow-type: tm+mt
source-wordcount: '1844'
ht-degree: 5%

---

# 주요 구성 요소를 기반으로 적응형 양식에서 적응형 Forms 조각을 만들기 하 고 사용 합니다. {#adaptive-form-fragments}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM 6.5 | 이 문서 |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/adaptive-form-fragments-core-components.html) |

모든 양식은 특정 목적을 위해 디자인되었지만 대부분의 양식에는 이름 및 주소, 가족 세부 사항, 소득 세부 사항 등의 개인 세부 사항을 제공하는 것과 같은 몇 가지 일반적인 세그먼트가 있습니다. 양식 개발자는 새 양식을 만들 때마다 이러한 공통 세그먼트를 만들어야 합니다.

적응형 Forms은 패널 또는 필드 그룹과 같은 양식 세그먼트를 한 번만 만들어 적응형 Forms 간에 재사용할 수 있는 편리한 메커니즘을 제공합니다. 이러한 재사용 가능한 독립 세그먼트를 적응형 양식 조각이라고 합니다.

양식 조각은 여러 양식에 원활하게 통합되어 일관되고 전문적인 양식을 간편하게 만들 수 있습니다. 양식 조각의 “한번 변경하여 전체 반영” 기능을 통해 재사용성, 표준화와 브랜드 일관성을 보장합니다. 한 위치에서의 업데이트가 이러한 조각을 활용하는 모든 양식에 자동으로 전파되므로 유지 관리 가능성과 효율성이 개선됩니다.

문서에 조각을 여러 번 추가하고 해당 구성 요소의 데이터 바인딩 속성을 사용하여 다른 데이터 소스 또는 스키마에 연결할 수 있습니다. 예를 들어 영구, 통신 및 청구 주소에 동일한 주소 조각을 사용하고 이를 데이터 소스 또는 스키마의 다른 필드에 연결할 수 있습니다.

>[!NOTE]
>
> 를 사용하여 사용자의 조각 경험을 손쉽게 맞춤화할 수 있습니다. [양식 조각 구성 요소의 구성 대화 상자 및 디자인 대화 상자](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-fragment.html).


## 양식 단편 만들기 {#create-a-fragment}

적응형 양식 조각을 처음부터 만들거나 기존 적응형 양식에 패널을 조각으로 저장할 수 있습니다. 양식 조각을 만들려면 다음 작업을 수행하십시오.

1. https://에서 AEM Forms 인스턴스에 로그인합니다&#x200B;[*호스트 이름*]:[*포트*]/aem/forms.html입니다.
1. 클릭 **만들기 > 적응형 양식 단편**.
1. 조각의 제목, 이름, 설명 및 태그를 지정합니다. 조각에 고유한 이름을 지정해야 합니다. 동일한 이름의 다른 조각이 존재하는 경우 조각을 생성하지 못합니다.
1. 양식 템플릿을 선택합니다. 적응형 Forms 또는 기초 구성 요소 기반 적응형 Forms 또는 적응형 에 대한 양식 조각을 만들 수 있습니다.
   * 핵심 구성 요소 기반 양식에 대한 양식 조각을 만들려면 핵심 구성 요소 기반 템플릿을 선택합니다.
   * 기초 구성 요소 기반 양식에 대한 양식 조각을 생성하려면 기초 구성 요소 템플릿을 선택합니다. 예: /libs/fd/af/templateForFragment/defaultFragmentTemplate.

   핵심 구성 요소 기반 양식의 양식 조각을 만들 때 양식 테마 선택 옵션을 사용하여 핵심 구성 요소 기반 테마를 선택합니다.

1. 클릭하여 열기 **양식 모델** 탭 및 **다음에서 선택** 드롭다운 메뉴에서 조각에 대해 다음 모델 중 하나를 선택합니다.

   ![양식 모델 탭에 모델 유형 표시](assets/create-af-1-1.png)

   * **없음**: 양식 모델을 사용하지 않고 조각을 처음부터 만들도록 지정합니다.

     >[!NOTE]
     >
     > 적응형 Forms에서 단일 양식 조각(핵심 구성 요소 기반)을 여러 번 사용할 수 있습니다. none 기반 양식 조각과 schema 기반 양식 조각을 모두 지원합니다.

   * **스키마** : AEM Forms에 업로드 된 XML 또는 JSON 스키마를 사용 하 여 단편을 만들도록 지정 합니다. 사용 가능한 XML 또는 JSON 스키마 중에서 조각을 위한 양식 모델로 업로드하거나 선택할 수 있습니다. XML 스키마를 선택하면 다음 위치에서 선택한 스키마에 있는 complexType을 선택하여 적응형 양식 조각을 만들 수도 있습니다. **[!UICONTROL XML 스키마 복합 유형]** 드롭다운 상자. JSON 스키마를 선택할 때 다음 항목에서 선택한 스키마에 있는 스키마 정의를 선택하여 적응형 양식 조각을 만들 수도 있습니다. **[!UICONTROL JSON 스키마 정의]** 드롭다운 상자.
   * **양식 데이터 모델**: 양식 데이터 모델을 사용하여 조각을 만들도록 지정합니다. 양식 데이터 모델에서 하나의 데이터 모델 개체만 기반으로 적응형 양식 조각을 만들 수 있습니다. 양식 데이터 모델 정의 드롭다운 확장 지정된 양식 데이터 모델의 모든 데이터 모델 개체를 나열합니다. 목록에서 데이터 모델 개체를 선택합니다.

   ![양식 데이터 모델](assets/create-af-3.png)



1. [만들기 **]을 클릭** 하 고 [열기 **]를 클릭** 하 여 편집 모드에서 기본 템플릿를 사용 하 여 조각을 엽니다. 편집 모드에서는 모든 적응형 양식 구성 요소를 조각에 추가할 수 있습니다.

<!-- For information about Adaptive Form components, see [Introduction to authoring Adaptive Forms](../../forms/using/introduction-forms-authoring.md). --> 또한 XML 스키마 나 XDP 양식을 조각의 양식 모델로 템플릿 선택한 경우 양식 모델 계층 표시 하는 새 탭 컨텐츠 finder에 표시 됩니다. 양식 모델 요소를 조각으로 드래그 앤 드롭할 수 있습니다. 추가된 양식 모델 요소는 연결된 XDP 또는 XSD의 원래 속성을 유지하면서 양식 구성 요소로 변환됩니다.

스키마 또는 양식 데이터 모델을 기반으로 하는 적응형 양식 조각이 생성되면 적응형 양식 편집기에 있는 콘텐츠 브라우저의 데이터 소스 탭에 양식 데이터 모델 또는 스키마 요소가 나타납니다. 양식 모델 요소를 조각에 드래그 앤 드롭할 수 있습니다. 추가된 양식 모델 요소는 연결된 스키마의 원래 속성을 유지하면서 양식 구성 요소로 변환됩니다.


## 적응형 양식에 조각 추가 {#insert-a-fragment-in-an-adaptive-form}

적응형 양식에 적응형 양식 조각을 추가하려면 다음 작업을 수행하십시오.

1. 편집 모드에서 적응형 양식을 엽니다.
1. 추가 **적응형 양식 단편** 구성 요소를 양식에 추가합니다.
1. 다음을 클릭합니다. **에셋** 콘텐츠 브라우저 - 사이드바. 에셋 브라우저의 경로에서 **적응형 양식 단편** 옵션을 선택합니다. 양식의 모델에 따라 양식에 사용할 수 있는 모든 적응형 Forms 조각이 표시됩니다.

   ![적응형 양식 단편 옵션 선택](assets/adaptive-forms-fragments.png)

1. 적응형 양식 단편을 다음 위치에 드래그 앤 드롭 **적응형 양식 단편** 적응형 양식의 구성 요소.

   >[!NOTE]
   >
   >적응형 양식 내에서 작성하려면 적응형 양식 조각을 사용할 수 없습니다. 또한 JSON 기반 적응형 양식에서 XSD 기반 조각을 사용할 수 없으며 그 반대의 방법도 사용할 수 없습니다.

적응형 양식 조각은 적응형 양식을 참조하여 추가되고 독립형 적응형 양식 조각과 동기화된 상태로 유지됩니다. 이는 적응형 양식 조각에 대한 모든 수정 사항이 조각이 적응형 Forms 내에 통합된 모든 인스턴스에 미러링됨을 의미합니다.

### 적응형 양식에 조각 포함 {#embed-a-fragment-in-adaptive-form}

추가 된 조각의 [포함 ](assets/Smock_Import_18_N.svg) ] 아이콘을 클릭 ![ 하 여 적응형 양식에 적응형 양식 단편을 포함 하도록 선택할 수 있습니다.

포함 된 조각은 더 이상 독립 실행형 조각과 연결 되지 않습니다. 적응형 양식 내에서 포함 된 조각의 구성 요소를 편집할 수 있습니다.

<!-- 
## Configure fragment appearance {#configure-fragment-appearance}

Any fragment you insert in Adaptive Forms appears as a placeholder image. The placeholder displays titles of up to a maximum of ten child panels in the fragment. You can configure AEM Forms to show the complete fragment instead of the placeholder image.

Perform the following steps to show complete fragments in forms:

1. Go to AEM web console configuration page at https:[*host*]:[*port*]/system/console/configMgr.

1. Search and click **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]** to open it in edit mode.
1. Disable **[!UICONTROL Enable Placeholder in place of Fragment]** checkbox to show complete fragments rather than the placeholder image.

-->

### 조각 내에서 조각 사용 {#using-fragments-within-fragments}

중첩된 적응형 양식 조각을 만들 수 있습니다. 즉, 다른 조각에서 조각을 드래그 앤 드롭할 수 있고 중첩된 조각 구조를 가질 수 있습니다.

### 적응형 양식에서 양식 단편을 여러 번 사용 {#using-form-fragment-mutiple-times-in-af}

적응형 양식에서 none 기반 및 스키마 기반 양식 조각을 여러 번 사용 하 여 각 양식 조각 필드에 대 한 데이터를 고유 하 게 저장할 수 있습니다. 예를 들어 주소 양식 단편을 사용 하 여 대출 애플리케이션 양식에서 영구적인 정보를 수집 하 고 살아있는 주소를 표시할 수 있습니다.

![적응형 양식에서 여러 조각 사용](assets/using-multiple-fragment-af.gif)

## 데이터 바인딩에 대 한 조각의 자동 매핑 {#auto-mapping-of-fragments-for-data-binding}

XFA 양식 템플릿 또는 XSD complex type을 사용 하 여 적응형 양식 단편을 만들고 조각을 적응형 양식으로 드래그 하면, XFA 조각 또는 XSD 복합 유형은 조각 모델 루트가 XFA 조각 또는 XSD 복합 유형에 매핑되는 해당 적응형 양식 조각으로 자동 대체 됩니다.

구성 요소 편집 대화 상자에서 조각 에셋과 해당 바인딩을 변경할 수 있습니다.

AEM 콘텐츠 파인더의 적응형 양식 단편 라이브러리에서 바인딩된 적응형 양식 단편을 드래그 앤 드롭하고 적응형 양식 단편 패널의 구성 요소 편집 대화 상자에서 올바른 바인딩 참조를 제공할 수도 있습니다.

## 조각 관리 {#manage-fragments}

AEM Forms UI를 사용하여 적응형 양식 조각에 대해 여러 작업을 수행할 수 있습니다.

1. `https://[hostname]/aem/forms.html`로 이동합니다.

1. 클릭 **선택** AEM Forms UI 도구 모음에서 적응형 양식 조각을 선택합니다. 도구 모음에는 선택한 적응형 양식 조각에서 수행할 수 있는 다음 작업이 표시됩니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>작업</strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p>편집</p> </td>
   <td><p>선택한 적응형 양식 단편을 편집 모드로 엽니다.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>속성</p> </td>
   <td><p>속성 패널을 엽니다. [속성] 패널에서 속성을 확인 및 편집하고, 미리 보기를 생성하고, 선택한 조각에 대한 썸네일 이미지를 업로드할 수 있습니다. 자세한 내용은 <a>메타데이터 관리</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>복사</p> </td>
   <td><p>선택한 조각을 복사합니다. 도구 모음에 붙여넣기 단추가 나타납니다.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>다운로드</p> </td>
   <td><p>선택한 조각을 다운로드합니다.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>미리보기</p> </td>
   <td><p>XML 파일의 데이터를 조각과 병합하여 조각을 HTML 또는 사용자 지정 미리 보기로 미리 보는 옵션을 제공합니다. 자세한 내용은 <a>양식 미리 보기</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>검토 시작/검토 관리</p> </td>
   <td><p>선택한 조각의 검토를 시작하고 관리할 수 있습니다. 자세한 내용은 <a>리뷰 생성 및 관리</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>사전 추가</p> </td>
   <td><p>선택한 조각을 현지화하기 위한 사전을 생성합니다. 자세한 내용은 <a>적응형 Forms 현지화</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>게시 / 게시 취소</p> </td>
   <td><p>선택한 단편을 게시/해제 합니다. <br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>삭제</p> </td>
   <td><p>선택한 조각을 삭제합니다.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## 조각을 사용하여 작업할 때 기억해야 할 주요 사항 {#key-points-to-remember-when-working-with-fragments}

* 조각 이름이 고유한지 확인합니다. 같은 이름의 기존 조각이 있는 경우 조각을 만들 수 없습니다.
* XDP 기반 적응형 양식에서 다른 XDP 조각을 포함하는 조각으로 패널을 저장하면 결과 조각이 하위 XDP 조각에 자동으로 바인딩됩니다. XSD 기반 적응형 양식의 경우 결과 조각은 스키마 루트에 바인딩됩니다.
* 적응형 양식 조각을 만들면 CRXDE Lite에서 적응형 양식에 대한 guideContainer 노드와 유사한 조각 노드가 만들어집니다.
* 다른 양식 데이터 모델을 사용하는 적응형 양식의 조각은 지원되지 않습니다. 예를 들어 XDP 기반 조각은 XSD 기반 적응형 양식에서 지원되지 않으며, 이와 반대입니다.
* 적응형 양식 조각은 AEM 콘텐츠 파인더의 적응형 양식 조각 탭을 통해 사용할 수 있습니다.
* 독립형 적응형 양식 조각의 모든 표현식, 스크립트 또는 스타일은 참조로 삽입되거나 적응형 양식에 임베드될 때 유지됩니다.
* 참조에 의해 삽입된 적응형 양식 단편을 적응형 양식 내에서 편집할 수 없습니다. 편집하려면 독립 실행형 적응형 양식 조각을 편집하거나 적응형 양식에 해당 조각을 임베드하십시오.
* 적응형 양식을 게시할 때 적응형 양식에 참조로 삽입된 독립 실행형 적응형 양식 조각을 게시해야 합니다.
* 업데이트된 적응형 양식 조각을 다시 게시하면 변경 사항이 조각이 사용되는 적응형 양식의 게시된 인스턴스에 반영됩니다.
* 확인 구성 요소가 포함된 적응형 양식은 익명 사용자를 지원하지 않습니다. 또한 적응형 양식 조각에서 확인 구성 요소를 사용하는 것은 권장되지 않습니다.
* ( **Mac만** 해당) 양식 조각 기능이 모든 시나리오에서 완벽 하 게 작동 하도록 하려면/private/etc/hosts 파일에 다음 항목을 추가 합니다.
  `127.0.0.1 <Host machine>` **호스트 컴퓨터**: AEM Forms이 배포되는 Apple Mac 시스템입니다.

## 참조 조각 {#reference-fragments}

양식을 만드는 데 사용할 수 있는 적응형 양식 조각을 참조하십시오.
<!-- For more information, see [Reference Fragments](../../forms/using/reference-adaptive-form-fragments.md). -->

## 추가 참조 {#see-also}

* [핵심 구성 요소 기반 적응형 양식 만들기](create-an-adaptive-form-core-components.md)
* [규칙 편집기를 사용 하 여 동적 동작을 양식에 추가 합니다.](rule-editor.md)
* [주요 구성 요소 기반 적응형에 대 한 테마를 만들기 하거나 사용자 지정 Forms](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [핵심 구성 요소 기반 적응형에 대 한 템플릿를 만들기 Forms](template-editor.md)
* [AEM Sites 페이지 또는 경험 조각에 적응형 양식 만들기 또는 추가](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [샘플 테마 템플릿 및 양식 데이터 모델](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)