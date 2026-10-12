---
title: 결과 추적 및 피드백 제공
description: 테스트 사례를 정의하는 방법과 위치, 결과 테스트 계획은 사용자가 결정합니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: 270e66d1-a3f2-457a-90d1-28b9f3c8c218
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 6%
---
# 결과 추적 및 피드백 제공{#tracking-results-and-providing-feedback}

테스트 사례를 정의하는 방법과 위치, 결과 테스트 계획은 사용자가 결정합니다. 다양한 도구를 사용할 수 있습니다.

그러나 선택한 방법이나 도구에 관계없이 정보는 다음과 같이 저장됩니다.

* 다음과 같아야 합니다.

  * 테스트 사례와 그 결과를 추적하는 것으로 제한됩니다. 이렇게 하면 유지 관리가 간단해지고 문서가 테스트 진행에 대한 명확한 개요를 제공할 수 있습니다.
  * 단일 사본으로 유지 관리되며, 프로젝트 팀의 모든 적절한 구성원이 사용할 수 있습니다.
  * 중립적이고 테스트 결과로 제한됩니다. 테스트 결과로 발생하는 모든 작업에 대한 결정은 프로젝트 관리자의 책임입니다.

* 다음이 아니어야 합니다.

  * 버그, 새로운 기능 및 후속 작업 등 추적 정보를 포함하도록 확장되었습니다. 이 정보는 다른 곳에서도 유지되어야 합니다. 사용할 수 있는 도구가 많습니다.
