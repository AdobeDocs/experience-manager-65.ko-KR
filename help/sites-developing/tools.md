---
title: 테스트 및 추적 도구
seo-title: Testing and Tracking Tools
description: AEM은 구성 요소 UI 테스트를 위한 프레임워크 및 구성 요소 테스트 및 디버깅을 위한 메커니즘을 제공합니다
seo-description: AEM provides a framework for testing component UI and a mechanism for testing and debugging components
uuid: 12abedb5-4ee7-4389-9340-e628adbbc053
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 3cf0fd8d-7fc8-468a-bb1e-1debb68a82a5
docset: aem65
exl-id: bb5d1c7c-56ce-4d1e-a3cb-4e74d6922137
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 4%

---

# 테스트 및 추적 도구{#testing-and-tracking-tools}

## 테스트 {#testing}

AEM은 다음을 제공합니다.

* [구성 요소 UI 테스트를 위한 프레임워크](/help/sites-developing/hobbes.md).
* [구성 요소를 테스트하고 디버깅하기 위한 메커니즘](/help/sites-developing/developer-mode.md).

다음은 두 가지 오픈 소스 테스트 도구입니다.

**Selenium**

Selenium은 활동당 한 명의 사용자가 있는 브라우저에서 기능 테스트에 사용됩니다. 테스트 단계(클릭 수)를 HTML 테이블 또는 Java 클래스로 기록합니다.

자세한 내용은 [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**JMeter**

JMeter는 요청을 추적하는 데 사용되며 기능, 성능 및 스트레스 테스트에 사용할 수 있습니다.

자세한 내용은 [https://jakarta.apache.org/jmeter/](https://jakarta.apache.org/jmeter).

또한 테스트 자동화 및 테스트 계획 관리를 위한 많은 독점 툴이 있습니다.

### 추적 {#tracking}

다음 도구를 쉽게 사용할 수 있습니다. 그러나 모든 경우 핵심 문제는 프로젝트 팀의 모든 구성원(파트너 및 고객)에게 데이터를 제공하는 것입니다.

**부질라**

자체 요구 사항에 맞게 구성할 수 있는 버그 추적 시스템.

**스프레드시트**

버그 추적 도구는 아니지만 스프레드시트는 다음과 같은 경우가 많습니다 *mis*&#x200B;이해하기 쉽고 대부분의 사용자가 해당 기능에 대한 경험을 가지고 있으므로 이 용도로 사용됩니다.

이러한 항목이 추적에 사용되는 경우:

* 단순하게 유지해야 합니다.
* 개별 스프레드시트의 수는 최소한으로 유지해야 합니다.
* 정기적으로 업데이트해야 합니다.
* 마스터 사본은 하나만 유지되어야 하며 모든 사용자는 마스터 사본의 위치를 알 수 있습니다.
* 모든 프로젝트 멤버가 액세스할 수 있어야 합니다.
* 보안이 문제이고(대기업에서 종종 발생) 공통 액세스가 불가능한 경우 모든 사람이 복사본이 아니며 업데이트할 수 없다는 것을 알고 있는 한 복사본이 배포될 수 있습니다.

버그 및 기능 요구 사항을 추적하기 위한 많은 독점 도구가 있습니다.
