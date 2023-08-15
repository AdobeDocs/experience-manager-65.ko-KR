---
title: Forms 포털 페이지 만들기
seo-title: Creating a forms portal page
description: Forms 포털은 웹 개발자에게 Adobe Experience Manager(AEM)를 사용하여 작성된 웹 사이트에서 양식 포털을 만들고 사용자 정의할 수 있는 구성 요소를 제공합니다.
seo-description: Forms Portal equips Web Developers with components to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM).
uuid: a5017de5-616c-4ce4-81aa-f28c741f8e8f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 8fff78cb-9ef9-426e-8b30-d70b4f26887f
docset: aem65
feature: Forms Portal
exl-id: 22d7c24e-7a77-4324-afdf-74c1fbf15773
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 2%

---

# Forms 포털 페이지 만들기{#creating-a-forms-portal-page}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-forms-portal.html) |
| AEM 6.5 | 이 문서 |

Forms 포털 구성 요소는 웹 개발자에게 Adobe Experience Manager(AEM)를 사용하여 작성된 웹 사이트에서 양식 포털을 만들고 사용자 지정할 수 있는 구성 요소를 제공합니다. Forms 포털에 대한 간략한 개요는 를 참조하십시오. [포털에 양식 게시 소개](../../forms/using/introduction-publishing-forms.md).

## 사전 요구 사항 {#prerequisites}

Forms 포털 구성 요소는 기본적으로 사용할 수 없습니다. 에 설명된 대로 다음 양식 포털 구성 요소 카테고리가 활성화되어 있는지 확인합니다. [Forms 포털 구성 요소 활성화](/help/forms/using/enabling-forms-portal-components.md).

**문서 서비스** 검색 및 목록, 링크, 초안 및 제출 구성 요소를 포함합니다.

**문서 서비스 조건자** 날짜 설명, 전체 텍스트 설명, 속성 설명 및 태그 설명 구성 요소를 포함합니다. 이러한 구성 요소는 검색 및 목록 구성 요소에서 검색을 구성하는 데 사용됩니다.

AEM 사이트 페이지에서 이러한 구성 요소 카테고리가 활성화되면 구성 요소 브라우저에서 사용할 수 있습니다.

![구성 요소 브라우저의 AEM Forms 포털 구성 요소](assets/component-categories.png)

Forms 포털 구성 요소 범주

## 검색 및 목록 구성 요소 {#search-amp-lister-component}

문서 서비스 구성 요소 카테고리 아래에 있는 검색 및 목록 구성 요소를 사용하여 페이지에 양식을 나열하고 나열된 양식에 검색을 구현할 수 있습니다. 구성 요소에는 두 개의 창이 있습니다.

* 양식이 나열된 목록 창입니다.
* 검색 기능을 추가하는 검색 창.

구성 요소 브라우저의 문서 서비스 구성 요소 카테고리에서 검색 및 목록 구성 요소를 페이지로 드래그 앤 드롭할 수 있습니다. 구성 요소가 추가되면 다음과 유사합니다.

![페이지의 검색 및 목록 구성 요소](assets/fp-grid-viw.png)

그리드 레이아웃이 있는 페이지의 검색 및 목록 구성 요소

### 목록 창 {#list-pane}

목록 창은 양식이 나열되는 영역입니다. 검색 및 목록 구성 요소는 목록 창에서 양식 표시를 제어하는 데 사용할 수 있는 다양한 구성 옵션을 제공합니다.

목록 창을 구성하려면 검색 및 목록 구성 요소를 탭한 다음 을 누릅니다 ![settings_icon](assets/settings_icon.png). 다음 **[!UICONTROL 구성 요소 편집]** 대화 상자가 열립니다.

![편집 모드의 목록 창](assets/edit-list.png)

편집 모드의 목록 창

