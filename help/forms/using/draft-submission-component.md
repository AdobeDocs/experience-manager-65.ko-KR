---
title: 초안 및 제출 구성 요소
description: 초안 및 제출 구성 요소는 초안 상태이며 이미 제출된 양식을 나열합니다. 구성 요소의 모양과 스타일을 사용자 지정할 수 있습니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: f3f013a7-a399-4178-a901-d4a8c65ddbd3
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---

# 초안 및 제출 구성 요소{#drafts-and-submissions-component}

초안 및 제출 구성 요소에는 초안 상태에 있는 모든 양식과 이미 제출된 양식이 나열됩니다. 구성 요소에는 초안과 제출된 양식에 대한 별도의 섹션(탭)이 있습니다. 사용자는 자신의 초안과 제출된 양식만 볼 수 있습니다.

## 구성 요소 구성 {#configuring-the-component}

초안 및 제출 구성 요소에는 초안과 제출의 두 가지 탭이 있습니다.

적응형 양식 제출이 제출 탭에 표시되도록 하려면 다음을 설정하십시오. **제출 액션** 끝 **[Forms 포털 제출 액션](../../forms/using/configuring-submit-actions.md). 또는** Forms 포털 제출 옵션을 활성화합니다. 사용자가 양식을 제출할 때마다 제출 탭에 양식이 추가됩니다.

초안 기능은 즉시 활성화됩니다. 사용자가 클릭할 때 **저장** 적응형 양식에서 양식이 초안 탭에 추가됩니다.

초안 및 제출 구성 요소를 추가하고 구성하려면 다음 단계를 수행하십시오.

1. 을(를) 드래그 앤 드롭합니다 **초안 및 제출** 구성 요소 브라우저의 문서 서비스 카테고리 아래에 있는 구성 요소를 페이지에 연결합니다.
1. 구성 요소를 선택한 다음 를 선택합니다 ![settings_icon](assets/settings_icon.png) 구성 요소의 편집 대화 상자를 엽니다.

   ![초안 및 제출 구성 요소](assets/drafts-submissions-edit.png)

1. 편집 대화 상자에서 다음 세부 정보를 지정하고 을 선택합니다 **완료** 설정을 저장합니다.

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
   <td>표시할 최대 결과 수를 지정합니다. 결과 수가 총 결과 제한을 증가시키는 경우 <strong>자세히 </strong>링크가 구성 요소의 하단에 나타납니다. 클릭 <strong>자세히 </strong>모든 양식을 표시합니다. </td>
  </tr>
  <tr>
   <td> </td>
   <td>스타일 유형</td>
   <td>구성 요소의 스타일을 지정합니다. 다음을 지정할 수 있습니다. <strong>스타일 없음</strong>, <strong>기본 스타일</strong>, 또는 <strong>사용자 정의 스타일</strong> 양식 목록을 만드는 경우. [사용자 지정 스타일] 옵션의 경우 <strong>사용자 지정 스타일 경로 </strong>필드<strong>.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>사용자 지정 스타일 경로</td>
   <td>다음을 선택하는 경우 <strong>사용자 정의 스타일</strong> 의 옵션 <strong>스타일 유형</strong> 필드, 사용 <strong>사용자 지정 스타일 경로</strong> 사용자 지정 CSS 파일의 경로를 지정하는 필드입니다. </td>
  </tr>
  <tr>
   <td> </td>
   <td>표시 옵션</td>
   <td><p>표시할 탭을 지정합니다. 초안 양식, 제출된 양식 또는 둘 다를 표시하도록 선택할 수 있습니다. </p> <p><strong>참고</strong>:<em> 대상 <strong>옵션 표시</strong>, 이외의 옵션을 선택하는 경우 <strong>모두</strong>, <strong>기본 탭</strong> 필드 옵션은 사용되지 않습니다.</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>기본 탭</td>
   <td>Forms 포털 페이지가 로드될 때 표시할 탭을 지정합니다. 다음 중 하나를 선택할 수 있습니다. <strong>초안 Forms 탭</strong> 및 <strong>제출된 Forms 탭</strong>.</td>
  </tr>
  <tr>
   <td>초안 Forms 탭 구성</td>
   <td>사용자 정의 제목</td>
   <td>제목 지정 <strong>초안 Forms</strong> 탭. 기본값은 입니다. <strong>초안 Forms.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>레이아웃 템플릿</td>
   <td>초안 Forms 목록에 사용할 레이아웃을 지정합니다.</td>
  </tr>
  <tr>
   <td>제출된 Forms 탭 구성</td>
   <td>사용자 정의 제목 </td>
   <td>제목 지정 <strong>제출된 Forms </strong>탭. 기본값은 입니다. <strong>Forms을 제출했습니다.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>레이아웃 템플릿</td>
   <td>제출된 Forms에 사용할 레이아웃을 지정합니다.<strong> </strong>목록을 표시합니다. </td>
  </tr>
 </tbody>
