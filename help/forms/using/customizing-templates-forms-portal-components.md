---
title: 양식 포털 구성 요소에 대한 템플릿 사용자 정의
seo-title: 양식 포털 구성 요소에 대한 템플릿 사용자 정의
description: 양식 목록에 사용자 지정 메타데이터 표시
seo-description: 양식 목록에 사용자 지정 메타데이터 표시
uuid: 212109ca-85c8-4915-82e5-a18a0443be1b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 7566203f-2f80-4ce7-bff9-073d67119f64
docset: aem65
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 0%

---


# 양식 포털 구성 요소에 대한 템플릿 사용자 정의{#customizing-templates-for-forms-portal-components}

## 전제 조건 {#prerequisites}

[양식 메타데이터 관리](../../forms/using/manage-form-metadata.md)

HTML 및 CSS에 대한 작업 지식

## 개요 {#overview}

AEM Forms 사용자 인터페이스를 사용하면 모든 양식에 메타데이터를 추가할 수 있습니다. 사용자 지정 메타데이터를 사용하면 조직의 양식을 나열하고 검색하는 동안 사용자 경험을 향상시킬 수 있습니다.

Forms 포털을 통해 양식 목록에 사용자 정의 메타데이터를 사용할 수 있습니다. 자산에 대한 사용자 정의 템플릿을 만드는 동안 레이아웃을 수정하고 CSS 스타일 세트와 함께 사용자 정의 메타데이터를 사용할 수 있습니다.

다양한 Forms 포털 구성 요소에 대한 사용자 정의 템플릿을 만들려면 다음 단계를 수행하십시오.

## Creating a custom template {#creating-a-nbsp-custom-template}

1. /apps 아래에 sling:Folder 노드 만들기

   &quot;fpContentType&quot; 속성을 추가합니다. 사용자 지정 템플릿을 정의하는 구성 요소에 따라 속성에 적절한 값을 지정합니다.

   * 검색 및 라이브러리 구성 요소: &quot;/libs/fd/fp/formTemplate&quot;
   * 초안 및 제출 구성 요소:

      * 초안 섹션: /libs/fd/fp/drafsTemplate
      * 제출 섹션: /libs/fd/fp/submissions템플릿
   * 링크 구성 요소: /libs/fd/fp/linkTemplate

   레이아웃 템플릿을 선택할 때 표시할 제목을 추가합니다.

   >[!NOTE]
   >
   >제목은 사용자가 만든 sling:Folder의 노드 이름과 다를 수 있습니다.

   다음 이미지는 검색 및 라이브러리 구성 요소의 구성을 보여 줍니다.
   ![sling:Folder 만들기](assets/1.png)

1. 이 폴더에 사용자 지정 템플릿으로 사용할 template.html 파일을 만듭니다.
1. 사용자 지정 템플릿을 작성하고 아래에 설명된 대로 사용자 지정 메타데이터를 사용합니다.

## 작업 예 {#working-example}

다음은 Forms 포털에서 검색 및 라이브러리 구성 요소에 대한 사용자 정의 Geometrixx Gov 카드 레이아웃을 취득하는 사용자 정의 템플릿의 샘플 구현입니다.

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

## 사용자 정의 템플릿을 위한 기술 사양 {#technical-specifications-for-custom-templates}

모든 Forms 포털 구성 요소에 대한 사용자 정의 템플릿에는 반복 및 반복되지 않는 항목이 포함됩니다. 반복 가능한 항목은 나열된 기본 엔티티입니다. 반복 가능한 항목의 예는 검색 및 목록, 초안 및 제출, 링크 구성 요소입니다.

Forms 포털에서는 자리 표시자가 사용자 지정/OOTB 메타데이터를 표시하는 구문을 제공합니다. 자리 표시자는 양식, 초안 또는 제출 결과를 표시한 후에 채워집니다.

반복 가능한 항목을 포함하려면 **데이터 반복 가능 속성 값을** true로 **구성합니다**.

*설명한 예에서 사용자 지정 템플릿의 맨 위에 두 개의 Div 요소가 있습니다. 첫 번째 클래스는 &quot;__FP_boxes-container&quot; CSS 클래스를 사용하여 나열된 양식의 컨테이너 요소로 작동합니다. 두 번째 CSS 클래스는 &quot;__FP_boxes&quot; CSS 클래스를 사용하는 것으로, 이 경우에는 Form입니다. Div 요소에 있는&#x200B;**데이터 반복**속성은 값이&#x200B;**true입니다**.*

