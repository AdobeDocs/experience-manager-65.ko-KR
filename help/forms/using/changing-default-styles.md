---
title: HTML5 양식의 기본 스타일 변경
seo-title: HTML5 양식의 기본 스타일 변경
description: HTML5 양식 스타일링은 CSS를 기반으로 합니다. 양식의 기본 스타일을 변경할 수 있습니다.
seo-description: HTML5 양식 스타일링은 CSS를 기반으로 합니다. 양식의 기본 스타일을 변경할 수 있습니다.
uuid: 5e23237d-42d8-4d29-b79e-4dc276ef65ff
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 582b0fe8-a92b-4a1d-b859-57f13f53d0d8
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# HTML5 양식의 기본 스타일 변경{#changing-default-styles-of-html-forms}

HTML5 양식은 HTML5 기능을 사용하여 렌더링되고 렌더링된 양식의 스타일이 CSS를 사용하여 수행됩니다. HTML5 양식의 기본 모양은 PDF 변환과 유사합니다. 개발자는 맞춤형 CSS를 사용하여 HTML5 양식의 기본 모양을 변경할 수 있습니다.

이 문서에서는 HTML5 양식의 스타일을 변경하는 단계별 정보를 제공하며 [스타일 소개](/help/forms/using/css-styles.md) 아티클에는 HTML5 양식의 다양한 스타일 측면에 대한 자세한 정보가 포함되어 있습니다. 이 아티클에 언급된 단계를 수행하기 전에 스타일 소개 아티클을 읽어야 합니다.

다음 두 이미지는 기본 스타일과 사용자 지정된 스타일의 차이를 보여 줍니다.

![pictures-002-small](assets/pictures-002-small.png)

## 양식 스타일 지정 {#style-your-forms}

1. **사용자 정의 스타일을 추가할 프로필 선택**

   URL에서 CRX DE 인터페이스에 액세스합니다.**https://&lt;server>:&lt;port>/crx/de** 프로파일을 만들고 프로파일을 만들거나 기존 프로파일을 선택합니다. 프로필을 만드는 방법을 알아보려면 [새 프로필 만들기](/help/forms/using/custom-profile.md)를 참조하십시오.

1. **HTML5 양식 스타일을 지정할 CSS 스타일 시트 만들기**

   프로필 렌더러를 만든 폴더로 이동하여 CSS 스타일 시트 파일을 만듭니다. 다음 단계를 수행합니다.

   1. 폴더를 마우스 오른쪽 단추로 클릭하고 메뉴에서 **만들기** > **파일 만들기**&#x200B;를 선택합니다.

   1. 파일 만들기 대화 상자에서 스타일 시트 이름을 입력합니다. 확장명 .css를 사용해야 합니다(예: stylesheet.css).
   1. 탐색 창에서 만든 CSS 파일을 엽니다.
   1. 스타일을 지정하고 해당 클래스에 스타일을 추가할 구성 요소의 CSS 클래스를 정의합니다.

   HTML5 양식의 특정 구성 요소에 대해 만들 CSS 클래스를 알아보려면 [스타일 소개](/help/forms/using/css-styles.md)을 참조하십시오.

1. **프로필 렌더러에 스타일 시트 포함**

   CRX DE에서 프로필 렌더러 페이지(jsp 파일)를 열고 XFA 클라이언트 라이브러리 바로 아래의 페이지에 CSS 파일을 포함합니다. 프로파일에 CSS 파일을 포함하려면 다음 단계를 수행합니다.

   1. 렌더러 페이지에서 다음 줄을 검색합니다.

      &lt;cq:includeclientlib categories=&quot;xfaforms.profile&quot; />

   1. 스타일 시트를 포함하려면 위의 줄 아래에 다음을 삽입합니다.

      &lt;link href=&quot;/path/to/stylesheet&quot; rel=&quot;stylesheet&quot; type=&quot;text/css&quot; />

   1. 파일을 저장합니다.
