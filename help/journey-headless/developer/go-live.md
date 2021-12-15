---
title: 헤드리스 애플리케이션을 사용하여 라이브로 전환하는 방법
description: AEM Headless Developer 여정의 이 부분에서 헤드리스 애플리케이션을 라이브로 배포하는 방법을 알아봅니다.
source-git-commit: ee82e8edc9cdf7fb403d54d82ced6caa2c95fdc9
workflow-type: tm+mt
source-wordcount: '1903'
ht-degree: 0%

---

# 헤드리스 애플리케이션을 사용하여 라이브로 전환하는 방법 {#go-live}

의 이 부분에서 [AEM Headless Developer 여정](overview.md), 헤드리스 애플리케이션을 라이브로 배포하는 방법을 알아봅니다.

## 지금까지 그 이야기 {#story-so-far}

AEM 헤드리스 여정의 이전 문서에서, [AEM Assets API를 통해 콘텐츠를 업데이트하는 방법](update-your-content.md) API를 통해 AEM에서 기존 헤드리스 콘텐츠를 업데이트하는 방법을 배웠으며 이제 다음을 수행해야 합니다.

* AEM Assets HTTP API를 이해합니다.

이 문서는 이러한 기본 사항을 기반으로 하여 라이브로 전환하기 위해 고유한 AEM 헤드리스 프로젝트를 준비하는 방법을 이해합니다.

## 목표 {#objective}

이 문서는 애플리케이션을 사용하기 전에 AEM 헤드리스 게시 파이프라인과 알아야 하는 성능 고려 사항을 이해하는 데 도움이 됩니다.

* 필요한 AEM SDK 및 개발 도구에 대해 알아봅니다
* 라이브로 전환하기 전에 컨텐츠를 시뮬레이션하도록 로컬 개발 런타임을 설정합니다
* AEM 컨텐츠 복제 및 캐싱 기본 사항 이해
* Launch 전에 애플리케이션 보안 및 확장
* 성능 및 디버그 문제 모니터링

## AEM SDK {#the-aem-sdk}

AEM SDK는 사용자 지정 코드를 작성하고 배포하는 데 사용됩니다. 이 툴은 라이브로 전환하기 전에 헤드리스 애플리케이션을 개발하고 테스트하는 데 필요한 주요 도구입니다. 여기에는 다음 가공물이 포함됩니다.

* Quickstart jar - 작성자 및 게시 인스턴스를 모두 설정하는 데 사용할 수 있는 실행 가능한 jar 파일입니다
* Dispatcher 도구 - Dispatcher 모듈 및 Windows 및 UNIX 기반 시스템에 대한 종속성
* Java API Jar - AEM에 대해 개발하는 데 사용할 수 있는 모든 허용된 Java API를 표시하는 Java Jar/Maven 종속성입니다
* Javadoc jar - Java API jar용 javadocs

## 추가 개발 도구 {#additional-development-tools}

AEM SDK 외에, 코드 및 컨텐츠를 로컬에서 개발 및 테스트할 수 있는 추가 도구가 필요합니다.

* Java
* Git
* Apache Maven
* Node.js 라이브러리
* 원하는 IDE

AEM은 Java 애플리케이션이므로 AEM as a Cloud Service 개발을 지원하려면 Java 및 Java SDK를 설치해야 합니다.

Git은 소스 제어를 관리하고 Cloud Manager의 변경 사항을 체크 인한 다음 프로덕션 인스턴스에 배포하는 데 사용할 수 있습니다.

AEM은 Apache Maven을 사용하여 AEM Maven Project 원형을 통해 생성된 프로젝트를 빌드합니다. 모든 주요 IDE는 Maven에 대한 통합 지원을 제공합니다.

Node.js는 AEM 프로젝트의 프런트 엔드 자산에서 작업하는 데 사용되는 JavaScript 런타임 환경입니다 `ui.frontend` 하위 프로젝트. Node.js는 JavaScript 종속성을 관리하는 데 사용되는 사실상의 Node.js 패키지 관리자인 npm과 함께 배포됩니다.

## AEM 시스템의 구성 요소 개요 {#components-of-an-aem-system-at-a-glance}

다음으로, AEM 환경의 구성 부분을 살펴보겠습니다.

