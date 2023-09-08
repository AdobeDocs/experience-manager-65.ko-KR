---
title: Headless 애플리케이션 실행 방법
description: 이 AEM Headless 개발자 여정 부분에서는 Headless 애플리케이션을 라이브로 배포하는 방법을 알아봅니다.
exl-id: ec3356ef-9e60-4151-984d-3ebdab593b96
source-git-commit: 9c517590c2b78eed7c52e33e0a106237a2af3bb7
workflow-type: tm+mt
source-wordcount: '1873'
ht-degree: 51%

---

# Headless 애플리케이션 실행 방법 {#go-live}

의 이 부분에서 [AEM Headless 개발자 여정](overview.md), headless 애플리케이션을 라이브로 배포하는 방법에 대해 알아봅니다.

## 지금까지의 스토리 {#story-so-far}

AEM Headless 번역 여정의 이전 문서인 [AEM Assets API를 통해 콘텐츠를 업데이트하는 방법](update-your-content.md)에서 API를 통해 AEM의 기존 Headless 콘텐츠를 업데이트하는 방법에 대해 알아보았습니다. 여기에서 알게 된 내용은 다음과 같습니다.

* AEM Assets HTTP API를 이해합니다.

이 문서는 이러한 기본 사항을 기본으로 하며, 이를 통해 자체 AEM Headless 프로젝트를 준비하여 실행하는 방법을 이해할 수 있습니다.

## 목표 {#objective}

이 문서는 AEM Headless 게시 파이프라인을 이해하고 애플리케이션을 실행하기 전에 알아야 하는 성능을 고려하는 데 도움이 됩니다.

* 필요한 AEM SDK 및 개발 도구에 대해 알아봅니다
* 시작하기 전에 콘텐츠를 시뮬레이션하도록 로컬 개발 런타임을 설정합니다.
* AEM 컨텐츠 복제 및 캐싱 기본 사항 이해
* 실행하기 전 애플리케이션을 안전하게 확장
* 성능 모니터링 및 문제 디버그

## AEM SDK {#the-aem-sdk}

AEM SDK를 사용하여 사용자 정의 코드를 빌드하고 배포합니다. 시작하기 전에 Headless 애플리케이션을 개발하고 테스트해야 하는 주요 도구입니다. 다음 아티팩트가 포함되어 있습니다.

* Quickstart jar - 작성자와 게시 인스턴스를 모두 설정하는 데 사용할 수 있는 실행 가능한 jar 파일
* Dispatcher 도구 - Dispatcher 모듈 및 Windows 및 UNIX 기반 시스템에 대한 종속성
* Java™ API Jar - AEM 개발에 사용할 수 있는 허용된 모든 Java™ API를 노출하는 Java™ Jar/Maven 종속성
* Javadoc jar - Java™ API jar용 javadoc

## 추가 개발 도구 {#additional-development-tools}

AEM SDK 외에도 로컬에서 코드 및 콘텐츠를 개발 및 테스트하는 데 도움이 되는 추가 도구가 필요합니다.

* Java™
* Git
* Apache Maven
* Node.js 라이브러리
* 선택한 IDE

AEM은 Java™ 애플리케이션이므로 AEM as a Cloud Service 개발을 지원하려면 Java™ 및 Java™ SDK를 설치해야 합니다.

Git은 소스 제어를 관리하고 Cloud Manager의 변경 사항을 체크인한 다음 프로덕션 인스턴스에 배포하는 데 사용됩니다.

AEM은 Apache Maven을 사용하여 AEM Maven Project 원형에서 생성된 프로젝트를 빌드합니다. 모든 주요 IDE는 Maven에 대한 통합 지원을 제공합니다.

Node.js는 AEM 프로젝트의 프론트엔드 에셋으로 작업하는 데 사용되는 JavaScript 런타임 환경입니다. `ui.frontend` 하위 프로젝트. Node.js는 JavaScript 종속성을 관리하는 데 사용되는 npm(사실상 Node.js 패키지 관리자)과 함께 배포됩니다.

## AEM 시스템의 구성 요소 개요 {#components-of-an-aem-system-at-a-glance}

다음으로 AEM 환경의 구성 부분을 살펴보겠습니다.

