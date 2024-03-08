---
title: Forms 포털 구성 요소에 대한 템플릿 맞춤화
description: AEM Forms 사용자 인터페이스를 통해 사용자가 양식에 메타데이터를 추가하는 방법에 대해 알아봅니다. 사용자 지정 메타데이터는 양식 목록 및 검색에서 사용자 경험을 향상시킵니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
feature: Forms Portal
exl-id: f889d996-77f7-4a4f-a637-da43fe1343c5
source-git-commit: db0e9d6105484b37e2e21e49bf0f95cef9da2a62
workflow-type: tm+mt
source-wordcount: '1242'
ht-degree: 0%

---

# Forms 포털 구성 요소에 대한 템플릿 맞춤화{#customizing-templates-for-forms-portal-components}

## 사전 요구 사항 {#prerequisites}

[양식 메타데이터 관리](../../forms/using/manage-form-metadata.md)

HTML 및 CSS 관련 실무 지식

## 개요 {#overview}

AEM Forms 사용자 인터페이스를 사용하면 모든 양식에 메타데이터를 추가할 수 있습니다. 사용자 지정 메타데이터는 조직의 양식을 나열하고 검색하는 동안 사용자 경험을 향상시킬 수 있습니다.

Forms 포털을 사용하면 양식 목록에서 사용자 지정 메타데이터를 사용할 수 있습니다. 에셋에 대한 사용자 지정 템플릿을 만드는 동안 해당 레이아웃을 수정하고 CSS 스타일 세트와 함께 사용자 지정 메타데이터를 사용할 수 있습니다.

다양한 Forms 포털 구성 요소에 대한 사용자 지정 템플릿을 만들 수 있도록 다음을 수행하십시오.

## 사용자 지정 템플릿 만들기 {#creating-a-nbsp-custom-template}

1. /apps 아래에 sling:Folder 노드 만들기

   &quot;fpContentType&quot; 속성을 추가합니다. 사용자 지정 템플릿을 정의하는 구성 요소에 따라 속성에 적절한 값을 지정합니다.

   * 검색 및 목록 구성 요소: &quot;/libs/fd/fp/formTemplate&quot;
   * 초안 및 제출 구성 요소:

      * 초안 섹션: /libs/fd/fp/draftTemplate
      * 제출 섹션: /libs/fd/fp/submissionsTemplate

   * 링크 구성 요소: /libs/fd/fp/linkTemplate

   레이아웃 템플릿을 선택하는 동안 표시할 제목을 추가합니다.

   >[!NOTE]
   >
   >제목은 만든 sling:Folder의 노드 이름과 다를 수 있습니다.

   다음 이미지는 Search &amp; List 구성 요소에 대한 구성을 보여 줍니다.
   ![sling:Folder 만들기](assets/1.png)

1. 사용자 지정 템플릿으로 사용할 수 있도록 이 폴더에 template.html 파일을 만듭니다.
1. 사용자 지정 템플릿을 작성하고 아래 설명된 대로 사용자 지정 메타데이터를 사용합니다.

## 작업 예 {#working-example}

다음은 Forms 포털이 검색 및 목록 구성 요소에 대한 사용자 지정 Geometrixx Gov 카드 레이아웃을 획득하는 사용자 지정 템플릿의 샘플 구현입니다.

```html
<div class="__FP_boxes-container __FP_single-color">
    <div class="boxes __FP_boxes __FP_single-color" data-repeatable="true">
 <div class="__FP_boxes-thumbnail">
     <img src ="${path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png"/>
        </div>
        <h3 class="__FP_single-color" title="${name}" tabindex="0">${name}</h3>
        <p>${description}</p>
        <div class="boxes-icon-cont __FP_boxes-icon-cont">
            <div class="op-dow">
                <a href="${formUrl}" target="_blank" class="__FP_button ${htmlStyle}" title="${config-htmlLinkText}">${localize-Apply}</a>
                <a href="${pdfUrl}" class="__FP_button ${pdfStyle}" title="${config-pdfLinkText}">${localize-Download}</a>
            </div>
        </div>
    </div>
</div>
```

## 사용자 정의 템플릿에 대한 기술 사양 {#technical-specifications-for-custom-templates}

Forms 포털 구성 요소에 대한 사용자 지정 템플릿에는 반복 가능한 항목과 반복 불가능한 항목이 포함되어 있습니다. 반복 가능한 항목은 나열할 기본 엔티티입니다. 반복 가능한 항목의 예로는 검색 및 목록 작성자, 초안 및 제출, 링크 구성 요소 등이 있습니다.

