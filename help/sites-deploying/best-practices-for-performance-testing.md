---
title: 성능 테스트 우수 사례
seo-title: Best Practices for Performance Testing
description: 성능 테스트에 사용되는 전체 전략 및 방법론과 프로세스에 도움이 되는 툴 중 일부를 간략하게 설명합니다.
seo-description: This article outlines the overall strategies and methodologies used for performance testing as well as some of the tools that are available to assist in the process.
uuid: ab8720d6-b864-4d00-9e07-2e1699cfe7db
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 669018a0-f6ef-42b2-9c6f-83d7dd5a7095
exl-id: fcac75e1-15c1-4a37-8d43-93c95267b903
source-git-commit: b6de561422bc3533eef153b13d2c65b4cb7e0387
workflow-type: tm+mt
source-wordcount: '1897'
ht-degree: 0%

---

# 성능 테스트 우수 사례{#best-practices-for-performance-testing}

## 소개 {#introduction}

성능 테스트는 AEM 배포의 중요한 부분입니다. 고객 요구 사항에 따라 게시 인스턴스, 작성자 인스턴스 또는 둘 다에서 성능 테스트를 수행할 수 있습니다.

이 설명서는 성능 테스트를 수행하는 전반적인 전략 및 방법론과 Adobe이 프로세스를 지원하기 위해 사용할 수 있는 일부 도구에 대해 설명합니다. 마지막으로, 코드 분석과 시스템 구성 관점에서 AEM 6에서 사용할 수 있는 일부 도구를 성능 조정에 도움을 줄 것입니다.

### 현실 시뮬레이션 {#simulating-reality}

성능 테스트를 수행할 때 가장 중요한 것은 프로덕션 환경을 가능한 한 가깝게 모방하도록 하는 것입니다. 이 작업은 종종 어려울 수 있지만 이러한 테스트의 정확성을 확인하는 것이 중요합니다. 성능 테스트를 디자인할 때는 다음 사항을 고려해야 합니다.

* 프로덕션 유사 콘텐츠

AEM의 많은 성능 측정(예: 쿼리 응답 시간)은 시스템의 컨텐츠 크기에 의해 영향을 받을 수 있습니다. 테스트 환경에 프로덕션 데이터의 사본이 가능한 한 가까이 있는지 확인하는 것이 중요합니다.

* 프로덕션 코드

프로덕션에 배포된 AEM 버전 및 핫픽스는 테스트 환경에서 동일해야 합니다. 또한 프로덕션에 배포되는 코드의 버전을 테스트하는 것이 중요합니다.

* 운영 방식의 하드웨어 및 네트워크 구성

가능한 한 가깝게 제작과 유사한 환경이 없으면 시험은 의미가 없을 것이다. 가장 좋은 방법은 하드웨어 사양, 네트워크 인터페이스, 로드 밸런서 및 CDN은 테스트 환경의 프로덕션과 동일해야 합니다.

* 프로덕션 로드

시스템에 많은 로드가 발생할 때까지 많은 성능 문제가 표시되지 않습니다. 성능 테스트를 잘 수행하면 프로덕션 시스템이 최대 수준에 있을 때의 부하를 시뮬레이션해야 합니다.

### 목표 설정 {#setting-goals}

성능 테스트를 시작하기 전에 로드 및 응답 시간을 지정하려면 작동하지 않는 요구 사항을 설정해야 합니다. 기존 시스템에서 마이그레이션하는 경우 응답 시간이 현재 프로덕션 값과 비슷한지 확인합니다. 부하의 경우 현재 피크 부하를 가져다가 두 배로 늘리는 것이 가장 좋습니다. 이렇게 하면 웹 사이트가 계속 잘될 수 있습니다.

### 도구 {#tools}

시장에 상업적으로 이용할 수 있는 성능 테스트 도구가 많이 있습니다. 로드 생성 도구를 실행할 때는 테스트를 수행하는 컴퓨터에 충분한 네트워크 대역폭이 있는지 확인해야 합니다. 그렇지 않으면 테스트 컴퓨터가 연결 제한에 도달하면 테스트 중인 환경에서 추가 로드가 생성되지 않습니다.

#### 테스트 도구 {#testing-tools}

