---
title: OSGi 구성 설정
seo-title: OSGi 구성 설정
description: 이 문서에서는 프로젝트 구현과 관련된 OSGi 구성 설정(번들에 따라 나열됨)에 대해 자세히 설명합니다. 그 명단은 지침으로 사용되고 철저하지 않다.
seo-description: 이 문서에서는 프로젝트 구현과 관련된 OSGi 구성 설정(번들에 따라 나열됨)에 대해 자세히 설명합니다. 그 명단은 지침으로 사용되고 철저하지 않다.
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
translation-type: tm+mt
source-git-commit: 474fc122f557f32d34fddd9d35a113431f6ce491
workflow-type: tm+mt
source-wordcount: '3805'
ht-degree: 0%

---


# OSGi 구성 설정{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) 는 AEM의 기술 스택에서 기본적인 요소입니다. AEM 및 해당 구성의 복합 번들을 제어하는 데 사용됩니다.

OSGi는 &quot;*애플리케이션이 작고 재사용 가능한 공동 작업 구성 요소로 구성되도록 하는 표준화된 프리미티브 방식을 제공합니다. 이러한 구성 요소는 애플리케이션으로 구성하고 배포할*&#x200B;수 있습니다.&quot;

따라서 번들을 중지하거나 설치하고 개별적으로 시작할 수 있으므로 번들을 손쉽게 관리할 수 있습니다. 상호 종속성은 자동으로 처리됩니다. 각 OSGi 구성 요소( [OSGi 사양](https://www.osgi.org/Specifications/HomePage)참조)는 다양한 번들 중 하나에 포함됩니다. When working with AEM there are several methods of managing the configuration settings for such bundles; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

다음 OSGi 구성 설정(번들에 따라 나열됨)은 프로젝트 구현과 관련이 있습니다. 나열된 모든 설정을 조정할 필요는 없습니다. AEM의 작동 방식을 이해하는 데 도움이 되는 몇 가지 설정이 언급되었습니다.

>[!CAUTION]
>
>그 리스트는 지침으로 행동하기 위한 것이며 철저한 것은 아니다. 일부 번들이 나열되거나 일부 번들에 대한 모든 매개 변수가 나열되지 않습니다.
>
>필요한 구성은 프로젝트마다 다릅니다.
>
>사용된 값과 매개 변수에 대한 자세한 내용은 웹 콘솔을 참조하십시오.

>[!NOTE]
>
>AEM 도구 [의](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html)일부인 OSGi 구성 비교 도구를 사용하여 기본 OSGi 구성을 나열할 수 있습니다.

>[!NOTE]
>
>AEM 내의 특정 기능 영역에 추가 번들이 필요할 수 있습니다. 이러한 경우 구성 세부 사항은 해당 기능과 관련된 페이지에서 확인할 수 있습니다.

**AEM 복제 이벤트 리스너** 구성:

* 복제 이벤트가 **리스너에**&#x200B;배포되는 실행 모드. 예를 들어 작성자로 정의된 경우 복제를 &quot;시작&quot;하는 시스템입니다.

* 프로젝트 코드가 게시 환경에서 복제 이벤트(역 복제)를 처리하는 경우 실행 모드 **게시** 기능을 추가해야 합니다. 예를 들어, 디스패처가 게시 환경에서 플러시되는 데 사용되거나 다른 게시 인스턴스에 대한 표준 복제가 발생하는 경우

**AEM Repository change listener** Configure:

* 경로 ****, 배포할 저장소 이벤트를 수신하기 위한 위치입니다.

**CRX Sling Client Repository** 기본 컨텐츠 저장소에 대한 액세스를 구성합니다.

* 인스턴스 **의 보안을** 보장하려면 설치 후 관리자 암호를 [변경해야](/help/sites-administering/security-checklist.md) 합니다.
* 다른 변경 사항은 필요하지 않으며 저장소 액세스에 영향을 줄 수 있으므로 주의해야 합니다.

**Wiki 메일 서비스** Wiki가 보낸 이메일에 대한 이메일 설정을 구성합니다.

**Apache Felix OSGi 관리 콘솔** 구성:

* **Plugins**, the main navigation items (console plugins) to be available in the **Apache Felix Web Management Console** as top level menu items. 공간 및 리소스가 필요하므로 필요하지 않은 항목을 비활성화합니다.

>[!CAUTION]
>
>다음을 구성해야 합니다.
>
>**사용자 이름** 및 **암호**, Apache Felix 웹 관리 콘솔 자체에 액세스하기 위한 자격 증명입니다.
>인스턴스의 [보안을](/help/sites-administering/security-checklist.md) 보장하기 위해서는 초기 설치 후 암호를 변경해야 합니다.

>[!NOTE]
>
>Felix Console을 사용하여 구성한 후 저장소를 사용할 수 있습니다.

**Apache Sling 사용자 정의 가능한 요청 데이터 로거** 구성:

* **로거 이름** 및 **로그 형식** - 요청 및 액세스 로깅의 위치와 형식을 구성합니다(기본값: `request.log`). 이 로그 파일은 웹 체인과 관련된 성능 또는 디버깅 기능을 분석할 때 반드시 필요합니다.
Apache Sling [Request Logger와 함께 사용됩니다](#apacheslingrequestlogger).

자세한 내용은 [AEM 로깅](/help/sites-deploying/configure-logging.md) 및 [슬링 로깅을 참조하십시오](https://sling.apache.org/site/logging.html).

**Apache Sling 이벤트 스레드 풀** 구성:

* **최소 풀 크기** 및 **최대 풀 크기**, 이벤트 스레드를 보유하는 데 사용되는 풀의 크기입니다.

* **큐 크기**, 풀이 모두 소진된 경우 스레드 큐의 최대 크기입니다.
큐가 제한 `-1` 으로 설정되면 권장 값이 사용됩니다. 한도를 설정하면 초과될 때 손실이 발생할 수 있습니다.

* 이러한 설정을 변경하면 이벤트 수가 많은 시나리오의 성능에 도움이 될 수 있습니다. 예를 들어, AEM DAM 또는 Workflow 사용량이 많은 경우입니다.
* 시나리오와 관련된 값은 테스트를 사용하여 설정해야 합니다.
* 이러한 설정은 인스턴스의 성능에 영향을 줄 수 있으므로 이유나 고려 없이 변경하지 마십시오.

**Apache Sling GET Servlet** 렌더링의 일부 측면을 구성합니다.

* **자동 색인** 을 사용하여 검색할 디렉토리 렌더링을 활성화/비활성화할 수 있습니다.
* **HMTL** , **일반 텍스트**, **JSON**&#x200B;또는XML과 같은 기본 변환 **** ****을 활성화(또는 비활성화)합니다.
JSON을 비활성화해서는 안 됩니다.

>[!NOTE]
>
>이 설정은 프로덕션 준비 모드에서 AEM을 실행하는 경우 프로덕션 인스턴스에 대해 [자동으로 구성됩니다](/help/sites-administering/production-ready.md).

**Apache Sling Java Script Handler** .java 파일을 스크립트(서블릿)로 컴파일하기 위한 설정을 구성합니다.

특정 설정은 성능에 영향을 줄 수 있으며, 가능한 경우 특히 프로덕션 인스턴스에 대해 이 설정을 사용하지 않도록 설정해야 합니다.

* 소스&#x200B;**VM** 및 **Target** VM은 런타임 JVM으로 사용되는 JDK 버전을 정의합니다.

* 프로덕션 인스턴스의 경우:

   * 디버그 **정보 생성 비활성화**

**Apache Sling JCR 설치 관리자** 이러한 매개 변수에는 구성이 필요하지 않을 수 있지만 개발 또는 디버깅할 때 유용할 수 있습니다. 예를 들어 설치 폴더는 패키지를 체크 인/체크 아웃하거나 만드는 데 유용합니다.

* **설치 폴더 이름 등록** 및 **설치 폴더의** 최대 계층깊이 - 설치할 리소스를 검색할 위치와 깊이를 지정합니다. 와일드카드를 사용할 때(와 같이)*/install) 모든 적절한 일치 항목을 검색합니다(예: `/libs/sling/install` 및 `/libs/cq/core/install`).

* **검색 경로**, 설치 대상이 될 리소스를 검색하는 경로 목록과 해당 경로의 가중치를 나타내는 숫자가 함께 있습니다.

**Apache Sling 작업 이벤트 처리기** 작업 예약을 관리하는 매개 변수를 구성합니다.

* **재시도 간격**, **최대**&#x200B;재시도 **,**&#x200B;최대 병렬 작업 **,**&#x200B;대기 시간확인 등이 있습니다.

* 이러한 설정을 변경하면 작업 수가 많은 시나리오의 성능이 향상될 수 있습니다. 예를 들어, AEM DAM 및 워크플로우의 사용량이 많은 경우입니다.
* 시나리오와 관련된 값은 테스트를 사용하여 설정해야 합니다.
* 이유 없이 이 설정을 변경하지 말고, 고려 후에 변경하십시오.

**Apache Sling JSP Script Handler** JSP 스크립트 핸들러에 대한 성능 관련 설정을 구성합니다. 성능을 향상시키려면 가능한 한 많이 비활성화해야 합니다.

프로덕션 인스턴스:

* 디버그 **정보 생성 비활성화**
* 생성된 **Java 유지 비활성화**
* 매핑된 **콘텐츠 비활성화**
* 소스 조각 **표시 비활성화**

>[!NOTE]
>
>이 설정은 프로덕션 준비 모드에서 AEM을 실행하는 경우 프로덕션 인스턴스에 대해 [자동으로 구성됩니다](/help/sites-administering/production-ready.md).

**Apache Sling 로깅 구성** 구성:

* **로그 수준** 및 **로그 파일**- 중앙 로깅 구성(error.log)의 위치 및 로그 수준을 정의합니다. 수준을 `DEBUG`하나, `INFO``WARN`, `ERROR` 및 `FATAL`로 설정할 수 있습니다.

* **로그 파일의 크기** 및 **버전 순환을 정의하는 로그 파일** 및 로그 파일 임계값 수입니다.

* **메시지 패턴** 로그 메시지의 형식을 정의합니다.

자세한 내용은 [AEM 로깅](/help/sites-deploying/configure-logging.md#global-logging) 및 [슬링 로깅을 참조하십시오](https://sling.apache.org/site/logging.html).

**Apache Sling Logging Logger 구성(출하 시 구성)** :

* **로그 수준**, **로그 파일** 및 **메시지 형식** 을 참조하십시오.

* **로거** - 범주 정의 예를 들어 com.day.cq에 대한 로그만 있을 수 있습니다.

* Factory **구성을**&#x200B;사용하면 필요한 다양한 로그 수준 및 범주에 맞는 추가 구성을 추가할 수 있습니다.
* 이러한 구성은 개발 중에 유용합니다. 예를 들어 특정 서비스에 대한 TRACE 메시지를 특정 로그 파일에 기록할 수 있습니다.
* 이러한 구성은 제작 환경에서 유용합니다. 예를 들어 보다 쉽게 모니터링하기 위해 개별 로그 파일에 특정 서비스에 대한 메시지를 기록하도록 합니다.

자세한 내용은 [AEM 로깅](/help/sites-deploying/configure-logging.md) 및 [슬링 로깅을 참조하십시오](https://sling.apache.org/site/logging.html).

**Apache Sling Logging Writer 구성(출하 시 구성)** 구성:

* **로그 파일** : 로그 파일의 존재를 정의합니다.
* **버전 순환을 정의하는 로그** 파일의 수입니다.

* Apache Sling Logging **Logger 구성** 구성

* 이러한 구성은 개발 중에 유용합니다. 예를 들어 특정 서비스에 대한 TRACE 메시지를 특정 로그 파일에 기록할 수 있습니다.
* 이러한 구성은 제작 환경에서 유용합니다. 예를 들어 보다 쉽게 모니터링하기 위해 개별 로그 파일에 특정 서비스에 대한 메시지를 기록하도록 합니다.

자세한 내용은 [AEM 로깅](/help/sites-deploying/configure-logging.md) 및 [슬링 로깅을 참조하십시오](https://sling.apache.org/site/logging.html).

**Apache Sling Main Servlet** 구성:

* **무한 재귀** 및 **과도한 스크립트 호출으로부터 시스템을 보호하기** 위한 요청당 호출 수 및 재귀 깊이.

**Apache Sling MIME 유형 서비스** 구성:

* **MIME 형식을** 참조하십시오. 이렇게 하면 파일 형식 및 응용 프로그램 연결에 대한 올바른 내용 유형 헤더를 설정하는 파일 `GET` 요청이 가능합니다.

**Apache Sling Referrer 필터** CRX WebDAV 및 Apache Sling에서 CSRF(교차 사이트 요청 위조) 관련 알려진 보안 문제를 해결하려면 레퍼러 필터를 구성해야 합니다.

레퍼러 필터 서비스는 다음을 구성할 수 있는 OSGi 서비스입니다.

* http 메서드를 필터링해야 합니다.
* 빈 레퍼러 헤더가 허용되는지 여부
* 서버 호스트 외에 허용되는 서버 목록입니다.

자세한 내용은 [보안 검사 목록 - 사이트 간 요청 위조](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 관련 문제를 참조하십시오.

>[!NOTE]
>
>Apache Sling 레퍼러 필터는 빠른 수정 패키지 설치에 따라 달라집니다.

**Apache Sling 요청 로거** 구성:

* 다양한 매개 변수를 사용하여 요청이 기록된 방식을 정의할 수 있습니다.
* **요청 로그를**&#x200B;활성화하거나 비활성화합니다.

* **액세스 로그를**&#x200B;활성화하거나 비활성화합니다.

Apache Sling [Customizable Request Data Logger와 함께 사용됩니다](#apacheslingcustomizablerequestdatalogger).

자세한 내용은 [AEM 로깅](/help/sites-deploying/configure-logging.md) 및 [슬링 로깅을 참조하십시오](https://sling.apache.org/site/logging.html).

**Apache Sling Resource Resolver Factory** Sling 리소스 해상도의 중앙 측면 구성:

* **리소스 검색 경로**, 프로젝트별 경로 추가(제거 `/libs` 또는 `/apps`제거 안 함)

* **별칭** URL 매핑을 정의하는 가상 URL.

* **별칭을 정의하는 URL** 매핑; 예: to `/content` . `/`.

* **매핑 위치**. 맵 편집기 구성이 외부에서 `/etc/map`실행됩니다.

* 로컬 설치(예: 사용)를 사용하여 활성 리소스 확인자를 `https://localhost:4502/system/console/jcrresolver`확인합니다.

자세한 내용은 다음을 참조하십시오. [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>특히 이러한 옵션은 저장소에 구성해야 합니다.
>
>그렇지 않으면 Felix 콘솔을 사용하여 **URL** 매핑에 대한 변경 사항이 다음 시작 시 AEM에 의해 덮어쓰여질 수 있습니다.

**Apache Sling Servlet/Script Resolver 및 Error Handler** Sling Servlet 및 Script Resolver에는 다음과 같은 여러 작업이 있습니다.

1. 요청을 처리하기 위해 호출할 서블릿 또는 스크립트 `ServletResolver` 를 선택하는 데 사용됩니다.

1. 마치 `SlingScriptResolver`그런 것처럼

1. 이 엔진은 같은 알고리즘을 사용하여 `ErrorHandler` 인터페이스를 구현하여 오류 처리 서블릿 및 스크립트를 선택하고 요청 처리 서블릿 및 스크립트를 해결하는 데 사용되는 스크립트를 선택함으로써 오류 처리를 관리합니다.

다음을 포함하여 다양한 매개 변수를 설정할 수 있습니다.

* **실행 경로** : 실행 스크립트를 검색할 경로를 나열합니다. 특정 경로를 구성하여 실행할 수 있는 스크립트를 제한할 수 있습니다. 경로가 구성되지 않은 경우 기본값이 사용됩니다( `/` = 루트). 이렇게 하면 모든 스크립트를 실행할 수 있습니다.
구성된 경로 값이 슬래시로 끝나는 경우 전체 하위 트리가 검색됩니다. 이렇게 후행 슬래시가 없으면 스크립트가 정확히 일치하는 경우에만 실행됩니다.

* **스크립트 사용자** - 이 선택적 속성은 스크립트를 읽는 데 사용되는 저장소 사용자 계정을 지정할 수 있습니다. 계정을 지정하지 않으면 기본적으로 `admin` 사용자가 사용됩니다.

* **기본 익스텐션** 기본 동작을 사용할 익스텐션 목록입니다. 즉, 리소스 유형의 마지막 경로 세그먼트를 스크립트 이름으로 사용할 수 있습니다.

**Day Commons GFX Font Helper** 그래픽을 렌더링할 때 DrawText를 사용하여 텍스트를 포함할 수 있습니다. 이를 위해 고유한 글꼴을 설치할 수도 있습니다.

* 프로젝트별 **글꼴을 검색할 글꼴** 경로를 정의합니다.
예, `/apps/myapp/fonts`.

**HTTP가 만들어질 때 사용되는 Apache HTTP 클라이언트를 사용하는 모든 코드에 대한 Apache HTTP Components Proxy Configuration** Proxy 구성; 예를 들어 복제 시.

새 구성을 만들 때는 공장 구성을 변경하지 말고 여기에서 사용할 수 있는 구성 관리자를 사용하여 이 구성 요소에 대한 새 공장 구성을 만드십시오. **https://localhost:4502/system/console/configMgr/**. 프록시 구성은 **org.apache.http.proxyconfigurator에서 사용할 수 있습니다.**

>[!NOTE]
>
>AEM 6.0 및 이전 릴리스 프록시는 Day Commons HTTP 클라이언트에 구성되었습니다. AEM 6.1 이상 버전에서 프록시 구성이 &#39;Day Commons HTTP Client&#39; 구성 대신 &quot;Apache HTTP 구성 요소 프록시 구성&quot;으로 이동되었습니다.

**일 CQ 스팸** 방지 사용된 스팸 방지 서비스(Akismet)를 구성합니다. 이를 위해서는 다음을 등록해야 합니다.

* **공급자**
* **API 키**
* **등록된 URL**

**Adobe Granite HTML Library Manager** 클라이언트 라이브러리(css 또는 js)의 처리를 제어하도록 이 구성; 예를 들어 기본 구조가 표시되는 방식을 포함합니다.

* 프로덕션 인스턴스의 경우:

   * 축소 **활성화** (CRLF 및 공백 문자를 제거하려면).
   * gzip **을** 활성화합니다(하나의 요청으로 파일을 압축하고 액세스할 수 있도록 허용).
   * 디버그 **비활성화**
   * 타이밍 **비활성화**

* JS 개발(특히 방화벽/디버깅 시):

   * 미니화 **비활성화**
   * 디버그 **를** 활성화하여 디버깅할 파일을 구분하고 firebug와 함께 사용합니다.
   * 타이밍 **을** 활성화할 수 있습니다.
   * 디버그 **콘솔을 활성화하여** JS 콘솔 로그 메시지를 볼 수 있습니다.

>[!CAUTION]
>
>Minify **** 또는 Gzip에 대한 **** 설정을 변경할 때 `/var/clientlibs`의 내용도 삭제해야합니다. 이 버전은 Clientlibs의 캐시된 버전이며 다음에 요청할 때 다시 빌드됩니다.

>[!NOTE]
>
>이 설정은 프로덕션 준비 모드에서 AEM을 실행하는 경우 프로덕션 인스턴스에 대해 [자동으로 구성됩니다](/help/sites-administering/production-ready.md).

**일 CQ HTTP 헤더 인증 처리기** HTTP 요청의 기본 인증 방법에 대한 시스템 전체 설정입니다.

닫힌 사용자 그룹을 사용할 때 [](/help/sites-administering/cug.md) 구성(다른 그룹 포함)할 수 있습니다.

* **HTTP 영역**
* 기본 **로그인 페이지**

**CQ Link Checker Service** Check 및 필요한 경우 다음을 구성합니다.

* **스케줄러 기간** : 외부 링크를 자동으로 확인하는 간격을 정의합니다.

* 실패한 **외부 링크가 나쁜 것으로 간주되는 기간 동안 잘못된 링크 허용한도** 간격을 확인합니다.
* **링크 확인 대체 패턴**&#x200B;지정을 참조하십시오.

**일 CQ 링크 검사기 작업** 단일 링크 검사기 작업(외부 링크를 확인하는 작업)에 대한 설정을 구성합니다.

* 좋은 링크 테스트 간격 및 **잘못된 링크 테스트** 간격에 정의된 **간격을 확인합니다.**

* 링크를 확인할 때 외부 액세스에 필요한 인터넷 액세스용 프록시 및 NTLM과 관련된 다양한 매개 변수입니다.

**일 CQ 메일 서비스** 메일 서버의 호스트 이름 및 액세스 세부 정보를 구성합니다. 메일 서비스 구성 섹션을 참조하십시오.

**Day CQ MCM Newsletter** Newsletter에 사용되는 다양한 설정을 구성합니다.

**일 CQ 루트 매핑** 구성:

* **Target** &quot;&quot;에 대한 요청이 리디렉션되는 위치를 `/`정의하는 경로입니다.

AEM에는 두 개의 UI가 있습니다.

* 터치 지원 UI가 표준 UI임
* 그리고 마지막으로 가져온 클래식 UI는 여전히 완벽하게 작동합니다.

AEM Root Mapping을 사용하여 인스턴스에 대한 기본값으로 사용할 UI를 구성할 수 있습니다.

* 터치 지원 UI를 기본 UI로 만들려면 **Target 경로가** 다음을 가리켜야 합니다.

   ```
      /projects.html
   ```

* 기본 UI로 클래식 UI를 만들려면 **Target 경로가** 다음을 가리켜야 합니다.

   ```
      /welcome.html
   ```

>[!NOTE]
>
>표준 설치 시 터치에 적합한 UI가 기본 UI입니다.

**Adobe Granite SSO Authentication Handler** SSO(Single Sign On) 세부 사항 구성; 이러한 문제는 LDAP와 함께 기업 작성자 설정에서 자주 필요합니다.

다양한 구성 속성을 사용할 수 있습니다.

* **이 인증**&#x200B;처리기가 활성 상태인 경로. 이 매개 변수를 비워 두면 인증 처리기가 비활성화됩니다. 예를 들어 경로 / 는 전체 저장소에 대해 인증 핸들러를 사용합니다.

* **서비스 등급** OSGi 프레임워크 서비스 등급 값은 이 서비스를 호출하는 데 사용되는 순서를 나타내는 데 사용됩니다. 이것은 `int``0`

* `int` 값이 높을수록 우선 순위가 높습니다.
Default value is `0`.

* **헤더 이름**&#x200B;사용자 ID를 포함할 수 있는 헤더의 이름입니다.

* **쿠키 이름**&#x200B;사용자 ID를 포함할 수 있는 쿠키의 이름입니다.

* **매개 변수 이름**&#x200B;사용자 ID를 제공할 수 있는 요청 매개 변수의 이름입니다.`admin`

* **사용자 맵**&#x200B;선택한 사용자의 경우 HTTP 요청에서 추출한 사용자 이름을 자격 증명 개체에서 다른 이름으로 바꿀 수 있습니다. 매핑이 여기에 정의되어 있습니다. 사용자 이름이 

   * `admin` 맵의 양쪽에 나타나는 경우 매핑이 무시됩니다. &quot;=&quot;라는 문자는 &quot;\&quot;로 이스케이프해야 합니다.
   * **형식**&#x200B;사용자 ID가 제공되는 형식을 나타냅니다. 사용:

`Basic` 사용자 ID가 HTTP Basic 인증 형식으로 인코딩된 경우**

* `AsIs` 사용자 ID가 일반 텍스트로 제공되거나 정규 표현식이 적용된 값을 있는 그대로 또는 정규 표현식으로 사용해야 하는 경우

**일 CQ WCM 디버그 필터** 페이지에 액세스할 때 ?debug=layout과 같은 접미사를 사용할 수 있으므로 개발하는 경우 유용합니다. 예를 들어 https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout에서는 개발자에게 관심이 있는 레이아웃 정보를 제공합니다.

* 프로덕션 인스턴스에서 이 설정을 비활성화하여 성능과 보안을 보장합니다.
* **CQ WCM 필터** 구성 일:`analytics``?wcmmode=disabled`

* **WCM 모드 **를 사용하여 기본 모드를 정의합니다.`disabled`

>작성 인스턴스에서 이러한 경우는 `edit``disable,preview` 또는 `analytics`해당됩니다.
사이드 킥에서 다른 모드에 액세스하거나 접미어를 사용하여 프로덕션 환경을 에뮬레이션할 `?wcmmode=disabled` 수 있습니다.
>
>게시 인스턴스에서 다른 모드에 액세스할 수 없도록 `disabled` 설정해야 합니다.](/help/sites-administering/production-ready.md)

[!NOTE]**

* 이 설정은 프로덕션 준비 모드에서 AEM을 실행하는 경우 프로덕션 인스턴스에 대해 [자동으로 구성됩니다](/help/sites-administering/production-ready.md).

**CQ WCM 링크 검사기 구성자 구성일** :

* **컨텐츠 기반** linkchecker 구성의 위치 목록을 지정하는 재작성 구성 목록입니다. 구성은 실행 모드를 기반으로 할 수 있습니다. linkchecker 설정은 다를 수 있으므로 작성 환경과 게시 환경을 구분하는 것이 중요합니다.`jcr:Event`

**CQ WCM 페이지 프로세서 구성일** :

* **경로**, 시스템이 페이지를 트리거하기 전에 페이지 수정을 수신하는 위치 `jcr:Event`목록입니다.

>**Adobe 페이지 노출 횟수 추적기** 작성자 인스턴스의 경우:
>
>**sling.auth.requirements**: 이 속성의 값을 `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>이 구성은 추적 서비스에 대한 익명 요청을 허용합니다.[](/help/sites-deploying/configuring.md#enabling-page-impressions)

[!NOTE]**

* 자세한 내용은 [페이지 노출](/help/sites-deploying/configuring.md#enabling-page-impressions) 횟수를 참조하십시오.`https://localhost:4502/libs/wcm/stats/tracker`

* **일 CQ WCM 페이지 통계** 게시 인스턴스의 경우:`true``false``false`

>**페이지 통계를 추적하는 데 사용되는 URL을 구성하는 데이터를** 보내는 URL(추적기 요청이 디스패처를 통과하는 경우 중요); 예를 들어 기본값은 입니다 `https://localhost:4502/libs/wcm/stats/tracker`.
>
>**추적 스크립트** 는 페이지에 추적 스크립트 포함을 활성화( `true`) 또는 비활성화( `false`)할 수 있도록 활성화되었습니다. The default value is `false`.

[!NOTE]**

* 자세한 내용은 [페이지 노출](/help/sites-deploying/configuring.md#enabling-page-impressions) 횟수를 참조하십시오.
* **CQ WCM Version Manager** 관리 요일:

* **표준 설치에서**&#x200B;활성화한 활성화 버전 만들기
* **제거 사용**

* **경로**&#x200B;제거, 검색 작업이 검색하는 경로

* **암시적 버전 관리 경로**: 암시적 버전 관리가 활성화된 경로입니다.

**최대 버전 연령**, 버전의 최대 연령(일)

**최대 버전 수**, 유지할 최대 버전 수

자세한 내용은 [버전 삭제를](/help/sites-deploying/version-purging.md) 참조하십시오.

* **일 CQ 워크플로우 이메일 알림 서비스** 워크플로우에서 보낸 알림에 대한 이메일 설정을 구성합니다.
* **Day CQSE HTTP Service** Control the CQ Servlet Engine:

* ****HTTP의 경우 NIO, **HTTP의 경우 NIO를 사용할지 여부를 나타냅니다. 기본값은 true입니다. HTTP가 활성화된 경우에만 사용됩니다.**
* ****연결 시간 초과, **연결 시간 초과(밀리초) 이 속성은 HTTP 및 HTTPS 연결 모두에 적용됩니다. 기본값은 60초입니다.**
* **HTTPS 활성화,** HTTPS가 활성화되었는지 여부 기본값은 false입니다.
* **세션 시간 초과**, 분 단위로 지정된 HTTP 세션의 기본 라이프타임입니다. 제한 시간이 0 이하인 경우 세션이 시간 초과되지 않습니다. 기본값은 10분입니다.
* **디버그 로깅**, DEBUG 수준 메시지를 작성할지 여부. 기본값은 false입니다.

**요청 버퍼 크기**, 요청에 대한 버퍼 크기(바이트)입니다. 기본값은 8KB입니다.

* **최대 스레드**&#x200B;수, 요청을 처리하는 데 사용할 최대 스레드 수입니다. 기본값은 200입니다.
* **다음 속성은 HTTPS가 활성화된 경우에만 적용됩니다.**
* **HTTPS 포트**, HTTPS 요청을 수신하기 위한 포트입니다. 기본값은 433입니다.
* **HTTPS용** NIO, HTTP에 NIO를 사용할지 여부를 나타냅니다. 기본값은 HTTP용 NIO 속성 값입니다.
* **키 저장소**, HTTPS에 사용할 키 저장소의 절대 경로입니다. HTTPS가 활성화된 경우 필요합니다.
* **Keystore 암호**, Keystore에 액세스하기 위한 암호.
* **키 별칭**, 키 저장소에 있는 비밀 키의 별칭입니다.

**키 암호**, Keystore에서 비밀 키를 잠금 해제하는 암호.

**클라이언트 인증서**, 클라이언트가 유효한 인증서를 제공해야 합니다. 기본값은 none입니다.

SSL 관련 [옵션에 대한 자세한 내용 및 CQSE용 HTTPS를 사용하는 방법에 대한 전체 설명은 HTTP Over SSL](/help/sites-administering/ssl-by-default.md) 활성화를 참조하십시오.

* **CQ Rewriter HTML Parser Factory**
* **CQ 리저터에 대한 HTML 파서를 제어합니다.**

**처리할 추가** 태그 - 파서에서 처리할 HTML 태그를 추가하거나 제거할 수 있습니다. 기본적으로 다음 태그가 처리됩니다. A,IMG,AREA,FORM,BASE,LINK,SCRIPT,BODY,HEAD.

**카멜 대소문자** 유지 - 기본적으로 HTML 파서는 카멜 대소문자(예: eBay)의 속성을 소문자(예: ebay)로 변환합니다. 이 설정을 해제하면 낙타 케이스 특성을 유지할 수 있습니다. 이는 각도 2와 같은 프런트 엔드 프레임워크를 사용할 때 유용합니다.

**일 공용 JDBC 연결 풀** 컨텐츠 소스로 사용되는 외부 데이터베이스에 대한 액세스를 구성합니다.

이는 팩토리 구성이므로 여러 인스턴스를 구성할 수 있습니다.`dps.session.service.url.name`[-ERR:REF-NOT-FOUND-



* 
* **AEM과 CDN 간 CDN 리라이터** 통신은 안전하게 자산/바이너리가 최종 사용자에게 전달되도록 보장되어야 합니다. 여기에는 두 가지 작업이 포함됩니다.

CDN을 통해 AEM에서 리소스에 액세스하는 최초(또는 캐시에서 만료된 후).

CDN에서 리소스가 캐시되면 AEM으로 요청이 이동하고 해당 리소스에 액세스할 수 있는 모든 사용자는 CDN에서 안전하게 캐시됩니다.

1. AEM에서는 내부 자산 URL을 외부 CDN URL로 다시 작성하기 위한 리필터를 제공합니다. JWS 서명 및 만료 시간을 포함하여 CDN에 전달할 링크를 다시 작성하여 자산에 안전하게 액세스할 수 있도록 합니다. 이 기능은 작성자 인스턴스에 사용됩니다.
1. 전체 흐름은 다음과 같습니다.`/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. 사용자가 AEM으로 인증하고 자산이 있는 페이지를 요청합니다.   요청한 페이지에 `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`

1. 리라이터는 JWS 서명을 포함하는 CDN URL로 링크를 변환합니다.

1. `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`
1. 그런 다음 사용자의 브라우저가 자산 요청을 CDN 서버로 전달합니다.`cdn_sign`

CDN은 매개 변수와 함께 요청을 AEM에 전달하도록 `cdn_sign` 구성해야 합니다.

인증 핸들러는 매개 변수의 유효성을 `cdn_sign` 확인하고 자산을 사용자에게 전달된 CDN에 반환합니다](assets/chlimage_1-8.png)

>[!NOTE]사용자의 브라우저, CDN 및 AEM 간의 흐름은 다음과 같이 시각화할 수 있습니다.
>
>![chlimage_1-8](assets/chlimage_1-8.png)

[!NOTE]**

이 기능은 현재 AEM 작성자 인스턴스에만 활성화됩니다.****

**CDNConfigServiceImpl** CDN 구성 제공

com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl 구성에 **CDN 배포 도메인 이름을** 제공하여 CDN 재작성 기능을 활성화할 수 있습니다.

또한 서비스는 CDN 재작성 활성화/비활성화, CDN 재작성을 수행하는 경로 접두어, TTL 값 및 프로토콜(HTTP 또는 HTTPS)과 같은 다른 구성 옵션도 포함합니다.****
