---
title: 편집기 제한 사항
seo-title: 편집기 제한 사항
description: 터치 지원 UI의 편집기는 오버레이를 사용하여 iframe에 포함된 컨텐츠와 상호 작용합니다. 이러한 상호 작용으로 편집기와 개발자를 위한 두 가지 사용 모두에서 몇 가지 제한 사항이 발생합니다.
seo-description: 터치 지원 UI의 편집기는 오버레이를 사용하여 iframe에 포함된 컨텐츠와 상호 작용합니다. 이러한 상호 작용으로 편집기와 개발자를 위한 두 가지 사용 모두에서 몇 가지 제한 사항이 발생합니다.
uuid: ff524530-3f3a-4c5b-9f94-4aa9aeb9d461
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: d748decb-a614-4c9e-a502-d6176b720f1a
translation-type: tm+mt
source-git-commit: 844d42ed50da153077423190684aa85265bce12f
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 1%

---


# 편집기 제한 사항{#editor-limitations}

터치 지원 UI의 편집기는 오버레이를 사용하여 iframe에 포함된 컨텐츠와 상호 작용합니다. 이러한 상호 작용으로 편집기와 개발자를 위한 두 가지 사용 모두에서 몇 가지 제한 사항이 발생합니다. 이 페이지에서는 이러한 제한 사항을 요약하고 가능한 경우 해결 방법 또는 해결 방법을 제공합니다.

## 기능 제한 사항 {#functional-limitations}

작성자는 편집기를 사용하여 페이지를 작성할 때 다음과 같은 기능 제한 사항이 있을 수 있습니다.

### 링크가 활성화되지 않음 {#links-not-active}

[페이지](/help/sites-authoring/editing-content.md)를 편집하면 링크가 활성화되지 않습니다.

* [콘텐츠 **** ](/help/sites-authoring/editing-content.md#preview-mode) 의 링크를 사용하여 탐색하려면 미리 보기 모드로 전환합니다.

### 구조 페이지 {#structure-pages}

페이지 이름은 `structure`으로 지정할 수 없습니다. 이름 `structure`인 페이지는 페이지 편집기에서 편집할 수 없습니다.

## CSS 제한 사항 {#css-limitations}

개발자는 편집기의 CSS 상호 작용에 다음과 같은 제한 사항이 있을 수 있습니다.

### 절대 위치 요소 {#absolutely-positioned-elements}

절대 위치의 요소는 오버레이 위치에 문제를 일으킬 수 있습니다.

* 이러한 경우 편집기가 동일한 크기로 오버레이를 만들기 때문에 절대 위치 요소의 크기가 올바른지 확인하십시오.

### vh 단위 {#vh-units}

`vh` iframe 높이는 AEM에서 자동으로 조정되어야 하므로 단위가 지원되지 않습니다.

### 배경 이미지 {#fixed-background-images} 수정

배경 이미지가 iframe 내에 내장되어 있어 스크롤할 때 고정된 배경 이미지가 고정으로 표시되지 않을 수 있습니다.

* 헤더 막대 작업에서 **게시됨으로 페이지 보기**&#x200B;를 선택하면 페이지가 제대로 표시됩니다.

### 100% 높이 {#height}

100% 높이는 페이지의 본문 요소에서 지원되지 않습니다.

* 다음과 같이 본문 요소를 &quot;스트레치&quot;하여 전체 화면 본문을 구현하기 위해 작업을 할 수 있습니다.

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### 여백 축소 {#margin-collapsing}

본문 요소의 첫 번째 하위 요소에 여백이 있는 경우 여백 축소 문제를 확인할 수 있습니다.

* 해결 방법은 다음과 같은 body 요소 수준에서 지우기 수정을 추가하는 것입니다.

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```