다음 **편집** 대화 상자에는 아래 표에 설명된 구성 옵션을 제공하는 몇 가지 탭이 있습니다. 누르기 **확인** 구성을 저장할 수 있습니다.

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
   <td>AEM Forms UI를 사용하여 에셋을 업로드하는 폴더를 구성합니다. 기본적으로 업로드된 모든 에셋이 나열됩니다. AEM Forms UI에 대한 자세한 내용은 <a href="../../forms/using/introduction-managing-forms.md" target="_blank">양식 관리 소개</a>.</td>
  </tr>
  <tr>
   <td><p><span class="uicontrol"><strong>표시</strong></code></p> </td>
   <td>제목 텍스트</td>
   <td>검색 및 목록 작성자 구성 요소의 제목입니다. 기본 제목은 입니다. <strong>Forms 포털</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>레이아웃 템플릿</td>
   <td>에셋 레이아웃. </td>
  </tr>
  <tr>
   <td> </td>
   <td>고급 검색 비활성화</td>
   <td>활성화되면 고급 검색 아이콘을 숨깁니다.</td>
  </tr>
  <tr>
   <td> </td>
   <td>텍스트 검색 비활성화</td>
   <td>활성화되면 전체 텍스트 검색 막대를 숨깁니다.</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>결과</strong></code></td>
   <td>페이지당 결과 수</td>
   <td>페이지에 표시할 최대 양식 수를 구성합니다.</td>
  </tr>
  <tr>
   <td> </td>
   <td>결과 텍스트</td>
   <td><p>결과 텍스트 구성(예: 601의 1~12) <strong>결과</strong>). 기본값은 입니다. <strong>결과</strong>.</p> <p>예를 들어, <strong>Forms </strong>이 필드에서는 총 601개의 양식이 있으며 결과 텍스트가 601개의 1-12개로 변경됩니다 <strong>Forms.</strong></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>페이지 텍스트</td>
   <td><p>페이지 텍스트를 구성합니다(예: <strong>페이지 </strong>1/51). 기본값은 입니다. <strong>페이지</strong>.</p> <p>예를 들어, <strong>애플리케이션 양식 </strong>이 필드에서 51페이지가 표시되면 페이지 텍스트가 <strong>애플리케이션 양식 </strong>51개 중 1개</p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>/ 텍스트</td>
   <td><p>단어 바꾸기 <strong>/</strong> 지정된 텍스트 포함(1페이지) <strong>/ </strong>51). 기본값은 입니다. <strong>/</strong>.</p> <p>예를 들어, <strong>개 중 </strong>이 필드의 텍스트는 1페이지로 변경됩니다 <strong>개 중 </strong>51.</p> </td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>양식 링크</strong></code></td>
   <td>렌더링 유형</td>
   <td>지정된 렌더링 형식을 기반으로 양식 목록을 제어합니다. 사용 가능한 옵션은 PDF 및 HTML 입니다. 예를 들어 렌더링 유형으로 HTML 만 선택하면 PDF forms이 필터링됩니다.</td>
  </tr>
  <tr>
   <td> </td>
   <td>HTML 프로필</td>
   <td>렌더링에 사용할 HTML 프로필을 구성합니다. 사용 가능한 모든 프로필이 드롭다운 목록에 나열됩니다.</td>
  </tr>
  <tr>
   <td> </td>
   <td>URL 제출</td>
   <td><p>양식 데이터가 제출되는 서블릿을 구성합니다.</p> <p><strong>참고:</strong> <em>양식의 제출 URL은 여러 위치에서 지정할 수 있으며, 우선 순위는 다음과 같습니다.</em></p>
    <ol>
     <li><em>양식(제출 단추)에 포함된 제출 URL의 우선 순위가 가장 높습니다.</em></li>
     <li><em>AEM Forms UI에 언급된 제출 URL은 두 번째로 높은 우선 순위를 갖습니다.</em></li>
     <li><em>Forms 포털에 언급된 제출 URL의 우선 순위가 가장 낮습니다.</em></li>
    </ol> </td>
  </tr>
  <tr>
   <td> </td>
   <td>HTML 렌더링 작업 도구 팁</td>
   <td>포인터를 위에 올리면 표시되는 도구 설명에 대한 텍스트를 구성합니다. <img height="16" src="assets/aem6forms_panel-html.png" width="13" /> (HTML 5 아이콘).</td>
  </tr>
  <tr>
   <td> </td>
   <td>PDF 렌더링 작업 도구 팁</td>
   <td>포인터를 위에 올리면 표시되는 도구 설명에 대한 텍스트를 구성합니다. <img height="16" src="assets/aem6forms_panel-pdf.png" width="14" /> (PDF 아이콘).</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>스타일</strong></code></td>
   <td>스타일 유형</td>
   <td>다음을 지정할 수 있습니다. <strong>스타일 없음, 기본 스타일</strong>, 또는 <strong>사용자 정의 스타일 </strong>양식 목록을 만드는 경우.</td>
  </tr>
  <tr>
   <td> </td>
   <td>사용자 지정 스타일 경로</td>
   <td>[스타일 유형]으로 [사용자 지정]을 선택한 경우 사용자 지정 CSS의 경로를 찾아 지정한 다음 [기본값]을 선택합니다.</td>
  </tr>
 </tbody>
