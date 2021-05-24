---
title: 어떤 테스트 환경이 필요합니까?
seo-title: 어떤 테스트 환경이 필요합니까?
description: 몇 가지 환경은 테스트의 일부로 간주되어야 합니다
seo-description: 몇 가지 환경은 테스트의 일부로 간주되어야 합니다
uuid: bb725e50-edae-4c20-8107-d1c8df2e60e2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: db528b9b-3407-462d-8254-20b3cc2c3ccf
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 3%

---

# 어떤 테스트 환경이 필요합니까?{#which-test-environments-will-be-needed}

테스트할 구성을 정의하려면 다음을 고려해야 합니다.

**개발**  - 단위 및 특정 통합 테스트용.

**테스트**  - 대부분의 테스트에 대해.

**라이브**  - 최종 성능 및 스트레스 테스트. 고객과의 수락 테스트도 참조하십시오.

또한 어느 인스턴스가 필요한지 결정해야 합니다(일반적으로 모든 테스트 수준에 대해 각 인스턴스 중 하나 이상).

**작성자**  - 이 인스턴스를 사용하여 작성자가 컨텐츠를 입력하고 게시할 수 있습니다.

**게시**  - 이 인스턴스는 방문자가 액세스할 수 있도록 게시된 웹 사이트의 양식을 제공합니다.

디스패처와 함께 테스트해야 합니다.

마지막으로 실제 하드웨어는 고려해야 합니다. 최종 라이브 환경에 대한 구성에서 가능한 한 시스템에서 성능 테스트를 수행해야 합니다. 이러한 이유로 프로젝트 론치를 다음으로 분할하는 것이 좋습니다.

**Soft Launch**  - 가용성 감소실제 운영 환경에서 성능 테스트, 조정 및 최적화에 소요되는 시간을 허용합니다.

**하드 론치**  - 완벽한 가용성.
