---
title: AEM 코어 개념
seo-title: 기본 사항
description: AEM이 구조화된 방법과 JCR, Sling, OSGi, 디스패처, 워크플로우 및 MSM에 대한 이해를 포함하여 AEM을 기반으로 개발하는 방법에 대한 핵심 개념에 대한 개요
seo-description: AEM이 구조화된 방법과 JCR, Sling, OSGi, 디스패처, 워크플로우 및 MSM에 대한 이해를 포함하여 AEM을 기반으로 개발하는 방법에 대한 핵심 개념에 대한 개요
uuid: e49f29db-a5d6-48a0-af32-f8785156746e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6e913190-be92-4862-a8b9-517f8bde0044
translation-type: tm+mt
source-git-commit: 2d0e0325d1fce2587e4766bf2f60fc5d4accf45b

---


# AEM 코어 개념 {#aem-core-concepts}

>[!NOTE]
>
>AEM의 핵심 개념을 살펴보기 전에 AEM [개발 시작에서 WKND](/help/sites-developing/getting-started.md) 자습서를 완료하여 AEM 개발 프로세스에 대한 개요 및 핵심 개념을 소개할 것을 권장합니다.

## AEM에서 개발하기 위한 사전 요구 사항 {#prerequisites-for-developing-on-aem}

AEM을 기반으로 개발하는 데 다음 기술이 필요합니다.

* 다음을 비롯한 웹 애플리케이션 기술에 대한 기본 지식

   * request -response(XMLHttpRequest / XMLHttpResponse) 주기
   * HTML
   * CSS
   * JavaScript

* Content Explorer를 비롯한 Experience Server(CRX)에 대한 작업 지식
* 클래식 UI에서 개발하기 위해서는 간단한 JSP 예제를 이해하고 수정하는 기능을 비롯하여 JSP(JavaServer Pages)에 대한 기본 지식도 필요합니다.

또한 지침 및 우수 사례를 읽고 따르는 [것이 좋습니다](/help/sites-developing/dev-guidelines-bestpractices.md).

## Java 컨텐츠 저장소 {#java-content-repository}

JSR(Java Content Repository) 표준인 [JSR](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html)283은 컨텐츠 저장소 내의 세부적인 수준에서 컨텐츠를 양방향 액세스할 수 있는 벤더 독립적이고 구현 독립적 방법을 지정합니다.

사양 리드는 Adobe Research(스위스) AG에서 보유합니다.

JCR [API 2.0](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html) 패키지, javax.jcr.&amp;ast;저장소 컨텐츠의 직접 액세스 및 조작에 사용됩니다.

## Experience Server(CRX) 및 Jackrabbit {#experience-server-crx-and-jackrabbit}

Adobe Experience Server는 AEM이 기반으로 구축된 Experience Services를 제공하며, 이를 활용하여 맞춤형 애플리케이션을 구축하고 Jackrabbit를 기반으로 컨텐츠 저장소를 포함합니다.