각 자리 표시자에는 전용 OOTB 메타데이터 세트가 있습니다. 양식의 특정 위치에 사용자 지정 메타데이터를 표시하려면 해당 위치에 **${metadata_prop} 속성을** 추가하십시오.

*이 예제에서 메타데이터 속성은 여러 인스턴스에서 사용됩니다. 예를 들어, 설명,**이름**,**양식**URL **, html****스타일, html**pdfUrl ************, pdfUrl, pdf스타일, pdfStyleVertising, VertisingWith the mannerVertisingWith the manner에 지정된 방법으로 사용됩니다.*

## 기본 메타데이터 {#out-of-the-box-metadata}

다양한 Forms 포털 구성 요소는 나열을 위해 사용할 수 있는 OOTB 메타데이터의 전용 세트를 제공합니다.

### 검색 및 라이브러리 구성 요소 {#search-amp-lister-component}

* **제목:** 양식의 제목
* **이름**: 양식의 이름(대부분 제목과 동일)
* **설명**: 양식의 설명
* **formUrl**: 양식을 HTML로 렌더링하는 URL
* **pdfUrl**: 양식을 PDF로 렌더링하는 URL
* **assetType**: 자산의 유형입니다. 유효한 값에는 **양식**,**PDF 양식**, **인쇄 양식**&#x200B;및 **적응형 양식등이있습니다.**

* **htmlStyle**&amp; **pdfStyle**: 렌더링을 위해 각각 사용되는 HTML 및 PDF 아이콘의 스타일을 표시합니다. 유효한 값은 &quot;**__FP_display_none**&quot; 또는 비어 있는 값입니다.

>[!NOTE]
>
>사용자 지정 스타일 시트에서 __FP_display_none 클래스를 사용해야 합니다.

* **downloadUrl**: 자산을 다운로드하는 URL.

사용자 인터페이스에서 로컬라이제이션, 정렬 및 구성 속성 사용 지원(검색 및 목록만 해당):

1. **로컬라이제이션 지원**: 정적 텍스트를 현지화하려면 속성을 사용하고 현지화된 값을 사용할 수 있도록 `${localize-YOUR_TEXT}` 하십시오(아직 없는 경우).
   *설명한 예에서 속성`${localize-Apply}`과`${localize-Download}`는 적용 및 다운로드 텍스트를 현지화하는 데 사용됩니다.*

1. **정렬 지원**: 검색 결과를 정렬하려면 HTML 요소를 클릭합니다. 단일화된 레이아웃에서 정렬을 구현하려면 특정 테이블 머리글에 &quot;data-sortKey&quot; 속성을 추가하십시오. 또한 값을 정렬할 메타데이터로 추가합니다.
예를 들어 격자 보기의 &quot;제목&quot; 헤더의 경우 &quot;data-sortKey&quot; 헤더의 값은 &quot;title&quot;입니다. 제목을 클릭하여 특정 열의 값을 정렬합니다.

1. **구성 속성 사용**: 검색 및 목록 구성 요소에는 사용자 인터페이스에서 사용할 수 있는 여러 구성이 있습니다. 예를 들어 편집 대화 상자를 통해 저장된 HTML 도구 설명 텍스트를 표시하려면 속성을 `${config-htmlLinkText}` 사용합니다. **마찬가지로 PDF 도구 설명 텍스트의 경우 속성을** 사용하십시오 `${config-pdfLinkText}` .

### 링크 구성 요소 {#link-component}

* **제목:** 양식의 제목
* **formUrl**: 양식을 HTML로 렌더링하는 URL
* **target**: 링크의 Target 속성입니다. 유효한 값은 &quot;_blank&quot; 및 &quot;_self&quot;입니다.
* **linkText**: 링크 캡션

### 초안 및 제출 구성 요소 {#drafts-amp-submissions-component}

