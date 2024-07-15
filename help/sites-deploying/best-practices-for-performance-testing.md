---
title: 성능 테스트 우수 사례
description: 성능 테스트에 사용되는 전반적인 전략 및 방법론과 프로세스에 도움이 되는 몇 가지 도구에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: fcac75e1-15c1-4a37-8d43-93c95267b903
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1790'
ht-degree: 0%

---

# 성능 테스트 우수 사례{#best-practices-for-performance-testing}

## 소개 {#introduction}

성능 테스트는 AEM 배포의 중요한 부분입니다. 고객 요구 사항에 따라 게시 인스턴스, 작성자 인스턴스 또는 둘 다에서 성능 테스트를 수행할 수 있습니다.

이 설명서에서는 성능 테스트를 수행하는 전반적인 전략 및 방법론과 프로세스를 지원하기 위해 Adobe에서 사용할 수 있는 몇 가지 도구에 대해 설명합니다. 마지막으로, 코드 분석 및 시스템 구성 측면에서 성능 조정을 지원하기 위해 AEM 6에서 사용할 수 있는 도구에 대한 분석을 읽어 보십시오.

### 현실 시뮬레이션 {#simulating-reality}

성능 테스트를 수행할 때는 프로덕션 환경을 최대한 가깝게 모방해야 합니다. 이러한 작업은 종종 어려울 수 있지만 이러한 테스트의 정확성을 보장하는 것이 중요합니다. 성능 테스트를 디자인하는 동안 다음 사항을 고려하는 것이 중요합니다.

* 프로덕션 유사 콘텐츠

쿼리 응답 시간과 같은 AEM의 많은 성능 측정은 시스템의 콘텐츠 크기에 의해 영향을 받을 수 있습니다. 테스트 환경에서 가능한 한 프로덕션 데이터의 복제본을 닫도록 하는 것이 중요합니다.

* 프로덕션 코드

프로덕션에 배포된 AEM 버전 및 핫픽스는 테스트 환경에서 동일해야 합니다. 프로덕션에 배포된 코드 버전을 테스트하는 것도 중요합니다.

* 운영 하드웨어 및 네트워크 구성

최대한 제작과 비슷한 환경이 없으면 테스트는 의미가 없다. 하드웨어 사양, 네트워크 인터페이스, 로드 밸런서 및 CDN은 테스트 환경의 프로덕션과 동일해야 합니다.

* 프로덕션 로드

시스템에 과부하가 걸릴 때까지 많은 성능 문제가 표시되지 않습니다. 좋은 성능 테스트는 프로덕션 시스템이 최대 속도로 작동하는 로드를 시뮬레이션해야 합니다.

### 목표 설정 {#setting-goals}

성능 테스트를 시작하기 전에 로드 및 응답 시간을 지정하기 위해 비기능 요구 사항을 설정해야 합니다. 기존 시스템에서 마이그레이션하는 경우 응답 시간이 현재 프로덕션 값과 유사한지 확인하십시오. 부하의 경우 현재 피크 부하를 받아서 두 배로 늘리는 것이 가장 좋습니다. 이렇게 하면 웹 사이트가 성장하는 동안 계속 우수한 성능을 유지할 수 있습니다.

### 도구 {#tools}

시중에 나와 있는 성능 테스트 도구는 매우 다양합니다. 부하 생성 도구를 실행할 때는 테스트를 수행하는 컴퓨터의 네트워크 대역폭이 충분한지 확인하는 것이 중요합니다. 그렇지 않으면 테스트 시스템이 연결 한도에 도달하면 테스트 중인 환경에 추가 로드가 생성되지 않습니다.

#### 테스트 도구 {#testing-tools}

* Adobe의 **힘든 날** 도구를 사용하여 AEM 인스턴스에 대한 로드를 생성하고 성능 데이터를 수집할 수 있습니다. Adobe의 AEM 엔지니어링 팀은 실제로 도구를 사용하여 AEM 제품 자체의 부하 테스트를 수행합니다. Tough Day에서 실행되는 스크립트는 속성 파일과 JMX XML 파일을 통해 구성됩니다. 자세한 내용은 [힘든 날 설명서](/help/sites-developing/tough-day.md)를 참조하세요.

