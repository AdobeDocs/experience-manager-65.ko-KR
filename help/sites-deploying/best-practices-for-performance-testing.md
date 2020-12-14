---
title: 성능 테스트 모범 사례
seo-title: 성능 테스트 모범 사례
description: 이 문서에서는 성능 테스트에 사용되는 전반적인 전략 및 방법론과 프로세스를 지원하는 데 사용할 수 있는 일부 툴에 대해 간략히 살펴봅니다.
seo-description: 이 문서에서는 성능 테스트에 사용되는 전반적인 전략 및 방법론과 프로세스를 지원하는 데 사용할 수 있는 일부 툴에 대해 간략히 살펴봅니다.
uuid: ab8720d6-b864-4d00-9e07-2e1699cfe7db
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 669018a0-f6ef-42b2-9c6f-83d7dd5a7095
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1925'
ht-degree: 0%

---


# 성능 테스트 모범 사례{#best-practices-for-performance-testing}

## 소개 {#introduction}

성능 테스트는 모든 AEM 배포의 중요한 부분입니다. 고객 요구 사항에 따라 게시 인스턴스, 작성자 인스턴스 또는 두 가지 모두에서 성능 테스트가 수행될 수 있습니다.

이 설명서는 성능 테스트를 수행하는 전반적인 전략 및 방법론과 프로세스를 지원하기 위해 Adobe에서 사용할 수 있는 일부 도구의 개요를 설명합니다. 마지막으로, 코드 분석 및 시스템 구성 관점에서 성능 조정에 도움을 주기 위해 AEM 6에서 제공되는 일부 툴을 분석할 것입니다.

### 현실 시뮬레이션 {#simulating-reality}

성능 테스트를 수행할 때 가장 중요한 것은 프로덕션 환경을 가능한 한 가깝게 모방하도록 하는 것입니다. 이 경우 어려운 경우가 많지만 이러한 테스트의 정확성을 보장해야 합니다. 성능 테스트를 디자인할 때는 다음 사항을 고려해야 합니다.

* 제작 관련 컨텐츠

쿼리 응답 시간과 같은 AEM의 많은 성능 측정은 시스템의 컨텐츠 크기에 의해 영향을 받을 수 있습니다. 테스트 환경에서 가능한 한 프로덕션 데이터 사본의 근접 범위를 확인해야 합니다.

* 프로덕션 코드

프로덕션에 배포된 AEM 버전 및 핫픽스는 테스트 환경에서 동일해야 합니다. 또한 프로덕션에 배포된 코드 버전을 테스트하는 것도 중요합니다.

* 운영 방식의 하드웨어 및 네트워크 구성

가능한 한 생산 환경과 유사한 환경 없이는 테스트가 무의미할 것이다. 가장 좋은 방법은 하드웨어 사양, 네트워크 인터페이스, 로드 밸런서 및 CDN은 테스트 환경의 프로덕션과 동일해야 합니다.

* 프로덕션 로드

시스템이 과도하게 로드될 때까지 많은 성능 문제가 표시되지 않습니다. 우수한 성능 테스트를 통해 프로덕션 시스템이 최고의 상태에 있을 부하를 시뮬레이션해야 합니다.

### 목표 설정 {#setting-goals}

성능 테스트를 시작하기 전에 부하 및 응답 시간을 지정하기 위해 비기능 요구 사항을 설정해야 합니다. 기존 시스템에서 마이그레이션하는 경우 응답 시간이 현재 프로덕션 값과 비슷한지 확인합니다. 로드의 경우 현재 최고 부하를 가져다가 두 배로 늘리는 것이 가장 좋습니다. 이렇게 하면 웹 사이트가 성장함에 따라 계속 제대로 작동할 수 있습니다.

### 도구 {#tools}

시장에 시판되는 다양한 성능 테스트 툴이 있습니다. 로드 생성 도구를 실행할 때는 테스트를 수행하는 컴퓨터에 충분한 네트워크 대역폭이 있는지 확인해야 합니다. 그렇지 않으면 테스트 컴퓨터가 연결 제한에 도달하면 테스트 중인 환경에서 추가 로드가 생성되지 않습니다.

#### 테스트 도구 {#testing-tools}

