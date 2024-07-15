---
title: OSGi 구성 설정
description: 이 문서에서는 프로젝트 구현과 관련된 OSGi 구성 설정(번들에 따라 나열됨)에 대해 자세히 설명합니다. 목록은 가이드라인 역할을 하며, 완전한 것은 아닙니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
exl-id: 19eedcf2-140a-452d-aa8f-6fd7f219e5f8
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '3360'
ht-degree: 0%

---

# OSGi 구성 설정{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/)은(는) AEM 기술 스택에 있는 기본 요소입니다. AEM의 복합 번들과 해당 구성을 제어하는 데 사용됩니다.

OSGi &quot;*은(는) 응용 프로그램을 작고 재사용 가능한 공동 작업 구성 요소에서 구성할 수 있는 표준화된 기본 형식을 제공합니다. 이러한 구성 요소는 응용 프로그램으로 구성하고*&quot;을(를) 배포할 수 있습니다.

이 기능을 사용하면 번들을 개별적으로 중지, 설치 또는 시작할 수 있으므로 쉽게 관리할 수 있습니다. 상호 종속성이 자동으로 처리됩니다. 각 OSGi 구성 요소([OSGi 사양](https://docs.osgi.org/specification/) 참조)는 다양한 번들 중 하나에 포함되어 있습니다. AEM을 사용하여 작업할 때 이러한 번들에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다. 자세한 내용 및 권장 사례를 보려면 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)을 참조하십시오.

다음 OSGi 구성 설정(번들에 따라 나열됨)은 프로젝트 구현과 관련이 있습니다. 나열된 모든 설정을 조정할 필요는 없습니다. 일부 설정은 AEM 작동 방식을 이해하는 데 도움이 됩니다.

>[!CAUTION]
>
>이 목록은 지침으로 사용하기 위한 것이며, 완전한 것은 아닙니다. 모든 번들이 나열되지 않으며 일부 번들에 대한 모든 매개 변수도 나열되지 않습니다.
>
>필요한 구성은 프로젝트마다 다릅니다.
>
>사용된 값과 매개 변수에 대한 자세한 내용은 웹 콘솔을 참조하십시오.

>[!NOTE]
>
>[AEM 도구](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17488.html)의 일부인 OSGi 구성 비교 도구를 사용하여 기본 OSGi 구성을 나열할 수 있습니다.

>[!NOTE]
>
>AEM 내의 특정 기능 영역에 추가 번들이 필요할 수 있습니다. 이러한 경우 구성 세부 정보는 해당 기능과 관련된 페이지에서 확인할 수 있습니다.

**AEM 복제 이벤트 수신기** 구성:

* 복제 이벤트가 수신자에게 배포되는 **실행 모드**&#x200B;입니다. 예를 들어 작성자로 정의된 경우 복제를 &quot;시작&quot;하는 시스템이 됩니다.

* 프로젝트 코드가 게시 환경에서 복제 이벤트(역방향 복제)를 처리하는 경우 실행 모드 **게시**&#x200B;를 추가합니다. 예를 들어 Dispatcher을 사용하여 게시 환경에서 플러시하거나 다른 게시 인스턴스에 대한 표준 복제가 발생하는 경우.

**AEM 저장소 변경 수신기** 구성:

* **경로**, 배포할 준비가 된 저장소 이벤트를 수신할 위치입니다.

**CRX Sling 클라이언트 저장소** 기본 콘텐츠 저장소에 대한 액세스 권한을 구성합니다.

* 설치 후 **관리자 암호**&#x200B;를 변경해야 인스턴스의 [보안](/help/sites-administering/security-checklist.md)을 확인할 수 있습니다.
* 저장소 액세스에 영향을 줄 수 있으므로 다른 변경 사항은 필요하지 않으며 주의해야 합니다.

**Apache Felix OSGi 관리 콘솔** 구성:

* **플러그인**, 기본 탐색 항목(콘솔 플러그인)은 **Apache Felix 웹 관리 콘솔**&#x200B;에서 최상위 메뉴 항목으로 사용할 수 있습니다. 각각 공간 및 리소스가 필요하므로 필요하지 않은 모든 항목을 비활성화합니다.

>[!CAUTION]
>
>다음을 구성하십시오.
>
>Apache Felix 웹 관리 콘솔 자체에 액세스하기 위한 자격 증명인 **사용자 이름** 및 **암호**.
>인스턴스의 [보안](/help/sites-administering/security-checklist.md)을(를) 유지하려면 처음 설치한 후 암호를 변경해야 합니다.

>[!NOTE]
>
>저장소를 사용하려면 시작 시 Felix 콘솔을 사용하여 이 구성을 수행해야 합니다.

**Apache Sling 사용자 지정 가능 요청 데이터 로거** 구성:

* 요청 및 액세스 로깅의 위치 및 형식을 구성하기 위한 **로거 이름** 및 **로그 형식**(기본값: `request.log`). 이 로그 파일은 웹 체인과 관련된 성능 또는 디버깅 기능을 분석할 때 필수적입니다. [Apache Sling 요청 로거](#apacheslingrequestlogger)와(과) 쌍을 이룹니다.

[AEM 로깅](/help/sites-deploying/configure-logging.md) 및 [Sling 로깅](https://sling.apache.org/documentation/development/logging.html)을 참조하십시오.

**Apache Sling 이벤트 스레드 풀** 구성:

* 이벤트 스레드를 보관하는 데 사용되는 풀의 크기인 **최소 풀 크기** 및 **최대 풀 크기**&#x200B;입니다.

* **큐 크기**, 풀이 모두 소진된 경우 스레드 큐의 최대 크기입니다.
큐를 무제한으로 설정하므로 권장 값은 `-1`입니다. 제한을 설정하면 제한을 초과할 때 손실이 발생할 수 있습니다.

* 이러한 설정을 변경하면 이벤트 수가 많은 시나리오의 성능에 도움이 될 수 있습니다. (예: 무거운 AEM DAM 또는 워크플로우 사용)
* 테스트를 사용하여 시나리오와 관련된 값을 설정해야 합니다.
* 이러한 설정은 인스턴스의 성능에 영향을 줄 수 있으므로 합리적이고 정당한 고려 없이 변경하지 마십시오.

**Apache Sling GET 서블릿** 렌더링의 몇 가지 측면을 구성합니다.

* **자동 인덱스**&#x200B;을(를) 사용하여 검색할 디렉터리 렌더링을 활성화/비활성화합니다.
* **HTML**, **일반 텍스트**, **JSON** 또는 **XML**&#x200B;과(와) 같은 **기본 변환을 활성화**(또는 비활성화)합니다.
JSON을 비활성화하지 마십시오.

>[!NOTE]
>
>이 설정은 [프로덕션 준비 모드](/help/sites-administering/production-ready.md)에서 AEM을 실행하는 경우 프로덕션 인스턴스에 대해 자동으로 구성됩니다.

**Apache Sling JavaScript 처리기** .java 파일을 스크립트(서블릿)로 컴파일하기 위한 설정을 구성합니다.

특정 설정은 성능에 영향을 줄 수 있습니다. 가능한 경우 이러한 설정을 비활성화합니다(특히 프로덕션 인스턴스의 경우).

* **Source VM** 및 **대상 VM**&#x200B;에서 런타임 JVM으로 사용되는 JDK 버전을 정의합니다.

* 프로덕션 인스턴스의 경우:

   * **디버그 정보 생성** 사용 안 함

**Apache Sling JCR 설치 관리자** 이러한 매개 변수는 구성이 필요하지 않지만 개발하거나 디버깅할 때 유용하게 사용할 수 있습니다. 예를 들어, 설치 폴더는 체크인/체크아웃 또는 패키지 작성에 유용할 수 있습니다.

* **설치 폴더 이름 regexp** 및 **설치 폴더의 최대 계층 구조 깊이** - 설치할 리소스를 검색할 저장소 폴더의 위치와 깊이를 지정합니다. 와일드카드가 사용되는 경우( 에서와 같이)&#42;/install) `/libs/sling/install` 및 `/libs/cq/core/install`과(와) 같은 모든 적절한 일치 항목이 검색됩니다.

* **검색 경로**, jcrinstall에서 설치할 리소스를 검색하는 경로 목록과 해당 경로에 대한 가중치 계수를 나타내는 숫자를 표시합니다.

**Apache Sling 작업 이벤트 처리기** 작업 일정을 관리하는 매개 변수를 구성합니다.

* **다시 시도 간격**, **최대 다시 시도**, **최대 병렬 작업**, **대기 시간 확인** 등이 있습니다.

* 이러한 설정을 변경하면 작업 수가 많은 시나리오(예: AEM DAM 및 워크플로우의 과도한 사용)에서 성능이 향상될 수 있습니다.
* 테스트를 사용하여 시나리오와 관련된 값을 설정해야 합니다.
* 이러한 설정을 이유 없이 변경하지 마십시오. 충분히 고려한 후에만 변경하십시오.

**Apache Sling JSP Script Handler** JSP Script Handler에 대한 성능 관련 설정을 구성합니다. 성능을 향상시키려면 가능한 한 많이 비활성화해야 합니다.

특히 프로덕션 인스턴스의 경우:

* **디버그 정보 생성** 사용 안 함
* **생성된 Java 유지™** 사용 안 함
* **매핑된 콘텐츠** 사용 안 함
* **Source 조각 표시** 사용 안 함

>[!NOTE]
>
>이 설정은 [프로덕션 준비 모드](/help/sites-administering/production-ready.md)에서 AEM을 실행하는 경우 프로덕션 인스턴스에 대해 자동으로 구성됩니다.

**Apache Sling 로깅 구성** 구성:

* **로그 수준** 및 **로그 파일**&#x200B;을(를) 사용하여 중앙 로깅 구성(error.log)의 위치 및 로그 수준을 정의합니다. 수준을 `DEBUG`, `INFO`, `WARN`, `ERROR` 및 `FATAL` 중 하나로 설정할 수 있습니다.

* 로그 파일의 크기 및 버전 순환을 정의할 **로그 파일 수** 및 **로그 파일 임계값**&#x200B;입니다.

* **메시지 패턴**&#x200B;은(는) 로그 메시지의 형식을 정의합니다.

[AEM 로깅](/help/sites-deploying/configure-logging.md#global-logging) 및 [Sling 로깅](https://sling.apache.org/documentation/development/logging.html)을 참조하십시오.

**Apache Sling 로깅 로거 구성(팩터리 구성)** 구성:

* 로그 파일 및 메시지의 세부 정보를 정의하는 **로그 수준**, **로그 파일** 및 **메시지 형식**.

* 범주를 정의하려면 **로거**(으)로 설정합니다. 예를 들어 com.day.cq에 대해서만 기록합니다.

* **팩터리 구성**&#x200B;을 사용하면 필요한 다양한 로그 수준과 범주를 충족하기 위해 추가 구성을 원하는 수만큼 추가할 수 있습니다.
* 이러한 구성은 특정 서비스에 대한 TRACE 메시지를 특정 로그 파일에 기록하는 등 개발 중에 유용합니다.
* 이러한 구성은 프로덕션 환경에서 유용합니다. 예를 들어 특정 서비스에 대한 메시지가 개별 로그 파일에 기록되어 쉽게 모니터링할 수 있습니다.

[AEM 로깅](/help/sites-deploying/configure-logging.md) 및 [Sling 로깅](https://sling.apache.org/documentation/development/logging.html)을 참조하십시오.

**Apache Sling 로깅 작성기 구성(공장 구성)** 구성:

* 로그 파일의 존재를 정의하는 **로그 파일**.
* 버전 순환을 정의할 **로그 파일 수**&#x200B;입니다.

* 작성기는 **Apache Sling Logging Logger 구성** 구성에서 사용할 수 있습니다.

* 이러한 구성은 특정 서비스에 대한 TRACE 메시지를 특정 로그 파일에 기록하는 등 개발 중에 유용합니다.
* 이러한 구성은 프로덕션 환경에서 유용합니다. 예를 들어 특정 서비스에 대한 메시지가 개별 로그 파일에 기록되어 쉽게 모니터링할 수 있습니다.

[AEM 로깅](/help/sites-deploying/configure-logging.md) 및 [Sling 로깅](https://sling.apache.org/documentation/development/logging.html)을 참조하십시오.

**Apache Sling 주 서블릿** 구성:

* **요청당 호출 수** 및 **재귀 깊이**&#x200B;를 사용하여 무한 재귀 및 과도한 스크립트 호출로부터 시스템을 보호합니다.

**Apache Sling MIME 유형 서비스** 구성:

* 프로젝트에 필요한 형식을 시스템에 추가하려면 **MIME 형식**. 이렇게 하면 파일에 대한 `GET` 요청에서 파일 형식 및 응용 프로그램을 연결하는 올바른 콘텐츠 형식 헤더를 설정할 수 있습니다.

**Apache Sling Referrer Filter** CRX WebDAV 및 Apache Sling에서 CSRF(Cross-Site Request Forgery)와 관련된 알려진 보안 문제를 해결하려면 레퍼러 필터를 구성해야 합니다.

레퍼러 필터 서비스는 다음을 구성할 수 있는 OSGi 서비스입니다.

* 필터링해야 하는 http 메서드
* 빈 레퍼러 헤더 허용 여부
* 및 서버 호스트 외에 허용할 서버 목록입니다.

자세한 내용은 [보안 검사 목록 - 사이트 간 요청 위조 문제](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)를 참조하십시오.

>[!NOTE]
>
>Apache Sling Referrer 필터는 빠른 수정 패키지 설치에 따라 다릅니다.

**Apache Sling 요청 로거** 구성:

* 요청이 기록되는 방법을 정의하는 다양한 매개 변수입니다.
* **요청 로그 사용**&#x200B;을(를) 활성화하거나 비활성화합니다.

* **액세스 로그를 사용**&#x200B;하여 사용 또는 사용 안 함으로 설정합니다.

[Apache Sling 사용자 지정 가능 요청 데이터 로거](#apacheslingcustomizablerequestdatalogger)와(과) 연결되었습니다.

[AEM 로깅](/help/sites-deploying/configure-logging.md) 및 [Sling 로깅](https://sling.apache.org/documentation/development/logging.html)을 참조하십시오.

**Apache Sling Resource Resolver Factory** Sling 리소스 확인의 중앙 측면을 구성합니다.

* **리소스 검색 경로**&#x200B;에서 프로젝트별 경로를 추가하십시오. `/libs` 또는 `/apps`은(는) 제거하지 마십시오.

* vanity URL 매핑을 정의할 **가상 URL**.

* 별칭을 정의할 **URL 매핑**. 예: `/content`부터 `/`까지.

* **매핑 위치**, `/etc/map`에서 매퍼 구성을 외부화했습니다.

* 로컬 설치(예: `https://localhost:4502/system/console/jcrresolver` 사용)를 사용하여 활성화된 Resource Resolver를 확인합니다.

참조: [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>저장소에서 이러한 옵션을 구성합니다.
>
>그렇지 않으면 Felix 콘솔을 사용하여 **URL 매핑**&#x200B;을 변경하면 다음에 시작할 때 AEM에서 변경 내용을 덮어쓸 수 있습니다.

**Apache Sling Servlet/Script Resolver 및 Error Handler** Sling Servlet 및 Script Resolver에 여러 작업이 있습니다.

1. 요청을 처리하기 위해 호출할 서블릿 또는 스크립트를 선택하는 `ServletResolver`(으)로 사용됩니다.

1. `SlingScriptResolver` 역할을 합니다.

1. 요청 처리 서블릿 및 스크립트를 해결하는 데 사용되는 것과 동일한 알고리즘을 사용하여 오류 처리 서블릿 및 스크립트를 선택하는 `ErrorHandler` 인터페이스를 구현하여 오류 처리를 관리합니다.

다음을 포함하여 다양한 매개 변수를 설정할 수 있습니다.

* **실행 경로** - 실행 가능한 스크립트를 검색하는 경로를 나열합니다. 특정 경로를 구성하여 실행할 수 있는 스크립트를 제한할 수 있습니다. 구성된 경로가 없으면 모든 스크립트를 실행할 수 있도록 기본값이 사용됩니다(`/` = root).
구성된 경로 값이 슬래시로 끝나는 경우 전체 하위 트리가 검색됩니다. 이러한 후행 슬래시가 없으면 스크립트가 정확히 일치하는 경우에만 실행됩니다.

* **스크립트 사용자** - 이 선택적 속성은 스크립트를 읽는 데 사용되는 저장소 사용자 계정을 지정할 수 있습니다. 계정을 지정하지 않으면 기본적으로 `admin` 사용자가 사용됩니다.

* **기본 확장** - 기본 동작이 사용되는 확장 목록입니다. 리소스 유형의 마지막 경로 세그먼트를 스크립트 이름으로 사용할 수 있습니다.

**Apache HTTP 구성 요소 프록시 구성** - HTTP를 만들 때 사용되는 Apache HTTP 클라이언트를 사용하는 모든 코드에 대한 프록시 구성입니다. 예: 복제 시

구성을 만들 때 공장 구성을 변경하지 마십시오. 대신 **https://localhost:4502/system/console/configMgr/** 구성 관리자를 사용하여 이 구성 요소에 대한 팩터리 구성을 만드십시오. 프록시 구성은 **org.apache.http.proxyconfigurator.**&#x200B;에서 사용할 수 있습니다.

>[!NOTE]
>
>AEM 6.0 및 이전 릴리스에서는 프록시가 Day Commons HTTP 클라이언트에 구성되었습니다. AEM 6.1 및 이후 릴리스부터 프록시 구성이 &#39;Day Commons HTTP 클라이언트&#39; 구성 대신 &quot;Apache HTTP 구성 요소 프록시 구성&quot;으로 이동되었습니다.

**일 CQ 스팸 방지** 사용된 스팸 방지 서비스(Akismet)를 구성합니다. 이 기능을 사용하려면 다음을 등록해야 합니다.

* **공급자**
* **API 키**
* **등록된 URL**

**Adobe Granite HTML 라이브러리 관리자** 기본 구조가 표시되는 방식 등을 포함하여 클라이언트 라이브러리(css 또는 js)의 처리를 제어하도록 구성합니다.

* 프로덕션 인스턴스의 경우:

   * **축소** 사용(CRLF 및 공백 문자 제거)
   * **Gzip** 사용(한 번의 요청으로 파일을 압축하고 액세스할 수 있도록 허용)
   * **Debug** 사용 안 함
   * **시간** 사용 안 함

* JS 개발의 경우(특히 firebugging/debugging 시):

   * **축소** 사용 안 함
   * **Debug**&#x200B;을(를) 사용하여 디버깅을 위해 파일을 구분하고 버그 실행과 함께 사용할 수 있습니다.
   * 타이밍을 원하는 경우 **타이밍**&#x200B;을(를) 사용하도록 설정하십시오.
   * **Debug** 콘솔을 사용하여 JS 콘솔 로그 메시지를 볼 수 있습니다.

>[!CAUTION]
>
>**축소** 또는 **Gzip**&#x200B;에 대한 설정을 변경하는 경우 clientlibs 캐시의 내용을 삭제하십시오. 자세한 내용은 [기술 자료 문서](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html)를 참조하세요.

>[!NOTE]
>
>이 설정은 [프로덕션 준비 모드](/help/sites-administering/production-ready.md)에서 AEM을 실행하는 경우 프로덕션 인스턴스에 대해 자동으로 구성됩니다.

**일 CQ HTTP 헤더 인증 처리기** HTTP 요청의 기본 인증 방법에 대한 시스템 전체 설정입니다.

[폐쇄된 사용자 그룹](/help/sites-administering/cug.md)을(를) 사용하는 경우 특히 다음을 구성할 수 있습니다.

* **HTTP 영역**
* **기본 로그인 페이지**

**일 CQ 링크 검사기 서비스** 확인 및 필요한 경우 구성:

* 외부 링크를 자동으로 확인할 간격을 정의하는 **스케줄러 기간**.

* 실패한 외부 링크가 잘못된 것으로 간주되는 기간 동안 **잘못된 링크 허용 간격**&#x200B;을 확인하십시오.
* 링크 검사에서 제외할 경로를 정의하려면 **링크 검사 재정의 패턴**&#x200B;을(를) 사용하십시오.

**일 CQ 링크 검사기 작업** 단일 링크 검사기 작업(외부 링크를 검사하는 작업)에 대한 설정을 구성합니다.

* **양호한 링크 테스트 간격** 및 **잘못된 링크 테스트 간격**&#x200B;에 정의된 간격을 확인합니다.

* 링크를 확인할 때 외부 액세스에 필요한 인터넷 액세스 및 NTLM용 프록시와 관련된 다양한 매개 변수입니다.

**일 CQ 메일 서비스** 메일 서버의 호스트 이름과 액세스 세부 정보를 구성합니다. 메일 서비스 구성 섹션을 참조하십시오.

**일 CQ MCM 뉴스레터** 뉴스레터에 사용되는 다양한 설정을 구성합니다.

**일 CQ 루트 매핑** 구성:

* &quot;`/`&quot;에 대한 요청이 리디렉션되는 위치를 정의하는 **대상 경로**.

AEM에는 두 가지 UI가 있습니다.

* 터치 지원 UI는 표준 UI입니다
* 더 이상 사용되지 않는 클래식 UI는 여전히 완전히 작동합니다

AEM 루트 매핑을 사용하여 인스턴스에 대한 기본값으로 보유할 UI를 구성할 수 있습니다.

* 터치 사용 UI를 기본 UI로 사용하려면 **대상 경로**&#x200B;에서 다음을 가리켜야 합니다.

  ```shell
     /projects.html
  ```

* 클래식 UI를 기본 UI로 사용하려면 **대상 경로**&#x200B;에서 다음을 가리켜야 합니다.

  ```shell
     /welcome.html
  ```

>[!NOTE]
>
>표준 설치에서 터치에 적합한 UI가 기본 UI입니다.

**Granite SSO 인증 처리기 Adobe** - SSO(Single Sign-On) 세부 정보를 구성합니다. 이러한 세부 정보는 종종 LDAP를 사용하는 엔터프라이즈 작성자 설정에서 필요합니다.

다양한 구성 속성을 사용할 수 있습니다.

* **경로**
이 인증 처리기가 활성 상태인 경로입니다. 이 매개 변수를 비워 두면 인증 처리기가 비활성화됩니다. 예를 들어 경로 / 는 인증 핸들러가 전체 저장소에 대해 사용되도록 합니다.

* **서비스 순위**
OSGi 프레임워크 서비스 순위 값은 이 서비스 호출에 사용되는 순서를 나타내는 데 사용됩니다. 이 값은 값이 높을수록 우선 순위가 높은 `int` 값입니다.
기본값은 `0`입니다.

* **헤더 이름**
사용자 ID가 포함될 수 있는 헤더의 이름입니다.

* **쿠키 이름**
사용자 ID가 포함될 수 있는 쿠키의 이름입니다.

* **매개 변수 이름**
사용자 ID를 제공할 수 있는 요청 매개 변수의 이름입니다.

* **사용자 맵**
선택한 사용자의 경우 HTTP 요청에서 추출한 사용자 이름을 자격 증명 객체의 다른 이름으로 바꿀 수 있습니다. 매핑은 여기에 정의되어 있습니다. 사용자 이름 `admin`이(가) 맵 양쪽에 나타나면 매핑이 무시됩니다. 문자 &quot;=&quot;는 앞에 &quot;\&quot;를 사용하여 이스케이프해야 합니다.

* **형식**
사용자 ID가 제공되는 형식을 나타냅니다. 사용:

   * 사용자 ID가 HTTP 기본 인증 형식으로 인코딩된 경우 `Basic`
   * 사용자 ID가 일반 텍스트로 제공되거나 정규 표현식 적용 값을 그대로 사용하거나 정규 표현식을 사용해야 하는 경우 `AsIs`

**일 CQ WCM 디버그 필터** 페이지에 액세스할 때 ?debug=layout과 같은 접미사를 사용할 수 있으므로 개발할 때 유용합니다. 예를 들어, https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout 은 개발자가 관심을 가질 수 있는 레이아웃 정보를 제공합니다.

* 성능과 보안을 유지하려면 프로덕션 인스턴스에서 을 비활성화합니다.

**일 CQ WCM 필터** 구성:

* 기본 모드를 정의할 **WCM 모드**.
* 작성자 인스턴스에서 이 모드는 `edit`, `disable,preview` 또는 `analytics`일 수 있습니다.
다른 모드는 사이드 킥에서 액세스하거나 접미사 `?wcmmode=disabled`을(를) 사용하여 프로덕션 환경을 에뮬레이션할 수 있습니다.

* 게시 인스턴스에서 다른 모드에 액세스할 수 없도록 하려면 이 모드를 `disabled`(으)로 설정해야 합니다.

>[!NOTE]
>
>이 설정은 [프로덕션 준비 모드](/help/sites-administering/production-ready.md)에서 AEM을 실행하는 경우 프로덕션 인스턴스에 대해 자동으로 구성됩니다.

**일 CQ WCM 링크 검사기 구성자** 구성:

* 콘텐츠 기반 링크 검사기 구성의 위치 목록을 지정하는 **다시 작성 구성 목록**. 구성은 실행 모드를 기반으로 할 수 있습니다. 링크 검사기 설정이 다를 수 있으므로 이 사실은 작성자와 게시 환경을 구분하는 데 중요합니다.

**일 CQ WCM 페이지 관리자 팩터리** 구성:

* 복제 권한이 없는 사용자가 페이지를 삭제하거나 이동할 수 있도록 **페이지 하위 트리 활성화 확인**(페이지가 활성화되지 않은 경우에도)

**일 CQ WCM 페이지 프로세서** 구성:

* **경로**, `jcr:Event`을(를) 트리거하기 전에 시스템이 페이지 수정 내용을 수신하는 위치 목록입니다.

**Adobe 페이지 노출 횟수 추적기** 작성자 인스턴스의 경우 다음과 같이 구성하십시오.

* **sling.auth.requirements**: 이 속성의 값을 `-/libs/wcm/stats/tracker`(으)로 설정합니다.

>[!CAUTION]
>
>이 구성을 사용하면 추적 서비스에 대한 익명 요청을 사용할 수 있습니다.

>[!NOTE]
>
>자세한 내용은 [페이지 노출 횟수](/help/sites-deploying/configuring.md#enabling-page-impressions)를 참조하십시오.

게시 인스턴스 구성에 대한 **일 CQ WCM 페이지 통계**:

* 페이지 통계를 추적하는 데 사용되는 URL을 구성하기 위해 데이터를 전송할 **URL**(추적기 요청이 Dispatcher을 거치는 경우 필수). 예를 들어 기본값은 `https://localhost:4502/libs/wcm/stats/tracker`입니다.

* 페이지에 추적 스크립트를 포함할 수 있도록 **추적 스크립트가 활성화됨**(`true`) 또는 비활성화됨(`false`). 기본값은 `false`입니다.

>[!NOTE]
>
>자세한 내용은 [페이지 노출 횟수](/help/sites-deploying/configuring.md#enabling-page-impressions)를 참조하십시오.

**일 CQ WCM 버전 관리자** 시스템에서 버전을 관리하는 경우 및 방법을 제어합니다.

* 표준 설치에서 활성화된 **활성화 시 버전 만들기**
* **제거 사용**

* **경로 제거**, 검색 작업에서 검색하는 경로입니다.
* 암시적 버전 관리가 활성화된 경로인 **암시적 버전 관리 경로**.

* **최대 버전 사용 기간**, 버전의 최대 사용 기간(일)

* **최대 버전 수**, 유지할 최대 버전 수

자세한 내용은 [버전 제거](/help/sites-deploying/version-purging.md)를 참조하십시오.

**일 CQ 워크플로우 전자 메일 알림 서비스** 워크플로우에서 보내는 알림에 대한 전자 메일 설정을 구성합니다.

**CQ 재작성기 HTML 파서 팩터리**

CQ 재작성기의 HTML 파서를 제어합니다.

* **처리할 추가 태그** - 파서에서 처리할 HTML 태그를 추가하거나 제거할 수 있습니다. 기본적으로 A,IMG,AREA,FORM,BASE,LINK,SCRIPT,BODY,HEAD 태그가 처리됩니다.
* **카멜 대/소문자 유지** - 기본적으로 HTML 파서는 카멜 대/소문자(예: `eBay`)의 특성을 소문자(예: `ebay`)로 변환합니다. 이 설정을 해제하면 카멜 대/소문자 특성을 유지할 수 있습니다. 이 설정은 Angular 2와 같은 프론트엔드 프레임워크를 사용할 때 유용합니다.

**Day Commons JDBC 연결 풀** 컨텐츠의 소스로 사용되는 외부 데이터베이스에 대한 액세스를 구성합니다.

여러 인스턴스를 구성할 수 있는 출하 시 구성.

자산/바이너리가 안전한 방법으로 최종 사용자에게 전달되도록 AEM과 CDN 간의 **CDN 재작성기** 통신이 보장되어야 합니다. 이 프로세스에는 다음 두 가지 작업이 포함됩니다.

* 처음(또는 캐시에서 만료된 후) CDN을 통해 AEM에서 리소스에 액세스합니다.
* CDN에서 캐시된 리소스에 안전하게 액세스합니다. 리소스가 CDN에 캐시된 후에는 요청이 AEM으로 이동하지 않으므로 의 해당 리소스에 대한 액세스 권한이 있는 모든 사용자가 CDN에서 서비스를 받아야 합니다.

AEM은 내부 자산 URL을 외부 CDN URL로 재작성할 수 있는 재작성기를 제공합니다. 자산에 안전하게 액세스할 수 있도록 JWS 서명 및 만료 시간을 포함하여 CDN에 전달될 링크를 재작성합니다. 이 기능은 작성자 인스턴스에서 사용됩니다.

전체적인 흐름은 다음과 같습니다.

1. 사용자가 AEM을 통해 인증하고 에셋이 있는 페이지를 요청합니다.
1. 요청된 페이지에 `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`과(와) 유사한 자산이 포함되어 있습니다.
1. 재작성기는 링크를 JWS 서명이 포함된 CDN URL로 변환합니다.
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. 그런 다음 사용자의 브라우저가 자산 요청을 CDN 서버에 전달합니다
1. CDN은 `cdn_sign` 매개 변수와 함께 AEM에 요청을 전달하도록 구성해야 합니다.
1. 인증 처리기가 `cdn_sign` 매개 변수의 유효성을 검사하고 자산을 CDN으로 반환하면 사용자에게 전달됩니다.

사용자의 브라우저, CDN 및 AEM 간의 흐름은 다음과 같이 시각화할 수 있습니다.

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>이 기능은 AEM 작성자 인스턴스에만 활성화됩니다.

**CDNConfigServiceImpl**&#x200B;에서 CDN 구성을 제공합니다.

CDN 재작성 기능은 com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl의 구성에서 **CDN 배포 도메인 이름**&#x200B;을 제공하여 활성화할 수 있습니다.

이 서비스에는 CDN 재작성 활성화/비활성화, CDN 재작성이 수행되는 경로 접두사, TTL 값 및 프로토콜(HTTP 또는 HTTPS)과 같은 다른 구성 옵션도 포함되어 있습니다.

**CDNRewriter** 내부 이미지 URL을 CDN URL로 다시 쓰는 재작성기

선택적 이미지 링크만 다시 쓰도록 com.adobe.cq.cdn.rewriter.impl.CDNRewriter의 **태그 특성** 값을 정의할 수 있습니다.
