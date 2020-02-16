---
title: 통합 문제 해결
seo-title: 통합 문제 해결
description: 통합 문제를 해결하는 방법을 알아봅니다.
seo-description: 통합 문제를 해결하는 방법을 알아봅니다.
uuid: fe080e58-a855-4308-a611-f72eb47ba82d
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 422ee332-23ae-46bd-8394-a4e0915beaa2
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# 통합 문제 해결{#troubleshooting-integration-issues}

## 일반 문제 해결 팁 {#general-troubleshooting-tips}

### JavaScript 오류가 없는지 확인 {#ensure-there-are-no-javascript-errors}

브라우저의 JavaScript 콘솔에 오류가 표시되는지 확인합니다. 처리되지 않은 오류로 인해 후속 코드가 제대로 실행되지 않을 수 있습니다. 오류가 있는 경우 오류를 일으키는 스크립트와 어떤 영역을 사용하는지 확인하십시오. 스크립트 경로는 스크립트가 속한 기능에 대해 나타낼 수 있습니다.

### 구성 요소 수준에서 로깅 {#logging-on-component-level}

경우에 따라 구성 요소 수준에 다른 문을 추가하는 것이 유용할 수 있습니다. 구성 요소가 렌더링되므로 임시 마크업을 추가하여 잠재적 문제를 식별하는 데 도움이 되는 변수 값을 표시할 수 있습니다. 예:

```
<%
log.info("myVariable={}", myVariable);
%>

<!--
<%= myJspVariable %>
-->

<!--
${ myHtlVariable }
-->
```

로깅에 대한 자세한 내용은 로깅 및 [감사 기록](/help/sites-deploying/configure-logging.md) 및 [로그 파일 작업을](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) 참조하십시오.

## Analytics 통합 문제 {#analytics-integration-issues}

### 보고서 가져오기로 인해 CPU/메모리 사용량이 높음 {#the-report-importer-causes-high-cpu-memory-usage}

보고서 가져오기로 인해 CPU/메모리 사용량이 높거나 `OutOfMemoryError` 예외가 발생합니다.

#### 솔루션 {#solution}

이 문제를 해결하려면 다음을 시도해 보십시오.

* 등록된 많은 수의 PollingImporter가 없는지 확인합니다(아래 &quot;PollingImporter로 인해 시스템 종료에 시간이 오래 걸립니다&quot; 섹션 참조).
* OSGi 콘솔의 `ManagedPollingImporter` 구성에 대해 CRON 표현식을 사용하여 특정 시간에 보고서 [가져오기를 실행합니다](/help/sites-deploying/configuring-osgi.md).

AEM에서 사용자 지정 데이터 가져오기 서비스를 만드는 방법에 대한 자세한 내용은 https://helpx.adobe.com/experience-manager/using/polling.html [문서를 참조하십시오](https://helpx.adobe.com/experience-manager/using/polling.html).

### PollingImporter로 인해 종료에 오랜 시간이 걸립니다. {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

Analytics는 상속 메커니즘을 고려하여 설계되었습니다. 일반적으로 페이지 속성 클라우드 서비스 탭 내에서 Analytics 구성에 대한 참조를 추가하여 사이트에 대한 Analytics [를](/help/sites-developing/extending-cloud-config.md) 활성화합니다. 그런 다음 다른 구성이 필요하지 않은 경우 구성을 다시 참조할 필요 없이 모든 하위 페이지에 자동으로 상속됩니다. 사이트에 참조를 추가하면 Analytics 데이터를 AEM으로 가져오는 데 사용되는 PollingImporter를 인스턴스화하는 유형의 노드(AEM 6.3 및 이전 버전의 경우 12 또는 AEM 6.4 이상의 경우 6) `cq;PollConfig` 가 자동으로 만들어집니다. 그 결과:

* Analytics를 참조하는 페이지가 많으면 많은 PollingImporter가 발생합니다.
* 또한 Analytics 구성에 대한 참조를 사용하여 페이지를 복사하고 붙여넣으면 PollingImporter가 중복됩니다.

#### 솔루션 {#solution-1}

먼저, [error.log](/help/sites-deploying/configure-logging.md) 를 분석하면 활성 또는 등록된 PollingImporter의 양에 대한 통찰력을 얻을 수 있습니다. 예:

```
# Count PollingImporter entries
$ sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\),interval.*/\1/p" error.log | wc -l
86415
# Count PollingImporter entries for last30days
$ sed -n "s/.*(aem-analytics-integration-last30Days).*target=\(.*\),interval.*/\1/p" error.log | wc -l
14531
# Count unique paths of PollingImporter registrations
sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\)\/jcr:content.*/\1/p" error.log | sort | uniq -c
28115
```

