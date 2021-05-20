---
title: Forms 포털 구성 요소에 대한 템플릿 사용자 지정
seo-title: Forms 포털 구성 요소에 대한 템플릿 사용자 지정
description: 양식 목록에 사용자 지정 메타데이터 표시
seo-description: 양식 목록에 사용자 지정 메타데이터 표시
uuid: 212109ca-85c8-4915-82e5-a18a0443be1b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 7566203f-2f80-4ce7-bff9-073d67119f64
docset: aem65
feature: Forms 포털
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 0%

---


# Forms 포털 구성 요소에 대한 템플릿 사용자 지정{#customizing-templates-for-forms-portal-components}

## 전제 조건 {#prerequisites}

[양식 메타데이터 관리](../../forms/using/manage-form-metadata.md)

HTML 및 CSS에 대한 작업 지식

## 개요 {#overview}

AEM Forms 사용자 인터페이스를 사용하면 양식에 메타데이터를 추가할 수 있습니다. 사용자 지정 메타데이터는 조직의 양식을 나열하고 검색하는 동안 사용자 경험을 향상시킬 수 있습니다.

Forms Portal을 사용하면 양식 목록에 사용자 지정 메타데이터를 사용할 수 있습니다. 자산에 대한 사용자 지정 템플릿을 만드는 동안 레이아웃을 수정하고 CSS 스타일 세트를 사용하여 사용자 지정 메타데이터를 사용할 수 있습니다.

다양한 Forms Portal 구성 요소에 대한 사용자 지정 템플릿을 만들려면 다음 단계를 수행하십시오.

## 사용자 지정 템플릿 만들기 {#creating-a-nbsp-custom-template}

1. /apps 아래에 sling:Folder 노드를 만듭니다.

   &quot;fpContentType&quot; 속성을 추가합니다. 사용자 지정 템플릿을 정의하는 구성 요소에 따라 속성에 적절한 값을 지정합니다.

   * 검색 및 목록 구성 요소:&quot;/libs/fd/fp/formTemplate&quot;
   * 초안 및 제출 구성 요소:

      * 초안 섹션:/libs/fd/fp/draftTemplate
      * 제출 섹션:/libs/fd/fp/submissionsTemplate
   * 링크 구성 요소:/libs/fd/fp/linkTemplate

   레이아웃 템플릿을 선택하는 동안 표시할 제목을 추가합니다.

   >[!NOTE]
   >
   >제목은 생성한 sling:Folder의 노드 이름과 다를 수 있습니다.

   다음 이미지는 Search &amp; Lister 구성 요소의 구성을 나타냅니다.
   ![sling:Folder 만들기](assets/1.png)

1. 이 폴더에서 사용자 지정 템플릿으로 사용할 template.html 파일을 만듭니다.
1. 아래 설명된 대로 사용자 지정 템플릿을 작성하고 사용자 지정 메타데이터를 사용합니다.

## 작업 예 {#working-example}

다음은 Forms Portal에서 Search &amp; Lister 구성 요소에 대한 사용자 지정 Geometrixx Gov 카드 레이아웃을 획득하는 사용자 지정 템플릿의 샘플 구현입니다.

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

## 사용자 지정 템플릿에 대한 기술 사양 {#technical-specifications-for-custom-templates}

모든 Forms Portal 구성 요소에 대한 사용자 지정 템플릿에 반복 가능한 항목과 반복 가능한 항목이 포함됩니다. 반복 가능한 항목은 나열할 기본 엔티티입니다. 반복 가능한 항목의 예는 Search &amp; Lister, Draft &amp; Submissions 및 Link 구성 요소입니다.

Forms Portal은 자리 표시자가 사용자 지정/OOTB 메타데이터를 표시하는 구문을 제공합니다. 양식, 초안 또는 제출 결과를 표시한 후 자리 표시자가 채워집니다.

반복 가능한 항목을 포함하려면 **data-repeable** 특성의 값을 **true**&#x200B;로 구성합니다.

*설명한 예에서, 두 개의 Div 요소가 사용자 지정 템플릿의 맨 위에 있습니다. __FP_boxes-container&quot; CSS 클래스를 사용하는 첫 번째 는 나열된 양식의 컨테이너 요소로 작동합니다. __FP_boxes&quot; CSS 클래스를 사용하는 두 번째 템플릿은 기본 엔티티의 템플릿입니다(이 경우 Form). Div 요소에 있는&#x200B;**data-repeable**속성에는&#x200B;**true**.* 값이 있습니다.

