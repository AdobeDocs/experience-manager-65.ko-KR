---
title: OWASP 상위 10
description: AEM이 상위 10개의 OWASP 보안 위험을 어떻게 처리하는지 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 8b2a2f1d-8286-4ba5-8fe2-627509c72a45
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# OWASP 상위 10{#owasp-top}

다음 [웹 응용 프로그램 보안 프로젝트 열기](https://owasp.org/) (OWASP)는 다음과 같이 간주되는 항목의 목록을 유지 관리합니다. [10대 웹 응용 프로그램 보안 위험](https://owasp.org/www-project-top-ten/).

다음은 CRX가 이러한 자산을 처리하는 방법에 대한 설명과 함께 나와 있습니다.

## 1. 주사 {#injection}

* SQL - 디자인 금지: 기본 저장소 설정에는 기존 데이터베이스가 포함되어 있지 않고 필요하지 않으며 모든 데이터는 콘텐츠 저장소에 저장됩니다. 모든 액세스는 인증된 사용자로 제한되며 JCR API를 통해서만 수행할 수 있습니다. SQL은 검색 쿼리에만 지원됩니다(SELECT). 또한 SQL은 값 바인딩 지원을 제공합니다.
* LDAP - 인증 모듈이 입력을 필터링하고 바인드 메서드를 사용하여 사용자 가져오기를 수행하므로 LDAP 삽입을 수행할 수 없습니다.
* OS - 애플리케이션 내에서 수행되는 셸 실행이 없습니다.

## 2. XSS(크로스 사이트 스크립팅) {#cross-site-scripting-xss}

일반적인 완화 방법은 를 기반으로 서버측 XSS 보호 라이브러리를 사용하여 사용자 생성 콘텐츠의 모든 출력을 인코딩하는 것입니다. [OWASP 인코더](https://owasp.org/www-project-java-encoder/) 및 [앤티사미](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project).

XSS는 테스트 및 개발 기간 동안 최우선 순위가 되며, 발견된 문제는 (일반적으로) 즉시 해결됩니다.

## 3. 손상된 인증 및 세션 관리 {#broken-authentication-and-session-management}

AEM은 사운드 및 입증된 인증 기술을 사용하여 [아파치 잭래빗](https://jackrabbit.apache.org/jcr/index.html) 및 [Apache Sling](https://sling.apache.org/). 브라우저/HTTP 세션은 AEM에서 사용되지 않습니다.

## 4. 비보안 직접 개체 참조 {#insecure-direct-object-references}

데이터 객체에 대한 모든 액세스는 저장소에 의해 매개되므로 역할 기반 액세스 제어에 의해 제한됩니다.

## 5. CSRF(크로스 사이트 요청 위조) {#cross-site-request-forgery-csrf}

CSRF(교차 사이트 요청 위조)는 모든 양식 및 AJAX 요청에 암호화 토큰을 자동으로 삽입하고 모든 POST에 대해 서버에서 이 토큰을 확인하여 완화됩니다.

또한 AEM에는 를 구성할 수 있는 레퍼러 헤더 기반 필터가 제공됩니다. *전용* 목록에 정의된 특정 호스트의 POST 요청을 허용합니다.

## 6. 보안 구성 오류 {#security-misconfiguration}

모든 소프트웨어가 항상 올바르게 구성되었다고 보장할 수는 없다. 그러나 Adobe은 가능한 많은 지침을 제공하고 가능한 한 간단하게 구성을 만들기 위해 노력하고 있습니다. 또한 AEM은 [통합 보안 상태 점검](/help/sites-administering/operations-dashboard.md) 보안 구성을 한눈에 모니터링할 수 있습니다.

리뷰 [보안 검사 목록](/help/sites-administering/security-checklist.md) 단계별 경화 지침을 제공하는 추가 정보입니다.

## 7. 비보안 암호화 저장소 {#insecure-cryptographic-storage}

암호는 사용자 노드에 암호화 해시로 저장됩니다. 기본적으로 이러한 노드는 관리자 및 사용자 자신만 읽을 수 있습니다.

타사 자격 증명과 같은 중요한 데이터는 FIPS 140-2 인증 암호화 라이브러리를 사용하여 암호화된 형식으로 저장됩니다.

## 8. URL 액세스 제한 실패 {#failure-to-restrict-url-access}

저장소를 통해 다음을 설정할 수 있습니다. [세분화된 권한(JCR에 의해 지정됨)](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html) 액세스 제어 항목을 통해 지정된 경로에 있는 지정된 사용자 또는 그룹에 대해 액세스 제한은 저장소에 의해 적용됩니다.

## 9. 전송 계층 보호 부족 {#insufficient-transport-layer-protection}

서버 구성으로 완화됩니다(예: HTTPS만 사용).

## 10. 검증되지 않은 리디렉션 및 전달 {#unvalidated-redirects-and-forwards}

사용자가 제공한 대상에 대한 모든 리디렉션을 내부 위치로 제한하여 완화했습니다.