전체 AEM 환경은 작성자, 게시 및 Dispatcher로 구성됩니다. 이러한 동일한 구성 요소가 로컬 개발 런타임에서 사용할 수 있게 되므로 라이브로 전환하기 전에 코드 및 콘텐츠를 보다 쉽게 미리 볼 수 있습니다.

* **작성자 서비스** 는 내부 사용자가 컨텐츠를 만들고, 관리하고, 미리 보는 위치입니다.

* **게시 서비스** 는 &quot;라이브&quot; 환경으로 간주되며 일반적으로 최종 사용자가 상호 작용하는 것입니다. 작성자 서비스에서 편집하고 승인되면 컨텐츠가 게시 서비스에 배포(복제)됩니다. AEM 헤드리스 애플리케이션을 사용하는 가장 일반적인 배포 패턴은 애플리케이션의 프로덕션 버전이 AEM Publish 서비스에 연결되어 있는 것입니다.

* **디스패처** 는 AEM dispatcher 모듈을 사용하여 증강된 정적 웹 서버입니다. 성능을 개선하기 위해 게시 인스턴스에서 생성한 웹 페이지를 캐시합니다.

## 로컬 개발 워크플로우 {#the-local-development-workflow}

로컬 개발 프로젝트는 Apache Maven을 기반으로 구축되었으며 소스 제어에 Git을 사용합니다. 프로젝트를 업데이트하기 위해 개발자는 Eclipse, Visual Studio Code 또는 IntelliJ 등과 같은 선호하는 통합 개발 환경을 사용할 수 있습니다.

헤드리스 애플리케이션에서 수집할 코드 또는 컨텐츠 업데이트를 테스트하려면 AEM 작성자 및 게시 서비스의 로컬 인스턴스를 포함하는 로컬 AEM 런타임에 업데이트를 배포해야 합니다.

업데이트가 가장 중요한 위치를 테스트하는 것이 중요하므로 로컬 AEM 런타임에서 각 구성 요소 간의 차이점을 주의해야 합니다. 예를 들어, 작성자에서 컨텐츠 업데이트를 테스트하거나 게시 인스턴스에서 새 코드를 테스트합니다.

프로덕션 시스템에서 디스패처 및 http Apache 서버는 항상 AEM 게시 인스턴스 앞에 표시됩니다. AEM 시스템에 캐싱 및 보안 서비스를 제공하므로 디스패처에 대한 코드 및 콘텐츠 업데이트를 테스트하는 것이 가장 중요합니다.

## 로컬 개발 환경을 사용하여 로컬로 코드 및 컨텐츠 미리 보기 {#previewing-your-code-and-content-locally-with-the-local-development-environment}

AEM 헤드리스 프로젝트를 시작할 수 있도록 준비하려면 프로젝트의 모든 구성 부분이 제대로 작동하는지 확인해야 합니다.

이를 위해서는 모든 것을 통합해야 합니다. 실시간으로 준비하려면 로컬 개발 환경에서 코드, 컨텐츠 및 구성을 테스트하십시오.

로컬 개발 환경은 다음 세 가지 주요 영역으로 구성됩니다.

1. AEM 프로젝트 - AEM 개발자가 작업하려는 모든 사용자 지정 코드, 구성 및 컨텐츠가 포함됩니다
1. AEM 프로젝트에서 코드를 배포하는 데 사용할 AEM 작성자 및 게시 서비스의 로컬 버전 로컬 AEM 런타임
1. Local Dispatcher 런타임 - Dispatcher 모듈을 포함하는 Apache httpd 웹 서버의 로컬 버전입니다.

로컬 개발 환경이 설정되면 정적 노드 서버를 로컬로 배포하여 React 앱에 대한 콘텐츠 서비스를 시뮬레이션할 수 있습니다.