각 자리 표시자에는 배타적 OOTB 메타데이터 세트가 있습니다. 양식의 특정 위치에 사용자 지정 메타데이터를 표시하려면 위치에 **${metadata_prop} 속성**&#x200B;을 추가합니다.

*이 예제에서 메타데이터 속성은 여러 인스턴스에 사용됩니다. 예를 들어,**설명**,**이름**,**formUrl**,**htmlStyle**,**pdfUrl**,**pdfStyle**및&#x200B;**경로**에 지정된 방식으로 사용됩니다.*.

## 즉시 사용 가능한 메타데이터 {#out-of-the-box-metadata}

다양한 Forms Portal 구성 요소는 목록에 사용할 수 있는 OOTB 메타데이터의 전용 세트를 제공합니다.

### 검색 및 목록 구성 요소 {#search-amp-lister-component}

* **제목:** 양식의 제목
* **이름**:양식의 이름(대부분 제목과 동일함)
* **설명**:양식 설명
* **formUrl**:양식을 HTML로 렌더링할 URL
* **pdfUrl**:양식을 PDF로 렌더링할 URL
* **assetType**:자산의 유형입니다. 유효한 값에는 **양식**,**PDF 양식**, **인쇄 양식** 및 **적응형 양식**&#x200B;이 포함됩니다

* **htmlStyle**&amp;  **pdfStyle**:렌더링에 각각 사용되는 HTML 및 PDF 아이콘의 스타일을 표시합니다. 유효한 값은 &quot;**__FP_display_none**&quot;이거나 비어 있습니다.

>[!NOTE]
>
>사용자 지정 스타일 시트에서 __FP_display_none 클래스를 사용해야 합니다.

* **downloadUrl**:자산을 다운로드할 URL입니다.

사용자 인터페이스에서 현지화, 정렬 및 구성 속성 사용을 지원합니다(검색 및 구독만 해당).

1. **지역화 지원**:정적 텍스트를 현지화하려면 속성을  `${localize-YOUR_TEXT}` 사용하고 현지화된 값을 사용할 수 있도록 하십시오. 가 아직 없으면
   *설명한 예에서 속성  `${localize-Apply}` 및 `${localize-Download}` 는 적용 및 다운로드 텍스트를 현지화하는 데 사용됩니다.*

1. **정렬 지원**:검색 결과를 정렬하려면 HTML 요소를 클릭합니다. 상위 레이아웃에서 정렬을 구현하려면 특정 테이블 헤더에 &quot;data-sortKey&quot; 속성을 추가합니다. 또한 해당 값을 정렬할 메타데이터로 추가합니다.
예를 들어 그리드 보기의 &quot;Title&quot; 헤더에 대해 &quot;data-sortKey&quot; 헤더의 값은 &quot;title&quot;입니다. 특정 열의 값을 정렬하려면 제목을 클릭합니다.

1. **구성 속성 사용**:Search &amp; Lister 구성 요소에는 사용자 인터페이스에서 사용할 수 있는 몇 가지 구성이 있습니다. 예를 들어, 편집 대화 상자를 통해 저장된 HTML 도구 설명 텍스트를 표시하려면 `${config-htmlLinkText}` 속성을 사용합니다. **마찬가지로 PDF 도구 설명 텍스트의 경우 속성** `${config-pdfLinkText}` 을 사용합니다.

### 링크 구성 요소 {#link-component}

* **제목:** 양식의 제목
* **formUrl**:양식을 HTML로 렌더링할 URL
* **target**:링크의 Target 속성입니다. 유효한 값은 &quot;_blank&quot; 및 &quot;_self&quot;입니다.
* **linkText**:링크 캡션

### 초안 및 제출 구성 요소 {#drafts-amp-submissions-component}

