---
title: 최신 6.5.15.0 서비스 팩이 설치된 후 CRX/번들 및 시작 페이지 서비스를 사용할 수 없는 오류 발생
description: 최신 6.5.15.0 서비스 팩이 설치된 후 CRX/번들 및 시작 페이지 서비스를 사용할 수 없는 오류 발생
SEO Description: Trouble shooting steps to resolve the errors after installing latest 6.5.15.0 service pack
exl-id: dfe015a3-3a24-41c5-aede-8e086851d62b
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: 8c4fb903-572c-5473-ad45-8ebb0d5d8134
    internal-label: AEM Forms on OSGi
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%
---
# AEM(6.5.15.0) 서비스 팩을 설치한 후 서비스를 사용할 수 없음 오류 발생 {#steps-to-resolve-error-after-installing-service-pack}

## 문제 {#issue}

[AEM 6.5.15.0 서비스 팩](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)을 설치한 후 다음과 같이 오류가 발생합니다.
* 오류 [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent 오류(org.osgi.framework.BundleException: org.apache.sling.scripting.console을 해결할 수 없습니다.

AEM 6.5.15.0 서비스 팩을 설치한 후 CRX/번들 및 시작 페이지에 서비스를 사용할 수 없는 오류가 표시됩니다.

## 적용 대상 {#applies-to}

이 솔루션은 다음에 적용됩니다.
* JBoss EAP 7.4.0에서 실행되는 서버를 제외한 모든 JEE 서버의 AEM Forms

## 솔루션 {#solution}

>[!NOTE]
>
>문제 해결 단계는 JBoss EAP 7.4를 제외한 모든 애플리케이션 서버에 적용할 수 있습니다.

[AEM 6.5.15.0 서비스 팩](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)을 설치한 후 CRX/번들 및 시작 페이지에 서비스를 사용할 수 없는 오류가 표시되면 다음 단계를 수행하십시오.

1. 응용 프로그램 서버를 중지합니다.
1. 다음으로 이동 `[aem-forms root]\crx-repository\launchpad\felix\bundle52`.
1. `bundle.info` 파일을 찾습니다.
1. ANT 텍스트 편집기에서 `bundle.info` 파일을 열고 `org.apache.felix.http.bridge`(으)로 번들 이름을 검색합니다.

   >[!NOTE]
   >
   >`bundle52`의 `bundle.info`에 `org.apache.felix.http.bridge` 번들이 없는 경우 `org.apache.felix.http.bridge` 옆에 대괄호로 묶인 번들 번호를 확인하십시오. 그런 다음 [aem-forms 루트]\crx-repository\launchpad\felix\bundle[x]&#x200B;(으)로 이동하여 이 위치에서 다음 단계를 수행하십시오.

1. URL `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`(으)로 이동합니다.
1. `bundle.jar`을(를) 검색하고 `bundle.jar`의 이름을 `bundle.jar.bak`(으)로 변경합니다.
1. [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar)에서 이 위치에 있는 `Bundle for AEM 6.5 Forms on JEE Service Pack 15`을(를) 복사합니다.
1. 애플리케이션 서버를 시작하고 로그가 안정될 때까지 기다린 후 번들 상태를 확인합니다.
1. 모든 번들이 활성 상태가 되면 `system/console/bundles`에서 JEE 서비스 팩 15](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)의 AEM 6.5 Forms용 [조각을 설치하고 응용 프로그램 서버가 안정화될 때까지 기다리십시오.
1. 응용 프로그램 서버를 중지합니다.
1. `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1`(으)로 이동하여 `bundle.jar`을(를) 삭제합니다.
1. `bundle.jar.bak`의 이름을 `bundle.jar`(으)로 바꿉니다.
1. 응용 프로그램 서버를 시작합니다.
