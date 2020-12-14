---
title: 주석 구성 요소 확장
seo-title: 주석 구성 요소 확장
description: 주석 구성 요소를 확장하여 특정 용도의 모양이나 동작을 변경합니다
seo-description: 주석 구성 요소를 확장하여 특정 용도의 모양이나 동작을 변경합니다
uuid: 6f439097-b1d0-4e7d-afcf-01d8f43aa866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a07a4690-0e47-4a76-84cb-96abdc70b835
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# 주석 구성 요소 확장 {#extend-comments-component}

기본 구성 요소를 [확장](client-customize.md#extensions)하려는 의도는 특정 용도로 구성 요소의 모양 또는 동작을 변경하는 것입니다.

구성 요소의 경로는 고유하며 기본 구성 요소를 슈퍼 리소스 유형으로 참조합니다. 구성 요소 오버레이의 전역 범위에 비해 범위가 제한되므로 위험 요소가 줄어듭니다.

>[!NOTE]
>
>[오버레이된](client-customize.md#overlays) 구성 요소 확장은 지원되지 않습니다.

## 예 {#example}

주석 구성 요소의 헤더가 AEM 인스턴스의 한 사이트에 다른 사이트에 기본 디스플레이와 함께 표시되지만 다른 사이트에 있는 대체 모양과 함께 표시되어야 한다고 가정합니다. 모든 인스턴스에 대해 주석 구성 요소를 변경하는 기본 주석을 오버레이하는 대신 다양한 사이트에서 사용할 수 있는 주석 구성 요소가 여러 개 있는지 확인하는 것이 좋습니다.

이 솔루션을 구현하려면 기존 구성 요소를 확장(재정의)하고 핸들막대 스크립트를 수정하는 새 구성 요소를 만듭니다. 새 주석을 사용하는 사이트의 영역은 확장된 주석을 사용할 수 있고 기본 모양을 사용하는 사이트는 영향을 받지 않습니다.

주석 구성 요소는 주석 시스템을 구성하는 두 구성 요소 중 하나입니다. 따라서 확장할 구성 요소가 두 개 있습니다.*comments* 및 *comment*. 편집할 스크립트는 *comment* 구성 요소의 `header.hbs` 파일에 있고 상위 *comments* 구성 요소(주석 시스템)는 작성자가 페이지에 실제로 추가하는 것입니다.

주석을 확장하려면 다음을 수행해야 합니다.

1. [구성 요소 만들기](extend-create-components.md)
1. [샘플 페이지에 주석 추가](extend-sample-page.md)
1. [모양 변경](extend-alter-appearance.md)