전체 AEM 환경은 작성자, 게시와 Dispatcher로 구성됩니다. 라이브로 전환되기 전에 코드와 컨텐츠를 보다 쉽게 미리 볼 수 있도록 로컬 개발 런타임에서 동일한 구성 요소를 사용할 수 있습니다.

* **Author 서비스**&#x200B;는 내부 사용자가 콘텐츠를 만들고 관리하고 미리 보는 곳입니다.

* **Publish 서비스** 는 &quot;라이브&quot; 환경으로 간주되며 일반적으로 최종 사용자는 이 환경을 사용하여 상호 작용합니다. Author 서비스에서 편집 및 승인된 콘텐츠는 Publish 서비스로 배포(복제)됩니다. AEM Headless 애플리케이션의 가장 일반적인 배포 패턴은 애플리케이션의 프로덕션 버전을 AEM Publish 서비스에 연결하는 것입니다.

* **Dispatcher**&#x200B;는 AEM Dispatcher 모듈로 보강된 정적 웹 서버입니다. 게시 인스턴스에서 생성된 웹 페이지를 캐시하여 성능을 개선합니다.

## 로컬 개발 워크플로 {#the-local-development-workflow}

로컬 개발 프로젝트는 Apache Maven을 기반으로 빌드되어 소스 제어에 Git을 사용합니다. 프로젝트를 업데이트하려면 개발자는 Eclipse, Visual Studio Code 또는 IntelliJ 등 권장되는 통합 개발 환경을 사용할 수 있습니다.

Headless 애플리케이션에서 수집하는 코드 또는 콘텐츠 업데이트를 테스트하려면 로컬 AEM 런타임에 업데이트를 배포합니다. 여기에는 AEM 작성자 및 게시 서비스의 로컬 인스턴스가 포함됩니다.

가장 중요한 위치에서 업데이트를 테스트해야 하므로 로컬 AEM 런타임에서 각 구성 요소의 차이를 메모해 두십시오. 예를 들어 작성자의 콘텐츠 업데이트를 테스트하거나 게시 인스턴스의 새 코드를 테스트합니다.

프로덕션 시스템에서 Dispatcher 및 http Apache 서버는 항상 AEM 게시 인스턴스 앞에 있습니다. 캐싱 및 보안 서비스를 AEM 시스템에 제공하므로 Dispatcher에 대한 코드 및 콘텐츠 업데이트를 테스트해야 합니다.

## 로컬 개발 환경을 사용하여 로컬에서 코드 및 콘텐츠 미리보기 {#previewing-your-code-and-content-locally-with-the-local-development-environment}

AEM Headless 프로젝트를 시작하도록 준비하려면 프로젝트의 모든 구성 부분이 제대로 작동하는지 확인하십시오.

이를 위해서는 코드, 콘텐츠 및 구성과 같은 모든 것을 통합하고 Go-Live 준비를 위해 로컬 개발 환경에서 테스트해야 합니다.

로컬 개발 환경은 다음 세 가지 주요 영역으로 구성됩니다.

1. AEM 프로젝트 - AEM 개발자가 작업할 모든 사용자 지정 코드, 구성 및 콘텐츠가 포함됩니다
1. 로컬 AEM 런타임 - AEM 프로젝트에서 코드 배포에 사용되는 AEM 작성자 및 게시 서비스의 로컬 버전
1. 로컬 Dispatcher 런타임 - Dispatcher 모듈이 포함된 Apache htttpd 웹 서버의 로컬 버전

로컬 개발 환경이 설정되면 정적 노드 서버를 로컬로 배포하여 React 앱에 제공하는 콘텐츠를 시뮬레이션할 수 있습니다.

로컬 개발 환경 및 콘텐츠 미리 보기에 필요한 모든 종속성 설정에 대해 자세히 알아보려면 를 참조하십시오. [프로덕션 배포 설명서](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/overview.html?lang=en).

## Go-Live를 위해 AEM Headless 애플리케이션 준비 {#prepare-your-aem-headless-application-for-golive}

<!-- Start of CDN Review -->

이제 아래에 요약된 모범 사례를 따라 AEM Headless 애플리케이션을 시작할 준비가 되었습니다.

### 실행 전 Headless 애플리케이션 보안 {#secure-and-scale-before-launch}