* **경로**: 초안/제출 메타데이터 노드의 경로입니다. .HTML 확장자와 함께 URL로 사용하여 초안 또는 제출 양식을 엽니다.
* **contextPath**: AEM 인스턴스의 컨텍스트 경로
* **firstLetter**: 응용 양식 제목의 첫 번째 문자(대문자)로 저장되거나 제출됩니다.
* **formName**: 초안으로 저장하거나 제출된 적응형 양식의 제목입니다.
* **draftID**: 나열된 초안에 대한 ID(초안 섹션의 템플릿에만 사용).
* **submitID**: 나열된 제출용 ID(제출 섹션의 템플릿에만 사용).
* **상태**: 제출된 양식의 상태입니다. (제출 섹션의 템플릿에서만 사용).
* **설명**: 초안 또는 제출과 관련된 응용 양식에 대한 설명입니다.
* **diffTime**: 초안의 현재 시간과 마지막 저장 작업 간의 차이입니다. 또는 현재 시간과 제출한 마지막 제출 작업 간의 차이입니다.
* **iconClass**: 초안/제출의 첫 번째 문자를 표시하는 데 사용되는 CSS 클래스입니다. Forms 포털에는 다양한 색상 배경을 제공하는 다음 클래스가 포함되어 있습니다.
* **소유자**: 초안/제출을 만든 사용자입니다.
* **오늘**: DD:MM:YYYY 형식으로 초안 또는 제출 날짜
* **TimeNow**: HH:MM:SS 24시간 형식으로 초안 또는 제출 시간

*메모:*

1. 초안 및 제출 구성 요소 아래의 초안 섹션에 있는 삭제 옵션에 대해 CSS 클래스 이름 &quot;__FP_deleteDraft&quot;를 지정합니다. 또한 해당 초안의 초안 ID인 값 **${draftID}**&#x200B;와 함께 &quot;draftID&quot; 속성을 포함합니다.

1. 초안 및 제출 문서를 열기 위한 링크를 만드는 동안 앵커 태그에 대한 **href** 특성의 값으로${path}.html을 **** 지정할 수 있습니다.

![초안 및 제출 노드](assets/raw-image-with-index.png)

**A**. 컨테이너 요소

**B.** &quot;path&quot; 메타데이터를 사용하여 각 양식에 대해 저장된 축소판을 가져올 수 있습니다.

**C.** 각 양식의 템플릿 섹션에 사용되는 데이터 반복 속성

**D.** &quot;적용&quot; 문자열을 현지화하려면

**E.** 구성 속성 pdfLinkText 사용

**F.** &quot;pdfUrl&quot; 메타데이터 사용

## 팁, 기법 및 알려진 문제 {#tips-tricks-and-known-issues}

1. 사용자 지정 템플릿에서 단일 따옴표(&#39;)를 사용하지 마십시오.
1. 사용자 지정 메타데이터의 경우 이 속성을 **jcr:content/metadata** 노드에만 저장합니다. 다른 곳에 저장한 경우 Forms 포털에서 메타데이터를 표시할 수 없습니다.
1. 사용자 지정 메타데이터 또는 기존 메타데이터의 이름에 콜론(:)이 포함되어 있지 않은지 확인합니다. ). 이 경우 사용자 인터페이스에 표시할 수 없습니다.
1. **데이터 반복 가능** 요소에는 **링크 구성 요소의 중요성이** 없습니다. Adobe에서는 링크 구성 요소의 템플릿에서 이 속성을 사용하지 않는 것이 좋습니다.

## 관련 문서

* [양식 포털 구성 요소 활성화](/help/forms/using/enabling-forms-portal-components.md)
* [양식 포털 페이지 만들기](/help/forms/using/creating-form-portal-page.md)
* [API를 사용하여 웹 페이지의 양식 목록 작성](/help/forms/using/listing-forms-webpage-using-apis.md)
* [초안 및 제출 구성 요소 사용](/help/forms/using/draft-submission-component.md)
* [초안 및 제출된 양식의 저장 사용자 정의](/help/forms/using/draft-submission-component.md)
* [초안 및 제출 구성 요소를 데이터베이스와 통합하는 샘플](/help/forms/using/integrate-draft-submission-database.md)
* [양식 포털 구성 요소에 대한 템플릿 사용자 정의](/help/forms/using/customizing-templates-forms-portal-components.md)
* [포털에서 양식 게시 소개](/help/forms/using/introduction-publishing-forms.md)