</table>

### 검색 창 {#search-pane}

검색 창에서는 AEM Sidekick의 문서 서비스 술어 범주에서 날짜 술어, 전체 텍스트 술어, 속성 술어 및 태그 술어 구성 요소를 추가할 수 있습니다. 이러한 구성 요소는 사용자가 나열된 양식에서 검색을 수행할 수 있는 검색 기능을 구현합니다.

**팁:** *사전 설정된 기준에 따라 양식 포털에 표시되는 양식 목록을 제어하고 최종 사용자를 위한 검색 기능을 숨길 수 있습니다. 양식 목록을 제어하려면 술어 구성 요소를 사용하여 검색 필터를 적용합니다. 구성 요소 편집 대화 상자의 디스플레이 탭에서 기본 필터 값을 지정하고 검색을 비활성화할 수도 있습니다.*

![날짜, 전체 텍스트, 속성 및 태그 술어가 있는 검색 패널](assets/search-with-predicates.png)

날짜, 전체 텍스트, 속성 및 태그 술어가 있는 검색 패널

#### 날짜 조건자 {#date-predicate}

날짜 설명 구성 요소가 추가되면 지정된 기간 동안 수정된 나열된 양식을 검색할 수 있습니다.

날짜 설명 구성 요소를 구성하려면 다음을 수행하십시오.

1. 구성 요소를 탭한 다음 을 탭합니다. ![settings_icon](assets/settings_icon.png). 편집 대화 상자가 열립니다.
1. 다음을 지정합니다.

   * **유형:** 사용할 수 있는 유일한 옵션은 입니다. **마지막 수정 날짜**

   * **텍스트:** 날짜 설명 구성 요소의 레이블 또는 캡션입니다. 기본값은 입니다. **마지막으로 수정한 날짜.**

   * **시작 날짜 레이블:** 시작 날짜 필드의 레이블 또는 캡션
   * **종료 날짜 레이블:** 종료 날짜 필드의 레이블 또는 캡션
   * **숨기기:** 목록 양식에 기본 날짜 필터를 적용하려면

1. 누르기 **확인**

#### 전체 텍스트 조건자 {#full-text-predicate}

전체 텍스트 설명 구성 요소는 이름 및 설명과 같은 양식 데이터에 대한 전체 텍스트 검색을 구현합니다. 사용자는 모든 텍스트 문자열을 검색하여 이름 또는 설명에 텍스트가 포함된 양식을 반환할 수 있습니다.

전체 텍스트 설명 구성 요소를 구성하려면 다음을 수행합니다.

1. 구성 요소를 탭한 다음 을 탭합니다. ![settings_icon](assets/settings_icon.png). 편집 대화 상자가 열립니다.
1. 다음에서 제목을 지정합니다. **메인 제목** 필드.
1. 누르기 **확인**

#### 속성 조건자 {#properties-predicate}

속성 설명 구성 요소는 제목, 작성자 및 설명과 같은 양식 속성을 기반으로 양식 검색을 구현합니다.

속성 설명 구성 요소를 구성하려면 다음을 수행합니다.

1. 구성 요소를 탭한 다음 을 탭합니다. ![settings_icon](assets/settings_icon.png). 편집 대화 상자가 열립니다.
1. 일반 탭에서 검색 레이블을 지정합니다. 기본값은 입니다. **속성**

1. 옵션 탭에서 을 누릅니다. **항목 추가.**
1. 드롭다운 목록에서 속성을 선택하고 드롭다운 목록 아래의 필드에 속성에 대한 검색 레이블을 지정합니다.
1. 속성을 더 추가하려면 4단계를 반복합니다. 지정된 조건에 따라 양식을 나열할 기본 필터 값을 지정하고 최종 사용자가 검색할 속성을 숨길 수도 있습니다. 속성에 대한 숨기기 확인란을 선택하고 기본 필터 값을 지정합니다.
예를 들어 제목에 &quot;이동&quot;이 포함된 양식을 표시하려면 제목 속성 옆에 있는 숨기기를 선택합니다. 또한 기본 필터 값 텍스트 상자에 [이동]을 지정합니다.

1. 누르기 **확인**

#### 태그 조건자 {#tags-predicate}

태그 설명 구성 요소는 Forms Manager에 정의된 태그를 기반으로 양식 검색을 구현합니다.

태그 술어 구성 요소를 구성하려면 다음 작업을 수행하십시오.

