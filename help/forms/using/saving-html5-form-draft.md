---
title: HTML5 양식을 초안으로 저장
seo-title: HTML5 양식을 초안으로 저장
description: HTML5 양식을 초안으로 저장하고 나중에 양식 작성을 다시 시작합니다.
seo-description: HTML5 양식을 초안으로 저장하고 나중에 양식 작성을 다시 시작합니다.
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 4%

---


# HTML5 양식을 초안 {#saving-an-html-form-as-a-draft}으로 저장

HTML5 양식을 초안으로 저장하고 나중에 양식 작성을 다시 시작할 수 있습니다. Forms Portal을 사용하면 모든 사용자가 HTML5 양식을 저장하고 복원할 수 있습니다. 초안으로 저장 기능을 활성화하려면 프로파일 노드에 다음 구성을 추가합니다.

## 초안으로 저장 기능 {#custom-profile-to-allow-save-as-draft-feature}을 허용하는 사용자 지정 프로필

기본적으로 AEM Forms은 **초안으로 저장** 프로파일을 제공합니다. 초안으로 저장 프로파일을 사용하여 양식을 렌더링하여 HTML5 양식에 초안 기능을 활성화할 수 있습니다. [Forms Manager](/help/forms/using/introduction-managing-forms.md)에서 양식의 HTML 렌더링 프로필을 지정할 수 있습니다.

기존 [사용자 지정 프로필](/help/forms/using/custom-profile.md)에 대해 초안으로 저장 기능을 활성화하려면 사용자 지정 프로필 노드에 다음 속성을 추가하십시오.

<table>
 <tbody>
  <tr>
   <td><strong>속성 이름</strong></td>
   <td><strong>유형</strong></td>
   <td><strong>값</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>mfAllowFPDraft</td>
   <td>문자열</td>
   <td>true</td>
   <td><p>초안 기능으로 저장</p> <p>을 참조하십시오.</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>문자열</td>
   <td>true</td>
   <td><p>첨부 파일 업로드 허용</p> <p>이 프로파일을 사용합니다.</p> </td>
  </tr>
 </tbody>
</table>

## 초안 저장 및 {#drafts-storage-and-listing} 나열

양식에 대해 초안으로 저장 기능을 활성화한 후;양식이 저장되면 [초안 및 제출 구성 요소](/help/forms/using/draft-submission-component.md)에 나열됩니다. 초안 및 제출 구성 요소에서 저장된 양식을 검색하고 채울 수 있습니다.

초안 및 제출 구성 요소에 대한 양식 목록을 활성화하려면 프로필 노드에 다음 속성을 추가하십시오.

<table>
 <tbody>
  <tr>
   <td><strong>속성 이름</strong></td>
   <td><strong>유형</strong></td>
   <td><strong>값</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>fp.enablePortalSubmit</td>
   <td>문자열</td>
   <td>true</td>
   <td>제출 후 초안 및 양식이<br /> Forms 포털 초안 및 제출 구성 요소에 나열되도록 하려면</td>
  </tr>
 </tbody>
</table>

기본적으로 AEM Forms은 양식 초안 및 제출과 연관된 사용자 데이터를 게시 인스턴스의 /content/forms/fp 노드에 저장합니다. 사용자 지정 저장소 공급자를 추가할 수 있습니다. 자세한 내용은 [초안 및 제출 구성 요소에 대한 사용자 지정 저장소](/help/forms/using/adding-custom-storage-provider-forms.md)를 참조하십시오.