* Adobe의 **어려운 날** 도구는 AEM 인스턴스에서 로드를 생성하고 성능 데이터를 수집하는 데 사용할 수 있습니다. Adobe AEM 엔지니어링 팀은 실제로 이 도구를 사용하여 AEM 제품 자체의 로드 테스트를 수행합니다. 어려운 날에 실행되는 스크립트는 속성 파일과 JMX XML 파일을 통해 구성됩니다. 자세한 내용은 [힘든 날 설명서](/help/sites-developing/tough-day.md)를 참조하십시오.

* AEM은 문제가 있는 쿼리, 요청 및 오류 메시지를 빠르게 볼 수 있는 특별한 도구를 제공합니다. 자세한 내용은 Operations Dashboard 설명서의 [진단 도구](/help/sites-administering/operations-dashboard.md#diagnosis-tools) 섹션을 참조하십시오.
* Apache는 성능 및 로드 테스트 및 기능 동작에 사용할 수 있는 **JMeter**&#x200B;라는 제품을 제공합니다. 오픈 소스 소프트웨어이고 무료로 사용할 수 있지만 엔터프라이즈 제품보다 기능이 작으며 학습에 어려움이 따릅니다. JMeter는 Apache 웹 사이트([https://jmeter.apache.org/](https://jmeter.apache.org/))에서 찾을 수 있습니다.

* **Load** Runner는 Enterprise 등급 로드 테스트 제품입니다. 무료 평가 버전을 사용할 수 있습니다. 자세한 내용은 [https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)에서 확인할 수 있습니다.

* [Neustar](https://www.neustar.biz/services/web-performance/load-testing)과 같은 클라우드 기반 로드 테스트 도구도 사용할 수 있습니다.
* 모바일 또는 반응형 웹 사이트를 테스트하는 데 있어 별도의 도구 세트를 사용해야 합니다. 네트워크 대역폭을 조절하여 3G 또는 EDGE와 같은 느린 모바일 연결을 시뮬레이션합니다. 널리 사용되는 도구 중에는 다음과 같은 것들이 있습니다.

   * **[네트워크 링크](https://nshipster.com/network-link-conditioner/)**  - 사용하기 쉬운 UI를 제공하며 네트워킹 스택에서 매우 낮은 수준에서 작동합니다. 여기에는 OS X 및 iOS용 버전이 포함됩니다.[](https://nshipster.com/network-link-conditioner/)
   * [**Charles**](https://www.charlesproxy.com/)  - 여러 가지 다른 용도 외에 네트워크 조절 기능을 제공하는 웹 디버깅 프록시 응용 프로그램입니다. 버전은 Windows, OS X 및 Linux용으로 제공됩니다.[](https://www.charlesproxy.com/)

#### 최적화 도구 {#optimization-tools}

**모니터링**

[모니터링 성능](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) 설명서는 문제를 진단하고 튜닝할 영역을 식별하는 데 사용할 수 있는 도구 및 방법에 대한 유용한 리소스입니다.

**터치 UI의 개발자 모드**

AEM 6의 터치 UI에 새로운 기능 중 하나는 개발자 모드입니다. 작성자가 편집 모드와 미리 보기 모드 간을 전환할 수 있는 것처럼 개발자는 작성 UI에서 개발자 모드로 전환하여 페이지에 있는 각 구성 요소의 렌더링 시간을 보고 오류의 스택 추적을 확인할 수 있습니다. 개발자 모드에 대한 자세한 내용은 이 [CQ Gems 프레젠테이션](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html)을 참조하십시오.

**rlog.jar를 사용하여 요청 로그 읽기**

AEM 시스템에서 요청 로그에 대한 보다 포괄적인 분석을 위해 AEM에서 생성하는 `request.log` 파일을 검색하고 정렬하는 데 `rlog.jar`을 사용할 수 있습니다. 이 jar 파일은 `/crx-quickstart/opt/helpers` 폴더에 AEM 설치에 포함되어 있습니다. 로그 도구 및 일반적으로 요청 로그에 대한 자세한 내용은 [모니터링 및 유지 관리](/help/sites-deploying/monitoring-and-maintaining.md) 설명서를 참조하십시오.

**쿼리 설명 도구**

ACS AEM 도구의 [쿼리 설명 도구](/help/sites-administering/operations-dashboard.md#explain-query)는 쿼리를 실행할 때 사용되는 인덱스를 보는 데 사용할 수 있습니다. 이 기능은 느린 실행 쿼리를 최적화할 때 매우 유용합니다.

**PageSpeed 도구**

Google의 PageSpeed 도구는 페이지 성능에 대한 우수 사례를 따르기 위한 사이트 분석을 제공하며 추가적인 최적화를 위해 Apache 인스턴스의 디스패처 옆에 설치할 수 있는 플러그인을 제공합니다. 자세한 내용은 [PageSpeed 도구 웹 사이트](https://developers.google.com/speed/pagespeed/)를 참조하십시오.

## 작성 환경 {#author-environment}

### 테스트 수행 중 {#performing-tests}

작성 환경에서 성능 테스트를 수행하려면 프로덕션 작성자의 경험을 시뮬레이션해야 합니다. 즉, 작성자 설치에는 프로덕션 작성 인스턴스에 대해 모든 구성 요소, OSGi 번들, UI 사용자 정의, 사용자 정의 색인 및 기타 추가 항목이 포함되어야 합니다.

성능 및 로드 테스트를 위해 고안된 많은 자동화 프레임워크가 있습니다. 이러한 툴에 사용자 정의 스크립트를 기록한 다음 재생할 수 있으므로 유사한 컨텐츠 제작 및 활성화 활동을 동시에 수행하는 최대 작성자 수를 시뮬레이션할 수 있습니다. 수천 개의 에셋을 업로드하거나 대량의 페이지를 활성화하는 등의 활동을 시뮬레이션하려면 터프데이 툴을 사용하는 것이 좋습니다.

자산 로딩 또는 페이지 작성에 대한 요구 사항이 많은 환경의 경우 환경이 최대 로드 상태에서 효율적으로 작동할 수 있도록 하기 위해 어려운 날과 같은 도구를 사용해야 합니다. [WebDAV](/help/sites-administering/webdav-access.md) 는 스크립팅이 필요하지 않으며 대량의 에셋을 로드하는 데 사용할 수 있는 도구입니다.

#### MongoDB 특정 단계 {#mongodb-specific-steps}

MongoDB 백엔드가 있는 시스템에서 AEM은 로드 또는 성능 테스트를 수행할 때 모니터링해야 하는 여러 [JMX](/help/sites-administering/jmx-console.md) MBean을 제공합니다.

* **통합 캐시 통계** MBean. 다음 링크를 통해 직접 액세스할 수 있습니다.

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

**Document-Diff** 캐쉬의 경우 히트 비율은 `.90`보다 커야 합니다. 히트 비율이 90% 미만인 경우 `DocumentNodeStoreService` 구성을 수정해야 할 가능성이 높습니다. Adobe 제품 지원을 통해 환경에 적합한 설정을 권장합니다.

* **Oak 저장소 통계** Mbean. 다음 링크를 통해 직접 액세스할 수 있습니다.

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

**ObservationQueueMaxLength** 섹션은 최근 시간, 분, 초 및 주 동안 Oak의 관측 큐에 있는 이벤트 수를 표시합니다. &quot;시간당&quot; 섹션에서 가장 많은 이벤트 수를 찾습니다. 이 숫자는 [OSGi 콘솔](/help/sites-deploying/web-console.md)의 **SlingRepositoryManager** 구성 요소에서 찾을 수 있는 `oak.observation.queue-length` 설정과 비교해야 합니다. 관측 큐에 대해 표시되는 최대 수가 `queue-length` 설정을 초과하는 경우 Adobe 지원 센터에 문의하여 설정을 높이는 데 도움을 받으십시오. 기본 설정은 1,000이지만 대부분의 배포에서는 일반적으로 20,000 또는 50,000으로 설정해야 합니다.

## 게시 환경 {#publish-environment}

### 테스트 수행 중 {#performing-tests-1}

부하 테스트를 수행해야 하는 배포의 가장 중요한 부분은 게시 또는 디스패처 환경에 직면하는 최종 사용자입니다.

타사 자동 테스트 툴을 사용하여 웹 사이트의 성능을 테스트할 수 있습니다. 이러한 도구를 사용하면 사용자가 사이트에서 거치는 단계를 기록하고 이러한 많은 세션을 동시에 실행하여 프로덕션 웹 사이트의 일반적인 로드를 시뮬레이션할 수 있습니다.

대부분의 제작 웹 사이트는 발송자 캐싱 및 컨텐츠 전달 네트워크와 같이 적절한 최적화를 제공합니다. 테스트할 때 이러한 최적화를 테스트 환경에서도 사용할 수 있도록 해야 합니다. 최종 사용자에 대한 응답 시간을 모니터링할 수 있을 뿐만 아니라, 시스템이 하드웨어 리소스로 제한되지 않도록 게시 서버 및 디스패처에서 시스템 지표를 모니터링해야 합니다.

높은 수준의 개인화가 필요하지 않은 시스템에서 디스패처는 대부분의 요청을 캐시해야 합니다. 따라서 게시 인스턴스의 로드는 상대적으로 평평하게 유지되어야 합니다. 높은 수준의 개인화가 필요한 경우 디스패처 캐싱을 최대한 허용하도록 개인화된 컨텐츠에 대해 iFrame 또는 AJAX 요청과 같은 기술을 사용하는 것이 좋습니다.

기본 테스트의 경우 Apache Bench를 사용하여 웹 서버 응답 시간을 측정하고 메모리 누수와 같은 항목을 측정하는 로드를 생성할 수 있습니다. 자세한 내용은 [모니터링 문서](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench)에서 예제를 참조하십시오.

## 성능 문제 해결 {#troubleshooting-performance-issues}

작성자 인스턴스에서 성능 테스트를 실행한 후 모든 문제를 조사, 확인 및 해결해야 합니다. 분석 및 문제 해결 시 다음과 같은 여러 도구 및 기법을 사용할 수 있습니다.

* 작업 대시보드에서 [요청 성능 로그](/help/sites-administering/operations-dashboard.md#request-performance)를 검사할 수 있습니다. 이 도구를 사용하여 느린 페이지 요청을 식별할 수 있습니다.
* [쿼리 성능 도구를 사용하여 느린 실행 쿼리 분석](/help/sites-administering/operations-dashboard.md#query-performance)

* 오류 또는 경고가 있는지 확인하십시오. 자세한 내용은 [로깅](/help/sites-deploying/configure-logging.md)을 참조하십시오.
* 메모리 및 CPU 사용, 디스크 I/O 또는 네트워크 I/O와 같은 시스템 하드웨어 리소스를 모니터링합니다.이러한 리소스는 종종 성능 병목 현상의 원인이 됩니다.
* URL 매개 변수의 사용을 최소화하여 가능한 한 많은 캐싱을 허용하도록 페이지의 아키텍처 및 주소 지정 방식을 최적화합니다.
* [성능 최적화](/help/sites-deploying/configuring-performance.md) 및 [성능 조정 팁](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) 설명서를 따르십시오.

* 작성 인스턴스에서 특정 페이지 또는 구성 요소를 편집할 때 문제가 발생하면 TouchUI 개발자 모드를 사용하여 해당 페이지를 검사합니다. 이렇게 하면 페이지의 각 컨텐츠 영역과 로드 시간이 분류됩니다
* 사이트의 모든 JS 및 CSS를 미니어티화할 수 있습니다. 이 방법에 대한 자세한 내용은 이 [블로그 게시물](https://blogs.adobe.com/foxes/enable-js-and-css-minification/)을 참조하십시오.
* 구성 요소에서 포함된 CSS 및 JS를 제거할 수 있습니다. 페이지를 렌더링하는 데 필요한 요청 수를 최소화하기 위해 이러한 요청을 포함시키고 클라이언트측 라이브러리와 축소해야 합니다
* Chrome의 네트워크 탭과 같은 브라우저 도구를 사용하여 서버 요청을 검사하고 가장 오래 걸리는 서버 요청을 확인합니다.

문제 영역이 식별되면 애플리케이션 코드를 검사하여 성능을 최적화할 수 있습니다. 제대로 작동하지 않는 AEM 기능은 Adobe 지원으로 해결할 수 있습니다.