Forms 포털은 자리 표시자가 사용자 지정/기본 제공 메타데이터를 표시할 수 있는 구문을 제공합니다. 양식, 초안 또는 제출 결과를 표시한 후 자리 표시자가 채워집니다.

반복 가능한 항목을 포함하려면 속성 값을 구성합니다 **데이터 반복 가능** 끝 **true**.

*설명된 예제에서 사용자 지정 템플릿의 맨 위에 두 개의 Div 요소가 있습니다. 첫 번째는 &quot;__FP_boxes-container&quot; CSS 클래스와 함께 나열되는 양식의 컨테이너 요소로 작동합니다. 두 번째는 &quot;__FP_boxes&quot; CSS 클래스와 함께 기본 엔터티용 템플릿이며, 이 경우 폼입니다. 다음&#x200B;**데이터 반복 가능**div 요소에 있는 속성에는 값이 있습니다.**true**.*

각 자리 표시자에는 배타적인 기본 메타데이터 세트가 있습니다. 양식의 특정 위치에 사용자 지정 메타데이터를 표시하려면 **${metadata_prop} 속성** 그 장소 말이야.

*이 예제에서 메타데이터 속성은 여러 인스턴스에서 사용됩니다. 예를 들어에서 사용됩니다&#x200B;**설명**,**이름**,**formUrl**,**htmlStyle**,**pdfUrl**,**pdfStyle**, 및&#x200B;**경로**규정된 방식으로.*

## 기본 제공 메타데이터 {#out-of-the-box-metadata}

다양한 Forms 포털 구성 요소는 목록에 사용할 수 있는 독점적인 메타데이터 세트를 제공합니다.

### Search &amp; Lister 구성 요소 {#search-amp-lister-component}

* **제목:** 양식 제목
* **이름**: 양식 이름(대부분 제목과 동일함)
* **설명**: 양식에 대한 설명
* **formUrl**: 양식을 HTML으로 렌더링할 URL
* **pdfUrl**: 양식을 PDF으로 렌더링할 URL
* **assetType**: 에셋 유형입니다. 유효한 값은 다음과 같습니다 **양식**, **PDF 양식**, **인쇄 양식**, 및 **적응형 양식**

* **htmlStyle**&#x200B;및 **pdfStyle**: 렌더링에 각각 사용되는 HTML 및 PDF 아이콘의 표시 스타일입니다. 유효한 값은 &quot;**__FP_display_none**&quot;또는 비어 있음.

>[!NOTE]
>
>사용자 지정 스타일 시트에서 __FP_display_none 클래스를 사용해야 합니다.

* **downloadUrl**: 에셋을 다운로드할 URL입니다.

사용자 인터페이스에서 로컬라이제이션, 정렬 및 구성 속성 사용 지원(Search &amp; List만 해당):

1. **현지화 지원**: 정적 텍스트를 현지화하려면 속성을 사용합니다 `${localize-YOUR_TEXT}` 가 없는 경우 현지화된 값을 사용할 수 있도록 합니다.
   *설명한 예에서 속성은 `${localize-Apply}` 및 `${localize-Download}` 적용 및 다운로드 텍스트를 현지화하는 데 사용됩니다.*

1. **정렬 지원**: 검색 결과를 정렬하려면 HTML 요소를 클릭합니다. 테이블 레이아웃에서 정렬을 구현하려면 특정 테이블 헤더에 &quot;data-sortKey&quot; 속성을 추가하십시오. 또한 해당 값을 정렬할 메타데이터로 추가합니다.
예를 들어 그리드 보기의 &quot;Title&quot; 헤더의 경우 &quot;data-sortKey&quot; 헤더의 값은 &quot;title&quot;입니다. 특정 열의 값을 정렬할 수 있도록 제목을 클릭합니다.

1. **구성 속성 사용**: 검색 및 목록 구성 요소에는 사용자 인터페이스에서 사용할 수 있는 몇 가지 구성이 있습니다. 예를 들어 편집 대화 상자를 통해 저장된 HTML 도구 설명 텍스트를 표시하려면 `${config-htmlLinkText}` 특성. **마찬가지로 PDF 도구 설명 텍스트의 경우** `${config-pdfLinkText}` 특성.

### 링크 구성 요소 {#link-component}

* **제목:** 양식 제목
* **formUrl**: 양식을 HTML으로 렌더링할 URL
* **target**: 링크의 타겟 속성입니다. 유효한 값은 &quot;_blank&quot; 및 &quot;_self&quot;입니다.
* **linkText**: 링크 캡션

