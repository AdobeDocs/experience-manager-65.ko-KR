---
title: 보안
seo-title: Security
description: 개발 단계 중 응용 프로그램 보안 시작
seo-description: Application Security starts during the development phase
uuid: efd5f3bc-da07-4fc8-a6ce-f1e6f5084c9e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: d2267663-6c1d-413c-9862-e82e21ae6906
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 보안{#security}

개발 단계 동안 응용 프로그램 보안이 시작됩니다. Adobe은 다음 보안 모범 사례를 적용할 것을 권장합니다.

## 요청 세션 사용 {#use-request-session}

최소 권한의 원칙에 따라 Adobe은 사용자 요청에 바인딩된 세션과 적절한 액세스 제어를 사용하여 모든 저장소 액세스를 수행하는 것을 권장합니다.

## XSS(교차 사이트 스크립팅)에 대한 Protect {#protect-against-cross-site-scripting-xss}

XSS(교차 사이트 스크립팅)를 사용하면 공격자가 다른 사용자가 보는 웹 페이지에 코드를 삽입할 수 있습니다. 이 보안 취약성은 악의적인 웹 사용자가 액세스 제어를 무시하기 위해 사용할 수 있습니다.

AEM은 사용자가 제공한 모든 컨텐츠를 출력 시 필터링하는 원칙을 적용합니다. XSS 방지는 개발 및 테스트 중에 가장 높은 우선 순위가 지정됩니다.

AEM에서 제공하는 XSS 보호 메커니즘은 [AntiSamy Java 라이브러리](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) 제공 [OWASP(Open Web Application Security Project)](https://www.owasp.org/). 기본 AntiSamy 구성은

`/libs/cq/xssprotection/config.xml`

구성 파일을 오버레이하여 자체 보안 요구에 맞게 이 구성을 조정해야 합니다. 공식 [AntiSamy 설명서](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) 은 보안 요구 사항을 구현하는 데 필요한 모든 정보를 제공합니다.

>[!NOTE]
>
>항상 를 사용하여 XSS 보호 API에 액세스하는 것이 좋습니다 [AEM에서 제공하는 XSSAPI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html).

또한 다음과 같은 웹 애플리케이션 방화벽도 [Apache용 mod_security](https://www.modsecurity.org)를 사용하면 배포 환경의 보안을 중앙 집중식으로 안정적으로 제어할 수 있으며 이전에 감지되지 않은 교차 사이트 스크립팅 공격으로부터 보호할 수 있습니다.

## Cloud Service 정보에 액세스 {#access-to-cloud-service-information}

>[!NOTE]
>
>인스턴스 보안에 필요한 OSGi 설정과 Cloud Service 정보에 대한 ACL은 [프로덕션 준비 모드](/help/sites-administering/production-ready.md). 즉, 구성을 수동으로 변경할 필요가 없지만 배포로 라이브로 전환하기 전에 먼저 구성을 검토하는 것이 좋습니다.

다음 경우에 [Adobe Marketing Cloud과 AEM 인스턴스 통합](/help/sites-administering/marketing-cloud.md) 를 [Cloud Service 구성](/help/sites-developing/extending-cloud-config.md). 수집된 모든 통계와 함께 이러한 구성에 대한 정보가 저장소에 저장됩니다. 이 기능을 사용하는 경우 이 정보에 대한 기본 보안이 요구 사항과 일치하는지 여부를 검토하는 것이 좋습니다.

Webservicessupport 모듈은 다음과 같은 통계 및 구성 정보를 기록합니다.

`/etc/cloudservices`

기본 권한 사용:

* 작성 환경: `read` 대상 `contributors`

* 게시 환경: `read` 대상 `everyone`

## 사이트 간 요청 위조 공격에 대한 Protect {#protect-against-cross-site-request-forgery-attacks}

AEM에서 CSRF 공격을 완화하기 위해 사용하는 보안 메커니즘에 대한 자세한 내용은 다음을 참조하십시오. [Sling 레퍼러 필터](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 보안 확인 목록 및 [CSRF 보호 프레임워크 설명서](/help/sites-developing/csrf-protection.md).
