---
title: Markdown
seo-title: Markdown
description: 작성 시 컨텐츠 조각 편집기는 마크다운 구문을 사용하여 컨텐츠를 쉽게 작성할 수 있도록 합니다.
seo-description: 작성 시 컨텐츠 조각 편집기는 마크다운 구문을 사용하여 컨텐츠를 쉽게 작성할 수 있도록 합니다.
uuid: afcbf82f-3a75-4491-9172-706188db65bb
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: b193f28c-46c2-4eab-bbb8-578530f80ba5
docset: aem65
translation-type: tm+mt
source-git-commit: afed13a2f832b91d0df825d1075852cc84443646
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 4%

---


# Markdown{#markdown}

작성 [](content-fragments-variations.md#authoring-your-content)시 컨텐츠 조각 편집기는 *마크다운* 구문을 사용하여 컨텐츠를 쉽게 작성할 수 있도록 합니다.

![마크다운 편집기](/help/assets/content-fragments/assets/cfm-6420-08.png)

다음을 정의할 수 있습니다.

* [제목 표기법](/help/assets/content-fragments/content-fragments-markdown.md#heading-notation)
* [단락 및 줄 바꿈](/help/assets/content-fragments/content-fragments-markdown.md#paragraphs-and-line-breaks)
* [링크](/help/assets/content-fragments/content-fragments-markdown.md#links)
* [이미지](/help/assets/content-fragments/content-fragments-markdown.md#images)
* [따옴표 차단](/help/assets/content-fragments/content-fragments-markdown.md#block-quotes)
* [목록](/help/assets/content-fragments/content-fragments-markdown.md#lists)
* [강조](/help/assets/content-fragments/content-fragments-markdown.md#emphasis)
* [코드 블록](/help/assets/content-fragments/content-fragments-markdown.md#code-blocks)
* [백슬래시 이스케이프](/help/assets/content-fragments/content-fragments-markdown.md#backslash-escapes)

## 제목 표기법 {#heading-notation}

머리글 앞에 해시 태그(#)를 삽입하여 헤더를 만들려면 H1에는 하나의 해시 태그(#)가 사용되고 H2에는 두 개의 해시 태그(##)가 사용됩니다. 최대 6개의 해시 태그를 사용할 수 있습니다. 예:

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

선택적으로 동일한 기호로 텍스트에 밑줄을 그어 H1을 만들고 빼기 기호로 텍스트에 밑줄을 그어 H2를 만들 수 있습니다. 예:

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## 단락 및 줄 바꿈 {#paragraphs-and-line-breaks}

단락은 한 개 이상의 빈 줄로 구분되어 한 개 이상의 연속된 텍스트 행입니다. 공백은 공백이나 탭 이외의 항목이 포함된 라인입니다. 일반 단락은 공백이나 탭으로 들여쓰면 안 됩니다.

두 개 이상의 공백이 있는 행을 종료한 다음 반환하여 줄 바꿈이 만들어집니다.

## 링크 {#links}

인라인 및 참조 링크를 만들 수 있습니다.

두 스타일 모두에서 링크 텍스트는 대괄호로 구분됩니다 `[]`.

다음은 인라인 링크의 예입니다.

    `This is [an example](https://example.com/ "Title") inline link.`

    `This is [an example of an email link](emailto:myaddress@mydomain.info)`

    `[This link](https://example.net/) has no title attribute.`

참조 링크에는 다음 구문이 있습니다.

    `Hey you should [checkout][0] this [cool thing][wiki] that I [made][].`

    `[0]: https://www.google.ca`

    `[wiki]: https://www.wikipedia.org`

    `[made]: https://www.stackoverflow.com`

## 이미지 {#images}

이미지의 구문은 링크와 유사합니다. 인라인 및 참조된 이미지를 만들 수 있습니다.

예를 들어 인라인 이미지의 구문은 다음과 같습니다.

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

구문은 다음과 같습니다.

* 느낌표: !;
* 뒤에 이미지의 대체 속성 텍스트를 포함하는 대괄호 세트가 옵니다.
* 뒤에 이미지에 대한 URL 또는 경로를 포함하는 괄호 세트와, 큰따옴표나 작은 따옴표로 묶은 선택적 title 속성이 있습니다.

참조 스타일 이미지에는 다음 구문이 있습니다.

    `![Alt text][id]`

여기서 &quot;id&quot;는 정의된 이미지 참조의 이름입니다. 이미지 참조는 링크 참조와 동일한 구문을 사용하여 정의됩니다.

    `[id]: url/to/image "Optional title attribute"`

## 따옴표 차단 {#block-quotes}

텍스트 앞에 > 기호를 추가하여 텍스트를 인용할 수 있습니다. 예:

    `>This is block quotes`

    `>asdhfjlkasdhlf`

    `>asdfahsdlfasdfj`

블록 인용구를 중첩시킬 수 있습니다. 예:

    `> This is the first level of quoting.`

    `>`

        `>> This is nested blockquote.`

    `>`

    `> Back to the first level.`

## 목록 {#lists}

순차 목록과 비순차 목록을 만들 수 있습니다.

순서가 없는 목록을 만들려면 &amp;ast;를 사용하십시오. 심볼을 목록의 항목 앞에 놓습니다. 예:

    `* item in list`

    `* item in list`

    `* item in list`

순서가 지정된 목록을 만들려면 목록의 각 항목 앞에 숫자를 추가하고 마침표를 추가합니다. 예:

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## 강조 {#emphasis}

텍스트에 기울임꼴 또는 굵은 스타일을 추가할 수 있습니다.

다음과 같이 기울임체를 추가할 수 있습니다.

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

다음과 같이 텍스트를 굵게 지정할 수 있습니다.

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

코드 범위를 나타내려면 백틱 따옴표(&#39;)로 둘러싸십시오. 사전에 서식이 지정된 코드 블록과 달리 코드 범위는 일반 단락 내의 코드를 나타냅니다.

예:

    ``Use the `printf()` function.``

## 코드 블록 {#code-blocks}

코드 블록은 일반적으로 소스 코드를 표시하는 데 사용됩니다. 탭 또는 최소 4개의 공백을 사용하여 코드를 들여보내 코드 블록을 만들 수 있습니다. 예:

    `This is a normal paragraph.`

        `This is a code block.`

## 백슬래시 이스케이프 {#backslash-escapes}

백슬래시 이스케이프 처리를 사용하여 형식 구문에 특별한 의미가 있는 문자 그대로의 문자를 생성할 수 있습니다. 예를 들어 문자 별표(HTML &lt;em> 태그 대신)로 단어를 둘러싸려면 다음과 같이 별표 앞에 백슬래시를 사용할 수 있습니다.

    `\\*literal asterisks\\*`

백슬래시 이스케이스는 다음 문자에 사용할 수 있습니다.

    `\ backslash`

    &#39; 백틱

    `* asterisk`

    `_ underscore`

    `{} curly braces`

    `[] square brackets`

    `() parentheses`

    `# hash mark`

    `+ plus sign`

    `- minus sign (hyphen)`

    `. dot`