### 초안 및 제출 구성 요소 {#drafts-amp-submissions-component}

* **경로**: 초안/제출 메타데이터 노드 경로 초안 또는 제출을 열 수 있도록 확장자가 .HTML인 URL과 함께 사용합니다.
* **contextPath**: AEM 인스턴스의 컨텍스트 경로
* **first레터**: 적응형 양식 제목이 초안으로 저장되거나 제출되어 첫 번째 문자(대문자)로 표시됩니다.
* **formName**: 초안으로 저장되거나 제출된 적응형 양식의 제목
* **draftID**: 나열된 초안의 ID(초안 섹션의 템플릿에서만 사용).
* **submitID**: 나열된 제출 서류 ID(제출 서류 섹션의 템플릿에서만 사용).
* **상태**: 제출된 양식의 상태. (제출 서류 섹션의 템플릿에서만 사용하십시오.)
* **설명**: 초안 또는 제출과 관련된 적응형 양식에 대한 설명
* **diffTime**: 초안에 대한 현재 시간과 마지막 저장 작업의 차이입니다. 또는 현재 시간과 제출에 대해 마지막으로 제출된 작업 간의 차이입니다.
* **iconClass**: 초안/제출의 첫 번째 문자를 표시하는 데 사용되는 CSS 클래스입니다. Forms 포털에는 다양한 색상 배경을 제공하는 다음 클래스가 포함되어 있습니다.
* **소유자**: 초안/제출을 작성한 사용자.
* **오늘**: 초안 작성일 또는 제출일 `DD:MM:YYYY` 포맷.
* **TimeNow**: 초안 작성 또는 제출 시간 `HH:MM:SS` 24시간 형식

*참고:*

1. 초안 및 제출 구성 요소 아래의 초안 섹션에 있는 삭제 옵션에 대해 CSS 클래스 이름을 &quot;__FP_deleteDraft&quot;로 지정합니다. 또한 값과 함께 &quot;draftID&quot; 속성을 포함합니다. **${draftID}**: 해당 초안의 초안 id입니다.

1. 열린 초안 및 제출에 대한 링크를 만드는 동안 다음을 지정할 수 있습니다 **${path}.html** 을 값으로 사용 **href** 앵커 태그에 대한 특성입니다.

![초안 및 제출 노드](assets/raw-image-with-index.png)

**A**. 컨테이너 요소

**B.** 각 양식에 대해 저장된 썸네일을 가져올 수 있는 고정 계층 구조가 있는 &quot;경로&quot; 메타데이터

**C.** 각 양식의 템플릿 섹션에 사용되는 데이터 반복 가능 속성

**D.** &quot;적용&quot; 문자열 현지화

**E.** 구성 속성 pdfLinkText 사용

**F** &quot;pdfUrl&quot; 메타데이터 사용

## 팁, 요령 및 알려진 문제 {#tips-tricks-and-known-issues}

1. 사용자 지정 템플릿에서 작은따옴표(&#39;)를 사용하지 마십시오.
1. 사용자 지정 메타데이터의 경우 이 속성을에 저장합니다. **jcr:content/metadata** 노드만 다른 위치에 저장하면 Forms 포털에서 메타데이터를 표시할 수 없습니다.
1. 사용자 지정 메타데이터 또는 기존 메타데이터의 이름에 콜론(:)이 포함되어 있지 않은지 확인하십시오. 이 경우 사용자 인터페이스에 표시할 수 없습니다.
1. **데이터 반복 가능** 에 대한 의미가 없습니다. **링크** 구성 요소. Adobe 구성 요소용 템플릿에서는 이 속성을 사용하지 않는 것이 좋습니다.

## 관련 문서

* [Forms 포털 구성 요소 활성화](/help/forms/using/enabling-forms-portal-components.md)
* [Forms 포털 만들기 페이지](/help/forms/using/creating-form-portal-page.md)
* [API를 사용하여 웹 페이지의 목록 양식](/help/forms/using/listing-forms-webpage-using-apis.md)
* [초안 및 제출 구성 요소 사용](/help/forms/using/draft-submission-component.md)
* [초안 및 제출된 양식의 스토리지 사용자 지정](/help/forms/using/draft-submission-component.md)
* [초안 및 제출 구성 요소를 데이터베이스와 통합하기 위한 샘플](/help/forms/using/integrate-draft-submission-database.md)
* [Forms 포털 구성 요소에 대한 템플릿 맞춤화](/help/forms/using/customizing-templates-forms-portal-components.md)
* [포털에 양식 게시 소개](/help/forms/using/introduction-publishing-forms.md)
