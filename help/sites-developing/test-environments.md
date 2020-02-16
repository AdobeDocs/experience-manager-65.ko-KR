---
title: 어떤 테스트 환경이 필요합니까?
seo-title: 어떤 테스트 환경이 필요합니까?
description: 여러 환경은 테스트의 일부로 간주되어야 합니다.
seo-description: 여러 환경은 테스트의 일부로 간주되어야 합니다.
uuid: bb725e50-edae-4c20-8107-d1c8df2e60e2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: db528b9b-3407-462d-8254-20b3cc2c3ccf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 어떤 테스트 환경이 필요합니까?{#which-test-environments-will-be-needed}

테스트할 구성을 정의하려면 다음을 고려해야 합니다.

**개발** - 장치 및 특정 통합 테스트용

**테스트** - 대부분의 테스트

**라이브** - 최종 성능 및 스트레스 테스트를 위해 고객과의 수락 테스트도 참조하십시오.

또한 필요한 인스턴스를 결정해야 합니다(일반적으로 모든 테스트 수준에 대해 각 인스턴스 중 하나 이상).

**작성자** - 이 인스턴스는 작성자가 컨텐츠를 입력하고 게시할 수 있도록 합니다.

**게시** - 이 인스턴스는 방문자의 액세스를 위해 게시된 양식으로 웹 사이트를 표시합니다.

Dispatcher와 함께 테스트해야 합니다.

마지막으로, 실제 하드웨어는 고려해야 합니다. 모든 성능 테스트는 가능한 한 최종 라이브 환경에 대한 구성으로 시스템에서 수행해야 합니다. 따라서 프로젝트 론치를 다음 항목으로 나누는 것이 좋습니다.

**소프트 론치** - 가용성 감소실제 운영 환경에서 성능 테스트, 조정 및 최적화에 시간을 할애할 수 있습니다.

**하드 출시** - 전체 가용성.
