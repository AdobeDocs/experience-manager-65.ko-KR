---
title: HTML5 양식의 기본 스타일 변경
description: HTML5 양식 스타일은 CSS를 기반으로 합니다. 폼의 기본 스타일을 변경할 수 있습니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms
exl-id: 4c84cfd1-50a4-416f-b4a5-7f2f4c7f10af
source-git-commit: 524475c8f9dbd02bae30ecd558a376505fbe0aed
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# HTML5 양식의 기본 스타일 변경{#changing-default-styles-of-html-forms}

HTML5 양식은 HTML5 기능을 사용하여 렌더링되며 렌더링된 양식의 스타일링은 CSS를 사용하여 수행됩니다. HTML5 양식의 기본 모양은 PDF 렌디션과 유사합니다. 개발자는 사용자 지정 CSS를 사용하여 HTML 5 양식의 기본 모양을 변경할 수 있습니다.

이 문서에서는 HTML5 양식의 스타일을 변경하는 단계별 정보를 제공합니다. [스타일 소개](/help/forms/using/css-styles.md) 이 문서에는 HTML 5 양식의 다양한 스타일링 측면에 대한 자세한 정보가 포함되어 있습니다. 이 문서에 언급된 단계를 수행하기 전에 스타일 소개 문서를 읽어야 합니다.

다음 두 이미지는 기본 스타일과 사용자 지정된 스타일 간의 차이점을 보여 줍니다.

![pictures-002-small](assets/pictures-002-small.png)

## 양식 스타일 지정 {#style-your-forms}

1. **사용자 정의 스타일을 추가할 프로필 선택**

   다음 URL에서 CRX DE 인터페이스에 액세스합니다. **https://&lt;server>:&lt;port>/crx/de** 프로파일을 만들거나 기존 프로파일을 선택합니다. 프로필을 만드는 방법을 알아보려면 다음을 참조하십시오. [프로필 만들기](/help/forms/using/custom-profile.md)

1. **HTML5 양식의 스타일을 지정하는 CSS 스타일 시트 만들기**

   프로필 렌더러를 만든 폴더로 이동하고 CSS 스타일 시트 파일을 만듭니다. 따라야 할 단계는 다음과 같습니다

   1. 폴더를 마우스 오른쪽 단추로 클릭하고 **만들기** > **파일 만들기** 메뉴에서

   1. 파일 생성 대화 상자에서 스타일 시트의 이름을 입력합니다. 확장자 .css(예: stylesheet.css)를 사용해야 합니다
   1. 탐색 창에서 만든 CSS 파일을 엽니다.
   1. 스타일을 지정할 구성 요소의 CSS 클래스를 정의하고 해당 클래스에 스타일을 추가합니다.

   HTML5 양식의 특정 구성 요소에 대해 만들 CSS 클래스를 알아보려면 다음을 참조하십시오. [스타일 소개](/help/forms/using/css-styles.md).

1. **프로필 렌더러에 스타일 시트 포함**

   CRX DE에서 프로필 렌더러 페이지(jsp 파일)를 열고 CSS 파일을 XFA 클라이언트 라이브러리 바로 아래의 페이지에 포함합니다. 프로필에 CSS 파일을 포함하려면 다음 단계를 수행하십시오.

   1. 렌더러 페이지에서 다음 행을 검색합니다.

      &lt;cq:includeClientLib categories=&quot;xfaforms.profile&quot; />

   1. 스타일 시트를 포함하려면 위의 선 아래에 다음 내용을 삽입합니다.

      &lt;link href=&quot;/path/to/stylesheet&quot; rel=&quot;stylesheet&quot; type=&quot;text/css&quot;/>

   1. 파일을 저장합니다.
