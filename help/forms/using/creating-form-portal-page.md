---
title: 양식 포털 페이지 만들기
seo-title: Creating a forms portal page
description: Forms Portal은 웹 개발자에게 Adobe Experience Manager(AEM)을 사용하여 작성된 웹 사이트에서 양식 포털을 만들고 사용자 지정할 수 있는 구성 요소를 제공합니다.
seo-description: Forms Portal equips Web Developers with components to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM).
uuid: a5017de5-616c-4ce4-81aa-f28c741f8e8f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 8fff78cb-9ef9-426e-8b30-d70b4f26887f
docset: aem65
feature: Forms Portal
exl-id: 22d7c24e-7a77-4324-afdf-74c1fbf15773
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 1%

---

# 양식 포털 페이지 만들기{#creating-a-forms-portal-page}

Forms 포털 구성 요소는 웹 개발자에게 Adobe Experience Manager(AEM)을 사용하여 작성된 웹 사이트에서 양식 포털을 만들고 사용자 지정하는 구성 요소를 제공합니다. Forms 포털에 대한 간단한 개요를 알려면 [포털에서 양식 게시 소개](../../forms/using/introduction-publishing-forms.md).

## 사전 요구 사항 {#prerequisites}

Forms 포털 구성 요소는 기본적으로 사용할 수 없습니다. 다음에 설명된 대로 다음 forms portal 구성 요소 카테고리가 활성화되어 있는지 확인합니다. [Forms 포털 구성 요소 활성화](/help/forms/using/enabling-forms-portal-components.md).

**문서 서비스** 검색 및 목록, 링크, 초안 및 제출 구성 요소를 포함합니다.

**문서 서비스 설명** 날짜 설명, 전체 텍스트 설명, 속성 설명 및 태그 설명 구성 요소를 포함합니다. 이러한 구성 요소는 검색 및 목록 구성 요소에서 검색을 구성하는 데 사용됩니다.

AEM 사이트 페이지에서 활성화되면 이러한 구성 요소 카테고리를 구성 요소 브라우저에서 사용할 수 있습니다.

![구성 요소 브라우저의 AEM Forms 포털 구성 요소](assets/component-categories.png)

Forms 포털 구성 요소 카테고리

## 검색 및 목록 구성 요소 {#search-amp-lister-component}

문서 서비스 구성 요소 카테고리에서 사용할 수 있는 검색 및 목록 구성 요소는 페이지의 양식을 나열하고 나열된 양식에서 검색을 구현하는 데 사용됩니다. 구성 요소에는 두 개의 창이 있습니다.

* 양식이 나열된 목록 창입니다.
* 검색 기능을 추가하는 검색 창.

구성 요소 브라우저의 문서 서비스 구성 요소 카테고리에서 검색 및 목록 구성 요소를 페이지로 끌어다 놓을 수 있습니다. 구성 요소를 추가하면 다음과 비슷한 형태로 표시됩니다.

![페이지의 검색 및 목록 구성 요소](assets/fp-grid-viw.png)

그리드 레이아웃이 있는 페이지에서 구성 요소 검색 및 목록 작성

### 목록 창 {#list-pane}

목록 창은 양식이 나열된 영역입니다. 검색 및 목록 구성 요소는 목록 창에서 양식의 표시를 제어하는 데 사용할 수 있는 다양한 구성 옵션을 제공합니다.

목록 창을 구성하려면 검색 및 목록 구성 요소를 탭한 다음, ![settings_icon](assets/settings_icon.png). 다음 **[!UICONTROL 구성 요소 편집]** 대화 상자가 열립니다.

![편집 모드의 목록 창](assets/edit-list.png)

편집 모드의 목록 창

다음 **편집** 대화 상자에는 아래 표에 설명된 구성 옵션을 제공하는 여러 탭이 있습니다. 탭 **확인** 구성을 저장하려면 이 작업을 수행합니다.