* **경로**:초안/제출 메타데이터 노드의 경로입니다. .HTML 확장자와 함께 사용하여 초안 또는 제출을 열 수 있습니다.
* **contextPath**:AEM 인스턴스의 컨텍스트 경로
* **firstLetter**:적응형 양식의 제목 중 첫 번째 문자(대문자)로서 초안 또는 제출으로 저장되었습니다.
* **formName**:초안으로 저장되거나 제출된 적응형 양식의 제목입니다.
* **draftID**:나열된 초안의 ID(초안 섹션의 템플릿에서만 사용).
* **submitID**:나열된 제출 서류의 ID(제출 섹션의 템플릿에서만 사용)입니다.
* **상태**:제출된 양식의 상태입니다. (제출 서류 섹션의 템플릿에서만 사용)
* **설명**:초안 또는 제출과 연관된 적응형 양식의 설명입니다.
* **diffTime**:초안의 현재 시간과 마지막 저장 작업 간의 차이입니다. 또는 제출을 위한 현재 시간과 마지막 제출 작업 간의 차이입니다.
* **iconClass**:초안/제출의 첫 번째 문자를 표시하는 데 사용되는 CSS 클래스입니다. Forms Portal에는 다양한 색상 배경을 제공하는 다음 클래스가 포함되어 있습니다.
* **소유자**:초안/제출을 만든 사용자.
* **오늘**:DD:MM:YYYY 형식으로 초안 또는 제출 작성 날짜입니다.
* **TimeNow**:HH:MM:SS 24시간 형식으로 초안 또는 제출 작성 시간

*메모:*

1. 초안 및 제출 구성 요소의 초안 섹션에서 삭제 옵션에 대한 이름을 &quot;__FP_deleteDraft&quot;로 지정합니다. 또한 해당 초안의 초안 ID인 **${draftID}** 값과 함께 &quot;draftID&quot; 특성을 포함하십시오.

1. 초안 및 제출 문서를 여는 링크를 만드는 동안 **${path}.html** 을 앵커 태그에 대한 **href** 특성 값으로 지정할 수 있습니다.

![초안 및 제출 노드](assets/raw-image-with-index.png)

**A**. 컨테이너 요소

**B.**  &quot;path&quot; 메타데이터는 고정된 계층 구조로 되어 각 양식에 대해 저장된 축소판을 가져옵니다.

**C.** 각 양식의 템플릿 섹션에 사용되는 데이터 반복 가능한 속성입니다

**D.** &quot;적용&quot; 문자열을 현지화하려면

**E.** 구성 속성 pdfLinkText 사용

**F.** &quot;pdfUrl&quot; 메타데이터 사용

## 팁, 요령 및 알려진 문제 {#tips-tricks-and-known-issues}

1. 사용자 지정 템플릿에서 작은따옴표(&#39;)를 사용하지 마십시오.
1. 사용자 지정 메타데이터의 경우 이 속성을 **jcr:content/metadata** 노드에만 저장합니다. 다른 위치에 저장하면 Forms Portal에 메타데이터를 표시할 수 없습니다.
1. 사용자 지정 메타데이터 또는 기존 메타데이터의 이름에 콜론(:)이 포함되어 있지 않은지 확인하십시오.). 그럴 경우 사용자 인터페이스에 표시할 수 없습니다.
1. **data-** repeatableague는 Linkcomponent에 대한 의미가  **** 없습니다. Adobe은 링크 구성 요소에 대해 템플릿에서 이 속성을 사용하지 않도록 권장합니다.

## 관련 문서

* [Forms 포털 구성 요소 활성화](/help/forms/using/enabling-forms-portal-components.md)
* [Forms 포털 만들기 페이지](/help/forms/using/creating-form-portal-page.md)
* [API를 사용하여 웹 페이지의 양식 나열](/help/forms/using/listing-forms-webpage-using-apis.md)
* [초안 및 제출 구성 요소 사용](/help/forms/using/draft-submission-component.md)
* [초안 및 제출된 양식의 저장 공간 사용자 정의](/help/forms/using/draft-submission-component.md)
* [초안 및 제출 구성 요소와 데이터베이스를 통합하기 위한 샘플](/help/forms/using/integrate-draft-submission-database.md)
* [Forms 포털 구성 요소에 대한 템플릿 사용자 지정](/help/forms/using/customizing-templates-forms-portal-components.md)
* [포털에서 양식 게시 소개](/help/forms/using/introduction-publishing-forms.md)