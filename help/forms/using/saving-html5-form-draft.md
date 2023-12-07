---
title: HTML5 양식을 초안으로 저장
description: HTML5 양식을 초안으로 저장하고 이후 단계에서 양식 채우기를 재개합니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
feature: Mobile Forms
exl-id: a9879445-d626-4279-8a95-a9009294b483
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 5%

---

# HTML5 양식을 초안으로 저장 {#saving-an-html-form-as-a-draft}

HTML5 양식을 초안으로 저장하고 나중에 양식 채우기를 다시 시작할 수 있습니다. Forms 포털을 사용하면 모든 사용자가 HTML5 양식을 저장하고 복원할 수 있습니다. 초안으로 저장 기능을 활성화하려면 프로필 노드에 다음 구성을 추가합니다.

## 초안으로 저장 기능을 허용하는 사용자 지정 프로필 {#custom-profile-to-allow-save-as-draft-feature}

기본 제공되는 AEM Forms은 **초안으로 저장** 프로필. 초안으로 저장 프로필이 있는 양식을 렌더링하여 HTML5 양식에 대한 초안 기능을 활성화할 수 있습니다. 다음 위치에서 양식에 대한 HTML 렌더링 프로필을 지정할 수 있습니다. [Forms Manager](/help/forms/using/introduction-managing-forms.md).

기존 항목에 대해 초안으로 저장 기능을 활성화하려면 [사용자 지정 프로필](/help/forms/using/custom-profile.md)를 클릭하고 사용자 지정 프로필 노드에 다음 속성을 추가합니다.

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
   <td><p>초안으로 저장 기능 활성화</p> <p>이 프로필에 대해 설명합니다.</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>문자열</td>
   <td>true</td>
   <td><p>첨부 파일 업로드 허용</p> <p>이 프로필로.</p> </td>
  </tr>
 </tbody>
</table>

## 초안 저장 및 나열 {#drafts-storage-and-listing}

양식에 대해 초안으로 저장 기능을 활성화한 후 양식을 저장하면 [초안 및 제출 구성 요소](/help/forms/using/draft-submission-component.md). 초안 및 제출 구성 요소에서 저장된 양식을 읽어들이고 채우기를 시작할 수 있습니다.

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
   <td>초안과 양식을 나열할 수 있도록 하려면<br /> 제출 후 Forms 포털 초안 및 제출 구성 요소</td>
  </tr>
 </tbody>
</table>

기본적으로 AEM Forms은 양식 초안 및 제출과 관련된 사용자 데이터를 게시 인스턴스의 /content/forms/fp 노드에 저장합니다. 사용자 정의 스토리지 공급자를 추가할 수 있습니다. 자세한 내용은 [초안 및 제출 구성 요소에 대한 사용자 지정 저장소](/help/forms/using/adding-custom-storage-provider-forms.md).