<table>
 <tbody>
  <tr>
   <th>탭</th>
   <th>구성</th>
   <th>설명</th>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>에셋 폴더</strong></code></td>
   <td>항목 추가</td>
   <td>AEM Forms UI를 사용하여 자산이 업로드되는 폴더를 구성합니다. 기본적으로 업로드된 모든 자산이 나열됩니다. AEM Forms UI에 대한 자세한 내용은 <a href="../../forms/using/introduction-managing-forms.md" target="_blank">양식 관리 소개</a>.</td>
  </tr>
  <tr>
   <td><p><span class="uicontrol"><strong>표시</strong></code></p> </td>
   <td>제목 텍스트</td>
   <td>Search &amp; Lister 구성 요소의 제목. 기본 제목은 <strong>Forms 포털.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>레이아웃 템플릿</td>
   <td>자산의 레이아웃. </td>
  </tr>
  <tr>
   <td> </td>
   <td>고급 검색 비활성화</td>
   <td>활성화되면 고급 검색 아이콘을 숨깁니다.</td>
  </tr>
  <tr>
   <td> </td>
   <td>텍스트 검색 비활성화</td>
   <td>활성화되면 은 전체 텍스트 검색 막대를 숨깁니다.</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>결과</strong></code></td>
   <td>페이지당 결과 수</td>
   <td>페이지에 표시할 최대 양식 수를 구성합니다.</td>
  </tr>
  <tr>
   <td> </td>
   <td>결과 텍스트</td>
   <td><p>결과 텍스트를 구성합니다(예: 601의 1-12개) <strong>결과</strong>). 기본값은 입니다. <strong>결과</strong>.</p> <p>예를 들어 <strong>Forms </strong>이 필드에 총 601개의 양식이 있고 결과 텍스트가 601의 1-12로 변경됩니다 <strong>Forms.</strong></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>페이지 텍스트</td>
   <td><p>페이지 텍스트를 구성합니다(예: <strong>페이지 </strong>1 / 51) 기본값은 입니다. <strong>페이지</strong>.</p> <p>예를 들어 <strong>애플리케이션 양식 </strong>이 필드에 51페이지가 있고 페이지 텍스트가 <strong>애플리케이션 양식 </strong>51 중 1.</p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>/ 텍스트</td>
   <td><p>단어 바꾸기 <strong>의</strong> 지정된 텍스트 사용(페이지 1) <strong>의 </strong>51). 기본값은 입니다. <strong>의</strong>.</p> <p>예를 들어 <strong>out </strong>이 필드에서 텍스트가 1페이지로 변경됩니다 <strong>out </strong>51.</p> </td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>양식 링크</strong></code></td>
   <td>렌더링 유형</td>
   <td>지정된 렌더링 유형에 따라 양식 목록을 제어합니다. 사용 가능한 옵션은 PDF 및 HTML입니다. 예를 들어 HTML 유형으로만 렌더링 을 선택하면 PDF forms이 필터링됩니다.</td>
  </tr>
  <tr>
   <td> </td>
   <td>HTML 프로필</td>
   <td>렌더링에 사용할 HTML 프로필을 구성합니다. 사용 가능한 모든 프로필이 드롭다운 목록에 나열됩니다.</td>
  </tr>
  <tr>
   <td> </td>
   <td>제출 URL</td>
   <td><p>양식 데이터가 전송되는 서블릿을 구성합니다.</p> <p><strong>참고:</strong> <em>양식에 대한 제출 URL은 여러 위치에서 지정할 수 있으며 우선순위는 다음과 같습니다.</em></p>
    <ol>
     <li><em>양식(제출 단추)에 포함된 제출 URL의 우선 순위가 가장 높습니다.</em></li>
     <li><em>AEM Forms UI에 언급된 제출 URL은 두 번째로 높은 우선 순위를 갖습니다.</em></li>
     <li><em>양식 포털에 언급된 제출 URL의 우선 순위가 가장 낮습니다.</em></li>
    </ol> </td>
  </tr>
  <tr>
   <td> </td>
   <td>HTML 렌더링 작업 도구 팁</td>
   <td>포인터를 위에 두면 표시되는 도구 팁의 텍스트를 구성합니다 <img height="16" src="assets/aem6forms_panel-html.png" width="13" /> (HTML 5 아이콘)</td>
  </tr>
  <tr>
   <td> </td>
   <td>PDF 렌더링 작업 도구 팁</td>
   <td>포인터를 위에 두면 표시되는 도구 팁의 텍스트를 구성합니다 <img height="16" src="assets/aem6forms_panel-pdf.png" width="14" /> (PDF 아이콘)</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>스타일</strong></code></td>
   <td>스타일 유형</td>
   <td>다음을 지정할 수 있습니다 <strong>스타일 없음, 기본 스타일</strong>, 또는 <strong>사용자 지정 스타일 </strong>참조하십시오.</td>
  </tr>
  <tr>
   <td> </td>
   <td>사용자 지정 스타일 경로</td>
   <td>사용자 지정 을 스타일 유형으로 선택한 경우 이동하여 사용자 정의 CSS의 경로를 지정하고 그렇지 않으면 기본값 을 선택합니다.</td>
  </tr>
 </tbody>
