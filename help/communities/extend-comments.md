---
title: 주석 구성 요소 확장
description: Comments 구성 요소를 확장하여 특정 용도의 모양 또는 동작을 변경합니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: e57198cb-8fd9-43e2-b416-e40e462561c8
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# 주석 구성 요소 확장  {#extend-comments-component}

기본 구성 요소를 [확장](client-customize.md#extensions)하려는 목적은 특정 용도로 구성 요소의 모양 또는 동작을 변경하는 것입니다.

구성 요소에 대한 경로는 고유하며 기본 구성 요소를 슈퍼 리소스 유형으로 참조합니다. 컴포넌트 오버레이의 글로벌 범위에 비해 범위가 제한되므로 위험이 적다.

>[!NOTE]
>
>[오버레이된](client-customize.md#overlays) 구성 요소 확장은 지원되지 않습니다.

## 예 {#example}

주석 구성 요소의 헤더가 AEM 인스턴스의 한 사이트에는 대체 모양으로 표시되고 다른 사이트에는 기본 모양으로 표시되어야 한다고 가정합니다. 모든 인스턴스의 주석 구성 요소를 변경하는 기본 주석을 오버레이하는 대신 더 나은 해결책은 다양한 사이트에서 사용할 수 있는 주석 구성 요소가 여러 개 있는지 확인하는 것입니다.

이 솔루션을 구현하려면 기존 구성 요소를 확장(무시)하는 구성 요소를 만들고 Handlebars 스크립트를 수정합니다. 새 주석을 사용하는 사이트 영역은 확장된 주석을 사용할 수 있지만 기본 모양을 사용하는 사이트는 영향을 받지 않습니다.

설명 구성 요소는 실제로 설명 시스템을 구성하는 두 구성 요소 중 하나입니다. 따라서 확장할 구성 요소는 *댓글* 및 *댓글*&#x200B;입니다. 편집할 스크립트는 *comment* 구성 요소의 `header.hbs` 파일에 있지만, 상위 *comments* 구성 요소(댓글 시스템)는 작성자가 페이지에 실제로 추가하는 것입니다.

주석을 확장하려면 다음 작업을 수행해야 합니다.

1. [구성 요소 만들기](extend-create-components.md)
1. [샘플 페이지에 주석 추가](extend-sample-page.md)
1. [모양 변경](extend-alter-appearance.md)