* AEM은 문제가 있는 쿼리, 요청 및 오류 메시지를 빠르게 볼 수 있는 기본 도구를 제공합니다. 자세한 내용은 작업 대시보드 설명서의 [진단 도구](/help/sites-administering/operations-dashboard.md#diagnosis-tools) 섹션을 참조하십시오.
* Apache는 성능 및 로드 테스트 및 기능 동작에 사용할 수 있는 **JMeter**(이)라는 제품을 제공합니다. 오픈 소스 소프트웨어이며 자유롭게 사용할 수 있지만, 엔터프라이즈 제품보다 기능 세트가 작고 학습 곡선이 더 가파르다. JMeter는 Apache 웹 사이트([https://jmeter.apache.org/](https://jmeter.apache.org/))에서 찾을 수 있습니다.

* **Load Runner**&#x200B;은(는) 엔터프라이즈급 부하 테스트 제품입니다. 무료 평가 버전을 사용할 수 있습니다. 자세한 내용은 [https://www.microfocus.com/en-us/portfolio/performance-engineering/overview](https://www.microfocus.com/en-us/portfolio/performance-engineering/overview)을(를) 참조하십시오.

* [Vercara](https://vercara.com/website-performance-management)과(와) 같은 웹 사이트 로드 테스트 도구를 사용할 수도 있습니다.
* 모바일 또는 반응형 웹 사이트를 테스트할 때 별도의 도구 세트를 사용해야 합니다. 네트워크 대역폭을 조절하거나 3G 또는 EDGE과 같은 느린 모바일 연결을 시뮬레이션하여 작동합니다. 보다 널리 사용되는 도구 중 하나는 다음과 같습니다.

   * **[네트워크 링크 컨디셔너](https://nshipster.com/network-link-conditioner/)** - 사용하기 쉬운 UI를 제공하며 네트워킹 스택에서 매우 낮은 수준에서 작동합니다. 여기에는 OS X 및 iOS 버전이 포함됩니다.
   * [**Charles**](https://www.charlesproxy.com/) - 다른 여러 사용 외에 네트워크 제한을 제공하는 웹 디버깅 프록시 응용 프로그램입니다. Windows, OS X 및 Linux®용 버전이 제공됩니다.

#### 최적화 도구 {#optimization-tools}

**모니터링**

[성능 모니터링](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) 설명서는 문제를 진단하고 튜닝할 영역을 찾는 데 사용할 수 있는 도구와 방법에 적합한 리소스입니다.

Touch UI의 **개발자 모드**

AEM 6의 터치 UI에 있는 새로운 기능 중 하나는 개발자 모드입니다. 작성자가 편집 모드와 미리보기 모드 간을 전환할 수 있는 것처럼 개발자는 작성자 UI에서 개발자 모드로 전환할 수 있습니다. 이렇게 하면 페이지의 각 구성 요소에 대한 렌더링 시간을 확인하고 오류에 대한 스택 추적을 볼 수 있습니다. 개발자 모드에 대한 자세한 내용은 이 [CQ Gems 프레젠테이션](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2014/aem-developer-mode.html)을 참조하세요.

**rlog.jar을 사용하여 요청 로그를 읽습니다**

AEM 시스템에서 요청 로그를 보다 포괄적으로 분석하려면 `rlog.jar`을(를) 사용하여 AEM에서 생성한 `request.log` 파일을 검색하고 정렬할 수 있습니다. 이 jar 파일은 `/crx-quickstart/opt/helpers` 폴더의 AEM 설치에 포함되어 있습니다. rlog 도구 및 요청 로그온 일반에 대한 자세한 내용은 [모니터링 및 유지 관리](/help/sites-deploying/monitoring-and-maintaining.md) 설명서를 참조하십시오.

**쿼리 설명 도구**

ACS AEM 도구의 [쿼리 설명 도구](/help/sites-administering/operations-dashboard.md#explain-query)를 사용하여 쿼리를 실행할 때 사용되는 인덱스를 볼 수 있습니다. 이 도구는 느리게 실행되는 쿼리를 최적화할 때 유용합니다.

**PageSpeed 도구**

Google의 PageSpeed 도구는 페이지 성능에 대한 모범 사례를 준수하기 위한 사이트 분석과 추가적인 최적화를 위해 Apache 인스턴스에 Dispatcher과 함께 설치할 수 있는 플러그인을 제공합니다.
[PageSpeed 도구 웹 사이트](https://developers.google.com/speed)를 참조하세요.

## 작성 환경 {#author-environment}

### 테스트 수행 {#performing-tests}

작성 환경에서 성능 테스트를 수행하려면 프로덕션 작성자의 경험을 시뮬레이션해야 합니다. 즉, 작성자 설치에는 모든 구성 요소, OSGi 번들, UI 사용자 지정, 사용자 지정 인덱스 및 프로덕션 작성자 인스턴스를 위한 다른 추가 사항이 포함되어야 합니다.

성능 및 로드 테스트를 위해 설계된 다양한 자동화 프레임워크가 제공됩니다. 사용자 지정 스크립트는 이러한 도구에 기록한 다음 재생되어 유사한 콘텐츠 생성 및 활성화 활동을 동시에 수행하는 최대 수의 작성자를 시뮬레이션할 수 있습니다. 수천 개의 에셋을 업로드하거나 많은 수의 페이지를 활성화하는 것과 같은 활동을 시뮬레이션하려면 어려운 일 도구를 사용하는 것이 좋습니다.

많은 에셋 로드 또는 페이지 작성의 요구 사항이 있는 환경 유형의 경우 Tough Day와 같은 도구를 사용해야 합니다. 이렇게 하면 환경이 최대 부하 상태에서 효율적으로 작동하게 됩니다. [WebDAV](/help/sites-administering/webdav-access.md)은(는) 스크립팅이 필요하지 않은 도구이며 대량의 자산을 로드하는 데에도 사용할 수 있습니다.

#### MongoDB별 단계 {#mongodb-specific-steps}

MongoDB 백엔드가 있는 시스템에서 AEM은 부하 또는 성능 테스트를 수행할 때 모니터링해야 하는 여러 [JMX](/help/sites-administering/jmx-console.md)MBean을 제공합니다.

* **통합 캐시 통계** MBean. 다음으로 이동하여 직접 액세스할 수 있습니다.

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

이름이 **Document-Diff**&#x200B;인 캐시의 경우 적중률은 `.90`을(를) 넘어야 합니다. 적중률이 90% 미만이면 `DocumentNodeStoreService` 구성을 편집해야 합니다. Adobe 제품 지원은 환경에 가장 적합한 설정을 추천할 수 있습니다.

* **Oak 저장소 통계** Mbean입니다. 다음으로 이동하여 직접 액세스할 수 있습니다.

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

**ObservationQueueMaxLength** 섹션은 지난 시간, 분, 초 및 주에 걸친 Oak 관찰 큐의 이벤트 수를 표시합니다. &quot;시간당&quot; 섹션에서 가장 많은 이벤트를 검색합니다. 이 숫자를 `oak.observation.queue-length` 설정과 비교합니다. 관찰 큐에 대해 표시된 가장 높은 숫자가 `queue-length` 설정을 초과하는 경우:

1. `oak.observation.queue‐length=50000` 매개 변수를 포함하는 `com.adobe.granite.repository.impl.SlingRepositoryManager.cfg` 파일을 만듭니다.
1. /crx-quickstart/install 폴더 아래에 놓습니다.

>[!NOTE]
>[AEM 6.x 보기 | 성능 조정 팁](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html)

기본 설정은 10,000이지만 대부분의 배포에서는 20,000 또는 50,000으로 설정해야 합니다.

## 게시 환경 {#publish-environment}

### 테스트 수행 {#performing-tests-1}

배포에서 로드 테스트의 대상이 되는 가장 중요한 부분은 게시 또는 Dispatcher 환경에 직면한 최종 사용자입니다.

타사 자동화된 테스트 도구를 사용하여 웹 사이트의 성능을 테스트할 수 있습니다. 이러한 도구를 사용하면 사용자가 사이트에서 거치는 단계를 기록하고 이러한 세션 중 많은 세션을 동시에 실행하여 프로덕션 웹 사이트의 일반적인 로드를 시뮬레이션할 수 있습니다.

대부분의 프로덕션 웹 사이트에는 Dispatcher 캐싱 및 콘텐츠 전달 네트워크와 같은 최적화가 적용됩니다. 테스트할 때 테스트 환경에도 이러한 최적화를 사용할 수 있는지 확인하십시오. 최종 사용자의 응답 시간을 모니터링하는 것 외에도 게시 서버 및 디스패처에서 시스템 지표를 모니터링하여 시스템이 하드웨어 리소스에 의해 제한되지 않는지 확인합니다.

높은 수준의 개인화가 필요하지 않은 시스템에서는 Dispatcher이 대부분의 요청을 캐시해야 합니다. 따라서 게시 인스턴스의 로드는 상대적으로 일정하게 유지되어야 합니다. 높은 수준의 개인화가 필요한 경우 가능한 한 많은 Dispatcher 캐싱을 허용할 수 있도록 개인화된 콘텐츠에 대해 iFrame 또는 AJAX 요청과 같은 기술을 사용하는 것이 좋습니다.

기본 테스트의 경우 Apache Bench를 사용하여 웹 서버 응답 시간을 측정하고 메모리 누수와 같은 것을 측정하기 위한 로드를 만들 수 있습니다. [모니터링 설명서](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench)에서 예제를 참조하십시오.

## 성능 문제 해결 {#troubleshooting-performance-issues}

작성자 인스턴스에서 성능 테스트를 실행한 후 문제를 조사, 진단 및 해결해야 합니다. 분석을 수행하고 문제를 해결할 때 여러 가지 도구와 기법을 사용할 수 있습니다.

* 작업 대시보드에서 [요청 성능 로그](/help/sites-administering/operations-dashboard.md#request-performance)를 검사할 수 있습니다. 이 도구를 사용하여 느린 페이지 요청을 식별할 수 있습니다
* [쿼리 성능 도구](/help/sites-administering/operations-dashboard.md#query-performance)를 사용하여 느린 실행 쿼리 분석

* 오류 로그에서 오류 또는 경고를 확인하십시오. 자세한 내용은 [로깅](/help/sites-deploying/configure-logging.md)을 참조하십시오.
* 메모리 및 CPU 사용률, 디스크 I/O 또는 네트워크 I/O와 같은 시스템 하드웨어 리소스를 모니터링합니다. 이러한 리소스는 종종 성능 병목 현상의 원인입니다.
* 페이지의 아키텍처 및 페이지 처리 방법을 최적화하여 URL 매개 변수의 사용을 최소화하여 가능한 한 많은 캐싱을 허용합니다.
* [성능 최적화](/help/sites-deploying/configuring-performance.md) 및 [성능 조정 팁](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html) 설명서를 따르십시오.

* 작성자 인스턴스에서 특정 페이지 또는 구성 요소를 편집하는 데 문제가 있는 경우 TouchUI 개발자 모드를 사용하여 해당 페이지를 검사합니다. 이렇게 하면 페이지의 각 콘텐츠 영역과 로드 시간에 대한 분류가 제공됩니다.
* 사이트의 모든 JS 및 CSS를 축소합니다. 이 [블로그 게시물](https://blogs.adobe.com/foxes/enable-js-and-css-minification/)을 참조하세요.
* 구성 요소에서 포함된 CSS 및 JS를 제거합니다. 페이지 렌더링에 필요한 요청 수를 최소화하기 위해 클라이언트측 라이브러리와 함께 포함되고 축소되어야 합니다.
* 서버 요청을 검사하고 가장 오래 걸리는 요청을 확인하려면 Chrome의 네트워크 탭과 같은 브라우저 도구를 사용합니다.

문제 영역이 식별되면 성능 최적화를 위해 애플리케이션 코드를 검사할 수 있습니다. 제대로 수행되지 않는 AEM 기능은 Adobe 지원에서 해결할 수 있습니다.
