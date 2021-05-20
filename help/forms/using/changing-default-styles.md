---
title: HTML5 양식의 기본 스타일 변경
seo-title: HTML5 양식의 기본 스타일 변경
description: HTML5 양식 스타일은 CSS를 기반으로 합니다. 양식의 기본 스타일을 변경할 수 있습니다.
seo-description: HTML5 양식 스타일은 CSS를 기반으로 합니다. 양식의 기본 스타일을 변경할 수 있습니다.
uuid: 5e23237d-42d8-4d29-b79e-4dc276ef65ff
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 582b0fe8-a92b-4a1d-b859-57f13f53d0d8
docset: aem65
feature: Mobile Forms
exl-id: 4c84cfd1-50a4-416f-b4a5-7f2f4c7f10af
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---

# HTML5 양식의 기본 스타일 변경{#changing-default-styles-of-html-forms}

HTML5 양식이 HTML5 기능을 사용하여 렌더링되고 렌더링된 양식의 스타일은 CSS를 사용하여 수행됩니다. HTML5 양식의 기본 모양은 PDF 표현물과 비슷합니다. 개발자는 사용자 지정 CSS를 사용하여 HTML5 양식의 기본 모양을 변경할 수 있습니다.

이 문서에서는 HTML5 양식의 스타일을 변경하는 단계별 정보를 제공하며 [스타일 소개](/help/forms/using/css-styles.md) 문서에는 HTML5 양식의 다양한 스타일 측면에 대한 자세한 정보가 포함되어 있습니다. 이 문서에서 언급된 단계를 수행하기 전에 스타일 소개 문서를 읽어야 합니다.

다음 두 이미지는 기본 스타일과 사용자 지정된 스타일 간의 차이를 보여줍니다.

![사진-002-소형](assets/pictures-002-small.png)

## 양식 스타일 {#style-your-forms}

1. **사용자 지정 스타일을 추가할 프로필 선택**

   URL에서 CRX DE 인터페이스에 액세스합니다.**https://&lt;server>:&lt;port>/crx/de** 프로필을 만들고 기존 프로필을 선택합니다. 프로필을 만드는 방법을 알아보려면 [새 프로필 만들기](/help/forms/using/custom-profile.md)를 참조하십시오

1. **HTML5 양식의 스타일을 지정할 CSS 스타일 시트 만들기**

   프로필 렌더러를 만든 폴더로 이동하고 CSS 스타일 시트 파일을 만듭니다. 다음 단계를 수행합니다

   1. 폴더를 마우스 오른쪽 단추로 클릭하고 메뉴에서 **만들기** > **파일 만들기**&#x200B;를 선택합니다

   1. 파일 만들기 대화 상자에서 스타일 시트 이름을 입력합니다. 확장 .css(예: stylesheet.css)를 사용해야 합니다
   1. 탐색 창에서 만든 CSS 파일을 엽니다.
   1. 스타일을 지정할 구성 요소의 CSS 클래스를 정의하고 해당 클래스에 스타일을 추가합니다.

   HTML5 양식에서 특정 구성 요소에 대해 만들 CSS 클래스를 알려면 [스타일 소개](/help/forms/using/css-styles.md)를 참조하십시오.

1. **프로필 렌더러에 스타일 시트 포함**

   CRX DE에서 프로필 렌더러 페이지(jsp 파일)를 열고 XFA 클라이언트 라이브러리 바로 아래에 있는 페이지에 CSS 파일을 포함합니다. 프로필에 CSS 파일을 포함하려면 다음 단계를 수행합니다.

   1. 렌더러 페이지에서 다음 줄을 검색합니다.

      &lt;cq:includeclientlib categories=&quot;xfaforms.profile&quot; />

   1. 스타일 시트를 포함하려면 위의 줄 아래에 다음 내용을 삽입합니다.

      &lt;link href=&quot;/path/to/stylesheet&quot; rel=&quot;stylesheet&quot; type=&quot;text/css&quot; />

   1. 파일을 저장합니다.