1. 준비 [인증](/help/sites-developing/headless/graphql-api/graphql-authentication-content-fragments.md) GraphQL 요청에 대한

### 모델 구조와 GraphQL 출력 비교 {#structure-vs-output}

* 15KB 이상의 JSON(gzip 압축)을 출력하는 쿼리를 만들지 마십시오. 긴 JSON 파일은 리소스 집약으로 클라이언트 애플리케이션이 구문 분석할 수 있습니다.
* 중첩된 조각 계층 수준이 5단계를 초과하지 않도록 하십시오. 수준이 추가되면 콘텐츠 작성자는 변경 사항이 미치는 영향을 고려할 수 없습니다.
* 모델 내 종속성 계층이 있는 쿼리를 모델링하는 대신 여러 오브젝트 쿼리를 사용합니다. 이렇게 하면 장기간 동안 많은 콘텐츠 변경 작업을 수행하지 않고도 JSON 출력을 재구성할 수 있습니다.

### CDN 캐시 적중률 최대화 {#maximize-cdn}

* 표면에서 라이브 콘텐츠를 요청하지 않는 한 GraphQL 쿼리를 직접 사용하지 마십시오.
   * 가능하면 지속 쿼리를 사용합니다.
   * CDN이 캐시할 수 있도록 600초 이상의 CDN TTL을 제공합니다.
   * AEM은 모델 변경이 기존 쿼리에 미치는 영향을 계산할 수 있습니다.
* 낮은 콘텐츠 변경률과 높은 콘텐츠 변경률 간에 JSON 파일/GraphQL 쿼리를 분할하여 CDN에 대한 클라이언트 트래픽을 줄이고 더 높은 TTL을 할당합니다. 이렇게 하면 원본 서버와 함께 JSON의 유효성을 다시 검사하는 CDN이 최소화됩니다.
* CDN에서 콘텐츠를 무효화하려면 소프트 제거를 사용합니다. 이렇게 하면 CDN에서 캐시 누락을 발생시키지 않고 콘텐츠를 다시 다운로드할 수 있습니다.

