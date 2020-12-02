---
title: HTML5 양식에 대한 첨부 파일 활성화
seo-title: HTML5 양식에 대한 첨부 파일 활성화
description: 기본적으로 HTML5 양식에 대한 첨부 기능은 비활성화됩니다.
seo-description: 기본적으로 HTML5 양식에 대한 첨부 기능은 비활성화됩니다.
uuid: 2c62ac3e-4b27-46c7-a61d-a805fb5d26fb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
translation-type: tm+mt
source-git-commit: 00e14be8a0775149b3ee7ce8cd781dd7f1e49e4f
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---


# HTML5 양식 {#enabling-attachments-for-an-html-form}에 대한 첨부 파일 활성화

HTML5 양식을 사용하여 첨부 파일을 업로드, 미리 보기 및 제출할 수 있습니다. 기본적으로 첨부 파일 지원은 비활성화됩니다. 첨부 지원을 활성화하려면

1. 다중 선택 문자열 속성 `mfAttachmentOptions`으로 [사용자 지정 프로필](/help/forms/using/custom-profile.md)을 만듭니다.
1. 사용자 지정 프로필에서 속성 `fileSizeLimit`, `multiSelect` 및 `buttonTex`t를 지정하여 파일 첨부 위젯의 옵션을 구성합니다. 필요에 따라 사용자 지정 속성을 더 지정할 수도 있습니다.

1. 사용자 지정 프로필에서 다음 구성을 사용합니다.

   * **multiSelect** -> true 또는 false(기본적으로 true)
   * **fileSizeLimit** -> value_in_mb(say 5)(기본적으로 2MB)
   * **buttonText** -> 팝업 창의 단추 텍스트(기본적으로 &quot;첨부&quot;)
   * **accept** -> file type to accept (&quot;audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf&quot; by default)

   >[!NOTE]
   >
   >Microsoft Internet Explorer 9에서는 사용자가 지정한 제한보다 큰 파일을 첨부할 수 있습니다. 알려진 문제입니다.

1. [메타데이터 편집기](/help/forms/using/manage-form-metadata.md)를 사용하여 HTML 5 양식에 대해 위에서 만든 사용자 지정 프로필을 선택합니다.
1. 양식 템플릿을 사용자 정의 프로필로 렌더링하면 첨부 파일 아이콘이 양식 도구 모음에 나타납니다.

   >[!NOTE]
   >
   >기본적으로 양식 포털은 초안 및 첨부 기능이 활성화된 사용자 정의 프로파일을 제공합니다. **Save as Draft** 프로필에 대한 자세한 내용은 [HTML5 양식을 초안](/help/forms/using/saving-html5-form-draft.md)으로 저장을 참조하십시오.

1. 첨부 아이콘을 클릭하면 첨부 선택 대화 상자가 나타납니다. 첨부 파일을 찾아 선택하고 **첨부**&#x200B;를 클릭합니다.

   >[!NOTE]
   >
   >첨부 파일을 미리 보려면 첨부 파일 이름을 클릭합니다.

   >[!NOTE]
   >
   >익명의 사용자는 파일 미리 보기 옵션을 사용할 수 없습니다.

## 첨부 파일 제출 형식 {#attachment-submission-format}

첨부 파일이 활성화되면 HTML5 양식이 여러 부분으로 구성된 데이터를 제출합니다. 다중 부분 제출 데이터에는 두 개의 부분 **dataXml**&#x200B;과 **첨부 파일**&#x200B;이 있습니다.

>[!NOTE]
>
>이전 버전과의 호환성을 위해 `mfAllowAttachments` 옵션이 꺼져 있는 경우 HTML5 양식에서 다중 부분 데이터를 보내지 않습니다. 단순 데이터 xml을 **application/xml** 형식으로 전송합니다.

mfAllowAttachments 플래그가 켜진 경우 [제출 서비스 프록시 서비스](/help/forms/using/service-proxy.md)도 dataXml 및 첨부 파일이 있는 여러 파트 데이터도 게시합니다.