</table>

### 검색 창 {#search-pane}

검색 창에서는 AEM Sidekick의 문서 서비스 설명 범주에서 날짜 설명, 전체 텍스트 설명, 속성 설명 및 태그 설명 구성 요소를 추가할 수 있습니다. 이러한 구성 요소는 사용자가 나열된 양식에서 검색을 수행할 수 있도록 검색 기능을 구현합니다.

**팁:** *사전 설정된 기준에 따라 양식 포털에 표시되는 양식 목록을 제어하고 최종 사용자의 검색 기능을 숨길 수 있습니다. 양식 목록을 제어하려면 설명 구성 요소를 사용하여 검색 필터를 적용합니다. 기본 필터 값을 지정하고 구성 요소 편집 대화 상자의 표시 탭에서 검색을 비활성화할 수도 있습니다.*

![날짜, 전체 텍스트, 속성 및 태그 설명이 있는 검색 패널](assets/search-with-predicates.png)

날짜, 전체 텍스트, 속성 및 태그 설명이 있는 검색 패널

#### 날짜 설명 {#date-predicate}

날짜 설명 구성 요소를 추가하면 지정된 기간 동안 수정된 나열된 양식을 검색할 수 있습니다.

날짜 설명 구성 요소를 구성하려면

1. 구성 요소를 탭한 다음, ![settings_icon](assets/settings_icon.png). 편집 대화 상자가 열립니다.
1. 다음을 지정합니다.

   * **유형:** 사용 가능한 유일한 옵션은 다음과 같습니다 **마지막 수정 날짜**

   * **텍스트:** 날짜 설명 구성 요소의 레이블 또는 캡션입니다. 기본값은 입니다. **마지막 수정 날짜.**

   * **시작 날짜 레이블:** 시작 날짜 필드의 레이블 또는 캡션
   * **종료 날짜 레이블:** 종료 날짜 필드에 대한 레이블 또는 캡션
   * **숨기기:** 목록 양식에 기본 날짜 필터를 적용하려면

1. 탭 **확인**

#### 전체 텍스트 설명 {#full-text-predicate}

전체 텍스트 설명 구성 요소는 이름 및 설명과 같은 양식 데이터에 대한 전체 텍스트 검색을 구현합니다. 사용자는 텍스트 문자열을 검색하여 이름이나 설명에 텍스트가 포함된 양식을 반환할 수 있습니다.

전체 텍스트 설명 구성 요소를 구성하려면

1. 구성 요소를 탭한 다음, ![settings_icon](assets/settings_icon.png). 편집 대화 상자가 열립니다.
1. 에서 제목을 지정합니다. **기본 제목** 필드.
1. 탭 **확인**

#### 속성 설명 {#properties-predicate}

속성 설명 구성 요소는 제목, 작성자 및 설명과 같은 양식 속성을 기반으로 양식 검색을 구현합니다.

속성 설명 구성 요소를 구성하려면

1. 구성 요소를 탭한 다음, ![settings_icon](assets/settings_icon.png). 편집 대화 상자가 열립니다.
1. 일반 탭에서 검색 레이블을 지정합니다. 기본값은 입니다. **속성**

1. 옵션 탭에서 **항목 추가.**
1. 드롭다운 목록에서 속성을 선택하고 드롭다운 목록 아래의 필드에 속성에 대한 검색 레이블을 지정합니다.
1. 속성을 더 추가하려면 4단계를 반복합니다. 지정한 기준에 따라 양식을 나열하고 최종 사용자가 검색할 속성을 숨기도록 기본 필터 값을 지정할 수도 있습니다. 속성에 대한 숨기기 확인란을 선택하고 기본 필터 값을 지정합니다.
예를 들어 제목에 &quot;여행&quot;이 포함된 양식을 표시하려면 제목 속성 옆에 있는 숨기기를 선택합니다. 또한 기본 필터 값 텍스트 상자에 여행 을 지정합니다.

1. 탭 **확인**

#### 태그 설명 {#tags-predicate}

태그 설명 구성 요소는 Forms Manager에 정의된 태그를 기반으로 양식 검색을 구현합니다.

태그 설명 구성 요소를 구성하려면

