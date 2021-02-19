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
source-git-commit: ea4de28525ec4c2094e84d98aad6a518b03f011e
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---


# 보안{#security}

개발 단계에서 응용 프로그램 보안이 시작됩니다. Adobe은 다음과 같은 보안 우수 사례를 적용할 것을 권장합니다.

## 요청 세션 사용 {#use-request-session}

최소 권한 원칙에 따라 Adobe은 사용자 요청에 바인딩된 세션 및 적절한 액세스 제어를 사용하여 모든 저장소 액세스를 수행할 것을 권장합니다.

## 크로스 사이트 스크립팅(XSS)에 대한 Protect {#protect-against-cross-site-scripting-xss}

XSS(교차 사이트 스크립팅)를 통해 공격자는 다른 사용자가 보는 웹 페이지에 코드를 삽입할 수 있습니다. 이 보안 취약점은 악의적인 웹 사용자가 액세스 제어를 우회하도록 악용할 수 있습니다.

AEM은 출력 시 사용자가 제공하는 모든 컨텐츠를 필터링하는 원칙을 적용합니다. XSS 예방은 개발 및 테스트 과정에서 가장 우선적으로 고려됩니다.

AEM에서 제공하는 XSS 보호 메커니즘은 [OWASP(Open Web Application Security Project)](https://www.owasp.org/)에서 제공하는 [AntiSamy Java Library](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project)을 기반으로 합니다. 기본 AntiSamy 구성은

`/libs/cq/xssprotection/config.xml`

구성 파일을 오버레이하여 이 구성을 자신의 보안 요구에 맞게 조정하는 것이 중요합니다. 공식 [AntiSamy 문서](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project)는 보안 요구 사항을 구현하는 데 필요한 모든 정보를 제공합니다.

>[!NOTE]
>
>AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html)에서 제공하는 [XSSAPI를 사용하여 항상 XSS 보호 API에 액세스하는 것이 좋습니다.

또한 Apache](https://www.modsecurity.org)용 [mod_security와 같은 웹 응용 프로그램 방화벽은 배포 환경의 보안을 안정적이고 중앙에서 제어하여 이전에 감지하지 못한 교차 사이트 스크립팅 공격으로부터 보호할 수 있습니다.

## Cloud Service 정보 {#access-to-cloud-service-information} 액세스

>[!NOTE]
>
>Cloud Service 정보에 대한 ACL과 인스턴스 보안에 필요한 OSGi 설정은 [프로덕션 준비 모드](/help/sites-administering/production-ready.md)의 일부로 자동화됩니다. 즉, 수동으로 구성을 변경할 필요가 없지만 배포를 라이브하기 전에 이를 검토하는 것이 좋습니다.

[AEM 인스턴스를 Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md)에 통합할 때 [Cloud Service 구성](/help/sites-developing/extending-cloud-config.md)을 사용합니다. 이러한 구성에 대한 정보와 수집된 통계가 저장소에 저장됩니다. 이 기능을 사용하는 경우 이 정보의 기본 보안이 요구 사항과 일치하는지 여부를 검토하는 것이 좋습니다.

webservicessupport 모듈은 다음 아래에 통계 및 구성 정보를 기록합니다.

`/etc/cloudservices`

기본 권한 사용:

* 작성 환경:`contributors`에 대한 `read`

* 게시 환경:`everyone`에 대한 `read`

## 크로스 사이트 요청 위조 공격에 대한 Protect: {#protect-against-cross-site-request-forgery-attacks}

AEM이 CSRF 공격을 완화하는 보안 메커니즘에 대한 자세한 내용은 보안 체크리스트의 [Sling Referrer Filter](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 섹션 및 [CSRF Protection Framework 설명서](/help/sites-developing/csrf-protection.md)을 참조하십시오.