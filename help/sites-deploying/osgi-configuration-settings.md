---
title: OSGi 구성 설정
seo-title: OSGi 구성 설정
description: 이 문서에서는 프로젝트 구현과 관련된 OSGi 구성 설정(번들에 따라 나열됨)에 대해 자세히 설명합니다. 이 목록은 지침으로 사용되고 철저한 것은 아닙니다.
seo-description: 이 문서에서는 프로젝트 구현과 관련된 OSGi 구성 설정(번들에 따라 나열됨)에 대해 자세히 설명합니다. 이 목록은 지침으로 사용되고 철저한 것은 아닙니다.
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
translation-type: tm+mt
source-git-commit: 0849cfdd0e4f9a614c455214e6520ead07ae6da0

---


# OSGi 구성 설정{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) 는 AEM의 기술 스택에서 기본적인 요소입니다. AEM 및 해당 구성의 복합 번들을 제어하는 데 사용됩니다.

OSGi *는 &quot;애플리케이션이 작고 재사용 가능한 공동 작업 구성 요소로 구성될 수 있도록 하는 표준화된 프리미티브 방식을 제공합니다. 이러한 구성 요소를 애플리케이션으로 구성하고 배포할*&#x200B;수 있습니다.&quot;

이를 통해 번들은 개별적으로 시작, 중지, 설치 및 설치되므로 간편하게 관리할 수 있습니다. 상호 종속성은 자동으로 처리됩니다. 각 OSGi 구성 요소(OSGi [사양](https://www.osgi.org/Specifications/HomePage)참조)는 다양한 번들 중 하나에 포함되어 있습니다. When working with AEM there are several methods of managing the configuration settings for such bundles; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

다음 OSGi 구성 설정(번들에 따라 나열됨)은 프로젝트 구현과 관련이 있습니다. 나열된 모든 설정을 조정할 필요는 없습니다. 일부 설정은 AEM의 작동 방식을 이해하는 데 도움이 됩니다.

>[!CAUTION]
>
>이 목록은 지침으로 사용하기 위한 것이며 철저하지는 않다. 일부 번들이 나열되거나 일부 번들에 대한 모든 매개 변수가 나열되는 것은 아닙니다.
>
>필요한 구성은 프로젝트마다 다릅니다.
>
>사용된 값과 매개 변수에 대한 자세한 내용은 웹 콘솔을 참조하십시오.

>[!NOTE]
>
>AEM 도구의 일부인 OSGi 구성 [비교](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html)도구를 사용하여 기본 OSGi 구성을 나열할 수 있습니다.

>[!NOTE]
>
>AEM 내의 특정 기능 영역에 추가적인 번들이 필요할 수 있습니다. 이러한 경우 구성 세부 사항은 해당 기능과 관련된 페이지에서 찾을 수 있습니다.

**AEM 복제 이벤트 리스너** 구성:

* 복제 **이벤트가**&#x200B;리스너에 배포되는 실행 모드. 예를 들어 작성자로 정의된 경우 복제를 &quot;시작&quot;하는 시스템입니다.

* 프로젝트 코드가 게시 환경에서 복제 이벤트(역복제)를 처리하는 경우 실행 모드 **게시를** 추가해야 합니다. 예를 들어, 디스패처가 게시 환경에서 플러시되는 데 사용되거나 표준 복제가 다른 게시 인스턴스로 발생하는 경우

**AEM 리포지토리 변경 리스너** 구성:

* 경로 ****, 배포할 저장소 이벤트를 수신할 위치.

**CRX Sling 클라이언트** 저장소 기본 컨텐츠 저장소에 대한 액세스를 구성합니다.

* 관리자 **암호는** 설치 후 인스턴스 [보안을](/help/sites-administering/security-checklist.md) 위해 변경해야 합니다.
* 다른 변경 사항은 필요하지 않으며 저장소 액세스에 영향을 줄 수 있으므로 주의해야 합니다.

**Wiki 메일** 서비스 Wiki가 보낸 이메일에 대한 이메일 설정을 구성합니다.

**Apache Felix OSGi 관리 콘솔** 구성:

* **Apache** Felix Web Management Console에서 **최상위 메뉴 항목으로 사용할 수 있는 기본 탐색 항목(콘솔 플러그인** )입니다. 공간 및 리소스가 필요하므로 필요하지 않은 항목을 비활성화합니다.

>[!CAUTION]
>
>다음을 구성해야 합니다.
>
>**Apache** Felix **Web Management Console**자체에 액세스하기 위한 자격 증명인 사용자 이름 및 암호.
>인스턴스의 [보안을](/help/sites-administering/security-checklist.md) 보장하려면 초기 설치 후 암호를 변경해야 합니다.

>[!NOTE]
>
>Felix Console을 사용하여 구성한 후 저장소를 사용할 수 있습니다.

**Apache Sling 사용자 정의 가능한 요청 데이터 로거** 구성:

* **로거 이름** 및 **로그** 형식을 사용하여 요청 및 액세스 로깅의 위치 및 형식을 구성합니다(기본값: `request.log`). 이 로그 파일은 웹 체인과 관련된 성능 또는 디버깅 기능을 분석할 때 반드시 필요합니다.
Apache Sling 요청 [로거와 쌍을 이루었습니다](#apacheslingrequestlogger).

자세한 내용은 AEM [로깅](/help/sites-deploying/configure-logging.md) 및 [슬링 로깅을](https://sling.apache.org/site/logging.html)참조하십시오.

**Apache Sling 이벤트 스레드 풀** 구성:

* **최소 풀 크기** 및 **최대 풀 크기**, 이벤트 스레드를 보유하는 데 사용되는 풀의 크기입니다.

* **대기열**크기, 풀이 다 된 경우 스레드 큐의 최대 크기입니다.
권장 값은 큐를 제한 없이 `-1` 설정할 때와 같습니다.한도를 설정하면 초과될 때 손실이 발생할 수 있습니다.

* 이러한 설정을 변경하면 많은 수의 이벤트가 있는 시나리오의 성능에 도움이 될 수 있습니다.예를 들어 AEM DAM 또는 Workflow 사용량이 많은 경우입니다.
* 시나리오와 관련된 값은 테스트를 사용하여 설정해야 합니다.
* 이러한 설정은 인스턴스의 성능에 영향을 줄 수 있으므로 이유 및 고려 사항 없이 변경하지 마십시오.

**Apache Sling GET Servlet** 렌더링의 일부 측면을 구성합니다.

* **자동 색인** - 검색할 디렉토리 렌더링을 활성화/비활성화합니다.
* **HMTL** , 일반 텍스트, **JSON**&#x200B;또는 **XML**&#x200B;변환과 같은 **기본** ****변환을 활성화(또는 비활성화)합니다.
JSON을 비활성화하면 안 됩니다.

>[!NOTE]
>
>이 설정은 프로덕션 준비 모드에서 AEM을 실행하는 경우 프로덕션 인스턴스에 대해 자동으로 [구성됩니다](/help/sites-administering/production-ready.md).

**Apache Sling Java** Script Handler .java 파일을 스크립트(servlet)로 컴파일하기 위한 설정을 구성합니다.

특정 설정은 성능에 영향을 줄 수 있으며, 가능한 경우, 특히 프로덕션 인스턴스에 대해서는 이 설정을 비활성화해야 합니다.

* 소스&#x200B;**VM** 및 **Target** VM은 런타임 JVM으로 사용되는 JDK 버전을 정의합니다.

* 프로덕션 인스턴스의 경우:

   * 디버그 **정보 생성 비활성화**

**Apache Sling JCR 설치** 관리자 이러한 매개 변수에는 구성이 필요하지 않지만 개발 또는 디버깅 시 유용한 정보를 제공합니다. 예를 들어 설치 폴더는 패키지를 체크 인/체크 아웃하거나 만드는 데 유용할 수 있습니다.

* **설치 폴더 이름** regexp 및 **설치 폴더의** 최대 계층 깊이 - 설치할 리소스를 검색할 위치 및 깊이를 지정합니다. 와일드카드가 사용될 때(와 같이)*/install) 모든 적절한 일치 항목을 검색하게 됩니다(예: `/libs/sling/install` 및 `/libs/cq/core/install`).

* **검색 경로**, jcrinstall이 설치할 리소스를 검색하는 경로 목록과 해당 경로의 가중치를 나타내는 숫자입니다.

**Apache Sling 작업 이벤트** 처리기 작업 예약을 관리하는 매개 변수를 구성합니다.

* **다시 시도 간격**, **최대**&#x200B;재시도 **,**&#x200B;최대 병렬 작업 **,**&#x200B;대기 시간확인 등이있습니다.

* 이러한 설정을 변경하면 작업 수가 많은 시나리오의 성능이 향상될 수 있습니다.예를 들어, AEM DAM 및 워크플로우의 사용량이 많습니다.
* 시나리오와 관련된 값은 테스트를 사용하여 설정해야 합니다.
* 이유 없이 이러한 설정을 변경하지 마십시오. 고려 이후에만 변경하십시오.

**Apache Sling JSP Script** Handler JSP 스크립트 핸들러의 성능 관련 설정을 구성합니다. 성능을 향상시키려면 가능한 한 비활성화해야 합니다.

프로덕션 인스턴스의 경우:

* 디버그 **정보 생성 비활성화**
* 생성된 **Java 유지 비활성화**
* 매핑된 **콘텐츠 비활성화**
* 표시 **소스 조각 비활성화**

>[!NOTE]
>
>이 설정은 프로덕션 준비 모드에서 AEM을 실행하는 경우 프로덕션 인스턴스에 대해 자동으로 [구성됩니다](/help/sites-administering/production-ready.md).

**Apache Sling 로깅 구성** 구성:

* **로그 수준** 및 **로그**&#x200B;파일을 참조하십시오. 레벨을 `DEBUG`, `INFO`, `WARN`및 `ERROR``FATAL`중 하나로 설정할 수 있습니다.

* **로그 파일의 크기** 및 **버전** 회전을 정의하는 로그 파일 및 로그 파일 임계값 수입니다.

* **메시지** 패턴은 로그 메시지의 형식을 정의합니다.

자세한 내용은 AEM [로깅](/help/sites-deploying/configure-logging.md#global-logging) 및 [슬링 로깅을](https://sling.apache.org/site/logging.html)참조하십시오.

**Apache Sling Logger Configuration (Factory Configuration)** 구성:

* **로그**&#x200B;수준, **로그 파일** 및 **메시지 형식을** 사용하여 로그 파일과 메시지의 세부 사항을 정의합니다.

* **로거를** 사용하여 카테고리 정의예를 들어 com.day.cq에 대한 로그만 있을 수 있습니다.

* Factory **구성을**&#x200B;사용하면 필요한 다양한 로그 수준 및 카테고리에 맞는 추가 구성을 추가할 수 있습니다.
* 이러한 구성은 개발 중에 유용합니다.예를 들어 특정 서비스에 대한 추적 메시지를 특정 로그 파일에 기록할 수 있습니다.
* 이러한 구성은 제작 환경에서 유용합니다.예를 들어, 보다 쉽게 모니터링하기 위해 개별 로그 파일에 기록된 특정 서비스에 대한 메시지가 기록되도록 할 수 있습니다.

자세한 내용은 AEM [로깅](/help/sites-deploying/configure-logging.md) 및 [슬링 로깅을](https://sling.apache.org/site/logging.html)참조하십시오.

**Apache Sling Logging Writer 구성(출하 시 구성)** 구성:

* **로그** 파일을 참조하십시오.
* **버전 회전을** 정의하는 로그 파일의 수입니다.

* Apache Sling Logging Logger 구성 **구성에서 작성기를 사용할 수** 있습니다.

* 이러한 구성은 개발 중에 유용합니다.예를 들어 특정 서비스에 대한 추적 메시지를 특정 로그 파일에 기록할 수 있습니다.
* 이러한 구성은 제작 환경에서 유용합니다.예를 들어, 보다 쉽게 모니터링하기 위해 개별 로그 파일에 기록된 특정 서비스에 대한 메시지가 기록되도록 할 수 있습니다.

자세한 내용은 AEM [로깅](/help/sites-deploying/configure-logging.md) 및 [슬링 로깅을](https://sling.apache.org/site/logging.html)참조하십시오.

**Apache Sling Main Servlet** 구성:

* **무한 재귀 및** 과도한 **스크립트 호출으로부터 시스템을 보호하기** 위한 요청당 호출 수 및 재귀 깊이.

**Apache Sling MIME 유형 서비스** 구성:

* **MIME** 유형을 사용하여 프로젝트에 필요한 항목을 시스템에 추가합니다. 이렇게 하면 파일 형식 및 응용 프로그램의 연결에 대한 올바른 내용 유형 헤더를 설정하도록 파일에 대한 `GET` 요청을 할 수 있습니다.

**Apache Sling Referrer** 필터 CRX WebDAV 및 Apache Sling의 CSRF(교차 사이트 요청 위조) 관련 알려진 보안 문제를 해결하려면 레퍼러 필터를 구성해야 합니다.

레퍼러 필터 서비스는 다음을 구성할 수 있는 OSGi 서비스입니다.

* http 메서드를 필터링해야 합니다.
* 빈 레퍼러 헤더가 허용되는지 여부
* 서버 호스트 외에 허용 대상 서버 목록을 표시합니다.

자세한 [내용은 보안 검사 목록 - 사이트 간 요청 위조](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 문제를 참조하십시오.

>[!NOTE]
>
>Apache Sling 레퍼러 필터는 빠른 수정 패키지 설치에 따라 달라집니다.

**Apache Sling 요청 로거** 구성:

* 다양한 매개 변수를 사용하여 요청이 로깅되는 방식을 정의할 수 있습니다.
* **요청 로그를**&#x200B;활성화하거나 비활성화합니다.

* **액세스 로그를**&#x200B;활성화하거나 비활성화합니다.

Apache Sling 사용자 지정 [가능한 요청 데이터 로거와 쌍을 이루었습니다](#apacheslingcustomizablerequestdatalogger).

자세한 내용은 AEM [로깅](/help/sites-deploying/configure-logging.md) 및 [슬링 로깅을](https://sling.apache.org/site/logging.html)참조하십시오.

**Apache Sling Resource Resolver Factory** Sling 리소스 해상도의 중앙 측면 구성:

* **리소스 검색**&#x200B;경로, 프로젝트별 경로 추가( `/libs` 제거 또는 `/apps`제거 안 함)

* **별칭** URL 매핑을 정의하는 가상 URL.

* **별칭을** 정의하는 URL 매핑;예를 `/content` 들어 에서 `/`까지

* **매핑 위치**- 매퍼 구성이 외부화되어 `/etc/map`있습니다.

* 로컬 설치(예: `https://localhost:4502/system/console/jcrresolver`사용)를 사용하여 활성 상태의 리소스 확인자를 결정합니다.

자세한 내용은 다음을 참조하십시오.https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution [](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>특히 이러한 옵션은 저장소에 구성해야 합니다.
>
>그렇지 않으면 Felix **콘솔을** 사용하여 URL 매핑이 변경된 경우 다음 시작 시 AEM이 덮어쓸 수 있습니다.

**Apache Sling Servlet/Script Resolver 및** Error Handler Sling Servlet 및 Script Resolver에는 여러 작업이 있습니다.

1. Servlet 또는 Script를 `ServletResolver` 선택하여 요청을 처리하는 데 사용됩니다.

1. 그 `SlingScriptResolver`역할을 합니다.

1. 또한 동일한 알고리즘을 사용하여 `ErrorHandler` 인터페이스를 구현하여 오류 처리 서블릿과 스크립트를 선택하여 요청 처리 서블릿과 스크립트를 해결하는 데 사용한 대로 오류 처리를 관리합니다.

다음을 포함하여 다양한 매개 변수를 설정할 수 있습니다.

* **실행** 경로에는 실행 스크립트를 검색할 경로가 나열됩니다.특정 경로를 구성하면 실행할 수 있는 스크립트를 제한할 수 있습니다. 경로가 구성되지 않은 경우 기본값이 사용됩니다( `/` = root). 이렇게 하면 모든 스크립트를 실행할 수 있습니다.
구성된 경로 값이 슬래시로 끝나는 경우 전체 하위 트리가 검색됩니다. 이렇게 후행 슬래시가 없으면 스크립트가 정확히 일치하는 경우에만 실행됩니다.

* **스크립트 사용자** - 이 선택적 속성은 스크립트를 읽는 데 사용되는 저장소 사용자 계정을 지정할 수 있습니다. 계정을 지정하지 않으면 기본적으로 `admin` 사용자가 사용됩니다.

* **기본 익스텐션** 기본 동작을 사용할 익스텐션 목록입니다. 즉, 리소스 유형의 마지막 경로 세그먼트를 스크립트 이름으로 사용할 수 있습니다.

**Day Commons GFX Font Helper** 그래픽을 렌더링할 때 DrawText를 사용하여 텍스트를 포함할 수 있습니다. 따라서 고유한 글꼴을 설치할 수도 있습니다.

* 프로젝트별 **글꼴을** 검색할 글꼴 경로를 정의합니다.
예, `/apps/myapp/fonts`.

**HTTP가** 만들어질 때 사용되는 Apache HTTP 클라이언트를 사용하는 모든 코드에 대한 Apache HTTP 구성 프록시 구성예를 들어 복제 시 가능합니다.

새 구성을 만들 때는 공장 구성을 변경하지 말고 여기에서 사용 가능한 구성 관리자를 사용하여 이 구성 요소에 대한 새 출하 시 구성을 만드십시오.https://localhost:4502/system/console/configMgr/ ****. 프록시 구성은 **org.apache.http.proxyconfigurator에서 사용할 수 있습니다.**

>[!NOTE]
>
>AEM 6.0 및 이전 릴리스의 프록시는 Day Commons HTTP 클라이언트에서 구성되었습니다. AEM 6.1 이상 버전에서 프록시 구성이 &#39;Day Commons HTTP Client&#39; 구성 대신 &quot;Apache HTTP 구성 요소 프록시 구성&quot;으로 이동되었습니다.

**하루 CQ 스팸** 방지 사용된 스팸 방지 서비스(Akismet)를 구성합니다. 이렇게 하려면 다음을 등록해야 합니다.

* **공급자**
* **API 키**
* **등록된 URL**

**Adobe Granite HTML Library** Manager 클라이언트 라이브러리(css 또는 js)의 처리를 제어하도록 이 구성;예를 들어 기본 구조가 표시되는 방식을 포함합니다.

* 프로덕션 인스턴스의 경우:

   * 축소 **활성화** (CRLF 및 공백 문자를 제거하려면).
   * gzip **활성화** (하나의 요청으로 파일을 압축하고 액세스할 수 있도록 허용).
   * 디버그 **비활성화**
   * 타이밍 **비활성화**

* JS 개발(특히 방화벽/디버깅 시):

   * 축소 **비활성화**
   * 디버그를 **사용하여** 디버깅할 파일을 구분하고 firebug와 함께 사용할 수 있습니다.
   * 타이밍에 **관심** 있는 경우 타이밍 활성화
   * js **콘솔** 로그 메시지를 보려면 디버그 콘솔을 활성화합니다.

>[!CAUTION]
>
>Minify 또는 Gzip에 대한 **설정을** 변경할 **때** `/var/clientlibs`의 내용을 삭제해야합니다. 이 버전은 클라이언트의 캐시된 버전이며 다음에 요청할 때 다시 빌드됩니다.

>[!NOTE]
>
>이 설정은 프로덕션 준비 모드에서 AEM을 실행하는 경우 프로덕션 인스턴스에 대해 자동으로 [구성됩니다](/help/sites-administering/production-ready.md).

**일 CQ HTTP 헤더 인증** 처리기 HTTP 요청의 기본 인증 방법에 대한 시스템 전체 설정입니다.

폐쇄된 사용자 그룹을 [](/help/sites-administering/cug.md) 사용할 때(다른 그룹 중) 구성할 수 있습니다.

* **HTTP 영역**
* 기본 **로그인 페이지**

**CQ Link Checker Service Check** 및 필요한 경우 다음을 구성합니다.

* **스케줄러** 기간을 참조하십시오.

* 실패한 **외부 링크가** 나쁜 것으로 간주되는 기간 동안 잘못된 링크 허용치 간격을 확인합니다.
* **링크 확인 대체**&#x200B;패턴을 사용하여 링크 확인에서 제외할 경로를 정의합니다.

**CQ의 요일** 링크 검사기 작업 단일 링크 검사기 작업(외부 링크를 확인하는 작업)에 대한 설정을 구성합니다.

* 좋은 링크 테스트 간격 및 **잘못된 링크** 테스트 **간격에 정의된 간격을 확인합니다.**

* 링크를 확인할 때 외부 액세스에 필요한 인터넷 액세스용 프록시 및 NTLM과 관련된 다양한 매개 변수입니다.

**일 CQ 메일** 서비스 메일 서버에 대한 호스트 이름 및 액세스 세부 정보를 구성합니다. 메일 서비스 구성 섹션을 참조하십시오.

**Day CQ MCM Newsletter** Newsletter에 사용되는 다양한 설정을 구성합니다.

**일 CQ 루트 매핑** 구성:

* **타겟** 경로를 사용하여 &quot;&quot; `/`&quot;에 대한 요청이 리디렉션되는 위치를 정의합니다.

AEM 파섹

* 터치 지원 UI는 표준 UI입니다.
* 기본 클래식 UI는 여전히 완벽하게 작동합니다.

AEM 루트 매핑을 사용하여 인스턴스에 대한 기본값으로 사용할 UI를 구성할 수 있습니다.

* 터치 지원 UI를 기본 UI로 사용하려면 타겟 **경로가** 다음을 가리켜야 합니다.

   ```
      /projects.html
   ```

* 클래식 UI를 기본 UI로 사용하려면 타겟 **경로가** 다음을 가리켜야 합니다.

   ```
      /welcome.html
   ```

>[!NOTE]
>
>표준 설치 시 터치에 적합한 UI가 기본 UI입니다.

**Adobe Granite SSO 인증** 처리기 SSO(Single Sign On) 구성 세부 사항;이러한 기능은 LDAP와 함께 기업 작성자 설정에서 자주 필요합니다.

다양한 구성 속성을 사용할 수 있습니다.

* **경로**&#x200B;이 인증 처리기가 활성 상태인 경로입니다. 이 매개 변수를 비워 두면 인증 처리기가 비활성화됩니다. 예를 들어 경로 / 는 전체 저장소에 대해 인증 핸들러를 사용합니다.

* **서비스 등급** OSGi Framework 서비스 등급 값은 이 서비스를 호출하는 데 사용되는 순서를 나타내는 데 사용됩니다. 이 값은 높은 값이 높은 우선 순위를 지정하는 `int` 값입니다.
Default value is `0`.

* **헤더**&#x200B;이름사용자 ID를 포함할 수 있는 헤더의 이름입니다.

* **쿠키**&#x200B;이름 사용자 ID를 포함할 수 있는 쿠키의 이름입니다.

* **매개 변수**&#x200B;이름사용자 ID를 제공할 수 있는 요청 매개 변수의 이름입니다.

* **사용자**&#x200B;맵선택한 사용자의 경우 HTTP 요청에서 추출한 사용자 이름을 자격 증명 개체에서 다른 이름으로 바꿀 수 있습니다. 매핑은 여기에서 정의됩니다. 사용자 이름이 맵의 양쪽에 `admin` 나타나면 매핑이 무시됩니다. &quot;=&quot;라는 문자는 선행 &quot;\&quot;로 이스케이프해야 합니다.

* **형식사용자** ID가 제공되는 형식을 나타냅니다. 사용:

   * `Basic` 사용자 ID 파섹
   * `AsIs` 사용자 ID가 일반 텍스트로 제공되거나 정규 표현식이 적용된 값으로 사용되거나 정규 표현식으로 사용되어야 하는 경우

**일 CQ WCM 디버그** 필터 페이지에 액세스할 때 ?debug=layout과 같은 접미어를 사용할 수 있으므로 개발할 때 유용합니다. 예를 들어 https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout에서는 개발자에게 관심을 가질 수 있는 레이아웃 정보를 제공합니다.

* 프로덕션 인스턴스에서 이 기능을 비활성화하여 성능과 보안을 보장합니다.

**CQ WCM 필터 구성일** :

* **WCM 모드 **를 사용하여 기본 모드를 정의합니다.
* 작성자 인스턴스에서 `edit`또는 `disable,preview` 일 수 `analytics`있습니다.
사이드 킥에서 다른 모드에 액세스하거나 접미어를 사용하여 프로덕션 환경을 에뮬레이션할 `?wcmmode=disabled` 수 있습니다.

* 게시 인스턴스에서 다른 모드에 액세스할 수 없도록 설정해야 `disabled` 합니다.

>[!NOTE]
>
>이 설정은 프로덕션 준비 모드에서 AEM을 실행하는 경우 프로덕션 인스턴스에 대해 자동으로 [구성됩니다](/help/sites-administering/production-ready.md).

**CQ WCM Link Checker Configurator 구성** :

* **컨텐츠 기반 링크 검사기 구성에 대한 위치 목록을 지정하기 위한 재작성 구성** 목록입니다. 구성은 실행 모드를 기반으로 할 수 있습니다.링크 검사 설정이 다를 수 있으므로 작성 환경과 게시 환경을 구분하는 것이 중요합니다.

**CQ WCM 페이지 프로세서 구성일** :

* **경로**, 시스템이 페이지를 트리거하기 전에 페이지 수정을 수신하는 위치 `jcr:Event`목록입니다.

**Adobe 페이지 노출 횟수** 추적기 작성자 인스턴스의 경우:

* **sling.auth.requirements**:이 속성의 값을 `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>이 구성을 사용하면 추적 서비스에 대한 익명의 요청이 허용됩니다.

>[!NOTE]
>
>자세한 [내용은](/help/sites-deploying/configuring.md#enabling-page-impressions) 페이지 임프레션을 참조하십시오.

**일 CQ WCM 페이지 통계** 게시 인스턴스의 경우 다음을 구성합니다.

* **페이지 통계를 추적하는 데 사용되는 URL을 구성하기 위해 데이터를** 보내는 URL(추적기 요청이 디스패처를 통과하는 경우 중요);예를 들어 기본값은 `https://localhost:4502/libs/wcm/stats/tracker`입니다.

* **추적 스크립트를 사용하여** 페이지에 추적 스크립트 포함을 활성화( `true`) 또는 비활성화( `false`)할 수 있습니다. The default value is `false`.

>[!NOTE]
>
>자세한 [내용은](/help/sites-deploying/configuring.md#enabling-page-impressions) 페이지 임프레션을 참조하십시오.

**CQ WCM Version Manager의** 사용 시기 및 사용 방법:

* **표준 설치에서**&#x200B;활성화된 활성화 버전 만들기
* **제거 활성화**

* **경로**&#x200B;제거, 검색 작업이 검색할 경로
* **암시적 버전**&#x200B;지정 경로: 암시적 버전 관리가 활성화된 경로입니다.

* **최대 버전**&#x200B;연령, 버전의 최대 연령(일)

* **최대 버전**&#x200B;수, 유지할 최대 버전 수

자세한 [내용은](/help/sites-deploying/version-purging.md) 버전 삭제를 참조하십시오.

**일 CQ 워크플로우 이메일 알림** 서비스 워크플로우에서 보낸 알림에 대한 이메일 설정을 구성합니다.

**Day CQSE HTTP Service** , CQ Servlet Engine 제어:

* **HTTP의 경우 NIO, **HTTP의 경우 NIO를 사용할지 여부를 나타냅니다. 기본값은 true입니다. HTTP가 활성화된 경우에만 사용됩니다.
* **연결 시간 초과, **연결 시간 초과(밀리초) 이 속성은 HTTP 및 HTTPS 연결 모두에 적용됩니다. 기본값은 60초입니다.

* **HTTPS 활성화,** HTTPS가 활성화되었는지 여부. 기본값은 false입니다.
* **세션 시간 초과**, 분 단위로 지정된 HTTP 세션의 기본 라이프타임. 시간 초과가 0 이하인 경우 세션이 시간 초과되지 않습니다. 기본값은 10분입니다.
* **디버그 로깅**, 디버그 수준 메시지를 작성할지 여부. 기본값은 false입니다.
* **요청 버퍼 크기**, 요청에 대한 버퍼 크기(바이트)입니다. 기본값은 8KB입니다.
* **최대 스레드**&#x200B;수, 요청을 처리하는 데 사용할 최대 스레드 수입니다. 기본값은 200입니다.

다음 속성은 HTTPS가 활성화된 경우에만 적용됩니다.

* **HTTPS 포트**, HTTPS 요청을 수신할 포트입니다. 기본값은 433입니다.
* **HTTPS용** NIO, HTTP에 NIO를 사용할지 여부를 나타냅니다. 기본값은 HTTP용 NIO 속성 값입니다.
* **Keystore**, HTTPS에 사용할 Keystore의 절대 경로입니다. HTTPS가 활성화된 경우 필요합니다.
* **Keystore 암호**, Keystore에 액세스하기 위한 암호.
* **키**&#x200B;별칭, 키 저장소에 있는 비밀 키의 별칭입니다.
* **키 암호**, 암호 - Keystore에서 비밀 키를 잠금 해제합니다.
* **클라이언트 인증서**, 클라이언트가 유효한 인증서를 제공해야 하는 요건. 기본값은 none입니다.

SSL [관련 옵션에 대한 자세한 내용과](/help/sites-administering/ssl-by-default.md) CQSE에 대해 HTTPS를 활성화하는 방법에 대한 전체 설명은 HTTP Over SSL 활성화를 참조하십시오.

**CQ Rewriter HTML 파서 팩토리**

CQ 리기록기의 HTML 구문 분석기를 제어합니다.

* **처리할 추가** 태그 - 파서에서 처리할 HTML 태그를 추가하거나 제거할 수 있습니다. 기본적으로 다음 태그가 처리됩니다.A,IMG,AREA,FORM,BASE,LINK,SCRIPT,BODY,HEAD.
* **카멜 대소문자** 유지 - 기본적으로 HTML 파서는 카멜 대소문자(예: eBay)의 속성을 소문자로 변환합니다(예: ebay). 이 설정을 해제하면 낙타 케이스 특성을 유지할 수 있습니다. 이 기능은 Angular 2와 같은 프런트 엔드 프레임워크를 사용할 때 유용합니다.

**일 커머스 JDBC 접속** 풀 컨텐츠에 대한 소스로 사용되는 외부 데이터베이스에 대한 액세스를 구성합니다.

이는 출하 시 구성이므로 여러 인스턴스를 구성할 수 있습니다.

**Adobe CQ Media DPS 세션 서비스** 발행물에서 사용할 DPS 세션을 관리합니다.

특히 `dps.session.service.url.name`다음을 정의할 수 있습니다.기본값은 https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions으로 [설정되어 있습니다.](https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions)

**AEM과** CDN 간의 CDN 리작성기 통신은 자산/바이너리가 안전하게 최종 사용자에게 전달되도록 보장되어야 합니다. 여기에는 두 가지 작업이 포함됩니다.

* CDN을 통해 AEM 파섹
* 리소스가 CDN에 캐시되면 CDN에서 안전하게 캐싱된 리소스에 액세스하면 AEM으로 요청이 전송되지 않고 해당 리소스에 액세스할 수 있는 모든 사용자는 CDN에서 제공해야 합니다.

AEM 파섹 또한 JWS 서명을 포함하여 CDN에 전달할 링크를 다시 작성하여 자산에 안전하게 액세스할 수 있도록 합니다. 이 기능은 작성자 인스턴스에 사용됩니다.

전체 흐름은 다음과 같습니다.

1. 사용자가 AEM으로 인증하고 자산이 있는 페이지를 요청합니다.
1. 요청된 페이지에 `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. 리기록기는 JWS 서명을 포함하는 CDN URL로 링크를 변환합니다.
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. 사용자의 브라우저가 자산 요청을 CDN 서버로 전달합니다.
1. CDN은 `cdn_sign` 매개 변수와 함께 요청을 AEM에 전달하도록 구성해야 합니다.
1. 인증 핸들러는 매개 변수의 유효성을 검사한 다음 사용자에게 전달된 자산을 CDN에 반환합니다. `cdn_sign`

사용자의 브라우저, CDN 및 AEM 간의 흐름은 다음과 같이 시각화할 수 있습니다.

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>이 기능은 현재 AEM 작성자 인스턴스에만 활성화됩니다.

**CDNConfigServiceImpl** CDN 구성 제공

com.adobe.cq.cdn.rewriter.impl. **CDNConfigServiceImpl 구성에 CDN 배포 도메인 이름을** 제공하여 CDN 재작성 기능을 활성화할 수 있습니다.

또한 서비스에는 CDN 재작성 활성화/비활성화, CDN 재작성을 수행하는 경로 접두사, TTL 값 및 프로토콜(HTTP 또는 HTTPS)과 같은 다른 구성 옵션이 포함되어 있습니다.

**CDNRewriter** 내부 이미지 URL을 CDN URL 파섹

com.adobe.cq.cd **n** .rewriter.impl.CDNRewriter의 태그 속성 값을 정의하여 선택적 이미지 링크만 다시 작성할 수 있습니다.
