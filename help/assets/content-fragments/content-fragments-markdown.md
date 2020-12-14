---
title: Markdown
seo-title: Markdown
description: 작성 시 컨텐츠 조각 편집기에서는 Markdown 구문을 사용하므로 컨텐츠를 쉽게 작성할 수 있습니다.
seo-description: 작성 시 컨텐츠 조각 편집기에서는 Markdown 구문을 사용하므로 컨텐츠를 쉽게 작성할 수 있습니다.
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
ht-degree: 100%

---


# Markdown{#markdown}

[작성](content-fragments-variations.md#authoring-your-content) 시 컨텐츠 조각 편집기에서는 *Markdown* 구문을 사용하므로 컨텐츠를 쉽게 작성할 수 있습니다.

![Markdown 편집기](/help/assets/content-fragments/assets/cfm-6420-08.png)

다음을 항목을 정의할 수 있습니다.

* [제목 표기법](/help/assets/content-fragments/content-fragments-markdown.md#heading-notation)
* [단락 및 줄 바꿈](/help/assets/content-fragments/content-fragments-markdown.md#paragraphs-and-line-breaks)
* [링크](/help/assets/content-fragments/content-fragments-markdown.md#links)
* [이미지](/help/assets/content-fragments/content-fragments-markdown.md#images)
* [블록 인용](/help/assets/content-fragments/content-fragments-markdown.md#block-quotes)
* [목록](/help/assets/content-fragments/content-fragments-markdown.md#lists)
* [강조](/help/assets/content-fragments/content-fragments-markdown.md#emphasis)
* [코드 블록](/help/assets/content-fragments/content-fragments-markdown.md#code-blocks)
* [백슬래시 이스케이프](/help/assets/content-fragments/content-fragments-markdown.md#backslash-escapes)

## 제목 표기법 {#heading-notation}

제목 앞에 해시 태그(#)를 배치하여 제목을 만듭니다. H1에는 하나의 해시 태그(#)가 사용되고 H2에는 두 개의 해시 태그(##)가 사용되는 방식입니다. 최대 6개의 해시 태그를 사용할 수 있습니다. 예:

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

원할 경우 등호 기호로 텍스트에 밑줄을 그어 H1을 만들고 마이너스 기호로 텍스트에 밑줄을 그어 H2를 만들 수 있습니다. 예:

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## 단락 및 줄 바꿈 {#paragraphs-and-line-breaks}

단락은 하나 이상의 빈 행으로 구분된 하나 이상의 연속된 텍스트 행입니다. 빈 행은 공백이나 탭만 포함하는 행입니다. 일반적인 단락은 공백이나 탭으로 들여쓰면 안 됩니다.

행을 두 개 이상의 공백과 Return 키를 차례로 사용하여 끝맺음으로써 줄바꿈이 만들어집니다.

## 링크 {#links}

인라인 및 참조 링크를 만들 수 있습니다.

두 스타일 모두에서 링크 텍스트는 대괄호 `[]`로 구분됩니다.

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

이미지 구문은 링크와 유사합니다. 인라인 및 참조된 이미지를 만들 수 있습니다.

예를 들어 인라인 이미지에는 다음 구문이 있습니다.

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

구문은

* 느낌표(!)를 포함합니다.;
* 뒤에 이미지의 대체 특성 텍스트를 포함하는 대괄호 세트가 옵니다.
* 뒤에 이미지의 URL 또는 경로를 포함하는 괄호 세트와, 큰따옴표나 작은따옴표로 묶인 선택적 제목 특성이 있습니다.

참조 스타일 이미지에는 다음 구문이 있습니다.

    `![Alt text][id]`

여기서 &quot;id&quot;는 정의된 이미지 참조의 이름입니다. 이미지 참조는 링크 참조와 동일한 구문을 사용하여 정의됩니다.

    `[id]: url/to/image "Optional title attribute"`

## 블록 인용 {#block-quotes}

텍스트 앞에 > 기호를 추가하여 텍스트를 인용할 수 있습니다. 예:

    `>This is block quotes`

    `>asdhfjlkasdhlf`

    `>asdfahsdlfasdfj`

블록 인용을 중첩시킬 수 있습니다. 예:

    `> This is the first level of quoting.`

    `>`

        `>> This is nested blockquote.`

    `>`

    `> Back to the first level.`

## 목록 {#lists}

순차 목록과 비순차 목록을 만들 수 있습니다.

순서가 없는 무순차 목록을 만들려면 목록에 있는 항목 앞에 &amp;ast; 기호를 사용하십시오. 예:

    `* item in list`

    `* item in list`

    `* item in list`

순서가 지정된 순차 목록을 만들려면 목록에 있는 각 항목 앞에 숫자와 마침표를 차례로 추가합니다. 예:

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## 강조 {#emphasis}

텍스트에 기울임꼴이나 굵은 스타일을 추가할 수 있습니다.

다음과 같이 기울임체를 추가할 수 있습니다.

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

다음과 같이 텍스트를 굵게 지정할 수 있습니다.

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

코드 범위(code span)를 나타내려면 억음 악센트 따옴표(`)로 둘러쌉니다. 서식이 미리 지정된 코드 블록과 달리 코드 범위는 일반 단락 내의 코드를 나타냅니다.

예:

    ``Use the `printf()` function.``

## 코드 블록 {#code-blocks}

코드 블록은 일반적으로 소스 코드를 표시하는 데 사용됩니다. 한 개의 탭이나 최소 4개의 공백으로 코드를 들여써서 코드 블록을 만들 수 있습니다. 예:

    `This is a normal paragraph.`

        `This is a code block.`

## 백슬래시 이스케이프 {#backslash-escapes}

백슬래시 이스케이프를 사용하여 형식 지정 구문에서 특별한 의미가 있는 리터럴 문자를 생성할 수 있습니다. 예를 들어 리터럴 별표(HTML &lt;em> 태그 대신)로 단어를 둘러싸려면 다음과 같이 별표 앞에 백슬래시를 사용할 수 있습니다.

    `\\*literal asterisks\\*`

백슬래시 이스케이스는 다음 문자에 사용할 수 있습니다.

    `\ backslash`

    ` 억음 악센트

    `* asterisk`

    `_ underscore`

    `{} curly braces`

    `[] square brackets`

    `() parentheses`

    `# hash mark`

    `+ plus sign`

    `- minus sign (hyphen)`

    `. dot`
