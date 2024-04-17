---
title: 어떤 테스트 환경이 필요합니까?
description: 테스트의 일부로 여러 환경을 고려해야 합니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# 어떤 테스트 환경이 필요합니까?{#which-test-environments-will-be-needed}

테스트할 구성을 정의하려면 다음 사항을 고려해야 합니다.

**개발** - 장치 및 특정 통합 테스트의 경우.

**테스트** - 대부분의 테스트에 사용됩니다.

**라이브** - 최종 성능 및 스트레스 테스트 또한 고객과의 수락 테스트용입니다.

필요한 인스턴스와 위치를 결정합니다(일반적으로 모든 수준의 테스트에 대해 각각 최소 하나 이상).

**작성자** - 이 인스턴스를 사용하여 작성자가 콘텐츠를 입력하고 게시할 수 있습니다.

**게시** - 이 인스턴스는 방문자가 액세스할 수 있도록 게시된 양식으로 웹 사이트를 표시합니다.

Dispatcher를 사용하여 테스트했습니다.

마지막으로 실제 하드웨어를 고려해야 합니다. 가능한 최종 라이브 환경에 가까운 구성에서 시스템에서 성능 테스트를 수행해야 합니다. 이러한 이유로 프로젝트 시작 을 다음과 같이 분할하는 것이 좋습니다.

**소프트 실행** - 가용성이 감소하여 실제 운영 환경에서 성능 테스트, 튜닝 및 최적화에 소요되는 시간이 단축됩니다.

**하드 론치** - 전체 가용성