둘째, 상위 페이지(계층 구조 높음)만 Analytics 구성을 참조하도록 하십시오.

AEM에서 사용자 지정 데이터 가져오기 서비스를 만드는 방법에 대한 자세한 내용은 https://helpx.adobe.com/experience-manager/using/polling.html [문서를 참조하십시오](https://helpx.adobe.com/experience-manager/using/polling.html).

## DTM(기존) 문제 {#dtm-legacy-issues}

### DTM 스크립트 태그가 페이지 소스에서 렌더링되지 않음 {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

DTM [스크립트](/help/sites-administering/dtm.md) 태그가 페이지 속성 서비스 탭에서 구성을 참조했지만 페이지에 제대로 [포함되지](/help/sites-developing/extending-cloud-config.md) 않습니다.

#### 솔루션 {#solution-2}

문제를 해결하려면 다음을 시도해 보십시오.

* 암호화된 속성의 암호를 해독할 수 있는지 확인합니다. 암호화는 각 AEM 인스턴스에서 자동으로 생성된 다른 키를 사용할 수 있습니다. 자세한 내용은 구성 속성에 [대한 암호화 지원을 참조하십시오](/help/sites-administering/encryption-support-for-configuration-properties.md).
* 에 있는 구성 다시 게시 `/etc/cloudservices/dynamictagmanagement`
* ACL을 `/etc/cloudservices`확인합니다. ACL은 다음과 같아야 합니다.

   * allow;jcr:read;webservice-support-servicelibfinder
   * allow;jcr:read;everyonerep:glob:&amp;ast;/defaults/&amp;ast;
   * allow;jcr:read;everyonerep:glob:&amp;ast;/defaults
   * allow;jcr:read;everyonerep:glob:&amp;ast;/public/&amp;ast;
   * allow;jcr:read;everyonerep:glob:&amp;ast;/public