* Adobe **Tough Day** AEM 인스턴스에서 로드를 생성하고 성능 데이터를 수집하는 데 도구를 사용할 수 있습니다. Adobe의 AEM 엔지니어링 팀은 실제로 도구를 사용하여 AEM 제품 자체의 로드 테스트를 수행합니다. Tough Day에서 실행되는 스크립트는 속성 파일과 JMX XML 파일을 통해 구성됩니다. 자세한 내용은 [Tough Day 설명서](/help/sites-developing/tough-day.md).

* AEM은 문제 쿼리, 요청 및 오류 메시지를 빠르게 볼 수 있는 기본 도구를 제공합니다. 자세한 내용은 [진단 도구](/help/sites-administering/operations-dashboard.md#diagnosis-tools) 작업 대시보드 설명서의 섹션을 참조하십시오.
* Apache는 **JMeter** 성능 및 로드 테스트와 기능 동작에 사용할 수 있습니다. 오픈 소스 소프트웨어이며 자유롭게 사용할 수 있지만, 엔터프라이즈 제품보다 더 작은 기능 세트와 더 빠른 학습 곡선이 있습니다. JMeter는 Apache 웹 사이트( )에서 찾을 수 있습니다. [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **로드 런너** 는 엔터프라이즈급 로드 테스트 제품입니다. 무료 평가 버전이 제공됩니다. 자세한 내용은 [https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)

* 과 같은 클라우드 기반 로드 테스트 도구 [노이스타](https://www.neustar.biz/services/web-performance/load-testing) 사용할 수도 있습니다.
* 모바일 또는 응답형 웹 사이트를 테스트할 때는 별도의 도구 세트를 사용해야 합니다. 네트워크 대역폭을 조절하여 3G 또는 EDGE와 같은 느린 모바일 연결을 시뮬레이션하여 작동합니다. 널리 사용되는 도구 중에는 다음과 같습니다.

   * **[네트워크 링크 컨디셔너](https://nshipster.com/network-link-conditioner/)** - 사용하기 쉬운 UI를 제공하고 네트워킹 스택에서 매우 낮은 수준에서 작동합니다. 여기에는 OS X 및 iOS 버전이 포함되어 있습니다.
   * [**Charles**](https://www.charlesproxy.com/) - 여러 가지 다른 용도 외에 네트워크 조절 기능을 제공하는 웹 디버깅 프록시 애플리케이션입니다. 버전은 Windows, OS X 및 Linux용 제공됩니다.

#### 최적화 도구 {#optimization-tools}

**모니터링**

다음 [성능 모니터링](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) 설명서는 문제를 진단하고 튜닝할 영역을 파악하는 데 사용할 수 있는 도구와 방법에 대한 유용한 리소스입니다.

**Touch UI의 개발자 모드**

AEM 6의 터치 UI에 새로운 기능 중 하나는 개발자 모드입니다. 작성자가 편집 모드와 미리 보기 모드 간을 전환할 수 있듯이 개발자는 작성자 UI에서 개발자 모드로 전환하여 페이지의 각 구성 요소에 대한 렌더링 시간을 확인하고 오류 스택의 추적을 볼 수 있습니다. 개발자 모드에 대한 자세한 내용은 다음을 참조하십시오 [CQ Gems 프레젠테이션](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html).

**rlog.jar를 사용하여 요청 로그를 읽습니다.**

AEM 시스템에서 요청 로그를 보다 포괄적으로 분석하려면 `rlog.jar` 를 사용하여 을 검색하고 정렬할 수 있습니다 `request.log` AEM에서 생성하는 파일입니다. 이 jar 파일은 의 AEM 설치에 포함되어 있습니다. `/crx-quickstart/opt/helpers` 폴더를 입력합니다. 로그 도구 및 일반적으로 요청 로그에 대한 자세한 내용은 [모니터링 및 유지 관리](/help/sites-deploying/monitoring-and-maintaining.md) 설명서.

**쿼리 설명 도구**

다음 [쿼리 도구 설명](/help/sites-administering/operations-dashboard.md#explain-query) acs AEM 도구에서 쿼리를 실행할 때 사용되는 인덱스를 보는 데 사용할 수 있습니다. 이 기능은 느린 실행 쿼리를 최적화할 때 매우 유용할 수 있습니다.

**PageSpeed 도구**

Google의 PageSpeed 도구는 페이지 성능에 대한 우수 사례 및 추가적인 최적화를 위해 Apache 인스턴스의 dispatcher와 함께 설치할 수 있는 플러그인을 준수하기 위해 사이트 분석을 제공합니다. 자세한 내용은 [PageSpeed 도구 웹 사이트](https://developers.google.com/speed/pagespeed/).

## 작성 환경 {#author-environment}

### 테스트 수행 {#performing-tests}

작성 환경에서 성능 테스트를 수행하려면 프로덕션 작성자의 경험을 시뮬레이션해야 합니다. 즉, 작성자 설치에는 프로덕션 작성 인스턴스에 대해 보유하고 있는 모든 구성 요소, OSGi 번들, UI 사용자 지정, 사용자 지정 인덱스 및 기타 추가 사항이 포함되어야 합니다.

성능 및 로드 테스트를 위해 설계된 다양한 자동화 프레임워크를 사용할 수 있습니다. 사용자 지정 스크립트를 이러한 도구에 기록한 다음 다시 재생하여 유사한 컨텐츠 작성 및 활성화 활동을 동시에 수행하는 최대 수의 작성자를 시뮬레이션할 수 있습니다. 수천 개의 자산을 업로드하거나 많은 수의 페이지를 활성화하는 것과 같은 활동을 시뮬레이션하려면 거친 날 도구를 사용하는 것이 좋습니다.

자산 로드 또는 페이지 작성 요구 사항이 많은 환경 유형의 경우 환경이 최대 로드 상태에서 효율적으로 작동할 수 있도록 Tough Day와 같은 도구를 사용해야 합니다. [WebDAV](/help/sites-administering/webdav-access.md) 는 스크립팅이 필요하지 않으며 대량의 자산을 로드하는 데 사용할 수도 있는 도구입니다.

#### MongoDB 특정 단계 {#mongodb-specific-steps}

MongoDB 백엔드가 있는 시스템에서 AEM은 다음과 같은 몇 가지 기능을 제공합니다 [JMX](/help/sites-administering/jmx-console.md) 로드 또는 성능 테스트를 수행할 때 모니터링해야 하는 MB를 의미합니다.

* 다음 **통합 캐시 통계** MBean. 다음 위치로 이동하여 직접 액세스할 수 있습니다.

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

캐시 이름이 **Document-Diff**&#x200B;를 반환하고, 적중률은 넘어야 합니다 `.90`. 적중률이 90% 미만인 경우, 을 수정해야 할 수 있습니다 `DocumentNodeStoreService` 구성. Adobe 제품 지원을 통해 환경에 대한 최적의 설정을 추천할 수 있습니다.

* 다음 **Oak 저장소 통계** Mbean. 다음 위치로 이동하여 직접 액세스할 수 있습니다.

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

다음 **ObservationQueueMaxLength** 섹션에는 지난 시간, 분, 초 및 주 동안 Oak의 관찰 큐에 있는 이벤트 수가 표시됩니다. &quot;시간당&quot; 섹션에서 가장 큰 이벤트 수를 찾습니다. 이 숫자를 `oak.observation.queue-length` 설정 관찰큐에 표시된 최대 수가 `queue-length` 설정:

1. 이름이 인 파일을 만듭니다. `com.adobe.granite.repository.impl.SlingRepositoryManager.cfg` 매개 변수 포함 `oak.observation.queue‐length=50000`
1. /crx-quickstart/install 폴더 아래에 배치합니다.

>[!NOTE]
>KB 문서 참조 [AEM 6.x | 성능 조정 팁](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)

기본 설정은 10,000이지만, 대부분의 배포에서는 일반적으로 20,000 또는 50,000으로 늘려야 합니다.

## 게시 환경 {#publish-environment}

### 테스트 수행 {#performing-tests-1}

로드 테스트를 수행해야 하는 배포의 가장 중요한 부분은 게시 또는 디스패처 환경에 직면하는 최종 사용자입니다.

타사 자동화된 테스트 도구를 사용하여 웹 사이트의 성능을 테스트할 수 있습니다. 이러한 도구를 사용하면 사용자가 사이트에서 거치는 단계를 기록하고 동시에 이러한 여러 세션을 실행하여 프로덕션 웹 사이트의 일반적인 로드를 시뮬레이션할 수 있습니다.

대부분의 프로덕션 웹 사이트에는 디스패처 캐싱 및 콘텐츠 전달 네트워크와 같은 최적화 기능이 설정되어 있습니다. 테스트할 때 이러한 최적화를 테스트 환경에서도 사용할 수 있는지 확인해야 합니다. 최종 사용자에 대한 응답 시간을 모니터링하는 것 외에도, 시스템이 하드웨어 리소스에 의해 제한되지 않도록 게시 서버 및 디스패처에서 시스템 지표를 모니터링해야 합니다.

높은 수준의 개인화가 필요하지 않은 시스템에서 디스패처는 대부분의 요청을 캐시해야 합니다. 따라서 게시 인스턴스의 로드는 상대적으로 균일하게 유지되어야 합니다. 높은 수준의 개인화가 필요한 경우 최대한 디스패처 캐싱을 허용하기 위해 개인화된 콘텐츠에 iFrame 또는 AJAX 요청 등의 기술을 사용하는 것이 좋습니다.

기본 테스트의 경우 Apache Bench를 사용하여 웹 서버 응답 시간을 측정하고 메모리 누출과 같은 측정 작업을 위한 로드를 생성할 수 있습니다. 자세한 내용은 [모니터링 설명서](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench).

## 성능 문제 해결 {#troubleshooting-performance-issues}

작성자 인스턴스에서 성능 테스트를 실행한 후 모든 문제를 조사, 진단 및 해결해야 합니다. 분석 및 문제 해결 시 몇 가지 도구와 기술을 사용할 수 있습니다.

* 검사를 할 수 있습니다 [성능 로그 요청](/help/sites-administering/operations-dashboard.md#request-performance) 를 클릭합니다. 이 도구를 사용하여 느린 페이지 요청을 식별할 수 있습니다
* 를 사용하여 느린 실행 쿼리 분석 [쿼리 성능 도구](/help/sites-administering/operations-dashboard.md#query-performance)

* 오류 또는 경고 오류를 확인하십시오. 자세한 내용은 [로깅](/help/sites-deploying/configure-logging.md)
* 메모리 및 CPU 사용률, 디스크 I/O 또는 네트워크 I/O와 같은 시스템 하드웨어 리소스를 모니터링합니다. 이러한 리소스는 종종 성능 병목 현상을 야기합니다
* 페이지의 아키텍처와 주소를 지정하여 URL 매개 변수의 사용을 최소화하여 가능한 한 많은 캐싱을 허용할 수 있습니다
* 다음을 수행합니다 [성능 최적화](/help/sites-deploying/configuring-performance.md) 및 [성능 조정 팁](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) 설명서

* 작성자 인스턴스에서 특정 페이지 또는 구성 요소를 편집하는 데 문제가 있는 경우 TouchUI 개발자 모드를 사용하여 해당 페이지를 검사합니다. 이렇게 하면 페이지의 각 콘텐츠 영역과 로드 시간이 분류됩니다
* 사이트의 모든 JS 및 CSS를 축소합니다. 이 작업을 수행하는 방법에 대한 자세한 내용은 다음을 참조하십시오 [블로그 게시물](https://blogs.adobe.com/foxes/enable-js-and-css-minification/).
* 구성 요소에서 포함된 CSS 및 JS를 제거합니다. 페이지를 렌더링하는 데 필요한 요청 수를 최소화하기 위해 클라이언트 측 라이브러리에 포함되고 축소해야 합니다
* Chrome의 네트워크 탭과 같은 브라우저 도구를 사용하여 서버 요청을 검사하고 가장 오래 걸리는 항목을 확인할 수 있습니다.

문제 영역을 식별하면 애플리케이션 코드에서 성능 최적화를 검사할 수 있습니다. 제대로 작동하지 않는 즉시 사용 가능한 AEM 기능은 Adobe 지원 기능을 통해 해결할 수 있습니다.
