---
title: 보안
seo-title: 보안
description: 개발 단계에서 애플리케이션 보안 시작
seo-description: 개발 단계에서 애플리케이션 보안 시작
uuid: efd5f3bc-da07-4fc8-a6ce-f1e6f5084c9e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: d2267663-6c1d-413c-9862-e82e21ae6906
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 보안{#security}

개발 단계에서 애플리케이션 보안이 시작됩니다. Adobe에서는 다음과 같은 보안 모범 사례를 적용하는 것이 좋습니다.

## 요청 세션 사용 {#use-request-session}

leas 권한에 따라, Adobe는 모든 저장소 액세스를 사용자 요청에 바인딩된 세션 및 적절한 액세스 제어를 사용하여 수행하는 것이 좋습니다.

## XSS(교차 사이트 스크립팅)로부터 보호 {#protect-against-cross-site-scripting-xss}

XSS(교차 사이트 스크립팅)를 통해 공격자는 다른 사용자가 보는 웹 페이지에 코드를 삽입할 수 있습니다. 이 보안 취약점은 악의적인 웹 사용자가 액세스 제어를 우회하도록 악용될 수 있습니다.

AEM 파섹 XSS 방지는 개발 및 테스트 중 가장 높은 우선순위가 주어집니다.

AEM에서 제공하는 XSS 파섹 보호 메커니즘은 OWASP(Open Web Application Security Project) [에서](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) 제공하는 [AntiSamy Java 라이브러리를](https://www.owasp.org/)기반으로 합니다. 기본 AntiSamy 구성은

`/libs/cq/xssprotection/config.xml`

구성 파일을 오버레이하여 이 구성을 자체 보안 요구 사항에 맞게 조정하는 것이 중요합니다. 공식 [AntiSamy 설명서는](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) 보안 요구 사항을 이행하기 위해 필요한 모든 정보를 제공합니다.

>[!NOTE]
>
>AEM에서 제공하는 XSSAPI를 사용하여 항상 XSS 보호 API에 [액세스하는 것이 좋습니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html).

또한 Apache용 [mod_security와 같은](https://www.modsecurity.org)웹 애플리케이션 방화벽은 배포 환경의 보안을 중앙에서 안전하게 제어하고 이전에 감지되지 않은 크로스 사이트 스크립팅 공격으로부터 보호할 수 있습니다.

## 클라우드 서비스 정보 액세스 {#access-to-cloud-service-information}

>[!NOTE]
>
>Production Ready Mode의 일부로 클라우드 서비스 정보에 대한 ACL과 인스턴스 보안에 필요한 OSGi 설정이 [자동화됩니다](/help/sites-administering/production-ready.md). 즉, 수동으로 구성을 변경할 필요는 없지만 배포와 함께 라이브하기 전에 이를 검토하는 것이 좋습니다.

AEM 인스턴스를 [Adobe Marketing Cloud와 통합할 때](/help/sites-administering/marketing-cloud.md) 클라우드 서비스 [구성을](/help/sites-developing/extending-cloud-config.md)사용합니다. 이러한 구성에 대한 정보와 수집된 모든 통계가 저장소에 저장됩니다. 이 기능을 사용하는 경우 이 정보에 대한 기본 보안이 요구 사항과 일치하는지 여부를 검토하는 것이 좋습니다.

웹 서비스 지원 모듈은 다음 아래에서 통계 및 구성 정보를 기록합니다.

`/etc/cloudservices`

기본 권한 사용:

* 작성 환경: `read` for `contributors`

* 게시 환경: `read` for `everyone`

## 크로스 사이트 요청 위조 공격으로부터 보호 {#protect-against-cross-site-request-forgery-attacks}

AEM에서 CSRF 공격을 완화하는 데 사용하는 보안 메커니즘에 대한 자세한 내용은 보안 [체크리스트](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 및 CSRF 보호 [프레임워크 설명서를 참조하십시오](/help/sites-developing/csrf-protection.md).