ACL 관리에 대한 자세한 내용은 사용자 관리 [및 보안 페이지를](/help/sites-administering/security.md#permissions-in-aem) 참조하십시오.

## Target 통합 문제 {#target-integration-issues}

### 사용자 지정 페이지 구성 요소를 사용할 때 미리 보기 모드에서 타깃팅된 컨텐츠가 표시되지 않음 {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

이 문제는 사용자 지정 페이지 구성 요소에 Target DTM 통합을 처리하는 올바른 JSP 또는 클라이언트 라이브러리가 포함되어 있지 않기 때문에 발생합니다.

#### 솔루션 {#solution-3}

다음 솔루션을 사용해 볼 수 있습니다.

* 사용자 지정( `headlibs.jsp` 있는 경우)에 `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`다음이 포함되어 있는지 확인합니다.

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* 사용자 지정(있는 경우) `head.html` 에 아래 예와 같은 특정 통합 헤딩이 선택적으로 포함되지 `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`**** 않았는지 확인합니다.

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

에서는 필요한 분석 JavaScript 개체를 `servicelibs.jsp` 추가하고 웹 사이트와 연결된 클라우드 서비스 라이브러리를 로드합니다. Target 서비스의 경우 라이브러리는 `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

로드되는 라이브러리 집합은 Target 구성에 사용되는 대상 클라이언트 라이브러리( `mbox.js` 또는 `at.js`)의 유형에 따라 다릅니다.

DTM을 사용하여 컨텐츠를 렌더링하기 전에 라이브러리를 `mbox.js` 제공하거나 로드했는지 `at.js` 확인합니다. 이러한 라이브러리를 비동기적으로 로드하는 태그 관리 시스템을 사용하면 대상 특정 JavaScript 코드를 실행할 때 문제가 발생할 수 있습니다.

자세한 내용은 타깃팅된 컨텐츠를 [위한 개발 페이지를](/help/sites-developing/target.md#understanding-the-target-component) 참조하십시오.

### 브라우저 콘솔에 &quot;AppMeasurement 초기화에 보고서 세트 ID 누락&quot; 오류가 표시됩니다 {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

이 문제는 Adobe Analytics가 DTM 파섹 원인은 를 사용하여 `s = new AppMeasurement()` `s` 객체를 인스턴스화합니다.

#### 솔루션 {#solution-4}

인스턴스화 방법 `s_gi` 대신 `new AppMeasurement` 사용합니다. 예:

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### 올바른 오퍼 대신 임의로 표시되는 기본 오퍼 {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

이 문제에는 여러 가지 원인이 있을 수 있습니다.

* 타사 태그 관리 시스템을 사용하여 Target 클라이언트 라이브러리( `mbox.js` 또는 `at.js`)를 비동기식으로 로드하면 임의로 타깃팅을 중단할 수 있습니다. Target 라이브러리는 페이지 헤드에 동기식으로 로드되어야 합니다. 라이브러리는 AEM에서 제공되면 항상 적용됩니다.

* 두 개의 Target 클라이언트 라이브러리( `at.js`)를 동시에 로드합니다(예: DTM을 사용하는 라이브러리 및 AEM의 Target 구성을 사용하는 라이브러리). 따라서 버전이 다른 경우 `adobe.target` 정의에 충돌이 발생할 `at.js` 수 있습니다.

#### 솔루션 {#solution-5}

다음 솔루션을 사용해 볼 수 있습니다.

* DTM과 같은 라이브러리를 로드하는 고객 코드(Target 라이브러리를 차례로 로드하는)가 [페이지 헤드에서](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages)동기식으로 실행되는지 확인하십시오.
* dtm을 사용하여 Target 라이브러리를 제공하도록 사이트가 구성된 경우 DTM을 통해 **전달되는 Clientlib** 옵션이 [사이트의 Target 구성에서](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html) 체크인되었는지 확인합니다.

### AT.js 1.3+를 사용할 때는 항상 올바른 오퍼 대신 기본 오퍼가 표시됩니다 {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

기본적으로 AEM 6.2 및 6.3은 AT.js 버전 1.3.0+와 호환되지 않습니다. AT.js 버전 1.3.0에서는 API에 대한 매개 변수 유효성 검사를 도입하므로 `adobe.target.applyOffer()` 코드에 의해 제공되지 않는 &quot;mbox&quot; 매개 변수가 `atjs-itegration.js` 필요합니다.

#### 솔루션 {#solution-6}

이 문제를 해결하려면 다음과 `atjs-itegration.js` 같이 매개 변수 개체에 `"mbox": mboxName` `adobe.target.applyOffer()` 필드를 편집하고 추가합니다.

```
adobe.target.getOffer({
    "mbox": mboxName,
    "params": params,
    "success": function (response) {
        adobe.target.applyOffer({
            "mbox": mboxName, //<--- ADDED PARAM
            "selector": "#" + mboxName,
            "offer": response
        })
    },
```

### 목표 및 설정 페이지에는 보고 소스 섹션이 표시되지 않습니다. {#the-goals-settings-page-does-not-show-the-reporting-sources-section}

이 문제는 A4T Analytics [Cloud 구성 프로비저닝](/help/sites-administering/target-configuring.md) 문제입니다.

#### 솔루션 {#solution-7}

AEM에 다음 확인 요청을 실행하여 A4T가 Target 계정에 대해 제대로 활성화되었는지 확인해야 합니다.

```
http://localhost:4502/etc/cloudservices/testandtarget/<YOUR-CONFIG>/jcr:content.a4t.json

{
    "a4tEnabled": true,
    "sharedsecret": "SECRET",
    "proxyUrl": "/libs/cq/contentinsight/content/proxy.reportingservices.json",
    "active": "true",
    "pageName": "",
    "url": "https://api5.omniture.com/rs/0.5/",
    "username": "USER@DOMAIN"
}
```

응답에 라인이 포함된 `a4tEnabled:false`경우 Adobe 고객 [지원 센터에](https://helpx.adobe.com/contact.html) 문의하여 계정을 올바르게 프로비저닝하십시오.

### 유용한 타겟 API {#helpful-target-apis}

아래 제시된 두 개의 Target API는 Target 문제를 해결할 때 유용할 수 있습니다.

* 지정된 클라이언트 코드의 대상 끝점 검색

```
https://admin.testandtarget.omniture.com/rest/v1/endpoint/<CLIENTCODE>.json

{"api":"https://admin<N>.testandtarget.omniture.com/admin/rest/v1"}
```

* 클라이언트의 프로파일 검색

```
https://admin<N>.testandtarget.omniture.com/admin/rest/v1/clients/<CLIENT>?email=<EMAIL>&password=<PASSWORD>

Response for N=4, CLIENT-dayintegrationintern
{
    "clientCode": "dayintegrationintern",
    "companyName": "Day Integration - Internal",
    "omnitureCompanyId": "Day Integration Internal",
    "softTraxId": -1,
    "address1": "XYZ",
    "city": "San Francisco",
    "state": "ca",
    "zip": "94107",
    "country": "UNITED STATES",
    "locale": "de_DE",
    "timeZone": "Europe/Berlin",
    "phone": "XX-XX-XXXX",
    "serviceLevel": "Up to 100,000",
    "privileges": [
        "a4t",
        "hosts",
        "TnT-SC-integration",
        "mvt",
        "steps",
        "testing-campaigns",
        "view-snapshot",
        "on-site-editor",
        "optimizing-campaign",
        "third-party-id-support",
        "landing-page-campaigns",
        "segment",
        "rest-create-user",
        "advanced-targeting",
        "mobile-device-targeting",
        "beta",
        "geolocation"
    ]
}
```

