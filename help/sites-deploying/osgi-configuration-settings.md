---
title: OSGi 구성 설정
seo-title: OSGi 구성 설정
description: 이 문서에서는 프로젝트 구현과 관련된 OSGi 구성 설정(번들에 따라 나열됨)에 대해 자세히 설명합니다. 이 목록은 지침처럼 작동하며 완전한 것은 아닙니다.
seo-description: 이 문서에서는 프로젝트 구현과 관련된 OSGi 구성 설정(번들에 따라 나열됨)에 대해 자세히 설명합니다. 이 목록은 지침처럼 작동하며 완전한 것은 아닙니다.
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
feature: 구성
exl-id: 19eedcf2-140a-452d-aa8f-6fd7f219e5f8
source-git-commit: ca66c0655bcd878644e275fc8f7a41b38110beae
workflow-type: tm+mt
source-wordcount: '3561'
ht-degree: 0%

---

# OSGi 구성 설정{#osgi-configuration-settings}

[](https://www.osgi.org/) OSG는 AEM의 기술 스택에서 기본적인 요소입니다. AEM의 복합 번들과 해당 구성을 제어하는 데 사용됩니다.

OSGi &quot;*에서는 소규모 재사용 가능한 공동 작업 구성 요소에서 응용 프로그램을 구축할 수 있도록 하는 표준화된 프리미티브 집합을 제공합니다. 이러한 구성 요소는 응용 프로그램으로 구성하고*&quot;을 배포할 수 있습니다.

따라서 개별적으로 시작, 중지, 설치 및 설치가 가능하므로 번들을 쉽게 관리할 수 있습니다. 상호 종속성은 자동으로 처리됩니다. 각 OSGi 구성 요소( [OSGi Specification](https://www.osgi.org/Specifications/HomePage) 참조)는 다양한 번들 중 하나에 포함되어 있습니다. AEM을 사용하여 작업하는 경우 이러한 번들에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다.자세한 내용 및 권장 방법은 [OSGi](/help/sites-deploying/configuring-osgi.md) 구성 을 참조하십시오.

다음 OSGi 구성 설정(번들에 따라 나열됨)은 프로젝트 구현과 관련되어 있습니다. 나열된 모든 설정을 조정할 필요는 없으며, AEM 작동 방식을 이해하는 데 도움이 되는 설정이 포함되어 있습니다.

>[!CAUTION]
>
>이 목록은 지침으로 작동하기 위한 것이며, 완전한 것은 아닙니다. 일부 번들이나 일부 번들에 대한 모든 매개 변수가 나열되지는 않습니다.
>
>필요한 구성은 프로젝트마다 다릅니다.
>
>사용된 값과 매개 변수에 대한 자세한 정보는 웹 콘솔을 참조하십시오.

>[!NOTE]
>
>[AEM Tools](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html)의 일부인 OSGi 구성 차이 도구를 사용하여 기본 OSGi 구성을 나열할 수 있습니다.

>[!NOTE]
>
>AEM 내의 특정 기능 영역에 대해 추가 번들이 필요할 수 있습니다. 이러한 경우 구성 세부 사항은 해당 기능과 관련된 페이지에서 확인할 수 있습니다.

**AEM 복제 이벤트** 리스너 구성:

* 복제 이벤트가 리스너에 배포되는 **실행 모드**&#x200B;입니다. 예를 들어 작성자로 정의된 경우 이 시스템은 복제를 &quot;시작&quot;하는 시스템입니다.

* 프로젝트 코드가 게시 환경에서 복제 이벤트(역복제)를 처리하는 경우 실행 모드 **게시**&#x200B;를 추가해야 합니다. 예를 들어 디스패처가 게시 환경에서 플러시하는 데 사용되거나 다른 게시 인스턴스에 대한 표준 복제가 발생하는 경우,

**AEM Repository 변경** 리스너구성:

* 배포 준비가 된 저장소 이벤트를 수신할 위치 **경로**&#x200B;입니다.

**CRX Sling Client** Repository기본 컨텐츠 저장소에 대한 액세스를 구성합니다.

* 설치 후 **관리자 암호**&#x200B;를 변경해야 인스턴스의 [보안](/help/sites-administering/security-checklist.md)을 확인할 수 있습니다.
* 다른 변경 사항은 필요하지 않으며 저장소 액세스에 영향을 줄 수 있으므로 주의해야 합니다.

**Wiki 메일** 서비스Wiki에서 보낸 전자 메일에 대한 전자 메일 설정을 구성합니다.

**Apache Felix OSGi Management** Console구성:

* **Apache Felix 웹 관리 콘솔에서 사용할 수 있는 기본 탐색 항목**(콘솔 플러그인) **은** 최상위 메뉴 항목입니다. 각각 공간과 리소스가 필요하므로 필요하지 않은 항목을 비활성화합니다.

>[!CAUTION]
>
>다음을 구성해야 합니다.
>
>**Apache** Felix  **Web Management Console 자체에 액세스하기 위한 자격 증명인 사용자 이름 및 암호**.
>인스턴스의 [security](/help/sites-administering/security-checklist.md)를 확인하려면 처음 설치 후 암호를 변경해야 합니다.

>[!NOTE]
>
>이 구성은 Felix 콘솔을 사용하여 만들어야 리포지토리를 사용할 수 있습니다.

**Apache Sling 사용자 지정 가능 요청 데이터** 로거 구성:

* **로거** 이름 및  **로그** 형식을 사용하여 요청 및 액세스 로깅의 위치 및 형식을 구성합니다(기본값: `request.log`). 이 로그 파일은 웹 체인과 관련된 성능 또는 디버깅 기능을 분석할 때 반드시 필요합니다.
이는 [Apache Sling Request Logger](#apacheslingrequestlogger)와 쌍입니다.

자세한 내용은 [AEM 로깅](/help/sites-deploying/configure-logging.md) 및 [Sling 로깅](https://sling.apache.org/site/logging.html)을 참조하십시오.

**Apache Sling Eventing 스레드** 풀 구성:

* **최소 풀** 크기 및  **최대 풀 크기**(이벤트 스레드를 보유하는 데 사용되는 풀 크기)입니다.

* **대기열 크기** - 풀이 모두 소진된 경우 스레드 큐의 최대 크기입니다.
큐가 무제한으로 설정되므로 권장되는 값은 `-1`입니다.제한을 설정하면 제한을 초과할 때 손실이 발생할 수 있습니다.

* 이러한 설정을 변경하면 많은 이벤트가 있는 시나리오에서 성능이 저하될 수 있습니다.예를 들어, 많은 AEM DAM 또는 워크플로우 사용.
* 시나리오에 고유한 값은 테스트를 사용하여 설정해야 합니다.
* 이러한 설정은 인스턴스의 성능에 영향을 줄 수 있으므로 이유 및 고려 사항 없이 변경하지 마십시오.

**Apache Sling GET** 서블릿렌더링의 몇 가지 측면을 구성합니다.

* **검색** 을 위해 디렉터리 렌더링을 활성화/비활성화합니다.
* **HTML** ,  **일반 텍스트**,  **JSON 또는** XML **** 과 같은 기본 변환 **을 활성화(또는**비활성화)합니다.
JSON을 비활성화하면 안 됩니다.

>[!NOTE]
>
>이 설정은 [프로덕션 준비 모드](/help/sites-administering/production-ready.md)에서 AEM을 실행하는 경우 프로덕션 인스턴스에 대해 자동으로 구성됩니다.

**Apache Sling Java Script Handler** .java 파일을 스크립트(서블릿)로 컴파일하기 위한 설정을 구성합니다.

특정 설정은 성능에 영향을 줄 수 있으며, 가능한 경우, 특히 프로덕션 인스턴스의 경우 비활성화해야 합니다.

* S **소스 VM** 및 **Target VM**&#x200B;런타임 JVM으로 사용되는 JDK 버전을 정의합니다

* 프로덕션 인스턴스의 경우:

   * 비활성화 **디버그 정보 생성**

**Apache Sling JCR** 설치 프로그램이러한 매개 변수는 구성이 필요하지 않을 수 있지만 개발 또는 디버깅할 때 유용할 수 있습니다. 예를 들어 설치 폴더는 패키지를 체크 인하거나 체크 아웃하는 데 유용할 수 있습니다.

* **설치 폴더 이름** 은 설치 폴더의  **최대 계층 깊이를 나타냅니다** . 저장소 폴더의 설치 위치와 깊이를 지정합니다. 와일드카드를 사용할 때(에서와 같이)*/install) 과 같은 모든 적절한 일치 항목을 검색합니다(예: `/libs/sling/install` 및 `/libs/cq/core/install`).

* **검색 경로**, jcrinstall에서 설치할 리소스를 검색하는 경로 목록과 해당 경로의 가중치 요소를 나타내는 숫자를 추가합니다.

**Apache Sling 작업 이벤트** 핸들러 작업 예약을 관리하는 매개 변수를 구성합니다.

* **다시 시도 간격**,  **최대 다시 시도**,  **최대 병렬 작업**,  **대기 시간 승인** 등을 선택할 수 있습니다.

* 이러한 설정을 변경하면 많은 수의 작업이 있는 시나리오의 성능이 향상됩니다.예를 들어 AEM DAM 및 워크플로우의 사용량이 많습니다.
* 시나리오에 고유한 값은 테스트를 사용하여 설정해야 합니다.
* 이유 없이 이러한 설정을 변경하지 마십시오. 나중에 반드시 고려해야 합니다.

**Apache Sling JSP 스크립트** 핸들러 JSP 스크립트 핸들러의 성능 관련 설정을 구성합니다. 성능을 향상시키려면 가능한 한 많이 비활성화해야 합니다.

특히 프로덕션 인스턴스의 경우:

* 비활성화 **디버그 정보 생성**
* 비활성화 **생성된 Java 유지**
* **매핑된 콘텐츠 비활성화**
* **소스 조각 표시** 비활성화

>[!NOTE]
>
>이 설정은 [프로덕션 준비 모드](/help/sites-administering/production-ready.md)에서 AEM을 실행하는 경우 프로덕션 인스턴스에 대해 자동으로 구성됩니다.

**Apache Sling 로깅** 구성:

* **로그** 및  **로그 파일**&#x200B;을 사용하여 중앙 로깅 구성의 위치 및 로그 수준을 정의합니다(error.log). 수준은 `DEBUG`, `INFO`, `WARN`, `ERROR` 및 `FATAL` 중 하나로 설정할 수 있습니다.

* **로그 파일** 및  **로그 파일** 임계값 수 로그 파일의 크기와 버전 순환을 정의합니다.

* **메시지** 패턴은 로그 메시지의 형식을 정의합니다.

자세한 내용은 [AEM 로깅](/help/sites-deploying/configure-logging.md#global-logging) 및 [Sling 로깅](https://sling.apache.org/site/logging.html)을 참조하십시오.

**Apache Sling Logging Logger 구성(출하 시 구성)** 구성:

* **로그 수준**,  **로그** 파일 및  **메시지 형식** 을 사용하여 로그 파일 및 메시지의 세부 정보를 정의합니다.

* **** 카테고리를 정의하기 위한 로저링예를 들어 com.day.cq에 대해서만 기록됩니다.

* **출하 시 구성**&#x200B;을 사용하면 필요한 다양한 로그 수준 및 카테고리에 맞는 추가 구성을 추가할 수 있습니다.
* 이러한 구성은 개발 중에 유용합니다.예를 들어 특정 서비스에 대한 TRACE 메시지를 특정 로그 파일에 기록하려면
* 이러한 구성은 프로덕션 환경에서 유용합니다.예를 들어, 보다 쉽게 모니터링할 수 있도록 개별 로그 파일에 기록된 특정 서비스에 대한 메시지가 있을 수 있습니다.

자세한 내용은 [AEM 로깅](/help/sites-deploying/configure-logging.md) 및 [Sling 로깅](https://sling.apache.org/site/logging.html)을 참조하십시오.

**Apache Sling 로깅 작성기 구성(출하 시 구성)** 구성:

* **로그** 파일 을 사용하여 로그 파일이 있는지 확인합니다.
* **버전 순환** 을 정의하는 로그 파일 수입니다.

* 작성기는 **Apache Sling Logging Configuration** 구성에서 사용할 수 있습니다.

* 이러한 구성은 개발 중에 유용합니다.예를 들어 특정 서비스에 대한 TRACE 메시지를 특정 로그 파일에 기록하려면
* 이러한 구성은 프로덕션 환경에서 유용합니다.예를 들어, 보다 쉽게 모니터링할 수 있도록 개별 로그 파일에 기록된 특정 서비스에 대한 메시지가 있을 수 있습니다.

자세한 내용은 [AEM 로깅](/help/sites-deploying/configure-logging.md) 및 [Sling 로깅](https://sling.apache.org/site/logging.html)을 참조하십시오.

**Apache Sling 기본 ServletConfigure** :

* **무한 재귀 및** 과도한 스크립트 호출에서  **시스템** 을 보호하기 위한 요청당 호출 수 및 반복 깊이.

**Apache Sling MIME 유형** ServiceConfigure:

* **프로젝트** 에 필요한 MIME 유형을 시스템에 추가합니다. 이렇게 하면 파일에 대한 `GET` 요청에서 파일 형식과 응용 프로그램을 연결하는 올바른 콘텐츠 형식 헤더를 설정할 수 있습니다.

**Apache Sling Referrer** FilterCRX WebDAV 및 Apache Sling에서 CSRF(교차 사이트 요청 위조) 관련 알려진 보안 문제를 해결하려면 레퍼러 필터를 구성해야 합니다.

레퍼러 필터 서비스는 다음을 구성할 수 있는 OSGi 서비스입니다.

* 필터링해야 하는 http 메서드
* 빈 레퍼러 헤더가 허용되는지 여부
* 서버 호스트 외에 허용되는 서버 목록입니다.

자세한 내용은 [보안 검사 목록 - 사이트 간 요청 위조 시 발생하는 문제](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)를 참조하십시오.

>[!NOTE]
>
>Apache Sling 레퍼러 필터는 빠른 수정 패키지 설치에 따라 다릅니다.

**Apache Sling Request** Logger 구성:

* 다양한 매개 변수로 요청이 기록되는 방식을 정의할 수 있습니다.
* **요청 로그** 를 활성화하거나 비활성화합니다.

* **액세스 로그** 를 활성화하거나 비활성화합니다.

이는 [Apache Sling 사용자 지정 가능 요청 데이터 로거](#apacheslingcustomizablerequestdatalogger)와 쌍입니다.

자세한 내용은 [AEM 로깅](/help/sites-deploying/configure-logging.md) 및 [Sling 로깅](https://sling.apache.org/site/logging.html)을 참조하십시오.

**Apache Sling Resource Resolver** FactorySling 리소스 확인의 중앙 측면을 구성합니다.

* **리소스 검색 경로**, 프로젝트별 경로를 추가합니다(또는  `/libs`  `/apps`를 제거하지 않음).

* **별칭** URL 매핑을 정의하는 가상 URL입니다.

* **별칭** 을 정의하기 위한 URL 매핑예: 부터  `/content` 까지  `/`.

* **매핑 위치** 에서 외부화된 맵 구성  `/etc/map`.

* 로컬 설치(예: `https://localhost:4502/system/console/jcrresolver`)를 사용하여 활성 상태인 리소스 확인자를 확인합니다.

자세한 내용은 다음을 참조하십시오.[https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution)

>[!CAUTION]
>
>특히 이러한 옵션은 리포지토리에서 구성해야 합니다.
>
>그렇지 않은 경우 Felix 콘솔을 사용하여 **URL 매핑**&#x200B;에 변경한 내용은 다음 시작 시 AEM에서 덮어쓸 수 있습니다.

**Apache Sling Servlet/Script Resolver 및 Error** HandlerSling Servlet 및 Script Resolver에는 다음과 같은 여러 작업이 있습니다.

1. 요청을 처리하기 위해 호출할 서블릿 또는 스크립트를 선택하는 데에는 `ServletResolver` 로 사용됩니다.

1. `SlingScriptResolver` 역할을 합니다.

1. 동일한 알고리즘을 사용하여 `ErrorHandler` 인터페이스를 구현하여 요청 처리 서블릿 및 스크립트를 해결하는 데 사용되는 대로 오류 처리 서블릿 및 스크립트를 선택하여 오류 처리를 관리합니다.

다음을 포함한 다양한 매개 변수를 설정할 수 있습니다.

* **실행 경로** 가 경로를 슬립하여 실행 스크립트를 검색합니다.특정 경로를 구성하면 실행할 수 있는 스크립트를 제한할 수 있습니다. 경로를 구성하지 않으면 기본값이 사용됩니다( `/` = 루트). 이렇게 하면 모든 스크립트를 실행할 수 있습니다.
구성된 경로 값이 슬래시로 끝나는 경우 전체 하위 트리가 검색됩니다. 이 후행 슬래시가 없으면 스크립트가 정확히 일치하는 경우에만 실행됩니다.

* **스크립트 사용자**  - 이 선택적 속성은 스크립트를 읽는 데 사용되는 저장소 사용자 계정을 지정할 수 있습니다. 계정을 지정하지 않으면 기본적으로 `admin` 사용자가 사용됩니다.

* **기본** 확장기본 동작을 사용할 확장 목록입니다. 즉, 리소스 유형의 마지막 경로 세그먼트를 스크립트 이름으로 사용할 수 있습니다.

**Day Commons GFX Font** Helper그래픽을 렌더링할 때 DrawText를 사용하여 텍스트를 포함할 수 있습니다. 이를 위해 고유한 글꼴을 설치할 수도 있습니다.

* 프로젝트별 글꼴을 검색할 **글꼴 경로**를 정의합니다.
예, `/apps/myapp/fonts`.

**HTTP를 만들** 때 사용되는 Apache HTTP 클라이언트를 사용하는 모든 코드에 대한 Apache HTTP 구성 요소 프록시 구성예를 들어 복제 시

새 구성을 생성할 때 공장 구성을 변경하지 말고 여기에서 사용할 수 있는 구성 관리자를 사용하여 이 구성 요소에 대한 새 출하 시 구성을 만드십시오.**https://localhost:4502/system/console/configMgr/** 프록시 구성은 **org.apache.http.proxyconfigurator에서 사용할 수 있습니다.**

>[!NOTE]
>
>AEM 6.0 및 이전 릴리스 프록시에서 Day Commons HTTP Client에 프록시가 구성되었습니다. AEM 6.1 이후 릴리스에서 프록시 구성이 &#39;Day Commons HTTP Client&#39; 구성 대신 &quot;Apache HTTP 구성 요소 프록시 구성&quot;으로 이동되었습니다.

**Day CQ** Antispam사용된 스팸 방지 서비스(Akismet)를 구성합니다. 이를 위해서는 다음을 등록해야 합니다.

* **공급자**
* **API 키**
* **등록된 URL**

**Adobe Granite HTML 라이브러리** 관리자클라이언트 라이브러리(css 또는 js)의 처리를 제어하도록 구성합니다.예를 들어 기본 구조가 표시되는 방식을 포함합니다.

* 프로덕션 인스턴스의 경우:

   * **Minify**(CRLF 및 공백 문자를 제거하려면) 활성화합니다.
   * **Gzip**&#x200B;을 활성화합니다(하나의 요청으로 파일을 압축하고 액세스할 수 있도록 허용).
   * **Debug** 비활성화
   * **타이밍** 비활성화

* JS 개발 시(특히 디버깅/디버깅 시):

   * **Minify** 비활성화
   * **Debug**&#x200B;를 활성화하여 디버깅을 위해 파일을 구분하고 firebug와 함께 사용합니다.
   * 타이밍에 관심이 있는 경우 **타이밍**&#x200B;을 활성화합니다.
   * **Debug** 콘솔을 활성화하여 JS 콘솔 로그 메시지를 봅니다.

>[!CAUTION]
>
>**Minify** 또는 **Gzip**&#x200B;에 대한 설정을 변경할 때 `/var/clientlibs`의 콘텐츠도 삭제해야 합니다. clientlibs의 캐싱된 버전이며 다음 요청이 있을 때 다시 빌드됩니다.

>[!NOTE]
>
>이 설정은 [프로덕션 준비 모드](/help/sites-administering/production-ready.md)에서 AEM을 실행하는 경우 프로덕션 인스턴스에 대해 자동으로 구성됩니다.

**일별 CQ HTTP 헤더 인증** 핸들러HTTP 요청의 기본 인증 방법에 대한 시스템 전체 설정입니다.

[닫힌 사용자 그룹](/help/sites-administering/cug.md)을 사용할 때 (다른 그룹 중에서) 다음을 구성할 수 있습니다.

* **HTTP 영역**
* **기본 로그인 페이지**

**일별 CQ 링크 확인** 서비스 확인 및 필요한 경우 구성:

* **스케줄러** 기간: 외부 링크를 자동으로 확인할 간격을 정의합니다.

* 실패한 외부 링크가 잘못된 것으로 간주되는 기간에 대해 **잘못된 링크 허용한도 간격**&#x200B;을 선택합니다.
* **링크 확인 무시 패턴** 을 사용하여 링크 확인에서 제외할 경로를 정의합니다.

**일별 CQ 링크 확인** 작업단일 링크 확인 작업(외부 링크를 확인하는 작업)에 대한 설정을 구성합니다.

* **양호한 링크 테스트 간격** 및 **잘못된 링크 테스트 간격**&#x200B;에 정의된 간격을 확인합니다

* 링크를 확인할 때 외부 액세스에 필요한 NTLM 및 인터넷 액세스를 위한 프록시와 관련된 다양한 매개 변수입니다.

**일 CQ 메일** 서비스메일 서버의 호스트 이름 및 액세스 세부 정보를 구성합니다. 메일 서비스 구성 섹션을 참조하십시오.

**Day CQ MCM** NewsletterNewsletter에 사용되는 다양한 설정을 구성합니다.

**일 CQ 루트** 매핑구성:

* **Target** &quot;에 대한 요청이  `/`리디렉션되는 위치를 정의하는 경로.

AEM에는 두 가지 UI가 있습니다.

* 터치 지원 UI는 표준 UI입니다
* 기본 클래식 UI는 여전히 완벽하게 작동합니다

AEM 루트 매핑 을 사용하여 인스턴스에 대한 기본값으로 사용할 UI를 구성할 수 있습니다.

* 터치 활성화 UI를 기본 UI로 사용하려면 **Target 경로**&#x200B;가 다음과 같이 가리켜야 합니다.

   ```
      /projects.html
   ```

* 클래식 UI를 기본 UI로 사용하려면 **Target 경로**&#x200B;가 다음을 가리켜야 합니다.

   ```
      /welcome.html
   ```

>[!NOTE]
>
>표준 설치 시 터치에 적합한 UI가 기본 UI입니다.

**Adobe Granite SSO 인증** 처리기SSO(Single Sign On) 세부 사항 구성;이러한 요구 사항은 종종 LDAP와 함께 엔터프라이즈 작성자 설정에서 필요합니다.

다양한 구성 속성을 사용할 수 있습니다.

* ****
이 인증 처리기가 활성 상태인 경로 이 매개 변수를 비워 두면 인증 처리기가 비활성화됩니다. 예를 들어 경로 / 는 전체 저장소에 대해 인증 핸들러를 사용합니다.

* **서비스**
RankingOSGi Framework Service Ranking 값은 이 서비스를 호출하는 데 사용되는 순서를 나타내는 데 사용됩니다. 이것은 
`int` 값이 높을수록 우선순위가 높은 값
기본값은 `0`입니다.

* **헤더**
이름 사용자 ID를 포함할 수 있는 헤더의 이름입니다.

* **쿠키**
이름 사용자 ID를 포함할 수 있는 쿠키의 이름입니다.

* **매개**
변수 이름사용자 ID를 제공할 수 있는 요청 매개 변수의 이름입니다.

* **사용자**
맵선택한 사용자의 경우, HTTP 요청에서 추출한 사용자 이름을 자격 증명 개체의 다른 이름으로 바꿀 수 있습니다. 매핑이 여기에서 정의됩니다. 사용자 이름이 
`admin` 맵의 양쪽에 나타나는 매핑은 무시됩니다. 문자 &quot;=&quot;는 앞에 &quot;\&quot;를 사용하여 이스케이프 처리해야 합니다.

* ****
형식사용자 ID가 제공되는 형식을 나타냅니다. 사용:

   * `Basic` 사용자 ID가 HTTP 기본 인증 형식으로 인코딩된 경우
   * `AsIs` 사용자 ID가 일반 텍스트로 제공되거나 정규 표현식 적용 값을 그대로 또는 정규 표현식으로 사용해야 하는 경우

**일별 CQ WCM 디버그** 필터페이지를 액세스할 때 ?debug=layout과 같은 접미사를 사용할 수 있으므로 개발할 때 유용합니다. 예를 들어 https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout 은 개발자에게 관심이 있을 수 있는 레이아웃 정보를 제공합니다.

* 프로덕션 인스턴스에서 이 기능을 비활성화하여 성능과 보안을 보장합니다.

**일 CQ WCM** 필터 구성:

* **WCM 모드 **를 클릭하여 기본 모드를 정의합니다.
* 작성자 인스턴스에서 이는 `edit`, `disable,preview` 또는 `analytics`일 수 있습니다.
다른 모드는 사이드 킥에서 액세스할 수 있고, 접미사 `?wcmmode=disabled`는 프로덕션 환경을 에뮬레이션하는 데 사용할 수 있습니다.

* 게시 인스턴스에서 다른 모드에 액세스할 수 없도록 하려면 이 모드를 `disabled` 로 설정해야 합니다.

>[!NOTE]
>
>이 설정은 [프로덕션 준비 모드](/help/sites-administering/production-ready.md)에서 AEM을 실행하는 경우 프로덕션 인스턴스에 대해 자동으로 구성됩니다.

**구성일 CQ WCM 링크 확인** 구성:

* **콘텐츠 기반** 링크 확인 구성에 대한 위치 목록을 지정하는 재작성 구성 목록입니다. 구성은 실행 모드를 기반으로 할 수 있습니다.링크 확인 설정은 다를 수 있으므로 작성자와 게시 환경을 구분하는 것이 중요합니다.

**요일 CQ WCM 페이지** 프로세서구성:

* **경로**: 시스템이 페이지를 트리거하기 전에 페이지 수정 사항을 수신하는 위치  `jcr:Event`목록입니다.

**Adobe 페이지 노출 횟수** 추적기 작성자 인스턴스 구성의 경우:

* **sling.auth.requirements**:이 속성의 값을 로 설정합니다.  `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>이 구성에서는 추적 서비스에 대한 익명 요청을 허용합니다.

>[!NOTE]
>
>자세한 내용은 [페이지 노출 횟수](/help/sites-deploying/configuring.md#enabling-page-impressions)를 참조하십시오.

**일 CQ WCM 페이지** 통계게시 인스턴스의 경우

* **페이지 통계** 를 추적하는 데 사용되는 URL을 구성하여 데이터를 전송할 URL입니다(추적기 요청이 디스패처를 통과하는 경우 필수).예를 들어 기본값은  `https://localhost:4502/libs/wcm/stats/tracker`입니다.

* **추적 스크립트** 는 페이지에서 추적 스크립트 포함을 활성화(  `true`)하거나 비활성화(  `false`)하도록 활성화됩니다. 기본값은 `false`입니다.

>[!NOTE]
>
>자세한 내용은 [페이지 노출 횟수](/help/sites-deploying/configuring.md#enabling-page-impressions)를 참조하십시오.

**Day CQ WCM Version** Manager시스템에서 버전이 관리되는 경우 및 방법을 제어합니다.

* **활성화 버전 만들기** - 표준 설치에서 활성화됨
* **삭제 활성화**

* **경로 제거**, 검색 작업이 검색할 경로
* **암시적 버전 지정 경로**: 암시적 버전 관리가 활성화된 경로입니다.

* **최대 버전 나이**, 버전의 최대 연령(일)

* **최대 버전 수**, 유지할 최대 버전 수

자세한 내용은 [버전 삭제](/help/sites-deploying/version-purging.md)를 참조하십시오.

**일별 CQ 워크플로우 이메일 알림** 서비스워크플로우에서 보낸 알림에 대한 이메일 설정을 구성합니다.

**CQ 재작성기 HTML Parser Factory**

CQ 다시 작성기의 HTML 파서를 제어합니다.

* **처리할 추가 태그**  - 파서에서 처리할 HTML 태그를 추가하거나 제거할 수 있습니다. 기본적으로 다음 태그가 처리됩니다.A,IMG,AREA,FORM,BASE,LINK,SCRIPT,BODY,HEAD
* **카멜 표기법 유지**  - 기본적으로 HTML 파서는 카멜 표기법(예: eBay)의 특성을 소문자로 변환합니다(예: ebay). 카멜 표기법 특성을 유지하려면 이 설정을 해제할 수 있습니다. 이 기능은 Angular 2과 같은 프런트 엔드 프레임워크를 사용할 때 유용합니다.

**Day Commons JDBC Connections** Pool 컨텐츠에 대한 소스로 사용되는 외부 데이터베이스에 대한 액세스를 구성합니다.

출하 시 구성이므로 여러 인스턴스를 구성할 수 있습니다.

**Adobe CQ Media DPS 세션 서비스** 발행물에서 사용할 DPS 세션을 관리합니다.

특히 `dps.session.service.url.name` 을 정의할 수 있습니다.기본값은 [https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions](https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions)로 설정됩니다.

**자산/** 바이너리가 안전한 방식으로 최종 사용자에게 전달되도록 AEM과 CDN 간의 CDN RewriterCommunication을 보장해야 합니다. 여기에는 두 가지 작업이 포함됩니다.

* CDN을 통해 AEM에서 리소스에 처음으로 액세스하는 경우(또는 캐시에서 리소스가 만료된 후)
* CDN에 리소스가 캐시되면 CDN에 해당 리소스에 액세스할 수 있는 요청이 AEM으로 이동하지 않고, CDN에서 해당 리소스에 액세스할 수 있는 모든 사용자가 제공되어야 합니다.

AEM에서는 내부 자산 URL을 외부 CDN URL로 다시 작성하는 재작성기를 제공합니다. JWS 서명을 포함하여 CDN에 전달될 링크를 다시 작성하고 자산에 안전하게 액세스할 수 있도록 만료 시간을 포함합니다. 이 기능은 작성자 인스턴스에서 사용됩니다.

전체 흐름은 다음과 같습니다.

1. 사용자가 AEM으로 인증되고 자산이 있는 페이지를 요청합니다.
1. 요청된 페이지에 `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`과 유사한 자산이 포함되어 있습니다
1. 재작성자는 JWS 서명을 포함하는 CDN URL로 링크를 변환합니다.
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. 그러면 사용자의 브라우저가 자산 요청을 CDN 서버에 전달합니다
1. CDN은 `cdn_sign` 매개 변수와 함께 AEM에 요청을 전달하도록 구성해야 합니다.
1. 인증 처리기는 `cdn_sign` 매개 변수의 유효성을 확인하고 자산을 CDN으로 반환한 다음 사용자에게 전달합니다

사용자의 브라우저, CDN 및 AEM 간의 흐름을 다음과 같이 시각화할 수 있습니다.

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>이 기능은 현재 AEM 작성자 인스턴스에만 활성화되어 있습니다.

**** CDNConfigServiceImplCDN 구성 제공

com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl에 대한 구성에 **CDN 배포 도메인 이름**&#x200B;을 제공하여 CDN 재작성 기능을 활성화할 수 있습니다.

또한 이 서비스에는 CDN 재작성을 활성화/비활성화하고, CDN 재작성을 수행하는 경로 접두사, TTL 값 및 프로토콜(HTTP 또는 HTTPS)과 같은 다른 구성 옵션이 포함되어 있습니다.

**** CDNRewriter내부 이미지 URL을 CDN URL로 재작성하는 재기록입니다

com.adobe.cq.cdn.rewriter.impl.CDNRewriter의 **태그 속성** 값을 정의하여 선택적 이미지 링크만 다시 작성할 수 있습니다.