>[!NOTE]
>
>다음을 참조하십시오 [추가 리소스](#additional-resources) cdn 및 캐싱에 대한 자세한 내용은 을 참조하십시오.

### Headless 콘텐츠 다운로드 시간 개선 {#improve-download-time}

* HTTP 클라이언트가 HTTP/2를 사용하는지 확인합니다.
* HTTP 클라이언트가 gzip에 대한 헤더 요청을 수락하는지 확인합니다.
* JSON과 참조된 아티팩트를 호스팅하는 데 사용되는 도메인 수를 최소화합니다.
* 사용 `Last-modified-since` 리소스를 새로 고칩니다.
* JSON 파일의 `_reference`출력을 사용하여 전체 JSON 파일을 구문 분석하지 않고도 자산 다운로드를 시작합니다.

<!-- End of CDN Review -->

## 프로덕션에 배포 {#deploy-to-production}

프로덕션에 배포는 다음을 보유하고 있는지 여부에 따라 달라질 수 있습니다 *기존* Maven을 사용하여 배포하거나 Adobe Managed Services(AMS)에 있으므로 Cloud Manager를 사용하는 AEM 인스턴스.

## Maven을 사용하여 프로덕션에 배포 {#deploy-to-production-maven}

의 경우 *기존* Maven을 사용한 배포(AMS 이외), [WKND 자습서](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=en#build) 개요를 참조하십시오.

## Cloud Manager를 사용하여 프로덕션에 배포 {#deploy-to-production-cloud-manager}

Cloud Manager를 사용하는 AMS 고객의 경우 모든 것이 테스트되고 제대로 작동하는지 확인한 후 코드 업데이트를 [Cloud Manager의 중앙 집중식 Git 저장소](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html).

업데이트가 Cloud Manager에 업로드된 후 다음을 사용하여 AEM에 배포합니다. [Cloud Manager의 CI/CD 파이프라인](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-deployment.html).

<!-- Can't find a parallel link -->
<!--
You can start deploying your code by leveraging the Cloud Manager CI/CD pipeline, which is covered extensively [here](/help/implementing/deploying/overview.md).
-->

## 성능 모니터링 {#performance-monitoring}

사용자가 AEM Headless 애플리케이션 사용 시 최상의 사용자 경험이 있으면 아래에 설명된 핵심 성능 지표를 모니터링해야 합니다.

* 앱의 미리보기 및 프로덕션 버전 확인
* 현재 서비스 가용성 상태에 대한 AEM 상태 페이지 확인
* 성능 보고서 액세스
   * 게재 성능
      * 원본 서버 - 호출 수, 오류율, CPU 로드, 페이로드 트래픽
   * 작성자 성능
      * 사용자 수, 요청 및 로드 확인
* 앱 및 공간별 성능 보고서 액세스
   * 서버가 가동되면 일반 지표가 녹색/주황색/빨간색인지 확인한 다음 특정 앱 문제를 식별합니다.
   * 위에서 앱이나 공간(예: Photoshop 데스크탑, 페이월)으로 필터링한 동일한 보고서 열기
   * Splunk 로그 API를 사용하여 서비스 및 애플리케이션 성능에 액세스
   * 다른 문제가 있는 경우 고객 지원 팀에 문의하십시오.

## 문제 해결 {#troubleshooting}

### 디버깅 {#debugging}

다음 모범 사례에 따라 디버깅에 대한 일반적인 방식을 사용합니다.

* 애플리케이션의 미리보기 버전을 사용하여 기능 및 성능 확인
* 애플리케이션의 프로덕션 버전을 사용하여 기능 및 성능 확인
* 콘텐츠 조각 편집기의 JSON 미리보기를 사용하여 확인
* 클라이언트 애플리케이션 또는 게재 문제가 있는지 확인하려면 클라이언트 애플리케이션에서 JSON을 검사하십시오
* 캐시된 콘텐츠 또는 AEM과 관련된 문제가 있는지 확인하려면 GraphQL을 사용하여 JSON을 검사합니다

### 지원을 통해 버그 로깅 {#logging-a-bug-with-support}

지원이 더 필요한 경우 지원을 통해 버그를 효율적으로 기록하려면 다음 단계를 완료하십시오.

* 문제 발생 시 필요한 경우 스크린샷 찍기
* 문제를 재현하는 방식 문서화
* 문제가 재현되는 콘텐츠 문서화
* 적합한 우선 순위로 AEM 지원 포털을 통해 문제 로깅

## 여정 종료 - 종료되었습니까? {#journey-ends}

축하합니다! AEM Headless 개발자 번역 여정을 완료하셨습니다! 이제 다음 사항을 이해할 수 있어야 합니다.

* Headless 콘텐츠 게재와 Headful 콘텐츠 게재의 차이점.
* AEM의 Headless 기능.
* AEM Headless 프로젝트를 구성하고 방법.
* AEM에서 Headless 콘텐츠를 만드는 방법
* AEM에서 Headless 콘텐츠를 검색하여 업데이트하는 방법.
* AEM Headless 프로젝트를 실행하는 방법.
* Go-Live 완료 후 수행할 작업.

첫 번째 AEM Headless 프로젝트를 이미 시작했거나 이제 모든 지식을 갖추고 있습니다. 좋습니다!

### 단일 페이지 애플리케이션 살펴보기 {#explore-spa}

그러나 AEM에서 헤드리스 매장을 중단할 필요는 없습니다. 다음에서 [여정의 시작 부분](getting-started.md#integration-levels)에서는 AEM이 headless 전달 및 기존 전체 스택 모델을 지원하는 방법뿐만 아니라 두 가지 모두의 장점을 결합한 하이브리드 모델을 지원하는 방법에 대해 논의했습니다.

이러한 유연성이 프로젝트에 필요한 사항인 경우 여정의 선택적 추가 부분으로 계속 진행하십시오. [AEM으로 단일 페이지 애플리케이션(SPA)을 만드는 방법](create-spa.md)

## 추가 리소스 {#additional-resources}

* [AEM 개발 안내서](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/the-basics.html?lang=en)

* [WKND 자습서](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en)

* [AEM용 Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=ko)

* CDN 캐시

   * [CDN 캐시 제어](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#controlling-a-cdn-cache)

   * 구성 [CDN 재작성기](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html) (*cdn 재작성기 검색*)

* [AEM as a Headless CMS 소개](/help/sites-developing/headless/introduction.md)
* [AEM 개발자 포털](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html)
* [AEM의 Headless Tutorials](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)