[Apache](https://jackrabbit.apache.org/) Jackrabbit은 JCR API 2.0의 완벽한 구현을 따르는 개방형 소스입니다.

## Sling 요청 처리 {#sling-request-processing}

### Sling 소개 {#introduction-to-sling}

AEM은 컨텐츠 [중심](https://sling.apache.org/site/index.html)애플리케이션을 쉽게 개발할 수 있는 REST 원칙을 기반으로 하는 웹 애플리케이션 프레임워크인 Sling을 사용하여 구축되었습니다. Sling은 Apache Jackrabbit과 같은 JCR 저장소를 사용하거나 AEM의 경우 CRX 컨텐츠 저장소를 데이터 저장소로 사용합니다. Sling은 Apache Software Foundation에 기여했습니다. 자세한 내용은 Apache를 참조하십시오.

Sling을 사용하면 렌더링할 컨텐츠의 유형이 첫 번째 처리 고려 사항이 아닙니다. 대신 URL이 렌더링을 수행하기 위해 스크립트를 찾을 수 있는 컨텐츠 개체로 확인되는지 여부를 주로 고려해야 합니다. 따라서 웹 컨텐츠 작성자가 요구 사항에 맞게 손쉽게 맞춤화할 수 있는 페이지를 제작할 수 있습니다.

이러한 유연성의 이점은 다양한 컨텐츠 요소가 있는 애플리케이션이나 손쉽게 맞춤화할 수 있는 페이지가 필요할 때 분명히 나타날 수 있습니다. 특히 AEM 솔루션의 WCM과 같은 웹 컨텐츠 관리 시스템을 구현할 때

Sling [을 사용하여 개발하는 첫 번째 단계는 15분](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) 후에 Discover Sling을 참조하십시오.

다음 다이어그램에서는 Sling 스크립트 해상도에 대해 설명합니다.HTTP 요청에서 컨텐츠 노드, 컨텐츠 노드에서 리소스 유형에 이르기까지 리소스 유형, 스크립트 및 사용 가능한 스크립팅 변수를 가져오는 방법을 보여줍니다.

![chlimage_1-84](assets/chlimage_1-97.png)

다음 다이어그램은 저장소에서 노드를 생성, 수정, 삭제, 복사 및 이동하는 데 필요한 끝없는 옵션을 제공하는 모든 POST 요청에 대한 기본 핸들러인 SlingPostServlet을 처리할 때 사용할 수 있는 숨겨진 강력한 요청 매개 변수에 대해 설명합니다.

![chlimage_1-85](assets/chlimage_1-98.png)

### Sling은 컨텐츠 중심 {#sling-is-content-centric}

Sling은 *컨텐츠 중심적입니다*. 즉, 각(HTTP) 요청이 JCR 리소스(저장소 노드)의 형식으로 컨텐츠에 매핑되면 처리에 초점이 맞춰집니다.

* 첫 번째 대상은 컨텐츠를 보유하는 리소스(JCR 노드)입니다.
* 둘째, 표현 또는 스크립트는 요청의 특정 부분(예: 선택기 및/또는 확장)과 함께 리소스 속성에서 가져옵니다.

### RESTful Sling {#restful-sling}

컨텐츠 중심 철학으로 인해 Sling은 REST 지향 서버를 구현하므로 웹 애플리케이션 프레임워크에 새로운 개념을 제공합니다. 이점은 다음과 같습니다.

* 매우 안전하게, 단지 표면에만 있는 것이 아니라;리소스 및 표현이 서버 내부에서 올바르게 모델링됩니다.
* 하나 이상의 데이터 모델 제거

   * 이전에는 다음이 필요했습니다.URL 구조, 비즈니스 개체, DB 스키마;
   * 이제 다음으로 축소되었습니다.URL = 리소스 = JCR 구조

### URL 분해 {#url-decomposition}

Sling에서 처리는 사용자 요청의 URL에 의해 결정됩니다. 적절한 스크립트가 표시할 컨텐츠를 정의합니다. 이렇게 하려면 URL에서 정보가 추출됩니다.

다음 URL을 분석하는 경우:

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

합성 부품으로 나눌 수 있습니다.

| 프로토콜 | 호스트 | 컨텐츠 경로 | selector(s) | extension |  | 접미사 |  | param(s) |
|---|---|---|---|---|---|---|---|---|
| https:// | myhost | 도구/스파이 | .printed.a4. | html | / | a/b | ? | x=12 |

**프로토콜** HTTP

**호스트** 웹 사이트의 이름입니다.

**컨텐츠 경로** 렌더링할 컨텐츠를 지정하는 경로입니다. 확장자와 함께 사용됩니다.이 예에서는 tools/spy.html로 번역됩니다.

**selector(s)** 컨텐츠를 렌더링하는 대체 방법에 사용됩니다.이 예에서는 A4 형식의 프린터에 적합한 버전입니다.

**extension** Content format;렌더링에 사용할 스크립트를 지정합니다.

**접미사** 추가 정보를 지정하는 데 사용할 수 있습니다.

**param** 동적 컨텐츠에 필요한 모든 매개 변수입니다.

#### URL에서 콘텐트 및 스크립트 {#from-url-to-content-and-scripts}

다음 원칙 사용:

* 매핑은 요청에서 추출한 컨텐츠 경로를 사용하여 리소스를 찾습니다
* 적절한 리소스가 있으면 sling 리소스 유형이 추출되어 컨텐츠를 렌더링하는 데 사용할 스크립트를 찾는 데 사용됩니다

아래 그림은 사용되는 메커니즘을 보여 줍니다. 이 메커니즘은 다음 섹션에서 자세히 설명합니다.

![chlimage_1-86](assets/chlimage_1-86a.png)

Sling에서는 JCR 노드에서 속성을 설정하여 특정 엔티티를 렌더링하는 스크립트를 `sling:resourceType` 지정합니다. 이 메커니즘은 리소스가 여러 변환을 가질 수 있으므로 스크립트에서 데이터 엔티티에 액세스하는 것보다(PHP 스크립트의 SQL 문처럼) 더 자유롭습니다.

#### 요청에 리소스 매핑 {#mapping-requests-to-resources}

요청이 분류되고 필요한 정보가 추출됩니다. 저장소가 요청된 리소스(컨텐츠 노드)에 대해 검색됩니다.

* first Sling은 요청에 지정된 위치에 노드가 있는지 여부를 확인합니다.예: `../content/corporate/jobs/developer.html`
* 노드가 없으면 확장이 삭제되고 검색이 반복됩니다.예: `../content/corporate/jobs/developer`
* 노드가 없으면 Sling은 http 코드 404(찾을 수 없음)를 반환합니다.

Sling은 JCR 노드 이외의 다른 작업도 리소스가 될 수 있지만 고급 기능입니다.

### 스크립트 찾기 {#locating-the-script}

적절한 리소스(컨텐츠 노드)가 있으면 **슬링 리소스 유형이** 추출됩니다. 이 경로는 컨텐츠를 렌더링하는 데 사용할 스크립트를 찾는 경로입니다.

에 의해 지정된 경로는 다음 중 `sling:resourceType` 하나일 수 있습니다.

* 절대
* relative, to the configuration parameter

   상대적인 경로는 이식성을 높이기 위해 Adobe에서 권장합니다.

모든 Sling 스크립트는 `/apps` 또는 의 하위 폴더에 저장되며 `/libs`이 순서는 검색됩니다(구성 요소 및 기타 [요소 사용자 지정 참조](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

다른 몇 가지 사항은 다음과 같습니다.

* 메서드(GET, POST)가 필요한 경우 HTTP 사양에 따라 대문자로 지정됩니다(예: jobs.POST.esp(아래 참조).
* 다양한 스크립트 엔진이 지원됩니다.

   * `.esp, .ecma`:ECMAScript(JavaScript) 페이지(서버측 실행)
   * `.jsp`:Java Server 페이지(서버측 실행)
   * `.java`:Java Servlet Compiler(서버측 실행)
   * `.jst`:JavaScript 템플릿(클라이언트측 실행)

해당 AEM 인스턴스에서 지원하는 스크립트 엔진 목록은 Felix Management Console( `http://<host>:<port>/system/console/slingscripting`)에 나열되어 있습니다.

또한 Apache Sling은 널리 사용되는 다른 스크립팅 엔진(예: Groobi, JRuby, Freemarker)과의 통합을 지원하고 새로운 스크립팅 엔진을 통합하는 방법을 제공합니다.

위의 예를 사용하여, `sling:resourceType` 다음에 `hr/jobs` 대해

* GET/HEAD 요청 및 .html로 끝나는 URL(기본 요청 유형, 기본 형식)

   스크립트는 /apps/hr/jobs/jobs.esp입니다.sling:resourceType의 마지막 섹션은 파일 이름을 구성합니다.

* POST 요청(GET/HEAD를 제외한 모든 요청 유형, 메서드 이름은 대문자여야 함)

   POST는 스크립트 이름에 사용됩니다.

   대본이 될 `/apps/hr/jobs/jobs.POST.esp`것입니다.

* .html로 끝나지 않고 다른 형식의 URL

   예 `../content/corporate/jobs/developer.pdf`

   대본은 `/apps/hr/jobs/jobs.pdf.esp`다음과 같습니다.스크립트 이름에 접미어가 추가됩니다.

* 선택기가 있는 URL

   선택기를 사용하여 동일한 컨텐츠를 대체 형식으로 표시할 수 있습니다. 예를 들어 프린터 사용 버전, rss 피드 또는 요약입니다.

   선택기가 *인쇄될*&#x200B;수 있는 프린터 사용 버전을 살펴보는 경우as `../content/corporate/jobs/developer.print.html`

   대본은 `/apps/hr/jobs/jobs.print.esp`다음과 같습니다.선택기가 스크립트 이름에 추가됩니다.

* sling:resourceType이 정의되지 않은 경우:

   * 컨텐츠 경로는 적절한 스크립트를 검색하는 데 사용됩니다(경로 기반 ResourceTypeProvider가 활성 상태인 경우).

      예를 들어 에 대한 스크립트에서 검색을 `../content/corporate/jobs/developer.html` 생성했습니다 `/apps/content/corporate/jobs/`.

   * 기본 노드 유형이 사용됩니다.

* 스크립트를 전혀 찾을 수 없으면 기본 스크립트가 사용됩니다.

   기본 변환은 현재 일반 텍스트(.txt), HTML(.html) 및 JSON(.json)으로 지원되며, 이 모두 노드의 속성(적절한 형식)을 나열합니다. 확장 .res에 대한 기본 변환이나 요청 확장자가 없는 요청은 리소스를 스풀(가능한 경우)하는 것입니다.
* http 오류 처리(코드 403 또는 404)의 경우 Sling은 다음 중 하나에서 스크립트를 찾습니다.

   * 사용자 [지정된 스크립트에 대한 위치 /apps/sling/servlet/errorhandler](/help/sites-developing/customizing-errorhandler-pages.md)
   * 또는 표준 스크립트 위치(/libs/sling/servlet/errorhandler/403.esp 또는 404.esp)를 각각 지정합니다.

지정된 요청에 대해 여러 스크립트가 적용되는 경우 가장 일치하는 스크립트가 선택됩니다. 일치 항목이 구체적일수록 더 정확합니다.즉, 요청 확장이나 메서드 이름과 일치하더라도 더 많은 선택기가 더 잘 일치합니다.

예를 들어, 리소스`/content/corporate/jobs/developer.print.a4.html`유형의 리소스에 대한 액세스 요청을 고려해 보십시오`sling:resourceType="hr/jobs"`

다음 스크립트 목록이 올바른 위치에 있다고 가정해 보겠습니다.

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

그런 다음 (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1)의 기본 설정을 선택합니다.

리소스 유형(주로 `sling:resourceType` 속성으로 정의됨) 외에 리소스 슈퍼 유형도 있습니다. 일반적으로 `sling:resourceSuperType` 속성으로 표시됩니다. 이러한 수퍼 유형은 스크립트를 찾으려고 할 때도 고려됩니다. 리소스 슈퍼 유형의 장점은 기본 리소스 유형(기본 서블릿에서 사용)이 `sling/servlet/default` 루트인 리소스 계층을 만들 수 있다는 것입니다.

리소스의 슈퍼 유형은 다음 두 가지 방법으로 정의할 수 있습니다.

* 을 `sling:resourceSuperType` 참조하십시오.
* 를 `sling:resourceSuperType` 사용하여 해당 `sling:resourceType` 노드를 가리킵니다.

예:

* /

   * a
   * b

      * sling:resourceSuperType = a
   * c

      * sling:resourceSuperType = b
   * x

      * sling:resourceType = c
   * y

      * sling:resourceType = c
      * sling:resourceSuperType = a




/x의 유형 계층 구조는 [ c, b, a, &lt;default>] while for /y는 [ c, a,

#### Sling 스크립트를 직접 호출할 수 없습니다. {#sling-scripts-cannot-be-called-directly}

Sling 내에서 스크립트를 직접 호출할 수 없습니다. 이렇게 하면 REST 서버의 엄격한 개념이 깨지기 때문입니다.리소스와 표현을 혼합합니다.

표현(스크립트)을 직접 호출하면 스크립트 내에 리소스를 숨겨 프레임워크(Sling)가 더 이상 이것에 대해 알지 못합니다. 따라서 특정 기능을 잃게 됩니다.

* 다음을 포함하여 GET 이외의 http 메서드 자동 처리

   * 기본 구현을 사용하여 처리되는 POST, PUT, DELETE
   * sling:resourceType 위치의 `POST.jsp` 스크립트

* 귀하의 코드 아키텍처는 더 이상 깨끗하거나 명확하게 구조화되지 않습니다.대규모 개발을 위한 가장 중요한 요소

### Sling API {#sling-api}

Sling API 패키지, org.apache.sling을 사용합니다.&amp;ast; 및 태그 라이브러리.

### sling:include를 사용하여 기존 요소 참조 {#referencing-existing-elements-using-sling-include}

마지막으로 스크립트 내에서 기존 요소를 참조할 필요가 있습니다.

보다 복잡한 스크립트(스크립트 집계)는 여러 리소스(예: 탐색, 사이드바, 바닥글, 목록 요소)에 액세스해야 할 수 있으며 *리소스를*&#x200B;포함시켜야 합니다.

이렇게 하려면 sling:include(&quot;/&lt;path>/&lt;resource>&quot;) 명령을 사용할 수 있습니다. 이렇게 하면 이미지 렌더링에 대한 기존 정의를 참조하는 다음 문에서처럼 참조된 리소스의 정의가 효과적으로 포함됩니다.

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

OSGi는 모듈식 애플리케이션 및 라이브러리를 개발 및 배포하기 위한 아키텍처를 정의합니다(Java용 동적 모듈 시스템이라고도 함). OSGi 컨테이너를 사용하면 애플리케이션을 개별 모듈(추가 메타 정보가 있는 jar 파일 및 OSGi 용어에서 번들이라고 함)로 분류하고 다음 기능을 사용하여 애플리케이션 간의 상호 종속성을 관리할 수 있습니다.

* 컨테이너 내에 구현된 서비스
* 컨테이너와 응용 프로그램 간의 계약

이러한 서비스와 계약은 개별 요소가 협업을 위해 동적으로 서로를 검색할 수 있도록 하는 아키텍처를 제공합니다.

그런 다음 OSGi 프레임워크를 사용하면 다시 시작할 필요 없이 이러한 번들을 동적 로드/언로드, 구성 및 제어할 수 있습니다.

>[!NOTE]
>
>OSGi 기술에 대한 자세한 내용은 OSGi 웹 [사이트를](https://www.osgi.org)참조하십시오.
>
>특히 기본 교육 페이지에는 프레젠테이션과 자습서가 포함되어 있습니다.

이 아키텍처는 애플리케이션별 모듈로 Sling을 확장할 수 있도록 해줍니다. Sling은 OSGI(Open Services Gateway [이니셔티브](https://felix.apache.org/) )의 Apache Felix 구현을 사용하며 OSGi Service Platform 릴리스 4 버전 4.2 사양을 기반으로 합니다. OSGi 프레임워크에서 실행되는 OSGi 번들 모음입니다.

이렇게 하면 설치 내의 패키지에 대해 다음 작업을 수행할 수 있습니다.

* install
* start
* stop
* 업데이트
* uninstall
* 현재 상태 보기
* 특정 번들에 대한 자세한 정보(예: 기호 이름, 버전, 위치 등)에 액세스

자세한 [내용은 웹 콘솔](/help/sites-deploying/web-console.md), [OSGI 구성](/help/sites-deploying/configuring-osgi.md) 및 [OSGi 구성](/help/sites-deploying/osgi-configuration-settings.md) 설정을참조하십시오.

## AEM 환경의 개발 개체 {#development-objects-in-the-aem-environment}

개발에 대한 관심사는 다음과 같습니다.

**항목** 항목은 노드 또는 속성입니다.

항목 개체 조작에 대한 자세한 내용은 javax.jcr. [Item](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html) 인터페이스의 Javadocs를 참조하십시오.

**노드(및 해당 속성)** 노드 및 해당 속성은 JCR API 2.0 사양(JSR 283)에 정의됩니다. 컨텐츠, 객체 정의, 렌더링 스크립트 및 기타 데이터를 저장합니다.

노드는 컨텐츠 구조를 정의하며 해당 속성은 실제 컨텐츠와 메타데이터를 저장합니다.

컨텐츠 노드는 렌더링을 구동합니다. Sling은 들어오는 요청에서 컨텐트 노드를 가져옵니다. 이 노드의 sling:resourceType 속성은 사용할 Sling 렌더링 구성 요소를 가리킵니다.

JCR 이름인 노드를 Sling 환경에서 리소스라고도 합니다.

예를 들어 현재 노드의 속성을 가져오려면 스크립트에서 다음 코드를 사용할 수 있습니다.

`PropertyIterator properties = currentNode.getProperties();`

currentNode가 현재 노드 개체인 경우.

노드 객체 조작에 대한 자세한 내용은 Javadocs를 [참조하십시오](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html).

**위젯** AEM에서 모든 사용자 입력은 위젯에 의해 관리됩니다. 이러한 템플릿은 컨텐츠 일부를 편집하는 데 사용되는 경우가 많습니다.

대화 상자는 위젯을 결합하여 만들어집니다.

AEM은 위젯의 ExtJS 라이브러리를 사용하여 개발되었습니다.

**대화** 상자 대화 상자는 특별한 유형의 위젯입니다.

콘텐츠를 편집하려면 애플리케이션 개발자가 정의한 대화 상자를 사용합니다. 이러한 위젯은 일련의 위젯을 결합하여 사용자에게 관련 컨텐츠를 편집하는 데 필요한 모든 필드와 작업을 제공합니다.

대화 상자는 메타데이터 편집 및 다양한 관리 도구에도 사용됩니다.

**구성 요소** 소프트웨어 구성 요소는 사전 정의된 서비스 또는 이벤트를 제공하고 다른 구성 요소와 통신할 수 있는 시스템 요소입니다.

AEM 내에서 구성 요소는 종종 리소스의 컨텐츠를 렌더링하는 데 사용됩니다. 리소스가 페이지이면, 이를 렌더링하는 구성 요소를 최상위 구성 요소나 페이지 구성 요소라고 합니다. 그러나 구성 요소는 컨텐츠를 렌더링하거나 특정 리소스에 연결할 필요가 없습니다.예를 들어 탐색 구성 요소에는 여러 리소스에 대한 정보가 표시됩니다.

구성 요소의 정의에는 다음이 포함됩니다.

* 컨텐츠를 렌더링하는 데 사용되는 코드
* 사용자 입력에 대한 대화 상자와 결과 컨텐츠의 구성

**템플릿** 템플릿은 특정 유형의 페이지에 대한 기본 템플릿입니다. 웹 사이트 탭에서 페이지를 만들 때 사용자는 템플릿을 선택해야 합니다. 그런 다음 이 템플릿을 복사하여 새 페이지를 만듭니다.

템플릿은 만들 페이지와 동일한 구조를 가지지만 실제 컨텐츠가 없는 노드의 계층입니다.

페이지 및 기본 컨텐츠(기본 최상위 컨텐츠)를 렌더링하는 데 사용되는 페이지 구성 요소를 정의합니다. 컨텐츠는 AEM이 컨텐츠 중심인 것으로 렌더링되는 방식을 정의합니다.

**페이지 구성 요소(최상위 구성 요소)** 페이지를 렌더링하는 데 사용할 구성 요소입니다.

**페이지** A 페이지는 템플릿의 &#39;인스턴스&#39;입니다.

페이지에는 cq:Page 유형의 계층 노드 및 cq:PageContent 유형의 컨텐츠 노드가 있습니다. 컨텐츠 노드의 sling:resourceType 속성은 페이지 렌더링에 사용되는 페이지 구성 요소를 가리킵니다.

예를 들어 현재 페이지의 이름을 가져오려면 스크립트에서 다음 코드를 사용할 수 있습니다.

S`tring pageName = currentPage.getName();`

currentPage가 현재 페이지 개체인 경우. 페이지 개체 조작에 대한 자세한 내용은 Javadocs를 [참조하십시오](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html).

**페이지** 관리자 페이지 관리자는 페이지 수준 작업 방법을 제공하는 인터페이스입니다.

예를 들어 리소스의 포함 페이지를 가져오려면 스크립트에서 다음 코드를 사용할 수 있습니다.

Page myPage = pageManager.getContainingPage(myResource);

pageManager가 페이지 관리자 개체이고 myResource가 리소스 개체인 경우. 페이지 관리자에서 제공하는 방법에 대한 자세한 내용은 Javadocs를 [참조하십시오](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html).

## 저장소 내 구조 {#structure-within-the-repository}

다음 목록은 저장소 내에 표시되는 구조에 대한 개요를 제공합니다.

>[!CAUTION]
>
>이 구조나 그 안에 있는 파일들에 대한 변경 사항은 주의해서 이루어져야 합니다.
>
>개발 중에는 변경 사항이 필요하지만 변경 사항이 미치는 영향을 완전히 이해해야 합니다.

>[!CAUTION]
>
>패스에 있는 것은 변경할 수 `/libs` 없습니다. 구성 및 기타 변경 사항의 경우 항목을 에서 `/libs` 로 복사하고 `/apps` 변경 사항을 `/apps`적용합니다.

* `/apps`

   응용 프로그램 관련;에는 웹 사이트 고유의 구성 요소 정의가 포함되어 있습니다. 개발하는 구성 요소는 에서 사용할 수 있는 기본 구성 요소를 기반으로 할 수 `/libs/foundation/components`있습니다.

* `/content`

   웹 사이트를 위해 만든 콘텐츠

* `/etc`

* `/home`

   사용자 및 그룹 정보.

* `/libs`

   AEM의 핵심에 속하는 라이브러리 및 정의 의 하위 폴더는 검색 또는 복제와 같은 기본 AEM 기능을 `/libs` 나타냅니다. AEM 작동 방식에 영향을 주므로 의 컨텐츠를 수정할 `/libs` 수 없습니다. 웹 사이트 전용 기능은 에서 개발해야 합니다 `/apps` (구성 요소 및 기타 [요소 사용자 정의 참조](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

* `/tmp`

   임시 작업 영역.

* `/var`

   시스템에 의해 변경 및 업데이트되는 파일감사 로그, 통계, 이벤트 처리 등 하위 폴더에는 구성 요소 스크립트에서 생성된 소스 및 컴파일된 양식의 java 서블릿이 `/var/classes` 포함되어 있습니다.

## 환경 {#environments}

AEM을 사용하면 제작 환경은 종종 두 가지 유형의 인스턴스로 구성됩니다.작성자 [및 게시 인스턴스](/help/sites-deploying/deploy.md#author-and-publish-installs).

## 디스패처 {#the-dispatcher}

Dispatcher는 캐싱 및/또는 로드 밸런싱 모두를 위한 Adobe의 툴입니다. 자세한 내용은 디스패처 아래에 [있습니다](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html).

## FileVault(소스 개정 시스템) {#filevault-source-revision-system}

FileVault는 JCR 저장소에 파일 시스템 매핑 및 버전 제어를 제공합니다. 표준 버전 제어 시스템(예: Subversion)에서 프로젝트 코드, 컨텐츠, 구성 등의 저장 및 버전 관리를 완벽하게 지원하여 AEM 개발 프로젝트를 관리하는 데 사용할 수 있습니다.

자세한 내용은 [FileVault 도구](/help/sites-developing/ht-vlttool.md) 설명서를 참조하십시오.

## 워크플로우 {#workflows}

컨텐츠는 다양한 참가자의 승인 및 로그인과 같은 단계를 포함하여 조직 프로세스에 따르는 경우가 많습니다. 이러한 프로세스는 AEM 내에서 [정의 및 개발된 워크플로우로](/help/sites-developing/workflows-models.md)표현된 다음 [해당 컨텐츠 페이지](/help/sites-administering/workflows.md) 또는 [디지털 자산에](/help/assets/assets-workflow.md) 필요에 따라 적용할 수 있습니다.

워크플로우 엔진은 워크플로우의 구현과 컨텐츠에 대한 후속 애플리케이션을 관리하는 데 사용됩니다.

## Multi-Site Management {#multi-site-management}

MSM(Multi Site Manager)을 사용하면 일반적인 컨텐츠를 공유하는 여러 웹 사이트를 손쉽게 관리할 수 있습니다. MSM을 사용하면 한 사이트의 컨텐츠 변경 사항이 다른 사이트에서 자동으로 복제되도록 사이트 간의 관계를 정의할 수 있습니다.

예를 들어, 웹 사이트는 국제 고객을 위해 여러 언어로 제공되는 경우가 많습니다. 동일한 언어의 사이트 수가 낮으면(3~5개) 사이트 간에 컨텐츠를 동기화하는 수동 프로세스가 가능합니다. 그러나 사이트 수가 증가하거나 다국어 지원 시 프로세스를 자동화하는 것이 더 효율적입니다.

* 웹 사이트의 다양한 언어 버전을 효율적으로 관리할 수 있습니다.
* 소스 사이트를 기반으로 하나 이상의 사이트를 자동으로 업데이트합니다.

   * 공통 기본 구조를 적용하고 여러 사이트에서 일반적인 컨텐츠를 사용할 수 있습니다.
   * 사용 가능한 리소스의 사용을 최대화합니다.
   * 일반적인 모양과 느낌을 유지할 수 있습니다.
   * 사이트 간에 다른 컨텐츠를 관리하는 데 집중할 수 있습니다.

자세한 내용은 다중 사이트 [관리자를 참조하십시오](/help/sites-administering/msm.md).