---
title: HTML5 양식에 대한 첨부 파일 활성화
seo-title: HTML5 양식에 대한 첨부 파일 활성화
description: 기본적으로 HTML5 양식에 대한 첨부 파일은 비활성화됩니다.
seo-description: 기본적으로 HTML5 양식에 대한 첨부 파일은 비활성화됩니다.
uuid: 2c62ac3e-4b27-46c7-a61d-a805fb5d26fb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
feature: Mobile Forms
exl-id: 68912260-179a-4d1b-b944-0a1777c021ac
source-git-commit: 6e2a0f053a1f6989524e9ae2b1dcb001b0397ac6
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---

# HTML5 양식에 대한 첨부 파일 활성화 {#enabling-attachments-for-an-html-form}

HTML5 양식을 사용하여 첨부 파일을 업로드, 미리 보기 및 제출할 수 있습니다. 기본적으로 첨부 파일 지원은 비활성화됩니다. 첨부 지원을 사용하려면

1. `mfAttachmentOptions` 다중 선택 문자열 속성을 사용하여 [사용자 지정 프로필](/help/forms/using/custom-profile.md)을 만듭니다. 첨부 파일 위젯의 옵션을 구성하려면 `mfAttachmentOptions` 속성의 각 문자열에 `property=value` 형식이 있어야 합니다. `property` 및 `value` 값은 다음 값 중 하나를 가질 수 있습니다.

   | 속성 | 값 |
   |--- |---|
   | multiSelect | true 또는 false(기본적으로 true) |
   | fileSizeLimit | MB 수(기본적으로 2MB). 예, 5. |
   | buttonText | 팝업 창의 단추 텍스트(기본적으로 &quot;첨부&quot;) |
   | 동의 | 사용할 파일 형식의 쉼표로 구분된 목록(&quot;audio/&amp;ast;, 비디오/&amp;ast;, 이미지/&amp;ast;, 텍스트/amp;ast;, .pdf&quot; 기본적으로) |

   예:

   ![옵션 구성](assets/mfAttachmentOptions.png)

   필요에 따라 `mfAttachmentOptions` 속성에 대해 사용자 지정 옵션을 더 지정할 수도 있습니다.

   >[!NOTE]
   >
   >Microsoft Internet Explorer 9에서는 사용자가 지정된 제한보다 큰 파일을 첨부할 수 있습니다. 알려진 문제입니다.

1. [메타데이터 편집기](/help/forms/using/manage-form-metadata.md)를 사용하여 HTML5 양식에 대해 위에서 만든 사용자 지정 프로필을 선택합니다.
1. 사용자 지정 프로필로 양식 템플릿을 렌더링하고 첨부 파일 아이콘이 양식 도구 모음에 표시됩니다.

   >[!NOTE]
   >
   >곧바로 사용할 수 있는 양식 포털은 초안 및 첨부 파일 기능이 활성화된 사용자 지정 프로필을 제공합니다. **초안으로 저장** 프로필에 대한 자세한 내용은 [HTML5 양식을 초안](/help/forms/using/saving-html5-form-draft.md)으로 저장 을 참조하십시오.

1. 첨부 아이콘 을 클릭하면 첨부 선택 대화 상자가 나타납니다. 첨부 파일을 찾아 선택하고 **첨부**&#x200B;를 클릭합니다.

   >[!NOTE]
   >
   >첨부 파일을 미리 보려면 첨부 파일 이름을 클릭합니다.

   >[!NOTE]
   >
   >익명 사용자는 파일 미리 보기 옵션을 사용할 수 없습니다.

## 첨부 파일 제출 형식 {#attachment-submission-format}

첨부 파일이 활성화되면 HTML5 양식이 다중 부분 데이터를 제출합니다. 다중 부분 제출 데이터에는 **dataXml** 및 **첨부 파일**&#x200B;이 두 개 있습니다.

>[!NOTE]
>
>이전 버전과의 호환성을 위해 `mfAllowAttachments` 옵션이 꺼져 있으면 HTML5 양식에서 다중 부분 데이터를 전송하지 않습니다. 단순 데이터 xml을 **application/xml** 형식으로 보냅니다.

mfAllowAttachments 플래그가 설정되어 있으면 [제출 서비스 프록시 서비스](/help/forms/using/service-proxy.md)에서 dataXml 및 첨부 파일이 있는 다중 부분 데이터도 게시합니다.
