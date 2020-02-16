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

---


# 초안 및 제출 구성 요소{#drafts-and-submissions-component}

초안 및 제출 구성 요소는 초안 상태에 있는 모든 양식과 이미 제출된 양식을 나열합니다. 구성 요소에는 초안 및 제출된 양식에 대한 별도의 섹션(탭)이 있습니다. 사용자는 자신의 초안과 제출된 양식만 볼 수 있습니다.

## 구성 요소 구성 {#configuring-the-component}

초안 및 제출 구성 요소에는 두 개의 탭이 있습니다.초안 및 제출.

적응형 양식을 제출 탭에 표시하려면 제출 작업을 **양식 포털 제출** 동작으로 **[설정합니다](../../forms/using/configuring-submit-actions.md). 또는&#x200B;**Forms 포털 제출 옵션을 활성화합니다. 사용자가 양식을 제출할 때마다 양식이 제출 탭에 추가됩니다.

초안 기능은 즉시 사용할 수 있습니다. 사용자가 적응형 **양식에서** 저장을 클릭하면 양식이 초안 탭에 추가됩니다.

초안 및 제출 구성 요소를 추가하고 구성하려면 다음 단계를 수행하십시오.

1. 초안 및 제출 **구성 요소를** 페이지의 구성 요소 브라우저에서 문서 서비스 범주 아래에 드래그하여 놓습니다.
1. 구성 요소를 누른 다음 ![settings_icon](assets/settings_icon.png) 을 탭하여 구성 요소에 대한 편집 대화 상자를 엽니다.

   ![초안 및 제출 구성 요소](assets/drafts-submissions-edit.png)

1. 편집 대화 상자에서 다음 세부 사항을 지정하고 완료를 **눌러** 설정을 저장합니다.

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
   <td>표시할 최대 결과 수를 지정합니다. 결과 수가 전체 결과 제한을 늘리면 추가 <strong>링크가 구성 요소 </strong>하단에 나타납니다. [ <strong>자세히]를 </strong>클릭하면 모든 양식이 표시됩니다. </td>
  </tr>
  <tr>
   <td> </td>
   <td>스타일 유형</td>
   <td>구성 요소의 스타일을 지정합니다. 양식을 나열할 <strong>스타일 없음</strong>, <strong>기본 스타일</strong>또는 <strong>사용자</strong> 지정 스타일을 지정할수 있습니다. 사용자 지정 스타일 옵션의 경우 사용자 지정 스타일 경로 <strong>필드에서 </strong><strong>사용자 지정 CSS 파일의 경로를 지정할 수 있습니다.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>사용자 지정 스타일 경로</td>
   <td>스타일 유형 <strong>필드에서 사용자</strong> 지정 스타일 <strong></strong> 옵션을 선택한 경우 <strong>사용자 지정 스타일 경로</strong> 필드를 사용하여 사용자 지정 CSS 파일의경로를 지정합니다. </td>
  </tr>
  <tr>
   <td> </td>
   <td>표시 옵션</td>
   <td><p>표시할 탭을 지정합니다. 초안 양식, 제출된 양식 또는 두 가지 모두를 표시하도록 선택할 수 있습니다. </p> <p><strong></strong> 참고<em>:표시 <strong>옵션의</strong>경우 둘 다 이외의 옵션을 <strong>선택하면</strong>기본 <strong>탭</strong> 필드 옵션이사용되지 않습니다.</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>기본 탭</td>
   <td>양식 포털 페이지가 로드될 때 표시할 탭을 지정합니다. 초안 양식 탭과 <strong>제출된 양식 탭</strong> 중에서 선택할 <strong>수 있습니다</strong>.</td>
  </tr>
  <tr>
   <td>초안 양식 탭 구성</td>
   <td>사용자 정의 제목</td>
   <td>초안 양식 <strong>탭의 제목을</strong> 지정합니다. 기본값은 초안 <strong>양식입니다.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>레이아웃 템플릿</td>
   <td>초안 양식 목록에 사용할 레이아웃을 지정합니다.</td>
  </tr>
  <tr>
   <td>제출된 양식 탭 구성</td>
   <td>사용자 정의 제목 </td>
   <td>제출된 양식 <strong></strong>탭의 제목을 지정합니다. 기본값은 제출된 <strong>양식입니다.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>레이아웃 템플릿</td>
   <td>제출된 양식<strong> 목록에 사용할 레이아웃을 지정합니다 </strong>. </td>
  </tr>
 </tbody>
</table>

## 스토리지 사용자 정의 {#customizing-the-storage}

Forms Portal 제출 작업을 사용하거나 적응형 양식의 양식 포털에 데이터 저장 옵션을 활성화하면 양식 데이터가 AEM 저장소에 저장됩니다. 제작 환경에서는 초안 또는 제출된 양식 데이터를 AEM 저장소에 저장하지 않는 것이 좋습니다. 대신 초안 및 제출 구성 요소를 엔터프라이즈 데이터베이스와 같은 보안 스토리지와 통합하여 초안 및 제출된 양식 데이터를 저장해야 합니다.

양식 포털을 통해 로컬 AEM 저장소, 원격 AEM 저장소 또는 데이터베이스에 데이터를 저장할 수 있습니다. AEM Forms를 사용하면 초안 및 제출용 사용자 데이터 저장 구현을 사용자 지정할 수 있습니다. 기본 방법을 무시하여 초안 및 제출 데이터가 원하는 저장소에 저장되는 방식을 지정할 수 있습니다. 예를 들어 현재 조직에 구현된 데이터 저장소에 데이터를 저장할 수 있습니다.

양식 포털은 로컬 및 원격 AEM Forms 게시 인스턴스의 crx-repository에 데이터를 저장하는 즉시 사용 가능한 API(서비스)를 제공합니다. 초안 및 제출 [](/help/forms/using/configuring-draft-submission-storage.md) 문서에 대한 스토리지 서비스 구성에 설명된 기본 구현을 기본 기능을 대체할 수 있는 사용자 지정 구현으로 대체할 수 있습니다. 보안 위치에 컨텐츠를 저장하는 사용자 정의 구현에 필요한 방법에 대한 자세한 내용은 초안 및 제출 [데이터 서비스](/help/forms/using/custom-draft-submission-data-services.md) 사용자 정의 및 초안 및 제출 [구성 요소에 대한 사용자 정의스토리지를 참조하십시오.](/help/forms/using/adding-custom-storage-provider-forms.md)

AEM Forms 설명서는 초안 및 제출 [구성 요소를 데이터베이스와](integrate-draft-submission-database.md)통합하기 위한 샘플을 제공합니다. 샘플 구현을 사용하여 사용자 지정 구현을 개발할 수 있습니다.

## 관련 문서

* [양식 포털 구성 요소 활성화](/help/forms/using/enabling-forms-portal-components.md)
* [양식 포털 페이지 만들기](/help/forms/using/creating-form-portal-page.md)
* [API를 사용하여 웹 페이지의 양식 목록 작성](/help/forms/using/listing-forms-webpage-using-apis.md)
* [초안 및 제출 구성 요소 사용](/help/forms/using/draft-submission-component.md)
* [초안 및 제출된 양식 저장 사용자 정의](/help/forms/using/draft-submission-component.md)
* [초안 및 제출 구성 요소를 데이터베이스와 통합하는 샘플](/help/forms/using/integrate-draft-submission-database.md)
* [양식 포털 구성 요소에 대한 템플릿 사용자 정의](/help/forms/using/customizing-templates-forms-portal-components.md)
* [포털에서 양식 게시 소개](/help/forms/using/introduction-publishing-forms.md)
