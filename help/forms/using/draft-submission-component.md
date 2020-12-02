---
title: 초안 및 제출 구성 요소
seo-title: 초안 및 제출 구성 요소
description: 초안 및 제출 구성 요소는 초안 상태이며 이미 제출된 양식을 나열합니다. 구성 요소의 모양과 스타일을 사용자 정의할 수 있습니다.
seo-description: 초안 및 제출 구성 요소는 초안 상태이며 이미 제출된 양식을 나열합니다. 구성 요소의 모양과 스타일을 사용자 정의할 수 있습니다.
uuid: 42c205b5-3141-4b80-85d9-dad921e223a2
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: ad71b423-02e1-4476-9c7c-f832cea6b0a6
docset: aem65
translation-type: tm+mt
source-git-commit: 23252989bb8649b2f0b96a58972c831257e0c5dc
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---


# 초안 및 제출 구성 요소{#drafts-and-submissions-component}

초안 및 제출 구성 요소는 초안 상태의 모든 양식과 이미 제출된 양식을 나열합니다. 구성 요소에는 초안 및 제출된 양식에 대한 별도의 섹션(탭)이 있습니다. 사용자는 자신의 초안 및 제출된 양식만 볼 수 있습니다.

## 구성 요소 {#configuring-the-component} 구성

초안 및 제출 구성 요소에는 두 개의 탭이 있습니다.초안 및 제출.

제출 탭에 나타나는 적응형 양식의 제출을 활성화하려면 **제출 작업**&#x200B;을 **[Forms 포털 제출 작업](../../forms/using/configuring-submit-actions.md)으로 설정합니다. 또는,** Forms 포털 제출 옵션을 활성화합니다. 사용자가 양식을 제출할 때마다 양식이 제출 탭에 추가됩니다.

초안 기능은 기본적으로 활성화되어 있습니다. 사용자가 적응형 양식에서 **저장**&#x200B;을 클릭하면 양식이 초안 탭에 추가됩니다.

초안 및 제출 구성 요소를 추가하고 구성하려면 다음 단계를 수행하십시오.

1. 구성 요소 브라우저의 문서 서비스 카테고리 아래에 있는 **초안 및 제출** 구성 요소를 페이지에 드래그하여 놓습니다.
1. 구성 요소를 누른 다음 ![settings_icon](assets/settings_icon.png)을 눌러 구성 요소에 대한 편집 대화 상자를 엽니다.

   ![초안 및 제출 구성 요소](assets/drafts-submissions-edit.png)

1. 편집 대화 상자에서 다음 세부 사항을 지정하고 **Done**&#x200B;을 눌러 설정을 저장합니다.

<table>
 <tbody>
  <tr>
   <th>탭</th>
   <th>구성</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>일반</td>
   <td>총 결과</td>
   <td>표시할 최대 결과 수를 지정합니다. 결과 개수가 전체 결과 제한을 늘리면 구성 요소 아래쪽에 <strong>자세히 </strong>링크가 나타납니다. <strong>자세히 </strong>를 클릭하면 모든 양식이 표시됩니다. </td>
  </tr>
  <tr>
   <td> </td>
   <td>스타일 유형</td>
   <td>구성 요소의 스타일을 지정합니다. 양식을 나열하려면 <strong>스타일 없음</strong>, <strong>기본 스타일</strong> 또는 <strong>사용자 지정 스타일</strong>을 지정할 수 있습니다. 사용자 지정 스타일 옵션의 경우 <strong>사용자 지정 스타일 경로 </strong>필드<strong>에서 사용자 지정 CSS 파일의 경로를 지정할 수 있습니다.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>사용자 지정 스타일 경로</td>
   <td><strong>스타일 유형</strong> 필드에서 <strong>사용자 지정 스타일</strong> 옵션을 선택하는 경우 <strong>사용자 지정 스타일 경로</strong> 필드를 사용하여 사용자 지정 CSS 파일의 경로를 지정합니다. </td>
  </tr>
  <tr>
   <td> </td>
   <td>표시 옵션</td>
   <td><p>표시할 탭을 지정합니다. 초안 양식, 제출된 양식 또는 둘 다를 표시하도록 선택할 수 있습니다. </p> <p><strong>참고</strong>:<em> 표시 옵션 <strong>의 경우</strong> 두 가지 옵션 <strong>이 아닌 옵션을</strong> 선택하면  <strong>기본</strong> Tabfield 옵션이 사용되지 않습니다.</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>기본 탭</td>
   <td>양식 포털 페이지가 로드될 때 표시할 탭을 지정합니다. <strong>초안 Forms 탭</strong>과 <strong>제출된 Forms 탭</strong> 중에서 선택할 수 있습니다.</td>
  </tr>
  <tr>
   <td>초안 Forms 탭 구성</td>
   <td>사용자 지정 제목</td>
   <td><strong>초안 Forms</strong> 탭의 제목을 지정합니다. 기본값은 <strong>초안 Forms입니다.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>레이아웃 템플릿</td>
   <td>초안 Forms 목록에 사용할 레이아웃을 지정합니다.</td>
  </tr>
  <tr>
   <td>제출된 Forms 탭 구성</td>
   <td>사용자 지정 제목 </td>
   <td><strong>제출된 Forms </strong> 탭의 제목을 지정합니다. 기본값은 <strong>제출된 Forms입니다.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>레이아웃 템플릿</td>
   <td>제출된 Forms<strong> </strong> 목록에 사용할 레이아웃을 지정합니다. </td>
  </tr>
 </tbody>