1. 구성 요소를 탭한 다음, ![settings_icon](assets/settings_icon.png). 편집 대화 상자가 열립니다.
1. 태그 필드 옆에 있는 아래쪽 화살표 단추를 누릅니다.
1. 적절한 태그 선택
1. 탭 **확인**

선택한 태그가 검색 창에 선택용 확인란과 함께 나타납니다. 이제 태그를 기준으로 검색 범위를 좁힐 수 있습니다.

## 페이지에 양식 나열 {#list-forms-on-a-page-br}

페이지에 양식을 나열하려면 **[!UICONTROL 검색 및 목록]** 구성 요소를 페이지에 추가하고 **[!UICONTROL 목록 창]**. 최종 사용자가 날짜, 텍스트 및 태그로 양식을 검색할 수 있도록 하려면 **[!UICONTROL 검색 창]** 구성 요소.

페이지의 어디에서든지 양식을 연결하려면 링크 구성 요소를 사용하십시오. 링크 구성 요소에 대한 자세한 내용은 [페이지에 링크 구성 요소 포함](../../forms/using/embedding-link-component-page.md).

초안 상태의 양식과 이미 제출된 양식을 나열하려면 **[!UICONTROL 초안 및 제출]** 구성 요소. 자세한 내용은 [초안 및 제출 구성 요소 사용자 정의](../../forms/using/draft-submission-component.md).

## 모바일 장치 친화성 {#mobile-device-friendliness}

Forms Portal Search &amp; Lister 구성 요소는 모바일 장치에 친숙하며 그에 따라 조정됩니다. 세 가지 기본 보기 모두: 사이트가 열려 있는 장치에 따른 그리드, 카드, 패널 릴레이아웃은 웹 페이지도 적용된다는 사실과 함께 제공됩니다. 간단한 사실은 Search &amp; Lister는 구성 요소만 제공하며 페이지 수준 스타일링을 제어하지 않는다는 것입니다.

다음 이미지는 모바일 장치에서 열 때 Search &amp; Lister 구성 요소를 나타냅니다.

![검색 및 목록 구성 요소의 스크린샷](assets/search_lister.png)

Search &amp; Lister 구성 요소

## 양식 포털 페이지 사용자 지정 {#customizing-a-forms-portal-page-br}

Forms 포털 페이지를 사용자 지정하여 페이지에 고유한 모양을 제공할 수 있습니다. 또한 메타데이터를 추가하여 검색 환경을 개선하고 페이지의 레이아웃을 변경하고 사용자 지정 CSS 스타일을 추가할 수도 있습니다. 자세한 내용은 [Forms Portal 구성 요소에 대한 템플릿 사용자 정의](../../forms/using/customizing-templates-forms-portal-components.md).

AEM Forms UI를 통해 사용자 지정 메타데이터를 양식에 추가할 수 있습니다. 사용자 지정 메타데이터는 최종 사용자에게 양식 경험을 제공하고 검색하는 데 유용합니다. 사용자 지정 메타데이터에 대한 자세한 내용은 [Forms Portal 구성 요소에 대한 템플릿 사용자 정의](../../forms/using/customizing-templates-forms-portal-components.md).

곧바로 사용할 수 있는 forms 포털에서는 렌더링 작업을 제공합니다. 양식 포털을 사용자 지정하여 추가 작업을 추가할 수 있습니다. 자세한 내용은 [양식 목록 항목에 사용자 지정 작업 추가](../../forms/using/add-custom-action-form-lister.md)

## 관련 문서

* [Forms 포털 구성 요소 활성화](/help/forms/using/enabling-forms-portal-components.md)
* [Forms 포털 만들기 페이지](/help/forms/using/creating-form-portal-page.md)
* [API를 사용하여 웹 페이지의 양식 나열](/help/forms/using/listing-forms-webpage-using-apis.md)
* [초안 및 제출 구성 요소 사용](/help/forms/using/draft-submission-component.md)
* [초안 및 제출된 양식의 저장 공간 사용자 정의](/help/forms/using/draft-submission-component.md)
* [초안 및 제출 구성 요소와 데이터베이스를 통합하기 위한 샘플](/help/forms/using/integrate-draft-submission-database.md)
* [Forms 포털 구성 요소에 대한 템플릿 사용자 지정](/help/forms/using/customizing-templates-forms-portal-components.md)
* [포털에서 양식 게시 소개](/help/forms/using/introduction-publishing-forms.md)
