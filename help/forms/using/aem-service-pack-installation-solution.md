---
title: 최신 6.5.15.0 서비스 팩이 설치되면 CRX/bundle 및 시작 페이지 서비스를 사용할 수 없는 오류가 발생합니다
description: 최신 6.5.15.0 서비스 팩이 설치되면 CRX/bundle 및 시작 페이지 서비스를 사용할 수 없는 오류가 발생합니다
source-git-commit: 813d8ffc53dc1928674367c9568b6269642cecb7
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 15%

---


# AEM(6.5.15.0) 서비스 팩을 설치한 후 서비스를 사용할 수 없는 오류가 발생했습니다 {#steps-to-resolve-error-after-installing-service-pack}

## 문제 {#issue}

설치 후 [AEM 6.5.15.0 서비스 팩](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)로 설정되어 있는 경우 오류가 발생합니다.
* 오류 [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR (org.osgi.framework.BundleException: org.apache.sling.scripting.console을 확인할 수 없습니다.

AEM 6.5.15.0 서비스 팩을 설치한 후 CRX/bundle을 설치하고 시작 페이지에 서비스 사용 불가 오류가 표시됩니다.

## 적용 대상 {#applies-to}

이 솔루션은 다음과 같은 경우에 적용됩니다.
* JBoss EAP 7.4.0에서 실행되는 서버를 제외한 모든 JEE 서버의 AEM Forms

## 솔루션 {#solution}

>[!NOTE]
>
>문제 해결 단계는 JBoss EAP 7.4를 제외한 모든 애플리케이션 서버에 적용됩니다.

설치 후 [AEM 6.5.15.0 서비스 팩](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), CRX/bundle 및 시작 페이지에 사용 가능한 서비스 오류가 표시되면 다음 단계를 수행하십시오.

1. 응용 프로그램 서버를 중지합니다.
1. 다음으로 이동 `[aem-forms root]\crx-repository\launchpad\felix\bundle52`.
1. 을(를) 찾습니다 `bundle.info` 파일.
1. 를 엽니다. `bundle.info` 파일(ant text editor)로 파일을 검색하고 번들 이름을 `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >경우에 따라 `bundle.info` 아래에 `bundle52` 에 이 포함되어 있지 않음 `org.apache.felix.http.bridge` 번들 옆의 대괄호 안에 있는 번들 번호를 확인합니다 `org.apache.felix.http.bridge`. 그런 다음 로 이동합니다. [aem forms 루트]\crx-repository\launchpad\felix\bundle[x] 이 위치에서 다음 단계를 수행합니다.

1. URL로 이동: `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. 검색 대상 `bundle.jar` 이름을 바꿀 수 있습니다 `bundle.jar` to `bundle.jar.bak`.
1. 복사 `bundle.jar` 여기서 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar).
1. 애플리케이션 서버를 시작하고 로그가 안정화될 때까지 기다렸다가 번들 상태를 확인합니다.
1. 모든 번들이 활성화 상태에 있으면 를 설치합니다. `org.apache.felix.http.servlet-api-1.2.0_fragment-full.jar` 에서 서블릿 조각 `system/console/bundles` 에서 다운로드 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) 그리고 애플리케이션 서버가 안정화될 때까지 기다립니다.
1. 응용 프로그램 서버를 중지합니다.
1. 다음으로 이동 `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` 삭제 `bundle.jar`.
1. 이름 바꾸기 `bundle.jar.bak` 변환 후 `bundle.jar`.
1. 응용 프로그램 서버를 시작합니다.