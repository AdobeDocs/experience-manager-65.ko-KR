---
title: 테스트 계획 컴파일
description: 개별 테스트 사례가 테스트 계획에 통합됩니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
docset: aem65
exl-id: ee5df2c8-ab31-4be9-8ede-3c96f26fc626
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# 테스트 계획 컴파일{#compiling-your-test-plan}

그런 다음 개별 테스트 사례가 테스트 계획에 통합되어 다음도 정의합니다.

**우선 순위**

어떤 검사는 다른 검사에 비해 유의성이 높으므로 우선 순위를 나타내는 것이 좋습니다.

예를 들어 특정 테스트는 Go/No-Go 결정에 영향을 줄 수 있으므로 테스트된 모든 중간 릴리스를 통해 확인해야 합니다.

**반복**

프로젝트에서 사용 가능한 여러 릴리스가 포함된 개발 반복을 사용하는 경우 각 반복에 대한 결과를 표시해야 하거나 표시해야 할 수 있습니다. 이를 사용하여 다음을 나타낼 수 있습니다.

* 어떤 반복에서 다뤄질 테스트인지 설명합니다.
* 여러 번 반복된 테스트에 대해 표시되는 결과입니다.
* 이 우선 순위 테스트와 기본 기능에 대한 테스트가 일정한 간격으로 반복됩니다.

**테스터**

어느 시점에서 적절한 테스트 팀이나 특정 테스트 사람(가용성 및/또는 경험에 따라 달라질 수 있음)을 할당할 수 있습니다.

**요약 또는 개요**

보고 목적으로 테스트 결과에 대한 개요를 제공할 것입니다.

* 이미 적용된 테스트 비율입니다.
* 성공/실패 비율입니다.
* 우선순위 테스트와 관련된 특정 수치입니다.