1. 구성 요소를 탭한 다음 을 탭합니다. ![settings_icon](assets/settings_icon.png). 편집 대화 상자가 열립니다.
1. 태그 필드 옆에 있는 아래쪽 화살표 단추를 누릅니다.
1. 적절한 태그 선택
1. 누르기 **확인**

선택한 태그는 검색 창에 선택 확인란과 함께 나타납니다. 이제 사용자는 태그를 기반으로 검색 범위를 좁힐 수 있습니다.

## 페이지의 양식 나열 {#list-forms-on-a-page-br}

페이지에 양식을 나열하려면 **[!UICONTROL Search &amp; Lister]** 구성 요소를 페이지에 추가하고 구성 요소를 **[!UICONTROL 목록 창]**. 최종 사용자가 날짜, 텍스트 및 태그를 사용하여 양식을 검색할 수 있도록 하려면 **[!UICONTROL 검색 창]** 구성 요소.

페이지의 어디에서든 양식을 연결하려면 링크 구성 요소를 사용하십시오. 링크 구성 요소에 대한 자세한 내용은 [페이지에 링크 구성 요소 포함](../../forms/using/embedding-link-component-page.md).

초안 상태의 양식과 이미 제출된 양식을 나열하려면 **[!UICONTROL 초안 및 제출]** 구성 요소. 자세한 내용은 [초안 및 제출 구성 요소 사용자 지정](../../forms/using/draft-submission-component.md).

## 모바일 장치 친화성 {#mobile-device-friendliness}

Forms 포털 검색 및 목록 구성 요소는 모바일 장치에 친숙하고 그에 따라 조정됩니다. 세 가지 기본 보기 모두: 격자, 카드, 패널 은 사이트가 열려 있는 장치에 따라 다시 레이아웃되며 웹 페이지도 조정된다는 사실을 제공합니다. 간단한 사실은 검색 및 목록 작성기는 구성 요소일 뿐이며 페이지 수준 스타일을 제어하지 않는다는 것입니다.

다음 이미지는 모바일 디바이스에서 열릴 때 검색 및 목록 작성기 구성 요소를 보여 줍니다.

![검색 및 목록 작성자 구성 요소의 스크린샷](assets/search_lister.png)

Search &amp; Lister 구성 요소

## Forms 포털 페이지 사용자 지정 {#customizing-a-forms-portal-page-br}

Forms 포털 페이지를 사용자 지정하여 페이지에 고유한 모양을 제공할 수 있습니다. 메타데이터를 추가하여 검색 환경을 개선하고, 페이지 레이아웃을 변경하고, 사용자 지정 CSS 스타일을 추가할 수도 있습니다. 자세한 내용은 [Forms 포털 구성 요소에 대한 템플릿 맞춤화](../../forms/using/customizing-templates-forms-portal-components.md).

AEM Forms UI를 사용하면 사용자 지정 메타데이터를 양식에 추가할 수 있습니다. 사용자 지정 메타데이터는 최종 사용자에게 목록 및 검색 양식 환경을 제공하는 데 유용합니다. 사용자 지정 메타데이터에 대한 자세한 내용은 [Forms 포털 구성 요소에 대한 템플릿 맞춤화](../../forms/using/customizing-templates-forms-portal-components.md).

기본적으로 Forms 포털에서는 렌더링 작업을 제공합니다. Forms 포털을 사용자 지정하여 더 많은 작업을 추가할 수 있습니다. 자세한 내용은 [양식 목록 항목에 사용자 지정 작업을 추가하는 중입니다.](../../forms/using/add-custom-action-form-lister.md)

## 관련 문서

* [Forms 포털 구성 요소 활성화](/help/forms/using/enabling-forms-portal-components.md)
* [Forms 포털 페이지 만들기](/help/forms/using/creating-form-portal-page.md)
* [API를 사용하여 웹 페이지의 목록 양식](/help/forms/using/listing-forms-webpage-using-apis.md)
* [초안 및 제출 구성 요소 사용](/help/forms/using/draft-submission-component.md)
* [초안 및 제출된 양식의 스토리지 사용자 지정](/help/forms/using/draft-submission-component.md)
* [초안 및 제출 구성 요소와 데이터베이스를 통합하기 위한 샘플](/help/forms/using/integrate-draft-submission-database.md)
* [Forms 포털 구성 요소에 대한 템플릿 맞춤화](/help/forms/using/customizing-templates-forms-portal-components.md)
* [포털에 양식 게시 소개](/help/forms/using/introduction-publishing-forms.md)