자세한 내용은 로컬 개발 환경 설정 및 컨텐츠 미리 보기에 필요한 모든 종속성을 참조하십시오. [프로덕션 배포 설명서](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=en#prerequisites).

## AEM Headless Application for Go-Live 준비 {#prepare-your-aem-headless-application-for-golive}

<!-- Start of CDN Review -->

이제 아래에 요약된 우수 사례를 따라 AEM 헤드리스 애플리케이션을 시작할 준비가 되었습니다.

### Launch 전에 헤드리스 애플리케이션 보안 {#secure-and-scale-before-launch}

1. 준비 [인증](/help/assets/content-fragments/graphql-authentication-content-fragments.md) GraphQL 요청에 대해

### 모델 구조와 GraphQL 출력 {#structure-vs-output}

* 15kb 이상의 JSON(gzip 압축)을 출력하는 쿼리를 만들지 마십시오. 긴 JSON 파일은 클라이언트 애플리케이션에서 구문 분석하기 위해 리소스를 많이 사용합니다.
* 5개 이상의 중첩 조각 계층 수준은 피하십시오. 추가 수준을 사용하면 컨텐츠 작성자가 변경 사항의 영향을 고려하기가 어렵습니다.
* 모델 내에서 종속성 계층 구조를 사용하는 쿼리를 모델링하는 대신 다중 개체 쿼리를 사용합니다. 따라서 많은 컨텐츠 변경 작업을 수행하지 않고도 JSON 출력을 재구성할 수 있는 장기적인 유연성을 얻을 수 있습니다.

### CDN 캐시 적중률 최대화 {#maximize-cdn}

* 서피스에서 라이브 컨텐츠를 요청하지 않는 한 직접 GraphQL 쿼리를 사용하지 마십시오.
   * 가능하면 항상 지속적인 쿼리를 사용합니다.
   * CDN이 TTL을 캐시할 수 있도록 600초 이상의 CDN TTL을 제공합니다.
   * AEM에서는 기존 쿼리에 대한 모델 변경의 영향을 계산할 수 있습니다.
* 클라이언트 트래픽을 CDN으로 줄이고 더 높은 TTL을 할당하기 위해 낮은 컨텐츠와 높은 컨텐츠 변경률 간에 JSON 파일/GraphQL 쿼리를 분할합니다. 이렇게 하면 원본 서버와 JSON의 유효성을 다시 검사하는 CDN이 최소화됩니다.
* CDN에서 컨텐츠를 적극적으로 무효화하려면 소프트 삭제를 사용합니다. 이렇게 하면 CDN이 캐시 누락을 유발하지 않고 컨텐츠를 다시 다운로드할 수 있습니다.

>[!NOTE]
>
>자세한 내용은 [추가 리소스](#additional-resources) cdn 및 캐싱에 대한 자세한 정보.

### 헤드리스 컨텐츠 다운로드 시간 개선 {#improve-download-time}

* HTTP 클라이언트가 HTTP/2를 사용하는지 확인합니다.
* HTTP 클라이언트가 gzip에 대한 Headers 요청을 수락하는지 확인합니다.
* JSON 및 참조된 아티팩트를 호스팅하는 데 사용되는 도메인 수를 최소화합니다.
* 활용 `Last-modified-since` 리소스를 새로 고치려면
* 사용 `_reference` 전체 JSON 파일을 구문 분석할 필요 없이 자산 다운로드를 시작하기 위해 JSON 파일에 출력됩니다.

<!-- End of CDN Review -->

## 프로덕션에 배포 {#deploy-to-production}

프로덕션에 배포는 *전통* Maven을 사용하여 배포하거나 AMS(Adobe Managed Services)를 사용하여 Cloud Manager를 사용하는 AEM 인스턴스.

## Maven을 사용하여 프로덕션에 배포 {#deploy-to-production-maven}

대상 *전통* Maven을 사용하여 배포(AMS 아님)를 만들면 [WKND 자습서](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=en#build) 개요

## Cloud Manager를 사용하여 프로덕션에 배포 {#deploy-to-production-cloud-manager}

Cloud Manager를 사용하는 AMS 고객의 경우 모든 것이 테스트되고 제대로 작동하는지 확인한 후 코드 업데이트를 [Cloud Manager의 중앙 집중식 Git 저장소](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html).

업데이트가 Cloud Manager에 업로드되면 다음을 사용하여 AEM에 배포할 수 있습니다 [Cloud Manager의 CI/CD 파이프라인](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

<!-- Can't find a parallel link -->
<!--
You can start deploying your code by leveraging the Cloud Manager CI/CD pipeline, which is covered extensively [here](/help/implementing/deploying/overview.md).
-->

## 성능 모니터링 {#performance-monitoring}

사용자가 AEM 헤드리스 애플리케이션을 사용할 때 최상의 경험을 얻으려면 아래에 자세히 설명된 대로 주요 성능 지표를 모니터링하는 것이 중요합니다.

* 앱의 미리 보기 및 프로덕션 버전 확인
* 현재 서비스 가용성 상태에 대한 AEM 상태 페이지 확인
* 성능 보고서 액세스
   * 게재 성능
      * 원본 서버 - 호출 수, 오류율, CPU 로드, 페이로드 트래픽
   * 작성자 성능
      * 사용자 수, 요청 및 로드 확인
* 앱 및 공간별 성능 보고서 액세스
   * 서버가 작동하면 일반 지표가 녹색/주황색/빨간색 인지 확인한 다음 특정 앱 문제를 식별합니다
   * 앱 또는 공간으로 필터링된 위에서 동일한 보고서 열기(예: Photoshop 데스크탑, 페이월)
   * Splunk 로그 API를 사용하여 서비스 및 응용 프로그램 성능에 액세스합니다
   * 다른 문제가 있을 경우 고객 지원 센터에 문의하십시오.

## 문제 해결 {#troubleshooting}

### 디버깅 {#debugging}

디버깅에 대한 일반적인 접근 방법으로 다음 우수 사례를 따르십시오.

* 응용 프로그램의 미리 보기 버전을 사용하여 기능 및 성능 유효성 검사
* 애플리케이션의 프로덕션 버전을 사용하여 기능 및 성능 확인
* 컨텐츠 조각 편집기의 JSON 미리 보기를 사용하여 유효성 검사
* 클라이언트 애플리케이션의 JSON을 Inspect하여 클라이언트 애플리케이션 또는 배달 문제가 있는지 확인합니다
* GraphQL을 사용하여 JSON을 Inspect에서 캐시된 컨텐츠 또는 AEM과 관련된 문제가 있는지 확인합니다

### 지원을 통해 버그 로깅 {#logging-a-bug-with-support}

추가 지원이 필요한 경우 지원 센터에 버그를 효율적으로 기록하려면 아래 단계를 따르십시오.

* 필요한 경우 문제 스크린샷을 수행합니다
* 문제를 재현할 수 있는 방법을 문서화합니다.
* 문제가 재현되는 내용을 문서화합니다.
* AEM 지원 포털을 통해 적절한 우선 순위로 문제 기록

## 여정이 끝나요? 아니면 끝나요? {#journey-ends}

축하합니다! AEM Headless Developer 여정을 완료했습니다! 이제 다음을 이해할 수 있습니다.

* 헤드리스와 제목이 없는 콘텐츠 전달 간의 차이입니다.
* AEM 헤드리스 기능.
* Headless 프로젝트를 구성하고 AEM 하는 방법입니다.
* AEM에서 헤드리스 컨텐츠를 만드는 방법.
* AEM에서 헤드리스 콘텐츠를 검색하고 업데이트하는 방법입니다.
* AEM Headless 프로젝트를 사용하여 라이브로 전환하는 방법
* Go-Live 후에 무엇을 합니까?

첫 번째 AEM Headless 프로젝트를 이미 시작했거나 이제 필요한 모든 정보를 가지고 있습니다. 잘했어요!

### 단일 페이지 애플리케이션 살펴보기 {#explore-spa}

하지만 AEM의 헤드리스 가게들은 여기서 멈출 필요가 없습니다. 당신은 [여정의 시작하기](getting-started.md#integration-levels) AEM에서 헤드리스 게재 및 기존 전체 스택 모델을 지원할 뿐만 아니라 두 가지 장점을 모두 결합한 하이브리드 모델을 지원할 수 있는 방법에 대해 간략하게 설명합니다.

이러한 종류의 유연성이 프로젝트에 필요한 경우 여정의 추가 부분인 선택 사항을 계속 진행합니다. [AEM을 사용하여 단일 페이지 애플리케이션(SPA)을 만드는 방법.](create-spa.md)

## 추가 리소스 {#additional-resources}

* [AEM Developing 안내서](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/the-basics.html?lang=en)

* [WKND 자습서](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en)

* [AEM용 Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=en)

* CDN 캐시

   * [CDN 캐시 제어](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#controlling-a-cdn-cache)

   * 구성 [CDN 재작성기](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html) (*CDN 재작성기 검색*)

<!--
* [An Overview of Deploying to AEM as a Cloud Service](/help/implementing/deploying/overview.md)
* [The AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [Set Up A Local AEM Environment](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)
* [Use Cloud Manager to Deploy Your Code](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [Integrate the Cloud Manager Git Repository with an External Git Repository and Deploy a Project to AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html)
-->