</table>

## {#customizing-the-storage} 저장소 사용자 지정

Forms 포털 제출 작업을 사용하거나 양식 포털에서 데이터 저장 옵션을 적응형 양식으로 활성화하면 양식 데이터가 AEM 저장소에 저장됩니다. 제작 환경에서는 초안 또는 제출된 양식 데이터를 AEM 저장소에 저장하지 않는 것이 좋습니다. 대신 초안 및 제출 구성 요소를 기업 데이터베이스와 같은 보안 스토리지와 통합하여 초안 및 제출된 양식 데이터를 저장해야 합니다.

Forms 포털을 통해 로컬 AEM 저장소, 원격 AEM 저장소 또는 데이터베이스에 데이터를 저장할 수 있습니다. AEM Forms을 사용하면 초안 및 제출용 사용자 데이터 저장 구현을 사용자 정의할 수 있습니다. 기본 방법을 무시하여 초안 및 제출 데이터가 원하는 저장 위치에 저장되는 방식을 지정할 수 있습니다. 예를 들어 조직에서 현재 구현된 데이터 저장소에 데이터를 저장할 수 있습니다.

Forms 포털은 로컬 및 원격 AEM Forms 게시 인스턴스의 crx-repository에 데이터를 저장하는 최신 API(서비스)를 제공합니다. 기본 기능을 대체할 사용자 지정 구현으로 [초안 및 제출](/help/forms/using/configuring-draft-submission-storage.md) 아티클에 대한 저장소 서비스 구성에 설명된 기본 구현을 바꿀 수 있습니다. 보안 위치에 컨텐츠를 저장하는 사용자 지정 구현에 필요한 방법에 대한 자세한 내용은 [초안 및 제출 데이터 서비스 사용자 지정](/help/forms/using/custom-draft-submission-data-services.md) 및 [초안 및 제출 구성 요소에 대한 사용자 지정 저장소를 참조하십시오.](/help/forms/using/adding-custom-storage-provider-forms.md)

AEM Forms 설명서는 초안 및 제출 구성 요소를 데이터베이스[와 통합하는 샘플을 제공합니다. ](integrate-draft-submission-database.md) 샘플 구현을 사용하여 사용자 지정 구현을 개발할 수 있습니다.

## 관련 문서

* [양식 포털 구성 요소 활성화](/help/forms/using/enabling-forms-portal-components.md)
* [양식 포털 페이지 만들기](/help/forms/using/creating-form-portal-page.md)
* [API를 사용하여 웹 페이지의 양식 목록 작성](/help/forms/using/listing-forms-webpage-using-apis.md)
* [초안 및 제출 구성 요소 사용](/help/forms/using/draft-submission-component.md)
* [초안 및 제출된 양식의 저장 사용자 정의](/help/forms/using/draft-submission-component.md)
* [초안 및 제출 구성 요소를 데이터베이스와 통합하는 샘플](/help/forms/using/integrate-draft-submission-database.md)
* [양식 포털 구성 요소에 대한 템플릿 사용자 정의](/help/forms/using/customizing-templates-forms-portal-components.md)
* [포털에서 양식 게시 소개](/help/forms/using/introduction-publishing-forms.md)