</table>

## 스토리지 사용자 정의 {#customizing-the-storage}

Forms 포털 제출 액션을 사용하거나 적응형 양식에서 Forms 포털에 데이터 저장 옵션을 활성화하면 양식 데이터가 AEM 저장소에 저장됩니다. 프로덕션 환경에서는 초안 또는 제출된 양식 데이터를 AEM 저장소에 저장하지 않는 것이 좋습니다. 대신 초안 및 제출 구성 요소를 엔터프라이즈 데이터베이스와 같은 보안 저장소와 통합하여 초안 및 제출된 양식 데이터를 저장해야 합니다.

Forms 포털을 사용하면 로컬 AEM 저장소, 원격 AEM 저장소 또는 데이터베이스에 데이터를 저장할 수 있습니다. AEM Forms을 사용하면 초안 및 제출에 대한 사용자 데이터 저장 구현을 사용자 지정할 수 있습니다. 기본 메서드를 재정의하여 초안 및 제출 데이터가 선택한 저장소에 저장되는 방법을 지정할 수 있습니다. 예를 들어 조직에 현재 구현된 데이터 저장소에 데이터를 저장할 수 있습니다.

Forms 포털은 로컬 및 원격 AEM Forms 게시 인스턴스의 crx-repository에 데이터를 저장하는 기본 서비스(API)를 제공합니다. 에 설명된 대로 기본 구현을 바꿀 수 있습니다. [초안 및 제출을 위한 스토리지 서비스 구성](/help/forms/using/configuring-draft-submission-storage.md) 기본 기능을 대체할 사용자 지정 구현과 함께 제공되는 문서입니다. 보안 위치에 콘텐츠를 저장하기 위해 사용자 지정 구현에 필요한 방법에 대한 자세한 내용은 을 참조하십시오. [초안 및 제출 데이터 서비스 사용자 정의](/help/forms/using/custom-draft-submission-data-services.md) 및 [초안 및 제출 구성 요소에 대한 사용자 지정 저장소입니다.](/help/forms/using/adding-custom-storage-provider-forms.md)

AEM Forms 설명서는 다음을 제공합니다 [초안 및 제출 구성 요소와 데이터베이스를 통합하기 위한 샘플](integrate-draft-submission-database.md). 샘플 구현을 사용하여 사용자 지정 구현을 개발할 수 있습니다.

## 관련 문서

* [Forms 포털 구성 요소 활성화](/help/forms/using/enabling-forms-portal-components.md)
* [Forms 포털 페이지 만들기](/help/forms/using/creating-form-portal-page.md)
* [API를 사용하여 웹 페이지의 목록 양식](/help/forms/using/listing-forms-webpage-using-apis.md)
* [초안 및 제출 구성 요소 사용](/help/forms/using/draft-submission-component.md)
* [초안 및 제출된 양식의 스토리지 사용자 지정](/help/forms/using/draft-submission-component.md)
* [초안 및 제출 구성 요소와 데이터베이스를 통합하기 위한 샘플](/help/forms/using/integrate-draft-submission-database.md)
* [Forms 포털 구성 요소에 대한 템플릿 맞춤화](/help/forms/using/customizing-templates-forms-portal-components.md)
* [포털에 양식 게시 소개](/help/forms/using/introduction-publishing-forms.md)
