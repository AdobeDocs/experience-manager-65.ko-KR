---
title: 최신 6.5.15.0 서비스 팩이 설치된 후 CRX/번들 및 시작 페이지 서비스를 사용할 수 없는 오류 발생
description: 최신 6.5.15.0 서비스 팩이 설치된 후 CRX/번들 및 시작 페이지 서비스를 사용할 수 없는 오류 발생
exl-id: dfe015a3-3a24-41c5-aede-8e086851d62b
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 2%

---

# AEM(6.5.15.0) 서비스 팩을 설치한 후 서비스를 사용할 수 없음 오류 발생 {#steps-to-resolve-error-after-installing-service-pack}

## 문제 {#issue}

설치 후 [AEM 6.5.15.0 서비스 팩](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), 오류는 다음과 같이 발생합니다.
* 오류 [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR (org.osgi.framework.BundleException: org.apache.sling.scripting.console을 해결할 수 없음

AEM 6.5.15.0 서비스 팩을 설치한 후 CRX/번들 및 시작 페이지에 서비스를 사용할 수 없는 오류가 표시됩니다.

## 적용 대상 {#applies-to}

이 솔루션은 다음에 적용됩니다.
* JBoss EAP 7.4.0에서 실행되는 서버를 제외한 모든 JEE 서버의 AEM Forms

## 솔루션 {#solution}

>[!NOTE]
>
>문제 해결 단계는 JBoss EAP 7.4를 제외한 모든 애플리케이션 서버에 적용할 수 있습니다.

설치 후 [AEM 6.5.15.0 서비스 팩](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), CRX/번들 및 시작 페이지에 서비스를 사용할 수 없는 오류가 표시되는 경우 다음 단계를 수행하십시오.

1. 응용 프로그램 서버를 중지합니다.
1. 다음으로 이동 `[aem-forms root]\crx-repository\launchpad\felix\bundle52`.
1. 를 찾습니다. `bundle.info` 파일.
1. 를 엽니다. `bundle.info` ant 텍스트 편집기의 파일 및 번들 이름 검색 `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >만일의 경우에 `bundle.info` 아래에 `bundle52` 이(가) 다음을 포함하지 않음 `org.apache.felix.http.bridge` 번들, 옆에 있는 대괄호로 묶은 번들 번호를 확인합니다. `org.apache.felix.http.bridge`. 다음으로 이동 [aem-forms 루트]\crx-repository\launchpad\felix\bundle[x] 이 위치에서 다음 단계를 수행합니다.

1. 다음 URL로 이동합니다. `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. 검색 대상 `bundle.jar` 및 이름 바꾸기 `bundle.jar` 끝 `bundle.jar.bak`.
1. 다음을 복사합니다. `Bundle for AEM 6.5 Forms on JEE Service Pack 15` 에서 이 위치에 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar).
1. 애플리케이션 서버를 시작하고 로그가 안정될 때까지 기다린 후 번들 상태를 확인합니다.
1. 모든 번들이 활성 상태가 되면 [JEE 서비스 팩 15의 AEM 6.5 Forms용 조각](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) 다음에서 `system/console/bundles` 응용 프로그램 서버가 안정될 때까지 기다립니다.
1. 응용 프로그램 서버를 중지합니다.
1. 다음으로 이동 `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` 및 삭제 `bundle.jar`.
1. 이름 바꾸기 `bundle.jar.bak` (으)로 `bundle.jar`.
1. 응용 프로그램 서버를 시작합니다.
