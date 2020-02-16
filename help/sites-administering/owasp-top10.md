---
title: OWASP 상위 10
seo-title: OWASP 상위 10
description: AEM에서 상위 10개의 OWASP 보안 위험을 처리하는 방법을 알아봅니다.
seo-description: AEM에서 상위 10개의 OWASP 보안 위험을 처리하는 방법을 알아봅니다.
uuid: a5a7e130-e15b-47ae-ba21-448f9ac76074
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e5323ae8-bc37-4bc6-bca6-9763e18c8e76
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# OWASP 상위 10{#owasp-top}

OWASP( [Open Web Application Security Project](https://www.owasp.org) )는 웹 애플리케이션 보안 [주요 10개 위험](https://www.owasp.org/index.php/OWASP_Top_Ten_Project)목록을 유지합니다.

다음은 CRX가 어떻게 처리하는지에 대한 설명과 함께 아래에 나와 있습니다.

## 1.주입 {#injection}

* SQL - 설계에서 방지:기본 저장소 설정은 기존 데이터베이스를 포함하거나 필요로 하지 않으며, 모든 데이터는 컨텐츠 저장소에 저장됩니다. 모든 액세스 권한은 인증된 사용자로 제한되며 JCR API를 통해서만 수행할 수 있습니다. SQL은 검색 쿼리에만 지원됩니다(SELECT). 또한 SQL은 값 바인딩 지원을 제공합니다.
* LDAP - 인증 모듈이 입력을 필터링하고 바인딩 방법을 사용하여 사용자 가져오기를 수행하므로 LDAP 주입이 불가능합니다.
* OS - 애플리케이션 내에서 수행되는 셸 실행이 없습니다.

## 2.사이트 간 스크립팅(XSS) {#cross-site-scripting-xss}

일반적인 완화 방법은 OWASP Encoder 및 AntiSamy를 기반으로 하는 서버측 XSS 보호 라이브러리를 사용하여 사용자 생성 컨텐츠의 모든 [출력을](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project) 인코딩하는 [것입니다](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project).

XSS는 테스트 및 개발 과정에서 가장 우선적으로 고려되며, 발견된 모든 문제는 즉시 해결됩니다(일반적으로).

## 3.끊어진 인증 및 세션 관리 {#broken-authentication-and-session-management}

AEM은 Apache Jackrabbit와 Apache [Sling에 의존하는](https://jackrabbit.apache.org/) 사운드 및 입증된 인증 기법을 [사용합니다](https://sling.apache.org/). 브라우저/HTTP 세션은 AEM에서 사용되지 않습니다.

## 4.안전하지 않은 직접 개체 참조 {#insecure-direct-object-references}

데이터 객체에 대한 모든 액세스는 저장소에 의해 조정되므로 역할 기반 액세스 제어에 의해 제한됩니다.

## 5.CSRF(교차 사이트 요청 위조) {#cross-site-request-forgery-csrf}

CSRF(교차 사이트 요청 위조)는 모든 양식 및 AJAX 요청에 암호화 토큰을 자동으로 삽입하고 모든 POST에 대해 서버에서 이 토큰을 확인하여 완화됩니다.

또한, AEM은 레퍼러 헤더 기반 필터와 함께 제공되는데, 이 필터는 특별히 화이트 리스트 호스트에서 POST 요청만 허용하도록 구성할 수 있습니다.

## 6.보안 오구성 {#security-misconfiguration}

모든 소프트웨어가 항상 올바로 구성되어 있다고 보장할 수는 없습니다. 그러나 가능한 한 많은 지침을 제공하고 구성을 최대한 단순화하기 위해 노력하고 있습니다. 또한 AEM에는 보안 구성을 한 눈에 모니터링할 수 있는 [통합 보안](/help/sites-administering/operations-dashboard.md) 상태 검사가 포함되어 있습니다.

단계별 보안 [강화](/help/sites-administering/security-checklist.md) 지침을 제공하는 자세한 내용은 보안 검사 목록을 참조하십시오.

## 7.안전하지 않은 암호화 저장소 {#insecure-cryptographic-storage}

암호는 사용자 노드에 암호화 해시로 저장됩니다.기본적으로 이러한 노드는 관리자와 사용자 자신만 읽을 수 있습니다.

타사 자격 증명과 같은 중요한 데이터는 FIPS 140-2 인증 암호화 라이브러리를 사용하여 암호화된 형식으로 저장됩니다.

## 8.URL 액세스 제한 실패 {#failure-to-restrict-url-access}

저장소는 액세스 제어 항목을 통해 지정된 경로에서 특정 사용자 또는 그룹에 대해 JCR에 의해 지정된 [세부적으로 분류된 권한을 설정할 수](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html) 있습니다. 액세스 제한은 저장소에 의해 적용됩니다.

## 9.불충분한 전송 레이어 보호 {#insufficient-transport-layer-protection}

서버 구성에 의해 완화됩니다(예: HTTPS만 사용).

## 10.확인되지 않은 리디렉션 및 전달 {#unvalidated-redirects-and-forwards}

사용자가 제공한 대상에 대한 모든 리디렉션을 내부 위치로 제한함으로써 완화된 효과를 얻을 수 있습니다.

